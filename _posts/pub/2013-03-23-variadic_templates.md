---
title: "C++11 variadic templates, for the doubters."
layout: post
---

One of the simple pleasures of working at facebook is that, because we fully control the deployment environments, I've been using gcc 4.7 for awhile. That means we get to seriously embrace C++11.

A variadic template, for those that don't know, is a C++ template that takes an arbitrary numbers of types. If you are an experienced C++ programmer, this might seem useful, or intriguing. This post probably isn't for you. If this terrifies you, read on.

Another simple pleasure is that I get to work with many non-C++ programmers. Some never use it, some occasionally. Almost all have opinions, though. Something about variadic templates causes anti-C++ sentiments, amongst journeymen and apostates alike, to crystallize.

My goal here is simply to motivate and give a quick tour of places where variadic templates are extremely useful, both in our codebase, and in the standard itself. For the doubters. Some of the patterns here are almost certain to show up in any non-trivial codebase. Some are already standardized, and I'll hit on those as we go.

## Variadic Templated Objects

It's pretty easy to come up with a use for an object that accepts a list of types. The standard provides `std::tuple`:

    std::tuple<int, float, string> bob = {1, 12.0, "hello"};

You can also imagine implementing the algebraic cousin to the typesafe tuple, the typesafe union, in a similar fashion. Check out: [`folly::DiscriminatedPtr`](https://github.com/facebook/folly/blob/master/folly/DiscriminatedPtr.h) which is a very space-optimized, typesafe union of pointers. (An astute reader would point out that `boost::variant` fits into this class of objects as well. It's conceivable that you could implement `boost::variant` as a variadic template, but there are, in my understanding, a bunch of implementation details that make this tricky. I'll dodge the issue entirely. This post is already going to be long.)

While easily motivated, example implementations here are long, if not a bit complex, revolving mostly around compile-time recursion. If you are interested, check out [this talk by Andrei Alexandrescu](http://www.youtube.com/watch?v=_zgq6_zFNGY) where he goes through variadic templates, and `std::tuple` in detail.

## Variadic Functions, now with safety

The other place where variadic templates can be used is to implement typesafe variadic functions. There aren't many variadic functions around, and they are often actively discouraged.  The most famous, though is `printf` (and all of his associated friends). Variadic templates gives us the opportunity to create typesafe `printf`. That is to say a version of printf that ensures the parameters to the function match the types specified in the format specifier. Again, I'm going to skate on by, but if you want details, see the talk above.

Here's another example stolen from `facebook::folly`:

	namespace folly {

	  template <typename T, typename... Ts>
	  size_t hash_combine(const T& t, const Ts&... ts) {
	    size_t seed = std::hash<T>()(t);
	    if (sizeof...(ts) == 0) {
	      return seed;
	    }	  
	    size_t remainder = hash_combine(ts...);   // not recursion!
	    return hash_128_to_64(seed, remainder);
	  }
	} //namespace

	// Simple example
	struct Obj {
	  int x;
	  string y;
	  float z;

	  size_t hash() const { return folly::hash_combine(x,y,z); }
	};


Note that `folly::hash_combine` is completely typesafe. It will only hash types that have a `std::hash` specialization, and if you try to pass a type that doesn't have such a specialization, it will fail to compile.

## The other great, hidden, variadic function

There is another widespread variadic function that is quite a bit more subtle. I would go as far as saying its existence has been haunting C++ for a long time. It's only now, with variadic templates, that we are able to fully come to terms with it. The greatest variadic function of them all is the lowly constructor.

Given an arbitrary type `T`, the constructor is a "variadic function". The copy constructor is well defined for T, but not the constructor. This has been a plague on templates since their introduction. Templates, unable to deal with constructors that take an unknown number of parameters of unknown types, have implemented various workarounds often resulting in reduced efficiency. Put another way, **templates can happily copy objects on your behalf, but they could never easily create objects on your behalf.**

### `Container<T>` ###

Containers, arguably the preeminent use of templates, have suffered from this issue for a long time. **Containers often want to create objects HOW you want, but WHERE they want.** Container templates have worked around this problem in two ways 1) use the default constructor and then give you access to modify it, or 2) let you construct the object, and then copy it to the correct location.

	vector<Obj> o;
	Obj obj(param1, param2); // I construct it the way I want...
	o.push_back(obj);        // ... and you copy it into the place you want it


	map<int, Obj> map;
	map[1] = Obj(param1, param2);  // DEFAULT construct, then operator=


What you'd like to be able to do is give the container the parameters it needs and have it construct the object where it wants, but the way you want it...

	vector<Obj> o;
	o.emplace_back(param1, param2); // doesn't take Obj, takes parameters to MAKE an Obj

This problem is now largely resolved by the introduction of the `emplace` family of container methods. `Emplace` is a variadic function that simply forwards any parameters you pass it to the constructor of the correct type. This allows you to give a container everything it needs to construct your object, and it will do so using the construction you want, but putting the object where it wants.

No copies, no moves.

## Creating objects on your behalf ##

Any template that creates objects on your behalf is likely to benefit from variadic templates due to the fact that these functions can now be parameterized to call any constructor on that object. This will be all but required for containers. But it is also true for any attempt to generalize logic around object construction. It's actually pretty easy to come up with situations where wrapping construction in some logic makes code better. The standard gives us one:

	std::shared_ptr<Obj> sharedObj = std::make_shared<Obj>(param1, param2);
	auto uniqObj = make_unique<Obj>(param1, params2);        // not std yet :(


There is no `std::make_unique`... yet. But it's easy enough to implement using a variadic template. 

Another idea (whether or not it is a -good- idea is probably arguable): a simple caching framework. Given a certain implemented interface for a type, it's construction/caching can be abstracted away. If the object exists in some cache (in memory, memcache, whatever), construct by deserializing from the cache, otherwise do the specified (presumably expensive) constructor and set the resulting serialized value into the cache for next time. 

### An Arena Allocator ###

[`folly::Arena`](https://github.com/facebook/folly/blob/master/folly/Arena.h) is an arena allocator. Arena allocators can be summarized with a simple line of code:

<pre>
void deallocate(void* p) {
    // Deallocate? Never!
  }
</pre>

An arena simply allocates memory in a never-ending forward fashion. It ignores all attempts to deallocate until it's destroyed, when all of its memory is freed at once. Arenas are extremely useful for servers and other per-request models because you can often avoid almost all memory overhead during the latency-inducing formation of the response, and then free up all memory, easily and quickly, once the response is gone.

How would you construct an arbitrary object inside this arena? Make `arenaNew`? Before C++11 this would be ugly. Now, it's relatively easy.


	template <typename T, typename ...Args>
	T* arenaNew(folly::SysArena* arena, Args&&... params) {
	   auto mem = arena->allocate(sizeof(T));
	   return new (mem) T(std::forward<Args>(params)...);
	}

	void f() {
	  folly::SysArena arena;
	  auto ptr = arenaNew<Obj>(&arena, param1, param2); 
	  // ...
	}

Warning: this code is a bit incomplete, because it's only "safe" for types with trivial destructors (and woe be to the unwitting programmer who `delete`s one of these pointers).

The syntax is new, and perhaps strange, but the concept is pretty simple. We pass in the arena we want to use, and the params to use on the constructor of `T`. We allocate the memory we need from the arena, and then construct T using placement new, forwarding the parameters into the constructor.

### tldr ###

Variadic templates fill a surprisingly frequent need in generic C++ code. Some places where variadic templates are likely to be useful:

* Specialized tuples and unions. Functions that operator on them generically.
* Typesafe variadic functions
* Templates that want to construct objects on your behalf (including containers)

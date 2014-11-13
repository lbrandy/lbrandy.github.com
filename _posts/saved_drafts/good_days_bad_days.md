A fundemental theory of programming language arguments

I give the C++ onboarding to new hires at Facebook. At the start of every class I have a slide that reads simply "why C++" and start a discussion. (note: this is actually a tactical to move to -force- programming language arguments to the front so I can get through the rest of the talk safely).

Asking this question to a roomful of all new hires has been a very enlightening cross section of programmer opinion, from dyed in the wool C++ fans, to apostates fallen from grace, to newcomers who've heard rumors. Different rooms have different personalities. Pro: Speed. Con: Templates error messages lol, just use C. Con: People are faster than machines, let's use python and 'drop down into C when we need speed". Pro: Garbage collection succcckkkkkksssss. Con: Object orientation is all about mutable state and mutability is the root of all evil.

I often observe a fairly fundamental axiomatic difference that frequently drives these conversation straight off the cliff. 

## Let me make some absurdly reductionist claims. 

In any given programming language (or technology), there are exactly two kinds of programmers: the **language expert** and the **language non-expert**. I'm using a fairly high bar for "expert" throughout this post. Just to be clear, non-experts are not just newbies, but even the rank and file professionals who don't bother to get very language lawyerly. Experts solve the hardest problems in a codebase. In the C++ world, you'll often hear the dog-whistle codeword "library writers" to refer to "experts". 

All programmers in a language, expert or not, have **good days** and **bad days**. Please note, the actual unit of time is irrelevant (we might also say good lines of code, and bad lines of code). FWIW, I've carefully chosen units of time instead of the skill of programmers. Very often "in the wild" these exact arguments are framed as "good vs bad" programmers which poisons shit beyond belief (and often heads into comical strawmen).

A **good day** is stronger than just writing bug free code. Your design is solid, your code is as idiomatic as it can be, utilizating everything the language provides, as well as being totally bug free. A **bad day** is, of course, when any of these things start to slip.

## A 2x2 matrix

So there are 4 situations where any of us might find ourselves in on a given day:

1. **Non-expert, and having a bad day**. You might be a newbie, and you are writing code you don't really understand, and bugs you definitely don't. Or you might be relatively experienced and writing a bug you'll find later when everything crashes. In this zone, a programming language is being judged by its documentation, tutorials, traps, error messages, and the kinds of simple bugs "possible". 
2. **Non-expert, and having a good day**. You are writing code as correct, idiomatic as you can. You don't know enough to make it -perfect- so it's probably not optimal in some (likely very unimportant) way, but it's going to work plenty good enough. This is the productivity square where the vast majority of business value is created every day. In this zone, a programming language is being judged on how productive it makes the majority of the people who use it.
3. **Expert, and having a bad day**. You are writing the most important code in the project and you are screwing it up. Your either making a bad design that we'll spend months fixing later, or you're doing something and you should *clearly* know better. You're going to be mad at yourself later. In this zone, a programming language is going to be judged by it's entire tooling ecosystem, all of its ability to prevent bugs and make debugging easier, and all the tools it has to fix huge messes (refactoring, debuggers, etc.) When the language is running close to its limit, with all of its features coming together, how forgiving is it? How much can it protect us? 
4. **Expert, and having a good day**. You are writing the most important piece of logic in a billion dollar program. It's critical that this code is perfect (for some definition, often involving speed, or correctnes, or both). Your design is right. No bugs, of course. You changed the course of an entire company today, maybe an industry. You go home by 5pm. In this zone, a programming language is essentially being judged at what's the best possible outcome. What is the limit on the types of programs this language can produce.

Here's my central claim: **essentially all programming language arguments that go sideways do so because two people are talking about (or, often, fundamentally valuing) different sections of this matrix.**

## Some examples 

**static vs dynamic typing**. This one is a bit more complicated than a paragraph can allow so let's see how I do. Many arguments in favor of dynamic typing sit squarely in the producitivity category (inexperienced programmers having good days) where huge amounts of business value can be created relatively easy. Most static typing arguments are talking about the other three squares. Namely, 1) on your bad days, the compiler can help alot more and 2) dynamic typing limits the best-possible-program in ways that are unacceptable. 

**Garbage collection**. Pro-gc arguments will typically argue that it greatly improves correctness and minimizes a huge class of really awful bugs (covering the bad days much better). All of this is a huge boost to productivity (our non-expert, good days zone). Essentially every argument against garbage collection comes from the "good day" side of the equation. If latency matters, garbage collection ends up putting limits on your program that experts, and even non-experts, could likely manually manage in a better way. All of the productivity gains dissapear as you enter a death struggle with the GC, and moreover your expert programmers are far more limited in what they can accomplish. 

**Haskell**. Haskell has this huge, principled and sophisticated type system. The treatment of inexperienced & experienced engineers on their bad days is very different. Newbies get brutalized but experienced engineers get -tremendous- value. ("oh! duh! it's just that old monomorphism restriction.. I'm such a newb").

**C++**. Essentially every argument against C++ focuses on the bad days. It doesn't protect you at all. Template error messages. Huge complexity that you constantly need to hold in your head. There's no one, including its supporters, that can say C++ is as good as it could be for those bad days. That said, essentially every defense of C++ is focused on those good days. They can all be essentially boiled down into: "once I get this right, my code will be at least one of faster, more generic, and safer than language X can ever reasonably produce". By safer, here, remembnering my code is perfect, I mean abstractions that are harder to misuse. For example, this is essentially the argument C++ programmers and those associated domains make against garbage collected languages.  

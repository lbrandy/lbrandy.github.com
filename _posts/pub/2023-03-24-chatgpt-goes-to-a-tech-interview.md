---
title: "ChatGPT goes to a tech interview"
date: '2023-03-24'
description:
categories:
tags: []

layout: post
type: draft
---

# ok, another interview phone-screen. let's do this.

_Hey ChatGPT, welcome to our interview. Today we're going to do a bit of coding. I'll leave time at the end for questions from you to me. Are you ready? Great. Can you write me code to validate whether a list of binary tree nodes forms exactly one valid binary tree?_

> Sure, here's an example code in Python to validate if a list of binary tree nodes forms exactly one valid tree:

```
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
 
def validate_tree(nodes):
    # Creating a dictionary with key as the node value and value as the TreeNode object
    node_dict = {node['val']: TreeNode(node['val']) for node in nodes}
 
    # Iterating through the list of nodes to create the tree structure using parent-child relationships
    for node in nodes:
        # Getting the node object
        parent_node = node_dict[node['val']]
        # Getting the left child node object
        if node['left'] is not None:
            left_child = node_dict[node['left']]
            parent_node.left = left_child
        # Getting the right child node object
        if node['right'] is not None:
            right_child = node_dict[node['right']]
            parent_node.right = right_child
 
    # Counting the number of root nodes 
    roots = 0
    for node in node_dict.values():
        if not node.left and not node.right:
            roots += 1
        elif (node.left and not node.right) or (not node.left and node.right):
            return False
 
    # Validating that only one root node is present in the tree
    return roots == 1
```

> The validate_tree function takes a list of nodes, each node represented as a dictionary with the keys val , left , and right , where val is the node value and left and right are the values of the left and right child nodes respectively.
 
> The function first creates a dictionary with the node values as the keys and the corresponding TreeNode objects as the values. It then iterates through the input list of nodes to create the tree structure using parent-child relationships.
 
> After the tree structure is created, the function counts the number of root nodes present in the tree. A node is considered to be a root node if it has no children. If a node has only one child or has two children, it cannot be a root node. Finally, the function validates whether there is only one root node present in the tree, and returns True if it is valid, and False otherwise.
 
> Note that this function assumes that the input list of nodes represents a valid binary tree, i.e., there are no loops in the tree structure and each node has at most two children.

# follow-up question!

_(okokokokok, I'm a smart human, so let's ask a followup question to catch any cheaters!) So, then, ChatGPT, can you write me a unit test that tests the code you just wrote?_

> Sure, here's an example unit test in Python using the built-in unittest module:


```
import unittest
 
class TestValidateTree(unittest.TestCase):
    def test_valid_tree(self):
        # Valid tree with 1 as root and 2 and 3 as children
        nodes = [{'val': 1, 'left': 2, 'right': 3}, {'val': 2, 'left': None, 'right': None}, {'val': 3, 'left': None, 'right': None}]
        self.assertTrue(validate_tree(nodes))
 
        # Valid tree with 5 as root and 2 and 7 as children
        nodes = [{'val': 5, 'left': 2, 'right': 7}, {'val': 2, 'left': None, 'right': None}, {'val': 7, 'left': None, 'right': None}]
        self.assertTrue(validate_tree(nodes))
 
    def test_invalid_tree(self):
        # Invalid tree with two root nodes
        nodes = [{'val': 1, 'left': None, 'right': None}, {'val': 2, 'left': None, 'right': None}, {'val': 3, 'left': None, 'right': None}]
        self.assertFalse(validate_tree(nodes))
 
        # Invalid tree with a node having two children, but no parent
        nodes = [{'val': 1, 'left': None, 'right': 2}, {'val': 3, 'left': None, 'right': None}, {'val': 2, 'left': 4, 'right': 5},
                 {'val': 4, 'left': None, 'right': None}, {'val': 5, 'left': None, 'right': None}]
        self.assertFalse(validate_tree(nodes))
 
        # Invalid tree with a node having only one child, but no parent
        nodes = [{'val': 1, 'left': None, 'right': 2}, {'val': 3, 'left': None, 'right': None}, {'val': 2, 'left': None, 'right': None},
                 {'val': 4, 'left': None, 'right': None}]
        self.assertFalse(validate_tree(nodes))
 
if __name__ == '__main__':
    unittest.main()
```

> The validate_tree function takes a list of nodes, each node represented as a dictionary with the keys val , left , and right , where val is the node value and left and right are the values of the left and right child nodes respectively.
 
> The function first creates a dictionary with the node values as the keys and the corresponding TreeNode objects as the values. It then iterates through the input list of nodes to create the tree structure using parent-child relationships.
 
> After the tree structure is created, the function counts the number of root nodes present in the tree. A node is considered to be a root node if it has no children. If a node has only one child or has two children, it cannot be a root node. Finally, the function validates whether there is only one root node present in the tree, and returns True if it is valid, and False otherwise.
 
> Note that this function assumes that the input list of nodes represents a valid binary tree, i.e., there are no loops in the tree structure and each node has at most two children.

# whoa (editor's comment)

So, the above was presented without (much) comment. It represented a very simple question/response from me to chatgpt (using [chat-gpt.com](http://chat-gpt.com)). The intention is to show what the very near future of a conventional "tech interview" might look like in our collectively brave new world.

The two questions asked to ChatGPT were:

1. Can you write me code to validate whether a list of binary tree nodes forms exactly one valid tree?
2. Can you write a unit test to test the code you just wrote?

Actual pastebin of the interchange:

* [https://pastebin.com/tYbuaJhE](https://pastebin.com/tYbuaJhE)
* [https://pastebin.com/dLv3ecjn](https://pastebin.com/dLv3ecjn)


# some commentary

First, if you look closely at the code, or the test, it's not _great_, or ideal... but holy cow does it _look_ legit at a glance. I think careful inspection of the code will reveal problems and edge cases not properly handled, but... still... wow.

Second, I'm genuinely alarmed by the seemingly plausible follow-up answer. It just looks shockingly good before I examine the details. In my own mind I somewhat expected ChatGPT to regurgitate a half-decent answer to a conventional "coding" question. I did _not_ expect it to produce a half-sensible answer to followup questions. 

Last, one of my long-held beliefs is that human interviewers for these kind of "coding" interviews _vastly_ overrate their ability to detect "preparedness", "cache hits" or, worse, cheaters. My guess is that many, many, many interviewers are fooled by people actively cheating or who have actively prepared an answer to their "known" leetcode question. Many interviewers, IMO mistakenly, believe that they can suss out such things with their clever followups. I am not convinced. There's a much longer discussion to be had here about what this implies when we consider the value of coding interviews, overall. 

# epilogue

I've not written here in a long, long, long time. In the interim, I spent ~10 years at Facebook and did hundreds of interviews (and have the t-shirt to prove it) and was part of the candidate review board that made final hire/no-hire decisions for I-don't-even-know-how-many written packets of conducted interview loops. I've since left FB at work at [Rockset](http://www.rockset.com) now, working on realtime analytics database.

I consider myself relatively well-calibrated on what a "big tech" interview might look like. And well-calibrated on how a "coding interview" looks when presented to someone downstream who is glancing at them to make final hire, no-hire decisions. 

I present the above simply so you can take my opinion for whatever you might think its worth. 
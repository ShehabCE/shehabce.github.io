---
layout: post
title:  "Red Black Trees"
date:   2018-03-18 08:40:00
<!-- author: Shehab -->
categories: Computer-Science
tags: Algorithms
cover:  "/assets/posts/RBT.JPG"
---

Red Black Trees! I've heard this name few times before and it scared me off because it looked complicated and I didn't have to use it when I was an undergrad. But hey, you can't judge things just by their title, right?. So whenever I think of Red Black Tree, I always remember this important keyword, <strong>Balance</strong>!

A Red Black Tree is not a totally new datastructure, it is rather an augmented form of a very popular datastructure, Binary Search Trees! It is a <strong> Balanced </strong> Binary Search Tree that <strong>ALWAYS</strong> guarantee the following operations of time complexity O(logN) in the worst case where N is the number of nodes in the tree! 
<ul>
	<li> Search(T, key) </li>
	<li> Insert(T, key) </li>
	<li> Delete(T, key)</li>
	<li> Maximum(T) </li>
	<li> Minimum(T) </li>
	<li> Successor(T) </li>
	<li> Predecessor(T) </li>
</ul>

But first, for those of you who don't know Binary Search Trees (BST), I'll briefly explain it in this following section and then talk about the importance of a Red Black Tree that makes it an imporved version of a BST. If you already know BST, you can skip this part. 

Okay, what is a Binary Search Tree?

....


Now, time for Red Black Tree!

...

{% highlight c++ %}
// an (RBT) Node structure.
class RedBlackNode {
public:
	RedBlackNode *parent;
	RedBlackNode *left;
	RedBlackNode *right;
	int val;
	int color;	// Red -> 1 | Black -> 0
	RedBlackNode(int k) : val(k) {
		parent = NULL;
		left = NULL;
		right = NULL;
		color = 1;
	};
};
{% endhighlight %}
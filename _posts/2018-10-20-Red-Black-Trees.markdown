---
layout: post
title:  "Red Black Trees"
date:   2018-10-20 08:40:00
author: Shehab
categories: Computer-Science
tags: Algorithms
---

Red-Black Trees! Though the name might say it is a complicated data structure, but it is not that hard given how powerful and useful it is in real world applications! C++ STL libraries such as set and map are implemented using Red-Black Trees! And one word to represent the core of Red Black Trees is, <strong>balance</strong>!

A Red Black Tree is not a totally new datastructure, it is rather an augmented form of a very popular datastructure, Binary Search Trees! It is a <strong> Balanced </strong> Binary Search Tree that <strong>ALWAYS</strong> guarantee the dynamic set operations of time complexity O(logN) in the worst case where N is the number of nodes in the tree.
<ul>
	<li> Search(T, key)</li>
	<li> Insert(T, key)</li>
	<li> Delete(T, key)</li>
	<li> Successor(T, key)</li>
	<li> Predecessor(T, key)</li>
	<li> Maximum(T)</li>
	<li> Minimum(T)</li>
</ul>

But first, for those of you who don't know Binary Search Trees (BST), I'll briefly explain it in this following section and then talk about the importance of a Red Black Tree as an improved version of a BST. If you already know BST, you can skip this part. 

<hr> 
Okay, what is a Binary Search Tree?

Binary Search Tree is a collection of nodes with keys that follows a certain ordering property. 
<ol>
	<li>Each tree has a root node.</li>
	<li>Each node can have up to 2 children</li>
	<li>Nodes are ordered in a way where key(left) < key(root) < key(right).</li>
</ol>

{% highlight c++ %}
class TreeNode {
public:
	TreeNode *left;
	TreeNode *right;
	int val;
	TreeNode(int k) : val(k) {
		left = NULL;
		right = NULL;
	}; 
};
{% endhighlight %}
To focus on the most important operations which have the same time complexity. 
<table cellpadding="0" cellspacing="0">
	<tr>
		<th>Operation</th><th>Best Case</th><th>Average Case</th><th>Worst Case</th>
	</tr>
	<tr>
		<td>Search</td><td>O(lgN)</td><td>O(lgN)</td><td>O(N)</td>
	</tr>
	<tr>
		<td>Insert</td><td>O(lgN)</td><td>O(lgN)</td><td>O(N)</td>
	</tr>
	<tr>
		<td>Delete</td><td>O(lgN)</td><td>O(lgN)</td><td>O(N)</td>
	</tr>
</table>
<hr>
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
<table cellpadding="0" cellspacing="0">
	<tr>
		<th>Operation</th><th>Best Case</th><th>Average Case</th><th>Worst Case</th>
	</tr>
	<tr>
		<td>Search</td><td>O(lgN)</td><td>O(lgN)</td><td>O(lgN)</td>
	</tr>
	<tr>
		<td>Insert</td><td>O(lgN)</td><td>O(lgN)</td><td>O(lgN)</td>
	</tr>
	<tr>
		<td>Delete</td><td>O(lgN)</td><td>O(lgN)</td><td>O(lgN)</td>
	</tr>
</table>
<h2>RBT Insert Operation</h2>
Everytime we insert a new node into our RBT, we need to do some maintenance checking to preserve the properties of the Red-Black Tree in case any violation occurs. There are two possible violations upon insertion:
<ol>
	<li>Red Violation: A red node has a red child.</li>
	<li>Black Violation: One path has more black nodes than another path.</li>
</ol>
There are <strong>3 cases</strong> to handle when we insert a new node to preserve the balance, and we handle those cases with two tools; either by some pointer structure manipulation (rotation) or node reconfiguration (recoloring).

<hr>
<h2>RBT Delete Operation</h2>
<hr>
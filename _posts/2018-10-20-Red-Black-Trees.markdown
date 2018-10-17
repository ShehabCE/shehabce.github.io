---
layout: post
title:  "Red Black Trees"
date:   2018-10-20 08:40:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/RBTree.png"
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
BSTs are useful when it comes to queries such as searching for a key in a tree that provides lookup of(lgN) faster than going through the array of elements in O(N). Cutting the search cost from O(N) to O(lgN) is significant to applications that can only afford a logarithmic operation in that structure. 
However, the problem arises when the tree is not balanced, adding sorted elements in a tree will give a skewed shape of the tree where all the keys are on one branch and not distributed on two branches. This skewed shape can very much be a linked list where the operations cost have become O(N) which is no better than going through the entire array. BSTs can not guarantee logarithmic cost of operations in the worst case, because in the worst case, the tree can become imbalanced and impractical. 
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
There are 4 properties that must hold in a Red-Black Tree:
<ol>
<li>Every node must be colored black or red.</li>
<li>Root node and leaves are always black.</li>
<li>For any red node, its children must be black. No red node can have a red child.</li>
<li>For node x, any simple path from x to its desendent leaves must have the same number of black nodes. Also known as black height.</li>
</ol>
<img src="/assets/posts/RBTree.png"> 
As you can see, the node structure of a RB tree is the same as BST node structure, just augmented with extra bit of information (color).
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
However, to ensure a logarithmic time complexity in set of operations, each update query (Insert/Delete) is followed by another method called RB-INSERT-FIXUP and RB-DELETE-FIXUP that provides some maintenance to the tree structure to make sure the four enlisted properties are well preserved, and if there is a violation, it is fixed.
They are not super easy I have to say, but you gotta admire the amount of effort and intellect put into this data structure to handle these cases. Let's start with Insert and then Delete operations, after rotation!
<h2>Rotation... but why?</h2>
There might be cases where the height of a branch might be larger than the height of the other branch, giving it this imbalanced shape. So by pivoting around two nodes X and Y, you can re-balance the tree! 
<div class="Image Row">
	<div class="Image Col">
		<img src="/assets/posts/LL.png">
	</div>
	<div class="Image Col">
		<img src="/assets/posts/LR.png">
	</div>
	<div class="Image Col">
		<img src="/assets/posts/RL.png">
	</div>
	<div class="Image Col">
		<img src="/assets/posts/RR.png">
	</div>
</div>
<img src="/assets/posts/rotations.png">
<p align="center"><I>source ["CLRS, Introduction to Algorithms"]</I></p>
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
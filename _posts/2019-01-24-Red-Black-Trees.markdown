---
layout: post
title:  "Red Black Trees [Incomplete]"
date:   2019-01-24 08:40:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/RBT.png"
---

Red-Black Trees! where C++ STL libraries such as set, multiset, and map are implemented using Red-Black Trees as one of many other balanced trees. So a one word to represent the core of Red Black Trees is, <strong>balance</strong>!

A Red Black Tree is not a totally new data structure, it is rather an augmented form of a very popular datastructure, Binary Search Trees! It is a <strong> Balanced </strong> Binary Search Tree that <strong>ALWAYS</strong> guarantee the dynamic set operations of time complexity O(logN) in the worst case where N is the number of nodes in the tree. 
<ul>
	<li> Search(T, key)</li>
	<li> Insert(T, key)</li>
	<li> Delete(T, key)</li>
	<li> Successor(T, key)</li>
	<li> Predecessor(T, key)</li>
	<li> Maximum(T)</li>
	<li> Minimum(T)</li>
</ul>

<p align="center"><emp>You can go quickly through Binary Search Trees <a href="https://shehabmmohamed.github.io/computer-science/2018/10/19/Binary-Search-Trees.html" target="_blank">here.</a></emp></p>

There are 4 properties that must hold in a Red-Black Tree:-
<ol>
	<li>Every node must be colored black or red.</li>
	<li>Root node AND leaves are always colored black.</li>
	<li>For any red node, its children must be black. No red node can have a red child.</li>
	<li>For node x, any simple path from x to its descendent leaf must have the same number of black nodes. Also known as black height bh(x).</li>
</ol>

<img src="/assets/posts/RBT.png"> 
<p align="center">An example of a Red Black Tree.</p>


As you can see, the node structure of a RB tree is the same as BST node structure, just augmented with an extra bit of information, its color.
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
However, to ensure a logarithmic time complexity of the Red-Black Tree, each update query (Insert/Delete) is followed by another method called RB-INSERT-FIXUP and RB-DELETE-FIXUP that provides some maintenance to the tree structure to make sure the four enlisted properties are well preserved, and if there is a violation, it gets fixed.
They are not super easy I have to say, but you gotta admire the amount of effort and intellect put into this data structure to handle these cases. I'll explain the modified insertion and deletion operations in the following section. But first, Insert and then Delete operations, after rotation!
<h2>Rotation... but why?</h2>
There might be cases where the height of a branch might be larger than the height of the other branch, giving it this imbalanced shape. So by pivoting around two nodes X and Y, you can re-balance the tree! 
<h2> So There are 4 cases for an imbalanced tree. </h2>
<ul>
	<li>Left Left Case (LL)</li>
	<li>Left Right Case (LR)</li>
	<li>Right Left Case (RL)</li>
	<li>Right Right Case (RR)</li>
</ul>
<div class="Image Row">
		<span style="display: inline-block; width: 180px; height: 180px;"><img src="/assets/posts/LL.png"></span>
		<span style="display: inline-block; width: 180px; height: 180px;"><img src="/assets/posts/LR.png"></span>
		<span style="display: inline-block; width: 180px; height: 180px;"><img src="/assets/posts/RL.png"></span>
		<span style="display: inline-block; width: 180px; height: 180px;"><img src="/assets/posts/RR.png"></span>
</div>
<img src="/assets/posts/rotations.png">
<p align="center"><I>source ["CLRS, Introduction to Algorithms"]</I></p>

<h2>RBT Insert </h2>
Everytime we insert a new node into our RBT, we need to do some maintenance checking to preserve the properties of the Red-Black Tree in case any violation occurs. There are two possible violations upon insertion:

<ol>
	<li>Red Violation: A red node has a red child.</li>
	<li>Black Violation: One path has more black nodes than another path.</li>

</ol>
There are 6 cases to handle when we insert a new node in a balanced tree, three of them are symmetric so its actually <strong>3 cases</strong> and we handle those cases with two tools; either by changing some pointer structure (rotation) or node reconfiguration (recoloring).

<hr>

<h2>RBT Delete </h2>
Deleting a node in a RBT is slightly more complicated than inserting a node in a RBT.

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

<p align="center"><a href="https://github.com/ShehabMMohamed/Datastructures-And-Algorithms/blob/master/Advanced%20Data%20Structures/Red%20Black%20Trees/RedBlackTrees.h" target="_blank"> Red Black Trees Implementation </a></p>
---
layout: post
title:  "Binary Search Trees"
date:   2018-10-19 08:15:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/BST.png"
---
The beauty of a data structure is that you can have a structure or a container that can hold data and a set of methods (algorithms) that can operate on your data. Yeah, that's pretty much the equation of a data structure. <strong>Container of data + Operations on that container = Data-Structure</strong> 
<br>
So we can have an array of elements and do a lot of things with that array like; sorting the data, finding an element in the array, adding or removing elements in that array. But when it comes to real world applications, we care about speed and efficiency. We want to do whatever we want with the data as fast as possible! An array wouldn't provide the most efficient way in certain context. If we want to find an element in a huge array, we have to go through the entire array to look for it, so that's O(N) time complexity. But what if there's a faster way? A way to find an element without going through the entire array? A way to find the smallest element in the array for example? That's where Binary Search Trees (or BSTs) step in.
<br>
Binary Search Tree is a dynamic data structure with a collection of nodes that follow a certain ordering property.  
<img src="/assets/posts/BST.png">
<p align="center">An example of a Binary Search Tree.</p>
<h4>Properties of a BST</h4>
<ol>
	<li>Each tree has a root node.</li>
	<li>Each node has a reference of the left child and a reference of the right child.</li>
	<li>Each node can have up to 2 children (that's why its called bianry).</li>
	<li>A node that doesn't have children is called a leaf node.</li>
	<li>Nodes are ordered in a way where key(left child) < key(root) < key(right child).</li>
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


Since there is an ordering property in this tree, standard operations like Search/Insert/Delete are faster when used on a BST than on an array.
BSTs are useful when it comes to queries such as searching for a key in a tree that provides lookup of(h) where h is the height of the tree, and it is proved that h = log(N), faster than going through the array of elements in O(N). Cutting the search cost from O(N) to O(lgN) is significant to applications that can only afford a logarithmic operation in that structure.
<br>

<code>Number of nodes: n = 1 + 2 + 4 + 8 + ... + (2^h-1) = (2^h) - 1</code><br>
<code>Height of the tree: h = log(n+1)</code><br>

<h4>This table is a small comparison of basic operations in <emp>average case</emp> using Big O notation.</h4> 
<table cellpadding="0" cellspacing="0">
	<tr>
		<th>Operation</th><th>Search()</th><th>Delete()</th><th>Insert()</th><th>Max()/Min()</th>
	</tr>
	<tr>
		<td>Unsorted Array</td><td>O(N)</td><td>O(N)</td><td>O(N)</td><td>O(N)</td>
	</tr>
	<tr>
		<td>Sorted Array</td><td>O(lgN)</td><td>O(N)</td><td>O(N)</td><td>O(1)</td>
	</tr>
	<tr>
		<td>Binary Search Tree (balanced)</td><td>O(lgN)</td><td>O(lgN)</td><td>O(lgN)</td><td>O(lgN)</td>
	</tr>
</table>

<hr>

Okay, since we already praised the fact that BST can search for an element in logarithmic time. How does it actually work? Remember that the nodes are distributed in the binary tree with the order key(left child) < key(root) < key(right child), so we know that if we want to find the smallest key we just have to go down to the leftmost node in the tree, same idea applies to finding the largest key in the tree.

<br>

<h2>BST Search</h2>

Since BST is a non-linear data structure, there is no unique way for traversal. There are two ways to traverse in the tree, both of O(lgN):
<ul>
	<li><strong> Depth-First Search (DFS) </strong></li>
	<li><strong> Breadth-First Search (BFS) </strong></li>
</ul> 

<h3> Depth-First Search (DFS) </h3>

There are three types of depth-first search. They don't differ in speed or efficiency. They just differ in the order where they visit the nodes.
<ol>
	<li>Pre-Order Traversal</li>
	<li>In-Order Traversal</li>
	<li>Post-Order Traversal</li>
</ol>

<h4>1. Pre-Order Traversal</h4>
Traversing through the BST by visiting the parent node first, then its left child, and then its right child. 
<p align="center">ROOT -> LEFT CHILD -> RIGHT CHILD</p>
{% highlight c++ %}
void PreOrder(TreeNode *t) {
	Visit(t);	// visit root.
	PreOrder(t->left);
	PreOrder(t->right);
}
{% endhighlight %}

<h4>2. In-Order Traversal</h4>
Traversing through the BST by visiting the left child first, then the parent, and then its right child. Its also the sorted order of visiting the tree.
<p align="center">LEFT CHILD -> ROOT -> RIGHT CHILD</p>
{% highlight c++ %}
void InOrder(TreeNode *t) {
	InOrder(t->left);
	Visit(t);	// visit root.
	InOrder(t->right);
}
{% endhighlight %}

<h4>3. Post-Order Traversal</h4>
Traversing through the BST by visiting the left child first, then the right child, and then the parent.
<p align="center">LEFT CHILD -> RIGHT CHILD -> ROOT</p>
{% highlight c++ %}
void PostOrder(TreeNode *t) {
	PostOrder(t->left);
	PostOrder(t->right);
	Visit(t);	//visit root.
}
{% endhighlight %}


<h3> Breadth-First Search (BFS) </h3>
There is only one type of breadth-first search, the level order traversal.
<ol>
	<li>Level-Order Traversal</li>
</ol>
<h4>Level-Order Traversal</h4>
Traversing through the BST level by level from leftmost to rightmost. Start from the root node at level 0, go to level 1, go through all nodes in level 1 from left to right, go to level 2 and so on.

<hr>

<h2>BST Insertion </h2>
Inserting a node in a BST is straightforward, since we have the ordering property and no duplicate keys are allowed. It is almost identical to searching a node in a BST where you start from the root, recursively go down either in left subtree or right subtree depending on the value of the new key. Once you reach to that location, you link it to its parent either as a left child or a right child. Inserting any node is always at the deepest level of the tree (a new leaf).

<hr>

<h2>BST Deletion </h2>
Unlike Insertion, deleting a node might be tricky and less obvious. There are three scenarios to consider when deleting a node in a BST. 
<ol>
	<li><strong>Node to delete has no children (A leaf node)</strong></li>
	<li><strong>Node to delete has one child</strong></li>
	<li><strong>Node to delete has two children</strong></li>
</ol>
<h4> 1. Node (N) to delete has no children (A leaf node) </h4>
Deleting a leaf node is the simplest case. It doesn't have children so there won't be any tree split. Simply delete it. 

<h4> 2. Node (N) to delete has one child </h4>
Say we want to delete <strong>N</strong> where its child is <strong>C</strong> and its parent is <strong>P</strong>. Deleting <strong>N</strong> will cause a tree split between <strong>P</strong> and <strong>C</strong>. So you just need to bypass <strong>N</strong> where you link <strong>C</strong> to <strong>P</strong> as <strong>P</strong>'s new child instead of <strong>N</strong>, and then safely delete old <strong>N</strong>.

<h4> 3. Node (N) to delete has two children </h4>
This scenario again splits the tree into two sub-trees. There are two solutions for it. 
<ul>
	<li>Find N's Successor (Smallest node in the right sub-tree of N), replace it with N (now N has become a leaf), and then delete N. </li>
	<li>Find N's Predecessor (Largest node in the left sub-tree of N), replace it with N (now N has become a leaf), and then delete N.</li>
</ul>

<hr>

<div>
Binary Search Trees are amazing, right?
</div>
Not quite...
It is a pretty useful data structure, but what if the nodes weren't properly distributed in a BST? Imagine you have an array of N elements that is sorted and you build a BST with it. what would the tree look like?
<div>
The problem arises when the tree is not balanced, adding sorted elements in a tree will give a skewed shape of the tree where all the keys are on one branch and not distributed on two branches. This skewed shape can very much be a linked list where the operations cost have become O(N) which is no better than going through the entire array. BSTs can not <emp>guarantee</emp> logarithmic cost of operations in the worst case, because in the worst case, the tree can become imbalanced and impractical. However, there are self-balancing binary search trees that can solve this issue that a regular BST can't. 
</div>

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

Curious about self-balancing trees? Take a look at <a href="https://shehabmmohamed.github.io/computer-science/2018/10/20/Red-Black-Trees.html" target="_blank">Red-Black Trees</a>.

<h3>Resources used for this article</h3>
<ul>
	<li>Introduction To Algorithms, Third Edition by C.L.R.S.</li>
	<li><a href="https://www.geeksforgeeks.org/binary-search-tree-data-structure/" target="_blank">GeeksForGeeks-BinarySearchTree</a></li>
</ul>

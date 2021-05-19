---
layout: post
title: "Binary Search Trees"
date: 2019-05-19 08:30:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/BST.png"
---

Best thing about data structures is that you can have a structure or a container that can hold data and a set of methods (algorithms) that can operate on your data. Yeah, that's pretty much the receipe of a data structure. <strong>Container of data + Operations on that container = Data structure</strong>
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
	<li>Each node can have up to 2 children (that's why its called binary).</li>
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
BSTs are useful when it comes to frequent queries, searching for a key in a BST provides lookup of time complexity O(h) where h is the height of the tree, and it is proved that h = log(N), faster than going through the array of elements in O(N). Cutting the search cost from O(N) to O(logN) is significant to applications that can only afford a logarithmic operation in that structure.
<br>
How can you know the number of nodes in a tree? Well, counting them is a strategy, but don't do that. Please. Instead, think of the levels of the tree. First level which is the root node has one node. Second level has two nodes. Third level has four nodes. You see the pattern? Each level you go down the tree, the number of nodes increases by a multiple of 2 since each node can have two children. So if you have a a tree of height 12, you can get the number of nodes through this equation.
<br>
<code>Number of nodes: n = 1 + 2 + 4 + 8 + ... + (2^h-1) = (2^h) - 1</code><br>
<code>Max # of nodes at height h: (2^h) - 1</code><br>
<code>Height of the tree: h = log(n+1)</code><br>

<strong>This table is a small comparison of basic operations in <emp>average case</emp> using Big O notation.</strong>

<table cellpadding="0" cellspacing="0">
	<tr>
		<th>Operation</th><th>Search()</th><th>Delete()</th><th>Insert()</th><th>Max()/Min()</th>
	</tr>
	<tr>
		<td>Unsorted Array</td><td>O(N)</td><td>O(N)</td><td>O(N)</td><td>O(N)</td>
	</tr>
	<tr>
		<td>Binary Search Tree</td><td>O(lgN)</td><td>O(lgN)</td><td>O(lgN)</td><td>O(lgN)</td>
	</tr>
</table>

Okay, since we already praised the fact that BST can search for an element in logarithmic time. How does it actually work? Remember that the nodes are distributed in the binary tree with the order key(left child) < key(root) < key(right child), so we know that if we want to find the smallest key we just have to go down to the leftmost node in the tree, finding the largest key in the tree would be the other way around.

<h2>BST Search</h2>

Since BST is a non-linear data structure, there is no unique way for traversal. There are two common ways to traverse in the tree, both of O(lgN):

<ul>
	<li><strong> Depth-First Search (DFS) </strong></li>
	<ul>
		<li>Pre-Order</li>
		<li>In-Order</li>
		<li>Post-Order</li>
	</ul>
	<li><strong> Breadth-First Search (BFS) </strong></li>
	<ul>
		<li>Level-Order</li>
	</ul>
</ul>

<h3> Depth-First Search (DFS) </h3>

There are three types of depth-first search. They don't differ in speed or efficiency. They just differ in the order where they visit the nodes.

<ol>
	<li>Pre-Order Traversal</li>
	<li>In-Order Traversal</li>
	<li>Post-Order Traversal</li>
</ol>

<h4>1. Pre-Order Traversal</h4>
Traversing the BST by visiting the parent node first, then its left child, and then its right child. 
<p align="center"><I>root -> left child -> right child</I></p>
{% highlight c++ %}
void PreOrder(TreeNode *t) {
	Visit(t);	// visit root.
	PreOrder(t->left);
	PreOrder(t->right);
}
{% endhighlight %}

<h4>2. In-Order Traversal</h4>
Traversing the BST by visiting the left child first, then the parent, and then its right child. Its also the sorted order of visiting the tree.
<p align="center"><I>left child -> root -> right child</I></p>
{% highlight c++ %}
void InOrder(TreeNode *t) {
	InOrder(t->left);
	Visit(t);	// visit root.
	InOrder(t->right);
}
{% endhighlight %}

<h4>3. Post-Order Traversal</h4>
Traversing the BST by visiting the left child first, then the right child, and then the parent.
<p align="center"><I>left child -> right child -> root</I></p>
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
Traversing the BST level by level from leftmost to rightmost. Start from the root node at level 0, go to level 1, go through all nodes in level 1 from left to right, go to level 2 and so on.

{% highlight c++ %}
void LevelOrder(TreeNode _t) {
if(!t) return NULL;
queue<TreeNode_> q;
q.push(t);
while(!q.empty()) {
TreeNode\* temp = q.front();
q.pop();
Visit(temp);
if(temp->left)
q.push(temp->left);
if(temp->right)
q.push(temp->right);
}
}
{% endhighlight %}

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
Say we want to delete (N) where its child is (C) and its parent is (P). Deleting (N) will cause a tree split between (P) and (C). So you just need to bypass (N) where you link (C) to (P) as (P)'s new child instead of (N), and then safely delete old (N).

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
The problem arises when the tree is not balanced, adding sorted elements in a tree will give a skewed shape of the tree where all the keys are on one branch and not distributed on two branches. This skewed shape can very much be a linked list where the operations cost have become O(N) which is no better than going through the entire array. BSTs can not <emp>guarantee</emp> logarithmic cost of operations in the worst case, because in the worst case, the tree can become imbalanced and impractical. However, there are self-balancing binary search trees that can solve this issue that a regular BST can't. Red-Black Trees is one of them. <a href="https://shehabmmohamed.github.io/computer-science/2019/01/24/Red-Black-Trees.html" target="_blank">Link to Red-Black Trees article</a>
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

<p align="center"><a href="https://github.com/ShehabMMohamed/Datastructures-And-Algorithms/tree/master/Data%20Structures/Binary%20Search%20Trees" target="_blank"> Binary Search Trees in C++ </a></p>

<p align="center"><a href="https://github.com/ShehabMMohamed/Go-Datastructures/blob/main/internal/BinarySearchTrees/BinarySearchTree.go" target="_blank"> Binary Search Trees in Go </a></p>

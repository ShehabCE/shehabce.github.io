---
layout: post
title: "Heaps & Priority Queues"
date: 2019-04-25 12:10:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/Heaps.png"
---

A heap is a datastructure that stores the data in a way where the smallest/largest element can be accessed in constant time, i.e., in Big O(1).

Binary Heaps are in general implemented using an array, however, we visualize it as a complete binary tree where the value of the parent is either smaller/greater than its children, depending on the variant that you want to implement.

There are two variants of Heaps:

<ol>
	<li>Max Heap - Largest value is at the root of the tree</li>
	<li>Min Heap - Smallest value is at the root of the tree</li>
</ol>

Well in that case, what is the Priority Queue?

Priority Queue as a definition, it is an abstract data type (ADT) based on Heaps. You can consider that Heaps and Priority Queues are both the same thing. We define a priority queue based on whether it is a Min or a Max heap, and we use it to solve our problem.

First let's define a Priority Queue class.
{% highlight c++ %}
class PriorityQueue {
private:
	int *A;
	int capacity;
	int size;
	int Parent(i);
	int Left(i);
	int Right(i);
	void HeapifyUp(int i);
	void HeapifyDown(in i);
public:
	PriorityQueue();
	void Push(const int& e);
	void Pop();
	int Top();
	bool IsFull();
	bool IsEmpty();
	~PriorityQueue();
};
{% endhighlight %}

As mentioned earlier, a heap is just an array visualized as a complete binary tree, so whenever we want fo find parent or child of a specific index, we calculate a certain formula to get that index.

<code>Parent(index) = (index - 1) / 2</code><br>
<code>LeftChild(index) = (index * 2) + 1</code><br>
<code>Parent(index) = (index * 2) + 2</code><br>

Based on that, let's cover the following methods that need to be implemented to preserve the order and the structure of the Heap.

<style>
.heap { 
	display: block;
	margin-left: auto;
	margin-right: auto;
	height: 250px;
	width: 200px;
}
</style>

1. Pushing an element to a Heap relies on two things:

<ol>
	<li>Insert an element at the end of the heap.</li>
	<li>Recursively Bubble Up the element to its correct place whether it is higher/lower than its parent.</li>
</ol>

<img class="heap" src="/assets/posts/Heap-Push-1.png">
<img class="heap" src="/assets/posts/Heap-Push-2.png">
<img class="heap" src="/assets/posts/Heap-Push-3.png">

2. Popping an element from a Heap relies on three things:

<ol>
	<li>Swap the top element with the last element in the heap.</li>
	<li>remove the last element from the heap (could be as simple as decrementing the array size).</li>
	<li>Recursively Bubble Down the newly swapped top element to its correct place whether it is higher/lower than its children.</li>
</ol>

<img class="heap" src="/assets/posts/Heap-Pop-1.png">
<img class="heap" src="/assets/posts/Heap-Pop-2.png">
<img class="heap" src="/assets/posts/Heap-Pop-3.png">
<img src="/assets/posts/Heap-Pop-4.png">
<img src="/assets/posts/Heap-Pop-5.png">


Once you implement BubbleUp() and BubbleDown() methods which are also known as HeapifyUp() and HeapifyDown(), you will use them in Push() and Pop() methods and the rest of the implementation is straight forward. 

When it comes to time complexity...

<table cellpadding="0" cellspacing="0">
	<tr>
		<td>Push</td><td>O(LogN)</td>
	</tr>
	<tr>
		<td>Pop</td><td>O(LogN)</td>
	</tr>
	<tr>
		<td>Top</td><td>O(1)</td>
	</tr>
</table>

<p align="center"><a href="https://github.com/ShehabMMohamed/Datastructures-And-Algorithms/blob/master/Data%20Structures/Priority%20Queues/PriorityQueue.h" target="_blank"> Heaps in C++ </a></p>

<p align="center"><a href="https://github.com/ShehabMMohamed/Go-Datastructures/blob/main/internal/Heaps/Heap.go" target="_blank"> Heaps in Go </a></p>

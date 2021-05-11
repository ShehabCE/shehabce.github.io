---
layout: post
title: "Heaps & Priority Queues [Draft In Progress]"
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

In this article, I'll cover how does heaps work and what are the possible applications for it.

First let's define a Priority Queue class.
{% highlight c++ %}
class PriorityQueue {
private:
int \*A;
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
bool IsFull();
bool IsEmpty();
~PriorityQueue();
};
{% endhighlight %}

As mentioned earlier, a heap is just an array visualized as a tree, so whenever we want fo find parent or child of a specific index, we calculate a certain formula to get that index.

<code>Parent(index) = (index - 1) / 2</code><br>
<code>LeftChild(index) = (index \* 2) + 1</code><br>
<code>Parent(index) = (index \* 2) + 2</code><br>

Based on that, let's cover the following methods that need to be implemented to preserve the order and the structure of the Heap.

1. Pushing an element to a Heap.

<img src="/assets/posts/Heap-Push-1.png">
<img src="/assets/posts/Heap-Push-2.png">
<img src="/assets/posts/Heap-Push-3.png">

2. Popping an element from a Heap.

<img src="/assets/posts/Heap-Pop-1.png">
<img src="/assets/posts/Heap-Pop-2.png">
<img src="/assets/posts/Heap-Pop-3.png">
<img src="/assets/posts/Heap-Pop-4.png">
<img src="/assets/posts/Heap-Pop-5.png">

When it comes to time complexity...

<table cellpadding="0" cellspacing="0">
	<tr>
		<td>Push</td><td>Add At End</td><td>O(LogN)</td>
	</tr>
	<tr>
		<td>Pop</td><td>Remove at Top</td><td>O(LogN)</td>
	</tr>
	<tr>
		<td>Top</td><td>Access Top</td><td>O(1)</td>
	</tr>
</table>

<p align="center"><a href="https://github.com/ShehabMMohamed/Datastructures-And-Algorithms/blob/master/Data%20Structures/Priority%20Queues/PriorityQueue.h" target="_blank"> Heaps in C++ </a></p>

<p align="center"><a href="https://github.com/ShehabMMohamed/Go-Datastructures/blob/main/internal/Heaps/Heap.go" target="_blank"> Heaps in Go </a></p>

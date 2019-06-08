---
layout: post
title:  "Stacks & Queues"
date:   2019-01-20 08:40:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/"
---

All sorts of applications can hold large amount of data for it to function, and storing data in a proper structure helps the applications to run efficiently. Datastructure is how we manage our stored information and more conveniently, operate on it.
A certain datastructure is useful for a certain application depending on which operation being called and how frequent it is being called. Therefore, a datastructure is based on the structure that holds the data + the algorithms of that structure.

In this article, I'll be talking about two primitive datastructures that every CS student has definitely used before one way or another.

<h2 align="center">Stacks</h2>

Let's start with stacks, a LIFO datastructure used for retrieval/insertion of the most recent data element in constant time. LIFO stands for "Last In First Out", meaning that the last element added to the stack is also the first one to be removed from the stack. Basically,

<ul>
	<li>Adding an element to the stack is called push.</li>
	<li>Removing an element from the stack is called pop.</li>
</ul>

<img src="/assets/posts/stack.jpg">

When it comes to time complexity...
<table cellpadding="0" cellspacing="0">
	<tr>
		<td>Push</td><td>(Add to top)</td><td>O(1)</td>
	</tr>
	<tr>
		<td>Pop</td><td>(Remove from top)</td><td>O(1)</td>
	</tr>
</table>

Implementing stacks is ridiciously easy, but still has to be implemented in order to understand it thoroughly. All insertions and deletions are done at one end called top. A stack can be implemented in two ways...
<ol>
	<li>Using Dynamic Arrays</li>
	<li>Using Linked Lists</li>
</ol>
How you implement it is your choice, but those are the common methods needed to define a new class called "SimpleStack".

{% highlight c++ %}
// A common Stack Interface.
template<typename T>
class SimpleStack {
public:
	SimpleStack(int size);		// Class Constructor.
	void push(const T& e);		// adds element to top of the stack.
	void pop();			// removes top element of the stack.
	T top();			// returns top element of the stack.
	bool IsEmpty();			// checks if stack is empty.
	bool IsFull();			// checks if stack is full.
	~SimpleStack();			// Class Destructor.
};
{% endhighlight %}


<p align="center"><a href="https://github.com/ShehabMMohamed/Datastructures-And-Algorithms/blob/master/Data%20Structures/Stacks%20and%20Queues/Stacks.h" target="_blank"> Stack Implementation </a></p>

<h4>Stack-based Applications</h4>
<ul>
	<li>Balancing Enclosure Symbols</li>
	<li>Conversion from Decimal to Hexadecimal</li>
	<li>Evaluation of Postfix Expression</li>
	<li>The Hanoi Towers</li>
	<li>Backtracking</li>
	<li>Transforming Recursive functions into Iterative functions</li>
	<li>Web browser history</li>
	<li>And many more...</li>
</ul>

<h2 align="center">Queues</h2>

Next, we'll talk about queues, a FIFO datastructure that works the same way as you'd expect after hearing the word queue. FIFO stands for "First In First Out", in other words, the first element that is added to the queue is also the first one to be removed from the queue. Think of it as standing in a queue for the movies, at the clinic, et cetera. It is a simple linear datastructure that serves well for all queue-based applications like CPU task scheduling in Operating Systems or applying Breadth-First Search Algorithm. 

However, some applications might require and advanced datastructure like a Priority Queue that handles the queue based on who has the highest priority (key). You can read about Priority Queue in this <a href="" target="_blank">article</a>, for now what you need to know is that Queues and Priority Queues are not the same. 

Back to Queues, it is a linear list of elements where access is by order of insertion. Insertions are done at one end <emp>rear</emp> and deletions are done at the other end <emp>front</emp>. Basically,
<ul>
	<li>Adding an element to end of queue is called enqueue.</li>
	<li>Removing an element from front of queue is called dequeue.</li>
</ul>

<img src="/assets/posts/queue.jpg">

When it comes to time complexity...
<table cellpadding="0" cellspacing="0">
	<tr>
		<td>Enqueue</td><td>(Add to Rear)</td><td>O(1)</td>
	</tr>
	<tr>
		<td>Dequeue</td><td>(Remove from Front)</td><td>O(1)</td>
	</tr>
</table>

When it comes to implementation, a queue is viewed as a circular array with two pointers <emp>front</emp> and <emp>rear</emp>. Both pointers advance clockwise and to enqueue: <code>rear = (rear + 1) % size</code> while to dequeue: <code>front = (front + 1) % size</code>. A queue can be implemented in two ways...
<ol>
	<li>Using Dynamic Arrays</li>
	<li>Using Linked Lists</li>
</ol>

{% highlight c++ %}
// A common Queue Interface.
template<typename T>
class SimpleQueue {
public:
	SimpleQueue(int size);			// Class Constructor.
	void enqueue(const T& e);		// adds element to end of the queue.
	T dequeue();				// removes the element from front of the queue.
	T queueFront();				// retrieves front element without removing it.
	bool IsEmpty();				// checks if queue is empty.
	bool IsFull();				// checks if queue is full.
	~SimpleQueue();				// Class Destructor.
};
{% endhighlight %}


<p align="center"><a href="https://github.com/ShehabMMohamed/Datastructures-And-Algorithms/blob/master/Data%20Structures/Stacks%20and%20Queues/Queues.h" target="_blank"> Queue Implementation </a></p>

<h4>Queue-based Applications</h4>
<ul>
	<li>Job Scheduling</li>
	<li>Simulation of Waiting Lines</li>
	<li>I/O Buffering</li>
	<li>And many more...</li>
</ul>

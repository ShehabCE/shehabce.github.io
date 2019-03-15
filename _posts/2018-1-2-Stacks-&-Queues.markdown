---
layout: post
title:  "Stacks & Queues [Not Complete]"
date:   2018-10-20 08:40:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/"
---

All sorts of applications can hold large amount of data for it to function, and storing data in a proper structure helps the applications to run efficiently. Datastructure is how we manage our stored information and more conveniently, operate on it.
A certain datastructure is useful for a certain application depending on which operation being called and how frequent it is called. Therefore, a datastructure is based on the structure that holds the data + the algorithms of that structure.

In this article, I'll be talking about two primitive datastructures that every CS student has definitely used before one way or another.

<h2 align="center">Stacks</h2>

Let's start with stacks, a LIFO datastructure used for retrieval/insertion of the most recent data element in constant time. LIFO stands for "Last In First Out", meaning that the last element added to the stack is also the first one removed from the stack. Let's rephrase it in a better way for convenience.

<ul>
	<li>Adding an element to the stack is called push.</li>
	<li>Removing an element from the stack is called pop.</li>
</ul>

GIF 1.1 here shows how do you push an element to the stack.

GIF 1.2 here shows how do you pop an element from the stack.

Implementing stacks is ridiciously easy, but still has to be implemented in order to understand it thoroughly. How you implement it is your choice, but those are the common methods needed to define a new class called "SimpleStack".

{% highlight c++ %}
// Stack common methods.
class SimpleStack {
public:
	SimpleStack(int size);	// Class Constructor.
	void push(int element);	// adds element to top of the stack.
	void pop();				// removes top element of the stack.
	int top();				// returns top element of the stack.
	bool IsEmpty();			// checks if stack is empty.
	bool IsFull();			// checks if stack is full.
	~SimpleStack();			// Class Destructor.
};
{% endhighlight %}



<h2 align="center">Queues</h2>

Next, we'll talk about queues, a FIFO datastructure that works the same way as you'd expect after hearing the word queue. FIFO stands for "First In First Out", in other words, the first element that is added to the queue is also the first one that is removed from the queue. Think of it as standing in a queue for the movies, at the clinic, et cetera. It is a simple datastructure that serves well for all queue-based applications like CPU task scheduling in Operating Systems or applying Breadth-First Search Algorithm! 

However, some applications might require and advanced datastructure like a Priority Queue that handles the queue based on who has the highest priority. You can read about Priority Queue in this article, for now what you need to know is that Queues and Priority Queues are not the same. 

Back to Queues,

<ul>
	<li>Adding an element to end of queue is called enqueue.</li>
	<li>Removing an element from front of queue is called dequeue.</li>
</ul>

GIF 2.1 here shows how do you enqueue an element to the queue.

GIF 1.2 here shows how do you dequeue an element from the queue.

{% highlight c++ %}
// Queue common methods.
class SimpleQueue {
public:
	SimpleQueue(int size);		// Class Constructor.
	void enqueue(int element);	// adds element to end of the queue.
	int back();					// returns the element at end of the queue.
	int dequeue();				// removes the element from front of the queue.
	int front();				// returns the element from front of the queue.
	bool IsEmpty();				// checks if queue is empty.
	bool IsFull();				// checks if queue is full.
	~SimpleQueue();				// Class Destructor.
};
{% endhighlight %}



<!-- <h3>Resources used for this article</h3>
<ul>
	<li>Introduction To Algorithms, Third Edition by C.L.R.S.</li>
	<li><a href="https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/" target="_blank">GeeksForGeeks-RedBlackTrees</a></li>
</ul> -->
---
layout: post
title:  "Linked Lists (Singly, Doubly, and Circularly)"
date:   2019-03-12 16:00:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/linkedlist2.png"
---

Linked Lists, another primitive datastructure with significant importance. It is a linear collection of data elements, slightly similar to arrays, the difference is the operations done on it.

A linked list is like a train when you think about it, such that each element is a block that is chained to the block next to it and so on. A linked list is a collection of blocks or nodes in this case such that each node carries some data and a pointer that points to the next node, and so on.

Although both linked lists and arrays are linear collections of data, they differ in the following
<ol>
	<li>Arrays have random access element such that an element can be accessed by its position (index), while a linked list has to go from the first node all the way to the nth node to access that nth element.
	</li>
	<li>Statically defined Arrays can not add more elements that exceeds its pre-defined size, while a linked lists is dynamic in the sense that a block can be added anywhere with no more than two pointer manipulation. It is a dynamic linear datastructure.
	</li>
</ol>

Usually when working with linked lists, when we point at the first node we often refer to it as the head, while pointing at the last node is often called the tail. It is a common practice so that we know if we want to traverse the list, we start from the <strong>head</strong> all the way to the <strong>tail</strong>.


<h3>There are 3 variations of a Linked List:-</h3>
<ol>
	<li>Singly list:- a list that has only one pointer called <emp>next</emp>, pointing to the next node. Last node in the list points to NULL.
	</li>
<p align="center"><img src="/assets/posts/singlylist.png"></p>
{% highlight c++ %}
template <typename T>
class SingleListNode {
public:
	T data;
	SingleListNode *next;
	SingleListNode(const T& d) : data(d), next(NULL) {}
};
{% endhighlight %}
	<li>Doubly list:- a list that has two pointers <emp>(next, prev)</emp> pointing to both the next node and the previous node of the current one. Last node's <emp>next</emp> points to NULL, and the first block's <emp>prev</emp> points to NULL.
	</li>
<p align="center"><img src="/assets/posts/doublylist.png"></p>
{% highlight c++ %}
template<typename T>
class DoublyListNode {
public:
	T data;
	DoublyListNode *next, *prev;
	DoublyListNode(const T& d) : data(d), next(NULL), prev(NULL) {}
};
{% endhighlight %}
	<li>Circularly list:- it is the same as a doubly list except that the last node points back to the first node (head) and head's <emp>prev</emp> pointer points to the last node (tail), thus forming a cycle.
	</li>
<p align="center"><img src="/assets/posts/circularlylist.png"></p>
</ol>

<p align="center"><a href="https://github.com/ShehabMMohamed/Datastructures-And-Algorithms/blob/master/Data%20Structures/Linked%20Lists/LinkedLists.h" target="_blank"> Linked List Implementation </a></p>


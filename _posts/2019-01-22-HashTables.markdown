---
layout: post
title: "Hash Tables"
date: 2019-01-22 01:05:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/Hash-Tables.jpg"
---

Hash Table is a key-value data structure which stores the data in an associative manner. A Hash Table stores the data as key-value pairs where the key is an output of a defined hash function and the value is the data itself that needs to be stored.

The idea of hashing is important in Computer Science. Hashing in general is a function applied to some key where we can determine the position of its value or entry in the array without going through the entire array. We refer to it as a "Hash Function". Under ideal circumstances, the cost of searching for a key is constant, i.e., O(1).

<img src="/assets/posts/Hash-Tables.jpg">

<p align="center">An example of a basic Hash Table</p>

Working with Hash Tables is incredibly important because now we have the ability to perform a set of operations like Search/Add/Delete on a certain record in constant time. This can be used as a lookup dictionary when solving lots of problems, given that the hash function is efficient and can provide that O(1) time complexity. An efficient hash function should provide a unique hashed key for every key.

What if the hash function was poorly written? Meaning that when we hash two keys, we get the same hashed value? That's where collision happens.


<h4>Collision Detection </h4>

Collision happens when two keys hash to the same position, say for example we have a table of size 11 and two keys, 55 and 66 and our hash function is key % size.

You will find that

<code> Hash(key=55) = 55 % 11 = 0</code>

<code> Hash(key=66) = 66 % 11 = 0</code>

As you can see, two distinct keys map to the same location which are called "synonyms" and the situation is called "collision"


<h4>Methods for handling collisions</h4>

1. <strong>Separate Chaining</strong> (Open Hashing): Chaining is a collision resolution mechanism. A smaller table is used in which each location is associated with a linked list. Synonyms of a key in slot are stored in the linked list associated with that slot. Searching is done by hashing the key first to a main slot and if not found, a linear search is conducted in the associated linked list.

<img src="/assets/posts/Hash-Tables-separate-chaining.png">


2. <strong>Open Addressing</strong> (Closed Hashing): We use a simple rule to decide where to put a new item when the desired space is already occupied. We always put it in the next occupied cell. On serching for a given item, we go to the intended location and search sequentially. If we find an empty cell before we fine the item, it does not exist anywhere in the table.
<ol>
	<li>Linear Probing</li>
	<li>Quadric Probing</li>
	<li>Double Hashing</li>		
</ol>

<img src="/assets/posts/Hash-Tables-probing.png">


Given a hash table with some inserted entries, we want to determine the performance of that table we use <emp>Load Factor</emp>.

Load Factor is a metric used to estimate the performance of a hash table. As the load factor grows larger, the hash table becomes slower. A low load factor is not especially beneficial because if the load factor approaches 0, the proportion of unused areas in the hash table increases, but there is not necessarily any reduction in search cost.
This results in wasted memory.

Load Factor Formula is  <code> α = # of keys / SIZE </code>

// A Basic Class of a HashTable (No Collision Handling)
{% highlight c++ %}
template <typename KeyType, typename DataType>
class HashTable {
private:
	DataType *A;
	int size;
	int hash(KeyType _key);
	bool keyExists(KeyType _key);
public:
	HashTable(const int _size);
	void Insert(KeyType k, DataType v);
	void Delete(KeyType k);
	DataType Get(KeyType k);
	void DisplayTable();
	~HashTable();
};
{% endhighlight %}



<h4>Properties of Hash Functions:</h4>
<ol>
	<li>Hash Functions should be simple and fast.</li>
	<li>Hash Functions should provide a uniform distribution across the table.</li>
	<li>Hash Functions should not cluster keys in regions of the table, using MaxSize as a prime number reduces clustering.</li>
	<li>Hash Functions should provide collisions as minimum as possible.</li>
	<li>Less Load factor without waste in memory.</li>
</ol>


There is an important concept when it comes to Hash Tables as well called Amortization which I highly recommend reading. 
<p align="center"><a href="https://www.cs.cornell.edu/courses/cs312/2008sp/lectures/lec20.html" target="_blank"> Amrotized Analysis - Cornell University </a></p>


<p align="center"><a href="https://github.com/ShehabMMohamed/Go-Datastructures/blob/main/internal/HashTables/HashTable.go" target="_blank"> Hash Tables in Go </a></p>

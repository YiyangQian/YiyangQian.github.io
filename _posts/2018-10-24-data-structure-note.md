---
title: "Data Structure Notes"
layout: post
date: 2018-10-24
# image: /assets/images/adsk.JPG
headerImage: false
tag:
- markdown
- components
- extra
category: blog
author: YY
description: Markdown summary with different options
---

## LinkedList and Array ##
1. Both are linear Data Structure
    * There is a sequence and an order of how they are constructed and traversed.
2. Different in how memory allocation
    * When an array is created, it needs a certain number of contiguous memory. Array is static data structure.
    * When LinkedList is born, it does not need to be specified size. LinkedList is dynamic data structure.
3. How LinkedList constructed
    * LinkedList is made up of nodes.
    * A node only knows what data it contains, and who its neighbour is.
4. Inserting and Searching trade off
    * LinkedList is easy for removing and adding, but slow to search.
    * Array is easy for searching (binary search, since contiguous), but slow for grow or shrink.

## HashTable ##
1. Compare direct-address table with HashTable
2. Chaining to solve collisions
    * To avoid collisions, choose a suitable hash function
    * Collisions are not avoidable
    * Time Complexity (Double Linked List)
         * Insert  O(1)
         * Delete  O(1) as pass in the object
         * Search  O(len) len is length of chaining(average case), worst case is O(n)
    * Loading Factor is n / m, n is number of elements to store, and m is number of slots
3. how to compute array indices from keys using hash functions
    * Hash function turns key into an array index
    * Each index of array stores a pointer to a linked list(or a Red Black Tree when length over 8)
    * Dynamic array resizing
        * Load Factor can be the trigger for resizing, when it reaches a threshold(default 0.75)
        * When hash collisions become inevitable (too many elements), allocate a larger array and rehashing all of our existing keys to figure out their new position. This takes O(n) time.
4. Java default initial capacity of HashMap is 16, and load factor is 0.75. 

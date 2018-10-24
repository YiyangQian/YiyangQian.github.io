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
5. Usage of Java HashMap
    ```
        public class SampleMap {
            public static void main(String[] args) {
                HashMap<Integer, Integer> map = new HashMap<>();
                int[] input = {1, 1, 2, 3};
                
                //if we want to count the frequency of input
                for (int i = 0; i < input.length; i++) {
                    map.put(input[i], map.getOrDefault(input[i], 0) + 1);
                }

                //iterate over a map
                for (Map.Entry<Integer, Integer> entry: map.entrySet()) {
                    System.out.println(entry.getKey());
                    System.out.println(entry.getValue());
                }

                for (Integer value: map.values()) {

                }

                for (Integer key: map.keySet()) {

                }

                Iterator it = map.entrySet().iterator();
                while (it.hasNext()) {
                    Map.Entry entry = (Map.Entry) it.next();
                    System.out.println(entry.getKey());
                    System.out.println(entry.getValue());
                }
            }
        }
    ```

## Heap ## 
1. Java implements PriorityQueue based on a min-heap.
2. Definition of Heap 
    * if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C.
3. Time Complexity
    * Heapify is O(lgn)
    * Build a heap is O(n), cause time for heapify each node is reated to its height
4. Heap is based on an array and use index to connect parent an children
    * Array[(i - 1) / 2] parent node
    * Array[2 * i + 1] left child
    * Array[2 * i + 2] right child
3. Customize PriorityQueue based on certain data structure in Java.
    ```
        public class SamplePQ {
            public static void main (String[] args) {
                //Two ways: Java8 lambda or traditional override Comparator
                PriorityQueue<Student> pq1 = new PriorityQueue<Student>((Student a, Student b) -> a.getId() - b.getId());

                PriorityQueue<Student> pq2 = new PriorityQueue<Student>(new StudentComparator());
            }
        }

        class StudentComparator implements Comparator<Student> {
            public int compare (Student a, Student b) {
                return a.getId() - b.getId();
            }
        }

        class Student {
            private String name;
            private int id;
            public String getName() {
                return this.name;
            }
            public int getId() {
                return this.id;
            }
        }
    ```

## Trie
1. Trie is also called prefix trie.
2. Advantage of a Trie
    * Worst time complexity for looking up data is better than hash table. For a Trie, it costs O(m), m is the length of a searching string. Hash Table might need O(n) at worst case. (no collision in trie).
3. How to implement a Trie
    ```
        class Trie {
            boolean isWord;
            //index of a node in children refers to its char
            Trie[] children; 
        }
    ```

## Binary Search Tree
1. Definition
    * root val is greater than value of all nodes in its left subtree
    * root val is smaller than value of all nodes in its right subtree
    * all subtrees are binary search tree
2. code
    ```
        class BSTNode {
            BSTNode left;
            BSTNode right;
            int val;
            BSTNode (int x) {
                this.val = x;
            }
        }
    ```

## Red Black Tree 
1. Self balanced binary search tree
2. A regular BST might become a linkedlist in the worst case
3. TreeMap is based on Red Black Tree
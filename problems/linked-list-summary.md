# Summary of Linked Lists

## Theoretical Basis of Linked Lists

In this article [Linked List Basics](https://keetcoder.com/problems/linked-list-basics.html), the following points are introduced:

- The main types of linked lists are: singly linked list, doubly linked list, and circular linked list.
- How linked lists are stored: Nodes in a linked list are stored in a scattered manner in memory and linked together via pointers.
- How insertion, deletion, modification, and retrieval are performed in linked lists.
- Performance analysis of arrays versus linked lists in different scenarios.

**This encompasses the basic knowledge of linked lists without the complexity of a textbook.**

## Classic Linked List Problems

### Dummy Head Node

In the article [0203.Remove Linked List Elements](https://keetcoder.com/problems/0203.remove-linked-list-elements.html), we explain an important technique for operating on linked lists: the dummy head node.

One major problem with linked lists is that you often need to find the previous node to operate on the current node. This creates an awkward situation for the head node, as it does not have a preceding node.

**Each time when dealing with the head node, a special case must be made. Thus, using the dummy head node technique can solve this issue.**

In the article [0203.Remove Linked List Elements](https://keetcoder.com/problems/0203.remove-linked-list-elements.html), I provide code with and without the dummy head node, allowing you to compare and notice the advantages of using a dummy head node.

### Basic Operations on Linked Lists

In [0707.Design Linked List](https://keetcoder.com/problems/0707.design-linked-list.html), we practice the five common operations of linked lists by designing one:

- Getting the value of the index-th node in the linked list.
- Inserting a node at the beginning of the linked list.
- Inserting a node at the end of the linked list.
- Inserting a node before the index-th node of the linked list.
- Deleting the index-th node from the linked list.

**By solving this problem, you can master basic operations on linked lists and will no longer find manipulation confusing.**

I also use the dummy head node technique here. When reviewing, you can take a look at the code.

### Reversing a Linked List

In [0206.Reverse Linked List](https://keetcoder.com/problems/0206.reverse-linked-list.html), we discuss how to reverse a linked list.

Since the code for reversing a linked list is relatively straightforward, some might just memorize it, yet implementation can still easily go wrong.

Reversing a linked list is a high-frequency interview problem, testing the interviewee's proficiency with linked list operations.

In [this article](https://keetcoder.com/problems/0206.reverse-linked-list.html), I provide two methods for reversal: iterative and recursive.

It is recommended to thoroughly understand the iterative approach first, then proceed to the recursive method, as recursion can be tricky. If the iterative approach is not clear, recursion will likely be a challenge.

**Focus on understanding the process of reversing a linked list through the iterative method first!**

### Removing the N-th Node from the End

In [0019.Remove Nth Node From End of List](https://keetcoder.com/problems/0019.remove-nth-node-from-end-of-list.html) we employ the dummy head node and the two-pointer technique to remove the n-th node from the end of the list.

### Intersection of Linked Lists

In [Intersection of Two Linked Lists](https://keetcoder.com/problems/intersection-of-two-linked-lists.html), two pointers are used to find the intersection point of two linked lists (where the reference is identical, i.e., the memory address is completely identical at the intersection).

### Linked List Cycle

In [0142.Linked List Cycle II](https://keetcoder.com/problems/0142.linked-list-cycle-ii.html), we discuss how to detect a cycle in a linked list and how to find the entry point of the cycle.

This problem is quite challenging in the realm of linked lists. However, the code is quite concise, relying on some mathematical proofs.

## Summary

![](https://file1.kamacoder.com/i/algo/链表总结.png)

This diagram was created by [Hailuo Ren](https://wx.zsxq.com/dweb2/index/footprint/844412858822412), a member of the [Keetcoder Knowledge Planet](https://www.keetcoder.com/other/kstar.html), and is very well-summarized, so I'm sharing it with everyone.

Testing linked list operations is essentially testing pointer operations, which is a common type in interviews.

In the linked list section, we start by introducing [linked list theoretical knowledge](https://keetcoder.com/problems/0203.remove-linked-list-elements.html), followed by classic problems to illustrate the following concepts:

1. [Linked List Basics](https://keetcoder.com/problems/linked-list-basics.html)
2. [The Technique of Dummy Head Nodes](https://keetcoder.com/problems/0203.remove-linked-list-elements.html)
3. [Insertion, Deletion, Modification, and Retrieval in Linked Lists](https://keetcoder.com/problems/0707.design-linked-list.html)
4. [Reversing a Linked List](https://keetcoder.com/problems/0206.reverse-linked-list.html)
5. [Removing the N-th Node from the End](https://keetcoder.com/problems/0019.remove-nth-node-from-end-of-list.html)
6. [Intersection of Linked Lists](https://keetcoder.com/problems/intersection-of-two-linked-lists.html)
7. [Detecting and Locating Cycles in a Linked List](https://keetcoder.com/problems/0142.linked-list-cycle-ii.html)
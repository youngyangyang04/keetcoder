# The Theoretical Foundation of Stacks and Queues

I believe everyone is familiar with the principle of stacks and queues: queues are first-in-first-out, and stacks are first-in-last-out.

As shown in the figure:

![Stack and Queue Theory 1](https://file1.kamacoder.com/i/algo/20210104235346563.png)

Here I list four questions about stacks that you can think about. The following questions are based on C++ as an example, so if you are using other programming languages, consider how stacks and queues work in the language you are using.

1. Is `stack` a container in C++?
2. Which version of the STL does the `stack` we use belong to?
3. How is the `stack` implemented in the STL we use?
4. Does `stack` provide iterators to traverse the `stack` space?

I believe these four questions are not so easy to answer, because some people use data structures only superficially; when asked in depth, they may have a vague understanding.

Some might only know that stack and queue are such data structures, but do not know their underlying implementation or the relationship between the stack, the queue, and the STL.

So here I will go over the basics again.

First, you must know that stack and queue are two data structures within the STL (C++ Standard Library).

The C++ Standard Library has multiple versions. To understand the principles of the stack and queue implementations, we need to know which version of the STL we are using.

Let me introduce three of the most common STL versions:

1. HP STL
   Other versions of C++ STL are generally implemented based on HP STL, which is the first implementation version of the C++ STL, and it is open-source.

2. P.J.Plauger STL
   This was implemented by P.J.Plauger based on HP STL and was adopted by the Visual C++ compiler; it is not open-source.

3. SGI STL
   This was implemented by Silicon Graphics Computer Systems based on HP STL and was adopted by the C++ compiler GCC in Linux. SGI STL is open-source software with highly readable source code.

The stack and queue data structures introduced next are from SGI STL. Knowing the version used allows us to understand the corresponding underlying implementation.

Let's talk about stacks. Stacks follow the first-in-last-out rule, as shown in the figure:

![Stack and Queue Theory 2](https://file1.kamacoder.com/i/algo/20210104235434905.png)

Stacks provide interfaces such as `push` and `pop`. All elements must comply with the first-in-last-out rule, so stacks do not provide traversal functions or iterators. Unlike `set` or `map`, stacks do not provide iterators to traverse all elements.

**The stack performs all its tasks based on its underlying container and provides a unified interface externally. The underlying container is plug-and-play (meaning that we can control which container to use to implement the stack's function).**

Therefore, in the STL, stacks are often classified as container adapters rather than containers.

So, what container is the STL stack implemented with?

As can be seen from the diagram below, the internal structure of a stack can be implemented in multiple ways: vector, deque, or list, primarily as an array or linked list implementation.

![Stack and Queue Theory 3](https://file1.kamacoder.com/i/algo/20210104235459376.png)

**In the commonly used SGI STL, if the underlying implementation is not specified, `deque` is the default underlying structure for the stack.**

A `deque` is a double-ended queue; by sealing one end and opening the other, you can achieve the stack's logic.

**In SGI STL, the queue's underlying implementation also defaults to using `deque`.**

We can also specify `vector` as the stack's underlying implementation. The initialization statement is as follows:

```cpp
std::stack<int, std::vector<int> > third;  // A stack using vector as the underlying container
```

The features of the stack are similar for queues.

Queues, which are first-in-first-out data structures, similarly do not allow traversal behavior and do not provide iterators. **In SGI STL, the queue also defaults to using `deque` as its underlying structure.**

You can also specify `list` as the underlying implementation by initializing a queue as follows:

```cpp
std::queue<int, std::list<int>> third; // Define a queue with list as the underlying container
```

Therefore, in the STL, queues are also classified as container adapters rather than containers.

I've discussed the situation in C++. If you are using other languages, you should also think about the underlying implementation of stacks and queues. Do not stop at the surface level understanding of data structures; dig deeper into their internal principles to build a solid foundation.
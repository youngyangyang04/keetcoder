# Stack and Queue Summary

## Theoretical Foundations of Stack and Queue

First, in [Stack and Queue Fundamentals](https://keetcoder.com/problems/stack-and-queue-fundamentals.html), we explained the theoretical foundations of stacks and queues.

It mentioned four core questions:

1. Are `stack` and `queue` in C++ containers?
2. Which version of STL do the `stack` and `queue` we use belong to?
3. How are `stack` and `queue` implemented in the STL we use?
4. Do `stack` and `queue` provide iterators for space traversal?

I believe these questions apply not only to C++; when using other programming languages, you can also consider how stacks and queues are implemented.

Stacks and queues are some of the most familiar data structures to us, but their underlying implementation is often less clear to many students, which is essentially a foundational issue.

You could pose an interview question: Are the elements in a stack continuously distributed in memory?

There are two pitfalls in this question:

* Pitfall 1: Stack is a container adapter; different underlying containers can lead to non-continuous distribution of stack data in memory.
* Pitfall 2: By default, the underlying container is `deque`, so how are `deque` data distributed in memory? The answer is: discontinuously, as will be discussed regarding `deque` below.

This makes it a good question for assessing the candidate's fundamental knowledge.

It's essential to pay great attention to these details!

After understanding the basics of stacks and queues, you can practice stack and queue operations using [0232.Implement Queue using Stacks](https://keetcoder.com/problems/0232.implement-queue-using-stacks.html) and [0225.Implement Stack using Queues](https://keetcoder.com/problems/0225.implement-stack-using-queues.html).

Notably, in [0225.Implement Stack using Queues](https://keetcoder.com/problems/0225.implement-stack-using-queues.html), you only need one queue.

**When simulating the popping of stack elements using one queue, you only need to re-add the elements at the front of the queue (excluding the last element) to the end of the queue. At this point, popping elements will follow the stack's order.**

## Classic Stack Problems

### Stack Application in Systems

If you recall the principles of compilation, the logic for handling brackets, braces, etc., in lexical analysis by the compiler uses the stack data structure.

Another example is the `cd` command in the Linux system, which you're likely very familiar with.

```
cd a/b/c/../../
```

This command eventually reaches the `a` directory. How does the system know it entered the `a` directory? This is an application of stacks. **This is also a problem on LeetCode, titled 71. Simplify Path, which you can try if you have time.**

**The implementation of recursion is a stack: each recursive call pushes the function's local variables, parameter values, and return address onto the call stack**, and when the recursion returns, these elements are popped from the stack, which is why recursion can return to the previous layer.

Thus, stacks have widespread applications in the computing field.

Some students often wonder about the usefulness of learning these data structures since they aren't used in developing software. Most of them refer to visual software like apps, websites, etc., which are the topmost applications, while the implementation of many underlying features relies on basic data structures and algorithms.

**Therefore, the application of data structures and algorithms is often hidden in places that aren't visible to us!**

### Parentheses Matching Problem

In [0020.Valid Parentheses](https://keetcoder.com/problems/0020.valid-parentheses.html), we explained the parentheses matching problem.

**Parentheses matching is a classic problem solved using stacks.**

It's recommended to analyze the mismatched situations before writing code. If you don't analyze before getting started, your code will likely have many issues.

Let's analyze the three types of mismatches:

1. The first situation is where there are extra left brackets in the string, causing a mismatch.
2. The second situation is where the brackets are not extra, but their types do not match.
3. The third situation is where there are extra right brackets in the string, causing a mismatch.

Here are some tips: when matching left brackets, push the right brackets onto the stack first. Then you only need to compare the current element with the top of the stack, which is simpler than pushing the left brackets first.

### String Deduplication Problem

In [1047.Remove All Adjacent Duplicates In String](https://keetcoder.com/problems/1047.remove-all-adjacent-duplicates-in-string.html), we discussed the string deduplication problem.

The idea is to place the string into a stack sequentially, then pop the stack if they are the same, leaving only consecutive non-identical elements in the stack at the end.

### Reverse Polish Notation Problem

In [0150.Evaluate Reverse Polish Notation](https://keetcoder.com/problems/0150.evaluate-reverse-polish-notation.html), we discussed evaluating reverse Polish notation.

In this problem, each subexpression yields a result, which is then used for further operations. **This is akin to a process of eliminating adjacent strings, similar to the game of pairing in [1047.Remove All Adjacent Duplicates In String](https://keetcoder.com/problems/1047.remove-all-adjacent-duplicates-in-string.html).**

## Classic Queue Problems

### Sliding Window Maximum Problem

In [0239.Sliding Window Maximum](https://keetcoder.com/problems/0239.sliding-window-maximum.html), we introduced a data structure: the monotonic queue.

This problem is relatively complex. If you encounter it for the first time, you may need to review it multiple times.

The main idea is that **the queue doesn't need to maintain all the elements in the window; it only needs to keep elements that might become the maximum in the window while ensuring the elements in the queue are sorted in descending order.**

This descending order-maintained queue is called a **monotonic queue, i.e., a queue that is either monotonic decreasing or monotonic increasing. C++ does not directly support monotonic queues, so we need to implement one ourselves.**

Furthermore, **don't assume that the implemented monotonic queue merely sorts the numbers within the window. If it did, how would it differ from a priority queue?**

When designing a monotonic queue, ensure that `pop` and `push` operations follow these rules:

1. `pop(value)`: If the element removed from the window, `value`, equals the exit element of the monotonic queue, then the queue pops the element; otherwise, no action is taken.
2. `push(value)`: If the pushed element `value` is greater than the entry element's value, then the queue pops the entry element until the `value` is less than or equal to the entry element's value.

Following these rules, each time the window moves, simply querying `que.front()` will return the maximum value of the current window.

Some may still find the monotonic queue confusing. Firstly, understand that **the `pop` and `push` interfaces of the monotonic queue in the solution apply only to this problem.**

**Monotonic queues aren't static and have different implementations in different contexts**, with the core principle being to ensure the queue is either monotonic decreasing or increasing.

**Don't assume the monotonic queue implementation in this problem is a fixed method.**

We use a `deque` as the underlying data structure for the monotonic queue. In C++, `deque` is the default underlying container for `stack` and `queue` (as discussed earlier), and while `deque` can expand at both ends, its elements aren't strictly continuously distributed.

### Top K Frequent Elements

In [0347.Top K Frequent Elements](https://keetcoder.com/problems/0347.top-k-frequent-elements.html), we discussed finding the top K frequent elements.

This introduced another type of queue: the **priority queue**.

What is a priority queue?

Actually, **it's a heap disguised as a queue** because the priority queue exposes the interface in such a way that elements can only be fetched from the head and added to the tail, with no other way to access elements, making it appear as a queue.

Additionally, the priority queue internally sorts elements according to their weights. How does it sort them?

By default, `priority_queue` uses a `max-heap` to sort the elements. This max-heap is represented as a `complete binary tree` using a `vector`.

What is a heap?

**A heap is a complete binary tree where each node's value is not less than (or not greater than) the values of its left and right children.** If the parent node is greater than or equal to its children, it's a max-heap; if smaller, it's a min-heap.

Thus, the often-mentioned max-heap (where the heap's head is the largest element) and min-heap (where the heap's head is the smallest element) can be easily used. If you don't want to implement these yourself, just use `priority_queue`. The internal implementations are the same. Sorting from smallest to largest produces a min-heap; from largest to smallest yields a max-heap.

This problem requires **using a priority queue to sort part of the frequency data.** Note that this is mainly about sorting part of the data rather than all of it!

Therefore, the sorting process has a time complexity of $O(\log k)$, and the overall algorithm has a time complexity of $O(n\log k)$.

## Conclusion

In the stack and queue series, we emphasize the fundamentals of stacks and queues, which are often overlooked by many.

The higher the level of abstraction in the language, the easier it is to overlook its underlying implementation. C++, being relatively close to the bottom layer, helps understand this better.

We practiced basic operations of stacks and queues through implementing queues with stacks and vice versa.

Furthermore, through parentheses matching, string deduplication, and reverse Polish notation problems, we discussed the system applications and techniques concerning stacks.

By covering how to find the sliding window maximum and the top K frequent elements, we introduced two types of queues: monotonic and priority queues, which are powerful tools in solving problems specific to particular scenarios.

This concludes our summary of stacks and queues. Next, Carl will lead you into a new chapter. Keep up the good work!
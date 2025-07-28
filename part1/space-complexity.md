# Space Complexity Analysis

So far, space complexity has not been discussed much, but I plan to cover it gradually. The content is not difficult, and you can get an overview by reading the article once.

What is space complexity?

It is a measure of the amount of memory space an algorithm occupies during its execution, denoted as \( S(n)=O(f(n)) \).

Space Complexity, written as \( S(n) \), is also represented using big O notation. By utilizing space complexity, we can estimate in advance how much memory a program will need during its execution.

There are two common related questions about space complexity:

1. Is space complexity considering the size of the program (executable file)?

Many people often confuse the memory size required to run a program with the size of the program itself. Here, it is emphasized that **space complexity is concerned with the size of memory occupied during program execution, not the size of the executable file.**

2. Does space complexity precisely calculate the memory occupied by a program during execution?

Do not assume that space complexity provides an exact measure of memory usage by a program. There are many factors that can affect the actual memory usage, such as memory alignment by the compiler, the underlying implementation of programming language containers, among others.

So space complexity is largely an advance estimate of the program's memory usage.

Regarding space complexity, you might have encountered errors like exceeding the memory limit on OJ (online judge) platforms. Generally, OJ has a limit on the memory usage of the program during its execution.

To avoid exceeding memory limits, we also need to have a rough estimate of the memory requirement of the algorithm.

Similarly, in engineering practice, computer memory space is not unlimited. Engineers need to have a general estimate of the memory usage of software during runtime, which requires an analysis of the algorithm's space complexity.

Let's take a look at an example, when is the space complexity $O(1)$? Consider the following C++ code:

```cpp
int j = 0;
for (int i = 0; i < n; i++) {
    j++;
}
```

The space required does not change with the increase of \( n \). Therefore, the space complexity of this algorithm is constant, denoted as \( O(1) \).

When is the space complexity \( O(n) \)?

When the space consumption grows linearly with the input parameter \( n \), it is denoted as \( O(n) \). Consider the following C++ code:

```cpp
int* a = new int(n);
for (int i = 0; i < n; i++) {
    a[i] = i;
}
```

We define an array whose size is \( n \). Although there is a for loop, no new space is allocated afterward. Thus, the space complexity is primarily determined by the first line. The space grows linearly with \( n \), i.e., \( O(n) \).

Other complexities like \( O(n^2) \), \( O(n^3) \), etc., can be derived similarly. **Now, think about when the space complexity is \( O(\log n) \)?**

Space complexity being \( O(\log n) \) is indeed somewhat special. In fact, **recursive functions can have space complexities of \( O(\log n) \).**

As for how to determine the space complexity of recursion, I will write an article specifically to introduce it, so stay tuned!

-----------------------
<div align="center"><img src='https://file1.kamacoder.com/i/algo/01二维码.jpg' width=450></img></div>
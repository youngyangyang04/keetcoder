# Analysis of Time and Space Complexity in Recursive Algorithms

In a previous discussion on [Analyzing the Time Complexity of Recursive Algorithms Using an Interview Question](https://keetcoder.com/前序/通过一道面试题目，讲一讲递归算法的时间复杂度！.html), we delved into how to analyze the time complexity of recursive algorithms, though space complexity was not covered.

In this article, we will further analyze recursive algorithms in terms of both time and space complexity by examining the Fibonacci sequence and binary search. A detailed read will provide you with refreshed insights into recursion!

## Performance Analysis of Recursively Calculating the Fibonacci Sequence

Let's first look at the recursive implementation of calculating Fibonacci numbers.

```CPP
int fibonacci(int i) {
       if(i <= 0) return 0;
       if(i == 1) return 1;
       return fibonacci(i-1) + fibonacci(i-2);
}
```

Recursive algorithms usually involve concise code with seemingly minimal storage requirements. However, they might consume significant memory at runtime.

### Time Complexity Analysis

Let's examine the time complexity of this recursive algorithm for Fibonacci numbers.

In discussing the time complexity of recursion, we noted that it essentially boils down to: **number of recursive calls * time complexity of each call**.

It is clear that each recursive call here is an O(1) operation. To understand the number of recursive calls, let's visualize the recursion tree when the input is i = 5:

![递归空间复杂度分析](https://file1.kamacoder.com/i/algo/20210305093200104.png)

From the diagram, we can observe that f(5) is derived from f(4) and f(3), while f(4) results from f(3) and f(2), and so forth.

In this binary tree, each node represents a single recursive call. How many nodes does this tree contain?

As previously mentioned, a binary tree of depth k (with the root node at depth 1) can have a maximum of 2^k - 1 nodes.

Thus, the time complexity of this recursive algorithm is O(2^n), which is notably large, causing the runtime to increase exponentially with n.

Let's conduct an experiment for a tangible demonstration.

Below is some C++ code to measure the execution time of the recursive Fibonacci calculation upon input of n.

```CPP
#include <iostream>
#include <chrono>
#include <thread>
using namespace std;
using namespace chrono;
int fibonacci(int i) {
       if(i <= 0) return 0;
       if(i == 1) return 1;
       return fibonacci(i - 1) + fibonacci(i - 2);
}
void time_consumption() {
    int n;
    while (cin >> n) {
        milliseconds start_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );

        fibonacci(n);

        milliseconds end_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );
        cout << milliseconds(end_time).count() - milliseconds(start_time).count()
            <<" ms"<< endl;
    }
}
int main()
{
    time_consumption();
    return 0;
}
```

Here are the experimental results:

Utilizing a 2015 MacPro for testing, with CPU specifications: `2.7 GHz Dual-Core Intel Core i5`

Test data is as follows:

* n = 40, duration: 837 ms
* n = 50, duration: 110306 ms

Clearly, the exponentially growing complexity of O(2^n) is considerably high.

Thus, while this algorithm for computing Fibonacci numbers seems succinct, its time complexity is significantly high, and this approach is generally not recommended.

The main culprit here is the dual recursion, leading to exponential time complexity.

```CPP
return fibonacci(i-1) + fibonacci(i-2);
```

Can we optimize this recursive algorithm to reduce the number of recursive calls?

Consider the following alternative code:

```CPP
// Version 2
int fibonacci(int first, int second, int n) {
    if (n <= 0) {
        return 0;
    }
    if (n < 3) {
        return 1;
    }
    else if (n == 3) {
        return first + second;
    }
    else {
        return fibonacci(second, first + second, n - 1);
    }
}
```

Here, first and second are used to record the two current sum values, eliminating the double recursion.

As each recursion reduces n by one, the time complexity is O(n).

Similarly, the recursion depth remains n, and the space required by each recursion is constant, thus retaining a space complexity of O(n).

The complexity of code (Version 2) is as follows:

* Time complexity: O(n)
* Space complexity: O(n)

Let's verify with some timing tests:

```CPP
#include <iostream>
#include <chrono>
#include <thread>
using namespace std;
using namespace chrono;
int fibonacci_3(int first, int second, int n) {
    if (n <= 0) {
        return 0;
    }
    if (n < 3) {
        return 1;
    }
    else if (n == 3) {
        return first + second;
    }
    else {
        return fibonacci_3(second, first + second, n - 1);
    }
}

void time_consumption() {
    int n;
    while (cin >> n) {
        milliseconds start_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );

        fibonacci_3(1, 1, n);

        milliseconds end_time = duration_cast<milliseconds >(
            system_clock::now().time_since_epoch()
        );
        cout << milliseconds(end_time).count() - milliseconds(start_time).count()
            <<" ms"<< endl;
    }
}
int main()
{
    time_consumption();
    return 0;
}

```

Test results are as follows:

* n = 40, duration: 0 ms
* n = 50, duration: 0 ms

You can sense the difference now!!

### Space Complexity Analysis

Having discussed the time complexity of this recursive code, what about calculating its space complexity? Here's a guiding formula: **Space complexity of a recursive algorithm = space complexity per recursive call * recursion depth**

Why consider recursion depth?

Because each recursion's space is pushed onto the call stack (an internal memory management data structure similar in principle to an algorithmic stack). Once a recursion ends, the stack releases that recursion's data. Hence, the stack's maximum depth equals the recursion depth.

Let's analyze the space complexity of this recursive code. Each recursive step requires the same amount of space; thus, the space needed per recursion is constant and independent of n. Therefore, the space complexity for each recursive call is $O(1)$.

Considering the recursion depth, as illustrated:

![递归空间复杂度分析](https://file1.kamacoder.com/i/algo/20210305094749554.png)

When calculating the nth Fibonacci number, the recursion call stack depth is n.

Since each recursion has a space complexity of O(1), and the call stack depth is n, this recursive code has an overall space complexity of O(n).

```CPP
int fibonacci(int i) {
       if(i <= 0) return 0;
       if(i == 1) return 1;
       return fibonacci(i-1) + fibonacci(i-2);
}
```

Finally, let's analyze the performance of different methods for calculating the Fibonacci sequence:

![递归的空间复杂度分析](https://file1.kamacoder.com/i/algo/20210305095227356.png)

It's evident that while recursive algorithms may not always offer optimal performance for calculating Fibonacci numbers, they certainly simplify code complexity.

### Performance Analysis of Binary Search (Recursive Implementation)

Let's examine a recursive implementation of binary search for its performance analysis.

```CPP
int binary_search( int arr[], int l, int r, int x) {
    if (r >= l) {
        int mid = l + (r - l) / 2;
        if (arr[mid] == x)
            return mid;
        if (arr[mid] > x)
            return binary_search(arr, l, mid - 1, x);
        return binary_search(arr, mid + 1, r, x);
    }
    return -1;
}
```

It's well-known that the time complexity of binary search is O(logn). But what about the space complexity of recursive binary search?

We again look at **space complexity per recursive call and recursion depth**.

The space complexity per recursive call mainly involves the arr array passed as a parameter. However, in C/C++, when passing an array to a function, only the address of the first element is passed, not a copy of the entire array.

**This means that each recursion layer shares the same address space for the array**, making the space complexity per recursive call a constant, i.e., O(1).

Considering recursion depth, the depth of recursive binary search is logn. Thus, the space complexity of this code is 1 * logn = O(logn).

Note that you should be aware of whether the language you're using copies the entire value or just the address when passing function parameters. If it involves copying the entire value, the space complexity for this binary method would be O(nlogn).

## Summary

In this chapter, we thoroughly analyzed the space complexity of recursive implementations in calculating the Fibonacci sequence and binary search, alongside discussing time complexity.

The time complexities of two recursive implementations for the Fibonacci sequence starkly differ, and experimental results verify that a time complexity of O(2^n) is highly time-consuming.

This article should help deepen your understanding of the time and space complexities of recursive algorithms.

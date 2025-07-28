# Explain the Time Complexity of Recursive Algorithms Through an Interview Question!

> This article uses an interview question and an interview scenario to thoroughly analyze how to determine the time complexity of a recursive algorithm.

I believe many students find the time complexity of recursive algorithms somewhat vague. This article aims to clarify the concept.

**For the same question using a recursive algorithm, some students write code with a time complexity of O(n), while others manage to write O(log n) code.**

Why is that?

If you don't have a deep understanding of the time complexity of recursion, this can happen!

Here, I will use a simple interview question to simulate an interview scenario and guide you through analyzing the time complexity of a recursive algorithm, finally finding the optimal solution. We'll see how the same recursive approach can result in O(n) code.

Interview Question: Calculate x raised to the power of n

Think about how you would write code for such a simple question. The most intuitive way might be using a for loop to get the result, as shown below:

```CPP
int function1(int x, int n) {
    int result = 1;  // Note: any number raised to the power of 0 equals 1
    for (int i = 0; i < n; i++) {
        result = result * x;
    }
    return result;
}
```
The time complexity here is O(n). At this point, the interviewer might ask if there is a more efficient algorithm.

**If you have no ideas at this moment, don't say: I don't know or I can't.**

You can discuss with the interviewer and ask, “Can you provide a hint?” The interviewer might hint, “Consider a recursive algorithm.”

You can then write a recursive solution like the one below to solve this problem.

```CPP
int function2(int x, int n) {
    if (n == 0) {
        return 1; // return 1 because anything to the power of 0 is 1
    }
    return function2(x, n - 1) * x;
}
```
The interviewer asks: "What is the time complexity of this code?”

Some students might immediately think of O(log n) when they see recursion, but that's not necessarily the case. The essence of time complexity in recursion is determined by: **the number of recursive calls multiplied by the operations conducted in each call**.

Now, let's look at the code. How many times is it recursive?

Each time you subtract 1 from n, it recurs n times, giving a time complexity of O(n). Each recursion performs a multiplication operation with a constant time complexity of O(1), so the time complexity of this solution is n × 1 = O(n).

This time complexity does not meet the interviewer's expectations. Next, the following recursive algorithm code is written:

```CPP
int function3(int x, int n) {
    if (n == 0) return 1;
    if (n == 1) return x;

    if (n % 2 == 1) {
        return function3(x, n / 2) * function3(x, n / 2) * x;
    }
    return function3(x, n / 2) * function3(x, n / 2);
}

```

Upon seeing this, the interviewer smiles slightly and asks: “What is the time complexity of this code?” At this point, some students may start pondering.

Let's analyze. First, how many times does it recurse? You can abstract this recursion into a complete binary tree. The algorithm the student just wrote can be represented by a complete binary tree (for simplicity, choose n as an even number, 16), as shown in the diagram:

![Time Complexity of Recursive Algorithm](https://file1.kamacoder.com/i/algo/20201209193909426.png)

This tree represents calculating x to the power of n, where n is 16. How many multiplications are performed when n is 16?

Each node in this tree represents a recursion and a multiplication operation, so the number of recursive calls is equal to the number of nodes in the tree.

Those familiar with binary trees know how to calculate the number of nodes in a complete binary tree. The number of nodes in this complete binary tree is `2^3 + 2^2 + 2^1 + 2^0 = 15`. Notice: **This is indeed a geometric series sum formula, and this conclusion frequently appears in binary tree interview questions**.

So, if we are calculating x to the power of n, how many nodes does this recursive tree have? As shown in the illustration below: (where m represents the depth, starting from 0)

![Calculate Time Complexity Using Recursion](https://file1.kamacoder.com/i/algo/20200728195531892.png)

**The time complexity, after ignoring the constant term `-1`, remains O(n).** That's right, the time complexity is still O(n)!

At this point, the interviewer will say, “This recursive algorithm is still O(n).” Clearly, it hasn't met the interviewer's expectations.

So, how can you write a recursive algorithm with a time complexity of O(log n)?

Think back to the previous recursive algorithm code. Is there redundancy? There are actually some repeated calculations.

Then the following recursive algorithm code is written:

```CPP
int function4(int x, int n) {
    if (n == 0) return 1;
    if (n == 1) return x;
    int t = function4(x, n / 2); // Compared to function3, this line extracts this recursive operation
    if (n % 2 == 1) {
        return t * t * x;
    }
    return t * t;
}
```

Now, what is the time complexity of this code?

We still examine how many times it recurses. Here, there's only a single recursive call, and it's n/2 each time. So, this recursive function is called a logarithmic number of times: log to the base 2 of n.

**In each recursive call, there is one multiplication operation, a constant-time operation, so this recursive algorithm truly has a time complexity of O(log n).**

At this point, students have written such a code and clearly explained the time complexity, which will likely satisfy the interviewer.

# Summary

For the time complexity of recursion, it might sometimes confuse beginners, and even seasoned problem solvers might find it tricky.

**In this article, I've used a very simple interview question: Calculate x to the power of n, to analyze the time complexity of recursive algorithms step by step. Don't automatically think of O(log n) when you see recursion!**

Different students might write O(log n) or O(n) code using recursion for the same problem.

For the recursive solution like function3, it's easy to misinterpret it as having a time complexity of O(log n), whereas it's actually O(n)!

```CPP
int function3(int x, int n) {
    if (n == 0) return 1;
    if (n == 1) return x;
    if (n % 2 == 1) {
        return function3(x, n / 2) * function3(x, n / 2) * x;
    }
    return function3(x, n / 2) * function3(x, n / 2);
}
```
As you can see, this question is extremely simple but also tests the depth of understanding in algorithms, especially recursion, which is why I've used it in interviews before. That's why this scenario is written so vividly.

In major company interviews, they love to test candidates' algorithmic proficiency through "simple problems." Note that these "simple problems" aren't necessarily simple!

If you've read this article thoroughly, I believe you will have a newfound understanding of recursive algorithms. The same problem, the same recursion, but the efficiency varies!

-----------------------
<div align="center"><img src='https://file1.kamacoder.com/i/algo/01二维码.jpg' width=450> </img></div>
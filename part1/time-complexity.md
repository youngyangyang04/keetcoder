# Everything You Didn't Know About Time Complexity Is Here!

I believe every programmer has encountered time complexity, but many may have a somewhat vague understanding of it. So it's time to have an in-depth analysis of time complexity.

This article will analyze time complexity from the following six points:

* What exactly is time complexity?
* What is Big O?
* Differences in data scales
* Simplifying complex expressions
* What's the base of log in O(log n)?
* An example

This might be the most comprehensive analysis of time complexity you've ever seen.

## What Exactly Is Time Complexity?

**Time complexity is a function that qualitatively describes the runtime of an algorithm.**

In software development, time complexity is a convenient way for developers to estimate the approximate runtime of a program.

How can we estimate the runtime of a program? You typically estimate the number of operations an algorithm performs as a representative of the time consumed, with the assumption that each operation takes the same amount of time on a CPU.

Assuming the problem size of the algorithm is n, the number of operations is represented by a function f(n). As the data size n increases, the growth rate of the algorithm's execution time is the same as the growth rate of f(n). This is called the asymptotic time complexity of the algorithm, usually referred to as time complexity and denoted by O(f(n)).

## What Is Big O?

So what does Big O mean? When we talk about time complexity, **everyone knows O(n), O(n^2), but can't quite explain what Big O is.**

The introduction to algorithms explains: **Big O is used to denote an upper bound**, representing the upper bound of the worst-case runtime for any input data of the algorithm.

For example, in the case of insertion sort, we often say its time complexity is O(n^2).

The form of input data significantly affects the program's runtime. In an already sorted dataset, the time complexity might be O(n), but if the data is in reverse order, insertion sort has a time complexity of O(n^2). Therefore, for all inputs, the worst-case time complexity is O(n^2), and hence we say the time complexity of insertion sort is O(n^2).

Similarly, consider quicksort. We know quicksort is O(nlogn), but for already sorted data, its time complexity becomes O(n^2). **Thus, strictly speaking from the definition of Big O, the time complexity of quicksort should be O(n^2)**.

**However, we still say quicksort has a time complexity of O(nlogn). This is a conventional understanding in the industry, where O refers to typical rather than strict upper bounds.** As shown in the diagram:
![Usual time complexity representation](https://file1.kamacoder.com/i/algo/20200728185745611-20230310123844306.png)

We are mainly concerned with the general form of the data.

**When asked about the time complexity of an algorithm in an interview, it generally refers to the average case.** But if the interviewer dives deeper into the implementation and performance of an algorithm, remember that different data sets lead to different time complexities; this point is crucial to keep in mind.

## Differences in Data Scales

The following diagram shows the differences in time complexity for various algorithms at different data input scales.

![Differences in data scales](https://file1.kamacoder.com/i/algo/20200728191447384-20230310124015324.png)

When deciding which algorithms to use, it's not always best to choose the one with the lowest time complexity (since simplified time complexity ignores constant terms, etc.). Consider the data scale. If the data scale is small, even an O(n^2) algorithm might be more suitable than O(n) (when there are constant terms involved).

As in the diagram, O(5n^2) is clearly more optimal than O(100n) before n reaches 20 and takes the least amount of time.

So why do we ignore constant terms when calculating time complexity? In other words, why is O(100n) considered O(n) time complexity, and O(5n^2) considered O(n^2), and why is O(n) assumed to be better than O(n^2)?

Here, it’s tied to the definition of Big O. **Because Big O signifies the time complexity when the data size reaches a certain point and is considerably large enough for the constant term co-efficients to become insignificant.**

For instance, in the diagram, 20 is that point. As long as n is greater than 20, the constant term coefficients become insignificant.

**Therefore, we often omit the constant term coefficients in time complexity calculations, assuming that data scales are typically large enough. Based on this assumption, the ranking of algorithm time complexities is as shown below:**

O(1) constant time < O(logn) logarithmic time < O(n) linear time < O(nlogn) linearithmic time < O(n^2) quadratic time < O(n^3) cubic time < O(2^n) exponential time.

But also consider large constants; if such constants are very large, like 10^7 or 10^9, then they cannot be ignored.

## Simplifying Complex Expressions

Sometimes, when calculating time complexity, we encounter complex expressions rather than simple O(n) or O(n^2). For instance:

```
O(2*n^2 + 10*n + 1000)
```

How do we describe this algorithm's time complexity? One approach is simplification.

Remove the additive constant terms in runtimes (since constant terms do not increase the computer's operation count as n grows).

```
O(2*n^2 + 10*n)
```

Remove constant coefficients (as we've previously discussed why constant terms can be omitted).

```
O(n^2 + n)
```

Only keep the highest term, and remove terms of lower order, leading to:

```
O(n^2)
```

If this step is difficult to understand, factor out n, resulting in O(n(n+1)), which after omitting the additive constant terms also results in:

```
O(n^2)
```

So finally, we say the algorithm's time complexity is O(n^2).

Alternatively, you can think of it in terms of upper bounds. When n is greater than 40, this complexity will always be less than O(3 × n^2), so O(2 × n^2 + 10 × n + 1000) < O(3 × n^2). After omitting constant coefficients, the final time complexity is also O(n^2).

## What's the Base of log in O(log n)?

When we say an algorithm's time complexity is log n, does it imply that it's the logarithm to the base 2 of n?

Not necessarily. It could be logarithm to the base 10 of n or to the base 20. **But we uniformly say log n, ignoring the base.**

Why can we do this? As illustrated in the diagram:

![Time complexity base](https://file1.kamacoder.com/i/algo/20200728191447349-20230310124032001.png)

Assuming there are two algorithms with time complexities represented by logarithms to the base 2 of n and to the base 10 of n, recall from high school mathematics that `log to the base 2 of n = log to the base 2 of 10 * log to the base 10 of n`.

The logarithm to the base 2 of 10 is a constant, and as discussed, we ignore constant coefficients when calculating time complexity.

In abstraction, log to the base i of n equals log to the base j of n in time complexity calculations, so we omit 'i' and simply call it log n.

This explanation helps clarify why we ignore the base.

## An Example

Let's analyze time complexity using an interview question: Find the two identical strings from n strings (assume there are only two identical strings).

What is the time complexity for using brute force? Is it O(n^2)?

Some might overlook the time consumption of string comparison. It's not as simple as comparing int-type numbers. Besides the n^2 iterations, string comparison still consumes m operations (where m is the length of the string), so the time complexity is O(m × n × n).

Let's consider another problem-solving approach.

First, sort the n strings in lexicographical order. Once sorted, the two identical strings will be adjacent. Then, iterate through the n strings once to find the identical pair.

Let's examine the time complexity of this algorithm: Quick sort has a time complexity of O(nlogn). Remember that strings have a length m, so every quick sort comparison involves m character comparison operations, resulting in O(m × n × log n).

Next, we need to iterate through the n strings to find the identical pair. Don't forget that string comparison is involved during iteration. Therefore, the total time complexity is O(m × n × log n + n × m).

Simplify O(m × n × log n + n × m) by factoring out m × n, resulting in O(m × n × (log n + 1)). Omitting the constant terms yields a final time complexity of O(m × n × log n).

Clearly, O(m × n × log n) is preferable to O(m × n × n)!

Thus, sorting the string set and then iterating once to find the identical strings is faster than using brute force.

This conclusion is derived through the analysis of the time complexities of the two methods.

**However, this is not necessarily the optimal solution for this problem. It is merely to illustrate the concept of time complexity.**

## Conclusion

This article discussed what time complexity is, what it is used for, and how data scale affects time complexity.

It also covered the often-overlooked definitions of Big O and the base of logs.

Lastly, it demonstrated how to simplify complex time complexities with a concrete example to tie together the content of the article.

I believe that after reading this article, your understanding of time complexity will be much deeper!
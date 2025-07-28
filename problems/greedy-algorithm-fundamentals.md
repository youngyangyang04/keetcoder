# What You Should Know About Greedy Algorithms!

The topic classification outline is as follows:

<img src='https://file1.kamacoder.com/i/algo/20210917104315.png' width=600 alt='Outline of Greedy Algorithms'> </img></div>

## What is Greediness

**The essence of greediness is choosing the local optimum at each stage to achieve the global optimum**.

This might sound abstract, so let's use an example:

For instance, you have a pile of cash, and you can take ten notes. To maximize the amount, how should you choose?

By choosing the largest each time, you end up taking the largest sum of money.

Choosing the largest each time is the local optimum, and the ultimate result of taking the largest sum is the global optimum.

Consider another example: you have a pile of boxes, and you have a knapsack with a volume of n. How to fill the knapsack as completely as possible? Choosing the largest box each time won't work. This is when you need dynamic programming. Dynamic programming will be explained in detail in the next series.

## The Pattern of Greediness (When to Use Greedy Algorithms)

Many learners struggle to determine if a problem requires a greedy approach. They wonder if there is a pattern to easily identify when to use one.

**Honestly, there is no fixed pattern for greedy algorithms.**

The only difficulty is determining how to achieve the overall optimum from the local optimum.

So, how can you tell if the local optimum leads to the global optimum? Are there any fixed strategies or patterns?

**Sorry, there aren't any!** It's about manually simulating the situation: if simulation shows it works, then try a greedy strategy; otherwise, it might require dynamic programming.

Some might ask how to verify if a greedy algorithm is applicable?

**The best strategy is to try finding counterexamples. If none come to mind, give the greedy approach a try.**

Some may feel that conclusions based on manual simulation and examples are unreliable and prefer strict mathematical proofs.

Generally, there are two mathematical methods to prove:

* Mathematical induction
* Proof by contradiction

Greedy explanations in textbooks can look like a pile of formulas that people might not even want to look at. Thus, mathematical proofs fall outside the scope of my explanations here. You are welcome to seek out resources if interested.

**In interviews, interviewers typically do not require candidates to prove the reasonableness of greediness; writing code that passes test cases or providing a reason that makes sense to you is enough.**

Here's an inappropriate example: I need to use `1 + 1 = 2`, but I must first prove why `1 + 1` equals `2`. It's rigorous but unnecessary.

Though extreme, this example showcases the idea: **when practicing or during interviews, if manual simulations suggest that local optimum could lead to a global optimum, and no counterexample is apparent, just try the greedy approach**.

**For example, in the earlier cash example, simulating taking the largest each time leads to the most cash. If you had to mathematically prove this, it extends beyond the realm of algorithm interviews, and one might consult specialized mathematics books!**

That’s why many people solve (accept) greedy problems without realizing they used a greedy algorithm. **Sometimes, greediness is merely common-sense reasoning, and the approach seems inherently correct!**

**When do you truly need a mathematical analysis during problem-solving?**

For instance, in the problem: [0142.Linked List Cycle II](https://keetcoder.com/problems/0142.linked-list-cycle-ii.html), without mathematical deduction, you can't locate the start of the cycle. Simply attempting without a proof might leave you clueless, and some mathematical deduction is genuinely necessary.

## General Problem-solving Steps for Greedy Algorithms

Greedy algorithm solving is generally divided into these four steps:

* Break down the problem into sub-problems
* Identify an appropriate greedy strategy
* Solve each sub-problem optimally
* Combine the local optimum solutions into a global solution

These steps are overly theoretical, and applying them in greedy problem-solving can feel somewhat "superfluous."  

When solving actual problems, just identify what the local optimum is, and if it can deduce the global optimum, that's often sufficient.

## Conclusion

This article outlines what greedy algorithms are and addresses the common concern about whether there are fixed patterns.

**Apologies, but greediness has no pattern—it's mainly common-sense reasoning coupled with finding counterexamples**.

Finally, the general greedy algorithm problem-solving steps presented here are somewhat abstract and lack the clearly defined patterns and templates seen in binary trees and backtracking algorithms.
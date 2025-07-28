# The Ultimate Summary of Dynamic Programming!

Now that 42 classic problems on dynamic programming with a total of 50 articles have been discussed, it is time to make a summary.

Regarding dynamic programming, in the first article of the topic [Dynamic Programming Fundamentals](https://keetcoder.com/problems/dynamic-programming-fundamentals.html), the five steps of dynamic programming were introduced and emphasized as crucial for solving dynamic programming problems!

These are the distilled pearls of wisdom Carl has gathered from completing over one hundred dynamic programming problems. If you've followed along with the "Coding Thoughts" series on dynamic programming, you'll deeply appreciate the significance of these five steps.

The five steps of dynamic programming are:

1. Define the dp array (dp table) and the meaning of its indices.
2. Determine the transition formula.
3. Initialize the dp array.
4. Decide on the order of traversal.
5. Deduce the dp array through examples.

At the start of the dynamic programming section, the problems discussed were relatively simple. Many readers mentioned that these simple problems seemed to be over-explained and could be solved directly by figuring out the transition formula.

**Carl's perspective has always been that simple problems are meant to reinforce methodology.** Simple problems can be tackled by intuition, but slightly more difficult problems are likely to defy such an approach.

Throughout the dynamic programming discussion, the importance of these five steps has consistently been highlighted.

Some readers believe that discovering the transition formula is the most challenging and crucial step, and once it's found, the rest follows easily.

**However, if you think this way, your understanding of dynamic programming is likely incomplete.**

In dynamic programming, if any of these steps are unclear, the problem can hardly be solved; even if it is, it hasn't been thoroughly understood, and the process feels foggy at best.

- If the specific meaning of the dp array is unclear, how can you discuss a transition formula? You may even make mistakes during initialization.
- For example, in [0063.Unique Paths II](https://keetcoder.com/problems/0063.unique-paths-ii.html), initialization is the key focus.
- If you've reviewed the knapsack series, especially the complete knapsack, the ordering of the two for loops can certainly confuse many people, while the transition formula is straightforward.
- As for the importance of deducing the dp array, it's almost always emphasized in each article within the dynamic programming section: when the program's output is incorrect, you must deduce the formula yourself to check it against the program's logs.

Great, let's revisit the content we've covered in the dynamic programming section.

## Basics of Dynamic Programming

- [Dynamic Programming Fundamentals](https://keetcoder.com/problems/dynamic-programming-fundamentals.html)
- [0509.Fibonacci Number](https://keetcoder.com/problems/0509.fibonacci-number.html)
- [0070.Climbing Stairs](https://keetcoder.com/problems/0070.climbing-stairs.html)
- [0746.Min Cost Climbing Stairs](https://keetcoder.com/problems/0746.min-cost-climbing-stairs.html)
- [0062.Unique Paths](https://keetcoder.com/problems/0062.unique-paths.html)
- [0063.Unique Paths II](https://keetcoder.com/problems/0063.unique-paths-ii.html)
- [0343.Integer Break](https://keetcoder.com/problems/0343.integer-break.html)
- [0096.Unique Binary Search Trees](https://keetcoder.com/problems/0096.unique-binary-search-trees.html)

## Knapsack Problem Series

<img src='https://file1.kamacoder.com/i/algo/动态规划-背包问题总结.png' width=500 alt='Knapsack Problem Outline'> </img></div>

- [Knapsack Theory 01 Knapsack-1](https://keetcoder.com/problems/knapsack-theory-01-knapsack-1.html)
- [Knapsack Theory 01 Knapsack-2](https://keetcoder.com/problems/knapsack-theory-01-knapsack-2.html)
- [0416.Partition Equal Subset Sum](https://keetcoder.com/problems/0416.partition-equal-subset-sum.html)
- [1049.Last Stone Weight II](https://keetcoder.com/problems/1049.last-stone-weight-ii.html)
- [0494.Target Sum](https://keetcoder.com/problems/0494.target-sum.html)
- [0474.Ones and Zeroes](https://keetcoder.com/problems/0474.ones-and-zeroes.html)
- [Knapsack Problem Theory Basics Complete Knapsack](https://keetcoder.com/problems/knapsack-problem-theory-basics-complete-knapsack.html)
- [0518.Coin Change II](https://keetcoder.com/problems/0518.coin-change-ii.html)
- [0377.Combination Sum IV](https://keetcoder.com/problems/0377.combination-sum-iv.html)
- [0070.Climbing Stairs Complete Knapsack Version](https://keetcoder.com/problems/0070.climbing-stairs-complete-knapsack-version.html)
- [0322.Coin Change](https://keetcoder.com/problems/0322.coin-change.html)
- [0279.Perfect Squares](https://keetcoder.com/problems/0279.perfect-squares.html)
- [0139.Word Break](https://keetcoder.com/problems/0139.word-break.html)
- [Knapsack Problem Theory Basics - Multiple Knapsack](https://keetcoder.com/problems/knapsack-problem-theory-basics---multiple-knapsack.html)
- [Knapsack Summary](https://keetcoder.com/problems/knapsack-summary.html)

## House Robbery Series

- [0198.House Robber](https://keetcoder.com/problems/0198.house-robber.html)
- [0213.House Robber II](https://keetcoder.com/problems/0213.house-robber-ii.html)
- [0337.House Robber III](https://keetcoder.com/problems/0337.house-robber-iii.html)

## Stock Series

<img src='https://file1.kamacoder.com/i/algo/股票问题总结.jpg' width=500 alt='Stock Problem Summary'> </img></div>

- [0121.Best Time to Buy and Sell Stock](https://keetcoder.com/problems/0121.best-time-to-buy-and-sell-stock.html)
- [Dynamic Programming-Stock Problem Summary](https://keetcoder.com/problems/dynamic-programming-stock-problem-summary.html)
- [0122.Best Time to Buy and Sell Stock II (Dynamic Programming)](https://keetcoder.com/problems/0122.best-time-to-buy-and-sell-stock-ii-(dynamic-programming).html)
- [0123.Best Time to Buy and Sell Stock III](https://keetcoder.com/problems/0123.best-time-to-buy-and-sell-stock-iii.html)
- [0188.Best Time to Buy and Sell Stock IV](https://keetcoder.com/problems/0188.best-time-to-buy-and-sell-stock-iv.html)
- [0309.Best Time to Buy and Sell Stock with Cooldown](https://keetcoder.com/problems/0309.best-time-to-buy-and-sell-stock-with-cooldown.html)
- [0714.Best Time to Buy and Sell Stock with Transaction Fee (Dynamic Programming)](https://keetcoder.com/problems/0714.best-time-to-buy-and-sell-stock-with-transaction-fee-(dynamic-programming).html)

## Subsequence Series

<img src='https://file1.kamacoder.com/i/algo/动态规划-子序列问题总结.jpg' width=500 alt=''> </img></div>

- [0300.Longest Increasing Subsequence](https://keetcoder.com/problems/0300.longest-increasing-subsequence.html)
- [0674.Longest Continuous Increasing Subsequence](https://keetcoder.com/problems/0674.longest-continuous-increasing-subsequence.html)
- [0718.Maximum Length of Repeated Subarray](https://keetcoder.com/problems/0718.maximum-length-of-repeated-subarray.html)
- [1143.Longest Common Subsequence](https://keetcoder.com/problems/1143.longest-common-subsequence.html)
- [1035.Uncrossed Lines](https://keetcoder.com/problems/1035.uncrossed-lines.html)
- [0053.Maximum Subarray (Dynamic Programming)](https://keetcoder.com/problems/0053.maximum-subarray-(dynamic-programming).html)
- [0392.Is Subsequence](https://keetcoder.com/problems/0392.is-subsequence.html)
- [0115.Distinct Subsequences](https://keetcoder.com/problems/0115.distinct-subsequences.html)
- [0583.Delete Operation for Two Strings](https://keetcoder.com/problems/0583.delete-operation-for-two-strings.html)
- [0072.Edit Distance](https://keetcoder.com/problems/0072.edit-distance.html)
- [Edit Distance in Three Steps by Karl](https://keetcoder.com/problems/edit-distance-in-three-steps-by-karl.html)
- [0647.Palindromic Substrings](https://keetcoder.com/problems/0647.palindromic-substrings.html)
- [0516.Longest Palindromic Subsequence](https://keetcoder.com/problems/0516.longest-palindromic-subsequence.html)

## Concluding Remarks on Dynamic Programming

Beyond dynamic programming, there are other types such as Tree DP (with one problem shown in the House Robbery series), Digit DP, Interval DP, Probability DP, Game DP, State Compression DP, etc. I won’t be explaining these; their occurrence in interviews is quite low.

If you thoroughly research all the problems listed in this article, your level of understanding of dynamic programming will be very high. It will be more than sufficient for interviews!

![image](https://file1.kamacoder.com/i/algo/_动态规划思维导图_青.png)

This diagram is created by a member [Qing](https://wx.zsxq.com/dweb2/index/footprint/185251215558842) from the [Coding Thoughts Knowledge Community](https://www.programmercarl.com/other/kstar.html). It’s beautifully summarized and I'd like to share it with everyone.

This should be the most detailed explanation series on dynamic programming available online.

**In fact, if you search online, you'll find that there are very few resources that can explain dynamic programming clearly because it is indeed challenging! Explaining it to others is even harder!**

In "Sword Offer Background," dynamic programming problems are scarce; the classic algorithm book "Algorithm 4" does not discuss dynamic programming, and "Introduction to Algorithms" covers it at a level that could be quite discouraging.

Explaining a single problem clearly is easy, explaining two problems clearly is easy, but thoroughly elucidating dynamic programming in its entirety and implementing it with a consistent methodology throughout is extremely difficult.

Therefore, Carl has devoted significant efforts to sharing his complete understanding of dynamic programming to help you avoid detours. Keep going!
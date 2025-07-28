# Summary of LeetCode Stock Problems!

Previously, we have gone through the series of stock problems on LeetCode, but we haven't had a summary to give everyone a high-level overview, so here it comes!

![Summary of Stock Problems](https://file1.kamacoder.com/i/algo/%E8%82%A1%E7%A5%A8%E9%97%AE%E9%A2%98%E6%80%BB%E7%BB%93.jpg)

* [Dynamic Programming: 0121.Best Time to Buy and Sell Stock](https://keetcoder.com/problems/0121.best-time-to-buy-and-sell-stock.html)
* [Dynamic Programming: 0122.Best Time to Buy and Sell Stock II (Dynamic Programming)](https://keetcoder.com/problems/0122.best-time-to-buy-and-sell-stock-ii-(dynamic-programming).html)
* [Dynamic Programming: 0123.Best Time to Buy and Sell Stock III](https://keetcoder.com/problems/0123.best-time-to-buy-and-sell-stock-iii.html)
* [Dynamic Programming: 0188.Best Time to Buy and Sell Stock IV](https://keetcoder.com/problems/0188.best-time-to-buy-and-sell-stock-iv.html)
* [Dynamic Programming: 0309.Best Time to Buy and Sell Stock with Cooldown](https://keetcoder.com/problems/0309.best-time-to-buy-and-sell-stock-with-cooldown.html)
* [Dynamic Programming: 0714.Best Time to Buy and Sell Stock with Transaction Fee (Dynamic Programming)](https://keetcoder.com/problems/0714.best-time-to-buy-and-sell-stock-with-transaction-fee-(dynamic-programming).html)

## Best Time to Sell Stock

[Dynamic Programming: 0121.Best Time to Buy and Sell Stock](https://keetcoder.com/problems/0121.best-time-to-buy-and-sell-stock.html), **you can only buy and sell once, ask for maximum profit**.

【Greedy Solution】

Take the smallest value on the left, and the largest value on the right, then the difference obtained is the maximum profit, the code is as follows:
```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int low = INT_MAX;
        int result = 0;
        for (int i = 0; i < prices.size(); i++) {
            low = min(low, prices[i]);  // Take the minimum price on the left
            result = max(result, prices[i] - low); // Directly take the maximum interval profit
        }
        return result;
    }
};
```

【Dynamic Programming】

* `dp[i][0]` means the cash obtained on day i when holding the stock.
* `dp[i][1]` means the cash obtained on day i when not holding the stock.

If holding the stock on day i, i.e., `dp[i][0]`, it can be derived from two states:
* Holding the stock on day i-1, that means keep the status quo, and the cash obtained is the cash from holding the stock yesterday: `dp[i - 1][0]`
* Buy the stock on day i, the cash obtained is the cash after buying the stock today: `-prices[i]`
So `dp[i][0] = max(dp[i - 1][0], -prices[i])`;

If not holding the stock on day i, i.e., `dp[i][1]`, it can also be derived from two states:
* Not holding the stock on day i-1, that means keep the status quo, and the cash obtained is the cash from not holding the stock yesterday: `dp[i - 1][1]`
* Sell the stock on day i, the cash obtained is the cash after selling the stock at today's price: `prices[i] + dp[i - 1][0]`
So `dp[i][1] = max(dp[i - 1][1], prices[i] + dp[i - 1][0])`;

The code is as follows:

```CPP
// Version one
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int len = prices.size();
        if (len == 0) return 0;
        vector<vector<int>> dp(len, vector<int>(2));
        dp[0][0] -= prices[0];
        dp[0][1] = 0;
        for (int i = 1; i < len; i++) {
            dp[i][0] = max(dp[i - 1][0], -prices[i]);
            dp[i][1] = max(dp[i - 1][1], prices[i] + dp[i - 1][0]);
        }
        return dp[len - 1][1];
    }
};
```
* Time Complexity: O(n)
* Space Complexity: O(n)

Using Rolling Array, the code is as follows:

```CPP
// Version two
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int len = prices.size();
        vector<vector<int>> dp(2, vector<int>(2)); // Note that here only a 2 * 2 array is opened
        dp[0][0] -= prices[0];
        dp[0][1] = 0;
        for (int i = 1; i < len; i++) {
            dp[i % 2][0] = max(dp[(i - 1) % 2][0], -prices[i]);
            dp[i % 2][1] = max(dp[(i - 1) % 2][1], prices[i] + dp[(i - 1) % 2][0]);
        }
        return dp[(len - 1) % 2][1];
    }
};
```

* Time Complexity: O(n)
* Space Complexity: O(1)

## Best Time to Buy and Sell Stock II

[Dynamic Programming: 0122.Best Time to Buy and Sell Stock II (Dynamic Programming)](https://keetcoder.com/problems/0122.best-time-to-buy-and-sell-stock-ii-(dynamic-programming).html) allows multiple trades, asking for maximum profit.

【Greedy Solution】

Collect positive profits each day, the code is as follows:

```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int result = 0;
        for (int i = 1; i < prices.size(); i++) {
            result += max(prices[i] - prices[i - 1], 0);
        }
        return result;
    }
};
```

* Time Complexity: O(n)
* Space Complexity: O(1)

【Dynamic Programming】

Definition of dp array:

* `dp[i][0]` means the cash obtained on day i when holding the stock.
* `dp[i][1]` means the cash obtained on day i when not holding the stock.

If holding the stock on day i, i.e., `dp[i][0]`, it can be derived from two states:
* Holding the stock on day i-1, that means keep the status quo, and the cash obtained is the cash from holding the stock yesterday: `dp[i - 1][0]`
* Buy the stock on day i, the cash obtained is the cash from not holding the stock yesterday minus the stock price today: `dp[i - 1][1] - prices[i]`

**Note the only difference here from [0121. Best Time to Buy and Sell Stock](https://keetcoder.com/problems/0121.best-time-to-buy-and-sell-stock.html) is when deriving `dp[i][0]`, it's about buying the stock on day i.**

In [0121. Best Time to Buy and Sell Stock](https://keetcoder.com/problems/0121.best-time-to-buy-and-sell-stock.html), since the stock can only be traded once overall, if buying a stock, then holding the stock on day i, i.e., `dp[i][0]` must be `-prices[i]`.

In this problem, since a stock can be traded multiple times, the cash obtained after buying the stock on day i may include the profits from previous trades.

The code is as follows (note the comments in the code, marking the only difference from [0121. Best Time to Buy and Sell Stock](https://keetcoder.com/problems/0121.best-time-to-buy-and-sell-stock.html)):

```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int len = prices.size();
        vector<vector<int>> dp(len, vector<int>(2, 0));
        dp[0][0] -= prices[0];
        dp[0][1] = 0;
        for (int i = 1; i < len; i++) {
            dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i]); // Note this is the only difference from 121. Best Time to Buy and Sell Stock.
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
        }
        return dp[len - 1][1];
    }
};
```

* Time Complexity: O(n)
* Space Complexity: O(n)

## Best Time to Buy and Sell Stock III

[Dynamic Programming: 0123.Best Time to Buy and Sell Stock III](https://keetcoder.com/problems/0123.best-time-to-buy-and-sell-stock-iii.html) at most allows two trades, asking for maximum profit.

【Dynamic Programming】

A total of five states are available per day,

0. No operation
1. First buy
2. First sell
3. Second buy
4. Second sell

`dp[i][j]` where i indicates the ith day, j [0 - 4], `dp[i][j]` represents the maximum cash left on day i with state j.

To reach state `dp[i][1]`, there are two specific operations:

* Operation one: stock is bought on day i, then `dp[i][1] = dp[i-1][0] - prices[i]`
* Operation two: there is no operation on day i, and the state from the previous day where the stock was bought is retained, i.e., `dp[i][1] = dp[i - 1][1]`

`dp[i][1] = max(dp[i-1][0] - prices[i], dp[i - 1][1])`;

Similarly, `dp[i][2]` also has two operations:

* Operation one: stock is sold on day i, then `dp[i][2] = dp[i - 1][1] + prices[i]`
* Operation two: there is no operation on day i, retain the state from the previous day where the stock was sold, i.e., `dp[i][2] = dp[i - 1][2]`

So `dp[i][2] = max(dp[i - 1][1] + prices[i], dp[i - 1][2])`

Similarly, the remaining states can be derived:

`dp[i][3] = max(dp[i - 1][3], dp[i - 1][2] - prices[i]);`

`dp[i][4] = max(dp[i - 1][4], dp[i - 1][3] + prices[i]);`

The code is as follows:

```CPP
// Version one
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.size() == 0) return 0;
        vector<vector<int>> dp(prices.size(), vector<int>(5, 0));
        dp[0][1] = -prices[0];
        dp[0][3] = -prices[0];
        for (int i = 1; i < prices.size(); i++) {
            dp[i][0] = dp[i - 1][0];
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
            dp[i][2] = max(dp[i - 1][2], dp[i - 1][1] + prices[i]);
            dp[i][3] = max(dp[i - 1][3], dp[i - 1][2] - prices[i]);
            dp[i][4] = max(dp[i - 1][4], dp[i - 1][3] + prices[i]);
        }
        return dp[prices.size() - 1][4];
    }
};
```

* Time Complexity: O(n)
* Space Complexity: O(n × 5)

Certainly, you can see an optimized space solution in the official LeetCode answer; here I provide the corresponding C++ version:

```CPP
// Version two
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.size() == 0) return 0;
        vector<int> dp(5, 0);
        dp[1] = -prices[0];
        dp[3] = -prices[0];
        for (int i = 1; i < prices.size(); i++) {
            dp[1] = max(dp[1], dp[0] - prices[i]);
            dp[2] = max(dp[2], dp[1] + prices[i]);
            dp[3] = max(dp[3], dp[2] - prices[i]);
            dp[4] = max(dp[4], dp[3] + prices[i]);
        }
        return dp[4];
    }
};
```

* Time Complexity: O(n)
* Space Complexity: O(1)

**This kind of solution looks simple, but the logic is quite convoluted. It is not recommended to write or think this way, as it can easily confuse oneself!** For this problem, understanding how version one is written is enough!

## Best Time to Buy and Sell Stock IV

[Dynamic Programming: 0188.Best Time to Buy and Sell Stock IV](https://keetcoder.com/problems/0188.best-time-to-buy-and-sell-stock-iv.html) enables at most k transactions, asking for maximum profit.

Using a two-dimensional array `dp[i][j]`: the i-th day, state j, the maximum cash left is `dp[i][j]`.

j state representation:

* 0 means no operation
* 1 means first buy
* 2 means first sell
* 3 means second buy
* 4 means second sell
* .....

**Except for 0, even numbers mean sell, and odd numbers mean buy**.

2. Confirm recurrence formula

To reach state `dp[i][1]`, there are two specific operations:

* Operation one: stock is bought on day i, then `dp[i][1] = dp[i - 1][0] - prices[i]`
* Operation two: no operation on day i, the stock bought state of the previous day is continued, i.e., `dp[i][1] = dp[i - 1][1]`

`dp[i][1] = max(dp[i - 1][0] - prices[i], dp[i - 1][1]);`

Similarly, `dp[i][2]` also has two operations:

* Operation one: stock is sold on day i, then `dp[i][2] = dp[i - 1][1] + prices[i]`
* Operation two: retain the state of selling the stock the day before, i.e., `dp[i][2] = dp[i - 1][2]`

`dp[i][2] = max(dp[i - 1][1] + prices[i], dp[i - 1][2])`

Similarly, the remaining states can be derived, the code is as follows:

```CPP
for (int j = 0; j < 2 * k - 1; j += 2) {
    dp[i][j + 1] = max(dp[i - 1][j + 1], dp[i - 1][j] - prices[i]);
    dp[i][j + 2] = max(dp[i - 1][j + 2], dp[i - 1][j + 1] + prices[i]);
}
```

The overall code is as follows:

```CPP
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {

        if (prices.size() == 0) return 0;
        vector<vector<int>> dp(prices.size(), vector<int>(2 * k + 1, 0));
        for (int j = 1; j < 2 * k; j += 2) {
            dp[0][j] = -prices[0];
        }
        for (int i = 1;i < prices.size(); i++) {
            for (int j = 0; j < 2 * k - 1; j += 2) {
                dp[i][j + 1] = max(dp[i - 1][j + 1], dp[i - 1][j] - prices[i]);
                dp[i][j + 2] = max(dp[i - 1][j + 2], dp[i - 1][j + 1] + prices[i]);
            }
        }
        return dp[prices.size() - 1][2 * k];
    }
};
```

Of course, some solutions define a three-dimensional array `dp[i][j][k]`, representing i-th day, j-th transaction, state of buying or selling, which is relatively intuitive by definition. However, operating on a three-dimensional array feels cumbersome, so directly using a two-dimensional array to simulate the three-dimensional array situation makes the code cleaner.

## Best Time to Buy and Sell Stock with Cooldown

[Dynamic Programming: 0309.Best Time to Buy and Sell Stock with Cooldown](https://keetcoder.com/problems/0309.best-time-to-buy-and-sell-stock-with-cooldown.html) allows multiple trades but each sell has a cooldown period of one day.

Compared with [Dynamic Programming: 0122.Best Time to Buy and Sell Stock II (Dynamic Programming)](https://keetcoder.com/problems/0122.best-time-to-buy-and-sell-stock-ii-(dynamic-programming).html), this problem adds a cooldown period.

In [Dynamic Programming: 0122.Best Time to Buy and Sell Stock II (Dynamic Programming)](https://keetcoder.com/problems/0122.best-time-to-buy-and-sell-stock-ii-(dynamic-programming).html), there are two states, cash after holding a stock, and cash after not holding a stock. In this problem, we can have four states.

`dp[i][j]` means the maximum cash left on day i when the state is j.

Specifically, it can be divided into the following four states:

* State 1: Buy stock state (Today buys stock, or it was already bought before and then no operation)
* Sell stock state, there are two kinds of sell stock states:
  * State 2: Sold stock two days ago, passed the cooldown period, always no operation, today keeps the sell stock state
  * State 3: Sold stock today
* State 4: Today is cooldown state, but cooldown state is not sustainable, only one day!

Reaching the buy stock state (State 1) is `dp[i][0]`, there are two specific operations:

* Operation one: holding stock state (State 1) on the previous day, `dp[i][0] = dp[i - 1][0]`
* Operation two: bought today, two situations:
  * Cooldown state (State 4) the previous day, `dp[i - 1][3] - prices[i]`
  * Maintaining sell stock state (State 2) the previous day, `dp[i - 1][1] - prices[i]`

So operation two takes the maximum value, i.e., `max(dp[i - 1][3], dp[i - 1][1]) - prices[i]`

Then `dp[i][0] = max(dp[i - 1][0], max(dp[i - 1][3], dp[i - 1][1]) - prices[i]);`

Reaching the keep selling stock state (State 2) is `dp[i][1]`, there are two specific operations:

* Operation one: it is state two on the previous day
* Operation two: it is cooldown state (State 4) on the previous day

`dp[i][1] = max(dp[i - 1][1], dp[i - 1][3]);`

Reaching the sell stock today state (State 3) is `dp[i][2]`, there is only one operation:

* Operation one: It must be bought stock state (State 1) the day before, sell today

i.e., `dp[i][2] = dp[i - 1][0] + prices[i];`

Reaching the cooldown state (State 4) is `dp[i][3]`, there is only one operation:

* Operation one: Sold stock (State 3) yesterday

`dp[i][3] = dp[i - 1][2];`

Summarizing the above analysis, the recurrence code is as follows:

```CPP
dp[i][0] = max(dp[i - 1][0], max(dp[i - 1][3], dp[i - 1][1]) - prices[i];
dp[i][1] = max(dp[i - 1][1], dp[i - 1][3]);
dp[i][2] = dp[i - 1][0] + prices[i];
dp[i][3] = dp[i - 1][2];
```

The overall code is as follows:

```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n == 0) return 0;
        vector<vector<int>> dp(n, vector<int>(4, 0));
        dp[0][0] -= prices[0]; // Hold stock
        for (int i = 1; i < n; i++) {
            dp[i][0] = max(dp[i - 1][0], max(dp[i - 1][3], dp[i - 1][1]) - prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][3]);
            dp[i][2] = dp[i - 1][0] + prices[i];
            dp[i][3] = dp[i - 1][2];
        }
        return max(dp[n - 1][3], max(dp[n - 1][1], dp[n - 1][2]));
    }
};
```

* Time Complexity: O(n)
* Space Complexity: O(n)

## Best Time to Buy and Sell Stock with Transaction Fee

[Dynamic Programming: 0714.Best Time to Buy and Sell Stock with Transaction Fee (Dynamic Programming)](https://keetcoder.com/problems/0714.best-time-to-buy-and-sell-stock-with-transaction-fee-(dynamic-programming).html) allows multiple trades but each has a transaction fee.

Compared with [Dynamic Programming: 0122.Best Time to Buy and Sell Stock II (Dynamic Programming)](https://keetcoder.com/problems/0122.best-time-to-buy-and-sell-stock-ii-(dynamic-programming).html), this question only needs to subtract the transaction fee in the calculation of the sell operation, and the code is almost the same.

The only difference lies in the recurrence formula part, so this article won't elaborate in detail according to the dynamic programming five-step framework, mainly explaining the recurrence formula.

Here restate the meaning of the dp array:

`dp[i][0]` means the maximum cash remaining on day i when holding a stock.
`dp[i][1]` means the maximum cash obtained without holding a stock on day i.

If holding the stock on day i, i.e., `dp[i][0]`, it can be derived from two states:
* Holding the stock on day i-1, that means keep the status quo, and the cash obtained is the cash from holding the stock yesterday: `dp[i - 1][0]`
* Buy the stock on day i, the cash obtained is the cash from not holding the stock yesterday minus the stock price today: `dp[i - 1][1] - prices[i]`

So: `dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i]);`

Now consider the situation if not holding the stock on day i, i.e., `dp[i][1]`. It can also be derived from two states:
* Not holding the stock on day i-1, that means keep the status quo, and the cash obtained is the cash from not holding the stock yesterday: `dp[i - 1][1]`
* Sell the stock on day i, the cash obtained is the cash from selling the stock at today's price, **note that a transaction fee is needed here**: `dp[i - 1][0] + prices[i] - fee`

So: `dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i] - fee);`

**The difference between this problem and [Dynamic Programming: 0122.Best Time to Buy and Sell Stock II (Dynamic Programming)](https://keetcoder.com/problems/0122.best-time-to-buy-and-sell-stock-ii-(dynamic-programming).html) is the need to subtract a transaction fee.**

Above analysis completed, the code is as follows:

```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int>(2, 0));
        dp[0][0] -= prices[0]; // Hold stock
        for (int i = 1; i < n; i++) {
            dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i] - fee);
        }
        return max(dp[n - 1][0], dp[n - 1][1]);
    }
};
```

* Time Complexity: O(n)
* Space Complexity: O(n)

## Conclusion

So far, the stock series has officially ended, and all have been fully explained!

From trading once to multiple trades, from trading up to twice to trading up to k times, from cooldown to transaction fee, finally coming to a great stock summary, this perfectly concludes the stock series.

The "Code Thoughts" is worth recommending to every friend and colleague learning algorithms, and those who follow it will find it a late encounter!
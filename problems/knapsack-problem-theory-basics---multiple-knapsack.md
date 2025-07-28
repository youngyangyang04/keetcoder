# Dynamic Programming: What You Should Know About the Multi-Knapsack Problem!

There is no original problem for this topic on LeetCode, but you can practice it on [KamaCoder Problem 56](https://kamacoder.com/problempage.php?pid=1066), which has a similar problem statement.

We have previously covered the 0/1 Knapsack and Complete Knapsack problems systematically. If you haven't read those articles, I suggest you first take a close look at the following three articles:

* [Knapsack Theory 01 Knapsack-1](https://keetcoder.com/problems/knapsack-theory-01-knapsack-1.html)
* [Knapsack Theory 01 Knapsack-2](https://keetcoder.com/problems/knapsack-theory-01-knapsack-2.html)
* [Knapsack Problem Theory Basics Complete Knapsack](https://keetcoder.com/problems/knapsack-problem-theory-basics-complete-knapsack.html)

This time, let's discuss the Multi-Knapsack Problem.

## Multi-Knapsack Problem

For the Multi-Knapsack Problem, I haven't found a corresponding problem on LeetCode, so I'll provide a simple introduction here. You should get a general understanding.

There are N types of items and a knapsack with a capacity of V. You can use up to Mi pieces of the ith type of item. Each piece costs Ci space and has a value of Wi. Determine which items to put in the knapsack to maximize the total value without exceeding the knapsack's capacity.

The Multi-Knapsack Problem is quite similar to the 0/1 Knapsack. Why is it similar?

Because with each item available up to Mi times, it's essentially a 0/1 Knapsack problem when you unfold these Mi items.

For example:

The maximum weight of the knapsack is 10.

Items are:

|       | Weight | Value | Quantity |
| ---   | ---    | ---   | ---      |
| Item 0| 1      | 15    | 2        |
| Item 1| 3      | 20    | 3        |
| Item 2| 4      | 30    | 2        |

What’s the maximum value the knapsack can carry?

Is it different from the following situation?

|        | Weight | Value | Quantity |
| ---    | ---    | ---   | ---      |
| Item 0 | 1      | 15    | 1        |
| Item 0 | 1      | 15    | 1        |
| Item 1 | 3      | 20    | 1        |
| Item 1 | 3      | 20    | 1        |
| Item 1 | 3      | 20    | 1        |
| Item 2 | 4      | 30    | 1        |
| Item 2 | 4      | 30    | 1        |

There is no difference; it becomes a 0/1 Knapsack problem where each item is used once.

Practice Problem: [KamaCoder Problem 56, Multi-Knapsack](https://kamacoder.com/problempage.php?pid=1066)

The code is as follows:

```CPP
// Timed out
#include<iostream>
#include<vector>
using namespace std;
int main() {
    int bagWeight,n;
    cin >> bagWeight >> n;
    vector<int> weight(n, 0); 
    vector<int> value(n, 0);
    vector<int> nums(n, 0);
    for (int i = 0; i < n; i++) cin >> weight[i];
    for (int i = 0; i < n; i++) cin >> value[i];
    for (int i = 0; i < n; i++) cin >> nums[i];    
    
    for (int i = 0; i < n; i++) {
        while (nums[i] > 1) { // Unfold items
            weight.push_back(weight[i]);
            value.push_back(value[i]);
            nums[i]--;
        }
    }
 
    vector<int> dp(bagWeight + 1, 0);
    for(int i = 0; i < weight.size(); i++) { // Traverse items
        for(int j = bagWeight; j >= weight[i]; j--) { // Traverse knapsack capacity
            dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
        }
    }
    cout << dp[bagWeight] << endl;
}
```

After submitting, you'll find this solution times out. Why? Where is the time consumed?

The time consumption lies in the following code:

```CPP 
for (int i = 0; i < n; i++) {
    while (nums[i] > 1) { // Unfold items
        weight.push_back(weight[i]);
        value.push_back(value[i]);
        nums[i]--;
    }
}
```

If there are many items, operations like this are very time-consuming in C++ due to the dynamic expansion of vectors. (This can be optimized here too; you could precalculate the total item count and allocate vector space in one go.)

There is another way to implement this by counting each item's quantity in the 0/1 Knapsack loop.

The code is as follows (see comments for details):

```CPP 
#include<iostream>
#include<vector>
using namespace std;
int main() {
    int bagWeight,n;
    cin >> bagWeight >> n;
    vector<int> weight(n, 0);
    vector<int> value(n, 0);
    vector<int> nums(n, 0);
    for (int i = 0; i < n; i++) cin >> weight[i];
    for (int i = 0; i < n; i++) cin >> value[i];
    for (int i = 0; i < n; i++) cin >> nums[i];

    vector<int> dp(bagWeight + 1, 0);

    for(int i = 0; i < n; i++) { // Traverse items
        for(int j = bagWeight; j >= weight[i]; j--) { // Traverse knapsack capacity
            // It's 0/1 knapsack, then add a loop for item quantity
            for (int k = 1; k <= nums[i] && (j - k * weight[i]) >= 0; k++) { // Traverse quantity
                dp[j] = max(dp[j], dp[j - k * weight[i]] + k * value[i]);
            }
        }
    }

    cout << dp[bagWeight] << endl;
}
```

Time Complexity: O(m × n × k), where m is the number of item types, n is the knapsack capacity, and k is the quantity of a single type of item.

From the code, you can see it’s a 0/1 Knapsack with an additional loop to iterate through each item’s quantity. It’s very much like a 0/1 Knapsack.

There’s also a binary optimization method, which essentially packs each type of item into independent parcels.

The difference from the above is in the loop since it’s split into several parcels that can form a complete knapsack. I won't go into the specifics here, but you can explore it on your own. It’s unlikely to be tested in an interview at this depth. 

## Summary

The Multi-Knapsack Problem is unlikely to appear in interviews. There's no corresponding problem on LeetCode. It’s enough to understand that it’s a variant of the 0/1 Knapsack and be able to write the corresponding code based on the 0/1 Knapsack Problem.

As for other types of knapsack problems mentioned in knapsack lectures, such as Mixed Knapsack, Two-Dimensional Cost Knapsack, Group Knapsack, and so on, you can study them if you’re interested. However, they won't be covered here and aren’t likely to be tested in interviews.

## Other Language Versions

### Java:

```Java
import java.util.Scanner;
class multi_pack{
    public static void main(String [] args) {
        Scanner sc = new Scanner(System.in);

        /**
         * bagWeight: Capacity of the knapsack
         * n: Number of item types
         */
        int bagWeight, n;
        
        // Retrieve user input with spaces in between, new line with Enter
        bagWeight = sc.nextInt();
        n = sc.nextInt();
        int[] weight = new int[n];
        int[] value = new int[n];
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) weight[i] = sc.nextInt();
        for (int i = 0; i < n; i++) value[i] = sc.nextInt();
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();

        int[] dp = new int[bagWeight + 1];

        // First traverse items, then traverse the knapsack like 0/1 Knapsack
        for (int i = 0; i < n; i++) {
            for (int j = bagWeight; j >= weight[i]; j--) {
                // Iterate over the quantity of each type of item
                for (int k = 1; k <= nums[i] && (j - k * weight[i]) >= 0; k++) {
                    dp[j] = Math.max(dp[j], dp[j - k * weight[i]] + k * value[i]);
                }
            }
        }
        System.out.println(dp[bagWeight]);
    }
}
```
### Python:

```python

C, N = input().split(" ")
C, N = int(C), int(N)

# Make sure the value array is not empty, otherwise it won't pass
weights = [int(x) for x in input().split(" ")]
values = [int(x) for x in input().split(" ") if x]
nums = [int(x) for x in input().split(" ")]

dp = [0] * (C + 1)
# Traverse knapsack capacity
for i in range(N):
    for j in range(C, weights[i] - 1, -1):
        for k in range(1, nums[i] + 1):
            # Traverse k, skip if it exceeds knapsack capacity
            if k * weights[i] > j:
                break
            dp[j] = max(dp[j], dp[j - weights[i] * k] + values[i] * k) 
print(dp[-1])

```

### Go:


### TypeScript:
# Summary of Dynamic Programming: Edit Distance

This week we covered the ultimate killer in dynamic programming: Edit Distance. Why call it the ultimate killer?

Observant readers may have noticed that the previous three articles on dynamic programming were laying the groundwork for this particular problem.

## Is Subsequence

[0392.Is Subsequence](https://keetcoder.com/problems/0392.is-subsequence.html) Given strings s and t, determine if s is a subsequence of t.

This problem can actually be solved using a two-pointer method or greedily, but as I mentioned at the beginning, it's an entry-level problem for Edit Distance. From the problem statement, we can see that it only requires counting deletions, not considering insertions or replacements.

* if (*s*[*i* - 1] == *t*[*j* - 1])
    * A character in *t* has been found that also appears in *s*
* if (*s*[*i* - 1] != *t*[*j* - 1])
    * Equivalent to deleting an element from *t*, continue matching

State transition equation:

```
if (s[i - 1] == t[j - 1]) dp[i][j] = dp[i - 1][j - 1] + 1;
else dp[i][j] = dp[i][j - 1];
```

## Distinct Subsequences

[0115.Distinct Subsequences](https://keetcoder.com/problems/0115.distinct-subsequences.html) Given a string s and a string t, count the number of distinct subsequences of s which equal t.

Although this problem also only involves deletion operations, without considering replacements or insertions, it is definitely more challenging than [0392.Is Subsequence](https://keetcoder.com/problems/0392.is-subsequence.html), and the two-pointer method won't work here.

When s[i - 1] is equal to t[j - 1], dp[i][j] can be composed of two parts:

One part uses s[i - 1] to match, with a count of dp[i - 1][j - 1].

The other part doesn't use s[i - 1] to match, with a count of dp[i - 1][j].

Some might wonder why we should consider not using s[i - 1] to match since they match. 

For example: s: bagg and t: bag, s[3] and t[2] are the same, but the string s can also form bag without using s[3], that is, using s[0]s[1]s[2].

Of course, s[3] can also be used to match, i.e., forming bag with s[0]s[1]s[3].

So when s[i - 1] equals t[j - 1], dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j].

When s[i - 1] is not equal to t[j - 1], dp[i][j] is composed of only one part, not using s[i - 1] to match, i.e., dp[i - 1][j].

State transition equation:
```CPP
if (s[i - 1] == t[j - 1]) {
    dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
} else {
    dp[i][j] = dp[i - 1][j];
}
```

## Delete Operation for Two Strings

[0583.Delete Operation for Two Strings](https://keetcoder.com/problems/0583.delete-operation-for-two-strings.html) Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same. In each step, you can delete one character in either string.

This problem, compared to [0115.Distinct Subsequences](https://keetcoder.com/problems/0115.distinct-subsequences.html), allows deletions in both strings. Though slightly more complex, the overall idea remains unchanged.

* When word1[i - 1] equals word2[j - 1]
* When word1[i - 1] does not equal word2[j - 1]

When word1[i - 1] equals word2[j - 1], dp[i][j] = dp[i - 1][j - 1].

When word1[i - 1] does not equal word2[j - 1], there are three cases:

Case 1: Delete word1[i - 1]; minimal operations = dp[i - 1][j] + 1

Case 2: Delete word2[j - 1]; minimal operations = dp[i][j - 1] + 1

Case 3: Delete both word1[i - 1] and word2[j - 1]; minimal operations = dp[i - 1][j - 1] + 2

Thus, take the minimum value. When word1[i - 1] doesn't equal word2[j - 1], the recursive formula is: dp[i][j] = min({dp[i - 1][j - 1] + 2, dp[i - 1][j] + 1, dp[i][j - 1] + 1}).

State transition equation:
```CPP
if (word1[i - 1] == word2[j - 1]) {
    dp[i][j] = dp[i - 1][j - 1];
} else {
    dp[i][j] = min({dp[i - 1][j - 1] + 2, dp[i - 1][j] + 1, dp[i][j - 1] + 1});
}
```

## Edit Distance

[0072.Edit Distance](https://keetcoder.com/problems/0072.edit-distance.html) Given two words word1 and word2, calculate the minimum number of operations required to convert word1 into word2.

Finally, we have reached the topic of Edit Distance. With the foundation laid by the previous three problems, you should have some hints about how to approach it. This problem involves both insertions, deletions, and substitutions, making it more complex than [0392.Is Subsequence](https://keetcoder.com/problems/0392.is-subsequence.html), [0115.Distinct Subsequences](https://keetcoder.com/problems/0115.distinct-subsequences.html), and [0583.Delete Operation for Two Strings](https://keetcoder.com/problems/0583.delete-operation-for-two-strings.html).

When determining the recursive formula, first consider the types of edits possible, as outlined below:

* if (*word1*[*i* - 1] == *word2*[*j* - 1])
    * Do nothing
* if (*word1*[*i* - 1] != *word2*[*j* - 1])
    * Insert
    * Delete
    * Replace

There are the above four possibilities.

If (*word1*[*i* - 1] == *word2*[*j* - 1]), this means no editing is required, thus dp[i][j] should be dp[i - 1][j - 1], i.e., dp[i][j] = dp[i - 1][j - 1];

Some of you may wonder why it has to be dp[i][j] = dp[i - 1][j - 1].

Recall the definition of dp[i][j]. If word1[i - 1] and word2[j - 1] are equal, no edits are needed. Then, the minimum edit distance for the strings ending at index i-2 of word1 and index j-2 of word2, dp[i - 1][j - 1], is the same as dp[i][j].

If any part is unclear, reviewing the definition of dp[i][j] should clarify things.

The key to dynamic programming is correctly understanding the definition of dp[i][j]!

If (*word1*[*i* - 1] != *word2*[*j* - 1]), editing is required. How to edit?

Operation 1: Add a character to word1 so that word1[i - 1] is like word2[j - 1]. This makes the minimum edit distance with word1 ending at index i-2 and word2 ending at index j-1, plus one addition.

i.e., dp[i][j] = dp[i - 1][j] + 1;

Operation 2: Add a character to word2 so that word1[i - 1] matches word2[j - 1]. This makes the minimum edit distance with word1 ending at index i-1 and word2 ending at index j-2, plus one addition.

i.e., dp[i][j] = dp[i][j - 1] + 1;

Some may notice both involve adding characters. What about deleting characters?

Adding a character to word2 is equivalent to deleting a character from word1, e.g., word1 = "ad", word2 = "a". Adding a character d to word2 is equivalent to deleting a character d from word1; the operations are the same!

Operation 3: Replace a character, replacing word1[i - 1] with word2[j - 1]. This prevents adding elements, adding one replacement to the minimum edit distance with both words ending at index i-2 and j-2.

i.e., dp[i][j] = dp[i - 1][j - 1] + 1;

In summary, when if (*word1*[*i* - 1] != *word2*[*j* - 1]), take the smallest, i.e., dp[i][j] = min({dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]}) + 1;

Recursive formula code is as follows:

```CPP
if (word1[i - 1] == word2[j - 1]) {
    dp[i][j] = dp[i - 1][j - 1];
}
else {
    dp[i][j] = min({dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]}) + 1;
}
```

## Summary

Thoughtful readers may have noticed I used three problems as groundwork before finally introducing [0072.Edit Distance](https://keetcoder.com/problems/0072.edit-distance.html). Carl’s meticulous efforts! Did you get it?

## Other Language Versions

### Java:

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m+1][n+1];
        for(int i = 1; i <= m; i++){
            dp[i][0] = i;
        }
        for(int i = 1; i <= n; i++){
            dp[0][i] = i;
        }
        for(int i = 1; i <= m; i++){
            for(int j = 1; j <= n; j++){
                int left = dp[i][j-1]+1;
                int mid = dp[i-1][j-1];
                int right = dp[i-1][j]+1;
                if(word1.charAt(i-1) != word2.charAt(j-1)){
                    mid ++;
                }
                dp[i][j] = Math.min(left,Math.min(mid,right));
            }
        }
        return dp[m][n];
    }
}
```
# Replace Number

LeetCode has removed the Sword Offer questions, so I am providing similar questions on Kamacoder for practice. 

[Link to the problem on Kamacoder](https://kamacoder.com/problempage.php?pid=1064)

Given a string `s` that contains lowercase letters and numeric characters, please write a function that replaces each numeric character in the string with "number", while keeping the letter characters unchanged.

For example, for the input string `"a1b2c3"`, the function should transform it into `"anumberbnumbercnumber"`.

For the input string `"a5b"`, it should be transformed into `"anumberb"`.

**Input:** A string `s` which contains only lowercase letters and numeric characters.

**Output:** Print a new string where each numeric character is replaced with "number".

**Sample Input:** `a1b2c3`

**Sample Output:** `anumberbnumbercnumber`

**Data Range:** `1 <= s.length < 10000`.

## Thought Process

To optimize this problem, avoid using additional auxiliary space. (However, those using Java should use auxiliary space as strings in Java are immutable.)

First, enlarge the array to accommodate the size after each numeric character is replaced with "number".

For example, the string `"a5b"` is initially of length 3, but after transforming the numeric character into the string "number", it becomes `"anumberb"` with a length of 8.

Diagram:

![](https://file1.kamacoder.com/i/algo/20231030165201.png) 

Then, replace the numeric characters from back to front, using a two-pointer approach, as illustrated: `i` points to the end of the new length, `j` points to the end of the old length.

![](https://file1.kamacoder.com/i/algo/20231030173058.png)

Some might ask, why fill from back to front and not from front to back?

Filling from front to back results in an O(n^2) algorithm because each addition requires moving all subsequent elements back by one position.

**Many array filling problems follow this approach: expand the array to the filled size beforehand, then operate from back to front.**

Doing so has two advantages:

1. No need to allocate a new array.
2. Avoids the issue of moving all subsequent elements back by one position when adding elements from front to back.

Here is the C++ code:

```cpp
#include<iostream>
using namespace std;
int main() {
    string s;
    while (cin >> s) {
        int count = 0; // Count the number of digits
        int sOldSize = s.size();
        for (int i = 0; i < s.size(); i++) {
            if (s[i] >= '0' && s[i] <= '9') {
                count++;
            }
        }
        // Resize the string s to accommodate "number" for each digit
        s.resize(s.size() + count * 5);
        int sNewSize = s.size();
        // Replace digits with "number" from end to start
        for (int i = sNewSize - 1, j = sOldSize - 1; j < i; i--, j--) {
            if (s[j] > '9' || s[j] < '0') {
                s[i] = s[j];
            } else {
                s[i] = 'r';
                s[i - 1] = 'e';
                s[i - 2] = 'b';
                s[i - 3] = 'm';
                s[i - 4] = 'u';
                s[i - 5] = 'n';
                i -= 5;
            }
        }
        cout << s << endl;
    }
}
```

* Time complexity: O(n)
* Space complexity: O(1)

By now, we've completed seven twin-pointer problems, namely:

* [0027.Remove Element](https://keetcoder.com/problems/0027.remove-element.html)
* [0015.3Sum](https://keetcoder.com/problems/0015.3sum.html)
* [0018.4Sum](https://keetcoder.com/problems/0018.4sum.html)
* [0206.Reverse Linked List](https://keetcoder.com/problems/0206.reverse-linked-list.html)
* [0142.Linked List Cycle II](https://keetcoder.com/problems/0142.linked-list-cycle-ii.html)
* [0344.Reverse String](https://keetcoder.com/problems/0344.reverse-string.html)

## Extension

Here, I'll expand a little on the differences between strings and arrays.

A string is a finite sequence composed of several characters, which can also be understood as a character array. However, many programming languages have special rules for strings. Let's talk about strings in C/C++.

In C, when a string is stored in an array, the end marker '\0' is stored in the array as well, marking the end of the string.

For example, this code:

```c
char a[5] = "asd";
for (int i = 0; a[i] != '\0'; i++) {
}
```

In C++, a `string` class is provided that offers a `size` method, which can be used to determine if the string has ended, eliminating the need to use '\0'.

For example, this code:

```cpp
string a = "asd";
for (int i = 0; i < a.size(); i++) {
}
```

So what's the difference between `vector<char>` and `string`?

In essence, there is no difference in basic operations, but the `string` class provides more functions for string manipulation, such as overloaded `+`, which `vector` does not.

Therefore, when dealing with strings, we tend to define a `string` type.

## Other Language Versions

### C:

### Java:

### Go:

### Python:

### JavaScript:

### TypeScript:

### Swift:

### Scala:

### PHP:

### Rust:
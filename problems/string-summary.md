# String: Summary

We have actually been studying strings for ten days, from the definition of strings to the principles of using library functions, from various reversals to the KMP algorithm. I believe everyone should have a deeper understanding of strings by now.

Let's do a summary this time.

## What is a String

A string is a finite sequence composed of several characters and can be understood as a character array. However, many languages have special regulations for strings. Next, I will talk about strings in C/C++.

In C language, when storing a string in an array, the termination character '\0' is also stored in the array, which is used as the mark for whether the string ends.

For example, this piece of code:

```
char a[5] = "asd";
for (int i = 0; a[i] != '\0'; i++) {
}
```

In C++, a `string` class is provided. The `string` class offers a `size` method which can be used to determine whether the string has ended, eliminating the need to use '\0'.

For example, this piece of code:

```
string a = "asd";
for (int i = 0; i < a.size(); i++) {
}
```

So, what is the difference between `vector<char>` and `string`?

In basic operations, there is no difference, but `string` provides more related interfaces for string processing, such as the overloaded `+` operator, which `vector` doesn't have.

Therefore, if we want to handle strings, we usually define a `string` type.

## Whether to Use Library Functions

In the article [0344.Reverse String](https://keetcoder.com/problems/0344.reverse-string.html), it is emphasized that **when building a foundation, don't be too obsessed with library functions.**

Some students might habitually call library functions like `substr`, `split`, `reverse`, but do not know their implementation principles nor time complexity. If code like this is written in an interview, and the interviewer asks, "Analyze its time complexity," one would be baffled!

So it's recommended: **if the key part of the problem can be solved directly with a library function, it's better not to use the library function.**

**If the library function is just a small part of the solution and you are very familiar with its internal implementation principles, you can consider using the library function.**

## Two-pointer Technique

In [0344.Reverse String](https://keetcoder.com/problems/0344.reverse-string.html), we used the two-pointer technique to implement the reversal operation of strings. **The two-pointer technique is often used in arrays, linked lists, and strings.**

Then in [SwordOffer05.Replace Spaces](https://keetcoder.com/problems/swordoffer05.replace-spaces.html), we also used the two-pointer technique to replace spaces with a time complexity of O(n).

**Many array-filling problems can first pre-expand the array to the size after filling, then operate from back to front.**

For problems concerning array deletion, in [0027.Remove Element](https://keetcoder.com/problems/0027.remove-element.html), it was mentioned to use the two-pointer technique to perform the removal operation.

The same logic applies to [0151.Reverse Words in a String](https://keetcoder.com/problems/0151.reverse-words-in-a-string.html), where we removed redundant spaces with a time complexity of O(n).

Some students might use a `for` loop to call the library function `erase` to remove elements, which is actually an O(n^2) operation because `erase` itself is an O(n) operation. This is a typical case of not knowing the time complexity of library functions and using them directly.

## Series of Reversals

In the aspect of reversal, some more tricks can be added, actually testing the ability to control the code.

In [0541.Reverse String II](https://keetcoder.com/problems/0541.reverse-string-ii.html), some students might write a bunch of logic code or create a counter to handle the logic of reversing the first k characters for every 2k characters. 

However, **when there's a fixed pattern and you need to process the string piece by piece, consider tweaking the `for` loop expressions.**

As long as it is written as `i += (2 * k)`, and 'i' moves by 2 * k each time, it's possible to determine whether there's a section that needs reversing.

Since you only need to find the starting point of each 2 * k interval, writing the program this way will be much more efficient.

In [0151.Reverse Words in a String](https://keetcoder.com/problems/0151.reverse-words-in-a-string.html), which requires reversing the words in a string, this problem can be said to comprehensively test various string operations and is a good problem to test on strings.

This problem achieves reversing the words in a string through **first an overall reversal and then a local reversal**.

Later it was discovered that string reversal has another great use, which is to achieve the effect of a left rotation.

In [SwordOffer58-II.Left Rotation of String](https://keetcoder.com/problems/SwordOffer58-ii.left-rotation-of-string.html), we achieved the effect of left rotation through **first a local reversal and then an overall reversal**.

## KMP 

The main idea of the KMP algorithm is **when there is a mismatch in strings, some previously matched text content can be identified and used to avoid starting from scratch for the match.**

The essence of KMP lies in the prefix table, and in the [KMP Explanation](https://keetcoder.com/problems/0028.implement-strstr.html), it explains what KMP is, what the prefix table is, and why the prefix table is needed.

Prefix Table: In the substring from the starting position to before index 'i' (including 'i'), what is the length of the matching prefix and suffix.

KMP can solve two classic types of problems:

1. Matching problem: [0028.Implement strStr](https://keetcoder.com/problems/0028.implement-strstr.html)
2. Repeated substring problem: [0459.Repeated Substring Pattern](https://keetcoder.com/problems/0459.repeated-substring-pattern.html)

Highlighting once more what a prefix is, what a suffix is, and what the longest matching prefix and suffix is.

Prefix: Refers to all consecutive substrings starting with the first character, excluding the last character.

Suffix: Refers to all consecutive substrings ending with the last character, excluding the first character.

Additionally, **whether to subtract one from the prefix table depends on the different implementations of KMP**. In the [KMP Explanation](https://keetcoder.com/problems/0028.implement-strstr.html), we provided two different versions of KMP implementations for the two problems mentioned earlier.

Among them, understanding the step **j=next[x]** is most crucial!

## Summary

String-related problems often appear simple in concept but are not easy to implement. Complex string problems greatly test the ability to control code.

The two-pointer technique is a frequent guest in string processing.

The KMP algorithm is the most important string search algorithm, but thoroughly understanding KMP is not easy. We have written five articles on KMP, continuously summarizing and refining, and finally managed to explain KMP clearly.

Alright, the algorithm knowledge related to strings is introduced here. A new journey begins tomorrow, keep up the good work everyone!
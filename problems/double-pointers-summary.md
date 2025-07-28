> Another wave of summary

I believe everyone is already familiar with the two-pointer technique. However, the two-pointer technique does not belong exclusively to any particular data structure. We have used the two-pointer technique in arrays, linked lists, and strings, so it is necessary to make a summary specifically on the two-pointer technique.

# Two-pointer Technique Summary
## Array Section

In [0027.Remove Element](https://keetcoder.com/problems/0027.remove-element.html), when removing elements in place from an array, we emphasized that the elements on the array cannot be truly deleted, only overwritten.

Some students might write code like the following pseudo-code:

```
for (int i = 0; i < array.size(); i++) {
    if (array[i] == target) {
        array.erase(i);
    }
}
```

This code appears to have a time complexity of O(n), but it is actually O(n^2) because the erase operation is also O(n).

Therefore, it is precisely when using the two-pointer technique that the efficiency advantage becomes apparent: **By using two pointers, the work of two for loops can be completed within a single for loop.** 

## String Section

In [0344.Reverse String](https://keetcoder.com/problems/0344.reverse-string.html), we explained how to reverse a string in place, otherwise, it loses the meaning of the problem.

Using the two-pointer technique, **define two pointers (or index subscripts) — one starting from the front of the string, the other from the back. Both pointers move towards the center, and elements are swapped** with a time complexity of O(n).

In [SwordOffer05.Replace Spaces](https://keetcoder.com/problems/swordoffer05.replace-spaces.html), the method of using two pointers to fill a string was introduced. If you want to solve this problem to the extreme, don't use an extra auxiliary space!

The idea is to **first expand the array to the size after each space is replaced with "%20". Then use two pointers to replace spaces from back to front.**

Some might ask, why fill from back to front, isn't filling from front to back fine?

Filling from front to back results in an O(n^2) algorithm because each time elements are added, all subsequent elements must be moved backward.

**In fact, many array (and string) filling problems can first expand the array to the size after filling, and then operate from back to front.** 

In [0151.Reverse Words in a String](https://keetcoder.com/problems/0151.reverse-words-in-a-string.html), we used the two-pointer technique to perform O(n) complexity string deletion operations since the problem requires removing redundant spaces.

**In the process of removing redundant spaces, if you're not careful about code efficiency, it is easy to write an O(n^2) time complexity. In fact, using the two-pointer technique allows us to solve it in O(n).**

**The main reason is that many people use erase casually, especially in a for loop, which can generally be handled more efficiently with a two-pointer approach!**

## Linked List Section

Reversing a linked list is a great problem for onsite interviews or writing on paper, as it tests the candidate's familiarity with linked lists and pointers, and the code is short, making it suitable for paper writing.

In [0206.Reverse Linked List](https://keetcoder.com/problems/0206.reverse-linked-list.html), we discussed how to use the two-pointer technique to reverse a linked list. **All you need to do is change the direction of the linked list's next pointer to directly reverse the linked list without redefining a new one.**

The idea is simple, and the code is short, but writing bug-free code on paper isn't easy.

Finding a cycle in a linked list is classic usage of the two-pointer technique in linked lists. In [0142.Linked List Cycle II](https://keetcoder.com/problems/0142.linked-list-cycle-ii.html), we explained how to determine if there is a cycle with two pointers, but also find the entrance of the cycle.

**Using fast and slow pointers (the two-pointer technique), define the fast and slow pointers, starting from the head node. The fast pointer moves two nodes at a time, and the slow pointer moves one. If the fast and slow pointers meet along the way, this means there is a cycle.**

Finding the entrance requires simple mathematical reasoning, which I explained clearly in the article. If you're not clear on finding the entrance, I suggest checking out [0142.Linked List Cycle II](https://keetcoder.com/problems/0142.linked-list-cycle-ii.html).

## N-Sum Section

In [0015.3Sum](https://keetcoder.com/problems/0015.3sum.html), we discussed that while the hash method solves the two-sum problem, it is not suited for the three-sum problem!

Using a hash method requires putting matching triplets into a vector and then deduplicating, which is time-consuming, easily resulting in timeouts and the root cause of the low success rate for the three-sum problem.

Deduplication is hard to handle with many small details, which makes it difficult to get right in interviews.

Though time complexity can be O(n^2), it is still quite time-consuming as pruning is hard to apply.

Thus, using the two-pointer technique for this problem is most appropriate. It allows us to truly experience **how two pointers approaching each other in a single for-loop performs the work of two nested loops.**

Using the two-pointer approach alone cuts the time complexity to O(n^2), but it's far more efficient than the hash method's O(n^2), as the hash method offers few pruning opportunities.

In [0018.4Sum](https://keetcoder.com/problems/0018.4sum.html), the concept is similar, **adding another layer of for-loop to the 3Sum problem while still using the two-pointer technique.**

The two-pointer approach for the three-sum problem reduces the original brute-force O(n^3) to O(n^2), and the four-sum problem reduces the original O(n^4) to O(n^3).

Similarly, five-sum and n-sum problems are just extensions of this principle.

## Summary

This article introduced a total of nine classic LeetCode problems solved using the two-pointer technique. Apart from some linked list problems that must use the two-pointer approach, other problems use it to improve efficiency, usually reducing O(n^2) complexity to **O(n)**.

I suggest that everyone revisit and ponder these problems to gain a solid grasp of the two-pointer technique.
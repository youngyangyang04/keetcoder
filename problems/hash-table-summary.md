> The summary of hash tables is finally here

# Hash Table Summary

## Hash Table Basics

In [Hash Table Basics](https://keetcoder.com/problems/hash-table-basics.html), we introduced the fundamental theoretical knowledge of hash tables. Unlike dull explanations, the content here is all about theoretical knowledge that is helpful for problem-solving.

**Generally, hash tables are used to quickly determine if an element appears in a set.**

For hash tables, it’s important to understand the role of **hash functions** and **hash collisions**.

A hash function maps the input key to an index of the symbol table.

Hash collision handling occurs when multiple keys are mapped to the same index. Common methods for handling collisions include chaining and linear probing.

Next are the three common hash structures:

* Array
* Set
* Map

In the C++ language, both set and map provide three different data structures, each with different underlying implementations and uses, which are analyzed in detail in [Hash Table Basics](https://keetcoder.com/problems/hash-table-basics.html). This knowledge point is very important!

For example, when to use `std::set`, `std::multiset`, or `std::unordered_set` requires careful consideration.

**Only by being familiar with the underlying implementation of these data structures can they be used flexibly; otherwise, it is easy to write inefficient programs.**

## Classic Hash Table Problems

### Arrays as Hash Tables

Some application scenarios are tailor-made for arrays.

In [0242.Valid Anagram](https://keetcoder.com/problems/0242.valid-anagram.html), we mentioned that arrays are simple hash tables, but arrays have size limitations!

This problem involves lowercase letters, making it most appropriate to use an array as a hash.

In [0383.Ransom Note](https://keetcoder.com/problems/0383.ransom-note.html), similarly, only lowercase letters are required, strongly implying the use of an array!

This problem is very similar to [0242.Valid Anagram](https://keetcoder.com/problems/0242.valid-anagram.html), where the task is to determine if string `a` and string `b` can be composed of each other. In [0383.Ransom Note](https://keetcoder.com/problems/0383.ransom-note.html), the task is to check if string `a` can be composed of string `b` without concern for whether string `b` can be composed of string `a`.

Some might think, why bother with arrays? Just use a map.

**The two problems above can indeed be solved with a map, but the space consumption of a map is larger than an array because a map needs to maintain a red-black tree or symbol table and perform hash function calculations. Therefore, arrays are more straightforward, direct, and effective!**

### Set as Hash Table

In [0349.Intersection of Two Arrays](https://keetcoder.com/problems/0349.intersection-of-two-arrays.html), we explained when arrays are insufficient, and sets are needed.

This problem does not limit the size of numbers, making it impossible to use an array as a hash table.

**Mainly due to these two points:**

* The size of the array is limited by the system stack space (not the stack data structure).
* If the array space is large but the hash values are few, particularly scattered, and span a wide range, using an array results in significant space waste.

Thus, mapping the same would require a set.

Regarding set, C++ provides the following three available data structures: (For details, see [Hash Table Basics](https://keetcoder.com/problems/hash-table-basics.html))

* `std::set`
* `std::multiset`
* `std::unordered_set`

`std::set` and `std::multiset` are implemented with red-black trees, whereas `std::unordered_set` is implemented with a hash. Using `unordered_set` provides the highest read/write efficiency. This problem does not require data sorting and de-duplication, so `unordered_set` is chosen.

In [0202.Happy Number](https://keetcoder.com/problems/0202.happy-number.html), we again used `unordered_set` to check if a number reappears.

### Map as Hash Table

In [0001.Two Sum](https://keetcoder.com/problems/0001.two-sum.html), the map formally takes stage.

Let’s discuss the limitations of using arrays and sets as hash methods.

* The size of the array is limited. Moreover, if there are few elements and large hash values, memory space is wasted.
* A set is a collection, where an element can only be a key. However, in the two sum problem, we not only have to check if `y` exists but also record the index of `y` since we need to return the indices of `x` and `y`. Hence, sets cannot be used.

A map is a `<key, value>` structure. In this problem, keys can store values, and values can store indices of those values, making the use of a map most suitable.

C++ provides the following three types of maps: (For details, see [Hash Table Basics](https://keetcoder.com/problems/hash-table-basics.html))

* `std::map`
* `std::multimap`
* `std::unordered_map`

`std::unordered_map` is implemented using a hash, whereas `std::map` and `std::multimap` use red-black trees.

Similarly, the keys in `std::map` and `std::multimap` are ordered (this is often used as an interview question to assess understanding of the language container’s underlying mechanics); in [0001.Two Sum](https://keetcoder.com/problems/0001.two-sum.html), key ordering is not required, so using `std::unordered_map` is more efficient!

In [0454.4Sum II](https://keetcoder.com/problems/0454.4sum-ii.html), we mentioned that maps often appear where hash methods are needed.

At first glance, this problem seems similar to [0018.4Sum](https://keetcoder.com/problems/0018.4sum.html) and [0015.3Sum](https://keetcoder.com/problems/0015.3sum.html), but they are quite different!

**The key difference is that this problem requires finding `A[i] + B[j] + C[k] + D[l] = 0` for four independent arrays without worrying about duplication issues, whereas [0018.4Sum](https://keetcoder.com/problems/0018.4sum.html) and [0015.3Sum](https://keetcoder.com/problems/0015.3sum.html) involve finding combinations that sum up to 0 within a single array (set), which is much more difficult!**

Having solved two sum problems with hash methods, many may feel hash methods can also work for three sum and four sum problems.

Actually, it's possible but very cumbersome, and deduplication causes code efficiency to be low.

In [0015.3Sum](https://keetcoder.com/problems/0015.3sum.html), I provided both hash and two-pointer solutions, and one can readily feel that hash methods are more cumbersome.

Therefore, for problems like 18.4Sum and 15.3Sum, the two-pointer method is recommended!

## Summary

Many might be familiar with the knowledge of hash tables but find it fragmented.

In this summary, we presented a complete picture of hash tables from the theoretical basics to the classic applications of arrays, sets, and maps.

**We also emphasized, although maps are versatile, when to use arrays and when to use sets.**

I believe this summary will give everyone a comprehensive understanding of hash tables.
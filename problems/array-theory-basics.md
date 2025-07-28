# Basic Array Theory

Arrays are a very fundamental data structure. In interviews, questions that test arrays are generally not difficult in terms of logic but mainly test your ability to manage code.

This means the concept may be simple, but implementing it might not be as straightforward.

First, you need to understand how arrays are stored in memory to truly grasp related interview questions.

**An array is a collection of elements of the same type stored in contiguous memory space.**

An array allows easy access to elements via an index.

Here’s an example with a character array, as shown in this image:

![Algorithm Pass Array](https://file1.kamacoder.com/i/algo/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%84.png)

There are two important points to note:

* **Array indices start at 0.**
* **The memory spaces for arrays are contiguous.**

Precisely because arrays occupy contiguous memory addresses, deleting or adding elements requires moving other elements' addresses.

For instance, to delete the element at index 3, you would need to move all subsequent elements, as illustrated:

![Algorithm Pass Array 1](https://file1.kamacoder.com/i/algo/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%841.png)

And for those using C++, it’s important to distinguish between vectors and arrays. Vectors are implemented using arrays; strictly speaking, a vector is a container, not an array.

**Elements in an array cannot be deleted but only overwritten.**

Now, let's jump directly to a two-dimensional array to understand how it works:

![](https://file1.kamacoder.com/i/algo/20240606105522.png)

**Are the memory addresses of a two-dimensional array contiguous?**

Memory management differs among programming languages. In C++, for example, two-dimensional arrays are stored contiguously.

Let's do an experiment to test this in C++. Here is the test code:

```CPP
void test_arr() {
    int array[2][3] = {
        {0, 1, 2},
        {3, 4, 5}
    };
    cout << &array[0][0] << " " << &array[0][1] << " " << &array[0][2] << endl;
    cout << &array[1][0] << " " << &array[1][1] << " " << &array[1][2] << endl;
}

int main() {
    test_arr();
}
```

The test addresses are:

```
0x7ffee4065820 0x7ffee4065824 0x7ffee4065828
0x7ffee406582c 0x7ffee4065830 0x7ffee4065834
```

Notice the addresses are in hexadecimal. It’s evident that the addresses of two-dimensional arrays form a continuous line.

Some readers may not understand memory addresses, so here’s a brief explanation. The address 0x7ffee4065820 and 0x7ffee4065824 have a difference of 4, which means four bytes, as this is an array of `int` type, thus the difference between two adjacent elements is 4 bytes.

Similarly, 0x7ffee4065828 and 0x7ffee406582c differ by 4 bytes as well, where in hexadecimal, 8 + 4 = c, meaning 12.

As depicted: 

![Array Memory](https://file1.kamacoder.com/i/algo/20210310150641186.png)

**Thus, in C++, two-dimensional arrays are consecutively spaced in memory.**

In Java, pointers are absent, and the program does not expose the addresses of elements, with address operations entirely handled by the virtual machine.

Hence, you cannot view the address of each element. Let’s conduct an experiment using Java, as an example.

```Java
public static void test_arr() {
    int[][] arr = {{1, 2, 3}, {3, 4, 5}, {6, 7, 8}, {9,9,9}};
    System.out.println(arr[0]);
    System.out.println(arr[1]);
    System.out.println(arr[2]);
    System.out.println(arr[3]);
}
```

The printed addresses are:

```
[I@7852e922
[I@4e25154f
[I@70dea4e
[I@5c647e05
```

These values are in hexadecimal and are processed numbers rather than actual addresses. We can also deduce that the starting addresses of each row in a two-dimensional array lack regularity, let alone continuity.

Thus, a two-dimensional Java array might be arranged as follows:

![Algorithm Pass Array 3](https://file1.kamacoder.com/i/algo/20201214111631844.png)

This concludes the introduction to the theoretical knowledge of arrays you might encounter in interviews.
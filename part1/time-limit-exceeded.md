# The Algorithm of O Actually Timed Out, So How Large is n? 

Some students may not have a clear concept of how fast a computer can run and assume it should be very fast. Then why do some algorithm problems on LeetCode result in a timeout?

How many operations can a computer really execute in 1 second? Let's explore this issue.

## What Does Timeout Mean

![Program Timeout](https://file1.kamacoder.com/i/algo/20200729112716117-20230310124308704.png)

Anyone practicing algorithms on LeetCode has likely encountered the "Time Limit Exceeded" error.

This means the program's running time exceeded the allowed time, which is generally 1 second in an online judge (OJ) environment. For the purpose of explanation, let's assume the timeout is 1 second.

If you have written an $O(n)$ algorithm, you can estimate how large n has to be for the algorithm to take more than 1 second to execute.

If the size of n is enough to make an $O(n)$ algorithm run longer than 1 second, you should start thinking about a solution with an $O(\log n)$ complexity.

## Understanding Computer Performance from Hardware Configuration

The computing speed of a computer mainly depends on its CPU configuration. Take a 2015 MacPro for example, which has a CPU configuration of 2.7 GHz Dual-Core Intel Core i5.

This refers to a 2.7 GHz dual-core i5 processor. What does GHz mean? 1 Hz = 1/s, and 1 Hz is a CPU pulse (you can think of it as a state change, also known as a clock cycle). It's called Hertz, and 1 GHz is how many Hertz?

- 1 GHz = 1000 MHz
- 1 MHz = 1 million Hertz

So 1 GHz equals 1 billion Hertz, meaning the CPU can pulse a billion times per second (that is, it has a billion clock cycles). Don't simply equate one clock cycle to one CPU operation.

For instance, executing 1 + 2 = 3 requires four actions for the CPU: Step 1: load 1 into a register; Step 2: load 2 into a register; Step 3: perform addition; Step 4: save 3.

Moreover, the CPU doesn't just run our program; it also executes the operating system and other tasks. Our program is just one among many processes.

So, how many operations can our program actually execute in 1 second on a computer?

## Conducting a Test Experiment

To measure how much data can be processed in 1 second, consider three factors:

- The time CPU takes to execute each instruction can greatly vary; for example, addition and multiplication operations take different amounts of time.
- Most computer systems use caching in memory management, so frequently accessing data at the same address takes less time than accessing non-adjacent elements.
- Multiple programs run concurrently on a computer, with each having different processes and threads competing for resources.

Although many factors affect performance, you can still get a rough estimate of how long your program will take to run.

Quoting from Algorithm 4:

- A rocket scientist needs to know whether a test rocket will land in the ocean or in the city;
- Medical researchers need to know if a drug test will kill or cure the test subjects;

Thus, **software engineers developing computer programs should be able to estimate whether the program will take a second or a year to run**.

This is fundamental, so the above errors don't matter.

The following example uses C++ code:

Test Hardware: 2015 MacPro, CPU configuration: 2.7 GHz Dual-Core Intel Core i5

Three functions were implemented with time complexities of $O(n)$, $O(n^2)$, and $O(n \log n)$, using addition operations for uniform testing.

```cpp
// O(n)
void function1(long long n) {
    long long k = 0;
    for (long long i = 0; i < n; i++) {
        k++;
    }
}
```

```cpp
// O(n^2)
void function2(long long n) {
    long long k = 0;
    for (long long i = 0; i < n; i++) {
        for (long j = 0; j < n; j++) {
            k++;
        }
    }
}
```

```cpp
// O(nlogn)
void function3(long long n) {
    long long k = 0;
    for (long long i = 0; i < n; i++) {
        for (long long j = 1; j < n; j = j*2) { // Note here j=1
            k++;
        }
    }
}
```

Check how the runtime changes with the scale of n for these three functions, starting with function1 by commenting out function2 and function3.

```cpp
int main() {
    long long n; // Data size
    while (1) {
        cout << "Input n: ";
        cin >> n;
        milliseconds start_time = duration_cast<milliseconds>(
            system_clock::now().time_since_epoch()
        );
        function1(n);
        // function2(n);
        // function3(n);
        milliseconds end_time = duration_cast<milliseconds>(
            system_clock::now().time_since_epoch()
        );
        cout << "Time elapsed: " << milliseconds(end_time).count() - milliseconds(start_time).count()
            <<" ms"<< endl;
    }
}
```

Check the run effect shown below:

![Program Timeout Image 2](https://file1.kamacoder.com/i/algo/20200729200018460-20230310124315093.png)

An $O(n)$ algorithm can perform roughly 5 * (10^8) calculations in 1 second. You can infer that an $O(n^2)$ algorithm handles data of approximately 5 * (10^8) square root scale in 1 second. Experiment data is as follows.

![Program Timeout Image 3](https://file1.kamacoder.com/i/algo/2020072919590970-20230310124318532.png)

The $O(n^2)$ algorithm can perform approximately 22,500 calculations in 1 second, validating the previous inference.

Finally, infer the $O(n \log n)$ complexity's data scale in 1 second.

It should theoretically be a magnitude smaller than $O(n)$ because $\log n$ complexity is very quick. Check the experiment results below.

![Program Timeout Image 4](https://file1.kamacoder.com/i/algo/20200729195729407-20230310124322232.png)

The $O(n \log n)$ algorithm can perform approximately 2 * (10^7) calculations in 1 second, which aligns with expectations.

These are the results collected from testing on my personal PC. They might not be precisely accurate, but they should be fairly close. You can test them on your machine to verify.

**Overall Test Data Summary:**

![Program Timeout Image 1](https://file1.kamacoder.com/i/algo/20201208231559175-20230310124325152.png)

As for $O(\log n)$ and $O(n^3)$ time complexities, these can be tested similarly to determine scale sizes processed in 1 second.

## Complete Test Code

```cpp
#include <iostream>
#include <chrono>
#include <thread>
using namespace std;
using namespace chrono;
// O(n)
void function1(long long n) {
    long long k = 0;
    for (long long i = 0; i < n; i++) {
        k++;
    }
}

// O(n^2)
void function2(long long n) {
    long long k = 0;
    for (long long i = 0; i < n; i++) {
        for (long j = 0; j < n; j++) {
            k++;
        }
    }
}

// O(nlogn)
void function3(long long n) {
    long long k = 0;
    for (long long i = 0; i < n; i++) {
        for (long long j = 1; j < n; j = j*2) { // Note here j=1
            k++;
        }
    }
}
int main() {
    long long n; // Data size
    while (1) {
        cout << "Input n: ";
        cin >> n;
        milliseconds start_time = duration_cast<milliseconds>(
            system_clock::now().time_since_epoch()
        );
        function1(n);
        // function2(n);
        // function3(n);
        milliseconds end_time = duration_cast<milliseconds>(
            system_clock::now().time_since_epoch()
        );
        cout << "Time elapsed: " << milliseconds(end_time).count() - milliseconds(start_time).count()
            <<" ms"<< endl;
    }
}
```

Java Version

```java
import java.util.Scanner;

public class TimeComplexity {
    // o(n)
    public static void function1(long n) {
        System.out.println("o(n) algorithm");
        long k = 0;
        for (long i = 0; i < n; i++) {
            k++;
        }
    }

    // o(n^2)
    public static void function2(long n) {
        System.out.println("o(n^2) algorithm");
        long k = 0;
        for (long i = 0; i < n; i++) {
            for (long j = 0; j < n; j++) {
                k++;
            }
        }
    }

    // o(nlogn)
    public static void function3(long n) {
        System.out.println("o(nlogn) algorithm");
        long k = 0;
        for (long i = 0; i < n; i++) {
            for (long j = 1; j < n; j = j * 2) { // Note here j=1
                k++;
            }
        }
    }

    public static void main(String[] args) {
        while(true) {
            Scanner in = new Scanner(System.in);
            System.out.print("Input n: ");
            int n = in.nextInt();
            long startTime = System.currentTimeMillis();

            function1(n);
            // function2(n);
            // function3(n);

            long endTime = System.currentTimeMillis();
            long costTime = endTime - startTime;
            System.out.println("Algorithm Time Elapsed == " + costTime + "ms");
        }
    }
}
```

## Summary

This article provides a detailed analysis on why programs might time out on LeetCode and offers insights into how a CPU's speed can estimate runtime. A hands-on experiment shows approximately how large n must be for $O(n)$ algorithms to run for one second. Finally, it provides the possible data size that different time complexities can compute in one second. 

It's advisable for readers to conduct their own experiments and verify results. 

With this, you should gain an overall understanding of the scale of data when a program times out.
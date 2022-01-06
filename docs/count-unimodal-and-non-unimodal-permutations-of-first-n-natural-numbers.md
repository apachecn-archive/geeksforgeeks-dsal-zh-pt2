# 统计前 N 个自然数的单峰和非单峰排列

> 原文:[https://www . geesforgeks . org/count-第一个 n 个自然数的单峰和非单峰排列/](https://www.geeksforgeeks.org/count-unimodal-and-non-unimodal-permutations-of-first-n-natural-numbers/)

给定一个整数 **N** ，任务是统计可能的整数**【1，N】**的**单峰**和**非单峰**排列的总数。

> **单峰排列**是增加到某一点，然后开始减少的排列。
> 除**单峰排列外，**所有其他排列均为**非单峰**排列。

**注意:**由于总计数可以很大，所以打印模 10 <sup>9</sup> +7。

**示例:**

> **输入:** N = 3
> **输出:** 4 2
> **解释:**
> 所有可能的单峰排列为{1，2，3}、{1，3，2}、{2，3，1}、{3，2，1}。
> 因此，单峰排列数为 4。
> 剩余排列为{2，1，3}、{3，1，2}。
> 因此，非单峰排列的计数为 2。
> 
> **输入:**N = 4
> T3】输出: 8 16

**天真方法:**最简单的方法是[从范围**【1，N】**](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)中生成所有可能的整数排列，然后打印出所有那些单峰排列的计数。相应地打印单峰和非单峰排列的计数。
***时间复杂度:** O(N！)*
***辅助空间:** O(N)*

**高效法:**对上述方法进行优化，其思路是先求出给定整数 **N** 可能的单峰排列总数，然后求出非单峰排列数，从排列总数中减去单峰排列数。以下是步骤:

1.  在无限长数组中构造长度为 **N** 的单峰排列。
2.  将 **N** 放置在排列中的任意位置，则正好有两个位置可以放置**(N–1)<sup>第</sup>元素**，即在 **N** 的左侧或右侧。
3.  假设它向右。现在，第**(N–2)<sup>个</sup>元素**可以放在当前排列的左边或右边。
4.  这种情况会一直持续到 1。注意，除了 **N** 之外，每个元素都有两个选择。
5.  因此长度的单峰排列数 **N** 将为**2<sup>N–1</sup>T5】**
6.  排列总数将为 **N！**。
7.  现在非单模态排列的总数将等于 **(N！–单峰排列)。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

int mod = 1e9 + 7;
const int mx = 1e6;
int fact[mx + 1];

// Function to calculate the
// factorials up to a number
void Calculate_factorial()
{
    fact[0] = 1;

    // Calculate the factorial
    for (int i = 1; i <= mx; i++) {
        fact[i] = i * fact[i - 1];
        fact[i] %= mod;
    }
}

// Function to find power(a, b)
int UniModal_per(int a, int b)
{
    long long int res = 1;

    // Iterate until b exists
    while (b) {

        // If b is divisible by 2
        if (b % 2)
            res = res * a;
        res %= mod;
        a = a * a;
        a %= mod;

        // Decrease the value of b
        b /= 2;
    }

    // Return the answer
    return res;
}

// Function that counts the unimodal
// and non-unimodal permutations of
// a given integer N
void countPermutations(int n)
{

    // Function Call for finding
    // factorials up to N
    Calculate_factorial();

    // Function to count unimodal
    // permutations
    int uni_modal = UniModal_per(2, n - 1);

    // Non-unimodal permutation is
    // N! - unimodal permutations
    int nonuni_modal = fact[n] - uni_modal;

    cout << uni_modal << " " << nonuni_modal;

    return;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 4;

    // Function Call
    countPermutations(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG {

    static int mod = (int)(1e9 + 7);
    static int mx = (int)1e6;
    static int[] fact = new int[(int)mx + 1];

    // Function to calculate the
    // factorials up to a number
    static void Calculate_factorial()
    {
        fact[0] = 1;

        // Calculate the factorial
        for (int i = 1; i <= mx; i++) {
            fact[i] = i * fact[i - 1];
            fact[i] %= mod;
        }
    }

    // Function to find power(a, b)
    static int UniModal_per(int a, int b)
    {
        int res = 1;

        // Iterate until b exists
        while (b > 0) {
            // If b is divisible by 2
            if (b % 2 != 0)
                res = res * a;
            res %= mod;
            a = a * a;
            a %= mod;

            // Decrease the value of b
            b /= 2;
        }

        // Return the answer
        return res;
    }

    // Function that counts the unimodal
    // and non-unimodal permutations of
    // a given integer N
    static void countPermutations(int n)
    {
        // Function Call for finding
        // factorials up to N
        Calculate_factorial();

        // Function to count unimodal
        // permutations
        int uni_modal = UniModal_per(2, n - 1);

        // Non-unimodal permutation is
        // N! - unimodal permutations
        int nonuni_modal = fact[n] - uni_modal;

        System.out.print(uni_modal + " " + nonuni_modal);

        return;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Number N
        int N = 4;

        // Function Call
        countPermutations(N);
    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
mod = 1e9 + 7
mx = 1000000
fact = [0] * (mx + 1)

# Function to calculate the
# factorials up to a number

def Calculate_factorial():

    fact[0] = 1

    # Calculate the factorial
    for i in range(1, mx + 1):
        fact[i] = i * fact[i - 1]
        fact[i] %= mod

# Function to find power(a, b)

def UniModal_per(a, b):

    res = 1

    # Iterate until b exists
    while (b != 0):

        # If b is divisible by 2
        if (b % 2 != 0):
            res = res * a

        res %= mod
        a = a * a
        a %= mod

        # Decrease the value of b
        b //= 2

    # Return the answer
    return res

# Function that counts the unimodal
# and non-unimodal permutations of
# a given integer N

def countPermutations(n):

    # Function Call for finding
    # factorials up to N
    Calculate_factorial()

    # Function to count unimodal
    # permutations
    uni_modal = UniModal_per(2, n - 1)

    # Non-unimodal permutation is
    # N! - unimodal permutations
    nonuni_modal = fact[n] - uni_modal

    print(int(uni_modal), "",
          int(nonuni_modal))

    return

# Driver Code
# Given number N
N = 4

# Function call
countPermutations(N)

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
class GFG
{
    static int mod = (int)(1e9 + 7);
    static int mx = (int)1e6;
    static int[] fact = new int[(int)mx + 1];

    // Function to calculate the
    // factorials up to a number
    static void Calculate_factorial()
    {
        fact[0] = 1;

        // Calculate the factorial
        for (int i = 1; i <= mx; i++)
        {
            fact[i] = i * fact[i - 1];
            fact[i] %= mod;
        }
    }

    // Function to find power(a, b)
    static int UniModal_per(int a, int b)
    {
        int res = 1;

        // Iterate until b exists
        while (b > 0)
        {
            // If b is divisible by 2
            if (b % 2 != 0)
                res = res * a;

            res %= mod;
            a = a * a;
            a %= mod;

            // Decrease the value of b
            b /= 2;
        }

        // Return the answer
        return res;
    }

    // Function that counts the unimodal
    // and non-unimodal permutations of
    // a given integer N
    static void countPermutations(int n)
    {
        // Function Call for finding
        // factorials up to N
        Calculate_factorial();

        // Function to count unimodal
        // permutations
        int uni_modal = UniModal_per(2, n - 1);

        // Non-unimodal permutation is
        // N! - unimodal permutations
        int nonuni_modal = fact[n] - uni_modal;

        Console.Write(uni_modal + " " + nonuni_modal);
        return;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given Number N
        int N = 4;

        // Function Call
        countPermutations(N);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for
      // the above approach
      var mod = parseInt(1e9 + 7);
      var mx = 1000000;
      var fact = new Array(mx + 1).fill(0);

      // Function to calculate the
      // factorials up to a number
      function Calculate_factorial() {
        fact[0] = 1;

        // Calculate the factorial
        for (var i = 1; i <= mx; i++) {
          fact[i] = i * fact[i - 1];
          fact[i] %= mod;
        }
      }

      // Function to find power(a, b)
      function UniModal_per(a, b) {
        var res = 1;

        // Iterate until b exists
        while (b > 0) {
          // If b is divisible by 2
          if (b % 2 !== 0) res = res * a;

          res %= mod;
          a = a * a;
          a %= mod;

          // Decrease the value of b
          b = parseInt(b / 2);
        }

        // Return the answer
        return res;
      }

      // Function that counts the unimodal
      // and non-unimodal permutations of
      // a given integer N
      function countPermutations(n) {
        // Function Call for finding
        // factorials up to N
        Calculate_factorial();

        // Function to count unimodal
        // permutations
        var uni_modal = UniModal_per(2, n - 1);

        // Non-unimodal permutation is
        // N! - unimodal permutations
        var nonuni_modal = fact[n] - uni_modal;

        document.write(uni_modal + " " + nonuni_modal);
        return;
      }

      // Driver Code
      // Given Number N
      var N = 4;

      // Function Call
      countPermutations(N);
    </script>
```

**Output**

```
8 16
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
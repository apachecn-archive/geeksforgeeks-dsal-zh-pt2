# 排列计数，使得给定范围内的 K 个数字之和为偶数

> 原文:[https://www . geeksforgeeks . org/排列计数这样来自给定范围的 k 个数字的和是偶数/](https://www.geeksforgeeks.org/count-of-permutations-such-that-sum-of-k-numbers-from-given-range-is-even/)

给定一个范围**【低，高】**，两者都包括在内，以及一个整数 **K** ，任务是从该范围中选择 **K** 个数字(一个数字可以选择多次)，使得这些 **K** 个数字的和为偶数。打印所有此类排列的数量。

**示例:**

> **输入:**低= 4，高= 5，k = 3
> **输出:** 4
> **说明:**
> 有 4 个有效排列。它们是{4，4，4}、{4，5，5}、{5，4，5}和{5，5，4}，加起来是一个偶数。
> 
> **输入:**低= 1，高= 10，k = 2
> **输出:** 50
> **说明:**
> 有 50 个有效排列。它们是{1，1}、{1，3}，..{1, 9} {2, 2}, {2, 4}, …, {2, 10}, …, {10, 2}, {10, 4}, … {10, 10}.
> 这 50 个排列，每一个加起来就是一个偶数。

**天真方法:**想法是[找到大小为 K 的所有子集](https://www.geeksforgeeks.org/print-subsets-given-size-set/)，使得子集的和为偶数，并且还计算每个所需子集的排列。
***时间复杂度:**O(K *(2<sup>K</sup>)*
***辅助空间:** O(K)*

**高效方法:**思路是利用两个偶数和奇数之和总是偶数的事实。按照以下步骤解决问题:

1.  [求给定范围内偶数和奇数的总计数**【低，高】**](https://www.geeksforgeeks.org/count-odd-and-even-numbers-in-a-range-from-l-to-r/) 。
2.  初始化变量**偶 _ 和= 1** 和**奇 _ 和= 0** 分别存储获取偶和和奇和的方式。
3.  循环 **K 次**，将前一个偶数和存储为**prev _ 偶数=偶数 _ 和**，将前一个奇数和存储为**prev _ 奇数=奇数 _ 和**，其中**偶数 _ 和=(prev _ 偶数*偶数 _ 计数)+(prev _ 奇数*奇数 _ 计数)**和**奇数 _ 和=(prev _ 偶数*奇数 _ 计数)+(prev _ 奇数*偶数 _ 计数)**。
4.  在末尾打印偶数和，因为奇数和有一个计数，因为前一个奇数和将影响下一个偶数和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the number
// of all permutations such that
// sum of K numbers in range is even
int countEvenSum(int low, int high, int k)
{

    // Find total count of even and
    // odd number in given range
    int even_count = high / 2 - (low - 1) / 2;
    int odd_count = (high + 1) / 2 - low / 2;

    long even_sum = 1;
    long odd_sum = 0;

    // Iterate loop k times and update
    // even_sum & odd_sum using
    // previous values
    for(int i = 0; i < k; i++)
    {

        // Update the prev_even and
        // odd_sum
        long prev_even = even_sum;
        long prev_odd = odd_sum;

        // Even sum
        even_sum = (prev_even * even_count) +
                    (prev_odd * odd_count);

        // Odd sum
        odd_sum = (prev_even * odd_count) +
                   (prev_odd * even_count);
    }

    // Return even_sum
    cout << (even_sum);
}

// Driver Code
int main()
{

    // Given ranges
    int low = 4;
    int high = 5;

    // Length of permutation
    int K = 3;

    // Function call
    countEvenSum(low, high, K);
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to return the number
    // of all permutations such that
    // sum of K numbers in range is even
    public static void
    countEvenSum(int low, int high,
                 int k)
    {
        // Find total count of even and
        // odd number in given range
        int even_count = high / 2 - (low - 1) / 2;
        int odd_count = (high + 1) / 2 - low / 2;

        long even_sum = 1;
        long odd_sum = 0;

        // Iterate loop k times and update
        // even_sum & odd_sum using
        // previous values
        for (int i = 0; i < k; i++) {

            // Update the prev_even and
            // odd_sum
            long prev_even = even_sum;
            long prev_odd = odd_sum;

            // Even sum
            even_sum = (prev_even * even_count)
                       + (prev_odd * odd_count);

            // Odd sum
            odd_sum = (prev_even * odd_count)
                      + (prev_odd * even_count);
        }

        // Return even_sum
        System.out.println(even_sum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given ranges
        int low = 4;
        int high = 5;

        // Length of permutation
        int K = 3;

        // Function call
        countEvenSum(low, high, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the number
# of all permutations such that
# sum of K numbers in range is even
def countEvenSum(low, high, k):

    # Find total count of even and
    # odd number in given range
    even_count = high / 2 - (low - 1) / 2
    odd_count = (high + 1) / 2 - low / 2

    even_sum = 1
    odd_sum = 0

    # Iterate loop k times and update
    # even_sum & odd_sum using
    # previous values
    for i in range(0, k):

        # Update the prev_even and
        # odd_sum
        prev_even = even_sum
        prev_odd = odd_sum

        # Even sum
        even_sum = ((prev_even * even_count) +
                     (prev_odd * odd_count))

        # Odd sum
        odd_sum = ((prev_even * odd_count) +
                    (prev_odd * even_count))

    # Return even_sum
    print(int(even_sum))

# Driver Code

# Given ranges
low = 4;
high = 5;

# Length of permutation
K = 3;

# Function call
countEvenSum(low, high, K);

# This code is contributed by Stream_Cipher
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the number
// of all permutations such that
// sum of K numbers in range is even
public static void countEvenSum(int low,
                                int high, int k)
{

    // Find total count of even and
    // odd number in given range
    int even_count = high / 2 - (low - 1) / 2;
    int odd_count = (high + 1) / 2 - low / 2;

    long even_sum = 1;
    long odd_sum = 0;

    // Iterate loop k times and update
    // even_sum & odd_sum using
    // previous values
    for(int i = 0; i < k; i++)
    {

        // Update the prev_even and
        // odd_sum
        long prev_even = even_sum;
        long prev_odd = odd_sum;

        // Even sum
        even_sum = (prev_even * even_count) +
                    (prev_odd * odd_count);

        // Odd sum
        odd_sum = (prev_even * odd_count) +
                   (prev_odd * even_count);
    }

    // Return even_sum
    Console.WriteLine(even_sum);
}

// Driver Code
public static void Main(String[] args)
{

    // Given ranges
    int low = 4;
    int high = 5;

    // Length of permutation
    int K = 3;

    // Function call
    countEvenSum(low, high, K);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to return the number
    // of all permutations such that
    // sum of K numbers in range is even
    function
    countEvenSum(low, high, k)
    {
        // Find total count of even and
        // odd number in given range
        let even_count = high / 2 - (low - 1) / 2;
        let odd_count = (high + 1) / 2 - low / 2;

        let even_sum = 1;
        let odd_sum = 0;

        // Iterate loop k times and update
        // even_sum & odd_sum using
        // previous values
        for (let i = 0; i < k; i++) {

            // Update the prev_even and
            // odd_sum
            let prev_even = even_sum;
            let prev_odd = odd_sum;

            // Even sum
            even_sum = (prev_even * even_count)
                       + (prev_odd * odd_count);

            // Odd sum
            odd_sum = (prev_even * odd_count)
                      + (prev_odd * even_count);
        }

        // Return even_sum
        document.write(even_sum);
    }

// Driver Code

     // Given ranges
        let low = 4;
        let high = 5;

        // Length of permutation
        let K = 3;

        // Function call
        countEvenSum(low, high, K);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*
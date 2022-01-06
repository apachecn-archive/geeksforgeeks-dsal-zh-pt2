# 计算总和可被 k 整除的所有子阵列

> 原文:[https://www . geesforgeks . org/count-子数组-和-整除-k/](https://www.geeksforgeeks.org/count-sub-arrays-sum-divisible-k/)

给你一个正整数和/或负整数的数组和一个值 K，任务是找出所有和能被 K 整除的子数组的个数？
**例:**

```
Input  : arr[] = {4, 5, 0, -2, -3, 1}, 
         K = 5
Output : 7
// there are 7 sub-arrays whose sum is divisible by K
// {4, 5, 0, -2, -3, 1}
// {5}
// {5, 0}
// {5, 0, -2, -3}
// {0}
// {0, -2, -3}
// {-2, -3}
```

这个问题的简单解决方案是逐个计算所有可能的子阵列的和，并检查是否能被 k 整除。这种方法的时间复杂度是 O(n^2).
一个**高效的解决方案**是基于下面的观察。

```
Let there be a subarray (i, j) whose sum is divisible by k
  sum(i, j) = sum(0, j) - sum(0, i-1)
Sum for any subarray can be written as q*k + rem where q 
is a quotient and rem is remainder
Thus,     
    sum(i, j) = (q1 * k + rem1) - (q2 * k + rem2)
    sum(i, j) = (q1 - q2)k + rem1-rem2

We see, for sum(i, j) i.e. for sum of any subarray to be
divisible by k, the RHS should also be divisible by k.
(q1 - q2)k is obviously divisible by k, for (rem1-rem2) to 
follow the same, rem1 = rem2 where
    rem1 = Sum of subarray (0, j) % k
    rem2 = Sum of subarray (0, i-1) % k 
```

所以如果从索引 i'th 到 j'th 的任何子数组和都可以被 k 整除，那么我们可以说**a[0]+…a[I-1](mod k)= a[0]+…+a[j](mod k)**
上面的解释是由 Ekta Goel 提供的。
所以我们需要找到这样一对满足上述条件的指标(I，j)。下面是算法:

*   制作一个大小为 k 的辅助数组作为**Mod【k】**。这个数组保存了我们在将累积和除以 arr[]中的任何索引后得到的每个余数的计数。
*   现在开始计算累积和，同时用 K 取它的 mod，无论哪个余数，我们得到的余数增量计数为 1，作为 Mod[]辅助数组中的索引。由每对具有相同值(cumSum % k)的位置组成的子阵列构成一个连续范围，其和可被 k 整除。
*   现在遍历 Mod[]辅助数组，对于任意 Mod[i] > 1，我们可以通过**(Mod[I]*(Mod[I]–1))/2**的方式选择子数组的任意两对索引。对所有余数< k 做同样的操作，并总结结果，结果将是可被 k 整除的所有可能子数组的数目

## C++

```
// C++ program to find count of subarrays with
// sum divisible by k.
#include <bits/stdc++.h>
using namespace std;

// Handles all the cases
// function to find all sub-arrays divisible by k
// modified to handle negative numbers as well
int subCount(int arr[], int n, int k)
{
    // create auxiliary hash array to count frequency
    // of remainders
    int mod[k];
    memset(mod, 0, sizeof(mod));

    // Traverse original array and compute cumulative
    // sum take remainder of this current cumulative
    // sum and increase count by 1 for this remainder
    // in mod[] array
    int cumSum = 0;
    for (int i = 0; i < n; i++) {
        cumSum += arr[i];

        // as the sum can be negative, taking modulo twice
        mod[((cumSum % k) + k) % k]++;
    }

    int result = 0; // Initialize result

    // Traverse mod[]
    for (int i = 0; i < k; i++)

        // If there are more than one prefix subarrays
        // with a particular mod value.
        if (mod[i] > 1)
            result += (mod[i] * (mod[i] - 1)) / 2;

    // add the elements which are divisible by k itself
    // i.e., the elements whose sum = 0
    result += mod[0];

    return result;
}

// Driver program to run the case
int main()
{
    int arr[] = { 4, 5, 0, -2, -3, 1 };
    int k = 5;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << subCount(arr, n, k) << endl;
    int arr1[] = { 4, 5, 0, -12, -23, 1 };
    int k1 = 5;
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    cout << subCount(arr1, n1, k1) << endl;
    return 0;
}

// This code is corrected by Ashutosh Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of
// subarrays with sum divisible by k.
import java.util.*;

class GFG {

    // Handles all the cases
    // function to find all sub-arrays divisible by k
    // modified to handle negative numbers as well
    static int subCount(int arr[], int n, int k)
    {

        // create auxiliary hash array to
        // count frequency of remainders
        int mod[] = new int[k];
        Arrays.fill(mod, 0);

        // Traverse original array and compute cumulative
        // sum take remainder of this current cumulative
        // sum and increase count by 1 for this remainder
        // in mod[] array
        int cumSum = 0;
        for (int i = 0; i < n; i++) {
            cumSum += arr[i];

            // as the sum can be negative, taking modulo twice
            mod[((cumSum % k) + k) % k]++;
        }

        // Initialize result
        int result = 0;

        // Traverse mod[]
        for (int i = 0; i < k; i++)

            // If there are more than one prefix subarrays
            // with a particular mod value.
            if (mod[i] > 1)
                result += (mod[i] * (mod[i] - 1)) / 2;

        // add the elements which are divisible by k itself
        // i.e., the elements whose sum = 0
        result += mod[0];

        return result;
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 4, 5, 0, -2, -3, 1 };
        int k = 5;
        int n = arr.length;
        System.out.println(subCount(arr, n, k));
        int arr1[] = { 4, 5, 0, -12, -23, 1 };
        int k1 = 5;
        int n1 = arr1.length;
        System.out.println(subCount(arr1, n1, k1));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# count of subarrays with
# sum divisible by k.

# Handles all the cases
# function to find all
# sub-arrays divisible by k
# modified to handle
# negative numbers as well
def subCount(arr, n, k):

    # create auxiliary hash
    # array to count frequency
    # of remainders
    mod =[]
    for i in range(k + 1):
        mod.append(0)

    # Traverse original array
    # and compute cumulative
    # sum take remainder of this
    # current cumulative
    # sum and increase count by
    # 1 for this remainder
    # in mod[] array
    cumSum = 0
    for i in range(n):
        cumSum = cumSum + arr[i]

        # as the sum can be negative,
        # taking modulo twice
        mod[((cumSum % k)+k)% k]= mod[((cumSum % k)+k)% k] + 1

    result = 0  # Initialize result

    # Traverse mod[]
    for i in range(k):

        # If there are more than
        # one prefix subarrays
        # with a particular mod value.
        if (mod[i] > 1):
            result = result + (mod[i]*(mod[i]-1))//2

    # add the elements which
    # are divisible by k itself
    # i.e., the elements whose sum = 0
    result = result + mod[0]

    return result

# driver code

arr = [4, 5, 0, -2, -3, 1]
k = 5
n = len(arr)

print(subCount(arr, n, k))
arr1 = [4, 5, 0, -12, -23, 1]

k1 = 5
n1 = len(arr1)
print(subCount(arr1, n1, k1))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find count of
// subarrays with sum divisible by k.
using System;

class GFG {

    // Handles all the cases
    // function to find all sub-arrays divisible by k
    // modified to handle negative numbers as well
    static int subCount(int[] arr, int n, int k)
    {
        // create auxiliary hash array to
        // count frequency of remainders
        int[] mod = new int[k];

        // Traverse original array and compute cumulative
        // sum take remainder of this current cumulative
        // sum and increase count by 1 for this remainder
        // in mod[] array
        int cumSum = 0;
        for (int i = 0; i < n; i++) {
            cumSum += arr[i];

            // as the sum can be negative, taking modulo twice
            mod[((cumSum % k) + k) % k]++;
        }

        // Initialize result
        int result = 0;

        // Traverse mod[]
        for (int i = 0; i < k; i++)

            // If there are more than one prefix subarrays
            // with a particular mod value.
            if (mod[i] > 1)
                result += (mod[i] * (mod[i] - 1)) / 2;

        // add the elements which are divisible by k itself
        // i.e., the elements whose sum = 0
        result += mod[0];

        return result;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 4, 5, 0, -2, -3, 1 };
        int k = 5;
        int n = arr.Length;
        Console.WriteLine(subCount(arr, n, k));
        int[] arr1 = { 4, 5, 0, -12, -23, 1 };
        int k1 = 5;
        int n1 = arr1.Length;
        Console.WriteLine(subCount(arr1, n1, k1));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
    // Javascript program to find count of
    // subarrays with sum divisible by k.

    // Handles all the cases
    // function to find all sub-arrays divisible by k
    // modified to handle negative numbers as well
    function subCount(arr, n, k)
    {
        // create auxiliary hash array to
        // count frequency of remainders
        let mod = new Array(k);
        mod.fill(0);

        // Traverse original array and compute cumulative
        // sum take remainder of this current cumulative
        // sum and increase count by 1 for this remainder
        // in mod[] array
        let cumSum = 0;
        for (let i = 0; i < n; i++) {
            cumSum += arr[i];

            // as the sum can be negative, taking modulo twice
            mod[((cumSum % k) + k) % k]++;
        }

        // Initialize result
        let result = 0;

        // Traverse mod[]
        for (let i = 0; i < k; i++)

            // If there are more than one prefix subarrays
            // with a particular mod value.
            if (mod[i] > 1)
                result += parseInt((mod[i] * (mod[i] - 1)) / 2, 10);

        // add the elements which are divisible by k itself
        // i.e., the elements whose sum = 0
        result += mod[0];

        return result;
    }

    let arr = [ 4, 5, 0, -2, -3, 1 ];
    let k = 5;
    let n = arr.length;
    document.write(subCount(arr, n, k) + "</br>");
    let arr1 = [ 4, 5, 0, -12, -23, 1 ];
    let k1 = 5;
    let n1 = arr1.length;
    document.write(subCount(arr1, n1, k1));

</script>
```

输出:

```
7
7
```

时间复杂度:O(n + k)
辅助空间:O(k)
**参考文献**:
[http://stackoverflow . com/questions/16605991/子阵数-可被 k 整除](http://stackoverflow.com/questions/16605991/number-of-subarrays-divisible-by-k)
本文由[**Shashank Mishra(Gulu)**](https://www.facebook.com/shashank.mishra.92167)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
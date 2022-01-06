# 最小化数组中要相加的整数的数量，使每个相邻的对共质数

> 原文:[https://www . geeksforgeeks . org/最小化数组中要添加的整数的数量以使每个相邻对成为同素/](https://www.geeksforgeeks.org/minimize-count-of-integers-to-be-added-in-array-to-make-each-adjacent-pairs-co-prime/)

给定一个整数数组**arr[]****N**个整数，任务是
通过将数组中的最小整数相加，使数组中的每个相邻对成为同素的。如果不可能，返回-1。

**示例:**

> **输入:** N = 2，arr = [7，42]
> **输出:** 1
> **说明:**加 11 后，最终数组为[7，11，42]。所有相邻的元素现在都是互质的
> 
> **输入:** N = 4，arr = [2200，42，2184，17]
> **输出:** 3
> **说明:** 43，2195，2199 可以加入当前数组。最终排序的数组将是[17，42，43，2184，2195，2199，2200]，所有相邻的对都是互素的。

**方法:**给定的问题可以通过做一些观察和基本数论来解决。可以遵循以下步骤:

*   [按非递减顺序排列数组](https://www.geeksforgeeks.org/find-the-non-decreasing-order-array-from-given-array/)
*   [从左向右迭代](https://www.geeksforgeeks.org/for_each-loop-c/)并检查每个相邻对是否存在以下情况:
*   如果当前对是[互质](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)，则不需要添加任何额外的元素
*   如果当前对不是互质，则迭代元素之间的所有值，并检查当前值是否与左右对都是互质的。
*   否则，总是有可能添加两个彼此互质的值以及分别具有左右值的值。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum additions
// required such that no adjacent pairs are
// coprime in their sorted order
int MinimumAdditions(int arr[], int n)
{
    // Sort the given array
    // in non-decreasing order
    sort(arr, arr + n);

    // First check if any two adjacent
    // elements are same then
    // the answer will be -1
    for (int i = 1; i < n; i++) {
        if (arr[i] == arr[i - 1]) {

            // Return directly from here
            return -1;
        }
    }

    // Variable to store the answer
    int ans = 0;

    for (int i = 1; i < n; i++) {
        if (__gcd(arr[i],
                  arr[i - 1])
            == 1) {
            continue;
        }

        // Check for a single middle element
        // Maintain a bool value
        bool found = 0;

        for (int j = arr[i - 1] + 1;
             j <= arr[i] - 1; j++) {
            if (__gcd(arr[i - 1], j) == 1
                && __gcd(j, arr[i]) == 1) {
                found = 1;
            }
        }
        if (found) {
            ans++;
        }
        else {
            ans += 2;
        }
    }

    // return the answer
    return ans;
}

// Driver Code
int main()
{
    int N = 4;
    int arr[] = { 2200, 42, 2184, 17 };
    cout << MinimumAdditions(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

static int gcd(int a, int b)
{
    return b == 0 ? a : gcd(b, a % b);
}

// Function to calculate minimum additions
// required such that no adjacent pairs are
// coprime in their sorted order
static int MinimumAdditions(int []arr, int n)
{
    // Sort the given array
    // in non-decreasing order
    Arrays.sort(arr);

    // First check if any two adjacent
    // elements are same then
    // the answer will be -1
    for (int i = 1; i < n; i++) {
        if (arr[i] == arr[i - 1]) {

            // Return directly from here
            return -1;
        }
    }

    // Variable to store the answer
    int ans = 0;

    for (int i = 1; i < n; i++) {
        if (gcd(arr[i],
                  arr[i - 1])
            == 1) {
            continue;
        }

        // Check for a single middle element
        // Maintain a bool value
        int found = 0;

        for (int j = arr[i - 1] + 1;
             j <= arr[i] - 1; j++) {
            if (gcd(arr[i - 1], j) == 1
                && gcd(j, arr[i]) == 1) {
                found = 1;
            }
        }
        if (found!=0) {
            ans++;
        }
        else {
            ans += 2;
        }
    }

    // return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
    {
    int N = 4;
    int []arr = { 2200, 42, 2184, 17 };
    System.out.println(MinimumAdditions(arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach
import math

# Function to calculate minimum additions
# required such that no adjacent pairs are
# coprime in their sorted order
def MinimumAdditions(arr, n):

    # Sort the given array
    # in non-decreasing order
    arr.sort()

    # First check if any two adjacent
    # elements are same then
    # the answer will be -1
    for i in range(1,  n):
        if (arr[i] == arr[i - 1]):

            # Return directly from here
            return -1

    # Variable to store the answer
    ans = 0

    for i in range(1, n):
        if (math.gcd(arr[i],
                     arr[i - 1])
                == 1):
            continue

        # Check for a single middle element
        # Maintain a bool value
        found = 0

        for j in range(arr[i - 1] + 1,
                       arr[i]):
            if (math.gcd(arr[i - 1], j) == 1
                    and math.gcd(j, arr[i]) == 1):
                found = 1

        if (found):
            ans += 1

        else:
            ans += 2

    # return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    N = 4
    arr = [2200, 42, 2184, 17]
    print(MinimumAdditions(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int gcd(int a, int b)
{
    return b == 0 ? a : gcd(b, a % b);
}

// Function to calculate minimum additions
// required such that no adjacent pairs are
// coprime in their sorted order
static int MinimumAdditions(int []arr, int n)
{
    // Sort the given array
    // in non-decreasing order
    Array.Sort(arr);

    // First check if any two adjacent
    // elements are same then
    // the answer will be -1
    for (int i = 1; i < n; i++) {
        if (arr[i] == arr[i - 1]) {

            // Return directly from here
            return -1;
        }
    }

    // Variable to store the answer
    int ans = 0;

    for (int i = 1; i < n; i++) {
        if (gcd(arr[i],
                  arr[i - 1])
            == 1) {
            continue;
        }

        // Check for a single middle element
        // Maintain a bool value
        int found = 0;

        for (int j = arr[i - 1] + 1;
             j <= arr[i] - 1; j++) {
            if (gcd(arr[i - 1], j) == 1
                && gcd(j, arr[i]) == 1) {
                found = 1;
            }
        }
        if (found!=0) {
            ans++;
        }
        else {
            ans += 2;
        }
    }

    // return the answer
    return ans;
}

// Driver Code
public static void Main()
{
    int N = 4;
    int []arr = { 2200, 42, 2184, 17 };
    Console.Write(MinimumAdditions(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach
       // Recursive function to return gcd of a and b
       function __gcd(a, b) {
           // Everything divides 0
           if (a == 0)
               return b;
           if (b == 0)
               return a;

           // base case
           if (a == b)
               return a;

           // a is greater
           if (a > b)
               return __gcd(a - b, b);
           return __gcd(a, b - a);
       }

       // Function to calculate minimum additions
       // required such that no adjacent pairs are
       // coprime in their sorted order
       function MinimumAdditions(arr, n) {
           // Sort the given array
           // in non-decreasing order
           arr.sort(function (a, b) { return a - b; });

           // First check if any two adjacent
           // elements are same then
           // the answer will be -1
           for (let i = 1; i < n; i++) {
               if (arr[i] == arr[i - 1]) {

                   // Return directly from here
                   return -1;
               }
           }

           // Variable to store the answer
           let ans = 0;

           for (let i = 1; i < n; i++) {
               if (__gcd(arr[i],
                   arr[i - 1])
                   == 1) {
                   continue;
               }

               // Check for a single middle element
               // Maintain a bool value
               let found = 0;

               for (let j = arr[i - 1] + 1;
                   j <= arr[i] - 1; j++) {
                   if (__gcd(arr[i - 1], j) == 1
                       && __gcd(j, arr[i]) == 1) {
                       found = 1;
                   }
               }
               if (found) {
                   ans++;
               }
               else {
                   ans += 2;
               }
           }

           // return the answer
           return ans;
       }

       // Driver Code

       let N = 4;
       let arr = [2200, 42, 2184, 17];
       document.write(MinimumAdditions(arr, N));

    // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
3
```

**时间复杂度:** O(Nlog(N) + M)，其中 M 为数组中最大元素
T3】辅助空间: O(1)
# 给定范围内最后 K 位数字相等的整数个数

> 原文:[https://www . geeksforgeeks . org/给定范围内的整数计数-最后 k 位等于/](https://www.geeksforgeeks.org/count-of-integers-in-given-range-having-their-last-k-digits-are-equal/)

给定从 **L** 到 **R** 的范围和一个整数 **K** ，任务是计算给定范围内的整数数量，使得它们的最后一个 **K** 位数相等。

**示例:**

> **输入:** L = 49，R = 101，K=2
> **输出:** 6
> **说明:**有 6 个可能的整数 t，即 55、66、77、88、99 和 100，使得它们的最后一个 K(即 2)位数相等。
> 
> **输入:** L = 10，R = 20，K = 2
> T3】输出: 1

**有效方法:**可以观察到在范围 **1** 到 **X** 中最后一个 **K** 位数等于一个整数 **z** (即 i % 10 <sup>K</sup> = z)的整数个数为**(X–z)/10<sup>K</sup>+1**。根据这一观察，可以通过以下步骤解决上述问题:

1.  假设**整数(X，K)** 代表从 **1** 到 **X** 的整数计数，最后一个 **K** 位数相等。
2.  要计算 **intCount(X，K)** ，迭代具有 **K** 位的 **z** 的所有可能性(即， *{00…0，11…1，22…2，33…3，44…4，…)。，99…9 }* )并保持它们的和为所需值。
3.  因此 **L** 到 **R** 范围内的整数个数可以得到为 **intCount(R，K)–int count(L-1，K)** 。

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// integers from 1 to X having the
// last K digits as equal
int intCount(int X, int K)
{
    // Stores the total count of integers
    int ans = 0;

    // Loop to iterate over all
    // possible values of z
    for (int z = 0; z < pow(10, K);
         z += (pow(10, K) - 1) / 9) {

        // Terminate the loop when z > X
        if (z > X)
            break;

        // Add count of integers with
        // last K digits equal to z
        ans += ((X - z) / pow(10, K) + 1);
    }

    // Return count
    return ans;
}

// Function to return the count of
// integers from L to R having the
// last K digits as equal
int intCountInRange(int L, int R, int K)
{
    return (intCount(R, K)
            - intCount(L - 1, K));
}

// Driver Code
int main()
{
    int L = 49;
    int R = 101;
    int K = 2;

    // Function Call
    cout << intCountInRange(L, R, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program of the above approach
import java.util.*;

class GFG{

// Function to return the count of
// integers from 1 to X having the
// last K digits as equal
static int intCount(int X, int K)
{
    // Stores the total count of integers
    int ans = 0;

    // Loop to iterate over all
    // possible values of z
    for (int z = 0; z < Math.pow(10, K);
         z += (Math.pow(10, K) - 1) / 9) {

        // Terminate the loop when z > X
        if (z > X)
            break;

        // Add count of integers with
        // last K digits equal to z
        ans += ((X - z) / Math.pow(10, K) + 1);
    }

    // Return count
    return ans;
}

// Function to return the count of
// integers from L to R having the
// last K digits as equal
static int intCountInRange(int L, int R, int K)
{
    return (intCount(R, K)
            - intCount(L - 1, K));
}

// Driver Code
public static void main(String[] args)
{
    int L = 49;
    int R = 101;
    int K = 2;

    // Function Call
    System.out.print(intCountInRange(L, R, K));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the count of
# integers from 1 to X having the
# last K digits as equal
def intCount(X, K):

    # Stores the total count of integers
    ans = 0

    # Loop to iterate over all
    # possible values of z
    for z in range(0, int(pow(10, K)),
                     int((pow(10, K) - 1) / 9)):

        # Terminate the loop when z > X
        if (z > X):
            break

        # Add count of integers with
        # last K digits equal to z
        ans += int((X - z) / int(pow(10, K)) + 1)

    # Return count
    return ans

# Function to return the count of
# integers from L to R having the
# last K digits as equal
def intCountInRange(L, R, K):

    return(intCount(R, K) - intCount(L - 1, K))

# Driver Code
L = 49
R = 101
K = 2

# Function Call
print(intCountInRange(L, R, K))

# This code is contributed by sanjoy_62
```

## C#

```
// C# Program of the above approach
using System;

class GFG{

// Function to return the count of
// integers from 1 to X having the
// last K digits as equal
static int intCount(int X, int K)
{
    // Stores the total count of integers
    int ans = 0;

    // Loop to iterate over all
    // possible values of z
    for (int z = 0; z < Math.Pow(10, K);
         z += ((int)Math.Pow(10, K) - 1) / 9) {

        // Terminate the loop when z > X
        if (z > X)
            break;

        // Add count of integers with
        // last K digits equal to z
        ans += ((X - z) / (int)Math.Pow(10, K) + 1);
    }

    // Return count
    return ans;
}

// Function to return the count of
// integers from L to R having the
// last K digits as equal
static int intCountInRange(int L, int R, int K)
{
    return (intCount(R, K)
            - intCount(L - 1, K));
}

// Driver Code
public static void Main(String[] args)
{
    int L = 49;
    int R = 101;
    int K = 2;

    // Function Call
    Console.Write(intCountInRange(L, R, K));

}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to return the count of
// integers from 1 to X having the
// last K digits as equal
function intCount(X, K)
{

    // Stores the total count of integers
    let ans = 0;

    // Loop to iterate over all
    // possible values of z
    for(let z = 0; z < Math.pow(10, K);
            z += Math.floor((Math.pow(10, K) - 1) / 9))
    {

        // Terminate the loop when z > X
        if (z > X)
            break;

        // Add count of integers with
        // last K digits equal to z
        ans += Math.floor(((X - z) /
               Math.pow(10, K) + 1));
    }

    // Return count
    return ans;
}

// Function to return the count of
// integers from L to R having the
// last K digits as equal
function intCountInRange(L, R, K)
{
    return(intCount(R, K) -
           intCount(L - 1, K));
}

// Driver Code
let L = 49;
let R = 101;
let K = 2;

// Function Call
document.write(intCountInRange(L, R, K));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
6
```

**时间复杂度:***O(log K)*
T5】空间复杂度: *O(1)*
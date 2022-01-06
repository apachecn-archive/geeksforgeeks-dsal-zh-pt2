# 使用给定数组中的任意一级计算到达第 n 级楼梯的路径

> 原文:[https://www . geeksforgeeks . org/count-到达第 n 级的方法-使用给定数组的任意步长/](https://www.geeksforgeeks.org/count-ways-to-reach-the-nth-stair-using-any-step-from-the-given-array/)

给定 **N** 级楼梯，站在底部的人想到达顶部。他可以从给定的正整数数组**中爬上任意数量的台阶。任务是找出所有可能到达顶端的方法。
**例:**** 

> **输入:** arr[] = {1，3，5}，N = 5
> **输出:**5
> (0->1->2->3->4->5)、(0 - > 1 - > 2 - > 5)、
> (0 - > 1 - > 4 - > 5)、(0 - > 3 - > 4 -
> **输入:** arr[] = {1，2，3}，N = 10
> **输出:** 274

**天真的做法:**利用递归，找到所有可能的方法并进行计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to return the
// total ways to reach the n'th stair
int countWays(int n, int arr[], int len)
{
    // Base case
    if (n == 0)
        return 1;

    // To store the number of ways
    int no_ways = 0;

    // Iterate each element of the given array
    for (int i = 0; i < len; i++) {

        // Here consider only the values of
        // "n - arr[i]" >= 0 because negative values
        // of n in the stair function are
        // not defined
        if (n - arr[i] >= 0) {
            no_ways += countWays(n - arr[i], arr, len);
        }
    }
    return no_ways;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 5 };
    int len = sizeof(arr) / sizeof(int);
    int n = 5;

    cout << countWays(n, arr, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Recursive function to return the
    // total ways to reach the n'th stair
    static int countWays(int n, int arr[], int len)
    {
        // Base case
        if (n == 0)
            return 1;

        // To store the number of ways
        int no_ways = 0;

        // Iterate each element of the given array
        for (int i = 0; i < len; i++) {

            // Here consider only the values of
            // "n - arr[i]" >= 0 because negative values
            // of n in the stair function are
            // not defined
            if (n - arr[i] >= 0) {
                no_ways += countWays(n - arr[i], arr, len);
            }
        }
        return no_ways;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 3, 5 };
        int len = arr.length;
        ;
        int n = 5;

        System.out.println(countWays(n, arr, len));
    }
}
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Recursive function to return the
# total ways to reach the n'th stair
def countWays(n, arr):

    # Base case
    if (n == 0):
        return 1

    # To store the number of ways
    no_ways = 0

    # Iterate each element of the given array
    for i in arr:

        # Here consider only the values of
        # "n - arr[i]" >= 0 because negative values
        # of n in the stair function are
        # not defined
        if (n - i >= 0):
            no_ways = no_ways + countWays(n - i, arr)
    return no_ways

# Driver code
arr = [1, 3, 5]
n = 5
print(countWays(n, arr))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Recursive function to return the
// total ways to reach the n'th stair
static int countWays(int n, int []arr,
                            int len)
{
    // Base case
    if (n == 0)
        return 1;

    // To store the number of ways
    int no_ways = 0;

    // Iterate each element
    // of the given array
    for (int i = 0; i < len; i++)
    {

        // Here consider only the values of
        // "n - arr[i]" >= 0 because negative values
        // of n in the stair function are
        // not defined
        if (n - arr[i] >= 0)
        {
            no_ways += countWays(n - arr[i], arr, len);
        }
    }
    return no_ways;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 3, 5 };
    int len = arr.Length;
    int n = 5;

    Console.Write(countWays(n, arr, len));
}
}

// This code is contributed by Mohit Kumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Recursive function to return the
// total ways to reach the n'th stair
function countWays(n, arr, len) {
    // Base case
    if (n == 0)
        return 1;

    // To store the number of ways
    let no_ways = 0;

    // Iterate each element of the given array
    for (let i = 0; i < len; i++) {

        // Here consider only the values of
        // "n - arr[i]" >= 0 because negative values
        // of n in the stair function are
        // not defined
        if (n - arr[i] >= 0) {
            no_ways += countWays(n - arr[i], arr, len);
        }
    }
    return no_ways;
}

// Driver code

let arr = [1, 3, 5];
let len = arr.length;
let n = 5;

document.write(countWays(n, arr, len));

</script>
```

**Output:** 

```
5
```
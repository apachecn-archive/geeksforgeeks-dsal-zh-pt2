# 所有数组元素的二进制表示中连续 1 的最大数量

> 原文:[https://www . geesforgeks . org/所有数组元素的二进制表示的最大连续 1 个数/](https://www.geeksforgeeks.org/maximum-number-of-consecutive-1s-in-binary-representation-of-all-the-array-elements/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是在给定数组的所有元素中找到一个元素的二进制表示中最大的连续 **1 的**个数。
**举例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 2
> 二进制(1) = 01
> 二进制(2) = 10
> 二进制(3) = 11
> 二进制(4) = 100
> **输入:** arr[] = {10，15，37，89}
> **输出:** 4

**方法:**在[这篇](https://www.geeksforgeeks.org/length-longest-consecutive-1s-binary-representation/)文章中已经讨论了一种在一个数的二进制表示中寻找最大连续 1 的计数的方法。相同的方法可以用于为给定数组的所有元素找到相同的值，这些值中的最大值就是所需的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count of
// maximum consecutive 1s in the
// binary representation of x
int maxConsecutiveOnes(int x)
{
    // Initialize result
    int count = 0;

    // Count the number of iterations to
    // reach x = 0.
    while (x != 0) {
        // This operation reduces length
        // of every sequence of 1s by one
        x = (x & (x << 1));

        count++;
    }

    return count;
}

// Function to return the count of
// maximum consecutive 1s in the
// binary representation among all
// the elements of arr[]
int maxOnes(int arr[], int n)
{
    // To store the answer
    int ans = 0;

    // For every element of the array
    for (int i = 0; i < n; i++) {

        // Count of maximum consecutive 1s in
        // the binary representation of
        // the current element
        int currMax = maxConsecutiveOnes(arr[i]);

        // Update the maximum count so far
        ans = max(ans, currMax);
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxOnes(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// maximum consecutive 1s in the
// binary representation of x
static int maxConsecutiveOnes(int x)
{
    // Initialize result
    int count = 0;

    // Count the number of iterations to
    // reach x = 0.
    while (x != 0)
    {
        // This operation reduces length
        // of every sequence of 1s by one
        x = (x & (x << 1));

        count++;
    }
    return count;
}

// Function to return the count of
// maximum consecutive 1s in the
// binary representation among all
// the elements of arr[]
static int maxOnes(int arr[], int n)
{
    // To store the answer
    int ans = 0;

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // Count of maximum consecutive 1s in
        // the binary representation of
        // the current element
        int currMax = maxConsecutiveOnes(arr[i]);

        // Update the maximum count so far
        ans = Math.max(ans, currMax);
    }
    return ans;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 2, 3, 4 };
    int n = arr.length;

    System.out.println(maxOnes(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# maximum consecutive 1s in the
# binary representation of x
def maxConsecutiveOnes(x) :

    # Initialize result
    count = 0;

    # Count the number of iterations to
    # reach x = 0.
    while (x != 0) :

        # This operation reduces length
        # of every sequence of 1s by one
        x = (x & (x << 1));

        count += 1;

    return count;

# Function to return the count of
# maximum consecutive 1s in the
# binary representation among all
# the elements of arr[]
def maxOnes(arr, n) :

    # To store the answer
    ans = 0;

    # For every element of the array
    for i in range(n) :

        # Count of maximum consecutive 1s in
        # the binary representation of
        # the current element
        currMax = maxConsecutiveOnes(arr[i]);

        # Update the maximum count so far
        ans = max(ans, currMax);

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4 ];
    n = len(arr);

    print(maxOnes(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// maximum consecutive 1s in the
// binary representation of x
static int maxConsecutiveOnes(int x)
{
    // Initialize result
    int count = 0;

    // Count the number of iterations to
    // reach x = 0.
    while (x != 0)
    {
        // This operation reduces length
        // of every sequence of 1s by one
        x = (x & (x << 1));

        count++;
    }
    return count;
}

// Function to return the count of
// maximum consecutive 1s in the
// binary representation among all
// the elements of arr[]
static int maxOnes(int []arr, int n)
{
    // To store the answer
    int ans = 0;

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // Count of maximum consecutive 1s in
        // the binary representation of
        // the current element
        int currMax = maxConsecutiveOnes(arr[i]);

        // Update the maximum count so far
        ans = Math.Max(ans, currMax);
    }
    return ans;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 3, 4 };
    int n = arr.Length;

    Console.WriteLine(maxOnes(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the count of
// maximum consecutive 1s in the
// binary representation of x
function maxConsecutiveOnes(x)
{
    // Initialize result
    var count = 0;

    // Count the number of iterations to
    // reach x = 0.
    while (x != 0)
    {
        // This operation reduces length
        // of every sequence of 1s by one
        x = (x & (x << 1));

        count++;
    }
    return count;
}

// Function to return the count of
// maximum consecutive 1s in the
// binary representation among all
// the elements of arr
function maxOnes(arr , n)
{
    // To store the answer
    var ans = 0;

    // For every element of the array
    for (i = 0; i < n; i++)
    {

        // Count of maximum consecutive 1s in
        // the binary representation of
        // the current element
        var currMax = maxConsecutiveOnes(arr[i]);

        // Update the maximum count so far
        ans = Math.max(ans, currMax);
    }
    return ans;
}

// Driver code
var arr = [ 1, 2, 3, 4 ];
var n = arr.length;

document.write(maxOnes(arr, n));

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
2
```
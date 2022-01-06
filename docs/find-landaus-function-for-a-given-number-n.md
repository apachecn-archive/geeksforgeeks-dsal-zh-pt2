# 求给定数 N 的朗道函数

> 原文:[https://www . geesforgeks . org/find-landaus-function-for-a-number-n/](https://www.geeksforgeeks.org/find-landaus-function-for-a-given-number-n/)

给定一个整数 **N** ，任务是找到数字 N 的[朗道函数](https://en.wikipedia.org/wiki/Landau%27s_function)

> 在数论中，**朗道函数**在给定数 n 的所有分区中找到最大的 [LCM](https://www.geeksforgeeks.org/lcm-gq/)
> 
> **例如:**如果 N = 4，那么可能的分区是:
> 1。{1，1，1，1}，LCM = 1
> 2。{1，1，2}，LCM = 2
> 3。{2，2}，LCM = 2
> 4。{1，3}，LCM = 3
> 
> 上述分区中，LCM 最大的分区为{1，3}，为 LCM = 3。

**示例:**

> **输入:** N = 4
> **输出:** 4
> **说明:**
> 4 的分区为[1，1，1，1]，[1，1，2]，[2，2]，[1，3]，[4]，其中最大 LCM 为 LCM 也为 4 的最后一个分区 4 的 LCM。
> 
> **输入:** N = 7
> **输出:** 12
> **说明:**
> 对于 N = 7，最大 LCM 为 12。

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)到[为给定的数 **N** 生成所有可能的分区](https://www.geeksforgeeks.org/generate-unique-partitions-of-an-integer/)，在所有分区中找到 LCM 的最大值。考虑从 **1 到 N** 的每一个整数，使得在每次递归调用时总和 **N** 可以减少这个数，如果在任何递归调用时 **N 减少到零**，则找到存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中的值的 LCM。以下是递归的步骤:

1.  得到数 **N** ，其和必须被分解成两个或多个正整数。
2.  递归地从值 **1 迭代到 N** 作为索引 **i** :
    *   **基本情况:**如果递归调用的值是 **0** ，那么求当前向量中存储的值的 LCM，因为这是将 N 分解成两个或多个正整数的方法之一。

```
if (n == 0)
    findLCM(arr);
```

*   **递归调用:**如果不满足基本情况，则从**【I，N–I】**递归迭代。将当前元素 **j** 推入向量(比如 **arr** )并递归迭代下一个索引，在这个递归结束后，弹出之前插入的元素**j【T9:** 

```
for j in range[i, N]:
    arr.push_back(j);
    recursive_function(arr, j + 1, N - j);
    arr.pop_back(j);
```

1.  在所有递归调用之后，打印所有计算出的 LCM 的最大值。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// To store Landau's function of the number
int Landau = INT_MIN;

// Function to return gcd of 2 numbers
int gcd(int a, int b)
{

    if (a == 0)

        return b;

    return gcd(b % a, a);
}

// Function to return LCM of two numbers
int lcm(int a, int b)
{
    return (a * b) / gcd(a, b);
}

// Function to find max lcm value
// among all representations of n
void findLCM(vector<int>& arr)
{
    int nth_lcm = arr[0];

    for (int i = 1; i < arr.size(); i++)

        nth_lcm = lcm(nth_lcm, arr[i]);

    // Calculate Landau's value
    Landau = max(Landau, nth_lcm);
}

// Recursive function to find different
// ways in which n can be written as
// sum of atleast one positive integers
void findWays(vector<int>& arr, int i, int n)
{
    // Check if sum becomes n,
    // consider this representation
    if (n == 0)
        findLCM(arr);

    // Start from previous element
    // in the representation till n
    for (int j = i; j <= n; j++) {

        // Include current element
        // from representation
        arr.push_back(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack - remove current
        // element from representation
        arr.pop_back();
    }
}

// Function to find the Landau's function
void Landau_function(int n)
{
    vector<int> arr;

    // Using recurrence find different
    // ways in which n can be written
    // as a sum of atleast one +ve integers
    findWays(arr, 1, n);

    // Print the result
    cout << Landau;
}

// Driver Code
int main()
{
    // Given N
    int N = 4;

    // Function Call
    Landau_function(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// To store Landau's function of the number
static int Landau = Integer.MIN_VALUE;

// Function to return gcd of 2 numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return LCM of two numbers
static int lcm(int a, int b)
{
    return (a * b) / gcd(a, b);
}

// Function to find max lcm value
// among all representations of n
static void findLCM(Vector<Integer> arr)
{
    int nth_lcm = arr.get(0);

    for(int i = 1; i < arr.size(); i++)
        nth_lcm = lcm(nth_lcm, arr.get(i));

    // Calculate Landau's value
    Landau = Math.max(Landau, nth_lcm);
}

// Recursive function to find different
// ways in which n can be written as
// sum of atleast one positive integers
static void findWays(Vector<Integer> arr,
                     int i, int n)
{

    // Check if sum becomes n,
    // consider this representation
    if (n == 0)
        findLCM(arr);

    // Start from previous element
    // in the representation till n
    for(int j = i; j <= n; j++)
    {

        // Include current element
        // from representation
        arr.add(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack - remove current
        // element from representation
        arr.remove(arr.size() - 1);
    }
}

// Function to find the Landau's function
static void Landau_function(int n)
{
    Vector<Integer> arr = new Vector<>();

    // Using recurrence find different
    // ways in which n can be written
    // as a sum of atleast one +ve integers
    findWays(arr, 1, n);

    // Print the result
    System.out.print(Landau);
}

// Driver Code
public static void main(String[] args)
{
    // Given N
    int N = 4;

    // Function call
    Landau_function(N);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# To store Landau's function of the number
Landau = -sys.maxsize - 1

# Function to return gcd of 2 numbers
def gcd(a, b):

    if (a == 0):
        return b

    return gcd(b % a, a)

# Function to return LCM of two numbers
def lcm(a, b):

    return (a * b) // gcd(a, b)

# Function to find max lcm value
# among all representations of n
def findLCM(arr):

    global Landau

    nth_lcm = arr[0]

    for i in range(1, len(arr)):
        nth_lcm = lcm(nth_lcm, arr[i])

    # Calculate Landau's value
    Landau = max(Landau, nth_lcm)

# Recursive function to find different
# ways in which n can be written as
# sum of atleast one positive integers
def findWays(arr, i, n):

    # Check if sum becomes n,
    # consider this representation
    if (n == 0):
        findLCM(arr)

    # Start from previous element
    # in the representation till n
    for j in range(i, n + 1):

        # Include current element
        # from representation
        arr.append(j)

        # Call function again
        # with reduced sum
        findWays(arr, j, n - j)

        # Backtrack - remove current
        # element from representation
        arr.pop()

# Function to find the Landau's function
def Landau_function(n):

    arr = []

    # Using recurrence find different
    # ways in which n can be written
    # as a sum of atleast one +ve integers
    findWays(arr, 1, n)

    # Print the result
    print(Landau)

# Driver Code

# Given N
N = 4

# Function call
Landau_function(N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// To store Landau's function of the number
static int Landau = int.MinValue;

// Function to return gcd of 2 numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return LCM of two numbers
static int lcm(int a, int b)
{
    return (a * b) / gcd(a, b);
}

// Function to find max lcm value
// among all representations of n
static void findLCM(List<int> arr)
{
    int nth_lcm = arr[0];

    for(int i = 1; i < arr.Count; i++)
        nth_lcm = lcm(nth_lcm, arr[i]);

    // Calculate Landau's value
    Landau = Math.Max(Landau, nth_lcm);
}

// Recursive function to find different
// ways in which n can be written as
// sum of atleast one positive integers
static void findWays(List<int> arr,
                     int i, int n)
{

    // Check if sum becomes n,
    // consider this representation
    if (n == 0)
        findLCM(arr);

    // Start from previous element
    // in the representation till n
    for(int j = i; j <= n; j++)
    {

        // Include current element
        // from representation
        arr.Add(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack - remove current
        // element from representation
        arr.RemoveAt(arr.Count - 1);
    }
}

// Function to find the Landau's function
static void Landau_function(int n)
{
    List<int> arr = new List<int>();

    // Using recurrence find different
    // ways in which n can be written
    // as a sum of atleast one +ve integers
    findWays(arr, 1, n);

    // Print the result
    Console.Write(Landau);
}

// Driver Code
public static void Main(String[] args)
{

    // Given N
    int N = 4;

    // Function call
    Landau_function(N);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// To store Landau's function of the number
var Landau = -1000000000;

// Function to return gcd of 2 numbers
function gcd(a, b)
{

    if (a == 0)

        return b;

    return gcd(b % a, a);
}

// Function to return LCM of two numbers
function lcm(a, b)
{
    return (a * b) / gcd(a, b);
}

// Function to find max lcm value
// among all representations of n
function findLCM(arr)
{
    var nth_lcm = arr[0];

    for (var i = 1; i < arr.length; i++)

        nth_lcm = lcm(nth_lcm, arr[i]);

    // Calculate Landau's value
    Landau = Math.max(Landau, nth_lcm);
}

// Recursive function to find different
// ways in which n can be written as
// sum of atleast one positive integers
function findWays(arr, i, n)
{
    // Check if sum becomes n,
    // consider this representation
    if (n == 0)
        findLCM(arr);

    // Start from previous element
    // in the representation till n
    for (var j = i; j <= n; j++) {

        // Include current element
        // from representation
        arr.push(j);

        // Call function again
        // with reduced sum
        findWays(arr, j, n - j);

        // Backtrack - remove current
        // element from representation
        arr.pop();
    }
}

// Function to find the Landau's function
function Landau_function(n)
{
    arr = [];

    // Using recurrence find different
    // ways in which n can be written
    // as a sum of atleast one +ve integers
    findWays(arr, 1, n);

    // Print the result
    document.write( Landau);
}

// Driver Code
// Given N
var N = 4;

// Function Call
Landau_function(N);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N <sup>2</sup> )*
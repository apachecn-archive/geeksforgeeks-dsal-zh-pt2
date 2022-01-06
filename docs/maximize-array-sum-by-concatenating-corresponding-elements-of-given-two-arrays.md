# 通过连接给定两个数组的对应元素来最大化数组和

> 原文:[https://www . geeksforgeeks . org/通过连接给定两个数组的对应元素来最大化数组总和/](https://www.geeksforgeeks.org/maximize-array-sum-by-concatenating-corresponding-elements-of-given-two-arrays/)

给定两个相同长度的数组 **A[]** 和 **B[]** ，任务是找出任意顺序连接数组对应元素所能形成的最大数组和。

> **输入:** A[] = {1，2，3，4，5}，B[] = {3，2，1，4，5}
> **输出:** 183
> **说明:**
> 元素的数字连接而成的数字是–
> Join(A[0]，B[0]) = Join(1，3) = 13 或 31
> Join(A[1]，B[1]) = Join(2，2) = 5) = 55
> 因此对于最大和，数组将是{31，22，31，44，55}，和= 183
> **输入:** A[] = {11，23，38，43，59}，B[] = {36，24，17，40，56}
> **输出:** 19850
> **解释:**
> 数字 24) = 2324 或 2423
> Join(A[2]，B[2]) = Join(38，17) = 3817 或 1738
> Join(A[3]，B[3]) = Join(43，40) = 4340 或 4043
> Join(A[4]，B[4]) = Join(59，56) = 5956 或 5659
> 因此对于最大和，数组

**方法:**想法是迭代数组和数组的每个对应元素

1.  通过迭代一个数字的数字将它们连接在一起，并将这些数字加到另一个数字中，可以定义如下:

```
// Join the numbers
for digits in numberA:
    numberB = numberB*10 + digit
```

2.  同样，以相反的顺序连接这些数字，取这些数字的最大值。
3.  用两者中的最大值更新结果数组的相应元素。
4.  类似地，找到结果数组的所有元素，并计算总和。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum array sum by concatenating
// corresponding elements of given two arrays

#include <bits/stdc++.h>
using namespace std;

// Function to join the two numbers
int joinNumbers(int numA, int numB)
{
    int revB = 0;

    // Loop to reverse the digits
    // of the one number
    while (numB > 0) {
        revB = revB * 10 + (numB % 10);
        numB = numB / 10;
    }

    // Loop to join two numbers
    while (revB > 0) {
        numA = numA * 10 + (revB % 10);
        revB = revB / 10;
    }
    return numA;
}

// Function to find the maximum array sum
int findMaxSum(int A[], int B[], int n)
{
    int maxArr[n];

    // Loop to iterate over the two
    // elements of the array
    for (int i = 0; i < n; ++i) {

        int X = joinNumbers(A[i], B[i]);
        int Y = joinNumbers(B[i], A[i]);
        int mx = max(X, Y);
        maxArr[i] = mx;
    }

    // Find the array sum
    int maxAns = 0;
    for (int i = 0; i < n; i++) {
        maxAns += maxArr[i];
    }

    // Return the array sum
    return maxAns;
}

// Driver Code
int main()
{
    int N = 5;
    int A[5] = { 11, 23, 38, 43, 59 };
    int B[5] = { 36, 24, 17, 40, 56 };

    cout << findMaxSum(A, B, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum array sum by concatenating
// corresponding elements of given two arrays
class GFG {

// Function to join the two numbers
static int joinNumbers(int numA, int numB)
{
    int revB = 0;

    // Loop to reverse the digits
    // of the one number
    while (numB > 0)
    {
        revB = revB * 10 + (numB % 10);
        numB = numB / 10;
    }

    // Loop to join two numbers
    while (revB > 0)
    {
        numA = numA * 10 + (revB % 10);
        revB = revB / 10;
    }

    return numA;
}

// Function to find the maximum array sum
static int findMaxSum(int A[], int B[], int n)
{
    int maxArr[] = new int[n];

    // Loop to iterate over the two
    // elements of the array
    for(int i = 0; i < n; ++i)
    {
       int X = joinNumbers(A[i], B[i]);
       int Y = joinNumbers(B[i], A[i]);
       int mx = Math.max(X, Y);

       maxArr[i] = mx;
    }

    // Find the array sum
    int maxAns = 0;
    for(int i = 0; i < n; i++)
    {
       maxAns += maxArr[i];
    }

    // Return the array sum
    return maxAns;
}

// Driver Code
public static void main(String args[])
{
    int N = 5;
    int A[] = { 11, 23, 38, 43, 59 };
    int B[] = { 36, 24, 17, 40, 56 };

    System.out.println(findMaxSum(A, B, N));
}
}

// This code is contributed by rutvik_56   
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum array sum by concatenating
# corresponding elements of given two arrays

# Function to join the two numbers
def joinNumbers(numA, numB):
    revB = 0

    # Loop to reverse the digits
    # of the one number
    while (numB > 0):
        revB = revB * 10 + (numB % 10)
        numB = numB // 10

    # Loop to join two numbers
    while (revB > 0):
        numA = numA * 10 + (revB % 10)
        revB = revB // 10

    return numA

# Function to find the maximum array sum
def findMaxSum(A, B, n):
    maxArr = [0 for i in range(n)]

    # Loop to iterate over the two
    # elements of the array
    for i in range(n):

        X = joinNumbers(A[i], B[i])
        Y = joinNumbers(B[i], A[i])
        mx = max(X, Y)
        maxArr[i] = mx

    # Find the array sum
    maxAns = 0

    for i in range(n):
        maxAns += maxArr[i]

    # Return the array sum
    return maxAns

# Driver Code
if __name__ == '__main__':

    N = 5
    A = [ 11, 23, 38, 43, 59 ]
    B = [ 36, 24, 17, 40, 56 ]

    print(findMaxSum(A, B, N))

# This code is contributed by Samarth
```

## C#

```
// C# implementation to find the
// maximum array sum by concatenating
// corresponding elements of given two arrays
using System;
class GFG{

// Function to join the two numbers
static int joinNumbers(int numA, int numB)
{
    int revB = 0;

    // Loop to reverse the digits
    // of the one number
    while (numB > 0)
    {
        revB = revB * 10 + (numB % 10);
        numB = numB / 10;
    }

    // Loop to join two numbers
    while (revB > 0)
    {
        numA = numA * 10 + (revB % 10);
        revB = revB / 10;
    }

    return numA;
}

// Function to find the maximum array sum
static int findMaxSum(int []A, int []B, int n)
{
    int []maxArr = new int[n];

    // Loop to iterate over the two
    // elements of the array
    for(int i = 0; i < n; ++i)
    {
        int X = joinNumbers(A[i], B[i]);
        int Y = joinNumbers(B[i], A[i]);
        int mx = Math.Max(X, Y);

        maxArr[i] = mx;
    }

    // Find the array sum
    int maxAns = 0;
    for(int i = 0; i < n; i++)
    {
        maxAns += maxArr[i];
    }

    // Return the array sum
    return maxAns;
}

// Driver Code
public static void Main(String []args)
{
    int N = 5;
    int []A = { 11, 23, 38, 43, 59 };
    int []B = { 36, 24, 17, 40, 56 };

    Console.WriteLine(findMaxSum(A, B, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// maximum array sum by concatenating
// corresponding elements of given two arrays

// Function to join the two numbers
function joinNumbers(numA, numB)
{
    var revB = 0;

    // Loop to reverse the digits
    // of the one number
    while (numB > 0) {
        revB = revB * 10 + (numB % 10);
        numB = parseInt(numB / 10);
    }

    // Loop to join two numbers
    while (revB > 0) {
        numA = numA * 10 + (revB % 10);
        revB = parseInt( revB / 10);
    }
    return numA;
}

// Function to find the maximum array sum
function findMaxSum(A, B, n)
{
    var maxArr = Array(n).fill(0);

    // Loop to iterate over the two
    // elements of the array
    for (var i = 0; i < n; ++i) {

        var X = joinNumbers(A[i], B[i]);
        var Y = joinNumbers(B[i], A[i]);
        var mx = Math.max(X, Y);
        maxArr[i] = mx;
    }

    // Find the array sum
    var maxAns = 0;
    for (var i = 0; i < n; i++) {
        maxAns += maxArr[i];
    }

    // Return the array sum
    return maxAns;
}

// Driver Code
var N = 5;
var A = [ 11, 23, 38, 43, 59 ];
var B = [ 36, 24, 17, 40, 56 ];
document.write( findMaxSum(A, B, N));

</script>
```

**Output:** 

```
19850
```
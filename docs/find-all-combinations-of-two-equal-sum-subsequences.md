# 找出两个相等和子序列的所有组合

> 原文:[https://www . geeksforgeeks . org/find-两个等和子序列的所有组合/](https://www.geeksforgeeks.org/find-all-combinations-of-two-equal-sum-subsequences/)

给定一个整数数组 **arr[]** ，任务是找到所有可能的方法将数组拆分为两个子序列，使得两个子序列中的元素之和相等。数组中的每个数字必须只属于两个子序列中的一个。打印两个子序列的所有可能组合。

**示例:**

> **输入:** arr[] = {1，2，3，9，4，5}
> **输出:**
> 1 2 9 和 3 4 5
> 1 2 4 5 和 3 9
> 3 9 和 1 2 4 5
> 3 4 5 和 1 2 9
> 
> **输入:** arr[] = {4，-1，2，-1}
> **输出:**
> 4 -1 -1 和 2
> 2 和 4 -1 -1

**方法:**一个简单的解决方案是使用递归形成所有可能的子序列对，并比较两个子序列中元素的总和。对于每个数组元素，我们有两个选择，我们可以选择第一个子序列中的当前元素，也可以选择第二个。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

// Function to print the subsequence elements
void print(int g1[], int a, int g2[], int b)
{

    // Prints elements of the 1st subarray
    for (int i = 0; i < a; i++) {
        cout << g1[i] << " ";
    }
    cout << "and ";

    // Prints elements of the 2nd subarray
    for (int i = 0; i < b; i++) {
        cout << g2[i] << " ";
    }
    cout << endl;
}

// Function that returns true if the sum of the
// elements of arrays g1[] and g2[] is equal
bool checksum(int g1[], int a, int g2[], int b)
{
    int i, x;

    // Adding elements of the 1st array
    for (i = 0, x = 0; i < a; i++) {
        x += g1[i];
    }

    // Subtracting elements of the 2nd array
    for (i = 0; i < b; i++) {
        x -= g2[i];
    }

    // If x is 0 then the sum of elements
    // in both the arrays is equal
    return (x == 0);
}

// Function to find all valid subsequences
void formgroups(int arr[], int x, int g1[], int a,
                int g2[], int b, int n)
{
    // Base Case
    if (x == n) {

        // If sum of the two subsequences
        // is equal then print the elements
        if (checksum(g1, a, g2, b)) {

            // Print the subsequences
            print(g1, a, g2, b);
        }
        return;
    }

    // Recursive Case

    // Choose current element to be a
    // part of the first subsequence
    g1[a] = arr[x];
    formgroups(arr, x + 1, g1, a + 1, g2, b, n);

    // Choose current element to be a
    // part of the second subsequence
    g2[b] = arr[x];
    formgroups(arr, x + 1, g1, a, g2, b + 1, n);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 9, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int g1[MAX], g2[MAX];
    formgroups(arr, 0, g1, 0, g2, 0, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 100000;

// Function to print the
// subsequence elements
static void print(int g1[], int a,
                  int g2[], int b)
{

    // Prints elements of the 1st subarray
    for (int i = 0; i < a; i++)
    {
        System.out.print(g1[i] + " ");
    }
    System.out.print("and ");

    // Prints elements of the 2nd subarray
    for (int i = 0; i < b; i++)
    {
        System.out.print(g2[i] + " ");
    }
    System.out.println();
}

// Function that returns true if
// the sum of the elements of
// arrays g1[] and g2[] is equal
static boolean checksum(int g1[], int a,
                        int g2[], int b)
{
    int i, x;

    // Adding elements of the 1st array
    for (i = 0, x = 0; i < a; i++)
    {
        x += g1[i];
    }

    // Subtracting elements of
    // the 2nd array
    for (i = 0; i < b; i++)
    {
        x -= g2[i];
    }

    // If x is 0 then the sum of elements
    // in both the arrays is equal
    return (x == 0);
}

// Function to find all valid subsequences
static void formgroups(int arr[], int x,
                       int g1[], int a,
                       int g2[], int b, int n)
{
    // Base Case
    if (x == n)
    {

        // If sum of the two subsequences
        // is equal then print the elements
        if (checksum(g1, a, g2, b))
        {

            // Print the subsequences
            print(g1, a, g2, b);
        }
        return;
    }

    // Recursive Case

    // Choose current element to be a
    // part of the first subsequence
    g1[a] = arr[x];
    formgroups(arr, x + 1, g1,
                    a + 1, g2, b, n);

    // Choose current element to be a
    // part of the second subsequence
    g2[b] = arr[x];
    formgroups(arr, x + 1, g1, a,
                g2, b + 1, n);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 9, 4, 5 };
    int n = arr.length;

    int []g1 = new int[MAX];
    int []g2 = new int[MAX];
    formgroups(arr, 0, g1, 0, g2, 0, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 100000

# Function to print the subsequence elements
def prints(g1, a, g2, b):

    # Prints elements of the 1st subarray
    for i in range(a):
        print(g1[i], end = " ")

    print("and ", end = "")

    # Prints elements of the 2nd subarray
    for i in range(b):
        print(g2[i], end = " ")

    print("\n", end = "")

# Function that returns true if the sum of the
# elements of arrays g1[] and g2[] is equal
def checksum(g1, a, g2, b):

    # Adding elements of the 1st array
    x = 0
    for i in range(0, a, 1):
        x += g1[i]

    # Subtracting elements of the 2nd array
    for i in range(b):
        x -= g2[i]

    # If x is 0 then the sum of elements
    # in both the arrays is equal
    return (x == 0)

# Function to find all valid subsequences
def formgroups(arr, x, g1, a, g2, b, n):

    # Base Case
    if (x == n):

        # If sum of the two subsequences
        # is equal then print the elements
        if (checksum(g1, a, g2, b)):

            # Print the subsequences
            prints(g1, a, g2, b)

        return

    # Recursive Case

    # Choose current element to be a
    # part of the first subsequence
    g1[a] = arr[x]
    formgroups(arr, x + 1, g1, a + 1, g2, b, n)

    # Choose current element to be a
    # part of the second subsequence
    g2[b] = arr[x]
    formgroups(arr, x + 1, g1, a, g2, b + 1, n)

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 9, 4, 5]
    n = len(arr)
    g1 = [0 for i in range(MAX)]
    g2 = [0 for i in range(MAX)]
    formgroups(arr, 0, g1, 0, g2, 0, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 100000;

// Function to print the
// subsequence elements
static void print(int []g1, int a,
                  int []g2, int b)
{

    // Prints elements of the 1st subarray
    for (int i = 0; i < a; i++)
    {
        Console.Write(g1[i] + " ");
    }
    Console.Write("and ");

    // Prints elements of the 2nd subarray
    for (int i = 0; i < b; i++)
    {
        Console.Write(g2[i] + " ");
    }
    Console.WriteLine();
}

// Function that returns true if
// the sum of the elements of
// arrays g1[] and g2[] is equal
static bool checksum(int []g1, int a,
                     int []g2, int b)
{
    int i, x;

    // Adding elements of the 1st array
    for (i = 0, x = 0; i < a; i++)
    {
        x += g1[i];
    }

    // Subtracting elements of
    // the 2nd array
    for (i = 0; i < b; i++)
    {
        x -= g2[i];
    }

    // If x is 0 then the sum of elements
    // in both the arrays is equal
    return (x == 0);
}

// Function to find all valid subsequences
static void formgroups(int []arr, int x,
                       int []g1, int a,
                       int []g2, int b, int n)
{
    // Base Case
    if (x == n)
    {

        // If sum of the two subsequences
        // is equal then print the elements
        if (checksum(g1, a, g2, b))
        {

            // Print the subsequences
            print(g1, a, g2, b);
        }
        return;
    }

    // Recursive Case

    // Choose current element to be a
    // part of the first subsequence
    g1[a] = arr[x];
    formgroups(arr, x + 1, g1,
                    a + 1, g2, b, n);

    // Choose current element to be a
    // part of the second subsequence
    g2[b] = arr[x];
    formgroups(arr, x + 1, g1, a,
                g2, b + 1, n);
}

// Driver code
public static void Main()
{
    int []arr = { 1, 2, 3, 9, 4, 5 };
    int n = arr.Length;

    int []g1 = new int[MAX];
    int []g2 = new int[MAX];
    formgroups(arr, 0, g1, 0, g2, 0, n);
}
}

// This code is contributed by anuj_67...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
const MAX = 100000;

// Function to print the subsequence elements
function printi($g1, $a, $g2, $b)
{

    // Prints elements of the 1st subarray
    for ($i = 0; $i < $a; $i++)
    {
        echo ($g1[$i]);
        echo " ";
    }
    echo ("and ");

    // Prints elements of the 2nd subarray
    for ($i = 0; $i < $b; $i++)
    {
        echo ($g2[$i]);
        echo " ";
    }
    echo "\n";
}

// Function that returns true if the sum of the
// elements of arrays g1[] and g2[] is equal
function checksum($g1, $a, $g2, $b)
{

    // Adding elements of the 1st array
    for ($i = 0, $x = 0; $i < $a; $i++)
    {
        $x += $g1[$i];
    }

    // Subtracting elements of the 2nd array
    for ($i = 0; $i < $b; $i++)
    {
        $x -= $g2[$i];
    }

    // If x is 0 then the sum of elements
    // in both the arrays is equal
    return ($x == 0);
}

// Function to find all valid subsequences
function formgroups($arr, $x, $g1, $a,
                          $g2, $b, $n)
{
    // Base Case
    if ($x == $n)
    {

        // If sum of the two subsequences
        // is equal then print the elements
        if (checksum($g1, $a, $g2, $b))
        {

            // Print the subsequences
            printi($g1, $a, $g2, $b);
        }
        return;
    }

    // Recursive Case

    // Choose current element to be a
    // part of the first subsequence
    $g1[$a] = $arr[$x];
    formgroups($arr, $x + 1, $g1,
               $a + 1, $g2, $b, $n);

    // Choose current element to be a
    // part of the second subsequence
    $g2[$b] = $arr[$x];
    formgroups($arr, $x + 1, $g1, $a,
                $g2, $b + 1, $n);
}

// Driver code
$arr = array(1, 2, 3, 9, 4, 5);
$n = count($arr);

$g1 = array();
$g2 = array();

formgroups($arr, 0, $g1, 0, $g2, 0, $n);

// This code is contributed by Naman_Garg.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var MAX = 100000;

// Function to print the subsequence elements
function print(g1, a, g2, b)
{

    // Prints elements of the 1st subarray
    for(var i = 0; i < a; i++)
    {
        document.write( g1[i] + " ");
    }
    document.write("and ");

    // Prints elements of the 2nd subarray
    for(var i = 0; i < b; i++)
    {
        document.write( g2[i] + " ");
    }
    document.write("<br>");
}

// Function that returns true if the sum of the
// elements of arrays g1[] and g2[] is equal
function checksum(g1, a, g2, b)
{
    var i, x;

    // Adding elements of the 1st array
    for(i = 0, x = 0; i < a; i++)
    {
        x += g1[i];
    }

    // Subtracting elements of the 2nd array
    for(i = 0; i < b; i++)
    {
        x -= g2[i];
    }

    // If x is 0 then the sum of elements
    // in both the arrays is equal
    return (x == 0);
}

// Function to find all valid subsequences
function formgroups(arr, x, g1, a, g2, b, n)
{

    // Base Case
    if (x == n)
    {

        // If sum of the two subsequences
        // is equal then print the elements
        if (checksum(g1, a, g2, b))
        {

            // Print the subsequences
            print(g1, a, g2, b);
        }
        return;
    }

    // Recursive Case

    // Choose current element to be a
    // part of the first subsequence
    g1[a] = arr[x];
    formgroups(arr, x + 1, g1, a + 1,
               g2, b, n);

    // Choose current element to be a
    // part of the second subsequence
    g2[b] = arr[x];
    formgroups(arr, x + 1, g1, a, g2,
                    b + 1, n);
}

// Driver code
var arr = [ 1, 2, 3, 9, 4, 5 ];
var n = arr.length;

var g1 = Array(MAX).fill(0),
    g2 = Array(MAX).fill(0);
formgroups(arr, 0, g1, 0, g2, 0, n);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
1 2 9 and 3 4 5 
1 2 4 5 and 3 9 
3 9 and 1 2 4 5 
3 4 5 and 1 2 9
```

**时间复杂度:** O(2 <sup>n</sup> )
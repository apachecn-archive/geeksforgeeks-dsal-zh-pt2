# 最长交替子序列

> 原文:[https://www . geesforgeks . org/最长-交替-子序列/](https://www.geeksforgeeks.org/longest-alternating-subsequence/)

序列{x1，x2，..如果 xn}的元素满足以下关系之一，则 xn }是交替序列:

```
  x1 < x2 > x3 < x4 > x5 < …. xn or 
  x1 > x2 < x3 > x4 < x5 > …. xn
```

**示例:**

```
Input: arr[] = {1, 5, 4}
Output: 3
The whole arrays is of the form  x1 < x2 > x3 

Input: arr[] = {1, 4, 5}
Output: 2
All subsequences of length 2 are either of the form 
x1 < x2; or x1 > x2

Input: arr[] = {10, 22, 9, 33, 49, 50, 31, 60}
Output: 6
The subsequences {10, 22, 9, 33, 31, 60} or
{10, 22, 9, 49, 31, 60} or {10, 22, 9, 50, 31, 60}
are longest subsequence of length 6.
```

这个问题是[最长增子序列问题](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)的扩展，但是在这个问题中寻找最优子结构性质需要更多的思考。
我们将通过动态规划的方法来解决这个问题，让 A 是给定长度为 n 的整数数组。我们定义了一个 2D 数组 las[n][2],使得 las[i][0]包含结束于索引 I 且最后一个元素大于它的前一个元素的最长交替子序列，las[i][1]包含结束于索引 I 且最后一个元素小于它的前一个元素的最长交替子序列，那么它们之间有如下递推关系，

```
las[i][0] = Length of the longest alternating subsequence 
          ending at index i and last element is greater
          than its previous element
las[i][1] = Length of the longest alternating subsequence 
          ending at index i and last element is smaller
          than its previous element

Recursive Formulation:
   las[i][0] = max (las[i][0], las[j][1] + 1); 
             for all j < i and A[j] < A[i] 
   las[i][1] = max (las[i][1], las[j][0] + 1); 
             for all j < i and A[j] > A[i]
```

第一个循环关系是基于这样一个事实，如果我们在位置 I，并且这个元素必须大于它的前一个元素，那么对于这个序列(直到 I)要更大，我们将尝试选择一个元素 j ( < i) such that A[j] < A[i] i.e. A[j] can become A[i]’s previous element and las[j][1] + 1 is bigger than las[i][0] then we will update las[i][0]. 
记住，我们选择了 las[j][1] + 1 而不是 las[j][0] + 1 来满足替代属性，因为在 las[j][0]中，最后一个元素大于它的前一个元素，并且 A[i]大于 A[j]，如果我们更新，这将打破交替属性。所以上述事实导出了第一个递推关系，对于第二个递推关系也可以做类似的论证。

## C++

```
// C++ program to find longest alternating
// subsequence in an array
#include<iostream>
using namespace std;

// Function to return max of two numbers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

// Function to return longest alternating
// subsequence length
int zzis(int arr[], int n)
{

    /*las[i][0] = Length of the longest
        alternating subsequence ending at
        index i and last element is greater
        than its previous element
    las[i][1] = Length of the longest
        alternating subsequence ending
        at index i and last element is
        smaller than its previous element */
    int las[n][2];

    // Initialize all values from 1
    for(int i = 0; i < n; i++)
        las[i][0] = las[i][1] = 1;

    // Initialize result
    int res = 1;

    // Compute values in bottom up manner
    for(int i = 1; i < n; i++)
    {

        // Consider all elements as
        // previous of arr[i]
        for(int j = 0; j < i; j++)
        {

            // If arr[i] is greater, then
            // check with las[j][1]
            if (arr[j] < arr[i] &&
                las[i][0] < las[j][1] + 1)
                las[i][0] = las[j][1] + 1;

            // If arr[i] is smaller, then
            // check with las[j][0]
            if(arr[j] > arr[i] &&
               las[i][1] < las[j][0] + 1)
                las[i][1] = las[j][0] + 1;
        }

        // Pick maximum of both values at index i
        if (res < max(las[i][0], las[i][1]))
            res = max(las[i][0], las[i][1]);
    }
    return res;
}

// Driver code
int main()
{
    int arr[] = { 10, 22, 9, 33,
                  49, 50, 31, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Length of Longest alternating "
         << "subsequence is " << zzis(arr, n);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to find longest alternating subsequence in
// an array
#include <stdio.h>
#include <stdlib.h>

// function to return max of two numbers
int max(int a, int b) {  return (a > b) ? a : b; }

// Function to return longest alternating subsequence length
int zzis(int arr[], int n)
{
    /*las[i][0] = Length of the longest alternating subsequence
          ending at index i and last element is greater
          than its previous element
     las[i][1] = Length of the longest alternating subsequence
          ending at index i and last element is smaller
          than its previous element   */
    int las[n][2];

    /* Initialize all values from 1  */
    for (int i = 0; i < n; i++)
        las[i][0] = las[i][1] = 1;

    int res = 1; // Initialize result

    /* Compute values in bottom up manner */
    for (int i = 1; i < n; i++)
    {
        // Consider all elements as previous of arr[i]
        for (int j = 0; j < i; j++)
        {
            // If arr[i] is greater, then check with las[j][1]
            if (arr[j] < arr[i] && las[i][0] < las[j][1] + 1)
                las[i][0] = las[j][1] + 1;

            // If arr[i] is smaller, then check with las[j][0]
            if( arr[j] > arr[i] && las[i][1] < las[j][0] + 1)
                las[i][1] = las[j][0] + 1;
        }

        /* Pick maximum of both values at index i  */
        if (res < max(las[i][0], las[i][1]))
            res = max(las[i][0], las[i][1]);
    }

    return res;
}

/* Driver program */
int main()
{
    int arr[] = { 10, 22, 9, 33, 49, 50, 31, 60 };
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Length of Longest alternating subsequence is %d\n",
            zzis(arr, n) );
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest
// alternating subsequence in an array
import java.io.*;

class GFG {

// Function to return longest
// alternating subsequence length
static int zzis(int arr[], int n)
{
    /*las[i][0] = Length of the longest
        alternating subsequence ending at
        index i and last element is
        greater than its previous element
    las[i][1] = Length of the longest
        alternating subsequence ending at
        index i and last element is
        smaller than its previous
        element */
    int las[][] = new int[n][2];

    /* Initialize all values from 1 */
    for (int i = 0; i < n; i++)
        las[i][0] = las[i][1] = 1;

    int res = 1; // Initialize result

    /* Compute values in bottom up manner */
    for (int i = 1; i < n; i++)
    {
        // Consider all elements as
        // previous of arr[i]
        for (int j = 0; j < i; j++)
        {
            // If arr[i] is greater, then
            // check with las[j][1]
            if (arr[j] < arr[i] &&
                las[i][0] < las[j][1] + 1)
                las[i][0] = las[j][1] + 1;

            // If arr[i] is smaller, then
            // check with las[j][0]
            if( arr[j] > arr[i] &&
              las[i][1] < las[j][0] + 1)
                las[i][1] = las[j][0] + 1;
        }

        /* Pick maximum of both values at
        index i */
        if (res < Math.max(las[i][0], las[i][1]))
            res = Math.max(las[i][0], las[i][1]);
    }

    return res;
}

/* Driver program */
public static void main(String[] args)
{
    int arr[] = { 10, 22, 9, 33, 49,
                  50, 31, 60 };
    int n = arr.length;
    System.out.println("Length of Longest "+
                    "alternating subsequence is " +
                    zzis(arr, n));
}
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to find longest
# alternating subsequence in an array

# Function to return max of two numbers
def Max(a, b):

    if a > b:
        return a
    else:
        return b

# Function to return longest alternating
# subsequence length
def zzis(arr, n):

    """las[i][0] = Length of the longest
        alternating subsequence ending at
        index i and last element is greater
        than its previous element
    las[i][1] = Length of the longest
        alternating subsequence ending
        at index i and last element is
        smaller than its previous element"""
    las = [[0 for i in range(2)]
              for j in range(n)]

    # Initialize all values from 1
    for i in range(n):
        las[i][0], las[i][1] = 1, 1

    # Initialize result
    res = 1

    # Compute values in bottom up manner
    for i in range(1, n):

        # Consider all elements as
        # previous of arr[i]
        for j in range(0, i):

            # If arr[i] is greater, then
            # check with las[j][1]
            if (arr[j] < arr[i] and
             las[i][0] < las[j][1] + 1):
                las[i][0] = las[j][1] + 1

            # If arr[i] is smaller, then
            # check with las[j][0]
            if(arr[j] > arr[i] and
            las[i][1] < las[j][0] + 1):
                las[i][1] = las[j][0] + 1

        # Pick maximum of both values at index i
        if (res < max(las[i][0], las[i][1])):
            res = max(las[i][0], las[i][1])

    return res

# Driver Code
arr = [ 10, 22, 9, 33, 49, 50, 31, 60 ]
n = len(arr)

print("Length of Longest alternating subsequence is" ,
      zzis(arr, n))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find longest
// alternating subsequence
// in an array
using System;

class GFG
{

// Function to return longest
// alternating subsequence length
static int zzis(int []arr, int n)
{
    /*las[i][0] = Length of the
        longest alternating subsequence
        ending at index i and last 
        element is greater than its
        previous element
    las[i][1] = Length of the longest
        alternating subsequence ending at
        index i and last element is
        smaller than its previous
        element */
    int [,]las = new int[n, 2];

    /* Initialize all values from 1 */
    for (int i = 0; i < n; i++)
        las[i, 0] = las[i, 1] = 1;

    // Initialize result
    int res = 1;

    /* Compute values in
    bottom up manner */
    for (int i = 1; i < n; i++)
    {
        // Consider all elements as
        // previous of arr[i]
        for (int j = 0; j < i; j++)
        {
            // If arr[i] is greater, then
            // check with las[j][1]
            if (arr[j] < arr[i] &&
                las[i, 0] < las[j, 1] + 1)
                las[i, 0] = las[j, 1] + 1;

            // If arr[i] is smaller, then
            // check with las[j][0]
            if( arr[j] > arr[i] &&
            las[i, 1] < las[j, 0] + 1)
                las[i, 1] = las[j, 0] + 1;
        }

        /* Pick maximum of both
        values at index i */
        if (res < Math.Max(las[i, 0],
                           las[i, 1]))
            res = Math.Max(las[i, 0],
                           las[i, 1]);
    }

    return res;
}

// Driver Code
public static void Main()
{
    int []arr = {10, 22, 9, 33,
                 49, 50, 31, 60};
    int n = arr.Length;
    Console.WriteLine("Length of Longest "+
            "alternating subsequence is " +
                             zzis(arr, n));
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find longest
// alternating subsequence in
// an array

// Function to return longest
// alternating subsequence length
function zzis($arr, $n)
{
    /*las[i][0] = Length of the
        longest alternating subsequence
        ending at index i and last element
        is greater than its previous element
    las[i][1] = Length of the longest
        alternating subsequence ending at
        index i and last element is
        smaller than its previous element */
    $las = array(array());

    /* Initialize all values from 1 */
    for ( $i = 0; $i < $n; $i++)
        $las[$i][0] = $las[$i][1] = 1;

    $res = 1; // Initialize result

    /* Compute values in
    bottom up manner */
    for ( $i = 1; $i < $n; $i++)
    {
        // Consider all elements
        // as previous of arr[i]
        for ($j = 0; $j < $i; $j++)
        {
            // If arr[i] is greater, then
            // check with las[j][1]
            if ($arr[$j] < $arr[$i] and
                $las[$i][0] < $las[$j][1] + 1)
               $las[$i][0] = $las[$j][1] + 1;

            // If arr[i] is smaller, then
            // check with las[j][0]
            if($arr[$j] > $arr[$i] and
               $las[$i][1] < $las[$j][0] + 1)
                $las[$i][1] = $las[$j][0] + 1;
        }

        /* Pick maximum of both
        values at index i */
        if ($res < max($las[$i][0], $las[$i][1]))
            $res = max($las[$i][0], $las[$i][1]);
    }

    return $res;
}

// Driver Code
$arr = array(10, 22, 9, 33,
             49, 50, 31, 60 );
$n = count($arr);
echo "Length of Longest alternating " .
    "subsequence is ", zzis($arr, $n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find longest
    // alternating subsequence in an array

    // Function to return longest
    // alternating subsequence length
    function zzis(arr, n)
    {
        /*las[i][0] = Length of the longest
            alternating subsequence ending at
            index i and last element is
            greater than its previous element
        las[i][1] = Length of the longest
            alternating subsequence ending at
            index i and last element is
            smaller than its previous
            element */
        let las = new Array(n);
        for (let i = 0; i < n; i++)
        {
            las[i] = new Array(2);
            for (let j = 0; j < 2; j++)
            {
                las[i][j] = 0;
            }
        }

        /* Initialize all values from 1 */
        for (let i = 0; i < n; i++)
            las[i][0] = las[i][1] = 1;

        let res = 1; // Initialize result

        /* Compute values in bottom up manner */
        for (let i = 1; i < n; i++)
        {
            // Consider all elements as
            // previous of arr[i]
            for (let j = 0; j < i; j++)
            {
                // If arr[i] is greater, then
                // check with las[j][1]
                if (arr[j] < arr[i] &&
                    las[i][0] < las[j][1] + 1)
                    las[i][0] = las[j][1] + 1;

                // If arr[i] is smaller, then
                // check with las[j][0]
                if( arr[j] > arr[i] &&
                  las[i][1] < las[j][0] + 1)
                    las[i][1] = las[j][0] + 1;
            }

            /* Pick maximum of both values at
            index i */
            if (res < Math.max(las[i][0], las[i][1]))
                res = Math.max(las[i][0], las[i][1]);
        }

        return res;
    }

    let arr = [ 10, 22, 9, 33, 49, 50, 31, 60 ];
    let n = arr.length;
    document.write("Length of Longest "+
                    "alternating subsequence is " +
                    zzis(arr, n));

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Length of Longest alternating subsequence is 6
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n)

**有效解:**
在上面的方法中，对于数组中的每个元素，我们随时都在跟踪两个值(结束于索引 I 的最长交替子序列的长度，最后一个元素小于或大于前一个元素)。为了优化空间，我们只需要在任何索引 I 存储元素的两个变量。

inc =当前值大于其先前值的最长备选子序列的长度。
dec =到目前为止最长备选子序列的长度，当前值小于其先前值。
这种方法的棘手之处在于更新这两个值。

当且仅当替代序列中的最后一个元素小于它的前一个元素时，应该增加“inc”。
“dec”应该增加，当且仅当替换序列中的最后一个元素大于它的前一个元素。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function for finding
// longest alternating
// subsequence
int LAS(int arr[], int n)
{

    // "inc" and "dec" initialized as 1
    // as single element is still LAS
    int inc = 1;
    int dec = 1;

    // Iterate from second element
    for (int i = 1; i < n; i++)
    {

        if (arr[i] > arr[i - 1])
        {

            // "inc" changes iff "dec"
            // changes
            inc = dec + 1;
        }

        else if (arr[i] < arr[i - 1])
        {

            // "dec" changes iff "inc"
            // changes
            dec = inc + 1;
        }
    }

    // Return the maximum length
    return max(inc, dec);
}

// Driver Code
int main()
{
    int arr[] = { 10, 22, 9, 33, 49,
                           50, 31, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << LAS(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
public class GFG
{

    // Function for finding
    // longest alternating
    // subsequence
    static int LAS(int[] arr, int n)
    {

        // "inc" and "dec" initialized as 1,
        // as single element is still LAS
        int inc = 1;
        int dec = 1;

        // Iterate from second element
        for (int i = 1; i < n; i++)
        {

            if (arr[i] > arr[i - 1])
            {
                // "inc" changes iff "dec"
                // changes
                inc = dec + 1;
            }
            else if (arr[i] < arr[i - 1])
            {

                // "dec" changes iff "inc"
                // changes
                dec = inc + 1;
            }
        }

        // Return the maximum length
        return Math.max(inc, dec);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 10, 22, 9, 33, 49,
                               50, 31, 60 };
        int n = arr.length;

        // Function Call
        System.out.println(LAS(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach
def LAS(arr, n):

    # "inc" and "dec" initialized as 1
    # as single element is still LAS
    inc = 1
    dec = 1

    # Iterate from second element
    for i in range(1,n):

        if (arr[i] > arr[i-1]):

            # "inc" changes iff "dec"
            # changes
            inc = dec + 1
        elif (arr[i] < arr[i-1]):

            # "dec" changes iff "inc"
            # changes
            dec = inc + 1

    # Return the maximum length
    return max(inc, dec)

# Driver Code
if __name__ == "__main__":
    arr = [10, 22, 9, 33, 49, 50, 31, 60]
    n = len(arr)

    # Function Call
    print(LAS(arr, n))
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function for finding
// longest alternating
// subsequence
static int LAS(int[] arr, int n)
{

    // "inc" and "dec" initialized as 1,
    // as single element is still LAS
    int inc = 1;
    int dec = 1;

    // Iterate from second element
    for(int i = 1; i < n; i++)
    {
        if (arr[i] > arr[i - 1])
        {

            // "inc" changes iff "dec"
            // changes
            inc = dec + 1;
        }
        else if (arr[i] < arr[i - 1])
        {

            // "dec" changes iff "inc"
            // changes
            dec = inc + 1;
        }
    }

    // Return the maximum length
    return Math.Max(inc, dec);
}

// Driver code 
static void Main()
{
    int[] arr = { 10, 22, 9, 33,
                  49, 50, 31, 60 };
    int n = arr.Length;

    // Function Call
    Console.WriteLine(LAS(arr, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript program for above approach

    // Function for finding
    // longest alternating
    // subsequence
    function LAS(arr, n)
    {

        // "inc" and "dec" initialized as 1
        // as single element is still LAS
        let inc = 1;
        let dec = 1;

        // Iterate from second element
        for (let i = 1; i < n; i++)
        {

            if (arr[i] > arr[i - 1])
            {

                // "inc" changes iff "dec"
                // changes
                inc = dec + 1;
            }

            else if (arr[i] < arr[i - 1])
            {

                // "dec" changes iff "inc"
                // changes
                dec = inc + 1;
            }
        }

        // Return the maximum length
        return Math.max(inc, dec);
    }

    let arr = [ 10, 22, 9, 33, 49, 50, 31, 60 ];
    let n = arr.length;

    // Function Call
    document.write(LAS(arr, n));

     // This code is contributed by mukesh07.
</script>
```

**输出:**

```
6
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由乌卡什·特里维迪供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
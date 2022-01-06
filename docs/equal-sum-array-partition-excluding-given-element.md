# 排除给定元素的等和数组划分

> 原文:[https://www . geesforgeks . org/equal-sum-array-partition-exclude-given-element/](https://www.geeksforgeeks.org/equal-sum-array-partition-excluding-given-element/)

给定数组 arr[]和其中的索引。找出数组 arr[]是否可以分成两个不相交的集合，使得这两个集合的和相等，并且没有一个集合包含 arr[index]

**示例:**

```
Input : arr[] = {2, 1, 3, 4}, 
        index = 2
Output : No
We need to exclude arr[2] which is 3.
Possible sets are : 
Set 1: (2, 1), Set 2: 4, sum = 3≠4
Set 1: 2, Set 2: (4, 1), sum = 2≠5
Set 1: 1, Set 2: (4, 2), sum = 1≠6
Neither of the sums are equal.

Input : arr[] = {2, 5, 1, 4, 0}, 
         index = 4
Output : Yes
Set 1 : (2, 4), sum = 6
Set 2 : (5, 1), sum = 6
```

**方法:**这个问题是[分区问题](https://www.geeksforgeeks.org/dynamic-programming-set-18-partition-problem/)的一个变种，带有一个附加的约束，即索引不能包含在数组的任何一个分区集中。
首先求数组中除第 6 个元素外的 S 的和。如果和为偶数，则数组可以被分区，否则不能被分区。如果总和是偶数，那么定义两个变量 set1Sum 和 set2Sum 来存储两个集合的总和。
可以递归判断 set1Sum 是否等于 set2Sum。从位置 0 开始，递归遍历数组。在每个数组位置，有两种选择:要么在集合 1 中包含当前数组元素，要么在集合 2 中包含当前数组元素。递归调用这两个条件，首先在集合 1 中包含当前元素，然后在集合 2 中包含。如果当前位置是要排除的索引，则递归调用下一个位置，而不更新任何总和。当遍历整个数组时，检查两组和是否相等。如果和相等，则结果被发现，否则回溯并检查其他可能性。

**实施:**

## C++

```
// C++ program to determine whether an array can be
// partitioned into two equal sum sets when an index
// is always excluded from both sets.
#include <bits/stdc++.h>
using namespace std;

// Utility function to partition array into two sets
// and check whether sum of both sets are equal or not.
bool isSubsetSumPoss(int arr[], int n, int set1Sum,
                    int set2Sum, int index, int pos)
{

    // If the entire array is traversed, then check
    // whether sum of both the sets are equal or not.
    if (pos == n)
        return (set1Sum == set2Sum);

    // If current position is the index to be excluded
    // then call the function for next position without
    // updating any sum.
    if (pos == index)
        isSubsetSumPoss(arr, n, set1Sum,
                 set2Sum, index, pos + 1);

    // Each element can be included either in
    // set 1 or in set 2\. Call function for
    // both the cases.
    return isSubsetSumPoss(arr, n, set1Sum + arr[pos],
                           set2Sum, index, pos + 1)
           || isSubsetSumPoss(arr, n, set1Sum, set2Sum +
                           arr[pos], index, pos + 1);
}

// Function that calls the main utility
// function and returns whether array can
// be partitioned into two sets or not.
bool canPartition(int arr[], int n, int index)
{

    // Calculate sum of entire array
    // excluding position index.
    int sum = 0;

    for (int i = 0; i < n; i++) {
        if (i == index)
            continue;       
        sum += arr[i];
    }

    // If sum is not even then array
    // cannot be partitioned into two
    // equal sum sets.
    if (sum % 2 != 0)
        return false;   

    // If sum is even call utility function.
    return isSubsetSumPoss(arr, n, 0, 0,
                              index, 0);
}

int main()
{
    int arr[] = { 2, 5, 1, 4, 0 };
    int index = 4;
    int n = sizeof(arr) / sizeof(arr[0]);

    if (canPartition(arr, n, index))
        cout << "Yes";   
    else
        cout << "No";   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine whether an array
// can be partitioned into two equal sum
// sets when an index is always excluded
// from both sets.
import java.io.*;
import java.util.*;

public class GFG {

    // Utility function to partition array
    // into two sets and check whether sum
    // of both sets are equal or not.
    static boolean isSubsetSumPoss(int []arr,
          int n, int set1Sum, int set2Sum,
                       int index, int pos)
    {

        // If the entire array is traversed,
        // then check whether sum of both
        // the sets are equal or not.
        if (pos == n)
            return (set1Sum == set2Sum);

        // If current position is the index
        // to be excluded then call the
        // function for next position without
        // updating any sum.
        if (pos == index)
            isSubsetSumPoss(arr, n, set1Sum,
                    set2Sum, index, pos + 1);

        // Each element can be included
        // either in set 1 or in set 2.
        // Call function for both the cases.
        return isSubsetSumPoss(arr, n, set1Sum
           + arr[pos], set2Sum, index, pos + 1)
            || isSubsetSumPoss(arr, n, set1Sum,
           set2Sum + arr[pos], index, pos + 1);
    }

    // Function that calls the main utility
    // function and returns whether array can
    // be partitioned into two sets or not.
    static boolean canPartition(int []arr, int n,
                                    int index)
    {

        // Calculate sum of entire array
        // excluding position index.
        int sum = 0;

        for (int i = 0; i < n; i++) {
            if (i == index)
                continue;    
            sum += arr[i];
        }

        // If sum is not even then array
        // cannot be partitioned into two
        // equal sum sets.
        if (sum % 2 != 0)
            return false;

        // If sum is even call utility function.
        return isSubsetSumPoss(arr, n, 0, 0,
                                index, 0);
    }

    // Driver code
    public static void main(String args[])
    {
        int []arr = { 2, 5, 1, 4, 0 };
        int index = 4;
        int n = arr.length;

        if (canPartition(arr, n, index))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to determine whether an array can be
# partitioned into two equal sum sets when an index
# is always excluded from both sets.

# Utility function to partition array into two sets
# and check whether sum of both sets are equal or not.
def isSubsetSumPoss(arr, n, set1Sum, set2Sum, index, pos) :

    # If the entire array is traversed, then check
    # whether sum of both the sets are equal or not.
    if (pos == n) :
        return (set1Sum == set2Sum)

    # If current position is the index to be excluded
    # then call the function for next position without
    # updating any sum.
    if (pos == index) :
        isSubsetSumPoss(arr, n, set1Sum, set2Sum,
                                     index, pos + 1)

    # Each element can be included either in
    # set 1 or in set 2\. Call function for
    # both the cases.
    return (isSubsetSumPoss(arr, n, set1Sum + arr[pos],
                               set2Sum, index, pos + 1)
                    or isSubsetSumPoss(arr, n, set1Sum,
                   set2Sum + arr[pos], index, pos + 1))

# Function that calls the main utility
# function and returns whether array can
# be partitioned into two sets or not.
def canPartition(arr, n, index) :

    # Calculate sum of entire array
    # excluding position index.
    sum = 0

    for i in range (0, n) :
        if (i == index) :
            continue   
        sum += arr[i]

    # If sum is not even then array
    # cannot be partitioned into two
    # equal sum sets.
    if (sum % 2 != 0) :
        return false

    # If sum is even call utility function.
    return isSubsetSumPoss(arr, n, 0, 0, index, 0)

# Driver Code
arr = [ 2, 5, 1, 4, 0 ]
index = 4
n = len(arr)

if (canPartition(arr, n, index)) :
    print ("Yes")
else :
    print ("No")

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to determine whether an array
// can be partitioned into two equal sum
// sets when an index is always excluded
// from both sets.
using System;
using System.Collections.Generic;
using System.Linq;
using System.Collections;

class GFG {

    // Utility function to partition array
    // into two sets and check whether sum
    // of both sets are equal or not.
    static bool isSubsetSumPoss(int []arr,
          int n, int set1Sum, int set2Sum,
                       int index, int pos)
    {

        // If the entire array is traversed,
        // then check whether sum of both
        // the sets are equal or not.
        if (pos == n)
            return (set1Sum == set2Sum);

        // If current position is the index
        // to be excluded then call the
        // function for next position without
        // updating any sum.
        if (pos == index)
            isSubsetSumPoss(arr, n, set1Sum,
                    set2Sum, index, pos + 1);

        // Each element can be included
        // either in set 1 or in set 2.
        // Call function for both the cases.
        return isSubsetSumPoss(arr, n, set1Sum
           + arr[pos], set2Sum, index, pos + 1)
            || isSubsetSumPoss(arr, n, set1Sum,
           set2Sum + arr[pos], index, pos + 1);
    }

    // Function that calls the main utility
    // function and returns whether array can
    // be partitioned into two sets or not.
    static bool canPartition(int []arr, int n,
                                    int index)
    {

        // Calculate sum of entire array
        // excluding position index.
        int sum = 0;

        for (int i = 0; i < n; i++) {
            if (i == index)
                continue;    
            sum += arr[i];
        }

        // If sum is not even then array
        // cannot be partitioned into two
        // equal sum sets.
        if (sum % 2 != 0)
            return false;

        // If sum is even call utility function.
        return isSubsetSumPoss(arr, n, 0, 0,
                                index, 0);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 5, 1, 4, 0 };
        int index = 4;
        int n = arr.Length;

        if (canPartition(arr, n, index))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to determine whether
// an array can be partitioned into
// two equal sum sets when an index
// is always excluded from both sets.

// Utility function to partition array
// into two sets and check whether sum
// of both sets are equal or not.
function isSubsetSumPoss($arr, $n, $set1Sum,
                         $set2Sum, $index, $pos)
{

    // If the entire array is traversed,
    // then check whether sum of both
    // the sets are equal or not.
    if ($pos == $n)
        return ($set1Sum == $set2Sum);

    // If current position is the index
    // to be excluded then call the
    // function for next position without
    // updating any sum.
    if ($pos == $index)
        isSubsetSumPoss($arr, $n, $set1Sum,
                        $set2Sum, $index,
                        $pos + 1);

    // Each element can be included
    // either in set 1 or in set 2.
    // Call function for both the cases.
    return isSubsetSumPoss($arr, $n, $set1Sum +
                           $arr[$pos], $set2Sum,
                           $index, $pos + 1) ||
           isSubsetSumPoss($arr, $n, $set1Sum,
                           $set2Sum + $arr[$pos],
                           $index, $pos + 1);
}

// Function that calls the main utility
// function and returns whether array can
// be partitioned into two sets or not.
function canPartition($arr, $n, $index)
{

    // Calculate sum of entire array
    // excluding position index.
    $sum = 0;

    for ($i = 0; $i < $n; $i++)
    {
        if ($i == $index)
            continue;    
        $sum += $arr[$i];
    }

    // If sum is not even then array
    // cannot be partitioned into two
    // equal sum sets.
    if ($sum % 2 != 0)
        return false;

    // If sum is even call
    // utility function.
    return isSubsetSumPoss($arr, $n, 0,
                           0, $index, 0);
}

// Driver Code
$arr = array( 2, 5, 1, 4, 0 );
$index = 4;
$n = count($arr);

if (canPartition($arr, $n, $index))
    echo ("Yes");
else
    echo ("No");

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript program to determine whether an array
// can be partitioned into two equal sum
// sets when an index is always excluded

    // Utility function to partition array
    // into two sets and check whether sum
    // of both sets are equal or not.
    function isSubsetSumPoss(arr,
          n, set1Sum, set2Sum,
                       index, pos)
    {

        // If the entire array is traversed,
        // then check whether sum of both
        // the sets are equal or not.
        if (pos == n)
            return (set1Sum == set2Sum);

        // If current position is the index
        // to be excluded then call the
        // function for next position without
        // updating any sum.
        if (pos == index)
            isSubsetSumPoss(arr, n, set1Sum,
                    set2Sum, index, pos + 1);

        // Each element can be included
        // either in set 1 or in set 2.
        // Call function for both the cases.
        return isSubsetSumPoss(arr, n, set1Sum
           + arr[pos], set2Sum, index, pos + 1)
            || isSubsetSumPoss(arr, n, set1Sum,
           set2Sum + arr[pos], index, pos + 1);
    }

    // Function that calls the main utility
    // function and returns whether array can
    // be partitioned into two sets or not.
    function canPartition(arr, n, index)
    {

        // Calculate sum of entire array
        // excluding position index.
        let sum = 0;

        for (let i = 0; i < n; i++) {
            if (i == index)
                continue;    
            sum += arr[i];
        }

        // If sum is not even then array
        // cannot be partitioned into two
        // equal sum sets.
        if (sum % 2 != 0)
            return false;

        // If sum is even call utility function.
        return isSubsetSumPoss(arr, n, 0, 0,
                                index, 0);
    }
// Driver code

        let arr = [ 2, 5, 1, 4, 0 ];
        let index = 4;
        let n = arr.length;

        if (canPartition(arr, n, index))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**Output :** 

```
Yes
```

**时间复杂度:**指数 O(2^n)
**练习:**尝试迭代解决这个问题。
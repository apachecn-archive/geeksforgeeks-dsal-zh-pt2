# 两个不相等元素之间的最大距离

> 原文:[https://www . geesforgeks . org/两个不等元素之间的最大距离/](https://www.geeksforgeeks.org/maximum-distance-between-two-unequal-elements/)

给定一个数组 **arr[]** ，任务是找出给定数组的两个不等元素之间的最大距离。
**例:**

> **输入:** arr[] = {3，2，1，2，1}
> **输出:** 4
> 最大距离在第一个和最后一个元素之间。
> **输入:** arr[] = {3，3，1，3，3}
> **输出:** 2

**天真法:**遍历整个数组中的每一个单个元素，找出不相等的元素的最长距离。
**高效方法:**利用不相等元素对必须包含第一个或最后一个元素或两者都包含的事实，通过固定第一个元素或固定最后一个元素遍历数组来计算不相等元素之间的最大距离。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum distance
// between two unequal elements
int maxDistance(int arr[], int n)
{
    // If first and last elements are unequal
    // they are maximum distance apart
    if (arr[0] != arr[n - 1])
        return (n - 1);

    int i = n - 1;

    // Fix first element as one of the elements
    // and start traversing from the right
    while (i > 0) {

        // Break for the first unequal element
        if (arr[i] != arr[0])
            break;
        i--;
    }

    // To store the distance from the first element
    int distFirst = (i == 0) ? -1 : i;

    i = 0;

    // Fix last element as one of the elements
    // and start traversing from the left
    while (i < n - 1) {

        // Break for the first unequal element
        if (arr[i] != arr[n - 1])
            break;
        i++;
    }

    // To store the distance from the last element
    int distLast = (i == n - 1) ? -1 : (n - 1 - i);

    // Maximum possible distance
    int maxDist = max(distFirst, distLast);
    return maxDist;
}

// Driver code
int main()
{
    int arr[] = { 4, 4, 1, 2, 1, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxDistance(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the maximum distance
// between two unequal elements
static int maxDistance(int arr[], int n)
{
    // If first and last elements are unequal
    // they are maximum distance apart
    if (arr[0] != arr[n - 1])
        return (n - 1);

    int i = n - 1;

    // Fix first element as one of the elements
    // and start traversing from the right
    while (i > 0)
    {

        // Break for the first unequal element
        if (arr[i] != arr[0])
            break;
        i--;
    }

    // To store the distance from the first element
    int distFirst = (i == 0) ? -1 : i;

    i = 0;

    // Fix last element as one of the elements
    // and start traversing from the left
    while (i < n - 1)
    {

        // Break for the first unequal element
        if (arr[i] != arr[n - 1])
            break;
        i++;
    }

    // To store the distance from the last element
    int distLast = (i == n - 1) ? -1 : (n - 1 - i);

    // Maximum possible distance
    int maxDist = Math.max(distFirst, distLast);
    return maxDist;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 4, 4, 1, 2, 1, 4 };
    int n = arr.length;
    System.out.print(maxDistance(arr, n));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the maximum distance
# between two unequal elements
def maxDistance(arr, n):

    # If first and last elements are unequal
    # they are maximum distance apart
    if (arr[0] != arr[n - 1]):
        return (n - 1);

    i = n - 1;

    # Fix first element as one of the elements
    # and start traversing from the right
    while (i > 0):

        # Break for the first unequal element
        if (arr[i] != arr[0]):
            break;
        i-=1;

    # To store the distance from the first element
    distFirst = -1 if(i == 0) else i;

    i = 0;

    # Fix last element as one of the elements
    # and start traversing from the left
    while (i < n - 1):

        # Break for the first unequal element
        if (arr[i] != arr[n - 1]):
            break;
        i+=1;

    # To store the distance from the last element
    distLast = -1 if(i == n - 1) else (n - 1 - i);

    # Maximum possible distance
    maxDist = max(distFirst, distLast);
    return maxDist;

# Driver code
arr = [4, 4, 1, 2, 1, 4];
n = len(arr);
print(maxDistance(arr, n));

# This code has been contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum distance
// between two unequal elements
static int maxDistance(int []arr, int n)
{
    // If first and last elements are unequal
    // they are maximum distance apart
    if (arr[0] != arr[n - 1])
        return (n - 1);

    int i = n - 1;

    // Fix first element as one of the elements
    // and start traversing from the right
    while (i > 0)
    {

        // Break for the first unequal element
        if (arr[i] != arr[0])
            break;
        i--;
    }

    // To store the distance from the first element
    int distFirst = (i == 0) ? -1 : i;

    i = 0;

    // Fix last element as one of the elements
    // and start traversing from the left
    while (i < n - 1)
    {

        // Break for the first unequal element
        if (arr[i] != arr[n - 1])
            break;
        i++;
    }

    // To store the distance from the last element
    int distLast = (i == n - 1) ? -1 : (n - 1 - i);

    // Maximum possible distance
    int maxDist = Math.Max(distFirst, distLast);
    return maxDist;
}

// Driver code
static public void Main ()
{
    int []arr = { 4, 4, 1, 2, 1, 4 };
    int n = arr.Length;
    Console.WriteLine(maxDistance(arr, n));
}
}

// This code is contributed by Tushil..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum distance
// between two unequal elements
function maxDistance(arr, n)
{
    // If first and last elements are unequal
    // they are maximum distance apart
    if (arr[0] != arr[n - 1])
        return (n - 1);

    var i = n - 1;

    // Fix first element as one of the elements
    // and start traversing from the right
    while (i > 0) {

        // Break for the first unequal element
        if (arr[i] != arr[0])
            break;
        i--;
    }

    // To store the distance from the first element
    var distFirst = (i == 0) ? -1 : i;

    i = 0;

    // Fix last element as one of the elements
    // and start traversing from the left
    while (i < n - 1) {

        // Break for the first unequal element
        if (arr[i] != arr[n - 1])
            break;
        i++;
    }

    // To store the distance from the last element
    var distLast = (i == n - 1) ? -1 : (n - 1 - i);

    // Maximum possible distance
    var maxDist = Math.max(distFirst, distLast);
    return maxDist;
}

// Driver code
var arr = [ 4, 4, 1, 2, 1, 4 ];
var n = arr.length;
document.write( maxDistance(arr, n));

</script>
```

**Output:** 

```
4
```
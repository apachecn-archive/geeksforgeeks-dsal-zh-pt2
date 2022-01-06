# 对数组中的对进行计数，使它们之间的绝对差值≥ K

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-array-so-它们之间的绝对差值为-k/](https://www.geeksforgeeks.org/count-pairs-in-an-array-such-that-the-absolute-difference-between-them-is-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是从数组中找到对的计数 **(arr[i]，arr[j])** ，使得**| arr[I]–arr[j]|≥K**。**注**注意 **(arr[i]，arr[j])** 和 **arr[j]，arr[i]** 只统计一次。
**举例:**

> **输入:** arr[] = {1，2，3，4}，K = 2
> **输出:** 3
> 所有有效对为(1，3)、(1，4)和(2，4)
> **输入:** arr[] = {7，4，12，56，123}，K = 50
> **输出:** 5

**方法:** [排序](https://www.geeksforgeeks.org/sort-c-stl/)给定的数组。现在对于每个元素 **arr[i]** ，找到右边的第一个元素 **arr[j]** ，使得**(arr[j]–arr[I])≥K**。这是因为在这个元素之后，随着数组的排序，每个元素都将满足与 **arr[i]** 相同的条件，与 **arr[i]** 构成有效对的元素计数将是**(N–j)**，其中 **N** 是给定数组的大小。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of required pairs
int count(int arr[], int n, int k)
{

    // Sort the given array
    sort(arr, arr + n);

    // To store the required count
    int cnt = 0;
    int i = 0, j = 1;

    while (i < n && j < n) {

        // Update j such that it is always > i
        j = (j <= i) ? (i + 1) : j;

        // Find the first element arr[j] such that
        // (arr[j] - arr[i]) >= K
        // This is because after this element, all
        // the elements will have absolute difference
        // with arr[i] >= k and the count of
        // valid pairs will be (n - j)
        while (j < n && (arr[j] - arr[i]) < k)
            j++;

        // Update the count of valid pairs
        cnt += (n - j);

        // Get to the next element to repeat the steps
        i++;
    }

    // Return the count
    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << count(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{

// Function to return the count of required pairs
static int count(int arr[], int n, int k)
{

    // Sort the given array
    Arrays.sort(arr);

    // To store the required count
    int cnt = 0;
    int i = 0, j = 1;

    while (i < n && j < n) {

        // Update j such that it is always > i
        j = (j <= i) ? (i + 1) : j;

        // Find the first element arr[j] such that
        // (arr[j] - arr[i]) >= K
        // This is because after this element, all
        // the elements will have absolute difference
        // with arr[i] >= k and the count of
        // valid pairs will be (n - j)
        while (j < n && (arr[j] - arr[i]) < k)
            j++;

        // Update the count of valid pairs
        cnt += (n - j);

        // Get to the next element to repeat the steps
        i++;
    }

    // Return the count
    return cnt;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 4 };
    int n = arr.length;
    int k = 2;

    System.out.println(count(arr, n, k));

}
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of required pairs
def count(arr, n, k) :

    # Sort the given array
    arr.sort();

    # To store the required count
    cnt = 0;
    i = 0; j = 1;

    while (i < n and j < n) :

        # Update j such that it is always > i
        if j <= i :
            j = i + 1
        else :
            j = j

        # Find the first element arr[j] such that
        # (arr[j] - arr[i]) >= K
        # This is because after this element, all
        # the elements will have absolute difference
        # with arr[i] >= k and the count of
        # valid pairs will be (n - j)
        while (j < n and (arr[j] - arr[i]) < k) :
            j += 1;

        # Update the count of valid pairs
        cnt += (n - j);

        # Get to the next element to repeat the steps
        i += 1;

    # Return the count
    return cnt;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4 ];
    n = len(arr);
    k = 2;

    print(count(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of required pairs
static int count(int []arr, int n, int k)
{

    // Sort the given array
    Array.Sort(arr);

    // To store the required count
    int cnt = 0;
    int i = 0, j = 1;

    while (i < n && j < n)
    {

        // Update j such that it is always > i
        j = (j <= i) ? (i + 1) : j;

        // Find the first element arr[j] such that
        // (arr[j] - arr[i]) >= K
        // This is because after this element, all
        // the elements will have absolute difference
        // with arr[i] >= k and the count of
        // valid pairs will be (n - j)
        while (j < n && (arr[j] - arr[i]) < k)
            j++;

        // Update the count of valid pairs
        cnt += (n - j);

        // Get to the next element to repeat the steps
        i++;
    }

    // Return the count
    return cnt;
}

// Driver code
static public void Main ()
{

    int []arr = { 1, 2, 3, 4 };
    int n = arr.Length;
    int k = 2;

    Console.Write(count(arr, n, k));

}
}

// This code is contributed by jit_t.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of required pairs
function count(arr, n, k) {

    // Sort the given array
    arr.sort();

    // To store the required count
    var cnt = 0;
    var i = 0;
    var j = 1;

    while (i < n && j < n) {

        // Update j such that it is always > i
        if (j <= i)
            j = i + 1
        else
            j = j

        // Find the first element arr[j] such that
        // (arr[j] - arr[i]) >= K
        // This is because after this element, all
        // the elements will have absolute difference
        // with arr[i] >= k and the count of
        // valid pairs will be (n - j)
        while (j < n && (arr[j] - arr[i]) < k)
            j += 1;

        // Update the count of valid pairs
        cnt += (n - j);

        // Get to the next element to repeat the steps
        i += 1;
    }

    // Return the count
    return cnt;

}

// Driver code 
var arr = [ 1, 2, 3, 4 ];
var n = arr.length;
var k = 2;

document.write(count(arr, n, k));

// This code is contributed by AnkThon

</script>
```

**Output:** 

```
3
```
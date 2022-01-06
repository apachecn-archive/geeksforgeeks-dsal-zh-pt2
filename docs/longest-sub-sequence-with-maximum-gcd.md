# GCD 最大的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列带最大值-gcd/](https://www.geeksforgeeks.org/longest-sub-sequence-with-maximum-gcd/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找到最大可能 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的最长子序列的长度。
**举例:**

> **输入:** arr[] = {2，1，2}
> **输出:** 2
> {2}、{2}和{2，2}是具有最大可能 GCD 的子序列
> 。
> **输入:** arr[] = {1，2，3}
> **输出:** 1
> {3}是需要的子序列。

**方法:**数组中最大可能的 GCD 将等于数组中最大元素的值。现在，为了最大化结果子序列的长度，找到数组中值等于这个最大值的元素的数量，这些元素的计数就是需要的答案。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length
// of the largest subsequence with
// maximum possible GCD
int maxLen(int* arr, int n)
{
    // Maximum value from the array
    int max_val = *max_element(arr, arr + n);

    // To store the frequency of the
    // maximum element in the array
    int freq = 0;

    for (int i = 0; i < n; i++) {

        // If current element is equal
        // to the maximum element
        if (arr[i] == max_val)
            freq++;
    }

    return freq;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 2, 3, 3, 3 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxLen(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function to return the length
// of the largest subsequence with
// maximum possible GCD
static int maxLen(int[] arr, int n)
{
    // Maximum value from the array
    int max_val = Arrays.stream(arr).max().getAsInt();

    // To store the frequency of the
    // maximum element in the array
    int freq = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is equal
        // to the maximum element
        if (arr[i] == max_val)
            freq++;
    }
    return freq;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 3, 2, 2, 3, 3, 3 };
    int n = arr.length;

    System.out.println(maxLen(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length
# of the largest subsequence with
# maximum possible GCD
def maxLen(arr, n) :

    # Maximum value from the array
    max_val = max(arr);

    # To store the frequency of the
    # maximum element in the array
    freq = 0;

    for i in range(n) :

        # If current element is equal
        # to the maximum element
        if (arr[i] == max_val) :
            freq += 1;

    return freq;

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 2, 2, 3, 3, 3 ];
    n = len(arr);

    print(maxLen(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

// Function to return the length
// of the largest subsequence with
// maximum possible GCD
static int maxLen(int[] arr, int n)
{
    // Maximum value from the array
    int max_val = arr.Max();

    // To store the frequency of the
    // maximum element in the array
    int freq = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is equal
        // to the maximum element
        if (arr[i] == max_val)
            freq++;
    }
    return freq;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 3, 2, 2, 3, 3, 3 };
    int n = arr.Length;

    Console.WriteLine(maxLen(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length
// of the largest subsequence with
// maximum possible GCD
function maxLen(arr, n)
{
    // Maximum value from the array
    var max_val = arr.reduce((a,b) => Math.max(a,b));

    // To store the frequency of the
    // maximum element in the array
    var freq = 0;

    for (var i = 0; i < n; i++) {

        // If current element is equal
        // to the maximum element
        if (arr[i] == max_val)
            freq++;
    }

    return freq;
}

// Driver code
var arr = [3, 2, 2, 3, 3, 3];
var n = arr.length;
document.write( maxLen(arr, n));

</script>
```

**Output:** 

```
4
```
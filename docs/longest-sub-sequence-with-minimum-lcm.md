# 最小 LCM 的最长子序列

> 原文:[https://www . geeksforgeeks . org/最长-最小子序列-lcm/](https://www.geeksforgeeks.org/longest-sub-sequence-with-minimum-lcm/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是以最小可能 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 找到最长子序列的长度。
**举例:**

> **输入:** arr[] = {1，3，1}
> **输出:** 2
> {1}和{1}是具有最小可能 LCM 的子序列
> 。
> **输入:** arr[] = {3，4，5，3，2，3}
> **输出:** 1
> {2}为所需子序列。

**方法:**来自数组的最小可能 LCM 将等于数组中最小元素的值。现在，为了最大化结果子序列的长度，找到数组中值等于这个最小值的元素的数量，这些元素的计数就是需要的答案。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length
// of the largest subsequence with
// minimum possible LCM
int maxLen(int* arr, int n)
{
    // Minimum value from the array
    int min_val = *min_element(arr, arr + n);

    // To store the frequency of the
    // minimum element in the array
    int freq = 0;

    for (int i = 0; i < n; i++) {

        // If current element is equal
        // to the minimum element
        if (arr[i] == min_val)
            freq++;
    }

    return freq;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 1 };
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
// minimum possible LCM
static int maxLen(int[] arr, int n)
{
    // Minimum value from the array
    int min_val = Arrays.stream(arr).min().getAsInt();

    // To store the frequency of the
    // minimum element in the array
    int freq = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is equal
        // to the minimum element
        if (arr[i] == min_val)
            freq++;
    }

    return freq;
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 3, 1 };
    int n = arr.length;

    System.out.println(maxLen(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length
# of the largest subsequence with
# minimum possible LCM
def maxLen(arr, n) :

    # Minimum value from the array
    min_val = min(arr);

    # To store the frequency of the
    # minimum element in the array
    freq = 0;

    for i in range(n) :

        # If current element is equal
        # to the minimum element
        if (arr[i] == min_val) :
            freq += 1;

    return freq;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 3, 1 ];

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
// minimum possible LCM
static int maxLen(int[] arr, int n)
{
    // Minimum value from the array
    int min_val = arr.Min();

    // To store the frequency of the
    // minimum element in the array
    int freq = 0;

    for (int i = 0; i < n; i++)
    {

        // If current element is equal
        // to the minimum element
        if (arr[i] == min_val)
            freq++;
    }

    return freq;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 3, 1 };
    int n = arr.Length;

    Console.WriteLine(maxLen(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length
// of the largest subsequence with
// minimum possible LCM
function maxLen(arr, n)
{
    // Minimum value from the array
    var min_val = arr.reduce((a, b) => Math.min(a,b))

    // To store the frequency of the
    // minimum element in the array
    var freq = 0;

    for (var i = 0; i < n; i++) {

        // If current element is equal
        // to the minimum element
        if (arr[i] == min_val)
            freq++;
    }

    return freq;
}

// Driver code
var arr = [ 1, 3, 1 ];
var n = arr.length;
document.write( maxLen(arr, n));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
2
```
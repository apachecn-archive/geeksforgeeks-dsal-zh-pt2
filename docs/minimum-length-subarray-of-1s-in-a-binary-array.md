# 二进制数组中 1 的最小长度子数组

> 原文:[https://www . geesforgeks . org/二进制数组中最小长度为 1s 的子数组/](https://www.geeksforgeeks.org/minimum-length-subarray-of-1s-in-a-binary-array/)

给定二进制数组。任务是找出 1 个数最少的子阵长度。
**注**:保证数组中至少有一个 1。
T4【示例】T5:

> **输入** : arr[] = {1，1，0，0，1，1，1，0，1，1，1}
> **输出**:3
> 1 的最小长度子阵为{1，1}。
> **输入** : arr[] = {0，0，1，0，1，0，1，0，1}
> **输出** : 1

**简单的解决方案**:简单的解决方案就是考虑每个子阵列，在每个子阵列中计数 1。最后返回 1 的最小长度子数组的返回大小。
**高效解**:高效解是从左向右遍历数组。如果我们看到 1，我们就增加计数。如果我们看到一个 0，到目前为止 1 的计数是正的，计算计数和结果的最小值，并将计数重置为零。
以下是上述方法的实施:

## C++

```
// C++ program to count minimum length
// subarray of 1's in a binary array.
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum length subarray
// of 1's in binary array arr[0..n-1]
int getMinLength(bool arr[], int n)
{
    int count = 0; // initialize count
    int result = INT_MAX; // initialize result

    for (int i = 0; i < n; i++) {
        if (arr[i] == 1) {
            count++;
        }
        else {
            if (count != 0)
                result = min(result, count);
            count = 0;
        }
    }

    return result;
}

// Driver code
int main()
{
    bool arr[] = { 1, 1, 0, 0, 1, 1, 1, 0,
                   1, 1, 1, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getMinLength(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum length
// subarray of 1's in a binary array.
import java.io.*;

class GFG
{

// Function to count minimum length subarray
// of 1's in binary array arr[0..n-1]
static int getMinLength(double arr[], int n)
{
    int count = 0; // initialize count
    int result = Integer.MAX_VALUE; // initialize result

    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 1)
        {
            count++;
        }
        else
        {
            if (count != 0)
                result = Math.min(result, count);
            count = 0;
        }
    }

    return result;
}

// Driver code
public static void main (String[] args)
{
    double arr[] = { 1, 1, 0, 0, 1, 1, 1, 0,
                1, 1, 1, 1 };
    int n = arr.length;
    System.out.println (getMinLength(arr, n));

}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python program to count minimum length
# subarray of 1's in a binary array.
import sys

# Function to count minimum length subarray
# of 1's in binary array arr[0..n-1]
def getMinLength(arr, n):
    count = 0; # initialize count
    result = sys.maxsize ; # initialize result

    for i in range(n):
        if (arr[i] == 1):
            count+=1;
        else:
            if(count != 0):
                result = min(result, count);
            count = 0;

    return result;

# Driver code
arr = [ 1, 1, 0, 0, 1, 1, 1, 0,
                1, 1, 1, 1 ];

n = len(arr);

print(getMinLength(arr, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to count minimum length
// subarray of 1's in a binary array.
using System;

class GFG
{

// Function to count minimum length subarray
// of 1's in binary array arr[0..n-1]
static int getMinLength(double []arr, int n)
{
    int count = 0; // initialize count
    int result = int.MaxValue; // initialize result

    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 1)
        {
            count++;
        }
        else
        {
            if (count != 0)
                result = Math.Min(result, count);
            count = 0;
        }
    }

    return result;
}

// Driver code
static public void Main ()
{
    double []arr = { 1, 1, 0, 0, 1, 1,
                     1, 0, 1, 1, 1, 1 };
    int n = arr.Length;
    Console.WriteLine(getMinLength(arr, n));
}
}

// This code is contributed by Tushil..
```

## java 描述语言

```
<script>

// javascript program to count minimum length
// subarray of 1's in a binary array.

// Function to count minimum length subarray
// of 1's in binary array arr[0..n-1]
function getMinLength(arr, n)
{
// initialize count
    var count = 0;
// initialize result
    var result = Number.MAX_VALUE;

    for (i = 0; i < n; i++)
    {
        if (arr[i] == 1)
        {
            count++;
        }
        else
        {
            if (count != 0)
                result = Math.min(result, count);
            count = 0;
        }
    }

    return result;
}

// Driver code
var arr = [ 1, 1, 0, 0, 1, 1, 1, 0,
           1, 1, 1, 1 ];
var n = arr.length;
document.write(getMinLength(arr, n));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
2
```

**时间复杂度** : O(N)
**辅助空间** : O(1)
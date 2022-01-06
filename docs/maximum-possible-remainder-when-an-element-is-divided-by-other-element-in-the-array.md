# 当一个元素被数组中的其他元素除时的最大可能余数

> 原文:[https://www . geesforgeks . org/当一个元素被数组中的其他元素除时的最大可能余数/](https://www.geeksforgeeks.org/maximum-possible-remainder-when-an-element-is-divided-by-other-element-in-the-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是从数组中找出任意一对 **(arr[i]，arr[j])** 的最大模值。
**举例:**

> **输入:** arr[] = {2，4，1，5，3，6}
> **输出:** 5
> (5 % 6) = 5 是最大可能 mod 值。
> **输入:** arr[] = {6，6，6，6}
> **输出:** 0

**逼近:**众所周知，当一个整数被另一个整数 **X** 除时，余数总是小于 **X** 。因此，当除数是数组中的最大元素时，可以从数组中获得的最大模值将是，当剩余元素中的被除数是最大值时，即数组中的第二个最大元素时，该值将是最大的，这是必需的答案。**注意**当数组所有元素相等时，结果将是 **0** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum mod
// value for any pair from the array
int maxMod(int arr[], int n)
{
    int maxVal = *max_element(arr, arr + n);
    int secondMax = 0;

    // Find the second maximum
    // element from the array
    for (int i = 0; i < n; i++) {
        if (arr[i] < maxVal
            && arr[i] > secondMax) {
            secondMax = arr[i];
        }
    }

    return secondMax;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 1, 5, 3, 6 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxMod(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static int max_element(int arr[], int n)
    {
        int max = arr[0];
        for(int i = 1; i < n ; i++)
        {
            if (max < arr[i])
                max = arr[i];
        }
        return max;
    }

    // Function to return the maximum mod
    // value for any pair from the array
    static int maxMod(int arr[], int n)
    {
        int maxVal = max_element(arr, n);
        int secondMax = 0;

        // Find the second maximum
        // element from the array
        for (int i = 0; i < n; i++)
        {
            if (arr[i] < maxVal &&
                arr[i] > secondMax)
            {
                secondMax = arr[i];
            }
        }
        return secondMax;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 4, 1, 5, 3, 6 };
        int n = arr.length;

        System.out.println(maxMod(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum mod
# value for any pair from the array
def maxMod(arr, n):

    maxVal = max(arr)
    secondMax = 0

    # Find the second maximum
    # element from the array
    for i in range(0, n):
        if (arr[i] < maxVal and
            arr[i] > secondMax):
            secondMax = arr[i]

    return secondMax

# Driver code
arr = [2, 4, 1, 5, 3, 6]
n = len(arr)
print(maxMod(arr, n))

# This code is contributed
# by Sanjit Prasad
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static int max_element(int []arr, int n)
    {
        int max = arr[0];
        for(int i = 1; i < n ; i++)
        {
            if (max < arr[i])
                max = arr[i];
        }
        return max;
    }

    // Function to return the maximum mod
    // value for any pair from the array
    static int maxMod(int []arr, int n)
    {
        int maxVal = max_element(arr, n);
        int secondMax = 0;

        // Find the second maximum
        // element from the array
        for (int i = 0; i < n; i++)
        {
            if (arr[i] < maxVal &&
                arr[i] > secondMax)
            {
                secondMax = arr[i];
            }
        }
        return secondMax;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 2, 4, 1, 5, 3, 6 };
        int n = arr.Length;

        Console.WriteLine(maxMod(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum mod
// value for any pair from the array
function maxMod(arr, n) {
    let maxVal = arr.sort((a, b) => b - a)[0]
    let secondMax = 0;

    // Find the second maximum
    // element from the array
    for (let i = 0; i < n; i++) {
        if (arr[i] < maxVal
            && arr[i] > secondMax) {
            secondMax = arr[i];
        }
    }

    return secondMax;
}

// Driver code

let arr = [2, 4, 1, 5, 3, 6];
let n = arr.length;

document.write(maxMod(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度** : O(N)。
**辅助空间** : O(1)。
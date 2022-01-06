# 一次将任意两个元素减一，使所有元素为零

> 原文:[https://www . geesforgeks . org/make-all-elements-零减任意两个元素一次减一个/](https://www.geeksforgeeks.org/make-all-elements-zero-by-decreasing-any-two-elements-by-one-at-a-time/)

给定一个数组 **arr[]** ，任务是检查是否有可能通过给定的操作使数组的所有元素都为零。在单次操作中，任意两个元素 **arr[i]** 和 **arr[j]** 可以同时递减 1。
**举例:**

> **输入:** arr[] = {1，2，1，2，2}
> **输出:**是
> 递减 1 <sup>st</sup> 和 2 <sup>nd</sup> 元素，arr[] = {0，1，1，2，2}
> 递减 2 <sup>nd</sup> 和 3 <sup>rd</sup> 元素，arr[] = {0，0，2，2}
> 递减 4【T15 1}
> 递减第 4 <sup>个</sup>和第 5 <sup>个</sup>元素，arr[] = {0，0，0，0，0}
> **输入:** arr[] = {1，2，3，4，5}
> **输出:**否

**方法:**给定的数组只有在满足以下条件时才能置零:

1.  数组元素的总和必须是偶数。
2.  最大元素必须小于或等于 **⌊sum / 2⌋** ，其中**之和**是其他元素的和。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if all
// the array elements can be made
// 0 with the given operation
bool checkZeroArray(int* arr, int n)
{

    // Find the maximum element
    // and the sum
    int sum = 0, maximum = INT_MIN;
    for (int i = 0; i < n; i++) {
        sum = sum + arr[i];
        maximum = max(maximum, arr[i]);
    }

    // Check the required condition
    if (sum % 2 == 0 && maximum <= sum / 2)
        return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 2, 2 };
    int n = sizeof(arr) / sizeof(int);

    if (checkZeroArray(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
public class GFG
{

    // Function that returns true if all
    // the array elements can be made
    // 0 with the given operation
    static boolean checkZeroArray(int []arr, int n)
    {

        // Find the maximum element
        // and the sum
        int sum = 0, maximum = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++)
        {
            sum = sum + arr[i];
            maximum = Math.max(maximum, arr[i]);
        }

        // Check the required condition
        if (sum % 2 == 0 && maximum <= sum / 2)
            return true;

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 1, 2, 2 };
        int n = arr.length;

        if (checkZeroArray(arr, n) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function that returns true if all
# the array elements can be made
# 0 with the given operation
def checkZeroArray(arr,n):

    # Find the maximum element
    # and the sum
    sum = 0
    maximum = -10**9
    for i in range(n):
        sum = sum + arr[i]
        maximum = max(maximum, arr[i])

    # Check the required condition
    if (sum % 2 == 0 and maximum <= sum // 2):
        return True

    return False

# Driver code

arr = [1, 2, 1, 2, 2]
n = len(arr)

if (checkZeroArray(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function that returns true if all
    // the array elements can be made
    // 0 with the given operation
    static bool checkZeroArray(int []arr, int n)
    {

        // Find the maximum element
        // and the sum
        int sum = 0, maximum = int.MinValue;

        for (int i = 0; i < n; i++)
        {
            sum = sum + arr[i];
            maximum = Math.Max(maximum, arr[i]);
        }

        // Check the required condition
        if (sum % 2 == 0 && maximum <= sum / 2)
            return true;

        return false;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 2, 1, 2, 2 };
        int n = arr.Length;

        if (checkZeroArray(arr, n) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

    // Function that returns true if all
    // the array elements can be made
    // 0 with the given operation
    function checkZeroArray(arr,n)
    {
        // Find the maximum element
        // and the sum
        let sum = 0, maximum = Number.MIN_VALUE;

        for (let i = 0; i < n; i++)
        {
            sum = sum + arr[i];
            maximum = Math.max(maximum, arr[i]);
        }

        // Check the required condition
        if (sum % 2 == 0 && maximum <= sum / 2)
            return true;

        return false;
    }

    // Driver code
    let arr=[1, 2, 1, 2, 2 ];
    let n = arr.length;
    if (checkZeroArray(arr, n) == true)
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```
# 奇数乘积的最长子阵列

> 原文:[https://www . geeksforgeeks . org/long-subarray-with-奇数-product/](https://www.geeksforgeeks.org/longest-subarray-with-odd-product/)

给定一个由 **N** 元素组成的数组**arr【】**，任务是用**奇数**乘积找到最长子阵的长度。
**示例:**

> **输入:** arr[] = {3，5，2，1}
> **输出:** 2
> **说明:**
> 连续奇数元素的子阵为{3，5}，{1}。
> 既然，{3，5}越长，答案就是 2。
> **输入:** arr[] = {8，5，3，1，0}
> **输出:** 3
> **解释:**
> 奇数积的最长子阵为{5，3，1}。

**进场:**
解决问题需要以下观察:

> 两个奇数的乘积产生一个奇数。
> 一个奇数和一个偶数的乘积生成一个偶数。
> 两个偶数的乘积生成一个偶数。

从上面的观察，我们可以得出结论，阵列中连续奇数元素的最长子阵列是必需的答案。
按照以下步骤解决问题:

*   遍历数组并检查当前元素是偶数还是奇数。
*   如果当前元素是奇数，将**计数**设置为 **1** ，并继续增加计数，直到在数组中遇到偶数元素。
*   一旦遇到偶数元素，将计数与 **ans** 进行比较，并更新 **ans** ，存储两者的最大值。
*   对其余阵列重复上述步骤。
*   最后，打印存储在**和**中的值。

以下是上述方法的实现:

## C++

```
// C++ Program to find the longest
// subarray with odd product
#include <bits/stdc++.h>
using namespace std;

// Function to return length of
// longest subarray with odd product
int Maxlen(int arr[], int n)
{
    int ans = 0;
    int count = 0;
    for (int i = 0; i < n; i++) {

        // If even element
        // is encountered
        if (arr[i] % 2 == 0)
            count = 0;
        else
            count++;

        // Update maximum
        ans = max(ans, count);
    }
    return ans;
}

// Driver Code
int main()
{

    // int arr[] = { 6, 3, 5, 1 };
    int arr[] = { 1, 7, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << Maxlen(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest
// subarray with odd product
import java.util.*;

class GFG{

// Function to return length of
// longest subarray with odd product
static int Maxlen(int arr[], int n)
{
    int ans = 0;
    int count = 0;
    for(int i = 0; i < n; i++)
    {

        // If even element
        // is encountered
        if (arr[i] % 2 == 0)
            count = 0;
        else
            count++;

        // Update maximum
        ans = Math.max(ans, count);
    }
    return ans;
}

// Driver Code
public static void main(String s[])
{
    int arr[] = { 1, 7, 2 };
    int n = arr.length;

    System.out.println(Maxlen(arr, n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to find the longest
# subarray with odd product

# Function to return length of
# longest subarray with odd product
def Maxlen(a, n):

    ans = 0
    count = 0

    for i in range(n):

        # If even element
        # is encountered
        if a[i] % 2 == 0:
            count = 0
        else:
            count += 1

        # Update maximum
        ans = max(ans, count)

    return ans

# Driver code
arr = [ 1, 7, 2 ]
n = len(arr)

print(Maxlen(arr, n))

# This code is contributed by amreshkumar3
```

## C#

```
// C# program to find the longest
// subarray with odd product
using System;

class GFG{

// Function to return length of
// longest subarray with odd product
static int Maxlen(int []arr, int n)
{
    int ans = 0;
    int count = 0;

    for(int i = 0; i < n; i++)
    {

        // If even element
        // is encountered
        if (arr[i] % 2 == 0)
            count = 0;
        else
            count++;

        // Update maximum
        ans = Math.Max(ans, count);
    }
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 7, 2 };
    int n = arr.Length;

    Console.WriteLine(Maxlen(arr, n));
}
}

// This code is contributed by amreshkumar3
```

## java 描述语言

```
<script>

// Javascript program to find the longest
// subarray with odd product

// Function to return length of
// longest subarray with odd product
function Maxlen(arr, n)
{
    let ans = 0;
    let count = 0;
    for(let i = 0; i < n; i++)
    {

        // If even element
        // is encountered
        if (arr[i] % 2 == 0)
            count = 0;
        else
            count++;

        // Update maximum
        ans = Math.max(ans, count);
    }
    return ans;
}

// Driver Code

       let arr = [ 1, 7, 2 ];
    let n = arr.length;

    document.write(Maxlen(arr, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
# 通过给定操作获得给定数组所需的最小步骤数

> 原文:[https://www . geesforgeks . org/按给定操作获取给定数组所需的最小步骤数/](https://www.geeksforgeeks.org/minimum-number-of-steps-required-to-obtain-the-given-array-by-the-given-operations/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出以下类型的最小运算次数，以便仅从零数组中获得数组 **arr[]** 。

*   选择任意索引 **i** ，并将索引**【I，N–1】**处的所有元素增加 **1** 。
*   选择任意指数 **i** 并将指数**【I，N–1】**处的所有元素减少 **1** 。

**例:**

> **输入:** arr[]={1，1，2，2，1}
> **输出:** 3
> **解释:**
> 最初 arr[] = {0，0，0，0，0}
> 第一步:arr[]={1，1，1，1，1，1}(索引 0 上的操作 1)
> 第二步:arr[]={1，1，2，2，2}，2 }(索引 2 上的操作 1)
> 第三步:arr[]

**朴素方法:**最简单的方法是通过对索引**【I，N–1】**执行上述操作之一，将数组结果数组的每个元素 **brr[]** 转换为 **arr[]** ，并增加执行的每个操作的计数。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)进行优化。按照以下步骤解决问题:

*   对于 **0 <sup>第</sup>索引**，将数字 **0** 转换为**arr【0】**。因此，所需的步数始终为**a【0】**。因此，在**答案**中加上**arr【0】**。
*   对于所有其他指标，常见的贪婪观察是使用 **abs(a[i]-a[i-1])乘以**的增减操作。
*   这种方法背后的直觉是，如果数字小于**a【i-1】**，那么从**开始增加一切((I-1)..n-1)** 乘**a【I】**，然后减**(a【I-1】–a【I】)**得到**a【I】。**
*   如果**a【I】>a【I-1】**，则方法是使用 **((i-1)的增加操作..n-1)** 由**a【I-1】**增加，剩余值由 **(i)增加**(a【I】-a【I-1】)**运算..(n-1)**。
*   因此，遍历数组，对于第一个元素之后的每个元素，将连续对的**绝对差**加到**答案**中。
*   最后，打印答案。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// steps to obtain the desired array
int min_operation(int a[], int n)
{
    // Initialize variable
    int ans = 0;

    // Iterate over the array arr[]
    for (int i = 0; i < n; i++) {

        // Check if i > 0
        if (i > 0)

            // Update the answer
            ans += abs(a[i] - a[i - 1]);

        else
            ans += abs(a[i]);
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << min_operation(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to calculate the minimum
// steps to obtain the desired array
static int min_operation(int a[], int n)
{
    // Initialize variable
    int ans = 0;

    // Iterate over the array arr[]
    for (int i = 0; i < n; i++)
    {

        // Check if i > 0
        if (i > 0)

            // Update the answer
            ans += Math.abs(a[i] - a[i - 1]);

        else
            ans += Math.abs(a[i]);
    }

    // Return the result
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int n = arr.length;

    System.out.print(min_operation(arr, n));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the minimum
# steps to obtain the desired array
def min_operation(a, n):

    # Initialize variable
    ans = 0

    # Iterate over the array arr[]
    for i in range(n):

        # Check if i > 0
        if (i > 0):

            # Update the answer
            ans += abs(a[i] - a[i - 1])
        else:
            ans += abs(a[i])

    # Return the result
    return ans

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4 ]
    n = len(arr)

    print(min_operation(arr, n))

# This code is contributed by chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to calculate the minimum
// steps to obtain the desired array
static int min_operation(int []a, int n)
{
    // Initialize variable
    int ans = 0;

    // Iterate over the array []arr
    for (int i = 0; i < n; i++)
    {

        // Check if i > 0
        if (i > 0)

            // Update the answer
            ans += Math.Abs(a[i] - a[i - 1]);

        else
            ans += Math.Abs(a[i]);
    }

    // Return the result
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4 };
    int n = arr.Length;

    Console.Write(min_operation(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript Program to implement
// the above approach

    // Function to calculate the minimum
    // steps to obtain the desired array
    function min_operation(a , n) {
        // Initialize variable
        var ans = 0;

        // Iterate over the array arr
        for (i = 0; i < n; i++) {

            // Check if i > 0
            if (i > 0)

                // Update the answer
                ans += Math.abs(a[i] - a[i - 1]);

            else
                ans += Math.abs(a[i]);
        }

        // Return the result
        return ans;
    }

    // Driver Code

        var arr = [ 1, 2, 3, 4 ];
        var n = arr.length;

        document.write(min_operation(arr, n));

// This code contributed by Rajput-Ji
</script>
```

**输出:**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
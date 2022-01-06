# 通过交替相邻元素的符号最大化数组和

> 原文:[https://www . geeksforgeeks . org/通过交替相邻元素的符号来最大化数组总和/](https://www.geeksforgeeks.org/maximize-array-sum-by-alternating-the-signs-of-adjacent-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是通过交替相邻数组元素的符号找到数组元素的最大可能[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = { -2，1，0 }
> **输出:** 3
> **解释:**
> 交替符号(arr[0]，arr[1])将 arr[]修改为{2，-1，0 }。
> 交替符号(arr[1]，arr[2])将 arr[]修改为{2，1，0}。
> 因此，要求的输出= (2 + 1 + 0) = 3，这是可能的最大和。
> 
> **输入:** arr[] = { 1，1，-2，-4，5 }
> **输出:** 13
> **解释:**
> 交替(arr[2]，arr[3])的符号将 arr[]修改为{ 1，1，2，4，5 }
> 因此，所需的输出= (1 + 1 + 2 + 4 + 5) = 13，这是可能的最大和。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。这个想法是基于这样一个事实，即在交替相邻元素的符号后，数组中负元素的最大数量不能大于 **1** 。按照以下步骤解决问题:

*   初始化一个变量，比如 **MaxAltSum** ，通过交替相邻元素的符号来存储数组元素的最大可能[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[统计数组中的负元素个数。](https://www.geeksforgeeks.org/c-program-to-count-positive-and-negative-numbers-in-an-array/)
*   如果数组中负元素的[计数为](https://www.geeksforgeeks.org/python-program-to-count-positive-and-negative-numbers-in-a-list/)[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则通过交替相邻数组元素的符号可能得到的最大可能和等于数组元素绝对值的和，即**MaxAltSum =σABS(arr[I])**
*   否则，通过交替相邻数组元素的符号从数组中获得的最大可能和等于所有可能的数组元素的绝对值之和，但数组元素的最小绝对值除外。即**MaxAltSum =((σABS(arr[I])–2 * X)**，其中 **X** 是数组元素的最小绝对值。
*   最后打印数值 **MaxAltSum** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum by alternating
// the signs of adjacent elements of the array
int findMaxSumByAlternatingSign(int arr[], int N)
{
    // Stores count of negative
    // elements in the array
    int cntNeg = 0;

    // Stores maximum sum by alternating
    // the signs of adjacent elements
    int MaxAltSum = 0;

    // Stores smallest absolute
    // value of array elements
    int SmValue = 0;

    // Stores sum of absolute
    // value of array elements
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If arr[i] is
        // a negative number
        if (arr[i] < 0) {

            // Update cntNeg
            cntNeg += 1;
        }

        // Update sum
        sum += abs(arr[i]);

        // Update SmValue
        SmValue = min(SmValue,
                    abs(arr[i]));
    }

    // Update MaxAltSum
    MaxAltSum = sum;

    // If cntNeg is
    // an odd number
    if (cntNeg & 1) {

        // Update MaxAltSum
        MaxAltSum -= 2 * SmValue;
    }
    return MaxAltSum;
}

// Drivers Code
int main()
{

    int arr[] = { 1, 1, -2, -4, 5 };
    int N = sizeof(arr)
            / sizeof(arr[0]);

    cout << findMaxSumByAlternatingSign(
        arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the maximum sum by alternating
// the signs of adjacent elements of the array
static int findMaxSumByAlternatingSign(int arr[],
                                       int N)
{

    // Stores count of negative
    // elements in the array
    int cntNeg = 0;

    // Stores maximum sum by alternating
    // the signs of adjacent elements
    int MaxAltSum = 0;

    // Stores smallest absolute
    // value of array elements
    int SmValue = 0;

    // Stores sum of absolute
    // value of array elements
    int sum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is
        // a negative number
        if (arr[i] < 0)
        {

            // Update cntNeg
            cntNeg += 1;
        }

        // Update sum
        sum += Math.abs(arr[i]);

        // Update SmValue
        SmValue = Math.min(SmValue,
                  Math.abs(arr[i]));
    }

    // Update MaxAltSum
    MaxAltSum = sum;

    // If cntNeg is
    // an odd number
    if (cntNeg % 2 == 1)
    {

        // Update MaxAltSum
        MaxAltSum -= 2 * SmValue;
    }
    return MaxAltSum;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 1, -2, -4, 5 };
    int N = arr.length;

    System.out.print(findMaxSumByAlternatingSign(
    arr, N));
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum by
# alternating the signs of adjacent
# elements of the array
def findMaxSumByAlternatingSign(arr, N):

    # Stores count of negative
    # elements in the array
    cntNeg = 0

    # Stores maximum sum by alternating
    # the signs of adjacent elements
    MaxAltSum = 0

    # Stores smallest absolute
    # value of array elements
    SmValue = 0

    # Stores sum of absolute
    # value of array elements
    sum = 0

    # Traverse the array
    for i in range(N):

        # If arr[i] is
        # a negative number
        if (arr[i] < 0):

            # Update cntNeg
            cntNeg += 1

        # Update sum
        sum += abs(arr[i])

        # Update SmValue
        SmValue = min(SmValue, abs(arr[i]))

    # Update MaxAltSum
    MaxAltSum = sum

    # If cntNeg is
    # an odd number
    if (cntNeg & 1):

        # Update MaxAltSum
        MaxAltSum -= 2 * SmValue

    return MaxAltSum

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 1, -2, -4, 5 ]
    N = len(arr)

    print(findMaxSumByAlternatingSign(arr, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the maximum sum by alternating
// the signs of adjacent elements of the array
static int findMaxSumByAlternatingSign(int []arr,
                                    int N)
{

    // Stores count of negative
    // elements in the array
    int cntNeg = 0;

    // Stores maximum sum by alternating
    // the signs of adjacent elements
    int MaxAltSum = 0;

    // Stores smallest absolute
    // value of array elements
    int SmValue = 0;

    // Stores sum of absolute
    // value of array elements
    int sum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is
        // a negative number
        if (arr[i] < 0)
        {

            // Update cntNeg
            cntNeg += 1;
        }

        // Update sum
        sum += Math.Abs(arr[i]);

        // Update SmValue
        SmValue = Math.Min(SmValue,
                Math.Abs(arr[i]));
    }

    // Update MaxAltSum
    MaxAltSum = sum;

    // If cntNeg is
    // an odd number
    if (cntNeg % 2 == 1)
    {

        // Update MaxAltSum
        MaxAltSum -= 2 * SmValue;
    }
    return MaxAltSum;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 1, -2, -4, 5 };
    int N = arr.Length;

    Console.Write(findMaxSumByAlternatingSign(
    arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the maximum sum by alternating
// the signs of adjacent elements of the array
function findMaxSumByAlternatingSign(arr, N)
{

    // Stores count of negative
    // elements in the array
    let cntNeg = 0;

    // Stores maximum sum by alternating
    // the signs of adjacent elements
    let MaxAltSum = 0;

    // Stores smallest absolute
    // value of array elements
    let SmValue = 0;

    // Stores sum of absolute
    // value of array elements
    let sum = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // If arr[i] is
        // a negative number
        if (arr[i] < 0)
        {

            // Update cntNeg
            cntNeg += 1;
        }

        // Update sum
        sum += Math.abs(arr[i]);

        // Update SmValue
        SmValue = Math.min(SmValue,
                  Math.abs(arr[i]));
    }

    // Update MaxAltSum
    MaxAltSum = sum;

    // If cntNeg is
    // an odd number
    if (cntNeg % 2 == 1)
    {

        // Update MaxAltSum
        MaxAltSum -= 2 * SmValue;
    }
    return MaxAltSum;
}

    // Driver Code
    let arr = [ 1, 1, -2, -4, 5 ];
    let N = arr.length;

    document.write(findMaxSumByAlternatingSign(
    arr, N));

// This code is contributed by souravghosh0416.
</script>
```

**输出:**

```
13
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
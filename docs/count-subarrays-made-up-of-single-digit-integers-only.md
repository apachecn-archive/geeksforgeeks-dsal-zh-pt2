# 只计算由一位数整数组成的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-仅由个位数组成-整数/](https://www.geeksforgeeks.org/count-subarrays-made-up-of-single-digit-integers-only/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算仅由一位数元素组成的[个子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:** arr[] = {0，1，14，2，5}
> **输出:** 6
> **解释:**所有仅由一位数组成的子阵列为{{0}、{1}、{2}、{5}、{0，1}、{2，5}}。因此，子阵列的总数是 6。
> 
> **输入:** arr[] ={12，5，14，17}
> **输出:** 1
> **说明:**所有仅由一位数组成的子阵均为{5}。
> 因此，子阵列总数为 1。

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。对于每个子阵列，检查其中的所有整数是否都是一位数整数。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，其思想是找到连续的一位数整数的每个块的大小，并用该长度的总子阵列来增加计数。按照以下步骤解决问题:

*   初始化一个变量，比如 **res = 0** 和 **c = 0** ，以存储子阵列的总计数和子阵列中一位数整数的总计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   如果 **arr[i] < 10，**将 **c** 的计数增加 1，将 **res** 的计数增加**c**
    *   否则，分配 **c = 0。**
*   最后，打印一位数整数子数组的总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count of subarrays made
// up of single digit integers only
int singleDigitSubarrayCount(int arr[],
                             int N)
{
    // Stores count of subarrays
    int res = 0;

    // Stores the count of consecutive
    // single digit numbers in the array
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        if (arr[i] <= 9) {

            // Increment size of block by 1
            count++;

            // Increment res by count
            res += count;
        }

        else {

            // Assign count = 0
            count = 0;
        }
    }

    cout << res;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 0, 1, 14, 2, 5 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);
    singleDigitSubarrayCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to count of subarrays made
// up of single digit integers only
static void singleDigitSubarrayCount(int arr[],
                             int N)
{

    // Stores count of subarrays
    int res = 0;

    // Stores the count of consecutive
    // single digit numbers in the array
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        if (arr[i] <= 9)
        {

            // Increment size of block by 1
            count++;

            // Increment res by count
            res += count;
        }

        else
        {

            // Assign count = 0
            count = 0;
        }
    }
    System.out.print(res);
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 0, 1, 14, 2, 5 };

    // Size of the array
    int N = arr.length;
    singleDigitSubarrayCount(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count of subarrays made
# up of single digit integers only
def singleDigitSubarrayCount(arr, N):

    # Stores count of subarrays
    res = 0

    # Stores the count of consecutive
    # single digit numbers in the array
    count = 0

    # Traverse the array
    for i in range(N):
        if (arr[i] <= 9):

            # Increment size of block by 1
            count += 1

            # Increment res by count
            res += count
        else:
            # Assign count = 0
            count = 0
    print (res)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [0, 1, 14, 2, 5]

    # Size of the array
    N = len(arr)
    singleDigitSubarrayCount(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count of subarrays made
// up of single digit integers only
static void singleDigitSubarrayCount(int[] arr,
                             int N)
{

    // Stores count of subarrays
    int res = 0;

    // Stores the count of consecutive
    // single digit numbers in the array
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        if (arr[i] <= 9)
        {

            // Increment size of block by 1
            count++;

            // Increment res by count
            res += count;
        }
        else
        {

            // Assign count = 0
            count = 0;
        }
    }
    Console.Write(res);
}

// Driver Code
public static void Main(string[] args)
{
    // Given array
    int[] arr = { 0, 1, 14, 2, 5 };

    // Size of the array
    int N = arr.Length;
    singleDigitSubarrayCount(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count of subarrays made
// up of single digit integers only
function singleDigitSubarrayCount(arr, N)
{

    // Stores count of subarrays
    let res = 0;

    // Stores the count of consecutive
    // single digit numbers in the array
    let count = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        if (arr[i] <= 9)
        {

            // Increment size of block by 1
            count++;

            // Increment res by count
            res += count;
        }
        else
        {

            // Assign count = 0
            count = 0;
        }
    }
    document.write(res);
}

// Driver Code

// Given array
let arr = [ 0, 1, 14, 2, 5 ];

// Size of the array
let N = arr.length;

singleDigitSubarrayCount(arr, N);

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
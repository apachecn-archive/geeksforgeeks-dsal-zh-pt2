# 给定数组中的最大不动点(值等于索引)

> 原文:[https://www . geesforgeks . org/最大定点值等于给定数组中的索引/](https://www.geeksforgeeks.org/maximum-fixed-point-value-equal-to-index-in-a-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是找到**最大**索引 **i** ，使得 **arr[i]** 等于 **i.** 如果[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** 中没有这样的索引，则打印 **-1** 。

**示例:**

> **输入:** arr[ ] = {-10，-5，0，3，7}
> **输出:** 3
> **说明:**仅针对 i=3，arr[3] = 3
> 
> **输入:** arr[ ] = {0，2，5，8，4}
> **输出:** 4

**方法:**按照以下步骤解决这个问题:

*   [使用变量 **i** : 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**中迭代
    *   如果当前元素等于 **i** ，则打印**I****返回**。
*   如果没有这样的索引，则打印 **-1。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to  find the maximum index
// i such that arr[i] is equal to i
void findLargestIndex(int arr[], int n)
{

    // Traversing the array from
    // backwards
    for (int i = n - 1; i >= 0; i--) {

        // If arr[i] is equal to i
        if (arr[i] == i) {
            cout << i << endl;
            return;
        }
    }

    // If there is no such index
    cout << -1 << endl;
}

// Driver code
int main()
{
    // Given Input
    int arr[] = { -10, -5, 0, 3, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findLargestIndex(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

    // Function to  find the maximum index
    // i such that arr[i] is equal to i
    static void findLargestIndex(int arr[], int n)
    {

        // Traversing the array from
        // backwards
        for (int i = n - 1; i >= 0; i--) {

            // If arr[i] is equal to i
            if (arr[i] == i) {
                System.out.println(i);
                return;
            }
        }

        // If there is no such index
        System.out.println(-1);
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given Input
        int arr[] = { -10, -5, 0, 3, 7 };
        int n = arr.length;

        // Function Call
        findLargestIndex(arr, n);
    }
}

// This code is contributed by Potta Lokesh
```

## 计算机编程语言

```
# Python implementation of the above approach
# Function to  find the maximum index
# i such that arr[i] is equal to i
def findLargestIndex(arr,  n):

    # Traversing the array from
    # backwards
    for i in range (n):

        # If arr[i] is equal to i
        if (arr[i] == i) :
            print( i )
            return

    # If there is no such index
    print( -1 )

# Driver code
# Given Input
arr =  [-10, -5, 0, 3, 7 ]
n = len(arr)

# Function Call
findLargestIndex(arr, n)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to  find the maximum index
    // i such that arr[i] is equal to i
    static void findLargestIndex(int []arr, int n)
    {

        // Traversing the array from
        // backwards
        for (int i = n - 1; i >= 0; i--) {

            // If arr[i] is equal to i
            if (arr[i] == i) {
                Console.Write(i);
                return;
            }
        }

        // If there is no such index
        Console.Write(-1);
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Given Input
        int []arr = { -10, -5, 0, 3, 7 };
        int n = arr.Length;

        // Function Call
        findLargestIndex(arr, n);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript implementation of the above approach

// Function to  find the maximum index
// i such that arr[i] is equal to i
function findLargestIndex( arr,  n)
    {

        // Traversing the array from
        // backwards
        for (var i = n - 1; i >= 0; i--) {

            // If arr[i] is equal to i
            if (arr[i] == i) {
                document.write(i);
                return ;
            }
        }

        // If there is no such index
        document.write(-1);
    }

    // Driver code
    // Given Input
        var arr = [ -10, -5, 0, 3, 7 ];
        var n = arr.length;

        // Function Call
        findLargestIndex(arr, n);

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
3
```

***时间复杂度** : O(N)*
***辅助空间** : O(1)*
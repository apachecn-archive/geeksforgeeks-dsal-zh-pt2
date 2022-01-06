# 所有可能的反向双离子子阵列的计数

> 原文:[https://www . geesforgeks . org/count-of-all-可能性-reverse-bitonic-subarries/](https://www.geeksforgeeks.org/count-of-all-possible-reverse-bitonic-subarrays/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算给定数组中**个反向双子数组**的总数。

> A [**反向双离子子阵列**](https://www.geeksforgeeks.org/longest-reverse-bitonic-sequence/) 是元素先按降序排列，再按升序排列的子阵列。严格递增或严格递减的子阵列也被认为是反向双离子子阵列。

**例:**

> **输入:** arr[] = {2，3，1，4}
> **输出:** 8
> **解释:**
> 这里我们将寻找给定阵列的所有长度的子阵列
> 对于长度 1，所有子阵列都是反向双子阵列{2}、{3}、{1}、{4}
> 对于长度 2，可能的子阵列是{2，3}、{3，1}、{1，4}
> 对于长度
> **输入:**arr[]=【1，2，3】
> **输出:** 6
> **解释:**
> 这里我们将寻找给定数组的所有长度的子数组
> 对于长度 1，所有的子数组都是反向双音素{1}、{2}、{3}
> 对于长度 2，可能的子数组是{1，2}、{2，3}
> 对于长度 3，可能的子数组
> 所以总共有 6 个子阵列可能。

**方法:**想法是[从给定的阵列生成所有的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并检查每个子阵列是否满足下面提到的条件:

*   当子阵元素**严格递增时，**则取第一个元素，然后检查下一个是否递增。
*   当子阵元素**严格递减时，**取第一个元素，然后检查下一个是否递减。
*   当子阵列元素是**严格递减然后递增，**那么在这种情况下，取第一个元素，然后检查下一个递减，当它变为假时，检查递增直到最后一个元素。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that counts all the reverse
// bitonic subarray in arr[]
void countReversebitonic(int arr[],
                         int n)
{
    // To store the count of reverse
    // bitonic subarray
    int c = 0;

    // Iterate the array and select
    // the starting element
    for (int i = 0; i < n; i++) {

        // Iterate for selecting the
        // ending element for subarray
        for (int j = i; j < n; j++) {

            // Subarray arr[i to j]
            int temp = arr[i], f = 0;

            // For 1 length, increment
            // the count and continue
            if (j == i) {
                c++;
                continue;
            }

            int k = i + 1;

            // For Decreasing Subarray
            while (temp > arr[k]
                   && k <= j) {
                temp = arr[k];
                k++;
            }

            // Check if only Decreasing
            if (k > j) {
                c++;
                f = 2;
            }

            // For Increasing Subarray
            while (temp < arr[k]
                   && k <= j && f != 2) {
                temp = arr[k];
                k++;
            }

            if (k > j && f != 2) {
                c++;
                f = 0;
            }
        }
    }

    // Print the total count of subarrays
    cout << c << endl;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 3, 1, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countReversebitonic(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that counts all the reverse
// bitonic subarray in arr[]
static void countReversebitonic(int arr[],
                                int n)
{

    // To store the count of reverse
    // bitonic subarray
    int c = 0;

    // Iterate the array and select
    // the starting element
    for(int i = 0; i < n; i++)
    {

       // Iterate for selecting the
       // ending element for subarray
       for(int j = i; j < n; j++)
       {

          // Subarray arr[i to j]
          int temp = arr[i], f = 0;

          // For 1 length, increment
          // the count and continue
          if (j == i)
          {
              c++;
              continue;
          }
          int k = i + 1;

          // For decreasing subarray
          while (temp > arr[k] && k <= j)
          {
              temp = arr[k];
              k++;
          }

          // Check if only decreasing
          if (k > j)
          {
              c++;
              f = 2;
          }

          // For increasing subarray
          while (k <= j && temp < arr[k] &&
                 f != 2)
          {
              temp = arr[k];
              k++;
          }
          if (k > j && f != 2)
          {
              c++;
              f = 0;
          }
       }
    }

    // Print the total count of subarrays
    System.out.print(c + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 3, 1, 4 };

    int N = arr.length;

    // Function Call
    countReversebitonic(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts all the reverse
# bitonic subarray in arr[]
def countReversebitonic(arr, n):

    # To store the count of reverse
    # bitonic subarray
    c = 0;

    # Iterate the array and select
    # the starting element
    for i in range(n):

        # Iterate for selecting the
        # ending element for subarray
        for j in range(i, n):

            # Subarray arr[i to j]
            temp = arr[i]
            f = 0;

            # For 1 length, increment
            # the count and continue
            if (j == i):
                c += 1;
                continue;

            k = i + 1;

            # For Decreasing Subarray
            while (k <= j and temp > arr[k]):
                temp = arr[k];
                k += 1;

            # Check if only Decreasing
            if (k > j):
                c += 1;
                f = 2;

            # For Increasing Subarray
            while (k <= j and temp < arr[k] and
                   f != 2):
                temp = arr[k];
                k += 1;

            if (k > j and f != 2):
                c += 1;
                f = 0;

    # Print the total count of subarrays
    print(c)

# Driver Code

# Given array arr[]
arr = [ 2, 3, 1, 4 ];

# Function Call
countReversebitonic(arr, len(arr));

# This code is contributed by grand_master
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that counts all the reverse
// bitonic subarray in arr[]
static void countReversebitonic(int []arr,
                                int n)
{

    // To store the count of reverse
    // bitonic subarray
    int c = 0;

    // Iterate the array and select
    // the starting element
    for(int i = 0; i < n; i++)
    {

        // Iterate for selecting the
        // ending element for subarray
        for(int j = i; j < n; j++)
        {

            // Subarray arr[i to j]
            int temp = arr[i], f = 0;

            // For 1 length, increment
            // the count and continue
            if (j == i)
            {
                c++;
                continue;
            }
            int k = i + 1;

            // For decreasing subarray
            while (temp > arr[k] && k <= j)
            {
                temp = arr[k];
                k++;
            }

            // Check if only decreasing
            if (k > j)
            {
                c++;
                f = 2;
            }

            // For increasing subarray
            while (k <= j && temp < arr[k] &&
                   f != 2)
            {
                temp = arr[k];
                k++;
            }
            if (k > j && f != 2)
            {
                c++;
                f = 0;
            }
        }
    }

    // Print the total count of subarrays
    Console.Write(c);
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = { 2, 3, 1, 4 };

    int N = arr.Length;

    // Function Call
    countReversebitonic(arr, N);
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that counts all the reverse
// bitonic subarray in arr[]
function countReversebitonic(arr, n)
{

    // To store the count of reverse
    // bitonic subarray
    let c = 0;

    // Iterate the array and select
    // the starting element
    for(let i = 0; i < n; i++)
    {

       // Iterate for selecting the
       // ending element for subarray
       for(let j = i; j < n; j++)
       {

          // Subarray arr[i to j]
          let temp = arr[i], f = 0;

          // For 1 length, increment
          // the count and continue
          if (j == i)
          {
              c++;
              continue;
          }
          let k = i + 1;

          // For decreasing subarray
          while (temp > arr[k] && k <= j)
          {
              temp = arr[k];
              k++;
          }

          // Check if only decreasing
          if (k > j)
          {
              c++;
              f = 2;
          }

          // For increasing subarray
          while (k <= j && temp < arr[k] &&
                 f != 2)
          {
              temp = arr[k];
              k++;
          }
          if (k > j && f != 2)
          {
              c++;
              f = 0;
          }
       }
    }

    // Print the total count of subarrays
    document.write(c + "<br/>");
}

// Driver Code

        // Given array arr[]
    let arr = [ 2, 3, 1, 4 ];

    let N = arr.length;

    // Function Call
    countReversebitonic(arr, N);

</script>
```

**Output:** 

```
8
```

**时间复杂度:** *O(N <sup>2</sup> )* ，其中 N 是给定数组中元素的个数。
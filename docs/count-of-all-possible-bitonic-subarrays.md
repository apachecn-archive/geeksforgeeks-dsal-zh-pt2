# 所有可能的双离子子阵列的计数

> 原文:[https://www . geesforgeks . org/count-of-all-可能性-bitonic-subarrays/](https://www.geeksforgeeks.org/count-of-all-possible-bitonic-subarrays/)

给定一个由 **N** 个整数组成的数组**arr【】**，任务是计算所有本质上是[比通](https://www.geeksforgeeks.org/bitonic-sort/)的子数组。

> 一个[比特子阵](https://www.geeksforgeeks.org/longest-bitonic-subsequence-dp-15/)是一个子阵，其中的元素要么严格递增要么严格递减，要么先递增后递减。

**例:**

> **输入:** arr[] = {2，1，4，5}
> **输出:** 8
> **解释:**
> 子阵列中所有双音素的子阵列为:{2}、{2，1}、{1}、{1，4}、{1，4，5}、{4}、{4，5}和{5}。
> **输入:** arr[] = {1，2，3，4}
> **输出:** 10

**进场:**
按照以下步骤解决问题:

1.  生成所有可能的子阵列。
2.  对于每个子阵列，检查它是否是二进制的。如果子阵列是**双音素**，则增加回答计数。
3.  最后返回答案。

以下是上述方法的实现:

## C++

```
// C++ program to count the
// number of possible
// bitonic subarrays
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of bitonic subarrays
void countbitonic(int arr[], int n)
{
    int c = 0;
    // Starting element of subarray
    for (int i = 0; i < n; i++) {
        // Ending element of subarray
        for (int j = i; j < n; j++) {

            int temp = arr[i], f = 0;

            // for 1 length
            if (j == i) {
                c++;
                continue;
            }

            int k = i + 1;

            // For increasing sequence
            while (temp < arr[k] && k <= j) {
                temp = arr[k];
                k++;
            }

            // If strictly increasing
            if (k > j) {
                c++;
                f = 2;
            }

            // For decreasing sequence
            while (temp > arr[k]
                   && k <= j
                   && f != 2) {
                temp = arr[k];
                k++;
            }

            if (k > j && f != 2) {
                c++;
                f = 0;
            }
        }
    }

    cout << c << endl;
}
// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 3, 6, 5 };
    int N = 6;

    countbitonic(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of possible bitonic subarrays
import java.io.*;
import java.util.*;

class GFG{

// Function to return the count
// of bitonic subarrays
public static void countbitonic(int arr[], int n)
{
    int c = 0;

    // Starting element of subarray
    for(int i = 0; i < n; i++)
    {

       // Ending element of subarray
       for(int j = i; j < n; j++)
       {
          int temp = arr[i], f = 0;

          // For 1 length
          if (j == i)
          {
              c++;
              continue;
          }
          int k = i + 1;

          // For increasing sequence
          while (temp < arr[k] && k <= j)
          {
              temp = arr[k];
              k++;
          }

          // If strictly increasing
          if (k > j)
          {
              c++;
              f = 2;
          }

          // For decreasing sequence
          while ( k <= j && temp > arr[k] && f != 2)
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
    System.out.println(c);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 3, 6, 5 };
    int N = 6;

    countbitonic(arr, N);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to count the number
# of possible bitonic subarrays

# Function to return the count
# of bitonic subarrays
def countbitonic(arr, n):

    c = 0;

    # Starting element of subarray
    for i in range(n):

        # Ending element of subarray
        for j in range(i, n):
            temp = arr[i]
            f = 0;

            # For 1 length
            if (j == i) :
                c += 1
                continue;
            k = i + 1;

            # For increasing sequence
            while (temp < arr[k] and k <= j):
                temp = arr[k];
                k += 1

            # If strictly increasing
            if (k > j) :
                c += 1
                f = 2;

            # For decreasing sequence
            while (k <= j and temp > arr[k] and f != 2):
                temp = arr[k];
                k += 1;

            if (k > j and f != 2):
                c += 1;
                f = 0;           
    print(c)

# Driver Code
arr = [ 1, 2, 4, 3, 6, 5 ];
N = 6;

countbitonic(arr, N);

# This code is contributed by grand_master
```

## C#

```
// C# program to count the number
// of possible bitonic subarrays
using System;

class GFG{

// Function to return the count
// of bitonic subarrays    
public static void countbitonic(int []arr, int n)
{
    int c = 0;

    // Starting element of subarray
    for(int i = 0; i < n; i++)
    {

       // Ending element of subarray
       for(int j = i; j < n; j++)
       {
          int temp = arr[i], f = 0;

          // for 1 length
          if (j == i)
          {
              c++;
              continue;
          }
          int k = i + 1;

          // For increasing sequence
          while (temp < arr[k] && k <= j)
          {
              temp = arr[k];
              k++;
          }

          // If strictly increasing
          if (k > j)
          {
              c++;
              f = 2;
          }

          // For decreasing sequence
          while ( k <= j && temp > arr[k] && f != 2)
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
    Console.Write(c);
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 4, 3, 6, 5 };
    int N = 6;

    countbitonic(arr, N);
}
}

// This code is contributed by grand_master
```

## java 描述语言

```
<script>

// Javascript program to count the
// number of possible
// bitonic subarrays

// Function to return the count
// of bitonic subarrays
function countbitonic(arr, n)
{
    var c = 0;

    // Starting element of subarray
    for (var i = 0; i < n; i++)
    {

        // Ending element of subarray
        for (var j = i; j < n; j++)
        {

            var temp = arr[i], f = 0;

            // for 1 length
            if (j == i)
            {
                c++;
                continue;
            }

            var k = i + 1;

            // For increasing sequence
            while (temp < arr[k] && k <= j) {
                temp = arr[k];
                k++;
            }

            // If strictly increasing
            if (k > j) {
                c++;
                f = 2;
            }

            // For decreasing sequence
            while (temp > arr[k]
                   && k <= j
                   && f != 2) {
                temp = arr[k];
                k++;
            }

            if (k > j && f != 2) {
                c++;
                f = 0;
            }
        }
    }

    document.write( c );
}

// Driver Code
var arr = [1, 2, 4, 3, 6, 5];
var N = 6;
countbitonic(arr, N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O (1)*
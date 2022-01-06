# 合并 K 个排序数组|集合 3(使用分治法)

> 原文:[https://www . geesforgeks . org/merge-k-sorted-arrays-set-3-使用分治法/](https://www.geeksforgeeks.org/merge-k-sorted-arrays-set-3-using-divide-and-conquer-approach/)

给出 k 个排序数组，每个数组大小为 **N** ，任务是将它们合并成一个排序数组。

**示例:**

```
Input: arr[][] = {{5, 7, 15, 18},
                   {1, 8, 9, 17},
                   {1, 4, 7, 7}}
Output: {1, 1, 4, 5, 7, 7, 7, 8, 9, 15, 17, 18}

Input: arr[][] = {{3, 2, 1}
                   {6, 5, 4}}
Output:  {1, 2, 3, 4, 5, 6}
```

**先决条件** : [合并排序](https://www.geeksforgeeks.org/merge-sort/)
**<u>简单方法:</u>** 一个简单的解决方案是将所有数组一个接一个地追加并排序。

## C++14

```
// C++ program to merge K
// sorted arrays
#include <bits/stdc++.h>
using namespace std;
#define N 4

// Merge and sort k arrays
void merge_and_sort(
    vector<int> &output, vector<vector<int>> arr,
    int n, int k)
{
    // Put the elements in sorted array.
    for (int i = 0; i < k; i++) {
        for (int j = 0; j < n; j++) {
            output[(i * n) + j] = arr[i][j];
        }
    }

    // Sort the output array
    sort(output.begin(), output.end());
}

// Driver Function
int main()
{
    // Input 2D-array
    vector<vector<int>> arr = { { 5, 7, 15, 18 },
                     { 1, 8, 9, 17 },
                     { 1, 4, 7, 7 } };
    int n = N;

    // Number of arrays
    int k = arr.size();

    // Output array
    vector<int> output(n*k);

    merge_and_sort(output, arr, n, k);

    // Print merged array
    for (int i = 0; i < n * k; i++)
        cout << output[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to merge K
// sorted arrays
import java.util.*;
class GFG
{
    static int N = 4; 

    // Merge and sort k arrays
    static void merge_and_sort(int output[], int arr[][],
                               int n, int k)
    {
        // Put the elements in sorted array.
        for (int i = 0; i < k; i++)
        {
            for (int j = 0; j < n; j++)
            {
                output[i * n + j] = arr[i][j];
            }
        }

        // Sort the output array
        Arrays.sort(output);
    }

  // Driver code
    public static void main(String[] args)
    {

        // Input 2D-array
        int arr[][] = { { 5, 7, 15, 18 },
                         { 1, 8, 9, 17 },
                         { 1, 4, 7, 7 } };
        int n = N;

        // Number of arrays
        int k = arr.length;

        // Output array
        int output[] = new int[n * k];     
        merge_and_sort(output, arr, n, k);

        // Print merged array
        for (int i = 0; i < n * k; i++)
            System.out.print(output[i] + " ");
    }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program to merge K
# sorted arrays
N = 4

# Merge and sort k arrays
def merge_and_sort(output, arr, n, k):

    # Put the elements in sorted array.
    for  i in range(k):
        for j in range(n):
            output[i * n + j] = arr[i][j];

    # Sort the output array
    output.sort()

# Driver Function
if __name__=='__main__':

    # Input 2D-array
    arr = [ [ 5, 7, 15, 18 ],
                     [ 1, 8, 9, 17 ],
                     [ 1, 4, 7, 7 ] ];
    n = N;

    # Number of arrays
    k = len(arr)

    # Output array
    output = [0 for i in range(n * k)]
    merge_and_sort(output, arr, n, k);

    # Print merged array
    for  i in range(n * k):
        print(output[i], end = ' ')

# This code is contributed by rutvik_56.
```

## C#

```
// C# program to merge K
// sorted arrays
using System;
class GFG
{

    static int N = 4; 

    // Merge and sort k arrays
    static void merge_and_sort(int[] output, int[,] arr,
                               int n, int k)
    {
        // Put the elements in sorted array.
        for (int i = 0; i < k; i++)
        {
            for (int j = 0; j < n; j++)
            {
                output[i * n + j] = arr[i,j];
            }
        }

        // Sort the output array
        Array.Sort(output);
    }

  // Driver code
  static void Main()
  {

    // Input 2D-array
    int[,] arr = { { 5, 7, 15, 18 },
                     { 1, 8, 9, 17 },
                     { 1, 4, 7, 7 } };
    int n = N;

    // Number of arrays
    int k = arr.GetLength(0);

    // Output array
    int[] output = new int[n * k];     
    merge_and_sort(output, arr, n, k);

    // Print merged array
    for (int i = 0; i < n * k; i++)
        Console.Write(output[i] + " ");
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript program to merge K
    // sorted arrays

    let N = 4;

    // Merge and sort k arrays
    function merge_and_sort(output, arr, n, k)
    {
        // Put the elements in sorted array.
        for (let i = 0; i < k; i++)
        {
            for (let j = 0; j < n; j++)
            {
                output[i * n + j] = arr[i][j];
            }
        }

        // Sort the output array
        output.sort(function(a, b){return a - b});
    }

    // Input 2D-array
    let arr = [ [ 5, 7, 15, 18 ],
                 [ 1, 8, 9, 17 ],
                 [ 1, 4, 7, 7 ] ];
    let n = N;

    // Number of arrays
    let k = 3;

    // Output array
    let output = new Array(n * k);    
    merge_and_sort(output, arr, n, k);

    // Print merged array
    for (let i = 0; i < n * k; i++)
        document.write(output[i] + " ");

        // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
1 1 4 5 7 7 7 8 9 15 17 18
```
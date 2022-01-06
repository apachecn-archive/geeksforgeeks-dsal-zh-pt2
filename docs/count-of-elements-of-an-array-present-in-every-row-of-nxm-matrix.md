# NxM 矩阵每行中出现的数组元素的计数

> 原文:[https://www . geeksforgeeks . org/nxm 矩阵每一行中出现的数组元素计数/](https://www.geeksforgeeks.org/count-of-elements-of-an-array-present-in-every-row-of-nxm-matrix/)

给定 N 行，每行有 M 个元素和一个由 L 个数字组成的数组 arr[]，任务是打印矩阵每行中该数组元素的计数。
**例:**

```
Input: {8 27 39 589 23
        23 34 589 12 45
        939 32 27 12 78
        23 349 48 21 32},  

       arr[] = {589, 39, 27}

Output: 1st row - 3
        2nd row - 1
        3rd row - 1 
        4th row - 0
In 1st row, all three elements in array z[] are present
In 2nd row, only 589 in array z[] are present
In 3rd row, only 27 in array z[] are present 
In 4th row, none of the elements are present. 

Input: {1, 2, 3
        4, 5, 6}, 

       arr[] = {2, 3, 4}

Output: 1st row - 2
        2nd row - 1
```

一种简单的**方法**是迭代数组 arr[]中的每个元素，对于第 i <sup>行</sup>行，对数组 arr[]中的每个元素进行[线性搜索](https://www.geeksforgeeks.org/linear-search/)。计算元素数量并打印每行的结果。
**时间复杂度:** O(N*M*L)
一种**有效的方法**是迭代矩阵的第 i <sup>行</sup>中的所有元素。使用[哈希表](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)标记所有元素。迭代 Z 数组中的数字数组，检查哈希表中是否存在该数字。增加每个元素的数量。检查完所有元素后，打印计数。
以下是上述方法的实施:

## C++

```
// C++ program to print the count of
// elements present in the NxM matrix
#include <bits/stdc++.h>
using namespace std;

// Function to print the count of
// elements present in the NxM matrix
void printCount(int a[][5], int n, int m, int z[], int l)
{
    // iterate in the n rows
    for (int i = 0; i < n; i++) {
        // map to mark elements in N-th row
        unordered_map<int, int> mp;

        // mark all elements in the n-th row
        for (int j = 0; j < m; j++)
            mp[a[i][j]] = 1;

        int count = 0;

        // check for occurrence of all elements
        for (int j = 0; j < l; j++) {
            if (mp[z[j]])
                count += 1;
        }

        // print the occurrence of all elements
        cout << "row" << i + 1 << " = " << count << endl;
    }
}

// Driver Code
int main()
{

    // NxM matrix
    int a[][5] = { { 8, 27, 39, 589, 23 },
                { 23, 34, 589, 12, 45 },
                { 939, 32, 27, 12, 78 },
                { 23, 349, 48, 21, 32 } };

    // elements array
    int arr[] = { 589, 39, 27 };

    int n = sizeof(a) / sizeof(a[0]);

    int m = 5;

    int l = sizeof(arr) / sizeof(arr[0]);

    printCount(a, n, m, arr, l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the count of
// elements present in the NxM matrix
import java.util.*;

class GFG
{

// Function to print the count of
// elements present in the NxM matrix
static void printCount(int a[][], int n, int m,
                                int z[], int l)
{
    // iterate in the n rows
    for (int i = 0; i < n; i++)
    {
        // map to mark elements in N-th row
        Map<Integer,Integer> mp = new HashMap<>();

        // mark all elements in the n-th row
        for (int j = 0; j < m; j++)
            mp.put(a[i][j], 1);

        int count = 0;

        // check for occurrence of all elements
        for (int j = 0; j < l; j++)
        {
            if (mp.containsKey(z[j]))
                count += 1;
        }

        // print the occurrence of all elements
                System.out.println("row" +(i + 1) + " = " + count);
    }
}

// Driver Code
public static void main(String[] args)
{
    // NxM matrix
    int a[][] = { { 8, 27, 39, 589, 23 },
                { 23, 34, 589, 12, 45 },
                { 939, 32, 27, 12, 78 },
                { 23, 349, 48, 21, 32 } };

    // elements array
    int arr[] = { 589, 39, 27 };

    int n = a.length;

    int m = 5;

    int l = arr.length;

    printCount(a, n, m, arr, l);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print the count of
# elements present in the NxM matrix

# Function to print the count of
# elements present in the NxM matrix
def printCount(a, n, m, z, l):

    # iterate in the n rows
    for i in range(n):

        # map to mark elements in N-th row
        mp = dict()

        # mark all elements in the n-th row
        for j in range(m):
            mp[a[i][j]] = 1

        count = 0

        # check for occurrence of all elements
        for j in range(l):

            if z[j] in mp.keys():

                count += 1

        # print the occurrence of all elements
        print("row", i + 1, " = ", count )

# Driver Code

# NxM matrix
a = [[ 8, 27, 39, 589, 23 ],
     [ 23, 34, 589, 12, 45 ],
     [ 939, 32, 27, 12, 78 ],
     [ 23, 349, 48, 21, 32 ]]

# elements array
arr = [ 589, 39, 27 ]

n = len(a)

m = 5

l = len(arr)

printCount(a, n, m, arr, l)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print the count of
// elements present in the NxM matrix
using System;
using System.Collections.Generic;

class GFG
{

// Function to print the count of
// elements present in the NxM matrix
static void printCount(int [,]a, int n, int m,
                                int []z, int l)
{
    // iterate in the n rows
    for (int i = 0; i < n; i++)
    {
        // map to mark elements in N-th row
        Dictionary<int,int> mp = new Dictionary<int,int>();

        // mark all elements in the n-th row
        for (int j = 0; j < m; j++)
            mp.Add(a[i,j], 1);

        int count = 0;

        // check for occurrence of all elements
        for (int j = 0; j < l; j++)
        {
            if (mp.ContainsKey(z[j]))
                count += 1;
        }

        // print the occurrence of all elements
        Console.WriteLine("row" +(i + 1) + " = " + count);
    }
}

// Driver Code
public static void Main(String[] args)
{
    // NxM matrix
    int [,]a = { { 8, 27, 39, 589, 23 },
                { 23, 34, 589, 12, 45 },
                { 939, 32, 27, 12, 78 },
                { 23, 349, 48, 21, 32 } };

    // elements array
    int []arr = { 589, 39, 27 };

    int n = a.GetLength(0);

    int m = 5;

    int l = arr.Length;

    printCount(a, n, m, arr, l);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to print the count of
// elements present in the NxM matrix

    // Function to print the count of
// elements present in the NxM matrix
    function printCount(a,n,m,z,l)
    {
        // iterate in the n rows
    for (let i = 0; i < n; i++)
    {
        // map to mark elements in N-th row
        let mp = new Map();

        // mark all elements in the n-th row
        for (let j = 0; j < m; j++)
            mp.set(a[i][j], 1);

        let count = 0;

        // check for occurrence of all elements
        for (let j = 0; j < l; j++)
        {
            if (mp.has(z[j]))
                count += 1;
        }

        // print the occurrence of all elements
                document.write("row" +(i + 1) +
                " = " + count+"<br>");
    }
    }

    // Driver Code

    // NxM matrix
    let a = [[ 8, 27, 39, 589, 23 ],
     [ 23, 34, 589, 12, 45 ],
     [ 939, 32, 27, 12, 78 ],
     [ 23, 349, 48, 21, 32 ]];

    // elements array 
    let arr=[ 589, 39, 27];
    let n = a.length;
    let m = 5;
    let l = arr.length;
    printCount(a, n, m, arr, l);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
row1 = 3
row2 = 1
row3 = 1
row4 = 0
```

**时间复杂度:** O(N*M)
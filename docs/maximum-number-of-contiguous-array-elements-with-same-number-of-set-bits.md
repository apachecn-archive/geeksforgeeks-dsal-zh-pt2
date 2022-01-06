# 设置位数相同的连续数组元素的最大数量

> 原文:[https://www . geeksforgeeks . org/具有相同集合位数的最大连续数组元素数/](https://www.geeksforgeeks.org/maximum-number-of-contiguous-array-elements-with-same-number-of-set-bits/)

给定一个有 n 个元素的数组。任务是找到具有相同设置位数的最大数量的连续数组元素。
**例** :

```
Input : arr[] = {14, 1, 2, 32, 12, 10}
Output : 3
Elements 1, 2, 32 have same number of set bits
and are contiguous.

Input : arr[] = {1, 6, 9, 15, 8}
Output : 2
Elements 6, 9 have same number of set bits.
```

**进场:**

*   从左到右遍历数组，并将每个元素的设置位数存储在一个向量中。
*   我们的任务简化为寻找这个向量中相同元素的最长链。
*   维护两个变量，current_count 和 max_count。用 1 初始化它们。
*   遍历向量并检查当前元素是否与前一个元素相同。如果相同，增加 current_count。如果不相同，则用 1 重新初始化 current_count。
*   在每一步中，max_count 必须被赋予 max_count 和 current_count 之间的最大值。
*   max_count 的最终值就是答案。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum number of
// contiguous array elements with same
// number of set bits
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum contiguous elements
// with same set bits
int sameSetBits(int arr[], int n)
{
    vector<int> v;

    // Insert number of set bits in each element
    // of the array to the vector
    // __builtin_popcount() function returns the number
    // of set bits in an integer in C++
    for (int i = 0; i < n; i++)
        v.push_back(__builtin_popcount(arr[i]));

    int current_count = 1, max_count = 1;

    // Finding the maximum number of same
    // contiguous elements
    for (int i = 1; i < v.size(); i++) {
        if (v[i + 1] == v[i])
            current_count++;
        else
            current_count = 1;

        max_count = max(max_count, current_count);
    }

    // return answer
    return max_count;
}

// Driver code
int main()
{
    int arr[] = { 9, 75, 14, 7, 13, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sameSetBits(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// number of contiguous array elements
// with same number of set bits
import java.io.*;
import java.util.*;

class GFG
{

    // Function to find maximum contiguous
    // elements with same set bits
    static int sameSetBits(int arr[], int n)
    {
        Vector<Integer> v = new Vector<>();

        // Insert number of set bits in each element
        // of the array to the vector
                for (int i = 0; i < n; i++)
        {
            int count = Integer.bitCount(arr[i]);
            v.add(count);
        }

        int current_count = 1, max_count = 1;

        // Finding the maximum number of same
        // contiguous elements
        for (int i = 1; i < v.size()-1; i++)
        {
            if (v.get(i + 1) == v.get(i))
                current_count++;
            else
                current_count = 1;

            max_count = Math.max(max_count, current_count);
        }

        // return answer
        return max_count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 9, 75, 14, 7, 13, 11 };
        int n = arr.length;
        System.out.println(sameSetBits(arr, n));
    }
}

// This code is contributed by Archana_kumari
```

## 蟒蛇 3

```
# Python 3 program to find the maximum
# number of contiguous array elements
# with same number of set bits

# Function to find maximum contiguous
# elements with same set bits
def sameSetBits(arr, n):
    v = []

    # Insert number of set bits in each
    # element of the array to the vector

    # function returns the number of set
    # bits in an integer
    for i in range(0, n, 1):
        v.append(bin(arr[i]).count('1'))

    current_count = 1
    max_count = 1

    # Finding the maximum number of same
    # contiguous elements
    for i in range(1, len(v) - 1, 1):
        if (v[i + 1] == v[i]):
            current_count += 1
        else:
            current_count = 1

        max_count = max(max_count,
                        current_count)

    # return answer
    return max_count

# Driver code
if __name__ == '__main__':
    arr = [9, 75, 14, 7, 13, 11]
    n = len(arr)

    print(sameSetBits(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the maximum
// number of contiguous array elements
// with same number of set bits
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find maximum contiguous
    // elements with same set bits
    static int sameSetBits(int []arr, int n)
    {
        List<int> v = new List<int>();

        // Insert number of set bits in each element
        // of the array to the vector
        for (int i = 0; i < n; i++)
        {
            int count = Bitcount(arr[i]);
            v.Add(count);
        }

        int current_count = 1, max_count = 1;

        // Finding the maximum number of same
        // contiguous elements
        for (int i = 1; i < v.Count-1; i++)
        {
            if (v[i + 1] == v[i])
                current_count++;
            else
                current_count = 1;

            max_count = Math.Max(max_count, current_count);
        }

        // return answer
        return max_count;
    }

    static int Bitcount(int n)
    {
        int count = 0;
        while (n != 0)
        {
            count++;
            n &= (n - 1);
        }
        return count;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 9, 75, 14, 7, 13, 11 };
        int n = arr.Length;
        Console.WriteLine(sameSetBits(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the maximum number of
// contiguous array elements with same
// number of set bits

function Bitcount(n)
{
    var count = 0;
    while (n != 0)
    {
        count++;
        n &= (n - 1);
    }
    return count;
}

// Function to find maximum contiguous elements
// with same set bits
function sameSetBits(arr, n)
{
    var v = [];

    // Insert number of set bits in each element
    // of the array to the vector
    // Bitcount function returns the number
    // of set bits in an integer in C++
    for (var i = 0; i < n; i++)
        v.push(Bitcount(arr[i]));

    var current_count = 1, max_count = 1;

    // Finding the maximum number of same
    // contiguous elements
    for (var i = 1; i < v.length; i++) {
        if (v[i + 1] == v[i])
            current_count++;
        else
            current_count = 1;

        max_count = Math.max(max_count, current_count);
    }

    // return answer
    return max_count;
}

// Driver code
var arr = [ 9, 75, 14, 7, 13, 11 ];
var n = arr.length;
document.write( sameSetBits(arr, n));

</script>
```

**Output:** 

```
4
```
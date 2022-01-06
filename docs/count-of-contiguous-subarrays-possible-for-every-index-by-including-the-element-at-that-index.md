# 通过在每个索引处包含元素来计算该索引可能的连续子阵列的数量

> 原文:[https://www . geeksforgeeks . org/连续子数组计数-通过在索引处包含元素来实现每个索引的可能性/](https://www.geeksforgeeks.org/count-of-contiguous-subarrays-possible-for-every-index-by-including-the-element-at-that-index/)

给定一个代表数组大小的数字**N****A[]**，任务是通过在原始数组中包含该索引处的元素，找到数组每个索引可以形成的连续子数组的数量。

**示例:**

> **输入:** N = 4
> **输出:** {4，6，6，4}
> **说明:**
> 既然数组的大小给定为 4。让我们假设数组是{1，2，3，4}。
> 包含 1 的子阵列数量为:{{1}、{1，2}、{1，2，3}、{1，2，3，4}}
> 包含 2 的子阵列数量为:{{2}、{2，3}、{2，3，4}、{1，2}、{1，2，3}、{1，2，3}，{1，3，4}}
> 包含 3 的子阵列数量为:{{3}、{2，3}、{3}
> 
> **输入:**3
> T3】输出: {3，4，3}
> **说明:**
> 既然数组的大小给定为 3。让我们假设数组是{1，2，3}。
> 包含 1 的子阵数量为:{{1}、{1，2}、{1，2，3}}
> 包含 2 的子阵数量为:{{2}、{1，2}、{2，3}、{1，2，3}}
> 包含 3 的子阵数量为:{{3}、{2，3}、{1，2，3}}

**做法:**思路是用排列组合的概念。可以观察到，包括位于第 **i <sup>第</sup>T5】索引处的元素的可能子阵列的数量总是等于包括位于索引处的元素的可能子阵列的数量(**N–I**)，其中 **N** 是阵列的长度。**

*   遍历数组的前半部分。
*   包含第 **i <sup>个</sup>T3】索引处元素的子阵列数量始终等于包含第**N–I**索引处元素的子阵列数量。因此，同时更新两个索引的计数。**
*   为了计算包含第**I**索引处元素的子阵列数量，我们只需从总路数中减去不包含第**I**索引处元素的子阵列数量。
*   因此，计算所需值的公式为:

```
Count of possible subarrays = N * (i + 1) - i * (i + 1)
```

其中 I 是当前指数。

*   计算并存储每个索引的上述值。

下面是上述方法的实现:

## C++

```
// C++ program to find the number of
// contiguous subarrays including
// the element at every index
// of the array of size N

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// subarrays including the element
// at every index of the array
vector<int> calculateWays(int N)
{
    int x = 0;
    vector<int> v;

    // Creating an array of size N
    for (int i = 0; i < N; i++)
        v.push_back(0);

    // The loop is iterated till half the
    // length of the array
    for (int i = 0; i <= N / 2; i++) {

        // Condition to avoid overwriting
        // the middle element for the
        // array with even length.
        if (N % 2 == 0 && i == N / 2)
            break;

        // Computing the number of subarrays
        x = N * (i + 1) - (i + 1) * i;

        // The ith element from the beginning
        // and the ending have the same
        // number of possible subarrays
        v[i] = x;
        v[N - i - 1] = x;
    }
    return v;
}

// Function to print the vector
void printArray(vector<int> v)
{
    for (int i = 0; i < v.size(); i++)
        cout << v[i] << " ";
}

// Driver code
int main()
{
    vector<int> v;
    v = calculateWays(4);

    printArray(v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of contiguous subarrays including
// the element at every index
// of the array of size N
import java.util.Scanner;

class contiguous_subarrays{

// Function to find the number of
// subarrays including the element
// at every index of the array
public static int[] calculateWays(int n)
{
    int x = 0;

    // Creating an array of size N
    int[]v = new int[n];

    for(int i = 0; i < n; i++)
    v[i] = 0;

    // The loop is iterated till half the
    // length of the array
    for(int i = 0; i < n / 2; i++)
    {
        // Condition to avoid overwriting
        // the middle element for the
        // array with even length.
        if(n % 2 == 0 && i == n / 2)
        break;

        // Computing the number of subarrays
        x = n * (i + 1) - (i + 1) * i;

        // The ith element from the beginning
        // and the ending have the same
        // number of possible subarray
        v[i] = x;
        v[n - i - 1] = x;
    }

    return v;
}

// Function to print the vector
public static void printArray(int[]v)
{
    for(int i = 0; i < v.length; i++)
    System.out.print(v[i] + " ");
}

// Driver code
public static void main (String args[])
{
    int[]v;
    v = calculateWays(4);

    printArray(v);
}
}

// This code is contributed by sayesha
```

## 蟒蛇 3

```
# Python3 program to find the number of
# contiguous subarrays including
# the element at every index
# of the array of size N

# Function to find the number of
# subarrays including the element
# at every index of the array
def calculateWays(N):
    x = 0;
    v = [];

    # Creating an array of size N
    for i in range(N):
        v.append(0);

    # The loop is iterated till half the
    # length of the array
    for i in range(N // 2 + 1):

        # Condition to avoid overwriting
        # the middle element for the
        # array with even length.
        if (N % 2 == 0 and i == N // 2):
            break;

        # Computing the number of subarrays
        x = N * (i + 1) - (i + 1) * i;

        # The ith element from the beginning
        # and the ending have the same
        # number of possible subarrays
        v[i] = x;
        v[N - i - 1] = x;

    return v;

# Function to print the vector
def printArray(v):

    for i in range(len(v)):
        print(v[i], end = " ");

# Driver code
if __name__ == "__main__":

    v = calculateWays(4);
    printArray(v);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the number
// of contiguous subarrays including
// the element at every index
// of the array of size N
using System;

class GFG{

// Function to find the number of
// subarrays including the element
// at every index of the array
public static int[] calculateWays(int N)
{
    int x = 0;

    // Creating an array of size N
    int[]v = new int[N];

    for(int i = 0; i < N; i++)
        v[i] = 0;

    // The loop is iterated till half
    // the length of the array
    for(int i = 0; i < N / 2; i++)
    {

       // Condition to avoid overwriting
       // the middle element for the
       // array with even length.
       if(N % 2 == 0 && i == N / 2)
          break;

       // Computing the number of subarrays
       x = N * (i + 1) - (i + 1) * i;

       // The ith element from the beginning
       // and the ending have the same
       // number of possible subarray
       v[i] = x;
       v[N - i - 1] = x;
    }
    return v;
}

// Function to print the vector
public static void printArray(int []v)
{
    for(int i = 0; i < v.Length; i++)
    {
       Console.Write(v[i] + " ");
    }
}

// Driver code
public static void Main (string []args)
{
    int []v;
    v = calculateWays(4);

    printArray(v);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to find the number
// of contiguous subarrays including
// the element at every index
// of the array of size N

// Function to find the number of
// subarrays including the element
// at every index of the array
function calculateWays(n)
{
    let x = 0;

    // Creating an array of size N
    let v = Array.from({length: n}, (_, i) => 0);

    for(let i = 0; i < n; i++)
        v[i] = 0;

    // The loop is iterated till half the
    // length of the array
    for(let i = 0; i < n / 2; i++)
    {

        // Condition to avoid overwriting
        // the middle element for the
        // array with even length.
        if(n % 2 == 0 && i == n / 2)
            break;

        // Computing the number of subarrays
        x = n * (i + 1) - (i + 1) * i;

        // The ith element from the beginning
        // and the ending have the same
        // number of possible subarray
        v[i] = x;
        v[n - i - 1] = x;
    }
    return v;
}

// Function to prlet the vector
function prletArray(v)
{
    for(let i = 0; i < v.length; i++)
        document.write(v[i] + " ");
}

// Driver Code
let v;
v = calculateWays(4);

prletArray(v);

// This code is contributed by target_2

</script>
```

**Output:** 

```
4 6 6 4
```

时间复杂度:0(n)

辅助空间:O(n)
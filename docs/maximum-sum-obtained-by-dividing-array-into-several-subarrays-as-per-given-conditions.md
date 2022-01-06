# 根据给定条件将阵列分成若干子阵列得到的最大和

> 原文:[https://www . geeksforgeeks . org/按给定条件将数组分成若干个子数组获得的最大和/](https://www.geeksforgeeks.org/maximum-sum-obtained-by-dividing-array-into-several-subarrays-as-per-given-conditions/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过将该阵列分成几个[子阵列(](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)可能是一个)来计算可以获得的最大和，其中每个子阵列从索引 **i** 开始，到索引 **j (j > =i)** 结束，将 **arr[j]-arr[i]** 贡献给和。

**示例:**

> **输入:** arr[]= {1，5，3}，N=3
> **输出:**
> 4
> ***解释*** **:** 阵列可分为 2 个子阵列:
> 
> *   {1，5} ->子阵列贡献的总和= 5-1 = 4
> *   {3} ->子阵列贡献的总和= 3-3 = 0
> 
> 因此，答案是 4。(可以看出，没有其他方法可以将这个阵列分成多个子阵列，从而使答案大于 4)。
> 
> **输入:** arr[] = {6，2，1}，N=3
> **输出:**
> 0

**天真方法:**天真方法是考虑将 **arr** 分成 1 个或多个子阵列并计算每个子阵列获得的最大和的所有可能方式。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**观察:**解决问题所需的观察如下:

1.  阵列应该被分成几个(可能是一个)子阵列，这样每个子阵列就是[最长的递增子阵列](https://www.geeksforgeeks.org/longest-increasing-subarray/)。例如，如果 **arr[]={3，5，7，9，1}** ，最好将 **{3，5，7，9}** 视为一个子阵列，因为它将贡献 **9-3=6** 之和。分解它进一步减少了非最优的总和。
2.  非递增子阵列的每个元素都应被视为单元素子阵列，以便它们对总和的贡献为 0。否则，它们将贡献一个负值。例如，如果 **arr[i] > arr[i+1]，**最好考虑长度为 1 的两个子阵列，分别包含 **arr[i]** 和 **arr[i+1]** ，这样它们就为答案贡献了**(arr[I]-arr[I])+(arr[I+1]-arr[I+1])= 0**。如果将它们放在一起考虑，它们将贡献 **arr[i+1]-arr[i]** ，这是一个负数，从而减少总和。

**高效方法:**按照以下步骤解决问题:

1.  初始化一个变量**将**求和为 0。
2.  使用变量 **i** 遍历**从 **1** 到 **N-1、**，并执行以下操作:**
    1.  如果 **arr[i] > arr[i-1]** ，则在 **Sum** 中加上 **arr[i]-arr[i-1]** 。这是因为排序数组中相邻元素的差之和等于末端元素的差。这里，只有增加的子阵列被认为是 **arr[i] > arr[i-1]。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required answer
int maximumSum(int arr[], int N)
{
    // Stores maximum sum
    int Sum = 0;
    for (int i = 1; i < N; i++) {

        // Adding the difference of elements at ends of
        // increasing subarray to the answer
        if (arr[i] > arr[i - 1])
            Sum += (arr[i] - arr[i - 1]);
    }
    return Sum;
}
// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 5, 3 };
    int N = (sizeof(arr) / (sizeof(arr[0])));

    // Functio calling
    cout << maximumSum(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the required answer
public static int maximumSum(int arr[], int N)
{

    // Stores maximum sum
    int Sum = 0;
    for(int i = 1; i < N; i++)
    {

        // Adding the difference of elements at ends
        // of increasing subarray to the answer
        if (arr[i] > arr[i - 1])
            Sum += (arr[i] - arr[i - 1]);
    }
    return Sum;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int arr[] = { 1, 5, 3 };
    int N = arr.length;

    // Function calling
    System.out.println(maximumSum(arr, N));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the required answer
def maximumSum(arr, N):

    # Stores maximum sum
    Sum = 0;
    for i in range(1,N):

        # Adding the difference of elements at ends of
        # increasing subarray to the answer
        if (arr[i] > arr[i - 1]):
            Sum += (arr[i] - arr[i - 1])

    return Sum;

# Driver Code

#Input
arr = [ 1, 5, 3 ];
N = len(arr)

# Functio calling
print(maximumSum(arr, N));

# This code is contributed by SoumikMondal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the required answer
static int maximumSum(int []arr, int N)
{

    // Stores maximum sum
    int Sum = 0;
    for(int i = 1; i < N; i++)
    {

        // Adding the difference of elements at
        // ends of increasing subarray to the answer
        if (arr[i] > arr[i - 1])
            Sum += (arr[i] - arr[i - 1]);
    }
    return Sum;
}

// Driver Code
public static void Main()
{

    // Input
    int []arr = { 1, 5, 3 };
    int N = arr.Length;

    // Functio calling
    Console.Write(maximumSum(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the required answer
function maximumSum(arr, N)
{

    // Stores maximum sum
    let Sum = 0;
    for(let i = 1; i < N; i++)
    {

        // Adding the difference of elements at ends
        // of increasing subarray to the answer
        if (arr[i] > arr[i - 1])
            Sum += (arr[i] - arr[i - 1]);
    }
    return Sum;
}

// Driver Code

// Input
let arr = [ 1, 5, 3 ];
let N = arr.length;

// Function calling
document.write(maximumSum(arr, N));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
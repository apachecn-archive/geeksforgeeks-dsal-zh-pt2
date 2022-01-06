# 通过单次交换最大化最小和最大数组元素之间的距离

> 原文:[https://www . geeksforgeeks . org/按单个交换最大化最小和最大数组元素之间的距离/](https://www.geeksforgeeks.org/maximize-distance-between-smallest-and-largest-array-elements-by-a-single-swap/)

给定由范围**【1，N】**中的 **N** 元素组成的 **arr[]** ，任务是通过单次交换最大化最小和最大数组元素之间的距离。
**举例:**

> **输入:** arr[] = {1，4，3，2}
> **输出:** 3
> **解释:**
> arr[1]和 arr[3]的互换使距离最大化。
> **输入:** arr[] = {1，6，5，3，4，7，2}
> **输出:** 6
> **解释:**
> arr[5]和 arr[6]的 Swappinf 最大化了距离。

**接近**T2】

1.  找出数组中 1 和 N 的索引。
2.  让 **minIdx** 和**maxdx**分别为这两个指标的最小值和最大值。
3.  现在，maxIdx–minIdx 是两个元素之间的当前距离。它可以通过以下两种互换的最大可能来实现最大化:
    *   将**a【minIdx】**换成**a【0】**增加 **minIdx** 的距离。
    *   将 **a【最大值】**换成**a【N–1】**，增加**N–1–最大值**的距离。

以下是上述方法的实现:

## C++

```
// C++ program maximize the
// distance between smallest
// and largest array element
// by a single swap
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the distance
// between the smallest and largest
// array element by a single swap
int find_max_dist(int arr[], int N)
{

    int minIdx = -1, maxIdx = -1;

    for (int i = 0; i < N; i++) {
        if (arr[i] == 1 || arr[i] == N) {
            if (minIdx == -1)
                minIdx = i;
            else {
                maxIdx = i;
                break;
            }
        }
    }

    return maxIdx - minIdx
           + max(minIdx, N - 1 - maxIdx);
}

// Driver Code
int main()
{
    int arr[] = { 1, 4, 3, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << find_max_dist(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program maximize the distance
// between smallest and largest array
// element by a single swap
import java.util.*;

class GFG{

// Function to maximize the distance
// between the smallest and largest
// array element by a single swap
static int find_max_dist(int arr[], int N)
{
    int minIdx = -1, maxIdx = -1;

    for(int i = 0; i < N; i++)
    {
       if (arr[i] == 1 || arr[i] == N)
       {
           if (minIdx == -1)
               minIdx = i;
           else
           {
               maxIdx = i;
               break;
           }
       }
    }
    return maxIdx - minIdx +
           Math.max(minIdx, N - 1 - maxIdx);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 4, 3, 2 };
    int N = arr.length;

    System.out.print(find_max_dist(arr, N) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program maximize the
# distance between smallest
# and largest array element
# by a single swap

# Function to maximize the distance
# between the smallest and largest
# array element by a single swap
def find_max_dist(arr, N):

    minIdx, maxIdx = -1, -1

    for i in range(N):
        if (arr[i] == 1 or arr[i] == N):
            if (minIdx == -1) :
                minIdx = i

            else :
                maxIdx = i
                break

    return (maxIdx - minIdx +
        max(minIdx, N - 1 - maxIdx))

# Driver code
arr = [ 1, 4, 3, 2 ]
N = len(arr)

print(find_max_dist(arr, N))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program maximize the distance
// between smallest and largest array
// element by a single swap
using System;

class GFG{

// Function to maximize the distance
// between the smallest and largest
// array element by a single swap
static int find_max_dist(int []arr, int N)
{
    int minIdx = -1, maxIdx = -1;

    for(int i = 0; i < N; i++)
    {
       if (arr[i] == 1 || arr[i] == N)
       {
           if (minIdx == -1)
               minIdx = i;
           else
           {
               maxIdx = i;
               break;
           }
       }
    }
    return maxIdx - minIdx +
           Math.Max(minIdx, N - 1 - maxIdx);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 4, 3, 2 };
    int N = arr.Length;

    Console.Write(find_max_dist(arr, N) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program maximize the distance
// between smallest and largest array
// element by a single swap

// Function to maximize the distance
// between the smallest and largest
// array element by a single swap
function find_max_dist(arr , N)
{
    var minIdx = -1, maxIdx = -1;

    for(i = 0; i < N; i++)
    {
       if (arr[i] == 1 || arr[i] == N)
       {
           if (minIdx == -1)
               minIdx = i;
           else
           {
               maxIdx = i;
               break;
           }
       }
    }
    return maxIdx - minIdx +
           Math.max(minIdx, N - 1 - maxIdx);
}

// Driver Code
var arr = [ 1, 4, 3, 2 ];
var N = arr.length;

document.write(find_max_dist(arr, N) + "\n");

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*T4】
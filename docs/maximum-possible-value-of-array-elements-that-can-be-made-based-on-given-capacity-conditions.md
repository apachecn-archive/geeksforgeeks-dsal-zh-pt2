# 基于给定的容量条件可以得到的阵列元素的最大可能值

> 原文:[https://www . geeksforgeeks . org/基于给定容量条件的最大可能数组元素值/](https://www.geeksforgeeks.org/maximum-possible-value-of-array-elements-that-can-be-made-based-on-given-capacity-conditions/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和**cap【】**均由 **N** 正整数组成，因此**I<sup>th</sup>T11】元素**cap【I】**表示**arr【I】**的容量， 任务是找到数组元素[的最大可能值](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，如果相邻元素的最终值没有超过其相应的容量，则允许将数组元素 **arr[i]** 减少某个任意值，并将其任何相邻元素增加相同的值。**

**示例:**

> **输入:** arr[] = {2，3}，cap[] = {5，6}
> **输出:** 5
> **解释:**
> 执行以下操作以最大化 arr[]:
> **操作 1:** 将 arr[0]减少 2，将 arr[1]增加 2。现在 arr[] = {0，5}。
> 因此，arr[]中的最大元素为 5。
> 
> **输入:** arr[] = {1，2，1}，cap[] = {2，3，2}
> **输出:** 3

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，该方法基于以下观察:在执行任意次数的操作后，最大值不能超过 cap[]中的最大容量。因此答案将是 **min(** [**所有阵元之和**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) ，**最大容量在 cap[])** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum element
// after shifting operations in arr[]
int maxShiftArrayValue(int arr[], int cap[],
                       int N)
{
    // Stores the sum of array element
    int sumVals = 0;
    for (int i = 0; i < N; i++) {
        sumVals += arr[i];
    }

    // Stores the maximum element in cap[]
    int maxCapacity = 0;

    // Iterate to find maximum element
    for (int i = 0; i < N; i++) {
        maxCapacity = max(cap[i], maxCapacity);
    }

    // Return the resultant maximum value
    return min(maxCapacity, sumVals);
}

// Driver Code
int main()
{
    int arr[] = { 2, 3 };
    int cap[] = { 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxShiftArrayValue(arr, cap, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to find the maximum element
    // after shifting operations in arr[]
    public static int maxShiftArrayValue(int arr[], int cap[], int N)
    {

        // Stores the sum of array element
        int sumVals = 0;
        for (int i = 0; i < N; i++) {
            sumVals += arr[i];
        }

        // Stores the maximum element in cap[]
        int maxCapacity = 0;

        // Iterate to find maximum element
        for (int i = 0; i < N; i++) {
            maxCapacity = Math.max(cap[i], maxCapacity);
        }

        // Return the resultant maximum value
        return Math.min(maxCapacity, sumVals);
    }

    // Driver Code
    public static void main(String args[]) {
        int arr[] = { 2, 3 };
        int cap[] = { 5, 6 };
        int N = arr.length;

        System.out.println(maxShiftArrayValue(arr, cap, N));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum element
# after shifting operations in arr[]
def maxShiftArrayValue(arr, cap, N):

    # Stores the sum of array element
    sumVals = 0
    for i in range(N):
        sumVals += arr[i]

    # Stores the maximum element in cap[]
    maxCapacity = 0

    # Iterate to find maximum element
    for i in range(N):
        maxCapacity = max(cap[i], maxCapacity)

    # Return the resultant maximum value
    return min(maxCapacity, sumVals)

# Driver Code
if __name__ == '__main__':
    arr  = [2, 3]
    cap  = [5, 6]
    N = len(arr)
    print(maxShiftArrayValue(arr, cap, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the maximum element
    // after shifting operations in arr[]
    public static int maxShiftArrayValue(int[] arr,
                                         int[] cap, int N)
    {

        // Stores the sum of array element
        int sumVals = 0;
        for (int i = 0; i < N; i++) {
            sumVals += arr[i];
        }

        // Stores the maximum element in cap[]
        int maxCapacity = 0;

        // Iterate to find maximum element
        for (int i = 0; i < N; i++) {
            maxCapacity = Math.Max(cap[i], maxCapacity);
        }

        // Return the resultant maximum value
        return Math.Min(maxCapacity, sumVals);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 2, 3 };
        int[] cap = { 5, 6 };
        int N = arr.Length;

        Console.WriteLine(maxShiftArrayValue(arr, cap, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the maximum element
       // after shifting operations in arr[]
       function maxShiftArrayValue(arr, cap, N)
       {

           // Stores the sum of array element
           let sumVals = 0;
           for (let i = 0; i < N; i++) {
               sumVals += arr[i];
           }

           // Stores the maximum element in cap[]
           let maxCapacity = 0;

           // Iterate to find maximum element
           for (let i = 0; i < N; i++) {
               maxCapacity = Math.max(cap[i], maxCapacity);
           }

           // Return the resultant maximum value
           return Math.min(maxCapacity, sumVals);
       }

       // Driver Code
       let arr = [2, 3];
       let cap = [5, 6];
       let N = arr.length

       document.write(maxShiftArrayValue(arr, cap, N));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
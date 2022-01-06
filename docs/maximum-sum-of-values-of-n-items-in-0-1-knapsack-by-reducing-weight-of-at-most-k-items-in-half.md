# 将最多 K 件物品重量减半，0-1 背包中 N 件物品的最大值之和

> 原文:[https://www . geeksforgeeks . org/0-1-1-背包中 n 件物品的最大价值总和减去最多 k 件物品的一半重量/](https://www.geeksforgeeks.org/maximum-sum-of-values-of-n-items-in-0-1-knapsack-by-reducing-weight-of-at-most-k-items-in-half/)

给定 **N** 物品的**重量**和**数值**以及背包的容量 **W** 。同样假设最多 **K** 件的重量可以改为原来重量的一半。任务是找出 **N** 个物品的最大值之和，使得背包中物品的重量之和不超过给定的容量 **W** 。

**示例:**

> **输入:** W = 4，K = 1，值= [17，20，10，15]，重量= [4，2，7，5]
> **输出:** 37
> **说明:**以最优方式将最多 **K** 个物品的重量改为重量的一半，以获得最大值。将第一个项目的重量减少一半，加上第二个项目的重量，得到的值总和为 37，这是最大值
> 
> **输入:** W = 8，K = 2，值= [17，20，10，15]，权重= [4，2，7，5]
> **输出:** 53
> **说明:**更改最后一个项目和第一个项目的权重，并将第二个项目的权重相加，项目的总值将为 53。

**方法:**给定的问题是 [0 1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)问题的变异。标志表示重量减半的项目数量。每次递归调用时，计算并返回以下情况的最大值:

*   基本情况:如果索引超过值的长度，则返回零
*   如果标志等于 **K，**最大值为则考虑 2 种情况:
    *   如果物品重量不超过剩余重量，则包括全重物品
    *   跳过该项目
*   如果标志小于 **K，**最大值为则考虑 3 种情况:
    *   如果物品重量不超过剩余重量，则包括全重物品
    *   如果物品的一半重量没有超过剩余重量，则包括一半重量的物品
    *   跳过该项目

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to find the maximum  value

int maximum(int value[],
            int weight[], int weight1,
            int flag, int K, int index, int val_len)
{

    // base condition
    if (index >= val_len)
    {

        return 0;
    }

    // K elements already reduced
    // to half of their weight
    if (flag == K)
    {

        // Dont include item
        int skip = maximum(value,
                           weight, weight1,
                           flag, K, index + 1, val_len);

        int full = 0;

        // If weight of the item is
        // less than  or equal to the
        // remaining weight then include
        // the item
        if (weight[index] <= weight1)
        {

            full = value[index] + maximum(
                                      value, weight,
                                      weight1 - weight[index], flag,
                                      K, index + 1, val_len);
        }

        // Return the maximum  of
        // both cases
        return max(full, skip);
    }

    // If the weight reduction to half
    // is possible
    else
    {

        // Skip the item
        int skip = maximum(
            value, weight,
            weight1, flag,
            K, index + 1, val_len);

        int full = 0;
        int half = 0;

        // Include item with full weight
        // if weight of the item is less
        // than the remaining weight
        if (weight[index] <= weight1)
        {

            full = value[index] + maximum(
                                      value, weight,
                                      weight1 - weight[index],
                                      flag, K, index + 1, val_len);
        }

        // Include item with half weight
        // if half weight of the item is
        // less than the remaining weight
        if (weight[index] / 2 <= weight1)
        {

            half = value[index] + maximum(
                                      value, weight,
                                      weight1 - weight[index] / 2,
                                      flag, K, index + 1, val_len);
        }

        // Return the maximum of all 3 cases
        return max(full,
                   max(skip, half));
    }
}
int main()
{

    int value[] = {17, 20, 10, 15};
    int weight[] = {4, 2, 7, 5};
    int K = 1;
    int W = 4;
    int val_len = sizeof(value) / sizeof(value[0]);
    cout << (maximum(value, weight, W,
                     0, K, 0, val_len));

    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the maximum  value
    static int maximum(int value[],
                       int weight[], int weight1,
                       int flag, int K, int index)
    {

        // base condition
        if (index >= value.length) {

            return 0;
        }

        // K elements already reduced
        // to half of their weight
        if (flag == K) {

            // Dont include item
            int skip = maximum(value,
                               weight, weight1,
                               flag, K, index + 1);

            int full = 0;

            // If weight of the item is
            // less than  or equal to the
            // remaining weight then include
            // the item
            if (weight[index] <= weight1) {

                full = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index], flag,
                             K, index + 1);
            }

            // Return the maximum  of
            // both cases
            return Math.max(full, skip);
        }

        // If the weight reduction to half
        // is possible
        else {

            // Skip the item
            int skip = maximum(
                value, weight,
                weight1, flag,
                K, index + 1);

            int full = 0;
            int half = 0;

            // Include item with full weight
            // if weight of the item is less
            // than the remaining weight
            if (weight[index] <= weight1) {

                full = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index],
                             flag, K, index + 1);
            }

            // Include item with half weight
            // if half weight of the item is
            // less than the remaining weight
            if (weight[index] / 2 <= weight1) {

                half = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index] / 2,
                             flag, K, index + 1);
            }

            // Return the maximum of all 3 cases
            return Math.max(full,
                            Math.max(skip, half));
        }
    }

    public static void main(String[] args)
        throws Exception
    {

        int value[] = { 17, 20, 10, 15 };
        int weight[] = { 4, 2, 7, 5 };
        int K = 1;
        int W = 4;
        System.out.println(
            maximum(value, weight, W,
                    0, K, 0));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum  value
def maximum(value,
            weight, weight1,
            flag, K, index, val_len) :

    # base condition
    if (index >= val_len) :

        return 0

    # K elements already reduced
    # to half of their weight
    if (flag == K) :

        # Dont include item
        skip = maximum(value,
                           weight, weight1,
                           flag, K, index + 1, val_len)

        full = 0

        # If weight of the item is
        # less than  or equal to the
        # remaining weight then include
        # the item
        if (weight[index] <= weight1) :

            full = value[index] + maximum(
                                      value, weight,
                                      weight1 - weight[index], flag,
                                      K, index + 1, val_len)

        # Return the maximum  of
        # both cases
        return max(full, skip)

    # If the weight reduction to half
    # is possible
    else :

        # Skip the item
        skip = maximum(
            value, weight,
            weight1, flag,
            K, index + 1, val_len)

        full = 0
        half = 0

        # Include item with full weight
        # if weight of the item is less
        # than the remaining weight
        if (weight[index] <= weight1) :

            full = value[index] + maximum(
                                      value, weight,
                                      weight1 - weight[index],
                                      flag, K, index + 1, val_len)

        # Include item with half weight
        # if half weight of the item is
        # less than the remaining weight
        if (weight[index] / 2 <= weight1) :

            half = value[index] + maximum(
                                      value, weight,
                                      weight1 - weight[index] / 2,
                                      flag, K, index + 1, val_len)

        # Return the maximum of all 3 cases
        return max(full,
                   max(skip, half))

# Driver Code

value =  [ 17, 20, 10, 15 ]
weight = [ 4, 2, 7, 5 ]
K = 1
W = 4
val_len = len(value)
print(maximum(value, weight, W,
                     0, K, 0, val_len))

# This code is contributed by sanjoy_62.
```

## C#

```
// C# implementation for the above approach
using System;

public class GFG {

    // Function to find the maximum  value
    static int maximum(int []value,
                       int []weight, int weight1,
                       int flag, int K, int index)
    {

        // base condition
        if (index >= value.Length) {

            return 0;
        }

        // K elements already reduced
        // to half of their weight
        if (flag == K) {

            // Dont include item
            int skip = maximum(value,
                               weight, weight1,
                               flag, K, index + 1);

            int full = 0;

            // If weight of the item is
            // less than  or equal to the
            // remaining weight then include
            // the item
            if (weight[index] <= weight1) {

                full = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index], flag,
                             K, index + 1);
            }

            // Return the maximum  of
            // both cases
            return Math.Max(full, skip);
        }

        // If the weight reduction to half
        // is possible
        else {

            // Skip the item
            int skip = maximum(
                value, weight,
                weight1, flag,
                K, index + 1);

            int full = 0;
            int half = 0;

            // Include item with full weight
            // if weight of the item is less
            // than the remaining weight
            if (weight[index] <= weight1) {

                full = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index],
                             flag, K, index + 1);
            }

            // Include item with half weight
            // if half weight of the item is
            // less than the remaining weight
            if (weight[index] / 2 <= weight1) {

                half = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index] / 2,
                             flag, K, index + 1);
            }

            // Return the maximum of all 3 cases
            return Math.Max(full,
                            Math.Max(skip, half));
        }
    }

  // Driver code
    public static void Main(String[] args)
    {

        int []value = { 17, 20, 10, 15 };
        int []weight = { 4, 2, 7, 5 };
        int K = 1;
        int W = 4;
        Console.WriteLine(
            maximum(value, weight, W,
                    0, K, 0));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript implementation for the above approach  
// Function to find the maximum  value
    function maximum(value,
                       weight , weight1,
                       flag , K , index)
    {

        // base condition
        if (index >= value.length) {

            return 0;
        }

        // K elements already reduced
        // to half of their weight
        if (flag == K) {

            // Dont include item
            var skip = maximum(value,
                               weight, weight1,
                               flag, K, index + 1);

            var full = 0;

            // If weight of the item is
            // less than  or equal to the
            // remaining weight then include
            // the item
            if (weight[index] <= weight1) {

                full = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index], flag,
                             K, index + 1);
            }

            // Return the maximum  of
            // both cases
            return Math.max(full, skip);
        }

        // If the weight reduction to half
        // is possible
        else {

            // Skip the item
            var skip = maximum(
                value, weight,
                weight1, flag,
                K, index + 1);

            var full = 0;
            var half = 0;

            // Include item with full weight
            // if weight of the item is less
            // than the remaining weight
            if (weight[index] <= weight1) {

                full = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index],
                             flag, K, index + 1);
            }

            // Include item with half weight
            // if half weight of the item is
            // less than the remaining weight
            if (weight[index] / 2 <= weight1) {

                half = value[index]
                       + maximum(
                             value, weight,
                             weight1 - weight[index] / 2,
                             flag, K, index + 1);
            }

            // Return the maximum of all 3 cases
            return Math.max(full,
                            Math.max(skip, half));
        }
    }

// Driver code
var value = [ 17, 20, 10, 15 ];
var weight = [ 4, 2, 7, 5 ];
var K = 1;
var W = 4;
document.write(
    maximum(value, weight, W,
            0, K, 0));

// This code is contributed by Princi Singh
</script>
```

**Output**

```
37
```

**时间复杂度:**o(3^n)
T3】辅助空间: O(N)
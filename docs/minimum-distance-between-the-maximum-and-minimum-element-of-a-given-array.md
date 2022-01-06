# 给定数组的最大和最小元素之间的最小距离

> 原文:[https://www . geesforgeks . org/给定数组的最大元素和最小元素之间的最小距离/](https://www.geeksforgeeks.org/minimum-distance-between-the-maximum-and-minimum-element-of-a-given-array/)

给定一个由 **N** 元素组成的数组 **A[]** ，任务是找到数组的[最小值](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)和[最大值元素之间的最小距离。
**示例:**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

> **输入:** arr[] = {3，2，1，2，1，4，5，8，6，7，8，2}
> **输出:** 3
> **解释:**
> 最小元素(= 1)出现在指数{2，4}
> 最大元素(= 8)出现在指数{7，10}上。
> 1 和 8 的出现之间的最小距离是 7–4 = 3
> **输入:** arr[] = {1，3，69}
> **输出:** 2
> **解释:**
> 最小元素(= 1)出现在索引 0 处。
> 最大元素(= 69)出现在索引 2 处。
> 因此，它们之间的最小距离为 2。

**天真的方法:**
解决这个问题最简单的方法如下:

*   找出数组的最小和最大元素。
*   遍历数组，对于每个出现的最大元素，计算它与数组中所有出现的最小元素的距离，并更新最小距离。
*   完成数组遍历后，打印所有获得的最小距离。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效途径:**
按照以下步骤优化上述途径:

*   遍历数组以找到最小和最大元素。
*   初始化两个变量 **min_index** 和 **max_index** 分别存储数组最小和最大元素的索引。用-1 初始化它们。
*   遍历数组。如果在任何时刻 **min_index** 和 **max_index** 都不等于-1，即两者都存储了有效的索引，则计算它们之间的差异。
*   将该差值与最小距离(例如， **min_dist** )进行比较，并相应地更新 **min_dist** 。
*   最后，打印完成数组遍历后得到的 **min_dist** 的最终值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// distance between the minimum
// and the maximum element
int minDistance(int a[], int n)
{
    // Stores the minimum and maximum
    // array element
    int maximum = -1, minimum = INT_MAX;

    // Stores the most recently traversed
    // indices of the minimum and the
    // maximum element
    int min_index = -1, max_index = -1;

    // Stores the minimum distance
    // between the minimum and the
    // maximium
    int min_dist = n + 1;

    // Find the maximum and
    // the minimum element
    // from the given array
    for (int i = 0; i < n; i++) {

        if (a[i] > maximum)
            maximum = a[i];

        if (a[i] < minimum)
            minimum = a[i];
    }

    // Find the minimum distance
    for (int i = 0; i < n; i++) {

        // Check if current element
        // is equal to minimum
        if (a[i] == minimum)
            min_index = i;

        // Check if current element
        // is equal to maximum
        if (a[i] == maximum)
            max_index = i;

        // If both the minimum and the
        // maximum element has
        // occurred at least once
        if (min_index != -1
            && max_index != -1)

            // Update the minimum distance
            min_dist
                = min(min_dist,
                      abs(min_index
                          - max_index));
    }

    // Return the answer
    return min_dist;
}

// Driver Code
int main()
{
    int a[] = { 3, 2, 1, 2, 1, 4,
                5, 8, 6, 7, 8, 2 };
    int n = sizeof a / sizeof a[0];
    cout << minDistance(a, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG {

    // Function to find the minimum
    // distance between the minimum
    // and the maximum element
    public static int minDistance(int a[], int n)
    {

        // Stores the minimum and maximum
        // array element
        int max = -1, min = Integer.MAX_VALUE;

        // Stores the most recently traversed
        // indices of the minimum and the
        // maximum element
        int min_index = -1, max_index = -1;

        // Stores the minimum distance
        // between the minimum and the
        // maximium
        int min_dist = n + 1;

        // Find the maximum and
        // the minimum element
        // from the given array
        for (int i = 0; i < n; i++) {
            if (a[i] > max)
                max = a[i];
            if (a[i] < min)
                min = a[i];
        }

        // Find the minimum distance
        for (int i = 0; i < n; i++) {

            // Check if current element
            // is equal to minimum
            if (a[i] == min)
                min_index = i;

            // Check if current element
            // is equal to maximum
            if (a[i] == max)
                max_index = i;

            // If both the minimum and the
            // maximum element has
            // occurred at least once
            if (min_index != -1
                && max_index != -1)
                min_dist
                    = Math.min(min_dist,
                               Math.abs(min_index
                                        - max_index));
        }
        return min_dist;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 12;
        int a[] = { 3, 2, 1, 2, 1, 4,
                    5, 8, 6, 7, 8, 2 };
        System.out.println(minDistance(a, n));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement the
# above approach
import sys

# Function to find the minimum
# distance between the minimum
# and the maximum element
def minDistance(a, n):

    # Stores the minimum and maximum
    # array element
    maximum = -1
    minimum = sys.maxsize

    # Stores the most recently traversed
    # indices of the minimum and the
    # maximum element
    min_index = -1
    max_index = -1

    # Stores the minimum distance
    # between the minimum and the
    # maximium
    min_dist = n + 1

    # Find the maximum and
    # the minimum element
    # from the given array
    for i in range (n):
        if (a[i] > maximum):
            maximum = a[i]

        if (a[i] < minimum):
            minimum = a[i]

    # Find the minimum distance
    for i in range (n):

        # Check if current element
        # is equal to minimum
        if (a[i] == minimum):
            min_index = i

        # Check if current element
        # is equal to maximum
        if (a[i] == maximum):
            max_index = i

        # If both the minimum and the
        # maximum element has
        # occurred at least once
        if (min_index != -1 and
            max_index != -1):

            # Update the minimum distance
            min_dist = (min(min_dist,
                        abs(min_index -
                            max_index)))

    # Return the answer
    return min_dist

# Driver Code
if __name__ == "__main__":

    a = [3, 2, 1, 2, 1, 4,
         5, 8, 6, 7, 8, 2]
    n = len(a)
    print (minDistance(a, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the minimum
// distance between the minimum
// and the maximum element
static int minDistance(int []a, int n)
{

    // Stores the minimum and maximum
    // array element
    int max = -1, min = Int32.MaxValue;

    // Stores the most recently traversed
    // indices of the minimum and the
    // maximum element
    int min_index = -1, max_index = -1;

    // Stores the minimum distance
    // between the minimum and the
    // maximium
    int min_dist = n + 1;

    // Find the maximum and
    // the minimum element
    // from the given array
    for(int i = 0; i < n; i++)
    {
        if (a[i] > max)
            max = a[i];
        if (a[i] < min)
            min = a[i];
    }

    // Find the minimum distance
    for(int i = 0; i < n; i++)
    {
        // Check if current element
        // is equal to minimum
        if (a[i] == min)
            min_index = i;

        // Check if current element
        // is equal to maximum
        if (a[i] == max)
            max_index = i;

        // If both the minimum and the
        // maximum element has
        // occurred at least once
        if (min_index != -1 && max_index != -1)
            min_dist = Math.Min(min_dist,
                                Math.Abs(
                                min_index -
                                max_index));
    }
    return min_dist;
}

// Driver Code
public static void Main()
{
    int n = 12;
    int []a = { 3, 2, 1, 2, 1, 4,
                5, 8, 6, 7, 8, 2 };

    Console.WriteLine(minDistance(a, n));
}
}

// This code is contributed by piyush3010
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to find the minimum
    // distance between the minimum
    // and the maximum element
   function minDistance(a, n)
    {

        // Stores the minimum and maximum
        // array element
        let max = -1, min = Number.MAX_VALUE;

        // Stores the most recently traversed
        // indices of the minimum and the
        // maximum element
        let min_index = -1, max_index = -1;

        // Stores the minimum distance
        // between the minimum and the
        // maximium
        let min_dist = n + 1;

        // Find the maximum and
        // the minimum element
        // from the given array
        for (let i = 0; i < n; i++) {
            if (a[i] > max)
                max = a[i];
            if (a[i] < min)
                min = a[i];
        }

        // Find the minimum distance
        for (let i = 0; i < n; i++) {

            // Check if current element
            // is equal to minimum
            if (a[i] == min)
                min_index = i;

            // Check if current element
            // is equal to maximum
            if (a[i] == max)
                max_index = i;

            // If both the minimum and the
            // maximum element has
            // occurred at least once
            if (min_index != -1
                && max_index != -1)
                min_dist
                    = Math.min(min_dist,
                               Math.abs(min_index
                                        - max_index));
        }
        return min_dist;
    }

    // Driver Code

        let n = 12;
        let a = [ 3, 2, 1, 2, 1, 4,
                    5, 8, 6, 7, 8, 2 ];
        document.write(minDistance(a, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
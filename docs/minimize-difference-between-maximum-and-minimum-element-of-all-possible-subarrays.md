# 最小化所有可能子阵列的最大和最小元素之间的差异

> 原文:[https://www . geesforgeks . org/minimum-所有可能子阵的最大和最小元素之差/](https://www.geeksforgeeks.org/minimize-difference-between-maximum-and-minimum-element-of-all-possible-subarrays/)

给定一个大小为 **N、**的数组 **arr[ ]** ，任务是找出 arr[ ]的所有可能大小的子数组的**最大值**和**最小值**元素之间的**最小值**差。

**示例:**

> **输入:** arr[] = { 5，14，7，10 }
> **输出:** 3
> **解释:** {7，10 }是 max 元素= 10 & min 元素= 7 的子阵列，它们的差= 10–7 = 3
> 
> **输入:** arr[] = { 2，6，15，7，6 }
> **输出:** 1
> **说明:** {7，6 }是 max 元素= 7 & min 元素= 6 的子阵列，它们的差= 7–6 = 1

**逼近**:简单的思路就是用**两个**循环，检查每一个子阵的**，最大和最小元素的最小差。记录差异并返回**最小**可能的差异。这种方法的时间复杂度是二次的。**

**高效方法**:想法是利用这样一个事实，即我们可以通过只迭代大小为**两个**的子阵列来获得最小差异。
假设我们的子阵列中有两个元素。让最大和最小元素之差为 **x** 。现在，如果我们包括从**右侧**或**左侧**到我们的子阵列的元素，最大元素或最小元素可能会更新。这个变化最终会使我们的差异 **x** **增加，**随着最大或最小元素的更新。

按照以下步骤实施上述方法:

*   迭代数组并跟踪最小相邻差
*   打印此最小差异作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the min difference
// between max and min element of all
// possible subarrays
int getMinDifference(int arr[], int n)
{
    // To store the adjacent difference
    int diff;

    // To compare with min difference
    int mn = INT_MAX;

    for (int i = 1; i < n; i++) {

        // Storing adjacent difference
        diff = abs(arr[i] - arr[i - 1]);

        // Updating the min difference
        mn = min(diff, mn);
    }

    // Returning min difference
    return mn;
}

// Driver code
int main()
{

    int arr[] = { 2, 6, 15, 7, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getMinDifference(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to get the min difference
// between max and min element of all
// possible subarrays
static int getMinDifference(int []arr, int n)
{
    // To store the adjacent difference
    int diff = 0;

    // To compare with min difference
    int mn = Integer.MAX_VALUE;

    for (int i = 1; i < n; i++) {

        // Storing adjacent difference
        diff = Math.abs(arr[i] - arr[i - 1]);

        // Updating the min difference
        mn = Math.min(diff, mn);
    }

    // Returning min difference
    return mn;
}

// Driver code
public static void main (String[] args)
{

    int []arr = {2, 6, 15, 7, 6 };
    int N = arr.length;
    System.out.println(getMinDifference(arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys,math

# Function to get the min difference
# between max and min element of all
# possible subarrays
def getMinDifference(arr, n) :

    INT_MAX = sys.maxsize;

    # To compare with min difference
    mn = INT_MAX;

    for i in range(1, n):

        # Storing adjacent difference
        diff = abs(arr[i] - arr[i - 1]);

        # Updating the min difference
        mn = min(diff, mn);

    # Returning min difference
    return mn;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 6, 15, 7, 6 ];
    N = len(arr);
    print(getMinDifference(arr, N));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to get the min difference
// between max and min element of all
// possible subarrays
static int getMinDifference(int []arr, int n)
{
    // To store the adjacent difference
    int diff = 0;

    // To compare with min difference
    int mn = Int32.MaxValue;

    for (int i = 1; i < n; i++) {

        // Storing adjacent difference
        diff = Math.Abs(arr[i] - arr[i - 1]);

        // Updating the min difference
        mn = Math.Min(diff, mn);
    }

    // Returning min difference
    return mn;
}

// Driver code
public static void Main()
{

    int []arr = {2, 6, 15, 7, 6 };
    int N = arr.Length;
    Console.Write(getMinDifference(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to get the min difference
        // between max and min element of all
        // possible subarrays
        function getMinDifference(arr, n) {
            // To store the adjacent difference
            let diff;

            // To compare with min difference
            let mn = Number.MAX_VALUE;

            for (let i = 1; i < n; i++) {

                // Storing adjacent difference
                diff = Math.abs(arr[i] - arr[i - 1]);

                // Updating the min difference
                mn = Math.min(diff, mn);
            }

            // Returning min difference
            return mn;
        }

        // Driver code

        let arr = [2, 6, 15, 7, 6];
        let N = arr.length;
        document.write(getMinDifference(arr, N));

// This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
1
```

***时间复杂度*** **:** O(N)，N 为元素个数
***辅助空间*** **:** O(1)
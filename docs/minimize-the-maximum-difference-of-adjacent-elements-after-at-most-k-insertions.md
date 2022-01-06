# 最多 K 次插入后最小化相邻元素的最大差异

> 原文:[https://www . geeksforgeeks . org/最小化最多 k 次插入后相邻元素的最大差异/](https://www.geeksforgeeks.org/minimize-the-maximum-difference-of-adjacent-elements-after-at-most-k-insertions/)

给定一个由 **N** 个元素组成的数组，任务是通过在数组中最多插入 **K** 个元素来最小化相邻元素的最大差异。
**例:**

> **输入:** arr = [2，6，8] K = 1
> **输出:** 2
> **解释:**
> 在 2 和 6 之间插入 4 后，数组变成[2，4，6，8]。在这种情况下，任何相邻元素之间的最大差值为 2，这是可以达到的最小值。
> **输入:** arr = [3，12] K = 2
> **输出:** 3
> **解释:**
> 在 3 和 12 之间插入 6 和 9 后，数组变成[3，6，9，12]。在这种情况下，任何相邻元素之间的最大差值为 3，这是可以达到的最小值。

**进场:**为了解决这个问题，我们采用以下[二分搜索法](https://www.geeksforgeeks.org/binary-search/)为主的进场:

1.  找出数组中任意两个相邻元素之间的最大差值，并将其存储在一个变量中，比如**最差**。
2.  从**最佳**(最初为 1)到**最差**进行搜索，对于每个**中间**值，找到所需的插入次数。
3.  每当**中**的特定值的插入次数大于 **K** 时，在**【中+ 1，最差】**之间搜索，即高半部分。否则，在**【最佳，中间 1】**之间搜索，也就是下半部分，检查最大差异是否可以通过最多 K 次插入进一步最小化。
4.  循环终止后的最终**最差**值给出了答案。

下面的代码是上述方法的实现:

## C++

```
// C++ Program to find the minimum of maximum
// differerence between adjacent elements
// after at most K insertions

#include <bits/stdc++.h>
using namespace std;

int minMaxDiff(int arr[], int n, int k)
{
    int max_adj_dif = INT_MIN;
    // Calculate the maximum
    // adjacent difference
    for (int i = 0; i < n - 1; i++)
        max_adj_dif
            = max(max_adj_dif,
                  abs(arr[i] - arr[i + 1]));

    // If the maximum adjacent
    // difference is already zero
    if (max_adj_dif == 0)
        return 0;

    // best and worst specifies
    // range of the maximum
    // adjacent difference
    int best = 1;
    int worst = max_adj_dif;
    int mid, required;

    while (best < worst) {

        mid = (best + worst) / 2;

        // To store the no of insertions
        // required for respective
        // values of mid
        required = 0;

        for (int i = 0; i < n - 1; i++) {

            required += (abs(arr[i]
                             - arr[i + 1])
                         - 1)
                        / mid;
        }

        // If the number of insertions
        // required exceeds K
        if (required > k)
            best = mid + 1;

        // Otherwise
        else
            worst = mid;
    }

    return worst;
}

// Driver code
int main()
{
    int arr[] = { 3, 12, 25, 50 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 7;

    cout << minMaxDiff(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// of maximum difference between
// adjacent elements after at most
// K insertions
import java.util.*;

class GFG{

static int minMaxDiff(int arr[], int n, int k)
{
    int max_adj_dif = Integer.MIN_VALUE;

    // Calculate the maximum
    // adjacent difference
    for(int i = 0; i < n - 1; i++)
        max_adj_dif = Math.max(max_adj_dif,
                      Math.abs(arr[i] -
                               arr[i + 1]));

    // If the maximum adjacent
    // difference is already zero
    if (max_adj_dif == 0)
        return 0;

    // best and worst specifies
    // range of the maximum
    // adjacent difference
    int best = 1;
    int worst = max_adj_dif;
    int mid, required;

    while (best < worst)
    {
        mid = (best + worst) / 2;

        // To store the no of insertions
        // required for respective
        // values of mid
        required = 0;

        for(int i = 0; i < n - 1; i++)
        {
            required += (Math.abs(arr[i] -
                                  arr[i + 1]) -
                                     1) / mid;
        }

        // If the number of insertions
        // required exceeds K
        if (required > k)
            best = mid + 1;

        // Otherwise
        else
            worst = mid;
    }
    return worst;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 12, 25, 50 };
    int n = arr.length;
    int k = 7;

    System.out.println(minMaxDiff(arr, n, k));
}
}

// This code is contributed by ANKITKUMAR34
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# of maximum difference between
# adjacent elements after at most
# K insertions
def minMaxDiff(arr, n, k):

    max_adj_dif = float('-inf');

    # Calculate the maximum
    # adjacent difference
    for i in range(n - 1):
        max_adj_dif = max(max_adj_dif,
                          abs(arr[i] -
                              arr[i + 1]));

    # If the maximum adjacent
    # difference is already zero
    if (max_adj_dif == 0):
        return 0;

    # best and worst specifies
    # range of the maximum
    # adjacent difference
    best = 1;
    worst = max_adj_dif;

    while (best < worst):
        mid = (best + worst) // 2;

        # To store the no of insertions
        # required for respective
        # values of mid
        required = 0

        for i in range(n - 1):
            required += (abs(arr[i] -
                             arr[i + 1]) - 1) // mid

        # If the number of insertions
        # required exceeds K
        if (required > k):
            best = mid + 1;

        # Otherwise
        else:
            worst = mid

    return worst

# Driver code
arr = [ 3, 12, 25, 50 ]
n = len(arr)
k = 7

print(minMaxDiff(arr, n, k))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# program to find the minimum
// of maximum difference between
// adjacent elements after at most
// K insertions
using System;
class GFG{

static int minMaxDiff(int []arr, int n, int k)
{
    int max_adj_dif = int.MinValue;

    // Calculate the maximum
    // adjacent difference
    for(int i = 0; i < n - 1; i++)
        max_adj_dif = Math.Max(max_adj_dif,
                      Math.Abs(arr[i] -
                               arr[i + 1]));

    // If the maximum adjacent
    // difference is already zero
    if (max_adj_dif == 0)
        return 0;

    // best and worst specifies
    // range of the maximum
    // adjacent difference
    int best = 1;
    int worst = max_adj_dif;
    int mid, required;

    while (best < worst)
    {
        mid = (best + worst) / 2;

        // To store the no of insertions
        // required for respective
        // values of mid
        required = 0;

        for(int i = 0; i < n - 1; i++)
        {
            required += (Math.Abs(arr[i] -
                                  arr[i + 1]) -
                                      1) / mid;
        }

        // If the number of insertions
        // required exceeds K
        if (required > k)
            best = mid + 1;

        // Otherwise
        else
            worst = mid;
    }
    return worst;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 12, 25, 50 };
    int n = arr.Length;
    int k = 7;

    Console.WriteLine(minMaxDiff(arr, n, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript Program to find the minimum of maximum
// differerence between adjacent elements
// after at most K insertions

function minMaxDiff(arr, n, k)
{
    var max_adj_dif = -1000000000;
    // Calculate the maximum
    // adjacent difference
    for (var i = 0; i < n - 1; i++)
        max_adj_dif
            = Math.max(max_adj_dif,
                  Math.abs(arr[i] - arr[i + 1]));

    // If the maximum adjacent
    // difference is already zero
    if (max_adj_dif == 0)
        return 0;

    // best and worst specifies
    // range of the maximum
    // adjacent difference
    var best = 1;
    var worst = max_adj_dif;
    var mid, required;

    while (best < worst) {

        mid = (best + worst) / 2;

        // To store the no of insertions
        // required for respective
        // values of mid
        required = 0;

        for (var i = 0; i < n - 1; i++) {

            required += parseInt((Math.abs(arr[i]
                             - arr[i + 1])
                         - 1)
                        / mid);
        }

        // If the number of insertions
        // required exceeds K
        if (required > k)
            best = mid + 1;

        // Otherwise
        else
            worst = mid;
    }

    return worst;
}

// Driver code
var arr = [ 3, 12, 25, 50 ];
var n = arr.length;
var k = 7;
document.write( minMaxDiff(arr, n, k));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(n * log n)

**辅助空间:** O(1)
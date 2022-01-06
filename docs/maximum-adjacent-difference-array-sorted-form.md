# 排序形式的数组中的最大相邻差

> 原文:[https://www . geesforgeks . org/maximum-相邻差-数组-排序-表单/](https://www.geeksforgeeks.org/maximum-adjacent-difference-array-sorted-form/)

给定一个数组，在其排序形式中找出它的两个连续元素之间的最大差异。
**例:**

```
Input: arr[] = {1, 10, 5}
Output: 5
Sorted array would be {1, 5, 10} and
maximum adjacent difference would be 
10 - 5 = 5

Input: arr[] = {2, 4, 8, 11}
Output: 4
```

**天真解决方案:**

首先对数组进行排序，然后遍历它并跟踪相邻元素之间的最大差异。
该方法的时间复杂度为 O(nlogn)。

**高效解决方案:**
这个**解决方案**是基于[鸽子洞排序](https://www.geeksforgeeks.org/pigeonhole-sort/)的思路。不需要对数组进行排序，只需要填充桶并跟踪每个桶的最大值和最小值。如果发现一个空桶，最大间隙将是前一桶 **中的**最大值–下一桶** **中的最小值之差。****

因为我们几乎要对这些进行排序，所以我们可以有最大的差距。同样对于任何 ith 元素，(arr[i]-min _ value)/(max _ value-min _ value)的值随着 arr[I]的不断增加而不断增加，并且该值始终在 0 到 1 之间变化。因为我们希望将排序后的结果放入大小为 n 的桶中。我们将该值乘以(n-1)，从而得到一个变量**δ=(max _ value–min _ value)/(n-1)**。现在在 maxBucket 或 minBucket 中，任何索引 I 之前的任何索引 j 处的所有值都将始终小于索引 I 处的值，minBucket[j] < minBucket[i]为 j < i。可能两个不同的 arr[i]，可能具有相同的 **(arr[i]-min_value)/delta** 值，因此我们正在制作 2 个不同的 buckets maxBucket 和 minBucket。

由于我们已经找到了**连续值**之间的最大差异，我们必须将直到上一个索引的最大可能值视为 prev_val，而当前索引 I 的最小桶[i]，ans 将是 ans 和最小桶[i]-prev_val 的最大值。

让我们用这种方法来解决上面的例子。

**工作示例:**

> **输入** : arr[] = {1，10，5}
> 
> **输出:5**
> 
> **步骤 1** :查找最大值和最小值
> 
> max_val = 10，min_val = 1
> 
> **第二步**:计算差值
> 
> 差值=(max _ val-min _ val)/(n-1)
> 
> δ=(10-1)/(3-1)= 4.5
> 
> **步骤 3** :初始化桶，maxBucket={INT_MIN}，minBucket={INT_MAX}
> 
> **第四步**:对于任何索引 I，计算桶中的索引 arr[i]并在桶中更新，
> 
> in = (arr[i]-min_val)/delta
> 
> maxBucket[in]= max(maxBucket[in]，arr[i])
> 
> 最小桶[in]=最小(最小桶[in]，arr[i])
> 
> 对于 arr 中的所有索引，值为=> 0，2，0
> 
> max bucket =[5.int _ min，10]
> 
> minBucket=[1，INT_MAX，10]
> 
> **第五步**:因此 ans 是 minBucket[i]的最大值(上一个索引的最大值)
> 
> 在这种情况下，对于 i=2: max_gap = max(max_gap，minBucket[2]–max(maxBucket[1]，maxBucket[0])
> 
> max_gap = 10-5=5
> 
> 这只是为了展示概念，所有其他基本验证都在主代码中。

以下是上述方法的代码:

## C++

```
// CPP program to find maximum adjacent difference
// between two adjacent after sorting.
#include <bits/stdc++.h>
using namespace std;

int maxSortedAdjacentDiff(int* arr, int n)
{
    // Find maximum and minimum in arr[]
    int maxVal = arr[0], minVal = arr[0];
    for (int i = 1; i < n; i++) {
        maxVal = max(maxVal, arr[i]);
        minVal = min(minVal, arr[i]);
    }

    // Arrays to store maximum and minimum values
    // in n-1 buckets of differences.
    int maxBucket[n - 1];
    int minBucket[n - 1];
    fill_n(maxBucket, n - 1, INT_MIN);
    fill_n(minBucket, n - 1, INT_MAX);

    // Expected gap for every bucket.
    float delta = (float)(maxVal - minVal) / (float)(n - 1);

    // Traversing through array elements and
    // filling in appropriate bucket if bucket
    // is empty. Else updating bucket values.
    for (int i = 0; i < n; i++) {
        if (arr[i] == maxVal || arr[i] == minVal)
            continue;

        // Finding index of bucket.
        int index = (float)(floor(arr[i] - minVal) / delta);

        maxBucket[index] = max(maxBucket[index], arr[i]);
           minBucket[index] = min(minBucket[index], arr[i]);
    }

    // Finding maximum difference between maximum value
    // of previous bucket minus minimum of current bucket.
    int prev_val = minVal;
    int max_gap = 0;
    for (int i = 0; i < n - 1; i++) {
        if (minBucket[i] == INT_MAX)
            continue;
        max_gap = max(max_gap, minBucket[i] - prev_val);
        prev_val = maxBucket[i];
    }
    max_gap = max(max_gap, maxVal - prev_val);

    return max_gap;
}

int main()
{
    int arr[] = { 1, 10, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxSortedAdjacentDiff(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

// Java program to find maximum adjacent difference
// between two adjacent after sorting.
class GFG {

    static int maxSortedAdjacentDiff(int[] arr, int n)
    {
        // Find maximum and minimum in arr[]
        int maxVal = arr[0];
        int minVal = arr[0];
        for (int i = 1; i < n; i++) {
            maxVal = Math.max(maxVal, arr[i]);
            minVal = Math.min(minVal, arr[i]);
        }

        // Arrays to store maximum and minimum values
        // in n-1 buckets of differences.
        int maxBucket[] = new int[n - 1];
        int minBucket[] = new int[n - 1];
        Arrays.fill(maxBucket, 0, n - 1, Integer.MIN_VALUE);
        Arrays.fill(minBucket, 0, n - 1, Integer.MAX_VALUE);

        // Expected gap for every bucket.
        float delta
            = (float)(maxVal - minVal) / (float)(n - 1);

        // Traversing through array elements and
        // filling in appropriate bucket if bucket
        // is empty. Else updating bucket values.
        for (int i = 0; i < n; i++) {
            if (arr[i] == maxVal || arr[i] == minVal) {
                continue;
            }

            // Finding index of bucket.
            int index = (int)(Math.round((arr[i] - minVal)
                                         / delta));

            // Filling/Updating maximum value of bucket
            if (maxBucket[index] == Integer.MIN_VALUE) {
                maxBucket[index] = arr[i];
            }
            else {
                maxBucket[index]
                    = Math.max(maxBucket[index], arr[i]);
            }

            // Filling/Updating minimum value of bucket
            if (minBucket[index] == Integer.MAX_VALUE) {
                minBucket[index] = arr[i];
            }
            else {
                minBucket[index]
                    = Math.min(minBucket[index], arr[i]);
            }
        }

        // Finding maximum difference between maximum value
        // of previous bucket minus minimum of current
        // bucket.
        int prev_val = minVal;
        int max_gap = 0;
        for (int i = 0; i < n - 1; i++) {
            if (minBucket[i] == Integer.MAX_VALUE) {
                continue;
            }
            max_gap = Math.max(max_gap,
                               minBucket[i] - prev_val);
            prev_val = maxBucket[i];
        }
        max_gap = Math.max(max_gap, maxVal - prev_val);

        return max_gap;
    }

    // Driver program to run the case
    public static void main(String[] args)
    {

        int arr[] = { 1, 10, 5 };
        int n = arr.length;
        System.out.println(maxSortedAdjacentDiff(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find maximum adjacent
# difference between two adjacent after sorting.

def maxSortedAdjacentDiff(arr, n):

    # Find maximum and minimum in arr[]
    maxVal, minVal = arr[0], arr[0]
    for i in range(1, n):
        maxVal = max(maxVal, arr[i])
        minVal = min(minVal, arr[i])

    # Arrays to store maximum and minimum
    # values in n-1 buckets of differences.
    maxBucket = [INT_MIN] * (n - 1)
    minBucket = [INT_MAX] * (n - 1)

    # Expected gap for every bucket.
    delta = (maxVal - minVal) // (n - 1)

    # Traversing through array elements and
    # filling in appropriate bucket if bucket
    # is empty. Else updating bucket values.
    for i in range(0, n):
        if arr[i] == maxVal or arr[i] == minVal:
            continue

        # Finding index of bucket.
        index = (arr[i] - minVal) // delta

        # Filling/Updating maximum value
        # of bucket
        if maxBucket[index] == INT_MIN:
            maxBucket[index] = arr[i]
        else:
            maxBucket[index] = max(maxBucket[index],
                                             arr[i])

        # Filling/Updating minimum value of bucket
        if minBucket[index] == INT_MAX:
            minBucket[index] = arr[i]
        else:
            minBucket[index] = min(minBucket[index],
                                             arr[i])

    # Finding maximum difference between 
    # maximum value of previous bucket
    # minus minimum of current bucket.
    prev_val, max_gap = minVal, 0

    for i in range(0, n - 1):
        if minBucket[i] == INT_MAX:
            continue

        max_gap = max(max_gap,
                      minBucket[i] - prev_val)
        prev_val = maxBucket[i]

    max_gap = max(max_gap, maxVal - prev_val)

    return max_gap

# Driver Code
if __name__ == "__main__":

    arr = [1, 10, 5]
    n = len(arr)
    INT_MIN, INT_MAX = float('-inf'), float('inf')

    print(maxSortedAdjacentDiff(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find maximum
// adjacent difference between
// two adjacent after sorting.
using System;
using System.Linq;

class GFG
{
static int maxSortedAdjacentDiff(int[] arr,    
                                 int n)
{
    // Find maximum and minimum in arr[]
    int maxVal = arr[0];
    int minVal = arr[0];
    for (int i = 1; i < n; i++)
    {
        maxVal = Math.Max(maxVal, arr[i]);
        minVal = Math.Min(minVal, arr[i]);
    }

    // Arrays to store maximum and
    // minimum values in n-1 buckets
    // of differences.
    int []maxBucket = new int[n - 1];
    int []minBucket = new int[n - 1];
    maxBucket = maxBucket.Select(i => int.MinValue).ToArray();
    minBucket = minBucket.Select(i => int.MaxValue).ToArray();

    // maxBucket.Fill(int.MinValue);
    // Arrays.fill(minBucket, 0, n - 1, Integer.MAX_VALUE);

    // Expected gap for every bucket.
    float delta = (float) (maxVal - minVal) /
                  (float) (n - 1);

    // Traversing through array elements and
    // filling in appropriate bucket if bucket
    // is empty. Else updating bucket values.
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == maxVal || arr[i] == minVal)
        {
            continue;
        }

        // Finding index of bucket.
        int index = (int) (Math.Round((arr[i] -
                             minVal) / delta));

        // Filling/Updating maximum value of bucket
        if (maxBucket[index] == int.MinValue)
        {
            maxBucket[index] = arr[i];
        }
        else
        {
            maxBucket[index] = Math.Max(maxBucket[index],
                                                  arr[i]);
        }

        // Filling/Updating minimum value of bucket
        if (minBucket[index] == int.MaxValue)
        {
            minBucket[index] = arr[i];
        }
        else
        {
            minBucket[index] = Math.Min(minBucket[index],
                                                  arr[i]);
        }
    }

    // Finding maximum difference between
    // maximum value of previous bucket
    // minus minimum of current bucket.
    int prev_val = minVal;
    int max_gap = 0;
    for (int i = 0; i < n - 1; i++)
    {
        if (minBucket[i] == int.MaxValue)
        {
            continue;
        }
        max_gap = Math.Max(max_gap, minBucket[i] -
                                    prev_val);
        prev_val = maxBucket[i];
    }
    max_gap = Math.Max(max_gap, maxVal -
                                prev_val);

    return max_gap;
}

// Driver Code
public static void Main()
{
    int []arr = {1, 10, 5};
    int n = arr.Length;
    Console.Write(maxSortedAdjacentDiff(arr, n));
}
}

// This code contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find maximum adjacent difference
// between two adjacent after sorting.

function maxSortedAdjacentDiff(arr, n)
{
    // Find maximum and minimum in arr[]
    var maxVal = arr[0], minVal = arr[0];
    for (var i = 1; i < n; i++) {
        maxVal = Math.max(maxVal, arr[i]);
        minVal = Math.min(minVal, arr[i]);
    }

    // Arrays to store maximum and minimum values
    // in n-1 buckets of differences.
    var maxBucket = Array(n-1).fill(-1000000000);
    var minBucket = Array(n-1).fill(1000000000);

    // Expected gap for every bucket.
    var delta = (maxVal - minVal) / (n - 1);

    // Traversing through array elements and
    // filling in appropriate bucket if bucket
    // is empty. Else updating bucket values.
    for (var i = 0; i < n; i++) {
        if (arr[i] == maxVal || arr[i] == minVal)
            continue;

        // Finding index of bucket.
        var index = Math.floor((arr[i] - minVal) / delta);

        maxBucket[index] = Math.max(maxBucket[index], arr[i]);
           minBucket[index] = Math.min(minBucket[index], arr[i]);
    }

    // Finding maximum difference between maximum value
    // of previous bucket minus minimum of current bucket.
    var prev_val = minVal;
    var max_gap = 0;
    for (var i = 0; i < n - 1; i++) {
        if (minBucket[i] == 1000000000)
            continue;
        max_gap = Math.max(max_gap, minBucket[i] - prev_val);
        prev_val = maxBucket[i];
    }
    max_gap = Math.max(max_gap, maxVal - prev_val);

    return max_gap;
}

var arr = [1, 10, 5];
var n = arr.length;
document.write( maxSortedAdjacentDiff(arr, n));

</script>
```

**Output**

```
5
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
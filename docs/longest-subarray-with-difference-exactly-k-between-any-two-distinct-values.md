# 任意两个不同值之间相差 K 的最长子阵列

> 原文:[https://www . geeksforgeeks . org/任意两个不同值之间有差异的最长子数组/](https://www.geeksforgeeks.org/longest-subarray-with-difference-exactly-k-between-any-two-distinct-values/)

给定一个长度为 **N** 的数组**arr【】**和一个整数 **K** ，任务是找到任意两个不同值之差等于 **K** 的最长子阵列。打印获得的最长子阵列的长度。否则，如果没有得到这样的子阵列，打印 **-1** 。

**示例:**

> **输入:** arr[] = {0，0，1，1，3，3}，K = 1
> **输出:** 4
> **解释:**
> 子阵列{0，0，1，1}是唯一一个在任意两个不同值之间存在差异的子阵列，该差异等于 K( = 1)。因此，长度等于 4。
> 
> **输入:** arr[] = {5，7，1，1，2，4，4，4，5，5，4，5，8，9}，K = 1
> **输出:** 7
> **解释:**
> 子阵列{1，1，2}、{4，4，4，5，5，4，5}和{8，9}是唯一在任意两个不同值之间有差异的子阵列，这些值等于 K( = 1)。
> 其中最长的子阵是{4，4，4，5，5，4，5}。
> 因此，长度为 7。

**天真方法:**

*   一个简单的解决方法是逐个考虑所有子阵，找到只包含两个截然不同的值的子阵，这两个值之差为 **K** 。不断更新获得的子阵列的最大长度。
*   最后打印获得的最大长度。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**有效方法:**
可以观察到，对于由任意两个元素之差恰好为 K 的元素组成的任何子阵列，该子阵列必须仅由两个不同的值组成。因此，上述方法可以通过使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)来进一步优化，以找到仅具有两个不同值 k 的最长子阵列。

*   从数组的起始索引开始第一个子数组。
*   将该元素插入到集合中。继续下一个元素，检查这个元素是否与前一个元素相同，或者绝对差值为 k。
*   如果是，将该元素插入集合中，并继续增加子阵列的长度。一旦找到第三个不同的元素，将当前子阵列的长度与子阵列的最大长度进行比较，并进行相应的更新。
*   将获得的新元素更新到集合中，并继续重复上述步骤。
*   一旦遍历了整个数组，打印得到的最大长度。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// longest subarray consisting of
// only two values with difference K
#include <bits/stdc++.h>
using namespace std;

// Function to return the length
// of the longest sub-array
int longestSubarray(int arr[], int n,
                    int k)
{
    int i, j, Max = 1;

    // Initialize set
    set<int> s;

    for (i = 0; i < n - 1; i++) {
        // Store 1st element of
        // sub-array into set
        s.insert(arr[i]);

        for (j = i + 1; j < n; j++) {
            // Check absolute difference
            // between two elements

            if (abs(arr[i] - arr[j]) == 0
                || abs(arr[i] - arr[j]) == k) {

                // If the new element is not
                // present in the set
                if (!s.count(arr[j])) {

                    // If the set contains
                    // two elements
                    if (s.size() == 2)
                        break;

                    // Otherwise
                    else
                        s.insert(arr[j]);
                }
            }
            else
                break;
        }

        if (s.size() == 2) {

            // Update the maximum
            // length
            Max = max(Max, j - i);

            // Remove the set
            // elements
            s.clear();
        }
        else
            s.clear();
    }

    return Max;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 2, 2, 5, 5, 5 };

    int N = sizeof(arr)
            / sizeof(arr[0]);
    int K = 1;

    int length = longestSubarray(
        arr, N, K);

    if (length == 1)
        cout << -1;
    else
        cout << length;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// longest subarray consisting of
// only two values with difference K
import java.util.*;

class GFG{

// Function to return the length
// of the longest sub-array
static int longestSubarray(int arr[], int n,
                        int k)
{
    int i, j, Max = 1;

    // Initialize set
    HashSet<Integer> s = new HashSet<Integer>();

    for(i = 0; i < n - 1; i++)
    {

        // Store 1st element of
        // sub-array into set
        s.add(arr[i]);

        for(j = i + 1; j < n; j++)
        {

            // Check absolute difference
            // between two elements
            if (Math.abs(arr[i] - arr[j]) == 0 ||
                Math.abs(arr[i] - arr[j]) == k)
            {

                // If the new element is not
                // present in the set
                if (!s.contains(arr[j]))
                {

                    // If the set contains
                    // two elements
                    if (s.size() == 2)
                        break;

                    // Otherwise
                    else
                        s.add(arr[j]);
                }
            }
            else
                break;
        }
        if (s.size() == 2)
        {

            // Update the maximum
            // length
            Max = Math.max(Max, j - i);

            // Remove the set
            // elements
            s.clear();
        }
        else
            s.clear();
    }
    return Max;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 0, 2, 2, 5, 5, 5 };

    int N = arr.length;
    int K = 1;
    int length = longestSubarray(arr, N, K);

    if (length == 1)
        System.out.print(-1);
    else
        System.out.print(length);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find the 
# longest subarray consisting of 
# only two values  with difference K

# Function to return the length 
# of the longest sub-array
def longestSubarray (arr, n, k):

    Max = 1

    # Initialize set
    s = set()

    for i in range(n - 1):

        # Store 1st element of
        # sub-array into set
        s.add(arr[i])

        for j in range(i + 1, n):

            # Check absolute difference
            # between two elements
            if (abs(arr[i] - arr[j]) == 0 or
                abs(arr[i] - arr[j]) == k):

                # If the new element is not
                # present in the set
                if (not arr[j] in s):

                    # If the set contains
                    # two elements
                    if (len(s) == 2):
                        break

                    # Otherwise
                    else:
                        s.add(arr[j])

            else:
                break

        if (len(s) == 2):

            # Update the maximum length
            Max = max(Max, j - i)

            # Remove the set elements
            s.clear()

        else:
            s.clear()

    return Max

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 0, 2, 2, 5, 5, 5 ]

    N = len(arr)
    K = 1

    length = longestSubarray(arr, N, K)

    if (length == 1):
        print("-1")
    else:
        print(length)

# This code is contributed by himanshu77
```

## C#

```
// C# implementation to find the
// longest subarray consisting of
// only two values with difference K
using System;
using System.Collections.Generic;

class GFG{

// Function to return the length
// of the longest sub-array
static int longestSubarray(int []arr, int n,
                                      int k)
{
    int i, j, Max = 1;

    // Initialize set
    HashSet<int> s = new HashSet<int>();

    for(i = 0; i < n - 1; i++)
    {

        // Store 1st element of
        // sub-array into set
        s.Add(arr[i]);

        for(j = i + 1; j < n; j++)
        {

            // Check absolute difference
            // between two elements
            if (Math.Abs(arr[i] - arr[j]) == 0 ||
                Math.Abs(arr[i] - arr[j]) == k)
            {

                // If the new element is not
                // present in the set
                if (!s.Contains(arr[j]))
                {

                    // If the set contains
                    // two elements
                    if (s.Count == 2)
                        break;

                    // Otherwise
                    else
                        s.Add(arr[j]);
                }
            }
            else
                break;
        }
        if (s.Count == 2)
        {

            // Update the maximum
            // length
            Max = Math.Max(Max, j - i);

            // Remove the set
            // elements
            s.Clear();
        }
        else
            s.Clear();
    }
    return Max;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 0, 2, 2, 5, 5, 5 };

    int N = arr.Length;
    int K = 1;
    int length = longestSubarray(arr, N, K);

    if (length == 1)
        Console.Write(-1);
    else
        Console.Write(length);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript implementation to find the
    // longest subarray consisting of
    // only two values with difference K

    // Function to return the length
    // of the longest sub-array
    function longestSubarray(arr, n, k)
    {
        let i, j, Max = 1;

        // Initialize set
        let s = new Set();

        for (i = 0; i < n - 1; i++) {
            // Store 1st element of
            // sub-array into set
            s.add(arr[i]);

            for (j = i + 1; j < n; j++) {
                // Check absolute difference
                // between two elements

                if (Math.abs(arr[i] - arr[j]) == 0
                    || Math.abs(arr[i] - arr[j]) == k) {

                    // If the new element is not
                    // present in the set
                    if (!s.has(arr[j])) {

                        // If the set contains
                        // two elements
                        if (s.size == 2)
                            break;

                        // Otherwise
                        else
                            s.add(arr[j]);
                    }
                }
                else
                    break;
            }

            if (s.size == 2) {

                // Update the maximum
                // length
                Max = Math.max(Max, j - i);

                // Remove the set
                // elements
                s.clear;
            }
            else
                s.clear;
        }

        return Max;
    }

    let arr = [ 1, 0, 2, 2, 5, 5, 5 ];

    let N = arr.length;
    let K = 1;

    let length = longestSubarray(arr, N, K);

    if (length == 1)
        document.write(-1);
    else
        document.write(length);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>* logN)*
***辅助空间:** O(N)*
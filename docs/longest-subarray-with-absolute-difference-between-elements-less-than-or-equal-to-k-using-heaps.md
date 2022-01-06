# 元素间绝对差小于或等于 K 的最长子阵列使用堆

> 原文:[https://www . geesforgeks . org/元素间绝对差小于或等于 k 的最长子数组使用堆/](https://www.geeksforgeeks.org/longest-subarray-with-absolute-difference-between-elements-less-than-or-equal-to-k-using-heaps/)

给定一个由 **N** 个整数和一个整数 **K** 组成的**数组** **arr[]** ，我们的任务是找到最长子阵列的长度，使得对于子阵列中所有可能的对，元素之间的绝对差小于或等于 K

**示例:**

> **输入:** arr[] = {2，4，5，5，5，3，1}，K = 0
> **输出:** 3
> **解释:**
> 元素相差为 0 的可能子阵是长度为 3 的{5，5，5}。因此输出为 3。
> 
> **输入:** arr[] = {1，2，3，6，7}，K = 2
> **输出:** 3
> **解释:**
> 元素最多相差 2 的可能子阵是长度为 3 的{1，2，3}。因此输出为 3。

**天真方法:**
解决上述问题的天真方法是使用蛮力方法，即生成给定阵列的所有[可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并检查子阵列的最大和最小元素之间的[差是否至多为 **K** 。如果是，则用最大长度更新当前子阵列的长度。完成所有操作后，打印子阵列的最大长度。](https://www.geeksforgeeks.org/minimize-the-maximum-difference-between-the-heights/)

下面是上述方法的实现:

## C++

```
// C++ implementation to find the Longest subarray
// of the given array with absolute difference between
// elements less than or equal to integer K
#include <bits/stdc++.h>
using namespace std;

int computeLongestSubarray(int arr[], int k, int n)
{

    // maxLength is 1 because k >= 0,
    // a single element, subarray will always
    // have absolute difference zero
    int maxLength = 1;

    // Check for all possible subarrays
    for(int i = 0; i < n; i++)
    {

        // Initialization of minimum &
        // maximum of current subarray
        int minOfSub = arr[i];
        int maxOfSub = arr[i];

        for(int j = i + 1; j < n; j++)
        {

            // Update the values for minimum & maximum
            if (arr[j] > maxOfSub)
                maxOfSub = arr[j];

            if (arr[j] < minOfSub)
                minOfSub = arr[j];

            // Check if current subarray satisfies
            // the given condition
            if ((maxOfSub - minOfSub) <= k)
            {
                int currLength = j - i + 1;

                // Update the value for maxLength
                if (maxLength < currLength)
                    maxLength = currLength;
            }
        }
    }

    // Return the final result
    return maxLength;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 6, 7 };

    int k = 2;
    int n = sizeof(arr) / sizeof(arr[0]);

    int maxLength = computeLongestSubarray(arr, k, n);

    cout << (maxLength);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the Longest subarray
// of the given array with absolute difference between
// elements less than or equal to integer K

class GFG {
    public static int computeLongestSubarray(int arr[],
                                                int k)
    {
        // maxLength is 1 because k >= 0,
        // a single element, subarray will always
        // have absolute difference zero
        int maxLength = 1;

        // Check for all possible subarrays
        for (int i = 0; i < arr.length; i++) {
            // Initialization of minimum &
            // maximum of current subarray
            int minOfSub = arr[i];
            int maxOfSub = arr[i];

            for (int j = i + 1; j < arr.length; j++) {

                // Update the values for minimum & maximum
                if (arr[j] > maxOfSub)
                    maxOfSub = arr[j];

                if (arr[j] < minOfSub)
                    minOfSub = arr[j];

                // Check if current subarray satisfies
                // the given condition
                if ((maxOfSub - minOfSub) <= k) {
                    int currLength = j - i + 1;

                    // Update the value for maxLength
                    if (maxLength < currLength)
                        maxLength = currLength;
                }
            }
        }

        // Return the final result
        return maxLength;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 6, 7 };

        int k = 2;

        int maxLength = computeLongestSubarray(arr, k);
        System.out.println(maxLength);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Longest subarray of the given array
# with absolute difference between
# elements less than or equal to integer K
def computeLongestSubarray (arr, k, n):

    # maxLength is 1 because k >= 0,
    # a single element, subarray will always
    # have absolute difference zero
    maxLength = 1

    # Check for all possible subarrays
    for i in range(n):

        # Initialization of minimum &
        # maximum of current subarray
        minOfSub = arr[i]
        maxOfSub = arr[i]

        for j in range(i + 1, n):

            # Update the values for
            # minimum & maximum
            if (arr[j] > maxOfSub):
                maxOfSub = arr[j]

            if (arr[j] < minOfSub):
                minOfSub = arr[j]

            # Check if current subarray
            # satisfies the given condition
            if ((maxOfSub - minOfSub) <= k):
                currLength = j - i + 1

                # Update the value for maxLength
                if (maxLength < currLength):
                    maxLength = currLength

    # Return the final result
    return maxLength

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 6, 7 ]
    k = 2
    n = len(arr)

    maxLength = computeLongestSubarray(arr, k, n)

    print(maxLength)

# This code is contributed by himanshu77
```

## C#

```
// C# implementation to find the longest subarray
// of the given array with absolute difference between
// elements less than or equal to integer K
using System;
class GFG
{
    public static int computelongestSubarray(int []arr,
                                                int k)
    {

        // maxLength is 1 because k >= 0,
        // a single element, subarray will always
        // have absolute difference zero
        int maxLength = 1;

        // Check for all possible subarrays
        for (int i = 0; i < arr.Length; i++)
        {

            // Initialization of minimum &
            // maximum of current subarray
            int minOfSub = arr[i];
            int maxOfSub = arr[i];

            for (int j = i + 1; j < arr.Length; j++)
            {

                // Update the values for minimum & maximum
                if (arr[j] > maxOfSub)
                    maxOfSub = arr[j];

                if (arr[j] < minOfSub)
                    minOfSub = arr[j];

                // Check if current subarray satisfies
                // the given condition
                if ((maxOfSub - minOfSub) <= k)
                {
                    int currLength = j - i + 1;

                    // Update the value for maxLength
                    if (maxLength < currLength)
                        maxLength = currLength;
                }
            }
        }

        // Return the readonly result
        return maxLength;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 3, 6, 7 };
        int k = 2;
        int maxLength = computelongestSubarray(arr, k);
        Console.WriteLine(maxLength);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript implementation to find the Longest subarray
// of the given array with absolute difference between
// elements less than or equal to integer K

function computeLongestSubarray(arr,k)
{
    // maxLength is 1 because k >= 0,
        // a single element, subarray will always
        // have absolute difference zero
        let maxLength = 1;

        // Check for all possible subarrays
        for (let i = 0; i < arr.length; i++) {
            // Initialization of minimum &
            // maximum of current subarray
            let minOfSub = arr[i];
            let maxOfSub = arr[i];

            for (let j = i + 1; j < arr.length; j++) {

                // Update the values for minimum & maximum
                if (arr[j] > maxOfSub)
                    maxOfSub = arr[j];

                if (arr[j] < minOfSub)
                    minOfSub = arr[j];

                // Check if current subarray satisfies
                // the given condition
                if ((maxOfSub - minOfSub) <= k) {
                    let currLength = j - i + 1;

                    // Update the value for maxLength
                    if (maxLength < currLength)
                        maxLength = currLength;
                }
            }
        }

        // Return the final result
        return maxLength;
}

 // Driver Code
let arr=[1, 2, 3, 6, 7];
let  k = 2;
let maxLength = computeLongestSubarray(arr, k);
document.write(maxLength);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n <sup>2</sup>

**高效方法:**
优化上述方法的思路是使用[堆数据结构](https://www.geeksforgeeks.org/heap-data-structure/)。初始化一个 **minHeap** ，它将存储当前子阵列的索引，使得元素按升序排列，其中最小的出现在顶部；初始化一个**MaxHep**，它将存储当前子阵列的索引，使得元素按降序排列，其中最大的元素出现在顶部。然后迭代整个数组，每次迭代检查是否:

*   所有的子阵列元素都满足 **maxOfSub-minOfSub < = k** 的条件，那么我们**将目前为止的 maxLength** 与当前子阵列的长度进行比较，并将 maxLength 更新为 maxLength 或当前子阵列长度的最大值。
*   如果条件不满足，则将子数组的开始指针增加 1，并删除新子数组中不包含的 minHeap 和 maxHeap 中的所有索引。
*   每次迭代后，我们通过增加结束指针来增加子阵列长度。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the Longest
// subarray of the given array with absolute
// difference between elements less than or equal
// to integer K using Heaps
import java.util.*;

class GFG {
    public static int computeLongestSubarray(int arr[],
                                                 int k)
    {
        // Stores the maximum length subarray so far
        int maxLength = 0;

        Deque<Integer> maxHeap = new LinkedList<>();
        Deque<Integer> minHeap = new LinkedList<>();

        // Marks to the beginning and end
        // pointer for current subarray
        int beg = 0, end = 0;

        while (end < arr.length) {

            // Stores the current element being
            // added to the subarray
            int currEl = arr[end];

            // Remove indices of all elements smaller
            // than or equal to current from maxHeap
            while (maxHeap.size() > 0 &&
                       arr[maxHeap.peekLast()] <= currEl)
                maxHeap.removeLast();

            // Add current element's index to maxHeap
            maxHeap.addLast(end);

            // Remove indices of all elements larger
            // than or equal to current from minHeap
            while (minHeap.size() > 0 &&
                       arr[minHeap.peekLast()] >= currEl)
                minHeap.removeLast();

            // Add current element's index to minHeap
            minHeap.addLast(end);

            // Index of maximum of current subarray
            int maxOfSub = arr[maxHeap.peekFirst()];

            // Index of minimum of current subarray
            int minOfSub = arr[minHeap.peekFirst()];

            // check if the largest possible difference
            // between a pair of elements <= k
            if (maxOfSub - minOfSub <= k) {
                // Length of current subarray
                int currLength = end - beg + 1;

                // Update maxLength
                if (maxLength < currLength)
                    maxLength = currLength;
            }

            else {
                // If current subarray doesn't satisfy
                // the condition then remove the starting
                // element from subarray that satisfy
                // increment the beginning pointer
                beg++;

                // Remove elements from heaps that
                // are not in the subarray anymore
                while (minHeap.size() > 0 &&
                               minHeap.peekFirst() < beg)
                    minHeap.removeFirst();

                while (maxHeap.size() > 0 &&
                               maxHeap.peekFirst() < beg)
                    maxHeap.removeFirst();
            }

            end++;
        }

        // Return the final answer
        return maxLength;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 6, 7 };

        int k = 2;

        int maxLength = computeLongestSubarray(arr, k);
        System.out.println(maxLength);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to find the Longest
# subarray of the given array with absolute
# difference between elements less than or equal
# to integer K using Heaps
from collections import deque

def computeLongestSubarray(arr, k):
    # Stores the maximum length subarray so far
    maxLength = 0

    maxHeap = []
    minHeap = []

    # Marks to the beginning and end
    # pointer for current subarray
    beg = 0
    end = 0

    while (end < len(arr)):
        # print(end)

        # Stores the current element being
        # added to the subarray
        currEl = arr[end]

        # Remove indices of all elements smaller
        # than or equal to current from maxHeap
        while (len(maxHeap) > 0 and arr[maxHeap[-1]] <= currEl):
            del maxHeap[-1]

        # Add current element's index to maxHeap
        maxHeap.append(end)

        # Remove indices of all elements larger
        # than or equal to current from minHeap
        while (len(minHeap) > 0 and arr[minHeap[-1]] >= currEl):

            # print(minHeap[-1])
            del minHeap[-1]

        # Add current element's index to minHeap
        minHeap.append(end)

        # Index of maximum of current subarray
        maxOfSub = arr[maxHeap[0]]

        # Index of minimum of current subarray
        minOfSub = arr[minHeap[0]]

        # check if the largest possible difference
        # between a pair of elements <= k
        if (maxOfSub - minOfSub <= k):

            # Length of current subarray
            currLength = end - beg + 1

            # Update maxLength
            if (maxLength < currLength):
                maxLength = currLength
        else:
            # If current subarray doesn't satisfy
            # the condition then remove the starting
            # element from subarray that satisfy
            # increment the beginning pointer
            beg += 1

            # Remove elements from heaps that
            # are not in the subarray anymore
            while (len(minHeap) > 0 and minHeap[0] < beg):
                del minHeap[0]

            while (len(maxHeap) > 0 and maxHeap[0] < beg):
                del maxHeap[0]

        end += 1

    # Return the final answer
    return maxLength

    # Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 6, 7]

    k = 2

    maxLength = computeLongestSubarray(arr, k)
    print(maxLength)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript implementation to find the Longest
// subarray of the given array with absolute
// difference between elements less than or equal
// to integer K using Heaps

function computeLongestSubarray(arr,k)
{
    // Stores the maximum length subarray so far
        let maxLength = 0;

        let maxHeap = [];
        let minHeap = [];

        // Marks to the beginning and end
        // pointer for current subarray
        let beg = 0, end = 0;

        while (end < arr.length) {

            // Stores the current element being
            // added to the subarray
            let currEl = arr[end];

            // Remove indices of all elements smaller
            // than or equal to current from maxHeap
            while (maxHeap.length > 0 &&
                       arr[maxHeap[maxHeap.length-1]] <= currEl)
                maxHeap.pop();

            // Add current element's index to maxHeap
            maxHeap.push(end);

            // Remove indices of all elements larger
            // than or equal to current from minHeap
            while (minHeap.length > 0 &&
                       arr[minHeap[minHeap.length-1]] >= currEl)
                minHeap.pop();

            // Add current element's index to minHeap
            minHeap.push(end);

            // Index of maximum of current subarray
            let maxOfSub = arr[maxHeap[0]];

            // Index of minimum of current subarray
            let minOfSub = arr[minHeap[0]];

            // check if the largest possible difference
            // between a pair of elements <= k
            if (maxOfSub - minOfSub <= k) {
                // Length of current subarray
                let currLength = end - beg + 1;

                // Update maxLength
                if (maxLength < currLength)
                    maxLength = currLength;
            }

            else {
                // If current subarray doesn't satisfy
                // the condition then remove the starting
                // element from subarray that satisfy
                // increment the beginning pointer
                beg++;

                // Remove elements from heaps that
                // are not in the subarray anymore
                while (minHeap.length > 0 &&
                               minHeap[0] < beg)
                    minHeap.shift();

                while (maxHeap.length > 0 &&
                               maxHeap[0] < beg)
                    maxHeap.shift();
            }

            end++;
        }

        // Return the final answer
        return maxLength;
}

// Driver code

let arr=[ 1, 2, 3, 6, 7 ];
let  k = 2;
let maxLength = computeLongestSubarray(arr, k);
document.write(maxLength);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)，因为数组的每个元素只从堆中添加和移除一次。
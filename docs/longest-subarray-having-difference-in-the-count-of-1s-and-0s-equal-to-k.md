# 1 和 0 的计数之差等于 k 的最长子阵列

> 原文:[https://www . geesforgeks . org/最长子阵列-1 和 0 的计数之差等于-k/](https://www.geeksforgeeks.org/longest-subarray-having-difference-in-the-count-of-1s-and-0s-equal-to-k/)

给定一个大小为 **n** 的二进制数组 **arr[]** 和一个值 **k** 。任务是找出 1 和 0 的计数相差等于 **k** 的最长子阵列的长度。根据 **k** 的值，子阵列中 1 的计数应等于或大于 0 的计数。
**举例:**

```
Input: arr[] = {0, 1, 1, 0, 1}, k = 2
Output: 4
The highlighted portion is the required subarray
{0, 1, 1, 0, 1}. In the subarray count of 1's is 3
and count of 0's is 1\. 
Therefore, difference in count = 3 - 1 = 2.

Input: arr[] = {1, 1, 0, 1, 1, 1, 0, 0, 1, 1, 1}, k = 0
Output: 6
The highlighted portion is the required subarray
{1, 1, 0, 1, 1, 1, 0, 0, 1, 1, 1}. In the subarray 
count of 1's is 3 and count of 0's is 3\. 
Therefore, difference in count = 3 - 3 = 0.
```

**天真方法:**考虑所有子阵列的 1 和 0 的计数差异，并返回所需差异等于“k”的最长子阵列的长度。时间复杂性将是 O(n^2).
**有效方法:**这个问题是寻找具有和 k 的[最长子阵列的变体。将**arr【】**中的所有 0 替换为-1，然后找到总和等于“k”的**最长的“arr”子阵列。**
以下是上述方法的实施:](https://www.geeksforgeeks.org/longest-sub-array-sum-k/) 

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function to find the length of the longest
// subarray having difference in the count
// of 1's and 0's equal to k
int lenOfLongSubarr(int arr[], int n, int k)
{

    // unordered_map 'um' implemented
    // as hash table
    unordered_map<int, int> um;
    int sum = 0, maxLen = 0;

    // traverse the given array
    for (int i = 0; i < n; i++) {

        // accumulate sum
        sum += ((arr[i] == 0) ? -1 : arr[i]);

        // when subarray starts from index '0'
        if (sum == k)
            maxLen = i + 1;

        // make an entry for 'sum' if it is
        // not present in 'um'
        if (um.find(sum) == um.end())
            um[sum] = i;

        // check if 'sum-k' is present in 'um'
        // or not
        if (um.find(sum - k) != um.end()) {

            // update maxLength
            if (maxLen < (i - um[sum - k]))
                maxLen = i - um[sum - k];
        }
    }

    // required maximum length
    return maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 1, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << "Length = "
         << lenOfLongSubarr(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
import java.util.HashMap;
import java.util.Map;

class GfG
{

    // Function to find the length of the longest
    // subarray having difference in the count
    // of 1's and 0's equal to k
    static int lenOfLongSubarr(int arr[], int n, int k)
    {
        // unordered_map 'um' implemented
        // as hash table
        HashMap<Integer, Integer> um = new HashMap<>();
        int sum = 0, maxLen = 0;

        // traverse the given array
        for (int i = 0; i < n; i++)
        {

            // accumulate sum
            sum += ((arr[i] == 0) ? -1 : arr[i]);

            // when subarray starts from index '0'
            if (sum == k)
                maxLen = i + 1;

            // make an entry for 'sum' if
            // it is not present in 'um'
            if (!um.containsKey(sum))
                um.put(sum, i);

            // check if 'sum-k' is present
            // in 'um' or not
            if (um.containsKey(sum - k))
            {

                // update maxLength
                if (maxLen < (i - um.get(sum - k)))
                    maxLen = i - um.get(sum - k);
            }
        }

        // required maximum length
        return maxLen;
    }

    // Driver code
    public static void main(String []args)
    {

        int arr[] = { 0, 1, 1, 0, 1 };
        int n = arr.length;
        int k = 2;

        System.out.println("Length = " + lenOfLongSubarr(arr, n, k));
    }
}

// This code is contributed by Rituraj Jain
```

## 计算机编程语言

```
# Python3 implementation of above approach

# function to find the length of the longest
# subarray having difference in the count
# of 1's and 0's equal to k
def lenOfLongSubarr(arr, n, k):

    # unordered_map 'um' implemented
    # as hash table
    um = dict()

    Sum, maxLen = 0, 0

    # traverse the given array
    for i in range(n):

        # accumulate sum
        if arr[i] == 0:
            Sum += -1
        else:
            Sum+=arr[i]

        # when subarray starts from index '0'
        if (Sum == k):
            maxLen = i + 1

        # make an entry for 'Sum' if it is
        # not present in 'um'
        if (Sum not in um.keys()):
            um[Sum] = i

        # check if 'Sum-k' is present in 'um'
        # or not
        if ((Sum - k) in um.keys()):

            # update maxLength
            if (maxLen < (i - um[Sum - k])):
                maxLen = i - um[Sum - k]

    # required maximum length
    return maxLen

# Driver Code
arr = [0, 1, 1, 0, 1]
n = len(arr)
k = 2
print("Length = ",lenOfLongSubarr(arr, n, k))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the length of the longest
    // subarray having difference in the count
    // of 1's and 0's equal to k
    static int lenOfLongSubarr(int []arr,
                               int n, int k)
    {
        // unordered_map 'um' implemented
        // as hash table
        Dictionary<int,
                   int> um = new Dictionary<int,
                                            int>();
        int sum = 0, maxLen = 0;

        // traverse the given array
        for (int i = 0; i < n; i++)
        {

            // accumulate sum
            sum += ((arr[i] == 0) ? -1 : arr[i]);

            // when subarray starts from index '0'
            if (sum == k)
                maxLen = i + 1;

            // make an entry for 'sum' if
            // it is not present in 'um'
            if (!um.ContainsKey(sum))
                um.Add(sum, i);

            // check if 'sum-k' is present
            // in 'um' or not
            if (um.ContainsKey(sum - k))
            {

                // update maxLength
                if (maxLen < (i - um[sum - k]))
                    maxLen = i - um[sum - k];
            }
        }

        // required maximum length
        return maxLen;
    }

    // Driver code
    public static void Main(String []args)
    {

        int []arr = { 0, 1, 1, 0, 1 };
        int n = arr.Length;
        int k = 2;

        Console.WriteLine("Length = " +
                lenOfLongSubarr(arr, n, k));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// function to find the length of the longest
// subarray having difference in the count
// of 1's and 0's equal to k
function lenOfLongSubarr(arr, n, k)
{

    // unordered_map 'um' implemented
    // as hash table
    var um = new Map();
    var sum = 0, maxLen = 0;

    // traverse the given array
    for (var i = 0; i < n; i++) {

        // accumulate sum
        sum += ((arr[i] == 0) ? -1 : arr[i]);

        // when subarray starts from index '0'
        if (sum == k)
            maxLen = i + 1;

        // make an entry for 'sum' if it is
        // not present in 'um'
        if (!um.has(sum))
            um.set(sum, i);

        // check if 'sum-k' is present in 'um'
        // or not
        if (um.has(sum - k)) {

            // update maxLength
            if (maxLen < (i - um.get(sum-k)))
                maxLen = i - um.get(sum-k);
        }
    }

    // required maximum length
    return maxLen;
}

// Driver Code
var arr = [0, 1, 1, 0, 1];
var n = arr.length;
var k = 2;
document.write( "Length = "
      + lenOfLongSubarr(arr, n, k));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Length = 4
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
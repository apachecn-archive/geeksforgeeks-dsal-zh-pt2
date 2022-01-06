# 子阵列的最大和，使得开始值和结束值相同

> 原文:[https://www . geesforgeks . org/maximum-sum-subarray-so-start-and-end-values-相同/](https://www.geeksforgeeks.org/maximum-sum-subarray-such-that-start-and-end-values-are-same/)

给定一个 N 个正数的数组，任务是找到一个连续的子数组(L-R)，使得 **a[L]=a[R]** 和 **a[L] + a[L+1] +…+ a[R]的和最大。**
**例:**

```
Input: arr[] = {1, 3, 2, 2, 3}
Output: 10
Subarray [3, 2, 2, 3] starts and ends with 3 and has sum = 10

Input: arr[] = {1, 3, 2, 2, 3}
Output: 10
```

**方法:**对于数组中的每个元素，让我们找到 2 个值:数组中的第一个(最左边)出现和数组中的最后一个(最右边)出现。因为所有数字都是正数，所以增加项数只能增加总和。因此，对于数组中的每个数字，我们找到它最左边和最右边出现的总和，这可以使用前缀总和快速完成。我们可以跟踪到目前为止找到的最大值，并最终打印出来。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
int maxValue(int a[], int n)
{
    unordered_map<int, int> first, last;
    int pr[n];

    for (int i = 0; i < n; i++) {

        // Build prefix sum array
        if (i)
            pr[i] = pr[i - 1] + a[i];
        else
            pr[i] = a[i];
        // If the value hasn't been encountered before,
        // It is the first occurrence
        if (first[a[i]] == 0)
            first[a[i]] = i + 1;

        // Keep updating the last occurrence
        last[a[i]] = i + 1;
    }

    int ans = 0;

    // Find the maximum sum with same first and last value
    for (int i = 0; i < n; i++) {
        int start = first[a[i]];
        int end = last[a[i]];
        if (start == 1) ans = max(ans, pr[end - 1]);
        else ans = max(ans, pr[end - 1] - pr[start - 2]);
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = {1,2,31,2,1};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxValue(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;

class GFG {
    static int maxValue(int[] a, int n)
    {
        HashMap<Integer, Integer> first = new HashMap<>();
        HashMap<Integer, Integer> last = new HashMap<>();

        int[] prefix = new int[n];

        for (int i = 0; i < n; i++) {

            // Build prefix sum array
            if (i != 0)
                prefix[i] = prefix[i - 1] + a[i];
            else
                prefix[i] = a[i];
            // If the value hasn't been encountered before,
            // It is the first occurrence
            if (!first.containsKey(a[i]))
                first.put(a[i], i);

            // Keep updating the last occurrence
            last.put(a[i], i);
        }

        int ans = -1;

        // Find the maximum sum with same first and last
        // value
        for (int i = 0; i < n; i++) {
            int start = first.get(a[i]);
            int end = last.get(a[i]);
            int sum = 0;
            if(start == 0)
                sum = prefix[end];
            else
                sum = prefix[end] - prefix[start - 1];
            if(sum > ans)
                ans = sum;
        }

        return ans;
    }

    // Driver Code
    public static void main(String args[])
    {
        int[] arr = { 1, 3, 5, 2, 4, 18, 2, 3 };
        int n = arr.length;
        System.out.print(maxValue(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from collections import defaultdict

# Function to find the maximum sum

def maxValue(a, n):

    first = defaultdict(lambda: 0)
    last = defaultdict(lambda: 0)

    pr = [None] * n
    pr[0] = a[0]
    first[a[0]] = 1
    last[a[0]] = 1
    for i in range(1, n):

        # Build prefix sum array
        pr[i] = pr[i - 1] + a[i]

        # If the value hasn't been encountered before,
        # It is the first occurrence
        if first[a[i]] == 0:
            first[a[i]] = i+1

        # Keep updating the last occurrence
        last[a[i]] = i+1

    ans = 0

    # Find the maximum sum with same first and last value
    for i in range(0, n):
        start = first[a[i]]
        end = last[a[i]]
        if start != 1:
            ans = max(ans, pr[end-1] - pr[start - 2])

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [1, 3, 5, 2, 4, 18, 2, 3]
    n = len(arr)

    print(maxValue(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the maximum sum
    static int maxValue(int[] a, int n)
    {
        Dictionary<int, int> first
            = new Dictionary<int, int>();
        Dictionary<int, int> last
            = new Dictionary<int, int>();

        for (int i = 0; i < n; i++) {
            first[a[i]] = 0;
            last[a[i]] = 0;
        }

        int[] pr = new int[n];
        pr[0] = a[0];
        first[a[0]] = 1;
        last[a[0]] = 1;
        for (int i = 1; i < n; i++) {

            // Build prefix sum array
            pr[i] = pr[i - 1] + a[i];

            // If the value hasn't been encountered before,
            // It is the first occurrence
            if (first[a[i]] == 0)
                first[a[i]] = i + 1;

            // Keep updating the last occurrence
            last[a[i]] = i + 1;
        }

        int ans = 0;

        // Find the maximum sum with
        // same first and last value
        for (int i = 0; i < n; i++) {
            int start = first[a[i]];
            int end = last[a[i]];
            if (start != 1)
                ans = Math.Max(ans,
                               pr[end - 1] - pr[start - 2]);
        }
        return ans;
    }

    // Driver Code
    static void Main()
    {
        int[] arr = { 1, 3, 5, 2, 4, 18, 2, 3 };
        int n = arr.Length;
        Console.Write(maxValue(arr, n));
    }
}

// This code is contributed by mohit kumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to find the maximum sum
function maxValue(a,n)
{
    let first = new Map();
        let last = new Map();
        for (let i = 0; i < n; i++) {
            first.set(a[i], 0);
            last.set(a[i], 0);
        }

        let pr = new Array(n);
        pr[0] = a[0];
        first[a[0]] = 0;
        last[a[0]] = 0;
        for (let i = 1; i < n; i++) {

            // Build prefix sum array
            pr[i] = pr[i - 1] + a[i];

            // If the value hasn't been encountered before,
            // It is the first occurrence
            if (parseInt((first.get(a[i]))) == 0)
                first.set(a[i], i+1);

            // Keep updating the last occurrence
            last.set(a[i], i+1);
        }

        let ans = 0;

        // Find the maximum sum with same first and last value
        for (let i = 0; i < n; i++) {
            let start = parseInt(first.get(a[i]));
            let end = parseInt(last.get(a[i]));
            if (start != 1)
                ans = Math.max(ans, pr[end-1] - pr[start - 2]);
        }

        return ans;
}

// Driver Code
let arr=[1, 3, 5, 2, 4, 18, 2, 3 ];
let n = arr.length;
document.write(maxValue(arr, n));   

// This code is contributed by patel2127

</script>
```

**Output**

```
37
```

**时间复杂度:** O(N)
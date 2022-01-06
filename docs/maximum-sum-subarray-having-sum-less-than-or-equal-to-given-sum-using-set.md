# 使用集合

具有小于或等于给定和的和的最大和子阵列

> 原文:[https://www . geesforgeks . org/sum-subarray-sum-小于或等于给定的 sum-use-set/](https://www.geeksforgeeks.org/maximum-sum-subarray-having-sum-less-than-or-equal-to-given-sum-using-set/)

给定一个长度为 **N** 的数组**arr【】**和一个整数 **K** ，任务是找到和小于 **K** 的最大和子数组。

***注意:**如果 K 小于**最小元素，则返回 INT_MIN。*

**示例:**

> **输入:** arr[] = {-1，2，2}，K = 4
> **输出:** 3
> **解释:**
> 最大和小于 4 的子阵为{-1，2，2}。
> 子阵{2，2}最大和= 4，但不小于 4。
> 
> **输入:** arr[] = {5，-2，6，3，-5}，K =15
> **输出:** 12
> **说明:**
> 最大和小于 15 的子阵为{5，-2，6，3}。

**有效方法:**子阵列[i，j]的和由阵列的**累积和直到 j–累积和直到 i** 给出。现在问题简化为找到两个指数 I 和 j，使得 i < j 和**cum【j】–cum【I】**与 **K** 一样接近，但小于它。
要解决这个问题，从左到右迭代数组。把你到目前为止遇到的 I 值的累计和放入一个集合中。当您处理累计量[j]时，您需要从集合中检索的是集合中最小的数字，该数字大于**累计量[j]–K**。这可以在 O(logN)中使用集合的上限来完成。

**以下是上述方法的实现:**

## C++

```
// C++ program to find maximum sum
// subarray less than K

#include <bits/stdc++.h>
using namespace std;

// Function to maximum required sum < K
int maxSubarraySum(int arr[], int N, int K)
{

    // Hash to lookup for value (cum_sum - K)
    set<int> cum_set;
    cum_set.insert(0);

    int max_sum = INT_MIN, cSum = 0;

    for (int i = 0; i < N; i++) {

        // getting cumulative sum from [0 to i]
        cSum += arr[i];

        // lookup for upperbound
        // of (cSum-K) in hash
        set<int>::iterator sit
            = cum_set.lower_bound(cSum - K);

        // check if upper_bound
        // of (cSum-K) exists
        // then update max sum
        if (sit != cum_set.end())

            max_sum = max(max_sum, cSum - *sit);

        // insert cumulative value in hash
        cum_set.insert(cSum);
    }

    // return maximum sum
    // lesser than K
    return max_sum;
}

// Driver code
int main()
{

    // initialise the array
    int arr[] = { 5, -2, 6, 3, -5 };

    // initialise the value of K
    int K = 15;

    // size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxSubarraySum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum
// subarray less than K
import java.util.*;
import java.io.*;

class GFG{

// Function to maximum required sum < K
static int maxSubarraySum(int arr[], int N,
                          int K)
{

    // Hash to lookup for value (cum_sum - K)
    Set<Integer> cum_set = new HashSet<>();
    cum_set.add(0);

    int max_sum =Integer.MIN_VALUE, cSum = 0;

    for(int i = 0; i < N; i++)
    {

        // Getting cumulative sum from [0 to i]
        cSum += arr[i];

        // Lookup for upperbound
        // of (cSum-K) in hash
        ArrayList<Integer> al = new ArrayList<>();
        Iterator<Integer> it = cum_set.iterator();
        int end = 0;

        while (it.hasNext())
        {
            end = it.next();
            al.add(end);
        }

        Collections.sort(al);
        int sit = lower_bound(al, cSum - K);

        // Check if upper_bound
        // of (cSum-K) exists
        // then update max sum
        if (sit != end)
            max_sum = Math.max(max_sum,
                               cSum - sit);

        // Insert cumulative value in hash
        cum_set.add(cSum);
    }

    // Return maximum sum
    // lesser than K
    return max_sum;
}

static int lower_bound(ArrayList<Integer> al,
                       int x)
{

    // x is the target value or key
    int l = -1, r = al.size();
    while (l + 1 < r)
    {
        int m = (l + r) >>> 1;
        if (al.get(m) >= x)
            r = m;
        else
            l = m;
    }
    return r;
}

// Driver code
public static void main(String args[])
{

    // Initialise the array
    int arr[] = { 5, -2, 6, 3, -5 };

    // Initialise the value of K
    int K = 15;

    // Size of array
    int N = arr.length;

    System.out.println(maxSubarraySum(arr, N, K));
}
}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Python3 program to find maximum sum
# subarray less than K
import sys
import bisect

# Function to maximum required sum < K

def maxSubarraySum(arr, N, K):
    # Hash to lookup for value (cum_sum - K)
    cum_set = set()
    cum_set.add(0)

    max_sum = 12
    cSum = 0

    for i in range(N):

        # getting cumulative sum from [0 to i]
        cSum += arr[i]

        # check if upper_bound
        # of (cSum-K) exists
        # then update max sum
        x = bisect.bisect_left(arr, cSum - K, lo=0, hi=len(arr))
        if x:
            max_sum = max(max_sum,x )

        # insert cumulative value in hash
        cum_set.add(cSum)

    # return maximum sum
    # lesser than K
    return max_sum

# Driver code
if __name__ == '__main__':
    # initialise the array
    arr = [5, -2, 6, 3, -5]

    # initialise the value of K
    K = 15

    # size of array
    N = len(arr)

    print(maxSubarraySum(arr, N, K))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// Java program to find maximum sum
// subarray less than K
using System;
using System.Collections.Generic;
class GFG {

    // Function to maximum required sum < K
    static int maxSubarraySum(int[] arr, int N, int K)
    {

        // Hash to lookup for value (cum_sum - K)
        HashSet<int> cum_set = new HashSet<int>();
        cum_set.Add(0);
        int max_sum = Int32.MinValue, cSum = 0;
        for (int i = 0; i < N; i++) {

            // Getting cumulative sum from [0 to i]
            cSum += arr[i];

            // Lookup for upperbound
            // of (cSum-K) in hash
            List<int> al = new List<int>();
            int end = 0;
            foreach(int it in cum_set)
            {
                end = it;
                al.Add(it);
            }

            al.Sort();
            int sit = lower_bound(al, cSum - K);

            // Check if upper_bound
            // of (cSum-K) exists
            // then update max sum
            if (sit != end)
                max_sum = Math.Max(max_sum, cSum - sit);

            // Insert cumulative value in hash
            cum_set.Add(cSum);
        }

        // Return maximum sum
        // lesser than K
        return max_sum;
    }
    static int lower_bound(List<int> al, int x)
    {

        // x is the target value or key
        int l = -1, r = al.Count;
        while (l + 1 < r) {
            int m = (l + r) >> 1;
            if (al[m] >= x)
                r = m;
            else
                l = m;
        }
        return r;
    }

    // Driver code
    public static void Main(string[] args)
    {

        // Initialise the array
        int[] arr = { 5, -2, 6, 3, -5 };

        // Initialise the value of K
        int K = 15;

        // Size of array
        int N = arr.Length;
        Console.Write(maxSubarraySum(arr, N, K));
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// JavaScript program to find maximum sum
// subarray less than K

    // Function to maximum required sum < K
    function maxSubarraySum(arr, N, K)
    {

        // Hash to lookup for value (cum_sum - K)
        let cum_set = new Set();

        cum_set.add(0);

        let max_sum = Number.MIN_SAFE_INTEGER;
        let cSum = 0;

        for(let i = 0; i < N; i++){

            // Getting cumulative sum from [0 to i]
            cSum += arr[i];

            // Lookup for upperbound
            // of (cSum-K) in hash
            let al = [];
            let end = 0;
            for(let it of cum_set)
            {
                end = it;
                al.push(it);
            }

            al.sort((a, b) => a - b);
            let sit = lower_bound(al, cSum - K);

            // Check if upper_bound
            // of (cSum-K) exists
            // then update max sum
            if (sit != end)
                max_sum = Math.max(max_sum, cSum - sit);

            // Insert cumulative value in hash
            cum_set.add(cSum);
        }

        // Return maximum sum
        // lesser than K
        return max_sum;
    }

    let lower_bound =
    (al, x) => al.filter((item) => item > x )[0]    

    // Driver code

        // Initialise the array
        let arr = [ 5, -2, 6, 3, -5 ];

        // Initialise the value of K
        let K = 15;

        // Size of array
        let N = arr.length;
        document.write(maxSubarraySum(arr, N, K));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
12
```

***时间复杂度:** O(N*Log(N))*
**类似文章:** [使用滑动窗口](https://www.geeksforgeeks.org/maximum-sum-subarray-sum-less-equal-given-sum/)
最大和子阵的和小于或等于给定和
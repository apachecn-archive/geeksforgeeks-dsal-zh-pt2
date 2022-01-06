# 最小 K，使得除以 K 后的数组元素之和不超过 S

> 原文:[https://www . geeksforgeeks . org/minimum-k-so-被 k 除后的数组元素之和不超过-s/](https://www.geeksforgeeks.org/minimum-k-such-that-sum-of-array-elements-after-division-by-k-does-not-exceed-s/)

给定一个由 **N** 元素和一个整数 **S** 组成的数组**。任务是在将所有元素除以 **K** 后，找到最小数量 **K** 使得数组元素的总和不超过 **S** 。
**注:**考虑整数除法。
**示例:****

> **输入:** arr[] = {10，7，8，10，12，19}，S = 27
> **输出:** 3
> 除以 3 后，数组变成
> {3，2，2，3，4，6}，新和为 20。
> **输入:** arr[] = {19，17，11，10}，S = 40
> **输出:** 2

**天真的方法:**迭代从 **1** 到数组中最大元素加上一个非最大元素的 **K** 的所有值，因为如果我们把 K 作为最大元素，那么和将是 1，如果给我们的 S 是零，会怎么样。所以我们从 k=1 迭代到数组中的 max 元素加 1。然后用 **K** 相除对数组元素求和，如果和不超过 **S** ，那么当前值就是答案。这种方法的时间复杂度为 **O(M * N)** ，其中 **M** 是数组中最大的元素。
**高效方法:**高效方法是通过对答案执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来找到 **K** 的值。对 **K** 的值进行二分搜索法运算，并检查其内部是否超过 **K** ，然后对后半部分或前半部分进行二分搜索法运算。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum value of k
// that satisfies the given condition
int findMinimumK(int a[], int n, int s)
{
    // Find the maximum element
    int maximum = a[0];
    for (int i = 0; i < n; i++) {
        maximum = max(maximum, a[i]);
    }

    // Lowest answer can be 1 and the
    // highest answer can be (maximum + 1)
    int low = 1, high = maximum + 1;

    int ans = high;

    // Binary search
    while (low <= high) {

        // Get the mid element
        int mid = (low + high) / 2;
        int sum = 0;

        // Calculate the sum after dividing
        // the array by new K which is mid
        for (int i = 0; i < n; i++) {
            sum += (int)(a[i] / mid);
        }

        // Search in the second half
        if (sum > s)
            low = mid + 1;

        // First half
        else {
            ans = min(ans, mid);
            high = mid - 1;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int a[] = { 10, 7, 8, 10, 12, 19 };
    int n = sizeof(a) / sizeof(a[0]);
    int s = 27;

    cout << findMinimumK(a, n, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the minimum value of k
    // that satisfies the given condition
    static int findMinimumK(int a[],
                            int n, int s)
    {
        // Find the maximum element
        int maximum = a[0];

        for (int i = 0; i < n; i++)
        {
            maximum = Math.max(maximum, a[i]);
        }

        // Lowest answer can be 1 and the
        // highest answer can be (maximum + 1)
        int low = 1, high = maximum + 1;

        int ans = high;

        // Binary search
        while (low <= high)
        {

            // Get the mid element
            int mid = (low + high) / 2;
            int sum = 0;

            // Calculate the sum after dividing
            // the array by new K which is mid
            for (int i = 0; i < n; i++)
            {
                sum += (int)(a[i] / mid);
            }

            // Search in the second half
            if (sum > s)
                low = mid + 1;

            // First half
            else
            {
                ans = Math.min(ans, mid);
                high = mid - 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 10, 7, 8, 10, 12, 19 };
        int n = a.length;
        int s = 27;

        System.out.println(findMinimumK(a, n, s));
    }
}   

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum value of k
# that satisfies the given condition
def findMinimumK(a, n, s):

    # Find the maximum element
    maximum = a[0]
    for i in range(n):
        maximum = max(maximum, a[i])

    # Lowest answer can be 1 and the
    # highest answer can be (maximum + 1)
    low = 1
    high = maximum + 1

    ans = high

    # Binary search
    while (low <= high):

        # Get the mid element
        mid = (low + high) // 2
        sum = 0

        # Calculate the sum after dividing
        # the array by new K which is mid
        for i in range(n):
            sum += (a[i] // mid)

        # Search in the second half
        if (sum > s):
            low = mid + 1

        # First half
        else:
            ans = min(ans, mid)
            high = mid - 1

    return ans

# Driver code
a = [10, 7, 8, 10, 12, 19]
n = len(a)
s = 27

print(findMinimumK(a, n, s))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum value of k
    // that satisfies the given condition
    static int findMinimumK(int []a,
                            int n, int s)
    {
        // Find the maximum element
        int maximum = a[0];

        for (int i = 0; i < n; i++)
        {
            maximum = Math.Max(maximum, a[i]);
        }

        // Lowest answer can be 1 and the
        // highest answer can be (maximum + 1)
        int low = 1, high = maximum + 1;

        int ans = high;

        // Binary search
        while (low <= high)
        {

            // Get the mid element
            int mid = (low + high) / 2;
            int sum = 0;

            // Calculate the sum after dividing
            // the array by new K which is mid
            for (int i = 0; i < n; i++)
            {
                sum += (int)(a[i] / mid);
            }

            // Search in the second half
            if (sum > s)
                low = mid + 1;

            // First half
            else
            {
                ans = Math.Min(ans, mid);
                high = mid - 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []a = { 10, 7, 8, 10, 12, 19 };
        int n = a.Length;
        int s = 27;

        Console.WriteLine(findMinimumK(a, n, s));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach    
// Function to return the minimum value of k
    // that satisfies the given condition
    function findMinimumK(a , n , s) {
        // Find the maximum element
        var maximum = a[0];

        for (i = 0; i < n; i++) {
            maximum = Math.max(maximum, a[i]);
        }

        // Lowest answer can be 1 and the
        // highest answer can be (maximum + 1)
        var low = 1, high = maximum + 1;

        var ans = high;

        // Binary search
        while (low <= high) {

            // Get the mid element
            var mid = parseInt((low + high) / 2);
            var sum = 0;

            // Calculate the sum after dividing
            // the array by new K which is mid
            for (i = 0; i < n; i++) {
                sum += parseInt( (a[i] / mid));
            }

            // Search in the second half
            if (sum > s)
                low = mid + 1;

            // First half
            else {
                ans = Math.min(ans, mid);
                high = mid - 1;
            }
        }
        return ans;
    }

    // Driver code

        var a = [ 10, 7, 8, 10, 12, 19 ];
        var n = a.length;
        var s = 27;

        document.write(findMinimumK(a, n, s));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N*(log N))，N =数组长度

**辅助空间:** O(1)
# 每次仅通过减少 K 使数组元素相等的最小减量操作

> 原文:[https://www . geeksforgeeks . org/最小-减量-运算-生成数组-元素-每次只等减-k/](https://www.geeksforgeeks.org/minimum-decrement-operations-to-make-array-elements-equal-by-only-decreasing-k-each-time/)

给定一个由正整数和整数 **K** 组成的大小为 **N** 的数组 **arr[]** ，任务是找到使数组的所有元素相等所需的最小步数，以便在每一步中，可以从数组中选择一个值并递减 **K** 。如果数组不能相等，则打印-1。
**举例:**

> **输入:** arr[] = {12，9，15}，K = 3
> **输出:** 3
> **解释:**
> 最初:{12，9，15}
> 从位置 3 的 15 开始递减 K 后:【12，9，12】
> 从位置 1 的 12 开始递减 K 后:【9，9，12】
> 从位置 3 的 12 开始递减 K 后:【9，9】

**方法:**想法是保持最小值元素不受影响，并计算其他元素为达到该最小值而进行的减量操作的次数。可以按照以下步骤计算结果:

1.  求数组中的最小元素 **minx** 。
2.  一旦找到最小值，变量**递减**并保持初始化为 0。
3.  然后在所有元素上运行一个循环，将 **(arr[i]-minx)/K** 添加到**递减**变量中。
4.  如果遇到任何 arr[i]使得 **arr[i]-minx** 不能被 K 整除，那么返回 **-1** ，因为它不能被减少到最小值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

#define lli long long int

lli solve(lli arr[], lli n, lli k)
{
    lli i, minx = INT_MAX;

    // Finding the minimum element
    for (i = 0; i < n; i++) {
        minx = min(minx, arr[i]);
    }

    lli decrements = 0;

    // Loop over all the elements
    // and find the difference
    for (i = 0; i < n; i++) {
        if ((arr[i] - minx) % k != 0) {
            return -1;
        }
        else {
            decrements += ((arr[i] - minx) / k);
        }
    }
    // Solution found and returned
    return decrements;
}

// Driver code
int main()
{
    lli n, k;
    n = 3;
    k = 3;
    lli arr[n] = { 12, 9, 15 };

    cout << solve(arr, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    static int INT_MAX = Integer.MAX_VALUE ;

    static int solve(int arr[], int n, int k)
    {
        int minx = INT_MAX;
        int i;

        // Finding the minimum element
        for (i = 0; i < n; i++)
        {
            minx = Math.min(minx, arr[i]);
        }

        int decrements = 0;

        // Loop over all the elements
        // and find the difference
        for (i = 0; i < n; i++)
        {
            if ((arr[i] - minx) % k != 0)
            {
                return -1;
            }
            else
            {
                decrements += ((arr[i] - minx) / k);
            }
        }

        // Solution found and returned
        return decrements;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n, k;
        n = 3;
        k = 3;
        int arr[] = { 12, 9, 15 };

        System.out.println(solve(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import sys

def solve(arr, n, k) :

    minx = sys.maxsize;

    # Finding the minimum element
    for i in range(n) :
        minx = min(minx, arr[i]);

    decrements = 0;

    # Loop over all the elements
    # and find the difference
    for i in range(n) :
        if ((arr[i] - minx) % k != 0) :
            return -1;

        else :
            decrements += ((arr[i] - minx) // k);

    # Solution found and returned
    return decrements;

# Driver code
if __name__ == "__main__" :

    n = 3;
    k = 3;
    arr = [ 12, 9, 15 ];

    print(solve(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int INT_MAX = int.MaxValue ;

    static int solve(int []arr, int n, int k)
    {
        int minx = INT_MAX;
        int i;

        // Finding the minimum element
        for (i = 0; i < n; i++)
        {
            minx = Math.Min(minx, arr[i]);
        }

        int decrements = 0;

        // Loop over all the elements
        // and find the difference
        for (i = 0; i < n; i++)
        {
            if ((arr[i] - minx) % k != 0)
            {
                return -1;
            }
            else
            {
                decrements += ((arr[i] - minx) / k);
            }
        }

        // Solution found and returned
        return decrements;
    }

    // Driver code
    public static void Main()
    {
        int n, k;
        n = 3;
        k = 3;
        int []arr = { 12, 9, 15 };

        Console.WriteLine(solve(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the above approach
var INT_MAX = Number.MAX_VALUE;

    function solve(arr , n , k) {
        var minx = INT_MAX;
        var i;

        // Finding the minimum element
        for (i = 0; i < n; i++) {
            minx = Math.min(minx, arr[i]);
        }

        var decrements = 0;

        // Loop over all the elements
        // and find the difference
        for (i = 0; i < n; i++) {
            if ((arr[i] - minx) % k != 0)
            {
                return -1;
            }
            else
            {
                decrements += ((arr[i] - minx) / k);
            }
        }

        // Solution found and returned
        return decrements;
    }

    // Driver code
        var n, k;
        n = 3;
        k = 3;
        var arr = [ 12, 9, 15 ];

        document.write(solve(arr, n, k));

// This code is contributed by Rajput-Ji.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)
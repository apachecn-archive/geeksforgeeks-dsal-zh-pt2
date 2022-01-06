# 最多移除一个元素后严格递增子阵列的最大长度

> 原文:[https://www . geeksforgeeks . org/最多移除一个元素后的严格递增子数组的最大长度/](https://www.geeksforgeeks.org/maximum-length-of-strictly-increasing-sub-array-after-removing-at-most-one-element/)

给定一个数组 **arr[]** ，任务是最多移除一个元素，并计算严格递增子数组的最大长度。

**示例:**

> **输入:** arr[] = {1，2，5，3，4}
> **输出:** 4
> 删除 5 后，得到的数组将为{1，2，3，4}
> ，其严格递增子数组的最大长度为 4。
> 
> **输入:** arr[] = {1，2}
> **输出:** 2
> 全阵已经在严格增加。

**进场:**

*   创建两个大小为 n 的数组 **pre[]** 和 **pos[]**
*   从(0，N)开始迭代输入数组 **arr[]** ，找出当前元素 **arr[i]** 在数组中的贡献，直到现在[0，i]，如果它在严格增加的子数组中有贡献，则更新 **pre[]** 数组。
*   从[N–2，0]开始迭代输入数组 **arr[]** ，找出当前元素 **arr[j]** 在数组中到现在(N，j)的贡献，如果 **arr[j]** 在最长的递增子数组中有贡献，则更新 **pos[]** 数组。
*   在不移除任何元素的情况下，计算急剧增加的子阵列的最大长度。
*   迭代数组 **pre[]** 和 **pos[]** ，通过排除当前元素找出该元素的贡献。
*   保持一个变量**和**来查找到目前为止找到的最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum length of
// strictly increasing subarray after
// removing atmost one element
int maxIncSubarr(int a[], int n)
{
    // Create two arrays pre and pos
    int pre[n] = { 0 };
    int pos[n] = { 0 };
    pre[0] = 1;
    pos[n - 1] = 1;
    int l = 0;

    // Find out the contribution of the current
    // element in array[0, i] and update pre[i]
    for (int i = 1; i < n; i++) {
        if (a[i] > a[i - 1])
            pre[i] = pre[i - 1] + 1;
        else
            pre[i] = 1;
    }

    // Find out the contribution of the current
    // element in array[N - 1, i] and update pos[i]
    l = 1;
    for (int i = n - 2; i >= 0; i--) {
        if (a[i] < a[i + 1])
            pos[i] = pos[i + 1] + 1;
        else
            pos[i] = 1;
    }

    // Calculate the maximum length of the
    // stricly increasing subarray without
    // removing any element
    int ans = 0;
    l = 1;
    for (int i = 1; i < n; i++) {
        if (a[i] > a[i - 1])
            l++;
        else
            l = 1;
        ans = max(ans, l);
    }

    // Calculate the maximum length of the
    // strictly increasing subarray after
    // removing the current element
    for (int i = 1; i <= n - 2; i++) {
        if (a[i - 1] < a[i + 1])
            ans = max(pre[i - 1] + pos[i + 1], ans);
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxIncSubarr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the maximum length of
    // strictly increasing subarray after
    // removing atmost one element
    static int maxIncSubarr(int a[], int n)
    {
        // Create two arrays pre and pos
        int pre[] = new int[n] ;
        int pos[] = new int[n] ;
        pre[0] = 1;
        pos[n - 1] = 1;
        int l = 0;

        // Find out the contribution of the current
        // element in array[0, i] and update pre[i]
        for (int i = 1; i < n; i++)
        {
            if (a[i] > a[i - 1])
                pre[i] = pre[i - 1] + 1;
            else
                pre[i] = 1;
        }

        // Find out the contribution of the current
        // element in array[N - 1, i] and update pos[i]
        l = 1;
        for (int i = n - 2; i >= 0; i--)
        {
            if (a[i] < a[i + 1])
                pos[i] = pos[i + 1] + 1;
            else
                pos[i] = 1;
        }

        // Calculate the maximum length of the
        // stricly increasing subarray without
        // removing any element
        int ans = 0;
        l = 1;
        for (int i = 1; i < n; i++)
        {
            if (a[i] > a[i - 1])
                l++;
            else
                l = 1;
            ans = Math.max(ans, l);
        }

        // Calculate the maximum length of the
        // strictly increasing subarray after
        // removing the current element
        for (int i = 1; i <= n - 2; i++)
        {
            if (a[i - 1] < a[i + 1])
                ans = Math.max(pre[i - 1] +
                                pos[i + 1], ans);
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {1, 2};
        int n = arr.length;

        System.out.println(maxIncSubarr(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the maximum length of
# strictly increasing subarray after
# removing atmost one element
def maxIncSubarr(a, n):

    # Create two arrays pre and pos
    pre = [0] * n;
    pos = [0] * n;
    pre[0] = 1;
    pos[n - 1] = 1;
    l = 0;

    # Find out the contribution of the current
    # element in array[0, i] and update pre[i]
    for i in range(1, n):
        if (a[i] > a[i - 1]):
            pre[i] = pre[i - 1] + 1;
        else:
            pre[i] = 1;

    # Find out the contribution of the current
    # element in array[N - 1, i] and update pos[i]
    l = 1;
    for i in range(n - 2, -1, -1):
        if (a[i] < a[i + 1]):
            pos[i] = pos[i + 1] + 1;
        else:
            pos[i] = 1;

    # Calculate the maximum length of the
    # stricly increasing subarray without
    # removing any element
    ans = 0;
    l = 1;
    for i in range(1, n):
        if (a[i] > a[i - 1]):
            l += 1;
        else:
            l = 1;
        ans = max(ans, l);

    # Calculate the maximum length of the
    # strictly increasing subarray after
    # removing the current element
    for i in range(1, n - 1):
        if (a[i - 1] < a[i + 1]):
            ans = max(pre[i - 1] + pos[i + 1], ans);

    return ans;

# Driver code
if __name__ == '__main__':
    arr = [ 1, 2 ];
    n = len(arr);

    print(maxIncSubarr(arr, n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum length of
    // strictly increasing subarray after
    // removing atmost one element
    static int maxIncSubarr(int []a, int n)
    {
        // Create two arrays pre and pos
        int []pre = new int[n] ;
        int []pos = new int[n] ;
        pre[0] = 1;
        pos[n - 1] = 1;
        int l = 0;

        // Find out the contribution of the current
        // element in array[0, i] and update pre[i]
        for (int i = 1; i < n; i++)
        {
            if (a[i] > a[i - 1])
                pre[i] = pre[i - 1] + 1;
            else
                pre[i] = 1;
        }

        // Find out the contribution of the current
        // element in array[N - 1, i] and update pos[i]
        l = 1;
        for (int i = n - 2; i >= 0; i--)
        {
            if (a[i] < a[i + 1])
                pos[i] = pos[i + 1] + 1;
            else
                pos[i] = 1;
        }

        // Calculate the maximum length of the
        // stricly increasing subarray without
        // removing any element
        int ans = 0;
        l = 1;
        for (int i = 1; i < n; i++)
        {
            if (a[i] > a[i - 1])
                l++;
            else
                l = 1;
            ans = Math.Max(ans, l);
        }

        // Calculate the maximum length of the
        // strictly increasing subarray after
        // removing the current element
        for (int i = 1; i <= n - 2; i++)
        {
            if (a[i - 1] < a[i + 1])
                ans = Math.Max(pre[i - 1] +
                                pos[i + 1], ans);
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 2};
        int n = arr.Length;

        Console.WriteLine(maxIncSubarr(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum length of
// strictly increasing subarray after
// removing atmost one element
function maxIncSubarr(a, n)
{

    // Create two arrays pre and pos
    let pre = new Array(n);
    let pos = new Array(n);
    pre.fill(0);
    pos.fill(0);
    pre[0] = 1;
    pos[n - 1] = 1;
    let l = 0;

    // Find out the contribution of the current
    // element in array[0, i] and update pre[i]
    for(let i = 1; i < n; i++)
    {
        if (a[i] > a[i - 1])
            pre[i] = pre[i - 1] + 1;
        else
            pre[i] = 1;
    }

    // Find out the contribution of the current
    // element in array[N - 1, i] and update pos[i]
    l = 1;
    for(let i = n - 2; i >= 0; i--)
    {
        if (a[i] < a[i + 1])
            pos[i] = pos[i + 1] + 1;
        else
            pos[i] = 1;
    }

    // Calculate the maximum length of the
    // stricly increasing subarray without
    // removing any element
    let ans = 0;
    l = 1;
    for(let i = 1; i < n; i++)
    {
        if (a[i] > a[i - 1])
            l++;
        else
            l = 1;
        ans = Math.max(ans, l);
    }

    // Calculate the maximum length of the
    // strictly increasing subarray after
    // removing the current element
    for(let i = 1; i <= n - 2; i++)
    {
        if (a[i - 1] < a[i + 1])
            ans = Math.max(pre[i - 1] +
                           pos[i + 1], ans);
    }
    return ans;
}

// Driver code
let arr = [ 1, 2 ];
let n = arr.length;

document.write(maxIncSubarr(arr, n));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)

**空间复杂度:** O(N)
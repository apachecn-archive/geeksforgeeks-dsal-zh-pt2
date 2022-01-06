# 翻转 M ^ 0 后，最大化任意两个连续 1 之间的距离

> 原文:[https://www . geeksforgeeks . org/最大化-翻转后任意两个连续 1 之间的距离-m-0s/](https://www.geeksforgeeks.org/maximize-distance-between-any-two-consecutive-1s-after-flipping-m-0s/)

给定一个二进制数组的大小，该数组仅由 0 作为 **n** 和一个整数 **m** 组成，该整数是从 0 到 1 允许的翻转次数；任务是在将 **m** 0 翻转为 1 后，最大化任意两个连续 1 之间的距离

**示例:**

> **输入:** n = 5，m = 3
> **输出:** 2
> **解释:**
> 初始数组为 arr = {0，0，0，0，0}，
> 最终数组为 arr = {1，0，1，0，1}，
> 所以两个连续 1 之间的距离为 2。
> **输入:** n = 9，m = 3
> **输出:** 4
> **解释:**
> 初始数组为 arr = {0，0，0，0，0，0，0，0，0，0}，
> 最终数组为 arr = {1，0，0，0，1，0，0，1}，
> 所以两个连续的 1 之间的距离为 4。

**进场:**

*   我们可以简单地在任意两个连续的 1 之间的距离上[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，并检查我们是否可以将 0 的 **m** 个数字翻转为 1。
*   首先，我们设置低= 1，高= n–1，
*   然后检查 mid =(低+高)/2 是否是合适的距离。
*   如果是，则更新的答案为中，否则降低高=中–1。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to Maximize distance between
// any two consecutive 1's after flipping M 0's

#include <bits/stdc++.h>
using namespace std;

// Function to return the count
bool check(int arr[], int n, int m, int d)
{
    // Flipping zeros at distance "d"
    int i = 0;
    while (i < n && m > 0) {
        m--;
        i += d;
    }

    return m == 0 ? true : false;
}

// Function to implement
// binary search
int maximumDistance(int arr[], int n, int m)
{

    int low = 1, high = n - 1;
    int ans = 0;

    while (low <= high) {

        int mid = (low + high) / 2;

        // Check for valid distance i.e mid
        bool flag = check(arr, n, m, mid);

        if (flag) {
            ans = mid;
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return ans;
}

// Driver code
int main()
{

    int n = 5, m = 3;
    int arr[n] = { 0 };

    cout << maximumDistance(arr, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Maximize distance between
// any two consecutive 1's after flipping M 0's

class GFG
{

    // Function to return the count
    static boolean check(int arr[], int n, int m, int d)
    {

        // Flipping zeros at distance "d"
        int i = 0;
        while (i < n && m > 0)
        {
            m--;
            i += d;
        }

        return m == 0 ? true : false;
    }

    // Function to implement
    // binary search
    static int maximumDistance(int arr[], int n, int m)
    {

        int low = 1, high = n - 1;
        int ans = 0;

        while (low <= high)
        {

            int mid = (low + high) / 2;

            // Check for valid distance i.e mid
            boolean flag = check(arr, n, m, mid);

            if (flag)
            {
                ans = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 5, m = 3;
        int arr[] = new int[n];

        System.out.print(maximumDistance(arr, n, m));

    }
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python3 program to Maximize distance between
# any two consecutive 1's after flipping M 0's

# Function to return the count
def check(arr, n, m, d):

    # Flipping zeros at distance "d"
    i = 0
    while (i < n and m > 0):
        m -= 1
        i += d
    if m == 0:
        return True

    return False

# Function to implement
# binary search
def maximumDistance(arr, n, m):

    low = 1
    high = n - 1
    ans = 0

    while (low <= high):

        mid = (low + high) // 2

        # Check for valid distance i.e mid
        flag = check(arr, n, m, mid)

        if (flag) :
            ans = mid
            low = mid + 1
        else :
            high = mid - 1

    return ans

# Driver code

n = 5
m = 3
arr = [0] * n

print(maximumDistance(arr, n, m))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to Maximize distance between
// any two consecutive 1's after flipping M 0's
using System;

class GFG
{

    // Function to return the count
    static bool check(int []arr, int n, int m, int d)
    {

        // Flipping zeros at distance "d"
        int i = 0;
        while (i < n && m > 0)
        {
            m--;
            i += d;
        }

        return m == 0 ? true : false;
    }

    // Function to implement
    // binary search
    static int maximumDistance(int []arr, int n, int m)
    {

        int low = 1, high = n - 1;
        int ans = 0;

        while (low <= high)
        {

            int mid = (low + high) / 2;

            // Check for valid distance i.e mid
            bool flag = check(arr, n, m, mid);

            if (flag)
            {
                ans = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {

        int n = 5, m = 3;
        int []arr = new int[n];

        Console.Write(maximumDistance(arr, n, m));

    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
//Javascript program to Maximize distance between
// any two consecutive 1's after flipping M 0's

// Function to return the count
function check(arr, n, m, d)
{
    // Flipping zeros at distance "d"
    var i = 0;
    while (i < n && m > 0) {
        m--;
        i += d;
    }

    return m == 0 ? true : false;
}

// Function to implement
// binary search
function maximumDistance(arr, n, m)
{

    var low = 1, high = n - 1;
    var ans = 0;

    while (low <= high) {

        var mid = parseInt( (low + high) / 2);

        // Check for valid distance i.e mid
        var flag = check(arr, n, m, mid);

        if (flag) {
            ans = mid;
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return ans;
}

var  n = 5, m = 3;
var arr = new Array(n);
arr.fill(0);
document.write(  maximumDistance(arr, n, m));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n*log(n))
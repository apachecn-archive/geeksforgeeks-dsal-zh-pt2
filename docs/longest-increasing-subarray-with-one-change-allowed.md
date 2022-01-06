# 允许一次改变的最长增加子阵列

> 原文:[https://www . geeksforgeeks . org/允许一次改变的最长增加子阵列/](https://www.geeksforgeeks.org/longest-increasing-subarray-with-one-change-allowed/)

给定一个数组，找到最长的递增子数组(连续元素)的长度，这样就可以从序列中最多改变一个数字(将一个数字改变为任意整数)，使序列严格递增。

**示例:**

```
Input  : 6
         7 2 3 1 5 10 
Output : 5
Explanation : 
Here, we can choose subarray 2, 3, 1, 5, 10 
and by changing its 3rd element (that is 1) 
to 4, it will become increasing sequence.

Input  : 2
         10 10
Output : 2
Explanation : 
Here, we can choose subarray 10, 10 and by
changing its 2nd element (that is 10) to 11,
it will become increasing sequence.
```

**进场:**

步骤 1:我们首先为给定数组中的每个索引计算以索引结束的最长递增子数组。我们将这些值存储在 l[]中。
步骤 2:然后为给定数组中的每个索引计算从一个索引开始的最长递增子数组。我们将这些值存储在 r[]中。
第三步:更新答案 ans = max ( ans，l[i-1] + r[i+1] + 1)，当 a[i-1] + 1 时< a[i+1]。

下面是上述想法的实现:

## C++

```
// CPP program to find longest increasing subarray
// with one change allowed.
#include <bits/stdc++.h>
using namespace std;

// Function to find length of
// subsequence
int seg(int a[], int n)
{
    int l[n], r[n + 1], ans = 0;

    // calculating the l array.
    l[0] = 1;
    for (int i = 1; i < n; i++)
    {
        if (a[i] > a[i - 1])
        {
            l[i] = l[i - 1] + 1;
            ans = max(ans, l[i]);
        }
        else
            l[i] = 1;
    }
    if (ans != n)
        ++ans;

    // calculating the r array.
    r[n] = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        if (a[i] < a[i + 1])
            r[i] = r[i + 1] + 1;
        else
            r[i] = 1;
    }

    // updating the answer.
    for (int i = n - 2; i > 0; i--)
    {
        if (a[i + 1] - a[i - 1] > 1)
            ans = max(ans, l[i - 1] + r[i + 1] + 1);
    }

    return max(ans, r[0]);
}

// Driver code.
int main()
{
    int a[] = { 9, 4, 5, 1, 13 };
    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << seg(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest increasing subarray
// with one change allowed.
class GFG
{

    // Function to find length of
    // subsequence
    static int seg(int[] a, int n)
    {
        int[] l = new int[n];
        int[] r = new int[n + 1];
        int ans = 0;

        // calculating the l array.
        l[0] = 1;
        for (int i = 1; i < n; i++)
        {
            if (a[i] > a[i - 1])
            {
                l[i] = l[i - 1] + 1;
                ans = Math.max(ans, l[i]);
            }
            else
                l[i] = 1;
        }
        if (ans != n)
            ++ans;

        // calculating the r array.
        r[n] = 0;
        for (int i = n - 1; i > 0; i--)
        {
            if (a[i - 1] < a[i])
                r[i] = r[i + 1] + 1;
            else
                r[i] = 1;
        }

        // updating the answer.
        for (int i = n - 2; i > 0; i--)
        {
            if (a[i + 1] - a[i - 1] > 1)
                ans = Math.max(ans,
                               l[i - 1] + r[i + 1] + 1);
        }
        return Math.max(ans, r[0]);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 9, 4, 5, 1, 13 };
        int n = a.length;

        // Function call
        System.out.println(seg(a, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find
# longest increasing subarray
# with one change allowed.

# Function to find length of
# subsequence
def seg(a, n):

    l = [0] * n
    r = [0] * (n + 1)
    ans = 0

    # calculating the l array.
    l[0] = 1
    for i in range(1, n):
        if (a[i] > a[i - 1]):
            l[i] = l[i - 1] + 1
            ans = max(ans, l[i])
        else:
            l[i] = 1

    if (ans != n):
        ans += 1

    # calculating the
    # r array.
    r[n] = 0
    for i in range(n - 1,
                   -1, -1):
        if (a[i - 1] < a[i]):
            r[i] = r[i + 1] + 1
        else:
            r[i] = 1

    # Updating the answer.
    for i in range(n - 2,
                   0, -1):
        if (a[i + 1] -
            a[i - 1] > 1):
            ans = max(ans, l[i - 1] +
                      r[i + 1] + 1)

    return max(ans, r[0])

# Driver code.
if __name__ == "__main__":

    a = [9, 4, 5, 1, 13]
    n = len(a)

    # Function call
    print(seg(a, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find longest increasing subarray
// with one change allowed.
using System;

class GFG {

    // Function to find length of
    // subsequence
    static int seg(int[] a, int n)
    {
        int[] l = new int[n];
        int[] r = new int[n + 1];
        int ans = 0;

        // calculating the l array.
        l[0] = 1;
        for (int i = 1; i < n; i++)
        {
            if (a[i] > a[i - 1])
            {
                l[i] = l[i - 1] + 1;
                ans = Math.Max(ans, l[i]);
            }
            else
                l[i] = 1;
        }
        if (ans != n)
            ++ans;

        // calculating the r array.
        r[n] = 0;
        for (int i = n - 1; i > 0; i--)
        {
            if (a[i - 1] < a[i])
                r[i] = r[i + 1] + 1;
            else
                r[i] = 1;
        }

        // updating the answer.
        for (int i = n - 2; i > 0; i--)
        {
            if (a[i + 1] - a[i - 1] > 1)
                ans = Math.Max(ans,
                               l[i - 1] + r[i + 1] + 1);
        }
        return Math.Max(ans, r[0]);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = { 9, 4, 5, 1, 13 };
        int n = a.Length;

        // Function call
        Console.WriteLine(seg(a, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find
// longest increasing subarray
// with one change allowed.

    // Function to find length of
    // subsequence
    function seg(a,n)
    {
        let l = new Array(n);
        let r = new Array(n + 1);
        let ans = 0;

        // calculating the l array.
        l[0] = 1;
        for (let i = 1; i < n; i++)
        {
            if (a[i] > a[i - 1])
            {
                l[i] = l[i - 1] + 1;
                ans = Math.max(ans, l[i]);
            }
            else
                l[i] = 1;
        }
        if (ans != n)
            ++ans;

        // calculating the r array.
        r[n] = 0;
        for (let i = n - 1; i >= 0; i--)
        {
            if (a[i - 1] < a[i])
                r[i] = r[i + 1] + 1;
            else
                r[i] = 1;
        }

        // updating the answer.
        for (let i = n - 2; i > 0; i--)
        {
            if (a[i + 1] - a[i - 1] > 1)
                ans = Math.max(ans,
                            l[i - 1] + r[i + 1] + 1);
        }
        return Math.max(ans, r[0]);
    }

    // Driver code.
    let a=[9, 4, 5, 1, 13 ];
    let n = a.length;

    document.write(seg(a, n));

    // This code is contributed by rag2127

</script>
```

**Output**

```
4
```

本文由 [**阿布舍克·夏尔马**](https://auth.geeksforgeeks.org/profile.php?user=Abhishek Sharma 44) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
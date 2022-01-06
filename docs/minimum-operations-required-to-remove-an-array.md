# 移除阵列所需的最小操作数

> 原文:[https://www . geeksforgeeks . org/移除阵列所需的最小操作数/](https://www.geeksforgeeks.org/minimum-operations-required-to-remove-an-array/)

给定 N 个整数的数组，其中 N 是偶数。数组上允许两种操作。

1.  将任何元素 A[i]的值增加 1。
2.  如果数组中两个相邻的元素是连续的素数，则删除这两个元素。即 A[i]是素数，A[i+1]是下一个素数。

任务是找到移除数组中所有元素所需的最小操作数。
**例:**

```
Input  : arr[] = { 1, 2, 4, 3 } 
Output : 5
Minimum 5 operation are required.
1\. Increase the 2nd element by 1
{ 1, 2, 4, 3 } -> { 1, 3, 4, 3 }
2\. Increase the 3rd element by 1
{ 1, 3, 4, 3 } -> { 1, 3, 5, 3 }
3\. Delete the 2nd and 3rd element
{ 1, 3, 5, 3 } -> { 1, 3 }
4\. Increase the 1st element by 1
{ 1, 3 } -> { 2, 3 }
5\. Delete the 1st and 2nd element
{ 2, 3 } -> { }

Input : arr[] = {10, 12}
Output : 3
```

要去掉数字，我们必须把两个数字转换成两个连续的素数。如何计算将两个数 **a，b** 转化为两个连续素数的最小代价，其中代价是两个数的递增数？
我们用筛子预计算素数，然后用数组找到第一个不大于 **a** 的素数 **p** 和第一个大于 **p** 。
一旦我们计算了两个最近的素数，我们就使用动态规划来解决这个问题。设 dp[i][j]为清除子阵列 A[i，j]的最小成本。如果数组中有两个数字，答案很容易找到。现在，对于 N > 2，将位置 k > i 的任意元素作为 A[i]的一对进行尝试，使得 A[i]和 A[k]之间有偶数个来自 A[i，j]的元素。对于固定的 k，清除 A[i，j]的最小成本，即 dp[i][j]，等于 DP[I+1][k–1]+DP[k+1][j]+(将 A[i]和 A[k]转换为连续素数的成本)。我们可以通过迭代所有可能的 k 来计算答案
下面是上述方法的实现:

## C++

```
// C++ program to count minimum operations
// required to remove an array
#include<bits/stdc++.h>
#define MAX 100005
using namespace std;

// Return the cost to convert two numbers into
// consecutive prime number.
int cost(int a, int b, int prev[], int nxt[])
{
    int sub = a + b;

    if (a <= b && prev[b-1] >= a)
        return nxt[b] + prev[b-1] - a - b;

    a = max(a, b);
    a = nxt[a];
    b = nxt[a + 1];

    return a + b - sub;
}

// Sieve to store next and previous prime
// to a number.
void sieve(int prev[], int nxt[])
{
    int pr[MAX] = { 0 };

    pr[1] = 1;
    for (int i = 2; i < MAX; i++)
    {
        if (pr[i])
            continue;

        for (int j = i*2; j < MAX; j += i)
            pr[j] = 1;
    }

    // Computing next prime each number.
    for (int i = MAX - 1; i; i--)
    {
        if (pr[i] == 0)
            nxt[i] = i;
        else
            nxt[i] = nxt[i+1];
    }

    // Computing previous prime each number.
    for (int i = 1; i < MAX; i++)
    {
        if (pr[i] == 0)
            prev[i] = i;
        else
            prev[i] = prev[i-1];
    }
}

// Return the minimum number of operation required.
int minOperation(int arr[], int nxt[], int prev[], int n)
{
    int dp[n + 5][n + 5] = { 0 };

    // For each index.
    for (int r = 0; r < n; r++)
    {
        // Each subarray.
        for (int l = r-1; l >= 0; l -= 2)
        {
            dp[l][r] = INT_MAX;

            for (int ad = l; ad < r; ad += 2)
                dp[l][r] = min(dp[l][r], dp[l][ad] +
                          dp[ad+1][r-1] +
                          cost(arr[ad], arr[r], prev, nxt));
        }
    }

    return dp[0][n - 1] + n/2;
}

// Driven Program
int main()
{
    int arr[] = { 1, 2, 4, 3 };
    int n = sizeof(arr)/sizeof(arr[0]);

    int nxt[MAX], prev[MAX];
    sieve(prev, nxt);

    cout << minOperation(arr, nxt, prev, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum operations
// required to remove an array
class GFG
{

static final int MAX = 100005;

// Return the cost to convert two
// numbers into consecutive prime number.
static int cost(int a, int b,
                int prev[], int nxt[])
{
    int sub = a + b;

    if (a <= b && prev[b - 1] >= a)
    {
        return nxt[b] + prev[b - 1] - a - b;
    }

    a = Math.max(a, b);
    a = nxt[a];
    b = nxt[a + 1];

    return a + b - sub;
}

// Sieve to store next and previous
// prime to a number.
static void sieve(int prev[], int nxt[])
{
    int pr[] = new int[MAX];

    pr[1] = 1;
    for (int i = 2; i < MAX; i++)
    {
        if (pr[i] == 1)
        {
            continue;
        }

        for (int j = i * 2; j < MAX; j += i)
        {
            pr[j] = 1;
        }
    }

    // Computing next prime each number.
    for (int i = MAX - 2; i > 0; i--)
    {
        if (pr[i] == 0)
        {
            nxt[i] = i;
        }
        else
        {
            nxt[i] = nxt[i + 1];
        }
    }

    // Computing previous prime each number.
    for (int i = 1; i < MAX; i++)
    {
        if (pr[i] == 0)
        {
            prev[i] = i;
        }
        else
        {
            prev[i] = prev[i - 1];
        }
    }
}

// Return the minimum number
// of operation required.
static int minOperation(int arr[], int nxt[],
                        int prev[], int n)
{
    int dp[][] = new int[n + 5][n + 5];

    // For each index.
    for (int r = 0; r < n; r++)
    {
        // Each subarray.
        for (int l = r - 1; l >= 0; l -= 2)
        {
            dp[l][r] = Integer.MAX_VALUE;

            for (int ad = l; ad < r; ad += 2)
            {
                dp[l][r] = Math.min(dp[l][r], dp[l][ad] +
                                    dp[ad + 1][r - 1] +
                                    cost(arr[ad], arr[r],
                                            prev, nxt));
            }
        }
    }

    return dp[0][n - 1] + n / 2;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = {1, 2, 4, 3};
    int n = arr.length;

    int nxt[] = new int[MAX], prev[] = new int[MAX];
    sieve(prev, nxt);

    System.out.println(minOperation(arr, nxt, prev, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to count minimum
# operations required to remove an array
MAX = 100005
INT_MAX = 10000000

# Return the cost to convert two numbers
# into consecutive prime number.
def cost(a, b, prev, nxt):
    sub = a + b
    if (a <= b and prev[b - 1] >= a):
        return nxt[b] + prev[b - 1] - a - b

    a = max(a, b)
    a = nxt[a]
    b = nxt[a + 1]
    return a + b - sub

# Sieve to store next and previous
# prime to a number.
def sieve(prev, nxt):
    pr = [0 for i in range(MAX)]

    pr[1] = 1
    for i in range(1, MAX):
        if (pr[i]):
            continue
        for j in range(i * 2, MAX, i):
            pr[j] = 1

    # Computing next prime each number.
    for i in range(MAX - 2, -1, -1):
        if (pr[i] == 0):
            nxt[i] = i
        else:
            nxt[i] = nxt[i + 1]

    # Computing previous prime each number.
    for i in range(1, MAX):
        if (pr[i] == 0):
            prev[i] = i
        else:
            prev[i] = prev[i - 1]

# Return the minimum number of
# operation required.
def minOperation(arr, nxt, prev, n):
    dp = [[0 for i in range(n + 5)]
             for i in range(n + 5)]

    # For each index.
    for r in range(n):

        # Each subarray.
        for l in range(r - 1, -1, -2):
            dp[l][r] = INT_MAX;

            for ad in range(l, r, 2):
                dp[l][r] = min(dp[l][r], dp[l][ad] +
                               dp[ad + 1][r - 1] +
                               cost(arr[ad], arr[r],
                                         prev, nxt))
    return dp[0][n - 1] + n // 2

# Driver Code
arr = [1, 2, 4, 3]
n = len(arr)

nxt = [0 for i in range(MAX)]
prev = [0 for i in range(MAX)]
sieve(prev, nxt)
print(minOperation(arr, nxt, prev, n))

# This code is contributed by sahishelangia
```

## C#

```
// C# program to count minimum operations
// required to remove an array
using System;
class GFG
{

static int MAX = 100005;

// Return the cost to convert two
// numbers into consecutive prime number.
static int cost(int a, int b,
                int[] prev, int[] nxt)
{
    int sub = a + b;

    if (a <= b && prev[b - 1] >= a)
    {
        return nxt[b] + prev[b - 1] - a - b;
    }

    a = Math.Max(a, b);
    a = nxt[a];
    b = nxt[a + 1];

    return a + b - sub;
}

// Sieve to store next and previous
// prime to a number.
static void sieve(int[] prev, int[] nxt)
{
    int[] pr = new int[MAX];

    pr[1] = 1;
    for (int i = 2; i < MAX; i++)
    {
        if (pr[i] == 1)
        {
            continue;
        }

        for (int j = i * 2; j < MAX; j += i)
        {
            pr[j] = 1;
        }
    }

    // Computing next prime each number.
    for (int i = MAX - 2; i > 0; i--)
    {
        if (pr[i] == 0)
        {
            nxt[i] = i;
        }
        else
        {
            nxt[i] = nxt[i + 1];
        }
    }

    // Computing previous prime each number.
    for (int i = 1; i < MAX; i++)
    {
        if (pr[i] == 0)
        {
            prev[i] = i;
        }
        else
        {
            prev[i] = prev[i - 1];
        }
    }
}

// Return the minimum number
// of operation required.
static int minOperation(int[] arr, int[] nxt,
                        int[] prev, int n)
{
    int[,] dp = new int[n + 5, n + 5];

    // For each index.
    for (int r = 0; r < n; r++)
    {
        // Each subarray.
        for (int l = r - 1; l >= 0; l -= 2)
        {
            dp[l, r] = Int32.MaxValue;

            for (int ad = l; ad < r; ad += 2)
            {
                dp[l, r] = Math.Min(dp[l, r], dp[l, ad] +
                                    dp[ad + 1, r - 1] +
                                    cost(arr[ad], arr[r],
                                            prev, nxt));
            }
        }
    }

    return dp[0, n - 1] + n / 2;
}

// Driver Code
public static void Main()
{
    int[] arr = {1, 2, 4, 3};
    int n = arr.Length;

    int[] nxt = new int[MAX];
    int[] prev = new int[MAX];
    sieve(prev, nxt);

    Console.WriteLine(minOperation(arr, nxt, prev, n));
}
}

// This code is contributed by Mukul Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count minimum operations
// required to remove an array

$MAX = 100005;

// Return the cost to convert two numbers into
// consecutive prime number.
function cost($a, $b, &$prev, &$nxt)
{
    $sub = $a + $b;

    if ($a <= $b && $prev[$b-1] >= $a)
        return $nxt[$b] + $prev[$b-1] - $a - $b;

    $a = max($a, $b);
    $a = $nxt[$a];
    $b = $nxt[$a + 1];

    return $a + $b - $sub;
}

// Sieve to store next and previous prime
// to a number.
function sieve(&$prev, &$nxt)
{
    global $MAX;
    $pr = array_fill(0,$MAX,NULL);

    $pr[1] = 1;
    for ($i = 2; $i < $MAX; $i++)
    {
        if ($pr[$i])
            continue;

        for ($j = $i*2; $j < $MAX; $j += $i)
            $pr[$j] = 1;
    }

    // Computing next prime each number.
    for ($i = $MAX - 1; $i; $i--)
    {
        if ($pr[$i] == 0)
            $nxt[$i] = $i;
        else
            $nxt[$i] = $nxt[$i+1];
    }

    // Computing previous prime each number.
    for ($i = 1; $i < $MAX; $i++)
    {
        if ($pr[$i] == 0)
            $prev[$i] = $i;
        else
            $prev[$i] = $prev[$i-1];
    }
}

// Return the minimum number of operation required.
function minOperation(&$arr, &$nxt, &$prev, $n)
{
    global $MAX;
    $dp = array_fill(0,($n + 5),array_fill(0,($n + 5),NULL));

    // For each index.
    for ($r = 0; $r < $n; $r++)
    {
        // Each subarray.
        for ($l = $r-1; $l >= 0; $l -= 2)
        {
            $dp[$l][$r] = PHP_INT_MAX;

            for ($ad = $l; $ad < $r; $ad += 2)
                $dp[$l][$r] = min($dp[$l][$r], $dp[$l][$ad] +
                          $dp[$ad+1][$r-1] +
                          cost($arr[$ad], $arr[$r], $prev, $nxt));
        }
    }

    return $dp[0][$n - 1] + $n/2;
}

// Driven Program

$arr = array( 1, 2, 4, 3 );
$n = sizeof($arr)/sizeof($arr[0]);

$nxt = array_fill(0,$MAX,NULL);
$prev = array_fill(0,$MAX,NULL);
sieve($prev, $nxt);

echo minOperation($arr, $nxt, $prev, $n);

return 0;
?>
```

## java 描述语言

```
<script>
// Javascript program to count minimum operations
// required to remove an array

    let MAX = 100005;

    // Return the cost to convert two
    // numbers into consecutive prime number.
    function cost(a,b,prev,nxt)
    {
        let sub = a + b;

        if (a <= b && prev[b - 1] >= a)
        {
            return nxt[b] + prev[b - 1] - a - b;
        }

        a = Math.max(a, b);
        a = nxt[a];
        b = nxt[a + 1];

        return a + b - sub;
    }

    // Sieve to store next and previous
    // prime to a number.
    function sieve(prev,nxt)
    {
        let pr = new Array(MAX);
        for(let i=0;i<MAX;i++)
        {
            pr[i]=0;
        }

        pr[1] = 1;
        for (let i = 2; i < MAX; i++)
        {
            if (pr[i] == 1)
            {
                continue;
            }

            for (let j = i * 2; j < MAX; j += i)
            {
                pr[j] = 1;
            }
        }

        // Computing next prime each number.
        for (let i = MAX - 2; i > 0; i--)
        {
            if (pr[i] == 0)
            {
                nxt[i] = i;
            }
            else
            {
                nxt[i] = nxt[i + 1];
            }
        }

        // Computing previous prime each number.
        for (let i = 1; i < MAX; i++)
        {
            if (pr[i] == 0)
            {
                prev[i] = i;
            }
            else
            {
                prev[i] = prev[i - 1];
            }
        }
    }

    // Return the minimum number
    // of operation required.
    function minOperation(arr,nxt,prev,n)
    {
        let dp = new Array(n + 5);
        for(let i=0;i<n+5;i++)
        {
            dp[i]=new Array(n+5);
            for(let j=0;j<n+5;j++)
            {
                dp[i][j]=0;
            }

        }

        // For each index.
        for (let r = 0; r < n; r++)
        {
            // Each subarray.
            for (let l = r - 1; l >= 0; l -= 2)
            {
                dp[l][r] = Number.MAX_VALUE;

                for (let ad = l; ad < r; ad += 2)
                {
                    dp[l][r] = Math.min(dp[l][r], dp[l][ad] +
                                        dp[ad + 1][r - 1] +
                                        cost(arr[ad], arr[r],
                                                prev, nxt));
                }
            }
        }

        return dp[0][n - 1] + n / 2;
    }

    // Driver Code
    let arr=[1, 2, 4, 3];
    let n = arr.length;
    let nxt=new Array(MAX);
    let prev=new Array(MAX);
    sieve(prev, nxt);

    document.write(minOperation(arr, nxt, prev, n));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
5
```

**时间复杂度:** O(N <sup>3</sup> )。
**参考:**
[http://stackoverflow . com/questions/42315625/移除数组所需的最小操作数](http://stackoverflow.com/questions/42315625/minimum-operation-required-to-remove-an-array)
本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
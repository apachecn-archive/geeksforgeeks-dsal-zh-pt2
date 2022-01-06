# 从无限字符串的前 N 个字符中仅 4 个字符的最长子字符串

> 原文:[https://www . geeksforgeeks . org/从无限字符串的第一个 n 个字符开始的最长的唯一 4 个子字符串/](https://www.geeksforgeeks.org/longest-substring-of-only-4s-from-the-first-n-characters-of-the-infinite-string/)

给定一个整数 N，任务是从无限字符串 **str** 的第一个 **N** 字符中找出仅包含 **4 的最长子串的长度。
字符串**字符串**是将仅由 **4 的**和 **5 的**组成的数字按递增顺序串联而成。例如 **4** 、 **5** 、 **44** 、 **45** 、 **54** 、 **55** 等等。所以弦**弦**看起来像**“454445545544444545454455……”**。**

**示例:**

```
Input : N = 4 
Output : 2
First 4 characters of str are "4544". 
Therefore the required length is 2.

Input : N = 10
Output : 3
First 10 characters of str are "4544455455". 
Therefore the required length is 3.
```

**做法:**观察模式就能轻松解决问题。任务是计算字符串中出现的最大连续 4。所以，没有必要生成整个字符串。
如果我们将字符串分成不同的组，我们可以观察到一个模式，因为**第一个**组将有 2 个字符，**第二个**组将有 4 个字符，**第三个**组将有 8 个字符，以此类推。

**例如**:

> **第 1 组**->**4**5
> T5】第 2 组->**444**55455
> T10】第 3 组->T12】44444545445545455
> 。
> 。
> 。
> 以此类推……

现在，任务简化为找到 N 所在的组，以及从一开始它在该组中覆盖了多少个字符。
这里，

*   如果 **N** 落在第 2 组，答案至少是 3。也就是说，如果长度= 4，那么答案将是 2，与长度 4 一样，字符串将只覆盖组中的第二个 4，如果长度= 5，答案将是 3。
*   同样，如果**长度**至少覆盖组 3 的前 5 个“4”，则答案为 5。

现在，
组 1 有 1 * 2^1 字符
组 2 有 2 * 2^2 字符
一般来说，组 **K** 有 **K** * 2^ **K** 字符。所以问题归结为找到给定的 **N** 属于哪个组。这很容易通过使用前缀和数组 *pre[]* 找到，其中*with*元素包含直到*with*组的字符数之和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAXN 30

// Function to return the length of longest
// contiguous string containing only 4’s from
// the first N characters of the string
int countMaxLength(int N)
{
    // Initialize result
    int res;

    // Initialize prefix sum array of
    // characters and product variable
    int pre[MAXN], p = 1;

    // Preprocessing of prefix sum array
    pre[0] = 0;
    for (int i = 1; i < MAXN; i++) {
        p *= 2;
        pre[i] = pre[i - 1] + i * p;
    }

    // Initialize variable to store the
    // string length where N belongs to
    int ind;

    // Finding the string length where
    // N belongs to
    for (int i = 1; i < MAXN; i++) {
        if (pre[i] >= N) {
            ind = i;
            break;
        }
    }

    int x = N - pre[ind - 1];
    int y = 2 * ind - 1;

    if (x >= y)
        res = min(x, y);
    else
        res = max(x, 2 * (ind - 2) + 1);

    return res;
}

// Driver Code
int main()
{
    int N = 25;
    cout << countMaxLength(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAXN = 30;

// Function to return the length of longest
// contiguous string containing only 4's from
// the first N characters of the string
static int countMaxLength(int N)
{
    // Initialize result
    int res;

    // Initialize prefix sum array of
    // characters and product variable
    int pre[] = new int[MAXN];
    int p = 1;

    // Preprocessing of prefix sum array
    pre[0] = 0;
    for (int i = 1; i < MAXN; i++)
    {
        p *= 2;
        pre[i] = pre[i - 1] + i * p;
    }

    // Initialize variable to store the
    // string length where N belongs to
    int ind = 0;

    // Finding the string length where
    // N belongs to
    for (int i = 1; i < MAXN; i++)
    {
        if (pre[i] >= N)
        {
            ind = i;
            break;
        }
    }

    int x = N - pre[ind - 1];
    int y = 2 * ind - 1;

    if (x >= y)
        res = Math.min(x, y);
    else
        res = Math.max(x, 2 * (ind - 2) + 1);

    return res;
}

// Driver Code
public static void main(String[] args)
{
    int N = 25;
    System.out.println(countMaxLength(N));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAXN = 30

# Function to return the length of longest
# contiguous string containing only 4’s from
# the first N characters of the string
def countMaxLength(N):

    # Initialize result
    # Initialize prefix sum array of
    # characters and product variable
    pre = [0 for i in range(MAXN)]
    p = 1

    # Preprocessing of prefix sum array
    pre[0] = 0
    for i in range(1, MAXN, 1):
        p *= 2
        pre[i] = pre[i - 1] + i * p

    # Initialize variable to store the
    # string length where N belongs to

    # Finding the string length where
    # N belongs to
    for i in range(1, MAXN, 1):
        if (pre[i] >= N):
            ind = i
            break

    x = N - pre[ind - 1]
    y = 2 * ind - 1

    if (x >= y):
        res = min(x, y)
    else:
        res = max(x, 2 * (ind - 2) + 1)
    return res

# Driver Code
if __name__ == '__main__':
    N = 25
    print(countMaxLength(N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAXN = 30;

// Function to return the length of longest
// contiguous string containing only 4's from
// the first N characters of the string
static int countMaxLength(int N)
{
    // Initialize result
    int res;

    // Initialize prefix sum array of
    // characters and product variable
    int[] pre = new int[MAXN];
    int p = 1;

    // Preprocessing of prefix sum array
    pre[0] = 0;
    for (int i = 1; i < MAXN; i++)
    {
        p *= 2;
        pre[i] = pre[i - 1] + i * p;
    }

    // Initialize variable to store the
    // string length where N belongs to
    int ind = 0;

    // Finding the string length where
    // N belongs to
    for (int i = 1; i < MAXN; i++)
    {
        if (pre[i] >= N)
        {
            ind = i;
            break;
        }
    }

    int x = N - pre[ind - 1];
    int y = 2 * ind - 1;

    if (x >= y)
        res = Math.Min(x, y);
    else
        res = Math.Max(x, 2 * (ind - 2) + 1);

    return res;
}

// Driver Code
public static void Main()
{
    int N = 25;
    Console.WriteLine(countMaxLength(N));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAXN = 30;

// Function to return the length of longest
// contiguous string containing only 4’s from
// the first N characters of the string
function countMaxLength($N)
{
    // Initialize result
    $res = 0;

    // Initialize prefix sum array of
    // characters and product variable
    $pre = array();
    $p = 1;

    // Preprocessing of prefix sum array
    $pre[0] = 0;
    for ($i = 1; $i < $GLOBALS['MAXN']; $i++)
    {
        $p *= 2;
        $pre[$i] = $pre[$i - 1] + $i * $p;
    }

    // Initialize variable to store the
    // string length where N belongs to
    $ind = 0;

    // Finding the string length where
    // N belongs to
    for ($i = 1; $i < $GLOBALS['MAXN']; $i++)
    {
        if ($pre[$i] >= $N)
        {
            $ind = $i;
            break;
        }
    }

    $x = $N - $pre[$ind - 1];
    $y = 2 * $ind - 1;

    if ($x >= $y)
        $res = min($x, $y);
    else
        $res = max($x, 2 * ($ind - 2) + 1);

    return $res;
}

// Driver Code
$N = 25;
echo countMaxLength($N);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var MAXN = 30;

// Function to return the length of longest
// contiguous string containing only 4’s from
// the first N characters of the string
function countMaxLength(N)
{

    // Initialize result
    var res;

    // Initialize prefix sum array of
    // characters and product variable
    var pre = Array(MAXN), p = 1;

    // Preprocessing of prefix sum array
    pre[0] = 0;
    for(var i = 1; i < MAXN; i++)
    {
        p *= 2;
        pre[i] = pre[i - 1] + i * p;
    }

    // Initialize variable to store the
    // string length where N belongs to
    var ind;

    // Finding the string length where
    // N belongs to
    for(var i = 1; i < MAXN; i++)
    {
        if (pre[i] >= N)
        {
            ind = i;
            break;
        }
    }

    var x = N - pre[ind - 1];
    var y = 2 * ind - 1;

    if (x >= y)
        res = Math.min(x, y);
    else
        res = Math.max(x, 2 * (ind - 2) + 1);

    return res;
}

// Driver Code
var N = 25;

document.write(countMaxLength(N));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
5
```
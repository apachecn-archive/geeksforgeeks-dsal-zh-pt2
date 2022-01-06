# 相邻元素差值的最大和

> 原文:[https://www . geesforgeks . org/max-sum-difference-neighbor-elements/](https://www.geeksforgeeks.org/maximum-sum-difference-adjacent-elements/)

给定一个数 n，我们必须找到 n 的所有置换的最大和，最大和将是数组中相邻元素的绝对差之和。

示例:

```
Input : 3
Output : 3
Permutations of size 3 are:
{1, 2, 3} = 1 + 1
{1, 3, 2} = 2 + 1
{2, 1, 3} = 1 + 2
{2, 3, 1} = 1 + 2
{3, 1, 2} = 2 + 1
{3, 2, 1} = 1 + 1

Input : 2
Output : 1
Permutations of 2 are:
{1, 2} = 1
{2, 1} = 1 
```

让我们以 n = 5 为例。我们可以很容易地看到，我们可以放置像 1 5 2 4 3 这样的数字。
ABS(1-5)= 4
ABS(5-2)= 3
ABS(2-4)= 2
ABS(4-3)= 1
其和为 4 + 3 + 2 + 1 = 10。
一般来说，这个排列的和是 n(n-1)/2。
但是如果我们在这个置换的开始移动 3
即 3 1 5 2 4，就可以得到最大和。
总和将变为 2 + 4 + 3 + 2 = 11。
最终关系= n(n–1)/2–1+n/2 为 n > 1。
具有最大和的 n 的排列将是从 n/2，n-1，2，n-2，3，n-3。
所以我们要求这个置换的和，就是 n(n-1)/2–1+n/2。

下面是上述方法的实现。

## C++

```
// CPP program to find maximum sum of
// adjacent elements of permutation of n
#include <iostream>
using namespace std;

// To find max sum of permutation
int maxSum(int n)
{
    // Base case
    if (n == 1)
        return 1;

    // Otherwise max sum will
    // be (n*(n-1)/2) - 1 + n/2
    else
        return (n * (n - 1) / 2) - 1 + n / 2;
}

// Driver program to test maxSum()
int main()
{
    int n = 3;
    cout << maxSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum of
// adjacent elements of permutation of n
public class Main {

    // To find max sum of permutation
    static int maxSum(int n)
    {
        // Base case
        if (n == 1)
            return 1;

        // Otherwise max sum will
        // be (n*(n-1)/2) - 1 + n/2
        else
            return (n * (n - 1) / 2) - 1 + n / 2;
    }

    // Driver program to test maxSum()
    public static void main(String[] args)
    {
        int n = 3;
        System.out.println(maxSum(n));
    }
}
```

## 蟒蛇 3

```
# Python program to find maximum sum of
# adjacent elements of permutation of n

# To find max sum of permutation
def maxSum(n):

    # Base case
    if (n == 1):
        return 1

    # Otherwise max sum will
    # be (n*(n-1)/2) - 1 + n / 2
    else:
        return int((n * (n - 1) / 2) - 1 + n / 2)

# Driver program to test maxSum()
n = 3
print(maxSum(n))

# This code is contributed
# by Azkia Anam.
```

## C#

```
// C# program to find maximum sum of
// adjacent elements of permutation of n
using System;

public class main {

    // To find max sum of permutation
    static int maxSum(int n)
    {

        // Base case
        if (n == 1)
            return 1;

        // Otherwise max sum will
        // be (n*(n-1)/2) - 1 + n/2
        else
            return (n * (n - 1) / 2)
                           - 1 + n / 2;
    }

    // Driver program to test maxSum()
    public static void Main()
    {
        int n = 3;

        Console.WriteLine(maxSum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum sum of
// adjacent elements of permutation of n
// To find max sum of permutation
function maxSum( $n)
{
    // Base case
    if ($n == 1)
        return 1;

    // Otherwise max sum will
    // be (n*(n-1)/2) - 1 + n/2
    else
        return ($n * ($n - 1) / 2) -
                        1 + $n / 2;
}

    // Driver Code
    $n = 3;
    echo intval( maxSum($n));

// This code is contributed by akur
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum sum of
// adjacent elements of permutation of n

// To find max sum of permutation
function maxSum(n)
{

    // Base case
    if (n == 1)
        return 1;

    // Otherwise max sum will
    // be (n*(n-1)/2) - 1 + n/2
    else
        return(parseInt(n * (n - 1) / 2, 10) - 1 +
               parseInt(n / 2, 10));
}

// Driver code
let n = 3;

document.write(maxSum(n));

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
3
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
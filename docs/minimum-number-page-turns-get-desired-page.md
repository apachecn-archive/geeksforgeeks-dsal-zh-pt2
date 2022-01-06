# 到达所需页面的最小页数

> 原文:[https://www . geesforgeks . org/最小页数-页数-获得所需页数/](https://www.geeksforgeeks.org/minimum-number-page-turns-get-desired-page/)

给定一本书的 **N** 页，任务是计算到达给定期望页面的最小页数 **K** 。我们可以从书的正面(即第 1 页)开始翻页，也可以从书的背面(即第 N 页)开始翻页。每一页都有两面，正面和背面，除了第一页只有背面，最后一页可能只有背面，这取决于书的页数。
**例:**

```
Input : N = 6 and K = 2.
Output : 1.
From front, (1) -> (2, 3), page turned = 1.
From back, (6) -> (4, 5) -> (2,3), page turned = 2.
So, Minimum number of page turned = 1.

Input : N = 5 and K = 4.
Output : 1.
From front, (1) -> (2, 3) -> (4,5), page turned = 2.
From back, (4, 5) page turned = 1\. From back, it is 2nd page, since 4 is on other side of page 5 and page 5 is the first one from back
So, Minimum number of page turned = 1.
```

这个想法是计算所需页面与书的正面和背面的距离，最小的距离就是所需答案。
现在，考虑有第 0 页，在第一页的前面。如果 N 是偶数，考虑有第 N+1 页，是最后一页的后面，所以总页数是 N+1。
计算距离，
1。如果 K 为偶数，则前距=(K–0)/2，后距=(N–1–K)/2。
2。如果 K 是奇数，前距离=(K–1)/2，后距离=(N–K)/2。

## C++

```
// C++ program to find minimum number of page
// turns to reach a page
#include<bits/stdc++.h>
using namespace std;

int minTurn(int n, int k)
{
    // Considering back of last page.
    if (n%2 == 0)
        n++;

    // Calculating Distance from front and
    // back of the book and return the min
    return min((k + 1)/2, (n - k + 1)/2);
}

// Driven Program
int main()
{
    int n = 6, k = 2;
    cout << minTurn(n,k) << endl;
    return 0;
}

// This code is modified by naveenkonda
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of page turns to
// reach a page
import java.io.*;

public class GFG
{

// Function to calculate
// minimum number of page
// turns required
static int minTurn(int n, int k)
{

    // Considering back of last page.
    if (n % 2 == 0)
        n++;

    // Calculating Distance from front and
    // back of the book and return the min
    Math.min((k + 1) / 2, (n - k + 1) / 2);
}

    // Driver Code
    static public void main (String[] args)
    {
        int n = 6, k = 2;
        System.out.println(minTurn(n, k));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find minimum number
# of page turns to reach a page
def minTurn(n, k):

    # Considering back of last page.
    if (n % 2 == 0):
        n += 1

    // Calculating Distance from front and
    // back of the book and return the min
    return min((k + 1) / 2, (n - k + 1) / 2)

# Driver Code
if __name__ == '__main__':
    n = 6
    k = 2
    print(int(minTurn(n, k)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find minimum
// number of page turns to
// reach a page
using System;

public class GFG
{

// Function to calculate
// minimum number of page
// turns required
static int minTurn(int n, int k)
{

    // Considering back of last page.
    if (n % 2 == 0)
        n++;                       

    // Calculating Distance from front and
    // back of the book and return the min
    return Math.Min((k + 1) / 2,
                    (n - k + 1) / 2);
}

    // Driver Code
    static public void Main (String[] args)
    {
        int n = 6, k = 2;
        Console.WriteLine(minTurn(n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number
// of page turns to reach a page

function minTurn($n, $k)
{
    // Considering back of last page.
    if ($n % 2 == 0)
        $n++;

    // Calculating Distance from front and
    // back of the book and return the min
    return min(($k + 1) / 2,
               ($n - $k + 1) / 2);
}

// Driver Code
$n = 6; $k = 2;
echo minTurn($n, $k) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum
// number of page turns to
// reach a page

// Function to calculate
// minimum number of page
// turns required
function minTurn(n, k)
{

    // Considering back of last page.
    if (n % 2 == 0)
        n++;

    // Calculating Distance from front and
    // back of the book and return the min
    let x = Math.min((k + 1) / 2, (n - k + 1) / 2);
    return Math.floor(x);
}

// Driver code   

        let n = 6, k = 2;
        document.write(minTurn(n, k));

</script>
```

**输出:**

```
1
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
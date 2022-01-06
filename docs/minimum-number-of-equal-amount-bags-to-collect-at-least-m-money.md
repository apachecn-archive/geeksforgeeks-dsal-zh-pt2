# 收集至少 M 张钞票的最少等量袋数

> 原文:[https://www . geeksforgeeks . org/最低等量袋数-至少要收集 m 个货币/](https://www.geeksforgeeks.org/minimum-number-of-equal-amount-bags-to-collect-at-least-m-money/)

给定无限数量的两种面额的硬币 **X** 和 **Y** 。还赠送容量为**卢比**的袋子，与硬币数量无关。任务是找到最小数量的袋子，使得每个袋子包含相同数量的卢比，并且所有袋子数量的总和至少为 **M** 。
**举例:**

```
Input : M = 27, N = 12, X = 2, Y = 5\. 
Output : 3
We put 2 coins of X, 1 coin of Y in each bag. 
So we have 9 rupees in each bag and we need 
at least 3 bags (Note that 27/9 = 3). There 
is no way to obtain sum with lesser number
of bags.

Input : M = 45, N = 9, X = 4, Y = 5\. 
Output : 5
```

任务是最小化袋子的数量，因此需要最大化袋子中的数量，使得所有袋子中的数量相同。假设我们取 X 硬币的‘p’数和 Y 硬币的‘q’数，那么任务是最大化 p*X + q*Y。同样，p*X + q*Y <= N.
现在，要找到等式左手边的最大可能值，将 p 从 0 变化到 N/X，然后找到特定 p 的最大可能 q。然后，在所有这样的对中，取给出 p*X + q*Y 最大值的(p，q)对。
下面是上述想法的实现:

## C++

```
// C++ program to find minimum number of bags such
// that each bag contains same amount and sum is at
// least M.
#include<bits/stdc++.h>
using namespace std;

// Return minimum number of bags required.
int minBags(int M, int N, int X, int Y)
{
    // Initialize maximum amount in a bag
    int maxAmount = 0;

    // Finding maximum possible q for the particular p.
    for (int p = 0; p <= N/X; p++)
    {
        int q = (N - p * X) / Y;

        maxAmount = max(maxAmount, p*X + q*Y);
    }

    // Calculating the minimum number of bags.
    int result = M/maxAmount;
    result += (M % maxAmount == 0? 0: 1);

    return result;
}

// Driven Program
int main()
{
    int M = 45, N = 9;
    int X = 4, Y = 5;

    cout << minBags(M, N, X, Y) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of bags such that each bag contains
// same amount and sum is at least M
import java.io.*;

public class GFG {

// Return minimum number of bags required.
static int minBags(int M, int N,
                   int X, int Y)
{

    // Initialize maximum amount in a bag
    int maxAmount = 0;

    // Finding maximum possible q
    // for the particular p.
    for (int p = 0; p <= N / X; p++)
    {
        int q = (N - p * X) / Y;

        maxAmount = Math.max(maxAmount, p * X +
                                        q * Y);
    }

    // Calculating the minimum number of bags.
    int result = M / maxAmount;
    result += (M % maxAmount == 0? 0: 1);

    return result;
}

    // Driver Code
    static public void main (String[] args)
    {
        int M = 45, N = 9;
        int X = 4, Y = 5;

        System.out.println(minBags(M, N, X, Y));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find minimum number
# of bags such that each bag contains same
# amount and sum is at least M.

# Return minimum number of bags required.
def minBags(M, N, X, Y):

    # Initialize maximum amount in a bag
    maxAmount = 0

    # Finding maximum possible q for
    # the particular p.
    for p in range(0, int(N / X) + 1, 1):
        q = int((N - p * X) / Y)

        maxAmount = max(maxAmount, p * X + q * Y)

    # Calculating the minimum number of bags.
    result = int(M / maxAmount)
    if(M % maxAmount == 0):
        result += 0
    else:
        result += 1

    return result

# Driver Code
if __name__ == '__main__':
    M = 45
    N = 9
    X = 4
    Y = 5

    print(minBags(M, N, X, Y))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find minimum number of
// bags such that each bag contains same
// amount and sum is at least M.
using System;

public class GFG
{

// Return minimum number of bags required.
static int minBags(int M, int N,
                int X, int Y)
{

    // Initialize maximum amount in a bag
    int maxAmount = 0;

    // Finding maximum possible q
    // for the particular p.
    for (int p = 0; p <= N / X; p++)
    {
        int q = (N - p * X) / Y;

        maxAmount = Math.Max(maxAmount, p * X +
                                        q * Y);
    }

    // Calculating the minimum number of bags.
    int result = M / maxAmount;
    result += (M % maxAmount == 0? 0: 1);

    return result;
}

    // Driver Code
    static public void Main ()
    {
        int M = 45, N = 9;
        int X = 4, Y = 5;

        Console.WriteLine(minBags(M, N, X, Y));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// number of bags such that each
// bag contains same amount and
// sum is at least M.

// Return minimum number
// of bags required.
function minBags($M, $N, $X, $Y)
{
    // Initialize maximum
    // amount in a bag
    $maxAmount = 0;

    // Finding maximum possible
    // q for the particular p.
    for ($p = 0; $p <= $N / $X; $p++)
    {
        $q = ($N - $p * $X) / $Y;

        $maxAmount = max($maxAmount,
                         $p * $X + $q * $Y);
    }

    // Calculating the minimum
    // number of bags.
    $result = $M / $maxAmount;
    $result += ($M % $maxAmount == 0? 0: 1);

    return $result;
}

// Driver Code
$M = 45; $N = 9;
$X = 4 ; $Y = 5;

echo minBags($M, $N, $X, $Y) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// Javascript program to find minimum number
// of bags such that each bag contains
// same amount and sum is at least M

// Return minimum number of bags required.
function minBags(M, N, X, Y)
{

    // Initialize maximum amount in a bag
    let maxAmount = 0;

    // Finding maximum possible q
    // for the particular p.
    for (let p = 0; p <= N / X; p++)
    {
        let q = (N - p * X) / Y;

        maxAmount = Math.max(maxAmount, p * X +
                                        q * Y);
    }

    // Calculating the minimum number of bags.
    let result = M / maxAmount;
    result += (M % maxAmount == 0? 0: 1);

    return result;
}

// Driver code   

    let M = 45, N = 9;
       let X = 4, Y = 5;

       document.write(minBags(M, N, X, Y));

      // This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
5
```

**时间复杂度:** O(N/X)
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
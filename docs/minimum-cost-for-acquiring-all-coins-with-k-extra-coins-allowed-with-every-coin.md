# 获得所有硬币的最低成本，每枚硬币允许有 k 个额外硬币

> 原文:[https://www . geeksforgeeks . org/用 k 额外硬币获得所有硬币的最低成本-每枚硬币允许/](https://www.geeksforgeeks.org/minimum-cost-for-acquiring-all-coins-with-k-extra-coins-allowed-with-every-coin/)

给你一张不同面值的 N 个硬币的清单。您可以支付相当于任何 1 枚硬币的金额，并可以获得该硬币。此外，一旦您支付了一枚硬币，我们最多可以选择 K 枚以上的硬币，并且可以免费获得这些硬币。任务是为给定的 k 值找到获得所有 N 个硬币所需的最小数量。

**示例:**

```
Input : coin[] = {100, 20, 50, 10, 2, 5}, 
        k = 3
Output : 7

Input : coin[] = {1, 2, 5, 10, 20, 50}, 
        k = 3
Output : 3
```

根据问题，我们可以看到，一枚硬币的成本，我们最多可以获得 K+1 枚硬币。因此，为了获得所有的 n 个硬币，我们将选择 ceil(n/(k+1))硬币，如果我们选择最小的 ceil(n/(k+1))(贪婪方法)，选择硬币的成本将是最小的。最小上限(n/(k+1))硬币可以通过简单地将所有 N 个值按递增顺序排序来找到。
如果我们要检查时间复杂度(n log n)是用于排序元素，而(k)是用于相加总量。最后，时间复杂度:O(n ^ log n)。

## C++

```
// C++ program to acquire all n coins
#include<bits/stdc++.h>
using namespace std;

// function to calculate min cost
int minCost(int coin[], int n, int k)
{
    // sort the coins value
    sort(coin, coin + n);

    // calculate no. of
    // coins needed
    int coins_needed = ceil(1.0 * n /
                            (k + 1));

    // calculate sum of
    // all selected coins
    int ans = 0;
    for (int i = 0; i <= coins_needed - 1;
                                      i++)
        ans += coin[i];

    return ans;
}

// Driver Code
int main()
{
    int coin[] = {8, 5, 3, 10,
                  2, 1, 15, 25};
    int n = sizeof(coin) / sizeof(coin[0]);
    int k = 3;
    cout << minCost(coin, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to acquire
// all n coins
import java.util.Arrays;

class GFG
{

    // function to calculate min cost
    static int minCost(int coin[],
                       int n, int k)
    {

        // sort the coins value
        Arrays.sort(coin);

        // calculate no. of
        // coins needed
        int coins_needed = (int)Math.ceil(1.0 *
                                  n / (k + 1));

        // calculate sum of
        // all selected coins
        int ans = 0;

        for (int i = 0; i <= coins_needed - 1;
                                          i++)
            ans += coin[i];

        return ans;
    }

    // Driver code
    public static void main(String arg[])
    {
        int coin[] = { 8, 5, 3, 10,
                       2, 1, 15, 25 };
        int n = coin.length;
        int k = 3;

        System.out.print(minCost(coin, n, k));
    }
}

// This code is contributed
// by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to
# acquire all n coins

import math

# function to calculate min cost
def minCost(coin, n, k):

    # sort the coins value
    coin.sort()

    # calculate no. of
    # coins needed
    coins_needed = math.ceil(1.0 * n //
                            (k + 1));

    # calculate sum of all
    # selected coins
    ans = 0
    for i in range(coins_needed - 1 + 1):
        ans += coin[i]

    return ans

# Driver code
coin = [8, 5, 3, 10,
        2, 1, 15, 25]
n = len(coin)
k = 3

print(minCost(coin, n, k))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to acquire all n coins
using System;

class GFG
{

    // function to calculate min cost
    static int minCost(int []coin,
                       int n, int k)
    {
        // sort the coins value
        Array.Sort(coin);

        // calculate no. of coins needed
        int coins_needed = (int)Math.Ceiling(1.0 *
                                     n / (k + 1));

        // calculate sum of
        // all selected coins
        int ans = 0;

        for (int i = 0; i <= coins_needed - 1; i++)
            ans += coin[i];

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []coin = {8, 5, 3, 10,
                      2, 1, 15, 25};
        int n = coin.Length;
        int k = 3;

        // Function calling
        Console.Write(minCost(coin, n, k));
    }
}

// This code is contributed
// by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to acquire all n coins

// function to calculate min cost
function minCost($coin, $n, $k)
{
    // sort the coins value
    sort($coin); sort($coin,$n);

    // calculate no. of coins needed
    $coins_needed = ceil(1.0 * $n / ($k + 1));

    // calculate sum of
    // all selected coins
    $ans = 0;
    for ($i = 0; $i <= $coins_needed - 1; $i++)
        $ans += $coin[$i];

    return $ans;
}

// Driver Code
{
    $coin = array(8, 5, 3, 10,
                  2, 1, 15, 25);
    $n = sizeof($coin) / sizeof($coin[0]);
    $k = 3;
    echo minCost($coin, $n, $k);
    return 0;
}        

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to acquire all n coins

// Function to calculate min cost
function minCost(coin, n, k)
{

    // Sort the coins value
    coin.sort(function(a, b){return a - b})

    // Calculate no. of
    // coins needed
    var coins_needed = Math.ceil(n /(k + 1));

    // Calculate sum of
    // all selected coins
    var ans = 0;
    for(var i = 0; i <= coins_needed - 1; i++)
        ans += coin[i];

    return ans;
}

// Driver Code
var coin = [ 8, 5, 3, 10,
             2, 1, 15, 25 ]
var n = coin.length;
var k = 3;

document.write(minCost(coin, n, k));

// This code is contributed by noob2000

</script>
```

**输出:**

```
3
```

时间复杂度:0(对数 n)

辅助空间:O(1)
注意，有更有效的方法来找到给定数量的最小值。例如，数组中 [m 个最大(或最小)元素的方法 6 可以在(n-m) Log m + m Log m 中找到第 m 个最小元素。](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)

**如何处理单个预定义数组的多个查询？**
在这种情况下，如果要求你为 K 的多个值找到上面的答案，你必须快速计算它，并且我们的时间复杂度随着 K 的查询数量而增加。为了服务的目的，我们可以在对所有 N 个值进行排序后维护一个前缀和数组，并且可以轻松快速地回答查询。
假设

## C++

```
// C++ program to acquire all
// n coins at minimum cost
// with multiple values of k.
#include<bits/stdc++.h>
using namespace std;

// Converts coin[] to prefix sum array
void preprocess(int coin[], int n)
{
    // sort the coins value
    sort(coin, coin + n);

    // Maintain prefix sum array
    for (int i = 1; i <= n - 1; i++)
        coin[i] += coin[i - 1];
}

// Function to calculate min
// cost when we can get k extra
// coins after paying cost of one.
int minCost(int coin[], int n, int k)
{
    // calculate no. of coins needed
    int coins_needed = ceil(1.0 * n / (k + 1));

    // return sum of from prefix array
    return coin[coins_needed - 1];
}

// Driver Code
int main()
{
    int coin[] = {8, 5, 3, 10,
                  2, 1, 15, 25};
    int n = sizeof(coin) / sizeof(coin[0]);
    preprocess(coin, n);
    int k = 3;
    cout << minCost(coin, n, k) << endl;
    k = 7;
    cout << minCost(coin, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C# program to acquire all n coins at
// minimum cost with multiple values of k.
import java .io.*;
import java.util.Arrays;

public class GFG {

    // Converts coin[] to prefix sum array
    static void preprocess(int []coin, int n)
    {

        // sort the coins value
        Arrays.sort(coin);

        // Maintain prefix sum array
        for (int i = 1; i <= n - 1; i++)
            coin[i] += coin[i - 1];
    }

    // Function to calculate min cost when we
    // can get k extra coins after paying
    // cost of one.
    static int minCost(int []coin, int n, int k)
    {

        // calculate no. of coins needed
        int coins_needed =(int) Math.ceil(1.0
                                * n / (k + 1));

        // return sum of from prefix array
        return coin[coins_needed - 1];
    }

    // Driver Code
    static public void main (String[] args)
    {
        int []coin = {8, 5, 3, 10, 2, 1, 15, 25};
        int n = coin.length;

        preprocess(coin, n);

        int k = 3;
        System.out.println(minCost(coin, n, k));

        k = 7;
        System.out.println( minCost(coin, n, k));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to acquire all n coins at
# minimum cost with multiple values of k.
import math as mt

# Converts coin[] to prefix sum array
def preprocess(coin, n):

    # sort the coins values
    coin.sort()

    # maintain prefix sum array
    for i in range(1, n):
        coin[i] += coin[i - 1]

# Function to calculate min cost when we can 
# get k extra coins after paying cost of one.
def minCost(coin, n, k):

    # calculate no. of coins needed
    coins_needed = mt.ceil(1.0 * n / (k + 1))

    # return sum of from prefix array
    return coin[coins_needed - 1]

# Driver code
coin = [8, 5, 3, 10, 2, 1, 15, 25]

n = len(coin)

preprocess(coin, n)
k = 3

print(minCost(coin, n, k))

k = 7

print(minCost(coin, n, k))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to acquire all n coins at
// minimum cost with multiple values of k.
using System;

public class GFG {

    // Converts coin[] to prefix sum array
    static void preprocess(int []coin, int n)
    {

        // sort the coins value
        Array.Sort(coin);

        // Maintain prefix sum array
        for (int i = 1; i <= n - 1; i++)
            coin[i] += coin[i - 1];
    }

    // Function to calculate min cost when we
    // can get k extra coins after paying
    // cost of one.
    static int minCost(int []coin, int n, int k)
    {

        // calculate no. of coins needed
        int coins_needed =(int) Math.Ceiling(1.0
                                 * n / (k + 1));

        // return sum of from prefix array
        return coin[coins_needed - 1];
    }

    // Driver Code
    static public void Main ()
    {
        int []coin = {8, 5, 3, 10, 2, 1, 15, 25};
        int n = coin.Length;

        preprocess(coin, n);

        int k = 3;
        Console.WriteLine(minCost(coin, n, k));

        k = 7;
        Console.WriteLine( minCost(coin, n, k));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to acquire all n coins at
// minimum cost with multiple values of k.

// Converts coin[] to prefix sum array
function preprocess(&$coin, $n)
{
    // sort the coins value
    sort($coin);

    // Maintain prefix sum array
    for ($i = 1; $i <= $n - 1; $i++)
        $coin[$i] += $coin[$i - 1];
}

// Function to calculate min cost
// when we can get k extra coins
// after paying cost of one.
function minCost(&$coin, $n, $k)
{
    // calculate no. of coins needed
    $coins_needed = ceil(1.0 * $n / ($k + 1));

    // return sum of from prefix array
    return $coin[$coins_needed - 1];
}

// Driver Code
$coin = array(8, 5, 3, 10,
              2, 1, 15, 25);
$n = sizeof($coin);
preprocess($coin, $n);

$k = 3;
echo minCost($coin, $n, $k) . "\n";

$k = 7;
echo minCost($coin, $n, $k) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to acquire all n coins at
// minimum cost with multiple values of k.

    // Converts coin[] to prefix sum array
    function preprocess(coin,n)
    {
        // sort the coins value
        coin.sort(function(a,b){return a-b;});

        // Maintain prefix sum array
        for (let i = 1; i <= n - 1; i++)
            coin[i] += coin[i - 1];
    }

    // Function to calculate min cost when we
    // can get k extra coins after paying
    // cost of one.
    function minCost(coin,n,k)
    {
        // calculate no. of coins needed
        let coins_needed =Math.ceil(1.0
                                * n / (k + 1));

        // return sum of from prefix array
        return coin[coins_needed - 1];
    }

    // Driver Code
    let coin=[8, 5, 3, 10, 2, 1, 15, 25];
    let n = coin.length;
    preprocess(coin, n);
    let k = 3;
    document.write(minCost(coin, n, k)+"<br>");

    k = 7;
    document.write( minCost(coin, n, k));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
3
1
```

时间复杂度:0(对数 n)

辅助空间:O(1)
预处理后，对于一个 k 的每个查询都需要 O(1)个时间。
本文由 [**希瓦姆·普拉丹(anuj_charm)**](https://www.facebook.com/anuj.charm) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
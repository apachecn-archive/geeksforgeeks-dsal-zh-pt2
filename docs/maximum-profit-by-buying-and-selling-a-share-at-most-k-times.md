# 最多 k 次买卖一股最大利润

> 原文:[https://www . geeksforgeeks . org/最多 k 次买卖每股最大利润/](https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-share-at-most-k-times/)

在股票交易中，买方购买股票并在未来某一天出售。给定 n 天的股票价格，允许交易者最多进行 k 次交易，其中新的交易只能在前一次交易完成后开始，找出股票交易者可能获得的最大利润。
**例:**

```
Input:  
Price = [10, 22, 5, 75, 65, 80]
    K = 2
Output:  87
Trader earns 87 as sum of 12 and 75
Buy at price 10, sell at 22, buy at 
5 and sell at 80

Input:  
Price = [12, 14, 17, 10, 14, 13, 12, 15]
    K = 3
Output:  12
Trader earns 12 as the sum of 5, 4 and 3
Buy at price 12, sell at 17, buy at 10 
and sell at 14 and buy at 12 and sell
at 15

Input:  
Price = [100, 30, 15, 10, 8, 25, 80]
    K = 3
Output:  72
Only one transaction. Buy at price 8 
and sell at 80.

Input:  
Price = [90, 80, 70, 60, 50]
    K = 1
Output:  0
Not possible to earn. 
```

这个问题有各种版本。如果只允许我们买卖一次，那么我们可以使用两个元素之间的最大差异算法。如果允许我们最多进行 2 笔交易，我们可以遵循这里讨论的方法。如果我们被允许买卖任何次数，我们可以遵循这里讨论的方法。

在这篇文章中，我们只被允许进行最大 k 交易。这个问题可以用动态规划来解决。
让**利润【t】【I】**代表使用最多 t 笔交易直到第 I 天(包括第 I 天)的最大利润。那么关系是:
利润[t][i] =最大值(利润[t][i-1]，最大值(价格[I]–价格[j] +利润[t-1][j])
对于范围[0，i-1]
中的所有 j，利润[t][i]将最大值为–

1.  利润[t][i-1],表示在第二天没有进行任何交易。
2.  第一天销售获得的最大利润。为了在第一天卖出股票，我们需要在[0，I–1]天的任何一天买入。如果我们在第一天买入股票并在第二天卖出，最大利润将是价格[I]–价格[j] +利润[t-1][j]，其中 j 从 0 到 i-1 不等。在这里，利润[t-1][j]是我们在第十天之前少做一笔交易的最好结果。

下面是基于动态编程的实现。

## C++

```
// C++ program to find out maximum profit by
// buying and selling a share atmost k times
// given stock price of n days
#include <climits>
#include <iostream>
using namespace std;

// Function to find out maximum profit by buying
// & selling a share atmost k times given stock
// price of n days
int maxProfit(int price[], int n, int k)
{
    // table to store results of subproblems
    // profit[t][i] stores maximum profit using
    // atmost t transactions up to day i (including
    // day i)
    int profit[k + 1][n + 1];

    // For day 0, you can't earn money
    // irrespective of how many times you trade
    for (int i = 0; i <= k; i++)
        profit[i][0] = 0;

    // profit is 0 if we don't do any transaction
    // (i.e. k =0)
    for (int j = 0; j <= n; j++)
        profit[0][j] = 0;

    // fill the table in bottom-up fashion
    for (int i = 1; i <= k; i++) {
        for (int j = 1; j < n; j++) {
            int max_so_far = INT_MIN;

            for (int m = 0; m < j; m++)
                max_so_far = max(max_so_far,
                                 price[j] - price[m] + profit[i - 1][m]);

            profit[i][j] = max(profit[i][j - 1], max_so_far);
        }
    }

    return profit[k][n - 1];
}

// Driver code
int main()
{
    int k = 2;
    int price[] = { 10, 22, 5, 75, 65, 80 };
    int n = sizeof(price) / sizeof(price[0]);

    cout << "Maximum profit is: "
         << maxProfit(price, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out maximum
// profit by buying and selling a
// share atmost k times given
// stock price of n days

class GFG {

    // Function to find out
    // maximum profit by
    // buying & selling a
    // share atmost k times
    // given stock price of n days
    static int maxProfit(int[] price,
                         int n,
                         int k)
    {

        // table to store results
        // of subproblems
        // profit[t][i] stores
        // maximum profit using
        // atmost t transactions up
        // to day i (including day i)
        int[][] profit = new int[k + 1][n + 1];

        // For day 0, you can't
        // earn money irrespective
        // of how many times you trade
        for (int i = 0; i <= k; i++)
            profit[i][0] = 0;

        // profit is 0 if we don't
        // do any transaction
        // (i.e. k =0)
        for (int j = 0; j <= n; j++)
            profit[0][j] = 0;

        // fill the table in
        // bottom-up fashion
        for (int i = 1; i <= k; i++)
        {
            for (int j = 1; j < n; j++)
            {
                int max_so_far = 0;

                for (int m = 0; m < j; m++)
                max_so_far = Math.max(max_so_far, price[j] -
                             price[m] + profit[i - 1][m]);

                profit[i][j] = Math.max(profit[i] [j - 1],
                                              max_so_far);
            }
        }

        return profit[k][n - 1];
    }

    // Driver code
    public static void main(String []args)
    {
        int k = 2;
        int[] price = { 10, 22, 5, 75, 65, 80 };
        int n = price.length;
        System.out.println("Maximum profit is: " +
                            maxProfit(price, n, k));
    }
}

// This code is contributed by Anshul Aggarwal.
```

## 蟒蛇 3

```
# Python program to maximize the profit
# by doing at most k transactions
# given stock prices for n days

# Function to find out maximum profit by
# buying & selling a share atmost k times
# given stock price of n days
def maxProfit(prices, n, k):

    # Bottom-up DP approach
    profit = [[0 for i in range(k + 1)]
                 for j in range(n)]

    # Profit is zero for the first
    # day and for zero transactions
    for i in range(1, n):

        for j in range(1, k + 1):
            max_so_far = 0

            for l in range(i):
                max_so_far = max(max_so_far, prices[i] -
                            prices[l] + profit[l][j - 1])

            profit[i][j] = max(profit[i - 1][j], max_so_far)

    return profit[n - 1][k]

# Driver code
k = 2
prices = [10, 22, 5, 75, 65, 80]
n = len(prices)

print("Maximum profit is:",
       maxProfit(prices, n, k))

# This code is contributed by vaibhav29498
```

## C#

```
// C# program to find out maximum profit by
// buying and selling a share atmost k times
// given stock price of n days
using System;

class GFG {

    // Function to find out maximum profit by
    // buying & selling/ a share atmost k times
    // given stock price of n days
    static int maxProfit(int[] price, int n, int k)
    {
        // table to store results of subproblems
        // profit[t][i] stores maximum profit using atmost
        // t transactions up to day i (including day i)
        int[, ] profit = new int[k + 1, n + 1];

        // For day 0, you can't earn money
        // irrespective of how many times you trade
        for (int i = 0; i <= k; i++)
            profit[i, 0] = 0;

        // profit is 0 if we don't do any transaction
        // (i.e. k =0)
        for (int j = 0; j <= n; j++)
            profit[0, j] = 0;

        // fill the table in bottom-up fashion
        for (int i = 1; i <= k; i++) {
            for (int j = 1; j < n; j++) {
                int max_so_far = 0;

                for (int m = 0; m < j; m++)
                max_so_far = Math.Max(max_so_far, price[j] -
                               price[m] + profit[i - 1, m]);

                profit[i, j] = Math.Max(profit[i, j - 1], max_so_far);
            }
        }

        return profit[k, n - 1];
    }

    // Driver code to test above
    public static void Main()
    {
        int k = 2;
        int[] price = { 10, 22, 5, 75, 65, 80 };

        int n = price.Length;

        Console.Write("Maximum profit is: " +
                     maxProfit(price, n, k));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find out maximum profit by
// buying and selling a share atmost k times
// given stock price of n days

// Function to find out maximum profit by buying
// & selling a share atmost k times given stock
// price of n days
function maxProfit($price, $n, $k)
{

    // table to store results of subproblems
    // profit[t][i] stores maximum profit using
    // atmost t transactions up to day i (including
    // day i)
    $profit[$k + 1][$n + 1] = 0;

    // For day 0, you can't earn money
    // irrespective of how many times you trade
    for ($i = 0; $i <= $k; $i++)
        $profit[$i][0] = 0;

    // profit is 0 if we don't
    // do any transaction
    // (i.e. k =0)
    for ($j = 0; $j <= $n; $j++)
        $profit[0][$j] = 0;

    // fill the table in
    // bottom-up fashion
    for ($i = 1; $i <= $k; $i++) {
        for ($j = 1; $j < $n; $j++) {
            $max_so_far = PHP_INT_MIN;

            for ($m = 0; $m < $j; $m++)
                $max_so_far = max($max_so_far,
                              $price[$j] - $price[$m] +
                              $profit[$i - 1][$m]);

            $profit[$i][$j] = max($profit[$i][$j - 1],
                                         $max_so_far);
        }
    }

    return $profit[$k][$n - 1];
}

    // Driver code
    $k = 2;
    $price = array (10, 22, 5, 75, 65, 80 );
    $n = sizeof($price);
    echo "Maximum profit is: ". maxProfit($price, $n, $k);

// This is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to find out maximum
// profit by buying and selling a
// share atmost k times given
// stock price of n days 

// Function to find out
// maximum profit by
// buying & selling a
// share atmost k times
// given stock price of n days
function maxProfit(price,n, k)
{

    // table to store results
    // of subproblems
    // profit[t][i] stores
    // maximum profit using
    // atmost t transactions up
    // to day i (including day i)
    var profit = Array(k+1).fill(0).map
    (x => Array(n+1).fill(0));

    // For day 0, you can't
    // earn money irrespective
    // of how many times you trade
    for (i = 0; i <= k; i++)
        profit[i][0] = 0;

    // profit is 0 if we don't
    // do any transaction
    // (i.e. k =0)
    for (j = 0; j <= n; j++)
        profit[0][j] = 0;

    // fill the table in
    // bottom-up fashion
    for (i = 1; i <= k; i++)
    {
        for (j = 1; j < n; j++)
        {
            var max_so_far = 0;

            for (m = 0; m < j; m++)
            max_so_far = Math.max(max_so_far, price[j] -
                         price[m] + profit[i - 1][m]);

            profit[i][j] = Math.max(profit[i] [j - 1],
                                          max_so_far);
        }
    }

    return profit[k][n - 1];
}

// Driver code
var k = 2;
var price = [ 10, 22, 5, 75, 65, 80 ];
var n = price.length;
document.write("Maximum profit is: " +
                    maxProfit(price, n, k));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
Maximum profit is: 87
```

**优化解:**
上述解的时间复杂度为 O(k.n <sup>2</sup> )。如果我们能计算出第一天在固定时间内卖出股票所获得的最大利润，这个数字就可以减少。
利润[t][i] =最大值(利润[t][i-1]，最大值(价格[I]–价格[j] +利润[t-1][j])
对于范围[0，i-1]
内的所有 j 如果我们仔细注意的话，
最大值(价格[I]–价格[j] +利润[t-1][j])
对于范围[0，i-1]
内的所有 j 可以改写为，
=价格[i] +最大值 i-2]
所以，如果我们已经计算了范围[0，i-2]内所有 j 的 max(利润[t-1][j]–价格[j])，那么我们可以在恒定时间内计算出 j = I–1。 换句话说，我们不必再回头看[0，i-1]范围来找出最佳购买日。我们可以用下面修正的关系式在恒定时间内确定。
利润[t][i] =最大值(利润[t][i-1]，价格[i] +最大值(previdiff，利润[t-1][I-1]–价格[i-1])
其中 previdiff 是范围[0，i-2]内所有 j 的最大值(利润[t-1][j]–价格[j])
下面是其优化实现–

## C++

```
// C++ program to find out maximum profit by buying
// and/ selling a share atmost k times given stock
// price of n days
#include <climits>
#include <iostream>
using namespace std;

// Function to find out maximum profit by buying &
// selling/ a share atmost k times given stock price
// of n days
int maxProfit(int price[], int n, int k)
{
    // table to store results of subproblems
    // profit[t][i] stores maximum profit using atmost
    // t transactions up to day i (including day i)
    int profit[k + 1][n + 1];

    // For day 0, you can't earn money
    // irrespective of how many times you trade
    for (int i = 0; i <= k; i++)
        profit[i][0] = 0;

    // profit is 0 if we don't do any transaction
    // (i.e. k =0)
    for (int j = 0; j <= n; j++)
        profit[0][j] = 0;

    // fill the table in bottom-up fashion
    for (int i = 1; i <= k; i++) {
        int prevDiff = INT_MIN;
        for (int j = 1; j < n; j++) {
            prevDiff = max(prevDiff,
                           profit[i - 1][j - 1] - price[j - 1]);
            profit[i][j] = max(profit[i][j - 1],
                               price[j] + prevDiff);
        }
    }

    return profit[k][n - 1];
}

// Driver Code
int main()
{
    int k = 3;
    int price[] = { 12, 14, 17, 10, 14, 13, 12, 15 };

    int n = sizeof(price) / sizeof(price[0]);

    cout << "Maximum profit is: "
         << maxProfit(price, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out maximum
// profit by buying and selling a
// share atmost k times given stock
// price of n days
import java.io.*;

class GFG {

    // Function to find out maximum profit by
    // buying & selling/ a share atmost k times
    // given stock price of n days
    static int maxProfit(int price[],
                         int n, int k)
    {

        // table to store results of subproblems
        // profit[t][i] stores maximum profit
        // using atmost t transactions up to day
        // i (including day i)
        int profit[][] = new int[k + 1][ n + 1];

        // For day 0, you can't earn money
        // irrespective of how many times you trade
        for (int i = 0; i <= k; i++)
            profit[i][0] = 0;

        // profit is 0 if we don't do any
        // transaction (i.e. k =0)
        for (int j = 0; j <= n; j++)
            profit[0][j] = 0;

        // fill the table in bottom-up fashion
        for (int i = 1; i <= k; i++)
        {
            int prevDiff = Integer.MIN_VALUE;
            for (int j = 1; j < n; j++)
            {
                prevDiff = Math.max(prevDiff,
                           profit[i - 1][j - 1] -
                           price[j - 1]);
                profit[i][j] = Math.max(profit[i][j - 1],
                               price[j] + prevDiff);
            }
        }

        return profit[k][n - 1];
    }

// Driver code
public static void main (String[] args)
    {
        int k = 3;
        int price[] = {12, 14, 17, 10, 14, 13, 12, 15};

        int n = price.length;

        System.out.println("Maximum profit is: " +
                            maxProfit(price, n, k));
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to find out maximum
# profit by buying and/ selling a share
# at most k times given the stock price
# of n days

# Function to find out maximum profit
# by buying & selling/ a share atmost
# k times given stock price of n days
def maxProfit(price, n, k):

    # Table to store results of subproblems
    # profit[t][i] stores maximum profit
    # using atmost t transactions up to
    # day i (including day i)
    profit = [[0 for i in range(n + 1)]
                 for j in range(k + 1)]

    # Fill the table in bottom-up fashion
    for i in range(1, k + 1):
        prevDiff = float('-inf')

        for j in range(1, n):
            prevDiff = max(prevDiff,
                           profit[i - 1][j - 1] -
                           price[j - 1])
            profit[i][j] = max(profit[i][j - 1],
                               price[j] + prevDiff)

    return profit[k][n - 1]

# Driver Code
if __name__ == "__main__":

    k = 3
    price = [12, 14, 17, 10, 14, 13, 12, 15]
    n = len(price)

    print("Maximum profit is:",
           maxProfit(price, n, k))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find out maximum profit by buying
// and selling a share atmost k times given stock
// price of n days
using System;

class GFG {

    // Function to find out maximum profit by
    // buying & selling/ a share atmost k times
    // given stock price of n days
    static int maxProfit(int[] price, int n, int k)
    {
        // table to store results of subproblems
        // profit[t][i] stores maximum profit using atmost
        // t transactions up to day i (including day i)
        int[, ] profit = new int[k + 1, n + 1];

        // For day 0, you can't earn money
        // irrespective of how many times you trade
        for (int i = 0; i <= k; i++)
            profit[i, 0] = 0;

        // profit is 0 if we don't do any transaction
        // (i.e. k =0)
        for (int j = 0; j <= n; j++)
            profit[0, j] = 0;

        // fill the table in bottom-up fashion
        for (int i = 1; i <= k; i++) {
            int prevDiff = int.MinValue;
            for (int j = 1; j < n; j++) {
            prevDiff = Math.Max(prevDiff,
                            profit[i - 1, j - 1] - price[j - 1]);
            profit[i, j] = Math.Max(profit[i, j - 1],
                                price[j] + prevDiff);
            }
        }

        return profit[k, n - 1];
    }

    // Driver code to test above
    public static void Main()
    {
        int k = 3;
        int[] price = {12, 14, 17, 10, 14, 13, 12, 15};

        int n = price.Length;

        Console.Write("Maximum profit is: " +
                     maxProfit(price, n, k));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find out maximum
// profit by buying and selling a
// share atmost k times given stock
// price of n days

// Function to find out maximum
// profit by buying & selling a
// share atmost k times given
// stock price of n days
function maxProfit($price, $n, $k)
{

    // table to store results
    // of subproblems profit[t][i]
    // stores maximum profit using
    // atmost t transactions up to
    // day i (including day i)
    $profit[$k + 1][$n + 1]=0;

    // For day 0, you can't
    // earn money irrespective
    // of how many times you trade
    for ($i = 0; $i <= $k; $i++)
        $profit[$i][0] = 0;

    // profit is 0 if we don't
    // do any transaction
    // (i.e. k =0)
    for ($j = 0; $j <= $n; $j++)
        $profit[0][$j] = 0;

    // fill the table in
    // bottom-up fashion
    $prevDiff = NULL;
    for ($i = 1; $i <= $k; $i++) {
        for ($j = 1; $j < $n; $j++) {
            $prevDiff = max($prevDiff, $profit[$i - 1][$j - 1] -
                                               $price[$j - 1]);
            $profit[$i][$j] = max($profit[$i][$j - 1],
                              $price[$j] + $prevDiff);
        }
    }
    return $profit[$k][$n - 1];
}

    // Driver Code
    $k = 3;
    $price = array(12, 14, 17, 10,
                   14, 13, 12, 15);
    $n = sizeof($price);
    echo "Maximum profit is: "
         , maxProfit($price, $n, $k);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// javascript program to find out maximum
// profit by buying and selling a
// share atmost k times given stock
// price of n days

    // Function to find out maximum profit by
    // buying & selling/ a share atmost k times
    // given stock price of n days
function maxProfit(price, n , k)
{

    // table to store results of subproblems
    // profit[t][i] stores maximum profit
    // using atmost t transactions up to day
    // i (including day i)
    var profit = Array(k+1).fill(0).map(x => Array(n+1).fill(0));

    // For day 0, you can't earn money
    // irrespective of how many times you trade
    for (var i = 0; i <= k; i++)
        profit[i][0] = 0;

    // profit is 0 if we don't do any
    // transaction (i.e. k =0)
    for (j = 0; j <= n; j++)
        profit[0][j] = 0;

    // fill the table in bottom-up fashion
    for (var i = 1; i <= k; i++)
    {
        var prevDiff = -Number.MAX_VALUE;
        for (var j = 1; j < n; j++)
        {
            prevDiff = Math.max(prevDiff,
                       profit[i - 1][j - 1] -
                       price[j - 1]);
            profit[i][j] = Math.max(profit[i][j - 1],
                           price[j] + prevDiff);
        }
    }

    return profit[k][n - 1];
}

// Driver code
var k = 3;
var price = [12, 14, 17, 10, 14, 13, 12, 15];

var n = price.length;

document.write("Maximum profit is: " +
                    maxProfit(price, n, k));
// This code contributed by shikhasingrajput
</script>
```

输出:

```
Maximum profit is: 12
```

上述解的时间复杂度为 O(kn)，空间复杂度为 O(nk)。当我们使用最后一个事务的结果时，空间复杂度可以进一步降低到 O(n)。但是为了使文章易于阅读，我们使用了 O(kn)空间。
本文由**阿迪亚·戈尔**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息
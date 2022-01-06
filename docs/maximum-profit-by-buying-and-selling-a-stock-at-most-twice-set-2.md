# 最多买卖一只股票两次的最大利润|第 2 集

> 原文:[https://www . geeksforgeeks . org/最多买卖两次股票的最大利润集-2/](https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-stock-at-most-twice-set-2/)

给定一个表示不同日股票价格的数组**prices【】**，任务是使用最多允许两次交易的交易在不同日买卖股票后找到最大可能利润。
**注:**不能同时从事多笔交易(即必须卖出股票后才能再次买入)。

**示例:**

> **输入:**价格[] = {3，3，5，0，0，3，1，4}
> **输出:** 6
> **解释:**
> 第 4 天买入，第 6 天卖出= >利润= 3–0 = 3
> 第 7 天买入，第 8 天卖出= >利润= 4 -1 = 3
> 因此，总利润= 3 + 3 = 6
> 
> **输入:**价格[] = {1，2，3，4，5}
> **输出:** 4
> **解释:**
> 第 1 天买入，第 6 天卖出= >利润= 5 -1 = 4
> 因此，总利润= 4

在本文的[中，我们已经在 O(N)空间中使用](https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-share-at-most-twice/)[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)讨论了这个问题。
**高效方法:**这里使用的想法是同时跟踪两个交易。这两只股票的利润计算如下

*   首次交易的最大利润
    *   找到我们必须从口袋中支付的最低价格(buy1)以获得第一只股票，即当天或前一天的股票价格。
    *   通过卖出当天的第一只股票找到最大利润。
*   第二次交易的最大利润
    *   我们必须从口袋里支付的购买第二只股票的最低价格是

```
buy2 = price[i] - profit1, 
// Profit 1 is the profit from 
// selling the first stock
```

*   通过卖出第二只股票来获得最大利润。

**举例说明:**

> 让我们取价格[] = { 3，5，4，5}
> 我们在第一天购买第一只股票
> buy1 = 3。
> 我们在第二天卖出第一只股票。
> 盈利 1 = 5–3 = 2。
> 在第一天买入股票，第二天卖出之后，我们将盈利 2。
> 所以，盈利 1 = 2
> 现在我们将在第 3 天买入第 2 只股票
> 第 3 天的股价是 4
> 由于我们已经盈利了 2，我们将只从我们的数据包中额外花费 2 来购买股票
> ，即(4–盈利 1) = 2
> 买入 2 = 2
> 现在，我们将在第 4 天卖出第 2 只股票。
> 第 4 天股价 5。
> 盈利 2 = 5–buy 2 = 5–2 = 3。
> 现在我们可以看到最终的利润包含了买卖两只股票的利润

下面是上述方法的实现:

## C++

```
// C++ implmenetation to find
// maximum possible profit
// with at most two transactions

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// profit with two transactions
// on a given list of stock prices
int maxProfit(int price[], int n)
{

    // buy1 - Money lent to buy 1 stock
    // profit1 - Profit after selling
    // the 1st stock buyed.
    // buy2 - Money lent to buy 2 stocks
    // including profit of selling 1st stock
    // profit2 - Profit after selling 2 stocks
    int buy1, profit1, buy2, profit2;

    // Set initial buying values to
    // INT_MAX as we want to minimize it
    buy1 = buy2 = INT_MAX;

    // Set initial selling values to
    // zero as we want to maximize it
    profit1 = profit2 = 0;

    for (int i = 0; i < n; i++) {

        // Money lent to buy the stock
        // should be minimum as possible.
        // buy1 tracks the minimum possible
        // stock to buy from 0 to i-1.
        buy1 = min(buy1, price[i]);

        // Profit after selling a stock
        // should be maximum as possible.
        // profit1 tracks maximum possible
        // profit we can make from 0 to i-1.
        profit1 = max(profit1, price[i] - buy1);

        // Now for buying the 2nd stock,
        // we will integrate profit made
        // from selling the 1st stock
        buy2 = min(buy2, price[i] - profit1);

        // Profit after selling a 2 stocks
        // should be maximum as possible.
        // profit2 tracks maximum possible
        // profit we can make from 0 to i-1.
        profit2 = max(profit2, price[i] - buy2);
    }

    return profit2;
}

// Driver Code
int main()
{
    int price[] = { 2, 30, 15, 10, 8, 25, 80 };
    int n = sizeof(price) / sizeof(price[0]);
    cout << "Maximum Profit = "
         << maxProfit(price, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implmenetation to find
// maximum possible profit
// with at most two transactions
import java.util.*;

class GFG{

// Function to find the maximum
// profit with two transactions
// on a given list of stock prices
static int maxProfit(int price[], int n)
{

    // buy1 - Money lent to buy 1 stock
    // profit1 - Profit after selling
    // the 1st stock buyed.
    // buy2 - Money lent to buy 2 stocks
    // including profit of selling 1st stock
    // profit2 - Profit after selling 2 stocks
    int buy1, profit1, buy2, profit2;

    // Set initial buying values to
    // Integer.MAX_VALUE as we want to
    // minimize it
    buy1 = buy2 = Integer.MAX_VALUE;

    // Set initial selling values to
    // zero as we want to maximize it
    profit1 = profit2 = 0;

    for(int i = 0; i < n; i++)
    {

        // Money lent to buy the stock
        // should be minimum as possible.
        // buy1 tracks the minimum possible
        // stock to buy from 0 to i-1.
        buy1 = Math.min(buy1, price[i]);

        // Profit after selling a stock
        // should be maximum as possible.
        // profit1 tracks maximum possible
        // profit we can make from 0 to i-1.
        profit1 = Math.max(profit1, price[i] - buy1);

        // Now for buying the 2nd stock,
        // we will integrate profit made
        // from selling the 1st stock
        buy2 = Math.min(buy2, price[i] - profit1);

        // Profit after selling a 2 stocks
        // should be maximum as possible.
        // profit2 tracks maximum possible
        // profit we can make from 0 to i-1.
        profit2 = Math.max(profit2, price[i] - buy2);
    }
    return profit2;
}

// Driver Code
public static void main(String[] args)
{
    int price[] = { 2, 30, 15, 10, 8, 25, 80 };
    int n = price.length;

    System.out.print("Maximum Profit = " +
                      maxProfit(price, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implmenetation to find
# maximum possible profit
# with at most two transactions
import sys

# Function to find the maximum
# profit with two transactions
# on a given list of stock prices
def maxProfit(price, n):

    # buy1 - Money lent to buy 1 stock
    # profit1 - Profit after selling
    # the 1st stock buyed.
    # buy2 - Money lent to buy 2 stocks
    # including profit of selling 1st stock
    # profit2 - Profit after selling 2 stocks

    # Set initial buying values to
    # INT_MAX as we want to minimize it
    buy1, buy2 = sys.maxsize, sys.maxsize

    # Set initial selling values to
    # zero as we want to maximize it
    profit1, profit2 = 0, 0

    for i in range(n):

        # Money lent to buy the stock
        # should be minimum as possible.
        # buy1 tracks the minimum possible
        # stock to buy from 0 to i-1.
        buy1 = min(buy1, price[i])

        # Profit after selling a stock
        # should be maximum as possible.
        # profit1 tracks maximum possible
        # profit we can make from 0 to i-1.
        profit1 = max(profit1, price[i] - buy1)

        # Now for buying the 2nd stock,
        # we will integrate profit made
        # from selling the 1st stock
        buy2 = min(buy2, price[i] - profit1)

        # Profit after selling a 2 stocks
        # should be maximum as possible.
        # profit2 tracks maximum possible
        # profit we can make from 0 to i-1.
        profit2 = max(profit2, price[i] - buy2)

    return profit2

# Driver code
price = [ 2, 30, 15, 10, 8, 25, 80 ]
n = len(price)

print("Maximum Profit = ", maxProfit(price, n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implmenetation to find
// maximum possible profit
// with at most two transactions
using System;

class GFG{

// Function to find the maximum
// profit with two transactions
// on a given list of stock prices
static int maxProfit(int []price, int n)
{

    // buy1 - Money lent to buy 1 stock
    // profit1 - Profit after selling
    // the 1st stock buyed.
    // buy2 - Money lent to buy 2 stocks
    // including profit of selling 1st stock
    // profit2 - Profit after selling 2 stocks
    int buy1, profit1, buy2, profit2;

    // Set initial buying values to
    // int.MaxValue as we want to
    // minimize it
    buy1 = buy2 = int.MaxValue;

    // Set initial selling values to
    // zero as we want to maximize it
    profit1 = profit2 = 0;

    for(int i = 0; i < n; i++)
    {

        // Money lent to buy the stock
        // should be minimum as possible.
        // buy1 tracks the minimum possible
        // stock to buy from 0 to i-1.
        buy1 = Math.Min(buy1, price[i]);

        // Profit after selling a stock
        // should be maximum as possible.
        // profit1 tracks maximum possible
        // profit we can make from 0 to i-1.
        profit1 = Math.Max(profit1, price[i] - buy1);

        // Now for buying the 2nd stock,
        // we will integrate profit made
        // from selling the 1st stock
        buy2 = Math.Min(buy2, price[i] - profit1);

        // Profit after selling a 2 stocks
        // should be maximum as possible.
        // profit2 tracks maximum possible
        // profit we can make from 0 to i-1.
        profit2 = Math.Max(profit2, price[i] - buy2);
    }
    return profit2;
}

// Driver Code
public static void Main(String[] args)
{
    int []price = { 2, 30, 15, 10, 8, 25, 80 };
    int n = price.Length;

    Console.Write("Maximum Profit = " +
                   maxProfit(price, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implmenetation to find
// maximum possible profit
// with at most two transactions

    // Function to find the maximum
    // profit with two transactions
    // on a given list of stock prices
    function maxProfit(price , n)
    {

        // buy1 - Money lent to buy 1 stock
        // profit1 - Profit after selling
        // the 1st stock buyed.
        // buy2 - Money lent to buy 2 stocks
        // including profit of selling 1st stock
        // profit2 - Profit after selling 2 stocks
        var buy1, profit1, buy2, profit2;

        // Set initial buying values to
        // Number.MAX_VALUE as we want to
        // minimize it
        buy1 = buy2 = Number.MAX_VALUE;

        // Set initial selling values to
        // zero as we want to maximize it
        profit1 = profit2 = 0;

        for (i = 0; i < n; i++) {

            // Money lent to buy the stock
            // should be minimum as possible.
            // buy1 tracks the minimum possible
            // stock to buy from 0 to i-1.
            buy1 = Math.min(buy1, price[i]);

            // Profit after selling a stock
            // should be maximum as possible.
            // profit1 tracks maximum possible
            // profit we can make from 0 to i-1.
            profit1 = Math.max(profit1, price[i] - buy1);

            // Now for buying the 2nd stock,
            // we will integrate profit made
            // from selling the 1st stock
            buy2 = Math.min(buy2, price[i] - profit1);

            // Profit after selling a 2 stocks
            // should be maximum as possible.
            // profit2 tracks maximum possible
            // profit we can make from 0 to i-1.
            profit2 = Math.max(profit2, price[i] - buy2);
        }
        return profit2;
    }

    // Driver Code   
        var price = [ 2, 30, 15, 10, 8, 25, 80 ];
        var n = price.length;

        document.write("Maximum Profit = " + maxProfit(price, n));

// This code is contributed by todaysgaurav.
</script>
```

**Output:** 

```
Maximum Profit = 100
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)
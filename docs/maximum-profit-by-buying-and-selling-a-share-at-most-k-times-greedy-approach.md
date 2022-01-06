# 最多 K 次买卖一股最大利润|贪婪进场

> 原文:[https://www . geeksforgeeks . org/最高 k 倍贪婪法每股买卖最大利润/](https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-share-at-most-k-times-greedy-approach/)

在股票交易中，买方购买股票并在未来某一天出售。给定 **N** 天的股价，交易者最多可以进行 **K** 次交易，其中新的交易只能在前一次交易完成后开始。任务是找出股票交易者可能获得的最大利润。

**示例:**

> **输入:**价格[] = {10，22，5，75，65，80}，K = 2
> **输出:** 87
> **解释:**交易者进行 2 次交易，第一次是以 10 价买入，以 22 价卖出，然后分别以 5 价和 80 价进行买卖。因此，获得的利润是 87。
> 
> **输入:**价格[] = {12，14，17，10，14，13，12，15}，K = 3
> **输出:** 12
> **说明:**第一笔交易涉及分别以 12 和 17 的价格买入和卖出。第二种是以 10 的价格买入，以 14 的价格卖出，然后以 12 的价格买入，以 15 的价格卖出。因此，总利润为 12。

动态规划方法请参考本文[](https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-share-at-most-k-times/)

******方法:**这个方法展示了如何使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题:****

*   ****找到一只股票上涨前的最低价，然后在价格再次下跌前找到最高价。这些分别作为当前的买卖价格。****
*   ****将这些买卖价格与前一笔交易的价格进行比较。如果当前买入价小于上一笔交易的买入价，则移除该笔交易，并考虑用移除交易的当前买入价和卖出价进行新的交易，以增加利润，只要利润可以用当前买入价进一步增加，就继续进行。****
*   ****同样，比较销售价格，如果可能的话增加利润。****
*   ****遍历所有 **N** 价格后，添加最高的 **K** 利润。如果交易数量少于 **K** ，计算所有交易的利润之和。****

****下面的代码是上述方法的实现:****

## ****C++14****

```
**// C++ program to find out maximum profit by
// buying and selling a share at most k times
// given the stock price of n days

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum profit
int maxProfit(int n, int k, int prices[])
{
    int ans = 0, buy = 0, sell = 0;

    stack<pair<int, int> > transaction;
    priority_queue<int> profits;

    while (sell < n) {

        buy = sell;

        // Find the farthest decreasing span
        // of prices before prices rise
        while (buy < n - 1
               && prices[buy] >= prices[buy + 1])
            buy++;

        sell = buy + 1;

        // Find the farthest increasing span
        // of prices before prices fall again
        while (sell < n
               && prices[sell] >= prices[sell - 1])
            sell++;

        // Check if the current buying price
        // is greater than that
        // of the previous transaction
        while (!transaction.empty()
               && prices[buy]
                      < prices[transaction.top().first]) {
            pair<int, int> p = transaction.top();

            // Store the profit
            profits.push(prices[p.second - 1]
                         - prices[p.first]);

            // Remove the previous transaction
            transaction.pop();
        }

        // Check if the current selling price is
        // less than that of the previous transactions
        while (!transaction.empty()
               && prices[sell - 1]
                      > prices[transaction.top().second - 1]) {
            pair<int, int> p = transaction.top();

            // Store the new profit
            profits.push(prices[p.second - 1]
                         - prices[buy]);
            buy = p.first;

            // Remove the previous transaction
            transaction.pop();
        }

        // Add the new transactions
        transaction.push({ buy, sell });
    }

    // Finally store the profits
    // of all the transactions
    while (!transaction.empty()) {
        profits.push(
            prices[transaction.top().second - 1]
            - prices[transaction.top().first]);
        transaction.pop();
    }

    // Add the highest K profits
    while (k && !profits.empty()) {
        ans += profits.top();
        profits.pop();
        --k;
    }

    // Return the maximum profit
    return ans;
}

// Driver code
int main()
{
    int k = 3;
    int prices[] = { 1, 12, 10, 7,
                     10, 13, 11, 10,
                     7, 6, 9 };
    int n = sizeof(prices) / sizeof(prices[0]);

    cout << "Maximum profit is "
         << maxProfit(n, k, prices);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to find out maximum profit
// by buying and selling a share at most k
// times given the stock price of n days
import java.util.*;
import java.lang.*;

class GFG{

// Function to return the maximum profit
static int maxProfit(int n, int k,
                     int prices[])
{
    int ans = 0, buy = 0, sell = 0;

    Stack<int[]> transaction = new Stack<>();
    PriorityQueue<Integer> profits = new PriorityQueue<>();

    while (sell < n)
    {
        buy = sell;

        // Find the farthest decreasing span
        // of prices before prices rise
        while (buy < n - 1 &&
        prices[buy] >= prices[buy + 1])
            buy++;

        sell = buy + 1;

        // Find the farthest increasing span
        // of prices before prices fall again
        while (sell < n &&
        prices[sell] >= prices[sell - 1])
            sell++;

        // Check if the current buying price
        // is greater than that of the
        // previous transaction
        while (!transaction.isEmpty() &&
               prices[buy] <
               prices[transaction.peek()[0]])
        {
            int[] p = transaction.peek();

            // Store the profit
            profits.add(prices[p[1] - 1] -
                        prices[p[0]]);

            // Remove the previous transaction
            transaction.pop();
        }

        // Check if the current selling price
        // is less than that of the previous
        // transactions
        while (!transaction.isEmpty() &&
               prices[sell - 1] >
               prices[transaction.peek()[1] - 1])
        {
            int[] p = transaction.peek();

            // Store the new profit
            profits.add(prices[p[1] - 1] -
                        prices[buy]);

            buy = p[0];

            // Remove the previous transaction
            transaction.pop();
        }

        // Add the new transactions
        transaction.push(new int[]{ buy, sell });
    }

    // Finally store the profits
    // of all the transactions
    while (!transaction.isEmpty())
    {
        profits.add(
            prices[transaction.peek()[1] - 1] -
            prices[transaction.peek()[0]]);

        transaction.pop();
    }

    // Add the highest K profits
    while (k > 0 && !profits.isEmpty())
    {
        ans += profits.peek();
        profits.poll();
        --k;
    }

    // Return the maximum profit
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int k = 3;
    int prices[] = { 1, 12, 10, 7, 10, 13,
                     11, 10, 7, 6, 9 };
    int n = prices.length;

    System.out.println("Maximum profit is " +
                       maxProfit(n, k, prices));
}
}

// This code is contributed by offbeat**
```

## ****蟒蛇 3****

```
**# Python3 program to find out maximum profit by
# buying and selling a share at most k times
# given the stock price of n days

# Function to return the maximum profit
def maxProfit(n, k, prices):
    ans = 0
    buy = 0
    sell = 0
    # stack
    transaction = []
    # priority queue
    profits = []

    while (sell < n):
        buy = sell

        # Find the farthest decreasing span
        # of prices before prices rise
        while (buy < n - 1 and prices[buy] >= prices[buy + 1]):
            buy += 1

        sell = buy + 1

        # Find the farthest increasing span
        # of prices before prices fall again
        while (sell < n and prices[sell] >= prices[sell - 1]):
            sell += 1

        # Check if the current buying price
        # is greater than that
        # of the previous transaction
        while (len(transaction) !=0 and prices[buy] < prices[transaction[len(transaction)-1][0]]):
            p = transaction[len(transaction)-1]

            # Store the profit
            profits.append(prices[p[1] - 1] - prices[p[0]])

            # Remove the previous transaction
            transaction.remove(transaction[len(transaction)-1])

        # Check if the current selling price is
        # less than that of the previous transactions
        profits.sort(reverse=True)
        while (len(transaction)!=0 and prices[sell - 1] > prices[transaction[len(transaction)-1][1] - 1]):
            p = transaction[len(transaction)-1]

            # Store the new profit
            profits.append(prices[p[1] - 1] - prices[buy])
            buy = p[0]

            # Remove the previous transaction
            transaction.remove(transaction[len(transaction)-1])

        # Add the new transactions
        transaction.append([buy, sell])

    profits.sort(reverse=True)
    # Finally store the profits
    # of all the transactions
    while (len(transaction) != 0):
        profits.append(prices[transaction[len(transaction)-1][1]- 1]-prices[transaction[len(transaction)-1][0]])
        transaction.remove(transaction[len(transaction)-1])

    profits.sort(reverse=True)
    # Add the highest K profits
    while (k!=0 and len(profits)!=0):
        ans += profits[0]
        profits.remove(profits[0])
        k -= 1

    # Return the maximum profit
    return ans

# Driver code
if __name__ == '__main__':
    k = 3
    prices = [1, 12, 10, 7,10, 13, 11, 10,7, 6, 9]
    n = len(prices)

    print("Maximum profit is",maxProfit(n, k, prices))

# This code is contributed by Surendra_Gangwar**
```

******Output:** 

```
Maximum profit is 20

```**** 

*******时间复杂度:**O(N * log N)*T4】****
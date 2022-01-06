# 根据每天给定的利率交易股票，实现利润最大化

> 原文:[https://www . geeksforgeeks . org/基于给定每日费率的股票交易利润最大化/](https://www.geeksforgeeks.org/maximize-profit-by-trading-stocks-based-on-given-rate-per-day/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，表示在 **N** 天的每一天买卖股票的成本。任务是找到在某一天买入一只股票或卖出所有先前买入的股票所能获得的最大利润。
**举例:**

> **输入:** arr[] = {2，3，5}
> **输出:** 5
> **说明:**
> 第 1 天价格= 2。因此，以这个价格在第一天购买股票。total _ wasted = 2
> 第 2 天的价格= 3。因此，以这个价格在第二天买入股票。total _ wasted = 2+3 = 5
> 第 3 天的价格= 5。如果股票以这个价格出售，利润将是最大的。因此，在第三天以这个价格卖出买入的股票。total _ gain = 5 * 2 = 10
> 利润= 10–5 = 5
> **输入:** arr[] = {8，5，1}
> **输出:** 0
> **说明:**
> 买了任何一只股票后我们不能在其他任何一天卖出，因为会导致亏损。因此利润为 0。

**方法:**想法是把给定的股票价格分解成不同的子阵列，使得每个子阵列在阵列末端有最大值。然后，通过从每个子阵列的最后一个元素中减去每个股票价值来找到利润。以下是步骤:

1.  从头到尾遍历数组 **arr[]** ，把**arr[N–1]**看作一只股票当前的最高价，比如说 **maxM** 。
2.  只要价格最高，所有之前购买的股票都会获利。因此，在 **arr[]** 中向左移动，继续添加**MaxM–arr[I]**以使所有指数获利，直到任何指数的成本高于 **maxM** 。
3.  如果遇到比 **maxM** 更高的价格，那么买入就会造成亏损。因此，将当天的库存成本，即 arr[i]，设置为 **maxM** 的当前值，并重复**步骤 2** 。
4.  遍历数组后，在**arr【】**中打印步骤 2 中获得的每个可能价格的差值总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum profit
int maxProfit(int* prices, int n)
{
    int profit = 0, currentDay = n - 1;

    // Start from the last day
    while (currentDay > 0) {

        int day = currentDay - 1;

        // Traverse and keep adding the
        // profit until a day with
        // price of stock higher
        // than currentDay is obtained
        while (day >= 0
            && (prices[currentDay]
                > prices[day])) {

            profit += (prices[currentDay]
                    - prices[day]);

            day--;
        }

        // Set this day as currentDay
        // with maximum cost of stock
        // currently
        currentDay = day;
    }

    // Return the profit
    return profit;
}

// Driver Code
int main()
{
    // Given array of prices
    int prices[] = { 2, 3, 5 };

    int N = sizeof(prices) / sizeof(prices[0]);

    // Function Call
    cout << maxProfit(prices, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum profit
static int maxProfit(int[] prices, int n)
{
    int profit = 0, currentDay = n - 1;

    // Start from the last day
    while (currentDay > 0)
    {
        int day = currentDay - 1;

        // Traverse and keep adding the
        // profit until a day with
        // price of stock higher
        // than currentDay is obtained
        while (day >= 0 &&
            (prices[currentDay] > prices[day]))
        {
            profit += (prices[currentDay] -
                    prices[day]);

            day--;
        }

        // Set this day as currentDay
        // with maximum cost of stock
        // currently
        currentDay = day;
    }

    // Return the profit
    return profit;
}

// Driver Code
public static void main(String[] args)
{
    // Given array of prices
    int prices[] = { 2, 3, 5 };

    int N = prices.length;

    // Function Call
    System.out.print(maxProfit(prices, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement
# above approach

# Function to find the maximum profit
def maxProfit(prices, n):

    profit = 0
    currentDay = n - 1

    # Start from the last day
    while (currentDay > 0):
        day = currentDay - 1

        # Traverse and keep adding the
        # profit until a day with
        # price of stock higher
        # than currentDay is obtained
        while (day >= 0 and
              (prices[currentDay] >
               prices[day])):
            profit += (prices[currentDay] -
                       prices[day])

            day -= 1

        # Set this day as currentDay
        # with maximum cost of stock
        # currently
        currentDay = day;

    # Return the profit
    return profit;

# Driver Code

# Given array of prices
prices = [ 2, 3, 5 ]

N = len(prices)

# Function call
print(maxProfit(prices, N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum profit
static int maxProfit(int[] prices, int n)
{
    int profit = 0, currentDay = n - 1;

    // Start from the last day
    while (currentDay > 0)
    {
        int day = currentDay - 1;

        // Traverse and keep adding the
        // profit until a day with
        // price of stock higher
        // than currentDay is obtained
        while (day >= 0 &&
              (prices[currentDay] > prices[day]))
        {
            profit += (prices[currentDay] -
                       prices[day]);

            day--;
        }

        // Set this day as currentDay
        // with maximum cost of stock
        // currently
        currentDay = day;
    }

    // Return the profit
    return profit;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array of prices
    int []prices = { 2, 3, 5 };

    int N = prices.Length;

    // Function call
    Console.Write(maxProfit(prices, N));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above problem.

// Function to find the maximum profit
function maxProfit(prices, n)
{
    let profit = 0, currentDay = n - 1;

    // Start from the last day
    while (currentDay > 0)
    {
        let day = currentDay - 1;

        // Traverse and keep adding the
        // profit until a day with
        // price of stock higher
        // than currentDay is obtained
        while (day >= 0 &&
              (prices[currentDay] > prices[day]))
        {
            profit += (prices[currentDay] -
                       prices[day]);

            day--;
        }

        // Set this day as currentDay
        // with maximum cost of stock
        // currently
        currentDay = day;
    }

    // Return the profit
    return profit;
}

// Driver code

    // Given array of prices
    let prices = [2, 3, 5];

    let N = prices.length;

    // Function call
    document.write(maxProfit(prices, N));

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
5
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*
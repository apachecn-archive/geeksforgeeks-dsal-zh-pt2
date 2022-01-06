# 股票买卖最大化利润的 C 程序

> 原文:[https://www . geesforgeks . org/c-程序换股票-买入-卖出-利润最大化-2/](https://www.geeksforgeeks.org/c-program-for-stock-buy-sell-to-maximize-profit-2/)

**高效方法:**如果只允许我们买卖一次，那么我们可以使用以下算法。[两个元素之间的最大差异](https://www.geeksforgeeks.org/maximum-difference-between-two-elements/)。在这里，我们可以多次买卖。
下面是这个问题的算法。

1.  找到局部最小值并将其存储为起始索引。如果不存在，返回。
2.  找到局部极大值。并将其存储为结束索引。如果我们到达终点，将终点设置为终点索引。
3.  更新解决方案(增加买卖对的计数)
4.  如果没有到达终点，重复上述步骤。

## C

```
// Program to find best buying and 
// selling days
#include <stdio.h>

// Solution structure
struct Interval 
{
    int buy;
    int sell;
};

// This function finds the buy and sell 
// schedule for maximum profit
void stockBuySell(int price[], int n)
{
    // Prices must be given for at 
    // least two days
    if (n == 1)
        return;

    // Count of solution pairs
    int count = 0; 

    // Solution vector
    Interval sol[n / 2 + 1];

    // Traverse through given price array
    int i = 0;
    while (i < n - 1) 
    {
        // Find Local Minima. Note that the 
        // limit is (n-2) as we are comparing 
        // present element to the next element.
        while ((i < n - 1) && 
               (price[i + 1] <= price[i]))
            i++;

        // If we reached the end, break as no 
        // further solution possible
        if (i == n - 1)
            break;

        // Store the index of minima
        sol[count].buy = i++;

        // Find Local Maxima.  Note that the 
        // limit is (n-1) as we are comparing 
        // to previous element
        while ((i < n) && 
               (price[i] >= price[i - 1]))
            i++;

        // Store the index of maxima
        sol[count].sell = i - 1;

        // Increment count of buy/sell pairs
        count++;
    }

    // Print solution
    if (count == 0)
        printf(
        "There is no day when buying the stock will make profitn");
    else 
    {
        for (int i = 0; i < count; i++)
            printf(
            "Buy on day: %dt Sell on day: %dn", sol[i].buy, sol[i].sell);
    }

    return;
}

// Driver code
int main()
{
    // Stock prices on consecutive days
    int price[] = {100, 180, 260, 
                   310, 40, 535, 695};
    int n = sizeof(price) / sizeof(price[0]);

    // Function call
    stockBuySell(price, n);

    return 0;
}
```

**输出:**

```
Buy on day: 0     Sell on day: 3
Buy on day: 4     Sell on day: 6
```

**时间复杂度:**外环运行到我变成 n-1。内部两个循环在每次迭代中增加 I 的值。所以总的时间复杂度是 O(n)

更多详情请参考[股票买卖实现利润最大化](https://www.geeksforgeeks.org/stock-buy-sell/)整篇文章！
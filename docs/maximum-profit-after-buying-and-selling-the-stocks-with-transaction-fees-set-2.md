# 带交易费买卖股票后的最大利润|第 2 套

> 原文:[https://www . geeksforgeeks . org/带交易费的股票买卖后最大利润-set-2/](https://www.geeksforgeeks.org/maximum-profit-after-buying-and-selling-the-stocks-with-transaction-fees-set-2/)

给定一个代表股票价格的正整数数组**【arr】**和一个整数**交易费**，任务是在买卖股票任意多次并给出每笔交易的交易费后，找到可能的**最大利润**。

**示例:**

> **输入:** arr[] = {6，1，7，2，8，4}，交易费= 2
> **输出:** 8
> **说明:**
> 两笔交易最多可获得 8 的利润。
> 交易 1:以 1 价买入，7 价卖出。利润= 7–1–2 = 4。
> 交易 2:以 2 价买入，8 价卖出。利润= 8–2–2 = 4。
> 因此，利润总额= 4 + 4 = 8，这是最大可能。
> 
> **输入:** arr[] = {2，7，5，9，6，4}，交易费= 1
> **输出:** 7

**天真的做法:**参考[之前的帖子](https://www.geeksforgeeks.org/maximum-profit-after-buying-and-selling-the-stocks-with-transaction-fees/)最简单的解决问题的方法。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)T4。每天保持**最大利润，**当日买入(**买入**)当日全部卖出(**卖出**)最大利润。每天使用以下关系更新**买入**和**卖出**:

> **买入=最大(卖出-arr[I]，买入)**
> **卖出=最大(买入+arr[I]–交易费，卖出)**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// profit with transaction fee
int MaxProfit(int arr[], int n,
              int transactionFee)
{

    int buy = -arr[0];
    int sell = 0;

    // Traversing the stocks for
    // each day
    for (int i = 1; i < n; i++) {
        int temp = buy;

        // Update buy and sell
        buy = max(buy, sell - arr[i]);
        sell = max(sell,
                   temp + arr[i] - transactionFee);
    }

    // Return the maximum profit
    return max(sell, buy);
}

// Driver code
int main()
{
    // Given Input
    int arr[] = { 6, 1, 7, 2, 8, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int transactionFee = 2;

    // Function Call
    cout << MaxProfit(arr, n, transactionFee);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find the maximum
    // profit with transaction fee
    static int MaxProfit(int arr[], int n,
                         int transactionFee)
    {

        int buy = -arr[0];
        int sell = 0;

        // Traversing the stocks for
        // each day
        for (int i = 1; i < n; i++) {
            int temp = buy;

            // Update buy and sell
            buy = Math.max(buy, sell - arr[i]);
            sell = Math.max(sell,
                            temp + arr[i] - transactionFee);
        }

        // Return the maximum profit
        return Math.max(sell, buy);
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given Input
        int arr[] = { 6, 1, 7, 2, 8, 4 };
        int n = arr.length;
        int transactionFee = 2;

        // Function Call
        System.out.println(
            MaxProfit(arr, n, transactionFee));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum
# profit with transaction fee
def MaxProfit(arr, n, transactionFee):

    buy = -arr[0]
    sell = 0

    # Traversing the stocks for
    # each day
    for i in range(1, n, 1):
        temp = buy

        # Update buy and sell
        buy = max(buy, sell - arr[i])
        sell = max(sell, temp + arr[i] -
                   transactionFee)

    # Return the maximum profit
    return max(sell, buy)

# Driver code
if __name__ == '__main__':

    # Given Input
    arr = [ 6, 1, 7, 2, 8, 4 ]
    n = len(arr)
    transactionFee = 2

    # Function Call
    print(MaxProfit(arr, n, transactionFee))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the maximum
    // profit with transaction fee
    static int MaxProfit(int[] arr, int n,
                         int transactionFee)
    {

        int buy = -arr[0];
        int sell = 0;

        // Traversing the stocks for
        // each day
        for (int i = 1; i < n; i++) {
            int temp = buy;

            // Update buy and sell
            buy = Math.Max(buy, sell - arr[i]);
            sell = Math.Max(sell,
                            temp + arr[i] - transactionFee);
        }

        // Return the maximum profit
        return Math.Max(sell, buy);
    }

    // Driver code
    public static void Main()
    {

        // Given Input
        int[] arr = { 6, 1, 7, 2, 8, 4 };
        int n = arr.Length;
        int transactionFee = 2;

        // Function Call
        Console.WriteLine(
            MaxProfit(arr, n, transactionFee));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum
// profit with transaction fee
function MaxProfit(arr, n, transactionFee)
{
    let buy = -arr[0];
    let sell = 0;

    // Traversing the stocks for
    // each day
    for(let i = 1; i < n; i++)
    {
        let temp = buy;

        // Update buy and sell
        buy = Math.max(buy, sell - arr[i]);
        sell = Math.max(sell,
                        temp + arr[i] - transactionFee);
    }

    // Return the maximum profit
    return Math.max(sell, buy);
}

// Driver Code

// Given Input
let arr = [ 6, 1, 7, 2, 8, 4 ];
let n = arr.length;
let transactionFee = 2;

// Function Call
document.write(
    MaxProfit(arr, n, transactionFee));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
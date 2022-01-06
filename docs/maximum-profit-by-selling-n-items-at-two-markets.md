# 在两个市场销售 N 件商品的最大利润

> 原文:[https://www . geeksforgeeks . org/两个市场销售 n 种商品的最大利润/](https://www.geeksforgeeks.org/maximum-profit-by-selling-n-items-at-two-markets/)

给定两个数组， **A[]** 和 **B[]** ，每个数组长度为 **N** ，其中**A【I】**和**B【I】**分别是**I<sup>th</sup>T13】项目在市场 **A** 和市场 **B** 销售时的价格。任务是最大化销售所有 **N** 商品的轮廓，但是有一个陷阱:如果你去了市场 **B** ，那么你不能回来。例如，如果你在市场 A 出售前 k 个项目，而你必须在市场 b 出售剩余的项目。**

**示例:**

> **输入:** A[] = {2，3，2}，B[] = {10，3，40}
> **输出:** 53
> 为了
> 利润最大化卖出市场 B 的所有商品即(10 + 3 + 40) = 53。
> 
> **输入:** A[] = {7，5，3，4}，B[] = {2，3，1，3}
> **输出:** 19

**进场:**

*   创建前缀和数组 **preA[]** ，其中 **preA[i]** 将存储商品 **A[0…i]** 在市场 **A** 上销售时的利润。
*   创建后缀和数组**SufB[]**，其中**SufB[I]**将存储当商品 **B[i…n-1]** 在市场上销售时的利润 **B** 。
*   现在问题简化为找到一个指数 **i** ，使得**(PRa[I]+SubB[I+1])**为最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate max profit
int maxProfit(int profitA[], int profitB[], int n)
{

    // Prefix sum array for profitA[]
    int preSum[n];
    preSum[0] = profitA[0];
    for (int i = 1; i < n; i++) {
        preSum[i] = preSum[i - 1] + profitA[i];
    }

    // Suffix sum array for profitB[]
    int suffSum[n];
    suffSum[n - 1] = profitB[n - 1];
    for (int i = n - 2; i >= 0; i--) {
        suffSum[i] = suffSum[i + 1] + profitB[i];
    }

    // If all the items are sold in market A
    int res = preSum[n - 1];

    // Find the maximum profit when the first i
    // items are sold in market A and the
    // rest of the items are sold in market
    // B for all possible values of i
    for (int i = 1; i < n - 1; i++) {
        res = max(res, preSum[i] + suffSum[i + 1]);
    }

    // If all the items are sold in market B
    res = max(res, suffSum[0]);

    return res;
}

// Driver code
int main()
{
    int profitA[] = { 2, 3, 2 };
    int profitB[] = { 10, 30, 40 };
    int n = sizeof(profitA) / sizeof(int);

    // Function to calculate max profit
    cout << maxProfit(profitA, profitB, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to calculate max profit
    static int maxProfit(int profitA[], int profitB[], int n)
    {

        // Prefix sum array for profitA[]
        int preSum[] = new int[n];
        preSum[0] = profitA[0];
        for (int i = 1; i < n; i++)
        {
            preSum[i] = preSum[i - 1] + profitA[i];
        }

        // Suffix sum array for profitB[]
        int suffSum[] = new int[n];
        suffSum[n - 1] = profitB[n - 1];
        for (int i = n - 2; i >= 0; i--)
        {
            suffSum[i] = suffSum[i + 1] + profitB[i];
        }

        // If all the items are sold in market A
        int res = preSum[n - 1];

        // Find the maximum profit when the first i
        // items are sold in market A and the
        // rest of the items are sold in market
        // B for all possible values of i
        for (int i = 1; i < n - 1; i++)
        {
            res = Math.max(res, preSum[i] + suffSum[i + 1]);
        }

        // If all the items are sold in market B
        res = Math.max(res, suffSum[0]);

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int profitA[] = { 2, 3, 2 };
        int profitB[] = { 10, 30, 40 };
        int n = profitA.length;

        // Function to calculate max profit
        System.out.println(maxProfit(profitA, profitB, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to calculate max profit
def maxProfit(profitA, profitB, n) :

    # Prefix sum array for profitA[]
    preSum = [0] * n;
    preSum[0] = profitA[0];

    for i in range(1, n) :
        preSum[i] = preSum[i - 1] + profitA[i];

    # Suffix sum array for profitB[]
    suffSum = [0] * n;
    suffSum[n - 1] = profitB[n - 1];

    for i in range(n - 2, -1, -1) :
        suffSum[i] = suffSum[i + 1] + profitB[i];

    # If all the items are sold in market A
    res = preSum[n - 1];

    # Find the maximum profit when the first i
    # items are sold in market A and the
    # rest of the items are sold in market
    # B for all possible values of i
    for i in range(1 , n - 1) :
        res = max(res, preSum[i] + suffSum[i + 1]);

    # If all the items are sold in market B
    res = max(res, suffSum[0]);

    return res;

# Driver code
if __name__ == "__main__" :

    profitA = [ 2, 3, 2 ];
    profitB = [ 10, 30, 40 ];
    n = len(profitA);

    # Function to calculate max profit
    print(maxProfit(profitA, profitB, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to calculate max profit
    static int maxProfit(int []profitA,
                        int []profitB, int n)
    {

        // Prefix sum array for profitA[]
        int []preSum = new int[n];
        preSum[0] = profitA[0];
        for (int i = 1; i < n; i++)
        {
            preSum[i] = preSum[i - 1] + profitA[i];
        }

        // Suffix sum array for profitB[]
        int []suffSum = new int[n];
        suffSum[n - 1] = profitB[n - 1];
        for (int i = n - 2; i >= 0; i--)
        {
            suffSum[i] = suffSum[i + 1] + profitB[i];
        }

        // If all the items are sold in market A
        int res = preSum[n - 1];

        // Find the maximum profit when the first i
        // items are sold in market A and the
        // rest of the items are sold in market
        // B for all possible values of i
        for (int i = 1; i < n - 1; i++)
        {
            res = Math.Max(res, preSum[i] +
                            suffSum[i + 1]);
        }

        // If all the items are sold in market B
        res = Math.Max(res, suffSum[0]);

        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []profitA = { 2, 3, 2 };
        int []profitB = { 10, 30, 40 };
        int n = profitA.Length;

        // Function to calculate max profit
        Console.WriteLine(maxProfit(profitA, profitB, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
// Function to calculate max profit
function maxProfit(profitA, profitB, n) {

    // Prefix sum array for profitA[]
    let preSum = new Array(n);

    preSum[0] = profitA[0];

    for (let i = 1; i < n; i++) {
        preSum[i] = preSum[i - 1] + profitA[i];
    }

    // Suffix sum array for profitB[]
    let suffSum = new Array(n);
    suffSum[n - 1] = profitB[n - 1];

    for (let i = n - 2; i >= 0; i--) {
        suffSum[i] = suffSum[i + 1] + profitB[i];
    }

    // If all the items are sold in market A
    let res = preSum[n - 1];

    // Find the maximum profit when the first i
    // items are sold in market A and the
    // rest of the items are sold in market
    // B for all possible values of i
    for (let i = 1; i < n - 1; i++) {
        res = Math.max(res, preSum[i] + suffSum[i + 1]);
    }

    // If all the items are sold in market B
    res = Math.max(res, suffSum[0]);

    return res;
}

// Driver code

let profitA = [2, 3, 2];
let profitB = [10, 30, 40];
let n = profitA.length;

// Function to calculate max profit
document.write(maxProfit(profitA, profitB, n));
</script>
```

**Output:** 

```
80
```

**Python 中的替代实现:**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int maxProfit(vector<int> a, vector<int> b, int n)
{

    // Max profit will be saved here
    int maxP = -1;

    // loop to check all possible combinations of sales
    for (int i = 0; i < n + 1; i++) {

        // the sum of the profit after the sale
        // for products 0 to i in market A
        int sumA = 0;

        for (int j = 0; j < min(i, (int)a.size()); j++)
            sumA += a[j];

        // the sum of the profit after the sale
        // for products i to n in market B
        int sumB = 0;
        for (int j = i; j < b.size(); j++)
            sumB += b[j];

        // Replace the value of Max Profit with a
        // bigger value among maxP and sumA+sumB
        maxP = max(maxP, sumA + sumB);
    }

    //  Return the value of Max Profit
    return maxP;
}

// Driver Program11111111111111111111111
int main()
{
    vector<int> a = { 2, 3, 2 };
    vector<int> b = { 10, 30, 40 };
    cout << maxProfit(a, b, 4);
    return 0;
}

// This code is contributed by pankajsharmagfg.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def maxProfit (a, b, n):

    # Max profit will be saved here
    maxP = -1

    # loop to check all possible combinations of sales
    for i in range(0, n+1):

        # the sum of the profit after the sale
        # for products 0 to i in market A
        sumA = sum(a[:i])

        # the sum of the profit after the sale
        # for products i to n in market B
        sumB = sum(b[i:])

        # Replace the value of Max Profit with a
        # bigger value among maxP and sumA+sumB
        maxP = max(maxP, sumA+sumB)

    #  Return the value of Max Profit
    return maxP

# Driver Program
if __name__ == "__main__" : 
    a = [2, 3, 2]
    b = [10, 30, 40]
    print(maxProfit(a, b, 4))

# This code is contributed by aman_malhotra
```

**Output:** 

```
80
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
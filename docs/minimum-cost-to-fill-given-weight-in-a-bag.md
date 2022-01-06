# 在袋子中装入给定重量的最小成本

> 原文:[https://www . geeksforgeeks . org/最小填充成本-给定袋中重量/](https://www.geeksforgeeks.org/minimum-cost-to-fill-given-weight-in-a-bag/)

给你一袋 W 公斤大小的橘子，并向你提供不同重量的橘子包的成本，排列成本[]其中**成本【I】**基本上是**【I】**公斤橘子包的成本。其中成本[i] = -1 表示**‘I’**公斤橘子包不可用
找出购买正好 W 公斤橘子的最小总成本，如果不可能购买正好 W 公斤橘子，则打印-1。可以假设所有可用的包类型都有无限的供应。
**<u>注:</u>** 数组从索引 1 开始。

**示例:**

```
Input  : W = 5, cost[] = {20, 10, 4, 50, 100}
Output : 14
We can choose two oranges to minimize cost. First 
orange of 2Kg and cost 10\. Second orange of 3Kg
and cost 4\. 

Input  : W = 5, cost[] = {1, 10, 4, 50, 100}
Output : 5
We can choose five oranges of weight 1 kg.

Input  : W = 5, cost[] = {1, 2, 3, 4, 5}
Output : 5
Costs of 1, 2, 3, 4 and 5 kg packets are 1, 2, 3, 
4 and 5 Rs respectively. 
We choose packet of 5kg having cost 5 for minimum
cost to get 5Kg oranges.

Input  : W = 5, cost[] = {-1, -1, 4, 5, -1}
Output : -1
Packets of size 1, 2 and 5 kg are unavailable
because they have cost -1\. Cost of 3 kg packet 
is 4 Rs and of 4 kg is 5 Rs. Here we have only 
weights 3 and 4 so by using these two we can  
not make exactly W kg weight, therefore answer 
is -1.
```

这个问题可以简化为[无界 Knapsac](https://www.geeksforgeeks.org/unbounded-knapsack-repetition-items-allowed/) k，所以在成本数组中，我们首先忽略那些不可用的包，即；成本为-1，然后遍历成本数组，创建两个数组 val[]用于存储**‘I’**公斤橘子包的成本，wt[]用于存储相应包的重量。假设成本[i] = 50，那么包的重量将是 I，成本将是 50。
**<u>算法:</u>**

*   创建矩阵 min_cost[n+1][W+1]，其中 n 是不同加权的橙色包的数量，W 是包的最大容量。
*   用 INF(无穷大)初始化第 0 行，用 0 初始化第 0 列。
*   现在填充矩阵
    *   如果 wt[i-1] > j，则 min _ cost[I][j]= min _ cost[I-1][j]；
    *   如果 wt[i-1] <= j，则 min _ cost[I][j]= min(min _ cost[I-1][j]，val[I-1]+min _ cost[I][j-wt[I-1]])；
*   如果 min_cost[n][W]==INF，那么输出将是-1，因为这意味着我们不能通过使用这些权重来制作权重 W，否则输出将是 **min_cost[n][W]** 。

## C++

```
// C++ program to find minimum cost to get exactly
// W Kg with given packets
#include<bits/stdc++.h>
#define INF 1000000
using namespace std;

// cost[] initial cost array including unavailable packet
// W capacity of bag
int MinimumCost(int cost[], int n, int W)
{
    // val[] and wt[] arrays
    // val[] array to store cost of 'i' kg packet of orange
    // wt[] array weight of packet of orange
    vector<int> val, wt;

    // traverse the original cost[] array and skip
    // unavailable packets and make val[] and wt[]
    // array. size variable tells the available number
    // of distinct weighted packets
    int size = 0;
    for (int i=0; i<n; i++)
    {
        if (cost[i]!= -1)
        {
            val.push_back(cost[i]);
            wt.push_back(i+1);
            size++;
        }
    }

    n = size;
    int min_cost[n+1][W+1];

    // fill 0th row with infinity
    for (int i=0; i<=W; i++)
        min_cost[0][i] = INF;

    // fill 0'th column with 0
    for (int i=1; i<=n; i++)
        min_cost[i][0] = 0;

    // now check for each weight one by one and fill the
    // matrix according to the condition
    for (int i=1; i<=n; i++)
    {
        for (int j=1; j<=W; j++)
        {
            // wt[i-1]>j means capacity of bag is
            // less then weight of item
            if (wt[i-1] > j)
                min_cost[i][j] = min_cost[i-1][j];

            // here we check we get minimum cost either
            // by including it or excluding it
            else
                min_cost[i][j] = min(min_cost[i-1][j],
                     min_cost[i][j-wt[i-1]] + val[i-1]);
        }
    }

    // exactly weight W can not be made by given weights
    return (min_cost[n][W]==INF)? -1: min_cost[n][W];
}

// Driver program to run the test case
int main()
{
    int cost[] = {1, 2, 3, 4, 5}, W = 5;
    int n = sizeof(cost)/sizeof(cost[0]);

    cout << MinimumCost(cost, n, W);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for Minimum cost to
// fill given weight in a bag
import java.util.*;

class GFG {

    // cost[] initial cost array including
    // unavailable packet W capacity of bag
    public static int MinimumCost(int cost[], int n,
                                             int W)
    {
        // val[] and wt[] arrays
        // val[] array to store cost of 'i' kg
        // packet of orange wt[] array weight of
        // packet of orange
        Vector<Integer> val = new Vector<Integer>();
        Vector<Integer> wt = new Vector<Integer>();

        // traverse the original cost[] array and skip
        // unavailable packets and make val[] and wt[]
        // array. size variable tells the available
        // number of distinct weighted packets
        int size = 0;
        for (int i = 0; i < n; i++)
        {
            if (cost[i] != -1)
            {
                val.add(cost[i]);
                wt.add(i + 1);
                size++;
            }
        }

        n = size;
        int min_cost[][] = new int[n+1][W+1];

        // fill 0th row with infinity
        for (int i = 0; i <= W; i++)
            min_cost[0][i] = Integer.MAX_VALUE;

        // fill 0'th column with 0
        for (int i = 1; i <= n; i++)
            min_cost[i][0] = 0;

        // now check for each weight one by one and
        // fill the matrix according to the condition
        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= W; j++)
            {
                // wt[i-1]>j means capacity of bag is
                // less then weight of item
                if (wt.get(i-1) > j)
                    min_cost[i][j] = min_cost[i-1][j];

                // here we check we get minimum cost
                // either by including it or excluding
                // it
                else
                    min_cost[i][j] = Math.min(min_cost[i-1][j],
                                  min_cost[i][j-wt.get(i-1)] +
                                              val.get(i-1));
            }
        }

        // exactly weight W can not be made by
        // given weights
        return (min_cost[n][W] == Integer.MAX_VALUE)? -1:
                                        min_cost[n][W];
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
         int cost[] = {1, 2, 3, 4, 5}, W = 5;
            int n = cost.length;

        System.out.println(MinimumCost(cost, n, W));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python program to find minimum cost to get exactly
# W Kg with given packets

INF = 1000000

# cost[] initial cost array including unavailable packet
# W capacity of bag
def MinimumCost(cost, n, W):

    # val[] and wt[] arrays
    # val[] array to store cost of 'i' kg packet of orange
    # wt[] array weight of packet of orange
    val = list()
    wt= list()

    # traverse the original cost[] array and skip
    # unavailable packets and make val[] and wt[]
    # array. size variable tells the available number
    # of distinct weighted packets.
    size = 0
    for i in range(n):
        if (cost[i] != -1):
            val.append(cost[i])
            wt.append(i+1)
            size += 1

    n = size
    min_cost = [[0 for i in range(W+1)] for j in range(n+1)]

    # fill 0th row with infinity
    for i in range(W+1):
        min_cost[0][i] = INF

    # fill 0th column with 0
    for i in range(1, n+1):
        min_cost[i][0] = 0

    # now check for each weight one by one and fill the
    # matrix according to the condition
    for i in range(1, n+1):
        for j in range(1, W+1):
            # wt[i-1]>j means capacity of bag is
            # less than weight of item
            if (wt[i-1] > j):
                min_cost[i][j] = min_cost[i-1][j]

            # here we check we get minimum cost either
            # by including it or excluding it
            else:
                min_cost[i][j] = min(min_cost[i-1][j],
                    min_cost[i][j-wt[i-1]] + val[i-1])

    # exactly weight W can not be made by given weights
    if(min_cost[n][W] == INF):
        return -1
    else:
        return min_cost[n][W]

# Driver program to run the test case
cost = [1, 2, 3, 4, 5]
W = 5
n = len(cost)

print(MinimumCost(cost, n, W))

# This code is contributed by Soumen Ghosh.
```

## C#

```
// C# Code for Minimum cost to
// fill given weight in a bag

using System;
using System.Collections.Generic;

class GFG {

    // cost[] initial cost array including
    // unavailable packet W capacity of bag
    public static int MinimumCost(int []cost, int n,
                                            int W)
    {
        // val[] and wt[] arrays
        // val[] array to store cost of 'i' kg
        // packet of orange wt[] array weight of
        // packet of orange
        List<int> val = new List<int>();
        List<int> wt = new List<int>();

        // traverse the original cost[] array and skip
        // unavailable packets and make val[] and wt[]
        // array. size variable tells the available
        // number of distinct weighted packets
        int size = 0;
        for (int i = 0; i < n; i++)
        {
            if (cost[i] != -1)
            {
                val.Add(cost[i]);
                wt.Add(i + 1);
                size++;
            }
        }

        n = size;
        int [,]min_cost = new int[n+1,W+1];

        // fill 0th row with infinity
        for (int i = 0; i <= W; i++)
            min_cost[0,i] = int.MaxValue;

        // fill 0'th column with 0
        for (int i = 1; i <= n; i++)
            min_cost[i,0] = 0;

        // now check for each weight one by one and
        // fill the matrix according to the condition
        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= W; j++)
            {
                // wt[i-1]>j means capacity of bag is
                // less then weight of item
                if (wt[i-1] > j)
                    min_cost[i,j] = min_cost[i-1,j];

                // here we check we get minimum cost
                // either by including it or excluding
                // it
                else
                    min_cost[i,j] = Math.Min(min_cost[i-1,j],
                                min_cost[i,j-wt[i-1]] + val[i-1]);
            }
        }

        // exactly weight W can not be made by
        // given weights
        return (min_cost[n,W] == int.MaxValue )? -1: min_cost[n,W];
    }

    /* Driver program to test above function */
    public static void Main()
    {
            int []cost = {1, 2, 3, 4, 5};
            int W = 5;
            int n = cost.Length;

            Console.WriteLine(MinimumCost(cost, n, W));
    }
}
// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum cost to
// get exactly W Kg with given packets
$INF = 1000000;

// cost[] initial cost array including
// unavailable packet W capacity of bag
function MinimumCost(&$cost, $n, $W)
{
    global $INF;

    // val[] and wt[] arrays
    // val[] array to store cost of 'i'
    // kg packet of orange
    // wt[] array weight of packet of orange
    $val = array();
    $wt = array();

    // traverse the original cost[] array
    // and skip unavailable packets and
    // make val[] and wt[] array. size
    // variable tells the available number
    // of distinct weighted packets
    $size = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($cost[$i] != -1)
        {
            array_push($val, $cost[$i]);
            array_push($wt, $i + 1);
            $size++;
        }
    }

    $n = $size;
    $min_cost = array_fill(0, $n + 1,
                array_fill(0, $W + 1, NULL));

    // fill 0th row with infinity
    for ($i = 0; $i <= $W; $i++)
        $min_cost[0][$i] = $INF;

    // fill 0'th column with 0
    for ($i = 1; $i <= $n; $i++)
        $min_cost[$i][0] = 0;

    // now check for each weight one by
    // one and fill the matrix according
    // to the condition
    for ($i = 1; $i <= $n; $i++)
    {
        for ($j = 1; $j <= $W; $j++)
        {
            // wt[i-1]>j means capacity of bag
            // is less then weight of item
            if ($wt[$i - 1] > $j)
                $min_cost[$i][$j] = $min_cost[$i - 1][$j];

            // here we check we get minimum
            // cost either by including it
            // or excluding it
            else
                $min_cost[$i][$j] = min($min_cost[$i - 1][$j],
                                        $min_cost[$i][$j - $wt[$i - 1]] +
                                                           $val[$i - 1]);
        }
    }

    // exactly weight W can not be made
    // by given weights
    if ($min_cost[$n][$W] == $INF)
            return -1;
    else
        return $min_cost[$n][$W];
}

// Driver Code
$cost = array(1, 2, 3, 4, 5);
$W = 5;
$n = sizeof($cost);
echo MinimumCost($cost, $n, $W);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum cost to get exactly
    // W Kg with given packets

    let INF = 1000000;

    // cost[] initial cost array including unavailable packet
    // W capacity of bag
    function MinimumCost(cost, n, W)
    {
        // val[] and wt[] arrays
        // val[] array to store cost of 'i' kg packet of orange
        // wt[] array weight of packet of orange
        let val = [], wt = [];

        // traverse the original cost[] array and skip
        // unavailable packets and make val[] and wt[]
        // array. size variable tells the available number
        // of distinct weighted packets
        let size = 0;
        for (let i=0; i<n; i++)
        {
            if (cost[i]!= -1)
            {
                val.push(cost[i]);
                wt.push(i+1);
                size++;
            }
        }

        n = size;
        let min_cost = new Array(n+1);
        for(let i = 0; i < n + 1; i++)
        {
            min_cost[i] = new Array(W + 1);
        }

        // fill 0th row with infinity
        for (let i=0; i<=W; i++)
            min_cost[0][i] = INF;

        // fill 0'th column with 0
        for (let i=1; i<=n; i++)
            min_cost[i][0] = 0;

        // now check for each weight one by one and fill the
        // matrix according to the condition
        for (let i=1; i<=n; i++)
        {
            for (let j=1; j<=W; j++)
            {
                // wt[i-1]>j means capacity of bag is
                // less then weight of item
                if (wt[i-1] > j)
                    min_cost[i][j] = min_cost[i-1][j];

                // here we check we get minimum cost either
                // by including it or excluding it
                else
                    min_cost[i][j] = Math.min(min_cost[i-1][j],
                         min_cost[i][j-wt[i-1]] + val[i-1]);
            }
        }

        // exactly weight W can not be made by given weights
        return (min_cost[n][W]==INF)? -1: min_cost[n][W];
    }

    // Driver code
    let cost = [1, 2, 3, 4, 5], W = 5;
    let n = cost.length;

    document.write(MinimumCost(cost, n, W));

    // This code is contributed by suresh07.
</script>
```

**Output**

```
5
```
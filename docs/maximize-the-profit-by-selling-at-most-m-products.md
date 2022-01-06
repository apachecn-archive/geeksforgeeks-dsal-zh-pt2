# 最多销售 M 款产品最大化利润

> 原文:[https://www . geeksforgeeks . org/通过最多销售 m 种产品实现利润最大化/](https://www.geeksforgeeks.org/maximize-the-profit-by-selling-at-most-m-products/)

给出两个列表，分别包含产品的成本价 CP[]和售价 SP[]。任务是通过销售最多的“M”产品来最大化利润。

**示例:**

> **输入:** N = 5，M = 3
> CP[]= {5，10，35，7，23}
> SP[] = {11，10，0，9，19 }
> T5】输出: 8
> 第 0 个产品的利润即 11-5 = 6
> 第 3 个产品的利润即 9-7 = 2
> 销售任何其他产品都不会带来利润。
> 所以，利润总额= 6+2 = 8。
> 
> **输入:** N = 4，M = 2
> CP[] = {17，9，8，20}
> SP[] = {10，9，8，27 }
> T5】输出: 7

**进场:**

1.  将每个产品的买卖盈亏情况，即 **SP[i]-CP[i]** 存储在一个数组中。
2.  按降序排列该数组。
3.  将正值与 M 值相加，正值表示利润。
4.  返回总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach:
#include <bits/stdc++.h>
using namespace std;

// Function to find profit
int solve(int N, int M, int cp[], int sp[])
{
    int profit[N];

    // Calculating profit for each gadget
    for (int i = 0; i < N; i++)
        profit[i] = sp[i] - cp[i];

    // sort the profit array in descending order
    sort(profit, profit + N, greater<int>());

    // variable to calculate total profit
    int sum = 0;

    // check for best M profits
    for (int i = 0; i < M; i++) {
        if (profit[i] > 0)
            sum += profit[i];
        else
            break;
    }

    return sum;
}

// Driver Code
int main()
{

    int N = 5, M = 3;
    int CP[] = { 5, 10, 35, 7, 23 };
    int SP[] = { 11, 10, 0, 9, 19 };

    cout << solve(N, M, CP, SP);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach:
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to find profit
static int solve(int N, int M,
                 int cp[], int sp[])
{
    Integer []profit = new Integer[N];

    // Calculating profit for each gadget
    for (int i = 0; i < N; i++)
        profit[i] = sp[i] - cp[i];

    // sort the profit array
    // in descending order
    Arrays.sort(profit, Collections.reverseOrder());

    // variable to calculate total profit
    int sum = 0;

    // check for best M profits
    for (int i = 0; i < M; i++)
    {
        if (profit[i] > 0)
            sum += profit[i];
        else
            break;
    }

    return sum;
}

// Driver Code
public static void main(String args[])
{
    int N = 5, M = 3;
    int CP[] = { 5, 10, 35, 7, 23 };
    int SP[] = { 11, 10, 0, 9, 19 };

    System.out.println(solve(N, M, CP, SP));
}
}

// This code is contributed
// by Subhadeep Gupta
```

## 蟒蛇 3

```
# Python3 implementation
# of above approach

# Function to find profit
def solve(N, M, cp, sp) :

    # take empty list
    profit = []

    # Calculating profit
    # for each gadget
    for i in range(N) :
        profit.append(sp[i] - cp[i])

    # sort the profit array
    # in descending order
    profit.sort(reverse = True)

    sum = 0

    # check for best M profits
    for i in range(M) :
        if profit[i] > 0 :
            sum += profit[i]
        else :
            break

    return sum

# Driver Code
if __name__ == "__main__" :

    N, M = 5, 3
    CP = [5, 10, 35, 7, 23]
    SP = [11, 10, 0, 9, 19]

    # function calling
    print(solve(N, M, CP, SP))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# implementation of above approach:
using System;

class GFG
{

// Function to find profit
static int solve(int N, int M,
                 int[] cp, int[] sp)
{
    int[] profit = new int[N];

    // Calculating profit for each gadget
    for (int i = 0; i < N; i++)
        profit[i] = sp[i] - cp[i];

    // sort the profit array
    // in descending order
    Array.Sort(profit);
    Array.Reverse(profit);

    // variable to calculate total profit
    int sum = 0;

    // check for best M profits
    for (int i = 0; i < M; i++)
    {
        if (profit[i] > 0)
            sum += profit[i];
        else
            break;
    }

    return sum;
}

// Driver Code
public static void Main()
{
    int N = 5, M = 3;
    int[] CP = { 5, 10, 35, 7, 23 };
    int[] SP = { 11, 10, 0, 9, 19 };

    Console.Write(solve(N, M, CP, SP));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach:

// Function to find profit
function solve($N, $M, &$cp, &$sp)
{
    $profit = array_fill(0, $N, NULL);

    // Calculating profit for each gadget
    for ($i = 0; $i < $N; $i++)
        $profit[$i] = $sp[$i] - $cp[$i];

    // sort the profit array
    // in descending order
    rsort($profit);

    // variable to calculate
    // total profit
    $sum = 0;

    // check for best M profits
    for ($i = 0; $i < $M; $i++)
    {
        if ($profit[$i] > 0)
            $sum += $profit[$i];
        else
            break;
    }

    return $sum;
}

// Driver Code
$N = 5;
$M = 3;
$CP = array( 5, 10, 35, 7, 23 );
$SP = array( 11, 10, 0, 9, 19 );

echo solve($N, $M, $CP, $SP);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach:

// Function to find profit
function solve(N, M, cp, sp)
{
    let profit = new Array(N);

    // Calculating profit for each gadget
    for(let i = 0; i < N; i++)
        profit[i] = sp[i] - cp[i];

    // Sort the profit array
    // in descending order
    profit.sort(function(a, b){return b - a;});

    // Variable to calculate total profit
    let sum = 0;

    // Check for best M profits
    for(let i = 0; i < M; i++)
    {
        if (profit[i] > 0)
            sum += profit[i];
        else
            break;
    }
    return sum;
}

// Driver Code
let N = 5, M = 3;
let CP = [ 5, 10, 35, 7, 23 ];
let SP = [ 11, 10, 0, 9, 19 ];

document.write(solve(N, M, CP, SP));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
8
```
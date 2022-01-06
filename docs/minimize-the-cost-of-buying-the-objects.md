# 尽量降低购买物品的成本

> 原文:[https://www . geesforgeks . org/最小化购买对象的成本/](https://www.geeksforgeeks.org/minimize-the-cost-of-buying-the-objects/)

给定代表一个人拥有的物品总数的**‘T’**。**‘P’**代表每件商品的价格，**‘M’**代表如果他购买**‘N’**商品，他将获得**免费**商品的数量。任务是找出这个人为了得到 T 物品而必须支付的总额。
**举例:**

> **输入:** T = 13，P = 10，N = 3，M = 1
> **输出:**金额= 100
> **说明:**
> 一个人拥有的果瓶总数= 13
> 可提供的优惠是买 3 送 1
> 所以，一个人必须购买 9 个果汁瓶才能免费得到 3 个果汁瓶。
> 现在，由于瓶子的总数是 13，所以这个人以 P 价格买了 1 瓶。
> 该人必须支付的总金额= (9 + 1) * 10 即 100
> **输入:** T = 12，P = 8，N = 2，M = 1
> **输出:**金额= 64

**进场:**

1.  首先，我们应该尽可能多地获得免费项目，这样可以降低成本。
2.  将物品总数除以 **N** 和 **M** 的总和，因为当我们至少购买 **N** 个物品时，我们会得到 **M** 个免费物品。
3.  然后通过从项目总数中减去免费项目来计算您必须支付的项目总数
4.  最后，价格可以通过将一个项目的成本乘以项目的总数来计算。

以下是上述方法的实现:

## C++

```
// C++ program of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that will calculate the price
int totalPay(int totalItems, int priceOfOneItem,
             int N, int M)
{
    int freeItems = 0, actual = 0;

    // Calculate the number of items
    // we can get for free
    freeItems = totalItems / (N + M);

    // Calculate the number of items
    // we will have to pay the price for
    actual = totalItems - freeItems;

    // Calculate the price
    int amount = actual * priceOfOneItem;

    return amount;
}

// Driver code
int main()
{
    int T = 12, P = 8;
    int N = 2, M = 1;

    // Calling function
    cout << "Amount = "
         << totalPay(T, P, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that will calculate the price
static int totalPay(int totalItems,
                    int priceOfOneItem,
                    int N, int M)
{
    int freeItems = 0, actual = 0;

    // Calculate the number of items
    // we can get for free
    freeItems = totalItems / (N + M);

    // Calculate the number of items
    // we will have to pay the price for
    actual = totalItems - freeItems;

    // Calculate the price
    int amount = actual * priceOfOneItem;

    return amount;
}

// Driver code
public static void main(String[] args)
{
    int T = 12, P = 8;
    int N = 2, M = 1;

    // Calling function
    System.out.print("Amount = " +
                      totalPay(T, P, N, M));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program of above approach

# Function that will calculate the price
def totalPay(totalItems, priceOfOneItem, N, M):
    freeItems = 0
    actual = 0

    # Calculate the number of items
    # we can get for free
    freeItems = totalItems // (N + M)

    # Calculate the number of items
    # we will have to pay the price for
    actual = totalItems - freeItems

    # Calculate the price
    amount = actual * priceOfOneItem

    return amount

# Driver code
T = 12
P = 8
N = 2
M = 1

# Calling function
print("Amount = ", totalPay(T, P, N, M))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function that will calculate the price
static int totalPay(int totalItems,
                    int priceOfOneItem,
                    int N, int M)
{
    int freeItems = 0, actual = 0;

    // Calculate the number of items
    // we can get for free
    freeItems = totalItems / (N + M);

    // Calculate the number of items
    // we will have to pay the price for
    actual = totalItems - freeItems;

    // Calculate the price
    int amount = actual * priceOfOneItem;

    return amount;
}

// Driver code
public static void Main(String[] args)
{
    int T = 12, P = 8;
    int N = 2, M = 1;

    // Calling function
    Console.Write("Amount = " +
                   totalPay(T, P, N, M));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program of above approach

// Function that will calculate the price
function totalPay(totalItems, priceOfOneItem,
             N, M)
{
    var freeItems = 0, actual = 0;

    // Calculate the number of items
    // we can get for free
    freeItems = totalItems / (N + M);

    // Calculate the number of items
    // we will have to pay the price for
    actual = totalItems - freeItems;

    // Calculate the price
    var amount = actual * priceOfOneItem;

    return amount;
}

// Driver code
var T = 12, P = 8;
var N = 2, M = 1;
// Calling function
document.write( "Amount = "
     + totalPay(T, P, N, M));

</script>
```

**Output:** 

```
Amount = 64
```
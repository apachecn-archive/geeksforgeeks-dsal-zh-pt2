# 给定类型硬币可以购买的最大物品数

> 原文:[https://www . geesforgeks . org/用给定类型的硬币可以购买的最大物品数/](https://www.geeksforgeeks.org/maximum-items-that-can-be-bought-with-the-given-type-of-coins/)

给定三个整数 **X** 、 **Y** 和 **Z** ，代表购买某些物品的硬币数量。项目成本如下:

<figure class="table">

| 项目类型 | 费用 |
| --- | --- |
| one | 3 枚硬币 |
| Two | 3 Y 硬币 |
| three | 3 Z 硬币 |
| four | 1 X 角+ 1 Y 角+ 1 Z 角 |

任务是找到给定数量的硬币可以购买的最大物品数量。

> **输入:** X = 4，Y = 5，Z = 6
> **输出:** 4
> 购买 1 件 1 类物品:X = 1，Y = 5，Z = 6
> 购买 1 件 2 类物品:X = 1，Y = 2，Z = 6
> 购买 2 件 3 类物品:X = 1，Y = 2，Z = 0
> 购买物品总数= 1 + 1 + 2 = 4
> **输入:** X = 6，Y

**进场:**可购买的**1 型**、【T12 型和**3 型**商品数量分别为 **X / 3** 、 **Y / 3** 和 **Z / 3** 。现在购买这些物品后硬币数量会减少，如 **X = X % 3** 、 **Y = Y % 3** 、 **Z = Z % 3** 。因为，购买第四种类型的物品需要每种类型的硬币。因此，类型 4 中可以购买的项目总数将是 **X** 、 **Y** 和 **Z** 中的最小值，结果将是从每种类型中购买的这些项目的总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

const int COST = 3;

// Function to find maximum fruits
// Can buy from given values of x, y, z.
int maxItems(int x, int y, int z)
{

    // Items of type 1 that can be bought
    int type1 = x / COST;

    // Update the coins
    x %= COST;

    // Items of type 2 that can be bought
    int type2 = y / COST;

    // Update the coins
    y %= COST;

    // Items of type 3 that can be bought
    int type3 = z / COST;

    // Update the coins
    z %= COST;

    // Items of type 4 that can be bought
    // To buy a type 4 item, a coin
    // of each type is required
    int type4 = min(x, min(y, z));

    // Total items that can be bought
    int maxItems = type1 + type2 + type3 + type4;
    return maxItems;
}

// Driver code
int main()
{
    int x = 4, y = 5, z = 6;

    cout << maxItems(x, y, z);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{
static int COST = 3;

// Function to find maximum fruits
// Can buy from given values of x, y, z.
static int maxItems(int x, int y, int z)
{

    // Items of type 1 that can be bought
    int type1 = x / COST;

    // Update the coins
    x %= COST;

    // Items of type 2 that can be bought
    int type2 = y / COST;

    // Update the coins
    y %= COST;

    // Items of type 3 that can be bought
    int type3 = z / COST;

    // Update the coins
    z %= COST;

    // Items of type 4 that can be bought
    // To buy a type 4 item, a coin
    // of each type is required
    int type4 = Math.min(x, Math.min(y, z));

    // Total items that can be bought
    int maxItems = type1 + type2 + type3 + type4;
    return maxItems;
}

// Driver code
public static void main (String[] args)
{
    int x = 4, y = 5, z = 6;
    System.out.println(maxItems(x, y, z));
}
}

// This code is contributed by @tushil
```

## 蟒蛇 3

```
# Python3 implementation of the approach
COST = 3;

# Function to find maximum fruits
# Can buy from given values of x, y, z.
def maxItems(x, y, z) :

    # Items of type 1 that can be bought
    type1 = x // COST;

    # Update the coins
    x %= COST;

    # Items of type 2 that can be bought
    type2 = y // COST;

    # Update the coins
    y %= COST;

    # Items of type 3 that can be bought
    type3 = z // COST;

    # Update the coins
    z %= COST;

    # Items of type 4 that can be bought
    # To buy a type 4 item, a coin
    # of each type is required
    type4 = min(x, min(y, z));

    # Total items that can be bought
    maxItems = type1 + type2 + type3 + type4;
    return maxItems;

# Driver code
if __name__ == "__main__" :

    x = 4; y = 5; z = 6;

    print(maxItems(x, y, z));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int COST = 3;

// Function to find maximum fruits
// Can buy from given values of x, y, z.
static int maxItems(int x, int y, int z)
{

    // Items of type 1 that can be bought
    int type1 = x / COST;

    // Update the coins
    x %= COST;

    // Items of type 2 that can be bought
    int type2 = y / COST;

    // Update the coins
    y %= COST;

    // Items of type 3 that can be bought
    int type3 = z / COST;

    // Update the coins
    z %= COST;

    // Items of type 4 that can be bought
    // To buy a type 4 item, a coin
    // of each type is required
    int type4 = Math.Min(x, Math.Min(y, z));

    // Total items that can be bought
    int maxItems = type1 + type2 + type3 + type4;
    return maxItems;
}

// Driver code
static public void Main ()
{
    int x = 4, y = 5, z = 6;

    Console.Write (maxItems(x, y, z));
}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const COST = 3;

// Function to find maximum fruits
// Can buy from given values of x, y, z.
function maxItems(x, y, z)
{

    // Items of type 1 that can be bought
    let type1 = parseInt(x / COST);

    // Update the coins
    x %= COST;

    // Items of type 2 that can be bought
    let type2 = parseInt(y / COST);

    // Update the coins
    y %= COST;

    // Items of type 3 that can be bought
    let type3 = parseInt(z / COST);

    // Update the coins
    z %= COST;

    // Items of type 4 that can be bought
    // To buy a type 4 item, a coin
    // of each type is required
    let type4 = Math.min(x, Math.min(y, z));

    // Total items that can be bought
    let maxItems = type1 + type2 + type3 + type4;
    return maxItems;
}

// Driver code
    let x = 4, y = 5, z = 6;

    document.write(maxItems(x, y, z));

</script>
```

**Output:** 

```
4
```

</figure>
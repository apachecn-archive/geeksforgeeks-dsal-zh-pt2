# 从给定的售价和盈亏百分比中找出成本价

> 原文:[https://www . geesforgeks . org/find-成本价-从给定的销售价格-利润或亏损百分比/](https://www.geeksforgeeks.org/find-cost-price-from-given-selling-price-and-profit-or-loss-percentage/)

给定产品的销售价格和损益百分比。任务是计算产品的成本价。
**例:**

```
Input:  SP = 1020, Profit Percentage = 20
Output: CP = 850

Input: SP = 900, Loss Percentage = 10
Output:  CP = 1000
```

**进场:**

*   给出售价和利润百分比的成本价计算公式:

> CP = ( SP * 100 ) / ( 100 +利润百分比)。

*   给出售价和亏损百分比时成本价的计算公式:

> CP =(SP * 100)/(100–损失百分比)。

下面是需要的实现:

## C++

```
// C++ implementation to find Cost price
#include <iostream>
using namespace std;

// Function to calculate cost price with profit
float CPwithProfit(int sellingPrice, int profit)
{
    float costPrice;

    // required formula to calculate CP with profit
    costPrice = (sellingPrice * 100.0) / (100 + profit);
    return costPrice;
}

// Function to calculate cost price with loss
float CPwithLoss(int sellingPrice, int loss)
{
    float costPrice;

    // required formula to calculate CP with loss
    costPrice = (sellingPrice * 100.0) / (100 - loss);
    return costPrice;
}

// Driver code
int main()
{
    int SP, profit, loss;

    SP = 1020;
    profit = 20;
    cout << "Cost Price = " << CPwithProfit(SP, profit) << endl;

    SP = 900;
    loss = 10;
    cout << "Cost Price = " << CPwithLoss(SP, loss) << endl;

    SP = 42039;
    profit = 8;
    cout << "Cost Price = " << CPwithProfit(SP, profit) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find Cost price
import java.util.*;

class solution
{

// Function to calculate cost price with profit
static float CPwithProfit(int sellingPrice, int profit)
{
    float costPrice;

    // required formula to calculate CP with profit
    costPrice = (sellingPrice * 100) / (100 + profit);
    return costPrice;
}

// Function to calculate cost price with loss
static float CPwithLoss(int sellingPrice, int loss)
{
    float costPrice;

    // required formula to calculate CP with loss
    costPrice = (sellingPrice * 100) / (100 - loss);
    return costPrice;
}

// Driver code
public static void main(String args[])
{
    int SP, profit, loss;

    SP = 1020;
    profit = 20;
    System.out.println("Cost Price = "+CPwithProfit(SP, profit));

    SP = 900;
    loss = 10;
    System.out.println("Cost Price = "+CPwithLoss(SP, loss));

    SP = 42039;
    profit = 8;
    System.out.println("Cost Price = "+CPwithProfit(SP, profit));

}
}
// This code is contribute by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python 3 implementation to find Cost price

# Function to calculate cost price with profit
def CPwithProfit(sellingPrice, profit):

    # required formula to calculate CP with profit
    costPrice = ((sellingPrice * 100.0) /
                        (100 + profit))
    return costPrice

# Function to calculate cost price with loss
def CPwithLoss(sellingPrice, loss):

    # required formula to calculate CP with loss
    costPrice = ((sellingPrice * 100.0) /
                          (100 - loss))
    return costPrice

# Driver code
if __name__ == '__main__':
    SP = 1020
    profit = 20
    print("Cost Price =", CPwithProfit(SP, profit))

    SP = 900
    loss = 10
    print("Cost Price =", CPwithLoss(SP, loss))

    SP = 42039
    profit = 8
    print("Cost Price =", int(CPwithProfit(SP,
                                     profit)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// Csharp implementation to find Cost price

using System;

class solution
{

// Function to calculate cost price with profit
static float CPwithProfit(int sellingPrice, int profit)
{
    float costPrice;

    // required formula to calculate CP with profit
    costPrice = (sellingPrice * 100) / (100 + profit);
    return costPrice;
}

// Function to calculate cost price with loss
static float CPwithLoss(int sellingPrice, int loss)
{
    float costPrice;

    // required formula to calculate CP with loss
    costPrice = (sellingPrice * 100) / (100 - loss);
    return costPrice;
}

// Driver code
public static void Main()
{
    int SP, profit, loss;

    SP = 1020;
    profit = 20;
    Console.WriteLine("Cost Price = "+CPwithProfit(SP, profit));

    SP = 900;
    loss = 10;
    Console.WriteLine("Cost Price = "+CPwithLoss(SP, loss));

    SP = 42039;
    profit = 8;
    Console.WriteLine("Cost Price = "+CPwithProfit(SP, profit));

}
// This code is contribute by Ryuga

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find Cost price

// Function to calculate cost price with profit
function CPwithProfit($sellingPrice, $profit)
{

    // required formula to calculate CP with profit
    $costPrice = ($sellingPrice * 100.0) / (100 + $profit);
    return $costPrice;
}

// Function to calculate cost price with loss
function CPwithLoss($sellingPrice, $loss)
{

    // required formula to calculate CP with loss
    $costPrice = ($sellingPrice * 100.0) / (100 - $loss);
    return $costPrice;
}

// Driver code

    $SP = 1020;
    $profit = 20;
    echo("Cost Price = ");
    echo(CPwithProfit($SP, $profit));
    echo("\n");

    $SP = 900;
    $loss = 10;
    echo("Cost Price = ");
    echo(CPwithLoss($SP, $loss));
    echo("\n");

    $SP = 42039;
    $profit = 8;
    echo("Cost Price = ");
    echo(CPwithProfit($SP, $profit));
    echo("\n");

//This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
// javascript implementation to find Cost price

// Function to calculate cost price with profit
 function CPwithProfit(sellingPrice,  profit)
{
    var costPrice;

    // required formula to calculate CP with profit
    costPrice = (sellingPrice * 100) / (100 + profit);  
    return costPrice;
}

// Function to calculate cost price with loss
function CPwithLoss( sellingPrice,  loss)
{
    var costPrice;

    // required formula to calculate CP with loss
    costPrice = (sellingPrice * 100) / (100 - loss);
    return costPrice;
}

// Driver code

    var SP, profit, loss;

    SP = 1020;
    profit = 20;
    document.write("Cost Price = " + CPwithProfit(SP, profit) + "<br>");

    SP = 900;
    loss = 10;
    document.write("Cost Price = " + CPwithLoss(SP, loss)  + "<br>");

    SP = 42039;
    profit = 8;
    document.write("Cost Price = " + CPwithProfit(SP, profit)  + "<br>");

// This code is contributed by bunnyram19.
 </script>
```

**Output:** 

```
Cost Price = 850
Cost Price = 1000
Cost Price = 38925
```
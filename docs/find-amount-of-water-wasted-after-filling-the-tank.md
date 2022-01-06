# 查找加满水箱后浪费的水量

> 原文:[https://www . geeksforgeeks . org/find-注满水箱后浪费的水量/](https://www.geeksforgeeks.org/find-amount-of-water-wasted-after-filling-the-tank/)

给定以升为单位的油箱容积 **V** 。有一个泵正在以每分钟**米**升的速度给油箱加油。水箱底部有一个漏洞，以每分钟 N 升的速度浪费水。假设 N 小于 m。任务是计算如果在装满水箱后发现泄漏，将浪费多少水。
**例:**

```
Input : V = 700, M = 10, N = 3
Output : 300

Input : V = 1000, M = 100, N = 50
Output : 1000
```

**方法:**假设灌装泵的速度为每分钟 M 升。所以，一分钟内充满的水量是 M 升。此外，一分钟浪费 N 升水。因此，一分钟后，水箱中的水量将为(M–N)。因此，用泄漏物填充储罐所需的总时间将为 V / (M-N)。
因此废水量将为(V / (M-N)) * N.
以下是上述方法的实施:

## C++

```
// C++ program to find the volume of water wasted

#include <iostream>
using namespace std;

// Function to calculate amount of wasted water
double wastedWater(double V, double M, double N)
{
    double wasted_amt, amt_per_min, time_to_fill;

    // filled amount of water in one minute
    amt_per_min = M - N;

    // total time taken to fill the tank
    // because of leakage
    time_to_fill = V / amt_per_min;

    // wasted amount of water
    wasted_amt = N * time_to_fill;

    return wasted_amt;
}

// Driver code
int main()
{
    double V, M, N;
    V = 700;
    M = 10;
    N = 3;
    cout << wastedWater(V, M, N) << endl;

    V = 1000;
    M = 100;
    N = 50;
    cout << wastedWater(V, M, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// volume of water wasted
class GFG
{

// Function to calculate amount of wasted water
static double wastedWater(double V, double M, double N)
{
    double wasted_amt, amt_per_min, time_to_fill;

    // filled amount of water in one minute
    amt_per_min = M - N;

    // total time taken to fill the tank
    // because of leakage
    time_to_fill = V / amt_per_min;

    // wasted amount of water
    wasted_amt = N * time_to_fill;

    return wasted_amt;
}

// Driver code
public static void main(String[] args)
{
    double V, M, N;
    V = 700;
    M = 10;
    N = 3;
    System.out.println(wastedWater(V, M, N)) ;

    V = 1000;
    M = 100;
    N = 50;
    System.out.println(wastedWater(V, M, N));
}
}

// This Code is Contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 program to find the volume
# of water wasted

# Function to calculate amount
# of wasted water
def wastedWater(V, M, N):

    # filled amount of water in one minute
    amt_per_min = M - N

    # total time taken to fill the tank
    # because of leakage
    time_to_fill = V / amt_per_min

    # wasted amount of water
    wasted_amt = N * time_to_fill

    return wasted_amt

# Driver code
V = 700
M = 10
N = 3
print(wastedWater(V, M, N))

V = 1000
M = 100
N = 50
print(wastedWater(V, M, N))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find the
// volume of water wasted
using System;

class GFG
{

    // Function to calculate amount of wasted water
    static double wastedWater(double V, double M, double N)
    {
        double wasted_amt, amt_per_min, time_to_fill;

        // filled amount of water in one minute
        amt_per_min = M - N;

        // total time taken to fill the tank
        // because of leakage
        time_to_fill = V / amt_per_min;

        // wasted amount of water
        wasted_amt = N * time_to_fill;

        return wasted_amt;
    }

    // Driver code
    public static void Main()
    {
        double V, M, N;
        V = 700;
        M = 10;
        N = 3;
        Console.WriteLine(wastedWater(V, M, N)) ;

        V = 1000;
        M = 100;
        N = 50;
        Console.WriteLine(wastedWater(V, M, N));
    }
}

// This Code is Contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to find the
// volume of water wasted

// Function to calculate amount of wasted water
function wastedWater($V, $M, $N)
{

    // filled amount of water in one minute
    $amt_per_min = $M - $N;

    // total time taken to fill the tank
    // because of leakage
    $time_to_fill = $V / $amt_per_min;

    // wasted amount of water
    $wasted_amt = $N * $time_to_fill;

    return $wasted_amt;
}

// Driver code

$V = 700;
$M = 10;
$N = 3;
echo wastedWater($V, $M, $N), "\n";

$V = 1000;
$M = 100;
$N = 50;
echo wastedWater($V, $M, $N);

// This Code is Contributed by ihritik

?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// volume of water wasted

// Function to calculate amount of wasted water
function wastedWater(V, M, N)
{
    let wasted_amt, amt_per_min, time_to_fill;

    // filled amount of water in one minute
    amt_per_min = M - N;

    // total time taken to fill the tank
    // because of leakage
    time_to_fill = V / amt_per_min;

    // wasted amount of water
    wasted_amt = N * time_to_fill;

    return wasted_amt;
}

// driver program

    let V, M, N;
    V = 700;
    M = 10;
    N = 3;
    document.write(wastedWater(V, M, N), "<br>") ;

    V = 1000;
    M = 100;
    N = 50;
    document.write(wastedWater(V, M, N));

</script>
```

**Output:** 

```
300
1000
```
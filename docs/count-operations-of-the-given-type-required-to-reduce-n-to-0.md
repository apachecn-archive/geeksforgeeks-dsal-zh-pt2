# 计算将 N 减少到 0 所需的给定类型的操作数

> 原文:[https://www . geesforgeks . org/count-operations-of-the-给定类型-required-reduce-n-0/](https://www.geeksforgeeks.org/count-operations-of-the-given-type-required-to-reduce-n-to-0/)

给定一个整数 **n** 。任务是计算将 **n** 减少到 **0** 所需的操作次数。在每次操作中， **n** 可以更新为**n = n–d**，其中 **d** 是 **n** 的[最小素除数](https://www.geeksforgeeks.org/smallest-prime-divisor-of-a-number/)。
**举例:**

> **输入:** n = 5
> **输出:** 1
> 5 是最小的素除数，因此它被减去，n 被减少到 0。
> **输入:** n = 25
> **输出:** 11
> 5 是最小的素除数，因此被减去，n 减少到 20。那么 2 就是最小除数，以此类推。
> **输入:** n = 4
> **输出:** 2

**进场:**

1.  当 **n** 为**偶数**时， **n** 的最小质因数将为 **2** ，从 **n** 中减去 **2** 将再次给出一个偶数，即增益 **2** 将被选为最小质因数，这些步骤将重复进行，直到 **n** 减少到 **0** 。
2.  当 **n** 为**奇数**时， **n** 的最小素除数也将为奇数，从另一个奇数中减去一个奇数将得到一个偶数，然后对当前的偶数重复步骤 1 即可得出结果。
3.  因此，任务是找到最小除数 **d** ，减去它，**n = n–d**并打印**1+((n–d)/2)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the required
// number of operations
int countOperations (int n)
{
    int i = 2;

    // Finding the smallest divisor
    while ((i * i) < n && (n % i))
        i += 1;

    if ((i * i) > n)
        i = n;

    // Return the count of operations
    return (1 + (n - i)/2);
}

// Driver code
int main()
{
    int n = 5;
    cout << countOperations(n);
}

//This code is contributed by Shivi_Aggarwal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required
// number of operations
static int countOperations (int n)
{
    int i = 2;

    // Finding the smallest divisor
    while ((i * i) < n && (n % i) > 0)
        i += 1;

    if ((i * i) > n)
        i = n;

    // Return the count of operations
    return (1 + (n - i) / 2);
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    System.out.println(countOperations(n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required
# number of operations
def countOperations(n):
    i = 2

    # Finding the smallest divisor
    while ((i * i) < n and (n % i)):
        i += 1

    if ((i * i) > n):
        i = n

    # Return the count of operations
    return (1 + (n - i)//2)

# Driver code
n = 5
print(countOperations(n))
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the required
// number of operations
static int countOperations (int n)
{
    int i = 2;

    // Finding the smallest divisor
    while ((i * i) < n && (n % i) > 0)
        i += 1;

    if ((i * i) > n)
        i = n;

    // Return the count of operations
    return (1 + (n - i) / 2);
}

// Driver code
static void Main()
{
    int n = 5;
    Console.WriteLine(countOperations(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required
// number of operations
function countOperations($n)
{
    $i = 2;

    # Finding the smallest divisor
    while (($i * $i) < $n and ($n % $i))
        $i += 1;

    if (($i * $i) > $n)
        $i = $n;

    # Return the count of operations
    return 1 + floor(($n - $i) / 2);
}

// Driver code
$n = 5 ;
echo countOperations($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the required
// number of operations
function countOperations (n)
{
    var i = 2;

    // Finding the smallest divisor
    while ((i * i) < n && (n % i))
        i += 1;

    if ((i * i) > n)
        i = n;

    // Return the count of operations
    return (1 + (n - i)/2);
}

// Driver code
var n = 5;
document.write( countOperations(n))

</script>
```

**Output:** 

```
1
```

**时间复杂度:** ![O(\sqrt{n})  ](img/2d4520d6f3e600ec5bf4609c88d5caa3.png "Rendered by QuickLaTeX.com")
# 用可被其和整除的乘积计算从 1 到 N 的数对

> 原文:[https://www . geesforgeks . org/count-对从 1 到 n 的数加上可被其和整除的乘积/](https://www.geeksforgeeks.org/count-pairs-of-numbers-from-1-to-n-with-product-divisible-by-their-sum/)

给定一个数字![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")。任务是对(x，y)进行计数，使得 x*y 可被(x+y)整除，并且条件 **1 < = x < y < N** 成立。
T4【示例】T5:

```
Input : N = 6
Output : 1
Explanation: The only pair is (3, 6) which satisfies
all of the given condition, 3<6 and 18%9=0.

Input : N = 15
Output : 4
```

基本方法是使用两个循环迭代，仔细维护给定的条件 **1 < = x < y < N** ，并生成所有可能的有效对，并对其值的乘积可被和整除的对进行计数。
以下是上述办法的实施情况:

## C++

```
// C++ program to count pairs of numbers
// from 1 to N with Product divisible
// by their Sum

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs
int countPairs(int n)
{
    // variable to store count
    int count = 0;

    // Generate all possible pairs such that
    // 1 <= x < y < n
    for (int x = 1; x < n; x++) {
        for (int y = x + 1; y <= n; y++) {
            if ((y * x) % (y + x) == 0)
                count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int n = 15;

    cout << countPairs(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs of numbers
// from 1 to N with Product divisible
// by their Sum

import java.io.*;

class GFG {

// Function to count pairs
static int countPairs(int n)
{
    // variable to store count
    int count = 0;

    // Generate all possible pairs such that
    // 1 <= x < y < n
    for (int x = 1; x < n; x++) {
        for (int y = x + 1; y <= n; y++) {
            if ((y * x) % (y + x) == 0)
                count++;
        }
    }

    return count;
}

// Driver code

    public static void main (String[] args) {
            int n = 15;

    System.out.println(countPairs(n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to count pairs of numbers
# from 1 to N with Product divisible
# by their Sum

# Function to count pairs
def countPairs(n):

    # variable to store count
    count = 0

    # Generate all possible pairs such that
    # 1 <= x < y < n
    for x in range(1, n):
        for y in range(x + 1, n + 1):
            if ((y * x) % (y + x) == 0):
                count += 1

    return count

# Driver code
n = 15
print(countPairs(n))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# program to count pairs of numbers
// from 1 to N with Product divisible
// by their Sum
using System;

class GFG
{

// Function to count pairs
static int countPairs(int n)
{
    // variable to store count
    int count = 0;

    // Generate all possible pairs
    // such that 1 <= x < y < n
    for (int x = 1; x < n; x++)
    {
        for (int y = x + 1; y <= n; y++)
        {
            if ((y * x) % (y + x) == 0)
                count++;
        }
    }

    return count;
}

// Driver code
public static void Main ()
{
    int n = 15;

    Console.WriteLine(countPairs(n));
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs of
// numbers from 1 to N with Product
// divisible by their Sum

// Function to count pairs
function countPairs($n)
{
    // variable to store count
    $count = 0;

    // Generate all possible pairs
    // such that 1 <= x < y < n
    for ($x = 1; $x < $n; $x++)
    {
        for ($y = $x + 1; $y <= $n; $y++)
        {
            if (($y * $x) % ($y + $x) == 0)
                $count++;
        }
    }

    return $count;
}

// Driver code
$n = 15;
echo countPairs($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to count pairs of numbers
// from 1 to N with Product divisible
// by their Sum

// Function to count pairs
function countPairs(n)
{
    // variable to store count
    let count = 0;

    // Generate all possible pairs such that
    // 1 <= x < y < n
    for (let x = 1; x < n; x++) {
        for (let y = x + 1; y <= n; y++) {
            if ((y * x) % (y + x) == 0)
                count++;
        }
    }

    return count;
}

// Driver code
let n = 15;

document.write(countPairs(n));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N <sup>2</sup> )
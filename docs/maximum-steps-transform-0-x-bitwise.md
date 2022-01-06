# 通过按位“与”将 0 转换为 X 的最大步数

> 原文:[https://www . geesforgeks . org/maximum-steps-transform-0-x-bitwise/](https://www.geeksforgeeks.org/maximum-steps-transform-0-x-bitwise/)

对于整数 N，有从 0 到 N-1 的元素。某些元素可以转化为其他元素。每个转换都需要一定的努力，对于每个转换，这相当于 1 个单位。一个元素 A 可以转化为元素 B，当且仅当 A！= B 和 A & B = A(其中&是按位“与”运算符)。我们需要尽最大努力通过一系列转换从值为 0 的元素中获得值为 X 的元素。
**例:**

> 输入:X = 2
> 输出:1
> 获取 2 的唯一方法是直接将 0 转换为 2(0 和 2 的按位“与”为 0)，因此需要一步。
> 输入:X = 3
> 输出:2
> 3 可以分两步得到。首先，将 0 转换为 1(0 和 1 的按位“与”是 0)。然后，将 1 转换为 3(1 和 3 的按位“与”是 1)。

简单的解决方法是计算 x 中的设置位数
**说明:**
首先考虑一个**单步**从 A 到 B 的变换，A 的所有设置位(等于 1 的位)都应该设置在 B 中，否则 A 和 B 的按位 AND 就不等于 A，如果有任何位设置在 A 中而不在 B 中，那么这个变换是不可能的。A 的未置位位可以在 B 中置位也可以不置位，这并不重要。然后，我们可以通过一步设置 A 中所有未设置的位来将 A 更改为 B。因此，如果我们必须用最少的步骤将 0 转换为 X，答案应该是 1，因为 0 与任何数字的按位“与”是 0。
但是我们要计算最大步数。因此，在每一步中，我们从右边开始设置每个位，设置位一旦设置就不能被清除。
**例:**
假设我们想从 0 得到 13(二进制中的 1101)。我们首先通过将 0 转换为 1(二进制为 0001)来设置右边的第一位。接下来，我们将右边的第三位设置为形式 5(二进制为 0101)。最后一步是设置第 4 位并获得 13 (1101)。

## C++

```
// CPP code to find the maximum possible
// effort
#include <bits/stdc++.h>
using namespace std;

// Function to get no of set bits in binary
// representation of positive integer n
unsigned int countSetBits(unsigned int n)
{
    unsigned int count = 0;
    while (n) {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Driver code
int main()
{
    int i = 3;
    cout << countSetBits(i);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the maximum
// possible effort

class GFG {

// Function to get no. of
// set bits in binary
// representation of
// positive integer n
static int countSetBits(int n)
{
    int count = 0;
    while (n != 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int i = 3;
    System.out.print(countSetBits(i));
}
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python3 code to find the
# maximum possible effort

# Function to get no of
# set bits in binary
# representation of positive
# integer n
def countSetBits(n) :
    count = 0
    while (n) :
        count += n & 1
        n >>= 1
    return count

# Driver code
i = 3
print (countSetBits(i))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# code to find the maximum
// possible effort
using System;

class GFG {

// Function to get no. of
// set bits in binary
// representation of
// positive integer n
static int countSetBits(int n)
{
    int count = 0;
    while (n != 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int i = 3;
    Console.Write(countSetBits(i));
}
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the
// maximum possible effort

// Function to get no of
// set bits in binary
// representation of positive
// integer n
function countSetBits($n)
{
    $count = 0;
    while ($n)
    {
        $count += $n & 1;
        $n >>= 1;
    }
    return $count;
}

// Driver code
$i = 3;
echo (countSetBits($i));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript code to find the maximum possible
// effort

// Function to get no of set bits in binary
// representation of positive integer n
function countSetBits(n)
{
    var count = 0;
    while (n) {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Driver code
var i = 3;
document.write( countSetBits(i));

</script>
```

**输出:**

```
2
```

***时间复杂度:** O(log <sub>10</sub> N)*

***辅助空间:**O(1)*T4】
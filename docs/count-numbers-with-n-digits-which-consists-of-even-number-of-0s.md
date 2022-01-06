# 用 0 的偶数组成的 N 位数计数

> 原文:[https://www . geesforgeks . org/count-numbers-with-n-digits-其中-由-0 的偶数组成/](https://www.geeksforgeeks.org/count-numbers-with-n-digits-which-consists-of-even-number-of-0s/)

给定一个数字 **N** 。任务是找出有 N 个数字和偶数个零的数字的计数。
**注意:**数字可以有前面的 0。
**示例** :

```
Input: N = 2
Output: Count = 81 
Total 2 digit numbers are 99 considering 1 as 01.
2 digit numbers are 01, 02, 03, 04, 05.... 99
Numbers with odd 0's are 01, 02, 03, 04, 05, 06, 07, 08, 09
10, 20, 30, 40, 50, 70, 80, 90 i.e. 18
The rest of the numbers between 01 and 99 will 
do not have any zeroes and zero is also an even number.
So, numbers with even 0's are 99 - 18 = 81.

Input: N = 3
Output: Count = 755
```

**方法:**思路是找到由奇数个 0 组成的[计数 N 位数](https://www.geeksforgeeks.org/count-numbers-with-n-digits-which-consists-of-odd-number-of-0s/)再从 N 位数总数中减去得到偶数个 0 的数字

## C++

```
// C++ program to count numbers with N digits
// which consists of odd number of 0's
#include <bits/stdc++.h>
using namespace std;

// Function to count Numbers with N digits
// which consists of odd number of 0's
int countNumbers(int N)
{
    return (pow(10, N) - 1) - (pow(10, N) - pow(8, N)) / 2;
}

// Driver code
int main()
{
    int n = 2;

    cout << countNumbers(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers
// with N digits which consists
// of odd number of 0's
import java.lang.*;
import java.util.*;

class GFG
{

// Function to count Numbers with
// N digits which consists of odd
// number of 0's
static double countNumbers(int N)
{
    return (Math.pow(10, N) - 1) -
           (Math.pow(10, N) -
            Math.pow(8, N)) / 2;
}

// Driver code
static public void main (String args[])
{
    int n = 2;
    System.out.println(countNumbers(n));
}
}

// This code si contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3  program to count numbers with N digits
#  which consists of odd number of 0's

# Function to count Numbers with N digits
#  which consists of odd number of 0's
def countNumber(n):

    return (pow(10,n)-1)- (pow(10,n)-pow(8,n))//2

# Driver code
n = 2
print(countNumber(n))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to count numbers
// with N digits which consists
// of odd number of 0's
using System;

class GFG
{

// Function to count Numbers with
// N digits which consists of odd
// number of 0's
static double countNumbers(int N)
{
    return (Math.Pow(10, N) - 1) -
           (Math.Pow(10, N) -
            Math.Pow(8, N)) / 2;
}

// Driver code
static public void Main ()
{
    int n = 2;
    Console.WriteLine(countNumbers(n));
}
}

// This code si contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count numbers with N digits
// which consists of odd number of 0's

// Function to count Numbers with N digits
// which consists of odd number of 0's
function countNumbers($N)
{
    return (pow(10, $N) - 1) -
           (pow(10, $N) - pow(8, $N)) / 2;
}

// Driver code
$n = 2;
echo countNumbers($n),"\n";

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to count numbers with N digits
// which consists of odd number of 0's

// Function to count Numbers with N digits
// which consists of odd number of 0's
function countNumbers(N)
{
    return (Math.pow(10, N) - 1) - (Math.pow(10, N) - Math.pow(8, N)) / 2;
}

// Driver code
var n = 2;
document.write( countNumbers(n));

</script>
```

**Output:** 

```
81
```

**注**:答案可以很大，所以对于大于 9 的 N，使用[模幂运算。](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)
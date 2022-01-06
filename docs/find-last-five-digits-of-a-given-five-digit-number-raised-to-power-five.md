# 求给定的五位数的最后五位数字的五次方

> 原文:[https://www . geesforgeks . org/find-给定五位数的最后五位数-升五次方/](https://www.geeksforgeeks.org/find-last-five-digits-of-a-given-five-digit-number-raised-to-power-five/)

给定一个五位数 n，任务是通过将数字排列为:
来查找给定数字修改后升到 5 的幂的最后五位数字

```
first digit, third digit, fifth digit, fourth digit, second digit.
```

**例:**

```
Input : N = 12345
Output : 71232
Explanation : 
After modification the number becomes 13542\. (13542)5 is 
455422043125550171232

Input : N = 10000
Output : 00000
```

**接近**:在这个问题中，只需要实现语句中描述的动作。然而，这个问题有两个陷阱。
第一个问题是五位数的五次幂不能用 64 位整数表示。但是我们实际上不需要第五次幂，我们需要第五次幂模 10 <sup>5</sup> 。每次乘法后都可以进行模运算。
第二抓就是你需要输出五位数，而不是五次方模 10 <sup>5</sup> 。不同之处在于从末尾算起的第五个数字是零。要输出，前导零一的数字可以使用相应的格式(% printf 中的 05d)或提取数字并逐个输出。
以下是上述方法的实施:

## C++

```
// CPP program to find last five digits
// of a five digit number raised to power five

#include <bits/stdc++.h>
using namespace std;

// Function to find the last five digits
// of a five digit number raised to power five
int lastFiveDigits(int n)
{
    n = (n / 10000) * 10000
        + ((n / 100) % 10)
              * 1000
        + (n % 10)
              * 100
        + ((n / 10) % 10)
              * 10
        + (n / 1000) % 10;

    int ans = 1;
    for (int i = 0; i < 5; i++) {
        ans *= n;
        ans %= 100000;
    }

    printf("%05d", ans);
}

// Driver code
int main()
{
    int n = 12345;

    lastFiveDigits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find last five digits
// of a five digit number raised to power five

class GfG {

    // Function to find the last five digits
    // of a five digit number raised to power five
    static void lastFiveDigits(int n)
    {
        n = (n / 10000) * 10000
            + ((n / 100) % 10)
                  * 1000
            + (n % 10)
                  * 100
            + ((n / 10) % 10)
                  * 10
            + (n / 1000) % 10;

        int ans = 1;
        for (int i = 0; i < 5; i++) {
            ans *= n;
            ans %= 100000;
        }

        System.out.println(ans);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 12345;

        lastFiveDigits(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find last five digits
# of a five digit number raised to power five

# Function to find the last five digits
# of a five digit number raised to power five
def lastFiveDigits(n):
    n = ((int)(n / 10000) * 10000 +
        ((int)(n / 100) % 10) * 1000 + (n % 10) * 100 +
        ((int)(n / 10) % 10) * 10 + (int)(n / 1000) % 10)
    ans = 1
    for i in range(5):
        ans *= n
        ans %= 100000
    print(ans)

# Driver code
if __name__ == '__main__':
    n = 12345

    lastFiveDigits(n)

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to find last five
// digits of a five digit number
// raised to power five
using System;

class GFG
{

    // Function to find the last
    // five digits of a five digit
    // number raised to power five
    public static void lastFiveDigits(int n)
    {
        n = (n / 10000) * 10000 +
           ((n / 100) % 10) * 1000 +
            (n % 10) * 100 +
           ((n / 10) % 10) * 10 +
            (n / 1000) % 10;

        int ans = 1;
        for (int i = 0; i < 5; i++)
        {
            ans *= n;
            ans %= 100000;
        }

        Console.WriteLine(ans);
    }

    // Driver code
    public static void Main(string[] args)
    {
        int n = 12345;

        lastFiveDigits(n);
    }
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find last five digits
// of a five digit number raised to power five

// Function to find the last five digits
// of a five digit number raised to power five
function lastFiveDigits($n)
{
    $n = (int)($n / 10000) * 10000 +
        ((int)($n / 100) % 10) * 1000 +
              ($n % 10) * 100 +
        ((int)($n / 10) % 10) * 10 +
         (int)($n / 1000) % 10;

    $ans = 1;
    for ($i = 0; $i < 5; $i++)
    {
        $ans *= $n;
        $ans %= 100000;
    }

    echo $ans;
}

// Driver code
$n = 12345;

lastFiveDigits($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// JavaScript program to find last five digits
// of a five digit number raised to power five

// Function to find the last five digits
// of a five digit number raised to power five
function lastFiveDigits(n)
{
    n = (Math.floor(n / 10000)) * 10000
        + (Math.floor(n / 100) % 10)
            * 1000
        + (n % 10)
            * 100
        + (Math.floor(n / 10) % 10)
            * 10
        + Math.floor(n / 1000) % 10;

    let ans = 1;
    for (let i = 0; i < 5; i++) {
        ans *= n;
        ans %= 100000;
    }

    document.write(ans);
}

// Driver code

    let n = 12345;

    lastFiveDigits(n);

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
71232
```
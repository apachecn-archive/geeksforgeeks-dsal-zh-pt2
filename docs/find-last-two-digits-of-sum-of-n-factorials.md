# 求 N 阶乘之和的最后两位数

> 原文:[https://www . geeksforgeeks . org/find-n 因子和的最后两位数/](https://www.geeksforgeeks.org/find-last-two-digits-of-sum-of-n-factorials/)

给定一个数字 N，任务是找到前 N 个自然数阶乘的单位和十位数字，即 1 的最后两位数字！+2!+3!+….n！其中 N <=10e18.
**例:**

```
Input : n = 2 
Output :3
1! + 2! = 3
Last two digit  is 3

Input :4
Output :33
1!+2!+3!+4!=33
Last two digit is 33
```

**天真法:**在这种方法中，只需计算每个数的阶乘，并求出这些数的和。最后得到单位和十位数的和。这将花费大量时间和不必要的计算。
**有效方法:**在这种方法中，在[1，10]范围内只计算 N 的单位和十位数，因为:
1！= 1
2！= 2
3！= 6
4！= 24
5！= 120
6！= 720
7！= 5040
8！=40320
9！=362880
10！=3628800
以此类推。
As 10！= 3628800，大于 10 的阶乘有两个尾随零。所以，N > =10 做求和时不做单位和十位的贡献。
因此，

> if (n < 10) 
> ans = (1！+ 2 !+..+ n！) % 100;
> else
> ans = (1！+ 2 !+ 3 !+ 4 !+ 5 !+ 6 !+ 7 !+ 8 !+ 9 !+ 10 !) % 100;
> 注:我们知道(1！+ 2!+ 3!+ 4!+…+10!)% 100 = 13
> 所以当 n 大于 4 时我们总是返回 3。

下面是上述方法的实现。

## C++

```
// C++ program to find the unit place digit
// of the first N natural numbers factorials
#include <iostream>
using namespace std;
#define ll long int
// Function to find the unit's and ten's place digit
int get_last_two_digit(long long int N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 10.
    if (N <= 10) {
        ll ans = 0, fac = 1;
        for (int i = 1; i <= N; i++) {
            fac = fac * i;
            ans += fac;
        }
        return ans % 100;
    }

    // We know following
    // (1! + 2! + 3! + 4!...+10!) % 100 = 13
    else // (N >= 10)
        return 13;
}

// Driver code
int main()
{
    long long int N = 1;
    for (N = 1; N <= 10; N++)
        cout << "For N = " << N
             << " : " << get_last_two_digit(N)
             << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find the unit place digit
//of the first N natural numbers factorials
public class AAA {

    //Function to find the unit's and ten's place digit
    static int get_last_two_digit(long N)
    {

     // Let us write for cases when
     // N is smaller than or equal
     // to 10.
     if (N <= 10) {
         long ans = 0, fac = 1;
         for (int i = 1; i <= N; i++) {
             fac = fac * i;
             ans += fac;
         }
         return (int)ans % 100;
     }

     // We know following
     // (1! + 2! + 3! + 4!...+10!) % 100 = 13
     else // (N >= 10)
         return 13;
    }

    //Driver code
    public static void main(String[] args) {

        long N = 1;
         for (N = 1; N <= 10; N++)
             System.out.println( "For N = " + N
                  + " : " + get_last_two_digit(N));
    }

}
```

## 蟒蛇 3

```
# Python3 program to find the unit
# place digit of the first N natural
# numbers factorials

# Function to find the unit's
# and ten's place digit
def get_last_two_digit(N):

    # Let us write for cases when
    # N is smaller than or equal
    # to 10
    if N <= 10:
        ans = 0
        fac = 1
        for i in range(1, N + 1):
            fac = fac * i
            ans += fac
        ans = ans % 100
        return ans

    # We know following
    # (1! + 2! + 3! + 4!...+10!) % 100 = 13
    # // (N >= 10)
    else:
        return 13

# Driver Code
N = 1
for N in range(1, 11):
    print("For N = ", N, ": ",
           get_last_two_digit(N), sep = ' ')

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to find the unit
// place digit of the first N
// natural numbers factorials
using System;

class GFG
{

// Function to find the unit's
// and ten's place digit
static int get_last_two_digit(long N)
{

// Let us write for cases when
// N is smaller than or equal
// to 10.
if (N <= 10)
{
    long ans = 0, fac = 1;
    for (int i = 1; i <= N; i++)
    {
        fac = fac * i;
        ans += fac;
    }
    return (int)ans % 100;
}

// We know following
// (1! + 2! + 3! + 4!...+10!) % 100 = 13
else // (N >= 10)
    return 13;
}

// Driver code
public static void Main()
{
    long N = 1;
    for (N = 1; N <= 10; N++)
        Console.WriteLine( "For N = " + N +
            " : " + get_last_two_digit(N));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the unit place digit
// of the first N natural numbers factorials

// Function to find the unit's
// and ten's place digit
function get_last_two_digit($N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 10.
    if ($N <= 10)
    {
        $ans = 0; $fac = 1;
        for ($i = 1; $i <= $N; $i++)
        {
            $fac = $fac * $i;
            $ans += $fac;
        }
        return $ans % 100;
    }

    // We know following
    // (1! + 2! + 3! + 4!...+10!) % 100 = 13
    else // (N >= 10)
        return 13;
}

// Driver code
$N = 1;
for ($N = 1; $N <= 10; $N++)
    echo "For N = " . $N . " : " .
          get_last_two_digit($N) . "\n";

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// Javascript program to find the unit place digit
// of the first N natural numbers factorials

// Function to find the unit's and ten's place digit
function get_last_two_digit(N)
{

    // Let us write for cases when
    // N is smaller than or equal
    // to 10.
    if (N <= 10) {
        let ans = 0, fac = 1;
        for (let i = 1; i <= N; i++) {
            fac = fac * i;
            ans += fac;
        }
        return ans % 100;
    }

    // We know following
    // (1! + 2! + 3! + 4!...+10!) % 100 = 13
    else // (N >= 10)
        return 13;
}

// Driver code

    let N = 1;
    for (N = 1; N <= 10; N++)
        document.write("For N = " + N
            + " : " + get_last_two_digit(N)
            + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
For N = 1 : 1
For N = 2 : 3
For N = 3 : 9
For N = 4 : 33
For N = 5 : 53
For N = 6 : 73
For N = 7 : 13
For N = 8 : 33
For N = 9 : 13
For N = 10 : 13
```
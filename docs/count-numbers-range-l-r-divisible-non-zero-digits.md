# 计算 L-R 范围内可被其所有非零数字整除的数字

> 原文:[https://www . geesforgeks . org/count-numbers-range-l-r-除尽-非零数字/](https://www.geeksforgeeks.org/count-numbers-range-l-r-divisible-non-zero-digits/)

给定范围 l–r(包括 l–r)，计算可被其所有非零数字整除的数字。
**例:**

```
Input : 1 9 
Output : 9
Explanation: 
all the numbers are divisible by 
their digits in the range 1-9.

Input : 10 20 
Output : 5
Explanation: 
10, 11, 12, 15, 20 
```

**进场:**
1。运行一个循环，从 l 和 r 中生成每个数字
2。检查该数字的每个非零数字是否除以该数字。
3。记录所有能被其数字完全整除的数字。
4。打印数字计数。
以下是上述方法的实现:

## C++

```
// C++ program to
// Count numbers in
// range L-R that are
// divisible by
// all of its non-zero
// digits
#include <bits/stdc++.h>
using namespace std;

// check if the number is
// divisible by the digits.
bool check(int n)
{
    int m = n;
    while (n) {
        int r = n % 10;
        if (r > 0)
            if ((m % r) != 0)
                return false;       
        n /= 10;
    }

    return true;
}

// function to calculate the
// number of numbers
int count(int l, int r)
{
    int ans = 0;
    for (int i = l; i <= r; i++)
        if (check(i))
            ans += 1;   
    return ans;
}

// Driver function
int main()
{
    int l = 10, r = 20;
    cout << count(l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count
// numbers in range L-R
// that are divisible by
// all of its non-zero
// digits
import java.io.*;

class GFG {

    // check if the number
    // is divisible by the
    // digits.
    static boolean check(int n)
    {
        int m = n;

        while (n != 0)
        {
            int r = n % 10;

            if (r > 0)
                if ((m % r) != 0)
                    return false;    

            n /= 10;
        }

        return true;
    }

    // function to calculate
    // the number of numbers
    static int count(int l, int r)
    {
        int ans = 0;

        for (int i = l; i <= r; i++)
            if (check(i))
                ans += 1;
        return ans;
    }

    // Driver function
    public static void main(String args[])
    {
        int l = 10, r = 20;

        System.out.println(count(10, 20));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program
# to Count numbers in
# range L-R that are
# divisible by all of
# its non-zero digits

# check if the number is
# divisible by the digits.
def check(n) :
    m = n
    while (n != 0) :
        r = n % 10
        if (r > 0) :
            if ((m % r) != 0) :
                return False   
        n = n // 10

    return True

# function to calculate the
# number of numbers
def count(l, r) :
    ans = 0
    for i in range(l, r+1) :
        if (check(i)) :
            ans = ans + 1
    return ans

# Driver function
l = 10
r = 20
print(count(l, r))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Java program to Count
// numbers in range L-R
// that are divisible by
// all of its non-zero
// digits
using System;

class GFG {

    // check if the number
    // is divisible by the
    // digits.
    static bool check(int n)
    {
        int m = n;

        while (n != 0)
        {
            int r = n % 10;

            if (r > 0)
                if ((m % r) != 0)
                    return false;

            n /= 10;
        }

        return true;
    }

    // function to calculate
    // the number of numbers
    static int count(int l, int r)
    {
        int ans = 0;

        for (int i = l; i <= r; i++)
            if (check(i))
                ans += 1;
        return ans;
    }

    // Driver function
    public static void Main()
    {
        int l = 10, r = 20;

        Console.WriteLine(count(l, r));
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Count numbers
// in range L-R that are
// divisible by all of its
// non-zero digits

// check if the number is
// divisible by the digits.
function check($n)
{
    $m = $n;
    while ($n) {
        $r = $n % 10;
        if ($r > 0)
            if (($m % $r) != 0)
                return false;    
        $n /= 10;
    }

    return true;
}

// function to calculate the
// number of numbers
function countIn($l, $r)
{
    $ans = 0;
    for ($i = $l; $i <= $r; $i++)
        if (check($i))
            $ans += 1;

    return $ans;

}

// Driver function
$l = 10; $r = 20;
echo countIn($l, $r);

// This code is contributed ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to Count numbers
// in range L-R that are
// divisible by all of its
// non-zero digits

// check if the number is
// divisible by the digits.
function check(n)
{
     let m = n;
    while (n) {
        let r = n % 10;
        if (r > 0)
            if ((n % r) != 0)
                return false;   
        n /= 10;
    }

    return true;
}

// function to calculate the
// number of numbers
function countIn(l, r)
{
    let ans = 0;
    for (let i = l; i <= r; i++)
        if (check(i))
            ans += 1;

    return ans;

}

// Driver function
let l = 10;
let r = 20;
document.write(countIn(l, r));

// This code is contributed by sravan kumar

</script>
```

**输出:**

```
5
```
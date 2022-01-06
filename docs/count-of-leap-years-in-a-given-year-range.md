# 给定年份范围内闰年的计数

> 原文:[https://www . geesforgeks . org/给定年份范围内的闰年数/](https://www.geeksforgeeks.org/count-of-leap-years-in-a-given-year-range/)

给定两年 **L** 和 **R** ，任务是找到范围(L，R)内可能的闰年总数。
**例:**

> **输入:** L = 1，R = 400
> **输出:** 97
> **输入:** L = 400，R = 2000
> **输出:** 389

**天真法:**思路是用[这种](https://www.geeksforgeeks.org/program-check-given-year-leap-year/)法迭代 L 到 R，检查年份是不是闰年。
**时间复杂度:** O(N)
**高效方法:**

1.  如果满足以下条件，一年就是闰年:
    *   年份是 400 的倍数。
    *   年份是 4 的倍数，不是 100 的倍数。
2.  所以通过
    计算在(1，L)和(1，R)范围内满足上述条件的数

> 闰年数(1，年)=(年/4)–(年/ 100) +(年/ 400)

2.  范围(1，R)中的闰年数与范围(1，L)中的闰年数之差将是所需的输出。

下面是上述方法的实现。

## C++

```
// C++ implementation to find the 
// count of leap years in given
// range of the year 

#include <bits/stdc++.h>

using namespace std;

// Function to calculate the number
// of leap years in range of (1, year)
int calNum(int year)
{
    return (year / 4) - (year / 100) +
                        (year / 400);
}

// Function to calculate the number
// of leap years in given range
void leapNum(int l, int r)
{
    l--;
    int num1 = calNum(r);
    int num2 = calNum(l);
    cout << num1 - num2 << endl;
}

// Driver Code
int main()
{
    int l1 = 1, r1 = 400;
    leapNum(l1, r1);

    int l2 = 400, r2 = 2000;
    leapNum(l2, r2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the 
// count of leap years in given
// range of the year 
class GFG
{

// Function to calculate the number
// of leap years in range of (1, year)
static int calNum(int year)
{
    return (year / 4) - (year / 100) +
                        (year / 400);
}

// Function to calculate the number
// of leap years in given range
static void leapNum(int l, int r)
{
    l--;
    int num1 = calNum(r);
    int num2 = calNum(l);
    System.out.print(num1 - num2 +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int l1 = 1, r1 = 400;
    leapNum(l1, r1);

    int l2 = 400, r2 = 2000;
    leapNum(l2, r2);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find the 
# count of leap years in given 
# range of the year 

# Function to calculate the number 
# of leap years in range of (1, year) 
def calNum(year) : 

    return (year // 4) - (year // 100) + (year // 400) 

# Function to calculate the number 
# of leap years in given range 
def leapNum(l, r) :

    l -= 1 
    num1 = calNum(r)
    num2 = calNum(l)
    print(num1 - num2)

# Driver Code 
if __name__ == "__main__" : 

    l1 = 1
    r1 = 400 
    leapNum(l1, r1)

    l2 = 400
    r2 = 2000 
    leapNum(l2, r2)

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the 
// count of leap years in given
// range of the year 
using System;

class GFG
{

// Function to calculate the number
// of leap years in range of (1, year)
static int calNum(int year)
{
    return (year / 4) - (year / 100) +
                        (year / 400);
}

// Function to calculate the number
// of leap years in given range
static void leapNum(int l, int r)
{
    l--;
    int num1 = calNum(r);
    int num2 = calNum(l);
    Console.Write(num1 - num2 +"\n");
}

// Driver Code
public static void Main(String[] args)
{
    int l1 = 1, r1 = 400;
    leapNum(l1, r1);

    int l2 = 400, r2 = 2000;
    leapNum(l2, r2);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation to find the 
    // count of leap years in given
    // range of the year 

    // Function to calculate the number
    // of leap years in range of (1, year)
    function calNum(year)
    {
        return parseInt(year / 4, 10) - parseInt(year / 100, 10) + parseInt(year / 400, 10);
    }

    // Function to calculate the number
    // of leap years in given range
    function leapNum(l, r)
    {
        l--;
        let num1 = calNum(r);
        let num2 = calNum(l);
        document.write((num1 - num2) +"</br>");
    }

    let l1 = 1, r1 = 400;
    leapNum(l1, r1);

    let l2 = 400, r2 = 2000;
    leapNum(l2, r2);

// This code is contributed by divyeh072019.
</script>
```

**Output:** 

```
97
389
```

**时间复杂度:** O(1)
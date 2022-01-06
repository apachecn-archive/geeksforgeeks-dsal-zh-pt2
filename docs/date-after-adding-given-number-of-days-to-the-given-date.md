# 给定日期加上给定天数后的日期

> 原文:[https://www . geesforgeks . org/给定日期添加给定天数后的日期/](https://www.geeksforgeeks.org/date-after-adding-given-number-of-days-to-the-given-date/)

给定日期和正整数 **x** 。任务是在给定日期上增加 x 天后查找日期

示例:

```
Input : d1 = 14, m1 = 5, y1 = 2017
        Days to be added x = 10
Output : d2 = 24, m2 = 5, y2 = 2017

Input : d1 = 14, m1 = 3, y1 = 2015
        Days to be added x = 466
Output : d2 = 14, m2 = 3, y2 = 2016

```

1)让给定日期为 d1、m1 和 y1。求给定年份的偏移量(从开始到给定日期所花费的天数)(参考下面的 offset days())
2)让上述步骤中找到的偏移量为 offset1。查找结果年份 y2 和结果年份偏移量 2(参考下面突出显示的代码)
3)从偏移量 2 和 y2 中查找天数和月份。(请参考下面的 revoffsetDays()。

下面是以上步骤的实现。

## C++

```
// C++ program to find date after adding
// given number of days.
#include<bits/stdc++.h>
using namespace std;

// Return if year is leap year or not.
bool isLeap(int y)
{
    if (y%100 != 0 && y%4 == 0 || y %400 == 0)
        return true;

    return false;
}

// Given a date, returns number of days elapsed
// from the  beginning of the current year (1st
// jan).
int offsetDays(int d, int m, int y)
{
    int offset = d;

    switch (m - 1)
    {
    case 11:
        offset += 30;
    case 10:
        offset += 31;
    case 9:
        offset += 30;
    case 8:
        offset += 31;
    case 7:
        offset += 31;
    case 6:
        offset += 30;
    case 5:
        offset += 31;
    case 4:
        offset += 30;
    case 3:
        offset += 31;
    case 2:
        offset += 28;
    case 1:
        offset += 31;
    }

    if (isLeap(y) && m > 2)
        offset += 1;

    return offset;
}

// Given a year and days elapsed in it, finds
// date by storing results in d and m.
void revoffsetDays(int offset, int y, int *d, int *m)
{
    int month[13] = { 0, 31, 28, 31, 30, 31, 30,
                      31, 31, 30, 31, 30, 31 };

    if (isLeap(y))
        month[2] = 29;

    int i;
    for (i = 1; i <= 12; i++)
    {
        if (offset <= month[i])
            break;
        offset = offset - month[i];
    }

    *d = offset;
    *m = i;
}

// Add x days to the given date.
void addDays(int d1, int m1, int y1, int x)
{
    int offset1 = offsetDays(d1, m1, y1);
    int remDays = isLeap(y1)?(366-offset1):(365-offset1);

    // y2 is going to store result year and
    // offset2 is going to store offset days
    // in result year.
    int y2, offset2;
    if (x <= remDays)
    {
        y2 = y1;
        offset2 = offset1 + x;
    }

    else
    {
        // x may store thousands of days.
        // We find correct year and offset
        // in the year.
        x -= remDays;
        y2 = y1 + 1;
        int y2days = isLeap(y2)?366:365;
        while (x >= y2days)
        {
            x -= y2days;
            y2++;
            y2days = isLeap(y2)?366:365;
        }
        offset2 = x;
    }

    // Find values of day and month from
    // offset of result year.
    int m2, d2;
    revoffsetDays(offset2, y2, &d2, &m2);

    cout << "d2 = " << d2 << ", m2 = " << m2
         << ", y2 = " << y2;
}

// Driven Program
int main()
{
    int d = 14, m = 3, y = 2015;
    int x = 366;

    addDays(d, m, y, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find date after adding
// given number of days.

class GFG
{

// Find values of day and month from
// offset of result year.
static int m2, d2;

// Return if year is leap year or not.
static boolean isLeap(int y)
{
    if (y % 100 != 0 && y % 4 == 0 || y % 400 == 0)
        return true;

    return false;
}

// Given a date, returns number of days elapsed
// from the beginning of the current year (1st
// jan).
static int offsetDays(int d, int m, int y)
{
    int offset = d;

    if(m - 1 == 11)
        offset += 335;
    if(m - 1 == 10)
        offset += 304;
    if(m - 1 == 9)
        offset += 273;
    if(m - 1 == 8)
        offset += 243;
    if(m - 1 == 7)
        offset += 212;
    if(m - 1 == 6)
        offset += 181;
    if(m - 1 == 5)
        offset += 151;
    if(m - 1 == 4)
        offset += 120;
    if(m - 1 == 3)
        offset += 90;
    if(m - 1 == 2)
        offset += 59;
    if(m - 1 == 1)
        offset += 31;

    if (isLeap(y) && m > 2)
        offset += 1;

    return offset;
}

// Given a year and days elapsed in it, finds
// date by storing results in d and m.
static void revoffsetDays(int offset, int y)
{
    int []month={ 0, 31, 28, 31, 30, 31, 30,
                    31, 31, 30, 31, 30, 31 };

    if (isLeap(y))
        month[2] = 29;

    int i;
    for (i = 1; i <= 12; i++)
    {
        if (offset <= month[i])
            break;
        offset = offset - month[i];
    }

    d2 = offset;
    m2 = i;
}

// Add x days to the given date.
static void addDays(int d1, int m1, int y1, int x)
{
    int offset1 = offsetDays(d1, m1, y1);
    int remDays = isLeap(y1) ? (366 - offset1) : (365 - offset1);

    // y2 is going to store result year and
    // offset2 is going to store offset days
    // in result year.
    int y2, offset2 = 0;
    if (x <= remDays)
    {
        y2 = y1;
        offset2 =offset1 + x;
    }

    else
    {
        // x may store thousands of days.
        // We find correct year and offset
        // in the year.
        x -= remDays;
        y2 = y1 + 1;
        int y2days = isLeap(y2) ? 366 : 365;
        while (x >= y2days)
        {
            x -= y2days;
            y2++;
            y2days = isLeap(y2) ? 366 : 365;
        }
        offset2 = x;
    }
    revoffsetDays(offset2, y2);
    System.out.println("d2 = " + d2 + ", m2 = " +
                            m2 + ", y2 = " + y2);
}

// Driven Program
public static void main(String[] args)
{
    int d = 14, m = 3, y = 2015;
    int x = 366;
    addDays(d, m, y, x);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find date after adding
# given number of days.

# Return if year is leap year or not.
def isLeap(y):

    if (y % 100 != 0 and y % 4 == 0 or y % 400 == 0):
        return True
    return False

# Given a date, returns number of days elapsed
# from the beginning of the current year (1st
# jan).
def offsetDays(d, m, y):

    offset = d
    switcher = {
        10: 30,
        9: 31,
        8: 30,
        7: 31,
        6: 31,
        5: 30,
        4: 31,
        3: 30,
        2: 31,
        1: 28,
        0: 31
    }
    if (isLeap(y) and m > 1):
        offset += 1
    offset +=switcher.get(m)
    return offset

# Given a year and days elapsed in it, finds
# date by storing results in d and m.
def revoffsetDays(offset, y,d, m):
    month = [ 0, 31, 28, 31, 30, 31, 30,31, 31, 30, 31, 30, 31 ]

    if (isLeap(y)):
        month[2] = 29
    for i in range(1, 13):
        if (offset <= month[i]):
            break
        offset = offset - month[i]

    d[0] = offset
    m[0] = i + 1

# Add x days to the given date.
def addDays(d1, m1, y1, x):

    offset1 = offsetDays(d1, m1, y1)
    if isLeap(y1):
        remDays = 366 - offset1
    else:
        remDays = 365 - offset1

    # y2 is going to store result year and
    # offset2 is going to store offset days
    # in result year.
    if (x <= remDays):
        y2 = y1
        offset2 = offset1 + x
    else:

        # x may store thousands of days.
        # We find correct year and offset
        # in the year.
        x -= remDays
        y2 = y1 + 1
        if isLeap(y2):
            y2days = 366
        else:
            y2days = 365

        while (x >= y2days):
            x -= y2days
            y2 += 1
            if isLeap(y2):
                y2days = 366
            else:
                y2days = 365

        offset2 = x

    # Find values of day and month from
    # offset of result year.
    m2 = [0]
    d2 = [0]
    revoffsetDays(offset2, y2, d2, m2)
    print("d2 = ",*d2,", m2 = ",*m2,", y2 = ",y2,sep="")

# Driven Program
d = 14
m = 3
y = 2015
x = 366

addDays(d, m, y, x)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to find date after adding
// given number of days.
using System;
class GFG{

    // Find values of day and month from
    // offset of result year.
    static int m2, d2;

// Return if year is leap year or not.
static bool isLeap(int y)
{
    if (y % 100 != 0 && y % 4 == 0 || y % 400 == 0)
        return true;

    return false;
}

// Given a date, returns number of days elapsed
// from the beginning of the current year (1st
// jan).
static int offsetDays(int d, int m, int y)
{
    int offset = d;

    if(m - 1 == 11)
        offset += 335;
    if(m - 1 == 10)
        offset += 304;
    if(m - 1 == 9)
        offset += 273;
    if(m - 1 == 8)
        offset += 243;
    if(m - 1 == 7)
        offset += 212;
    if(m - 1 == 6)
        offset += 181;
    if(m - 1 == 5)
        offset += 151;
    if(m - 1 == 4)
        offset += 120;
    if(m - 1 == 3)
        offset += 90;
    if(m - 1 == 2)
        offset += 59;
    if(m - 1 == 1)
        offset += 31;

    if (isLeap(y) && m > 2)
        offset += 1;

    return offset;
}

// Given a year and days elapsed in it, finds
// date by storing results in d and m.
static void revoffsetDays(int offset, int y)
{
    int []month = { 0, 31, 28, 31, 30, 31, 30,
                    31, 31, 30, 31, 30, 31 };

    if (isLeap(y))
        month[2] = 29;
    int i;
    for (i = 1; i <= 12; i++)
    {
        if (offset <= month[i])
            break;
        offset = offset - month[i];
    }

    d2 = offset;
    m2 = i;
}

// Add x days to the given date.
static void addDays(int d1, int m1, int y1, int x)
{
    int offset1 = offsetDays(d1, m1, y1);
    int remDays = isLeap(y1) ? (366 - offset1) : (365 - offset1);

    // y2 is going to store result year and
    // offset2 is going to store offset days
    // in result year.
    int y2, offset2 = 0;
    if (x <= remDays)
    {
        y2 = y1;
        offset2 = offset1+x;
    }

    else
    {
        // x may store thousands of days.
        // We find correct year and offset
        // in the year.
        x -= remDays;
        y2 = y1 + 1;
        int y2days = isLeap(y2) ? 366 : 365;
        while (x >= y2days)
        {
            x -= y2days;
            y2++;
            y2days = isLeap(y2)?366:365;
        }
        offset2 = x;
    }
    revoffsetDays(offset2, y2);
    Console.WriteLine("d2 = " + d2 + ", m2 = " +
                        m2 + ", y2 = " + y2);
}

// Driven Program
static void Main()
{
    int d = 14, m = 3, y = 2015;
    int x = 366;
    addDays(d, m, y, x);
}
}
// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript program to find date after
// adding given number of days.   

// Find values of day and month from
// offset of result year.
var m2, d2;

// Return if year is leap year or not.
function isLeap(y)
{
    if (y % 100 != 0 &&
        y % 4 == 0 ||
        y % 400 == 0)
        return true;

    return false;
}

// Given a date, returns number of
// days elapsed from the beginning
// of the current year (1st jan).
function offsetDays(d , m , y)
{
    var offset = d;

    if (m - 1 == 11)
        offset += 335;
    if (m - 1 == 10)
        offset += 304;
    if (m - 1 == 9)
        offset += 273;
    if (m - 1 == 8)
        offset += 243;
    if (m - 1 == 7)
        offset += 212;
    if (m - 1 == 6)
        offset += 181;
    if (m - 1 == 5)
        offset += 151;
    if (m - 1 == 4)
        offset += 120;
    if (m - 1 == 3)
        offset += 90;
    if (m - 1 == 2)
        offset += 59;
    if (m - 1 == 1)
        offset += 31;

    if (isLeap(y) && m > 2)
        offset += 1;

    return offset;
}

// Given a year and days elapsed in it, finds
// date by storing results in d and m.
function revoffsetDays(offset, y)
{
    var month = [ 0, 31, 28, 31, 30, 31, 30,
                  31, 31, 30, 31, 30, 31 ];

    if (isLeap(y))
        month[2] = 29;

    var i;
    for(i = 1; i <= 12; i++)
    {
        if (offset <= month[i])
            break;

        offset = offset - month[i];
    }
    d2 = offset;
    m2 = i;
}

// Add x days to the given date.
function addDays(d1 , m1 , y1 , x)
{
    var offset1 = offsetDays(d1, m1, y1);
    var remDays = isLeap(y1) ? (366 - offset1) :
                               (365 - offset1);

    // y2 is going to store result year and
    // offset2 is going to store offset days
    // in result year.
    var y2, offset2 = 0;
    if (x <= remDays)
    {
        y2 = y1;
        offset2 =offset1 + x;
    }
    else
    {

        // x may store thousands of days.
        // We find correct year and offset
        // in the year.
        x -= remDays;
        y2 = y1 + 1;
        var y2days = isLeap(y2) ? 366 : 365;

        while (x >= y2days)
        {
            x -= y2days;
            y2++;
            y2days = isLeap(y2) ? 366 : 365;
        }
        offset2 = x;
    }

    revoffsetDays(offset2, y2);
    document.write("d2 = " + d2 +
                   ", m2 = " + m2 +
                   ", y2 = " + y2);
}

// Driver code
var d = 14, m = 3, y = 2015;
var x = 366;

addDays(d, m, y, x);

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
d2 = 14, m2 = 3, y2 = 2016
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
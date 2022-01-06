# 查找给定日期的星期几

> 原文:[https://www . geesforgeks . org/查找给定日期的星期几/](https://www.geeksforgeeks.org/find-day-of-the-week-for-a-given-date/)

编写一个函数，计算过去或未来任何特定日期的星期几。一个典型的应用是计算一周中某人出生或其他特殊事件发生的日期。

下面是[坂本、拉克曼、基思、克雷文](http://en.wikipedia.org/wiki/Determination_of_the_day_of_the_week#Implementation-dependent_methods_of_Sakamoto.2C_Lachman.2C_Keith_and_Craver)建议的一个简单的计算日的函数。以下函数返回 0 表示星期日，1 表示星期一，等等。

```
Understanding the Maths:

14/09/1998
dd=14
mm=09
yyyy=1998 //non-leap year

Step 1: Informations to be remembered.
 Magic Number Month array.
 For Year: {0,3,3,6,1,4,6,2,5,0,3,5}
 DAY array starting from 0-6: {Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday}
 Century Year Value: 1600-1699 = 6
      1700-1799 = 4
      1800-1899 = 2
      1900-1999 = 0
      2000-2099 = 6..

Step 2: Calculations as per the steps

 Last 2 digits of the year:  98
 Divide the above by 4:     24
 Take the date(dd):      14
 Take month value from array: 5 (for September month number 9)
 Take century year value:  0  ( 1998 is in the range 1900-1999 thus 0)
          -----
 Sum:        141

 Divide the Sum by 7 and get the remainder: 141 % 7 = 1

 Check the Day array starting from index 0: Day[1] = Monday

**If leap year it will be the remainder-1
```

## C++

```
/* A program to find day of a given date */
#include <bits/stdc++.h>
using namespace std;

int dayofweek(int d, int m, int y)
{
    static int t[] = { 0, 3, 2, 5, 0, 3,
                       5, 1, 4, 6, 2, 4 };
    y -= m < 3;
    return ( y + y / 4 - y / 100 +
             y / 400 + t[m - 1] + d) % 7;
}

// Driver Code
int main()
{
    int day = dayofweek(30, 8, 2010);
    cout << day;

    return 0;
}

// This is code is contributed
// by rathbhupendra
```

## C

```
/* A program to find day of a given date */
#include<stdio.h>

int dayofweek(int d, int m, int y)
{
    static int t[] = { 0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4 };
    y -= m < 3;
    return ( y + y/4 - y/100 + y/400 + t[m-1] + d) % 7;
}

/* Driver function to test above function */
int main()
{
    int day = dayofweek(30, 8, 2010);
    printf ("%d", day);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*This code will return the string value and the exact date
 * both for leap and non leap years*/
import java.util.*;
class FindDay {
    static int dd;
    static int mm;
    static int yyyy;
    FindDay(int dd, int mm, int yyyy)
    {
        this.dd = dd;
        this.mm = mm;
        this.yyyy = yyyy;
    }
    static int checkLeap(int y)
    {
        if ((y % 4 == 0 && y % 100 != 0) || (y % 400 == 0))
            return 1;
        else
            return 0;
    }
    static void calculate()
    {

        // Checking Leap year. If true then 1 else 0.
        int flag_for_leap = checkLeap(yyyy);

        /*Declaring and initialising the given informations
         * and arrays*/
        String day[] = { "Sunday",    "Monday",   "Tuesday",
                         "Wednesday", "Thursday", "Friday",
                         "Saturday" };
        int m_no[] = { 0, 3, 3, 6, 1, 4, 6, 2, 5, 0, 3, 5 };

        /*Generalised check to find any Year Value*/
        int j;
        if ((yyyy / 100) % 2 == 0) {
            if ((yyyy / 100) % 4 == 0)
                j = 6;
            else
                j = 2;
        }
        else {
            if (((yyyy / 100) - 1) % 4 == 0)
                j = 4;
            else
                j = 0;
        }

        /*THE FINAL FORMULA*/
        int total = (yyyy % 100) + ((yyyy % 100) / 4) + dd
                    + m_no[mm - 1] + j;
        if (flag_for_leap == 1) {
            if ((total % 7) > 0)
                System.out.println(day[(total % 7) - 1]);
            else
                System.out.println(day[6]);
        }
        else
            System.out.println(day[(total % 7)]);
    }
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        /*Take input in string format and then convert to
         * integer values*/
        String date = sc.next();
        String[] values = date.split("/");
        new FindDay(Integer.parseInt(values[0]),
                    Integer.parseInt(values[1]),
                    Integer.parseInt(values[2]));
        calculate();
    }
}
/*Contributed and written by Aniket Dey*/
```

## 蟒蛇 3

```
# Python3 program to find day
# of a given date

def dayofweek(d, m, y):
    t = [ 0, 3, 2, 5, 0, 3,
          5, 1, 4, 6, 2, 4 ]
    y -= m < 3
    return (( y + int(y / 4) - int(y / 100)
             + int(y / 400) + t[m - 1] + d) % 7)

# Driver Code
day = dayofweek(30, 8, 2010)
print(day)

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program to find day of a given date
using System;

class GFG {

    static int dayofweek(int d, int m, int y)
    {
        int []t = { 0, 3, 2, 5, 0, 3, 5,
                            1, 4, 6, 2, 4 };
        y -= (m < 3) ? 1 : 0;

        return ( y + y/4 - y/100 + y/400
                         + t[m-1] + d) % 7;
    }

    // Driver Program to test above function
    public static void Main()
    {
        int day = dayofweek(30, 8, 2010);

        Console.Write(day);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// day of a given date
function dayofweek($d, $m, $y)
{
    static $t = array(0, 3, 2, 5, 0, 3,
                      5, 1, 4, 6, 2, 4);
    $y -= $m < 3;
    return ($y + $y / 4 - $y / 100 +
            $y / 400 + $t[$m - 1] + $d) % 7;
}

// Driver Code
$day = dayofweek(30, 8, 2010);
echo $day;

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// Javascript program to find day of a given date

function dayofweek(d, m, y)
{
    let t = [ 0, 3, 2, 5, 0, 3, 5, 1, 4, 6, 2, 4 ];
    y -= (m < 3) ? 1 : 0;
    return ( y + y/4 - y/100 + y/400 + t[m-1] + d) % 7;
}

// Driver Code

    let day = dayofweek(30, 8, 2010);
    document.write(Math.round(day));

</script>
```

**输出:** 1(周一)

***时间复杂度:** O(1)*
以上功能解释见[本](http://stackoverflow.com/questions/6385190/correctness-of-sakamotos-algorithm-to-find-the-day-of-week/6385934#6385934)。
参考文献:
[http://en . Wikipedia . org/wiki/decision _ of _ day _ of _ the _ week](http://en.wikipedia.org/wiki/Determination_of_the_day_of_the_week)
本文由 **Dheeraj Jain** 编辑，GeeksforGeeks 团队审核。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息
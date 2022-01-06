# 以 0 为数字和最大“d”位的正整数计数

> 原文:[https://www . geesforgeks . org/count-正整数-0 位数/](https://www.geeksforgeeks.org/count-positive-integers-0-digit/)

给定一个数字 d，代表一个数字的位数。找出正整数的总数，其中至少有一个零，由 d 个或更少的数字组成。

```
Examples:
Input : d = 1
Output : 0
There's no natural number of 1 digit that contains a zero.

Input : d = 2
Output : 9

Input : d = 3
Output : 180
For d = 3, we've to count numbers from 1 to 999, that have 
atleast one zero in them.
Similarly for d=4, we'd check every number from 1 to 9999\. 
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/count-zero3710/1)

这主要是下文的延伸。
[计算以 0 为数字的 d 位正整数。](https://www.geeksforgeeks.org/count-d-digit-positive-integers-with-0-as-a-digit/)
如果我们仔细观察，这个问题和我们在第一集里讨论过的问题非常相似。对于给定的 d，如果我们找到由数字 1、2、3 组成的 0 的数字，我们就可以得到所需的答案…..最后我们可以将它们相加得到输出。
下面是同样的程序。

## C++

```
// C++ program to find the count of positive integer of a
// given number of digits that contain atleast one zero
#include<bits/stdc++.h>
using namespace std;

// Returns count of 'd' digit integers have 0 as a digit
int findCount(int d)
{
    return 9*(pow(10,d-1) - pow(9,d-1));
}

// utility function to count the required answer
int findCountUpto(int d)
{
    // Count of numbers with digits smaller than
    // or equal to d.
    int totalCount = 0;
    for (int i=1; i<=d; i++)
        totalCount += findCount(i);

    return totalCount;
}

// Driver Code
int main()
{
    int d = 1;
    cout << findCountUpto(d) << endl;

    d = 2;
    cout << findCountUpto(d) << endl;

    d = 4;
    cout << findCountUpto(d) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// positive integer of agiven number
// of digits that contain atleast one zero
import java.io.*;
import java.math.*;

class GFG {

    // Returns count of 'd' digit
    // integers have 0 as a digit
    static int findCount(int d)
    {
        return 9 * (int)((Math.pow(10, d - 1)
                         - Math.pow(9, d - 1)));
    }

    // utility function to count
    // the required answer
    static int findCountUpto(int d)
    {
        // Count of numbers with digits
        // smaller than or equal to d.
        int totalCount = 0;
        for (int i = 1; i <= d; i++)
            totalCount += findCount(i);

        return totalCount;
    }

    // Driver Code
    public static void main(String args[])
    {
        int d = 1;
        System.out.println(findCountUpto(d));

        d = 2;
        System.out.println( findCountUpto(d) );

        d = 4;
        System.out.println(findCountUpto(d));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to find the
# count of natural numbers upto a
# given number of digits that
# contain atleast one zero
import math

# Utility function to calculate
# the count of natural numbers
# upto a given number of digits
# that contain atleast one zero
def findCountUpto(d) :
    # Sum of two GP series
    GP1_Sum = 9*((int)((math.pow(10,d))-1)//9)
    GP2_Sum = 9*((int)((math.pow(9,d))-1)//8)

    return GP1_Sum - GP2_Sum

# Driver Code
d = 1
print(findCountUpto(d))

d = 2
print(findCountUpto(d))

d = 4
print(findCountUpto(d))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find the count of
// positive integer of agiven number
// of digits that contain atleast
// one zero
using System;

class GFG {

    // Returns count of 'd' digit
    // integers have 0 as a digit
    static int findCount(int d)
    {
        return 9 * (int)((Math.Pow(10, d - 1)
                        - Math.Pow(9, d - 1)));
    }

    // utility function to count
    // the required answer
    static int findCountUpto(int d)
    {
        // Count of numbers with digits
        // smaller than or equal to d.
        int totalCount = 0;
        for (int i = 1; i <= d; i++)
            totalCount += findCount(i);

        return totalCount;
    }

    // Driver Code
    public static void Main()
    {
        int d = 1;
        Console.WriteLine(findCountUpto(d));

        d = 2;
        Console.WriteLine( findCountUpto(d) );

        d = 4;
        Console.WriteLine(findCountUpto(d));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the count
// of positive integer of a given
// number of digits that contain
// atleast one zero

// Returns count of 'd' digit
// integers have 0 as a digit
function findCount($d)
{
    return 9 * (pow(10, $d - 1) -
                 pow(9, $d - 1));
}

// function to count
// the required answer
function findCountUpto($d)
{

    // Count of numbers with
    // digits smaller than
    // or equal to d.
    $totalCount = 0;
    for ($i = 1; $i <= $d; $i++)
        $totalCount += findCount($i);

    return $totalCount;
}

// Driver Code
{
    $d = 1;
    echo findCountUpto($d),"\n" ;

    $d = 2;
    echo findCountUpto($d),"\n" ;

    $d = 4;
    echo findCountUpto($d) ;
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the count of
// positive integer of agiven number
// of digits that contain atleast one zero

    // Returns count of 'd' digit
    // integers have 0 as a digit
    function findCount(d)
    {
        return 9 * ((Math.pow(10, d - 1)
                         - Math.pow(9, d - 1)));
    }

    // utility function to count
    // the required answer
    function findCountUpto(d)
    {
        // Count of numbers with digits
        // smaller than or equal to d.
        let totalCount = 0;
        for (let i = 1; i <= d; i++)
            totalCount += findCount(i);

        return totalCount;
    }

// Driver Code

        let d = 1;
        document.write(findCountUpto(d) + "<br/>");

        d = 2;
        document.write( findCountUpto(d) + "<br/>" );

        d = 4;
        document.write(findCountUpto(d) + "<br/>");   

    // This code is contributed by target_2.
</script>
```

输出:

```
0
9
2619 
```

时间复杂度:O(d)
辅助空间:O(1)
**我们能让解更高效吗？**
是的，如果我们仔细看，所需答案是使用以下两个几何级数之和获得的:

```
i'th term of G.P. 1 = 9*10i - 1  where 1 <= i <= d
i'th term of G.P. 2 = 9*9i - 1 where 1 <= i <= d
The final answer is nothing but,

Sum of G.P 1 = 9*(10d - 1)/(10-1) 
= 9*(10d - 1)/9
Similarly,
Sum of G.P 2 = 9*(9d - 1)/(9-1) 
= 9*(9d - 1)/8
Using the above facts, we can optimize the solution to run in O(1) 
```

下面是一个有效的程序。

## C++

```
// C++ program to find the count of natural numbers upto a
// given number of digits that contain atleast one zero
#include<bits/stdc++.h>
using namespace std;

// Utility function to calculate the count of natural numbers
// upto a given number of digits that contain atleast one zero
int findCountUpto(int d)
{
    // Sum of two GP series
    int GP1_Sum = 9*((pow(10,d)-1)/9);
    int GP2_Sum = 9*((pow(9,d)-1)/8);

    return GP1_Sum - GP2_Sum;
}

// Driver Code
int main()
{
    int d = 1;
    cout << findCountUpto(d) << endl;

    d = 2;
    cout << findCountUpto(d) << endl;

    d = 4;
    cout << findCountUpto(d) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// of natural numbers upto a
// given number of digits
// that contain atleast one zero
import java.io.*;
import java.math.*;

class GFG {

    // Utility function to calculate
    // the count of natural numbers
    // upto a given number of digits
    // that contain atleast one zero
    static int findCountUpto(int d)
    {
        // Sum of two GP series
        int GP1_Sum = 9 * ((int)((Math.pow(10, d)) - 1) / 9);
        int GP2_Sum = 9 * ((int)((Math.pow(9, d)) - 1) / 8);

        return GP1_Sum - GP2_Sum;
    }

    // Driver Code
    public static void main(String args[])
    {
        int d = 1;
        System.out.println(findCountUpto(d));

        d = 2;
        System.out.println(findCountUpto(d));

        d = 4;
        System.out.println(findCountUpto(d));

    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to find the
# count of positive integer of a
# given number of digits that
# contain atleast one zero
import math

# Returns count of 'd' digit
# integers have 0 as a digit
def findCount(d) :
    return 9*(pow(10,d-1) - pow(9,d-1));

# utility function to count
# the required answer
def findCountUpto(d) :

    # Count of numbers with
    # digits smaller than
    # or equal to d.
    totalCount = 0
    for i in range(1,d+1) :
        totalCount = totalCount + findCount(i)

    return totalCount

# Driver Code
d = 1
print(findCountUpto(d))

d = 2
print(findCountUpto(d))

d = 4
print(findCountUpto(d))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find the count
// of natural numbers upto a
// given number of digits
// that contain atleast one zero
using System;

class GFG {

    // Utility function to calculate
    // the count of natural numbers
    // upto a given number of digits
    // that contain atleast one zero
    static int findCountUpto(int d)
    {

        // Sum of two GP series
        int GP1_Sum = 9 * ((int)((Math.Pow(10,
                                d)) - 1) / 9);
        int GP2_Sum = 9 * ((int)((Math.Pow(9,
                                d)) - 1) / 8);

        return GP1_Sum - GP2_Sum;
    }

    // Driver Code
    public static void Main()
    {
        int d = 1;
        Console.WriteLine(findCountUpto(d));

        d = 2;
        Console.WriteLine(findCountUpto(d));

        d = 4;
        Console.WriteLine(findCountUpto(d));

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the count
// of natural numbers upto a
// given number of digits that
// contain atleast one zero

// function to calculate the
// count of natural numbers
// upto a given number of digits
// that contain atleast one zero
function findCountUpto($d)
{

    // Sum of two GP series
    $GP1_Sum = 9 * ((pow(10, $d) - 1) / 9);
    $GP2_Sum = 9 * ((pow(9, $d) - 1) / 8);

    return $GP1_Sum - $GP2_Sum;
}

    // Driver Code
    $d = 1;
    echo findCountUpto($d),"\n";

    $d = 2;
    echo findCountUpto($d),"\n";

    $d = 4;
    echo findCountUpto($d) ,"\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
// Javascript program to find the count
// of natural numbers upto a
// given number of digits that
// contain atleast one zero

// function to calculate the
// count of natural numbers
// upto a given number of digits
// that contain atleast one zero
function findCountUpto(d)
{

    // Sum of two GP series
    let GP1_Sum = 9 * ((Math.pow(10, d) - 1) / 9);
    let GP2_Sum = 9 * ((Math.pow(9, d) - 1) / 8);

    return GP1_Sum - GP2_Sum;
}

    // Driver Code
    let d = 1;
    document.write(findCountUpto(d) + "<br>");

     d = 2;
    document.write(findCountUpto(d) + "<br>");

     d = 4;
    document.write(findCountUpto(d)  + "<br>");

// This code is contributed by _saurabh_jaiswal.
```

输出:

```
0
9
2619 
```

时间复杂度:O(1)
辅助空间:O(1)
在下一集里，我们会看到另一个难度增加的问题，可以用非常相似的技巧来解决。

本文由[阿舒托什·库马尔](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 计算游戏中达到给定分数的方式数量

> 原文:[https://www . geesforgeks . org/count-number-way-reach-given-score-game/](https://www.geeksforgeeks.org/count-number-ways-reach-given-score-game/)

考虑一个游戏，玩家可以在一次移动中获得 3、5 或 10 分。给定总分 n，找出达到给定分数的方法。
**例:**

```
Input: n = 20
Output: 4
There are following 4 ways to reach 20
(10, 10)
(5, 5, 10)
(5, 5, 5, 5)
(3, 3, 3, 3, 3, 5)

Input: n = 13
Output: 2
There are following 2 ways to reach 13
(3, 5, 5)
(3, 10)
```

这个问题是[换币问题](https://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)的变种，可以在 O(n)时间和 O(n)辅助空间求解。
想法是创建一个大小为 n+1 的表来存储从 0 到 n 的所有分数的计数。对于每个可能的移动(3、5 和 10)，在表中增加值。

## C++

```
// A C++ program to count number of
// possible ways to a given score
// can be reached in a game where a
// move can earn 3 or 5 or 10
#include <iostream>
using namespace std;

// Returns number of ways
// to reach score n
int count(int n)
{
    // table[i] will store count
    // of solutions for value i.
    int table[n + 1], i;

    // Initialize all table
    // values as 0
    for(int j = 0; j < n + 1; j++)
            table[j] = 0;

    // Base case (If given value is 0)
    table[0] = 1;

    // One by one consider given 3 moves
    // and update the table[] values after
    // the index greater than or equal to
    // the value of the picked move
    for (i = 3; i <= n; i++)
    table[i] += table[i - 3];

    for (i = 5; i <= n; i++)
    table[i] += table[i - 5];

    for (i = 10; i <= n; i++)
    table[i] += table[i - 10];

    return table[n];
}

// Driver Code
int main(void)
{
    int n = 20;
    cout << "Count for " << n
         << " is " << count(n) << endl;

    n = 13;
    cout <<"Count for "<< n<< " is "
         << count(n) << endl;
    return 0;
}

// This code is contributed
// by Shivi_Aggarwal
```

## C

```
// A C program to count number of possible ways to a given score
// can be reached in a game where a move can earn 3 or 5 or 10
#include <stdio.h>

// Returns number of ways to reach score n
int count(int n)
{
    // table[i] will store count of solutions for
    // value i.
    int table[n+1], i;

    // Initialize all table values as 0
    memset(table, 0, sizeof(table));

    // Base case (If given value is 0)
    table[0] = 1;

    // One by one consider given 3 moves and update the table[]
    // values after the index greater than or equal to the
    // value of the picked move
    for (i=3; i<=n; i++)
       table[i] += table[i-3];
    for (i=5; i<=n; i++)
       table[i] += table[i-5];
    for (i=10; i<=n; i++)
       table[i] += table[i-10];

    return table[n];
}

// Driver program
int main(void)
{
    int n = 20;
    printf("Count for %d is %d\n", n, count(n));

    n = 13;
    printf("Count for %d is %d", n, count(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// possible ways to a given score
// can be reached in a game where
// a move can earn 3 or 5 or 10
import java.util.Arrays;

class GFG
{
    // Returns number of ways to reach score n
    static int count(int n)
    {
        // table[i] will store count of solutions for
        // value i.
        int table[] = new int[n + 1], i;

        // Initialize all table values as 0
        Arrays.fill(table, 0);

        // Base case (If given value is 0)
        table[0] = 1;

        // One by one consider given 3
        // moves and update the table[]
        // values after the index greater
        // than or equal to the value of
        // the picked move
        for (i = 3; i <= n; i++)
            table[i] += table[i - 3];
        for (i = 5; i <= n; i++)
            table[i] += table[i - 5];
        for (i = 10; i <= n; i++)
            table[i] += table[i - 10];

        return table[n];
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 20;
        System.out.println("Count for "+n+" is "+count(n));

        n = 13;
        System.out.println("Count for "+n+" is "+count(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to count number of possible ways to a given
# score can be reached in a game where a move can earn 3 or
# 5 or 10.

# Returns number of ways to reach score n.
def count(n):

    # table[i] will store count of solutions for value i.
    # Initialize all table values as 0.
    table = [0 for i in range(n+1)]

    # Base case (If given value is 0)
    table[0] = 1

    # One by one consider given 3 moves and update the
    # table[] values after the index greater than or equal
    # to the value of the picked move.
    for i in range(3, n+1):
        table[i] += table[i-3]
    for i in range(5, n+1):
        table[i] += table[i-5]
    for i in range(10, n+1):
        table[i] += table[i-10]

    return table[n]

# Driver Program
n = 20
print('Count for', n, 'is', count(n))

n = 13
print('Count for', n, 'is', count(n))

# This code is contributed by Soumen Ghosh
```

## C#

```
// C# program to count number of
// possible ways to a given score
// can be reached in a game where
// a move can earn 3 or 5 or 10
using System;

class GFG {

    // Returns number of ways to reach
    // score n
    static int count(int n)
    {

        // table[i] will store count
        // of solutions for value i.
        int []table = new int[n + 1];

        // Initialize all table values
        // as 0
        for(int j = 0; j < n+1; j++)
            table[j] = 0;

        // Base case (If given value is 0)
        table[0] = 1;

        // One by one consider given 3
        // moves and update the table[]
        // values after the index greater
        // than or equal to the value of
        // the picked move
        for (int i = 3; i <= n; i++)
            table[i] += table[i - 3];
        for (int i = 5; i <= n; i++)
            table[i] += table[i - 5];
        for (int i = 10; i <= n; i++)
            table[i] += table[i - 10];

        return table[n];
    }

    // Driver code
    public static void Main ()
    {
        int n = 20;
        Console.WriteLine("Count for "
             + n + " is " + count(n));

        n = 13;
        Console.Write("Count for "
            + n + " is " + count(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of
// possible ways to a given score
// can be reached in a game where
// a move can earn 3 or 5 or 10
// Returns number of ways to reach
// score n
function counts($n)
{
    // table[i] will store count
    // of solutions for value i.

    // Initialize all table
    // values as 0
    for($j = 0; $j < $n + 1; $j++)
            $table[$j] = 0;

    // Base case (If given value is 0)
    $table[0] = 1;

    // One by one consider given 3 moves
    // and update the table[] values after
    // the index greater than or equal to
    // the value of the picked move
    for ($i = 3; $i <= $n; $i++)
    $table[$i] += $table[$i - 3];

    for ($i = 5; $i <= $n; $i++)
    $table[$i] += $table[$i - 5];

    for ($i = 10; $i <= $n; $i++)
    $table[$i] += $table[$i - 10];

    return $table[$n];
}

// Driver Code
$n = 20;
echo "Count for ";
echo($n);
echo (" is ");
echo counts($n);

$n = 13;
echo ("\n") ;
echo "Count for ";
echo($n);
echo (" is " );
echo counts($n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// A JavaScript program to count number of
// possible ways to a given score
// can be reached in a game where a
// move can earn 3 or 5 or 10

// Returns number of ways
// to reach score n
function count(n)
{
    // table[i] will store count
    // of solutions for value i.
    let table = new Array(n + 1), i;

    // Initialize all table
    // values as 0
    for(let j = 0; j < n + 1; j++)
            table[j] = 0;

    // Base case (If given value is 0)
    table[0] = 1;

    // One by one consider given 3 moves
    // and update the table[] values after
    // the index greater than or equal to
    // the value of the picked move
    for (i = 3; i <= n; i++)
    table[i] += table[i - 3];

    for (i = 5; i <= n; i++)
    table[i] += table[i - 5];

    for (i = 10; i <= n; i++)
    table[i] += table[i - 10];

    return table[n];
}

// Driver Code

    let n = 20;
    document.write("Count for " + n
        + " is " + count(n) + "<br>");

    n = 13;
    document.write("Count for "+ n + " is "
        + count(n) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
Count for 20 is 4
Count for 13 is 2 
```

**练习:**当(10，5，5)，(5，5，10)和(5，10，5)被认为是不同的移动顺序时，如何计算分数。类似地，(5，3，3)，(3，5，3)和(3，3，5)被认为是不同的。
本文由**拉杰夫·阿罗拉**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息
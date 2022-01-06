# 炸弹最小数量

> 原文:[https://www.geeksforgeeks.org/minimum-number-bombs/](https://www.geeksforgeeks.org/minimum-number-bombs/)

n 栋建筑中有外星人(每栋建筑中至少有一个)，你必须以最少的爆炸次数杀死所有的外星人。建筑物编号为 1–n。被轰炸建筑物中的外星人在第一次轰炸中受伤，在第二次轰炸中死亡。当一栋建筑第一次被轰炸时，该建筑中的外星人试图逃到最近的建筑(对于第一栋建筑，最近的建筑是第二栋建筑，对于第 n 栋建筑是 n-1)。计算杀死所有外星人所需的最小炸弹数量和爆炸顺序。
示例:

```
Input: 3
Output: 4 
        2 1 3 2 
Explanation: Minimum number of bombs required are 4.
             First bomb the 2nd building, aliens 
             will  move to 1st or 3rd to save
             themselves. Then bomb at 1st building, 
             if some aliens have moved from 2nd 
             building to 1st they will be killed and
             the 1st building aliens will be injured,
             and they will move to the 2nd building
             as it is nearest to them. Now, bomb at
             the 3rd building to kill aliens who 
             moved from the 2nd building to 3rd and
             injure 3rd building aliens so they move 
             to 2nd building as it is nearest to them.
             Now, bomb at the 2nd building again and
             all aliens who moved from 1st or 3rd
             building will be killed.

Input: 2
Output: 3
        2 1 2  
```

我们可以用一种建设性的方式杀死所有外星人。由于每个人要么向左要么向右移动，我们必须确保所有的偶数位置都受到攻击，一次在开始时伤害外星人，另一次在最后。当我们第一次攻击偶数位置的外星人时，他们会移动到奇数位置的建筑，所以在奇数位置攻击他们会杀死所有以前的偶数位置，并伤害奇数位置的外星人。奇数位置的外星人受伤后会移动到偶数位置，所以在最后的偶数位置攻击他们杀死他们。
路数为 *n/2 + n/2 + n/2* 也就是 **n + n/2。**
以下是上述方法的实施:

## C++

```
// CPP program to find number of bombings required
// to kill all aliens.
#include <bits/stdc++.h>
using namespace std;

// function to print where to shoot
void print(int n)
{
    // no. of bombs required
    cout << n + n / 2 << endl;

    // bomb all the even positions
    for (int i = 2; i <= n; i += 2)
        cout << i << " ";

    // bomb all the odd positions
    for (int i = 1; i <= n; i += 2)
        cout << i << " ";

    // bomb all the even positions again
    for (int i = 2; i <= n; i += 2)
        cout << i << " ";
}

// driver program
int main()
{
    int n = 3;
    print(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of bombings
// required to kill all aliens.
class GFG {

    // function to print where to shoot
    static void print(int n)
    {

        // no. of bombs required
        System.out.println(n + n / 2);

        // bomb all the even positions
        for (int i = 2; i <= n; i += 2)
            System.out.print( i + " ");

        // bomb all the odd positions
        for (int i = 1; i <= n; i += 2)
            System.out.print(i + " ");

        // bomb all the even positions again
        for (int i = 2; i <= n; i += 2)
            System.out.print( i + " ");
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3;

        print(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
"""Python program to find number of
bombings required to kill all aliens"""

# function to print where to shoot
def bomb_required(n):

    # no. of bombs required
    print(n+n // 2)

    # bomb all the even positions
    for i in range(2, n + 1, 2):
        print(i, end = " ")

    # bomb all the odd positions
    for i in range(1, n + 1, 2):
        print(i, end = " ")

    # bomb all the even positions again
    for i in range(2, n, 2):
        print(i, end = " ")

# Driver Code        
bomb_required(3)

# This code is contributed by Abhishek Agrawal.
```

## C#

```
// C# program to find number of bombings
// required to kill all aliens.
using System;

class GFG {

    // function to print where to shoot
    static void print(int n)
    {

        // no. of bombs required
        Console.WriteLine(n + n / 2);

        // bomb all the even positions
        for (int i = 2; i <= n; i += 2)
            Console.Write( i + " ");

        // bomb all the odd positions
        for (int i = 1; i <= n; i += 2)
            Console.Write(i + " ");

        // bomb all the even positions
        // again
        for (int i = 2; i <= n; i += 2)
            Console.Write( i + " ");
    }

    // Driver code
    public static void Main ()
    {
        int n = 3;
        print(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number
// of bombings required to
// kill all aliens.

// function to print
// where to shoot
function p_rint($n)
{

    // no. of bombs required
    echo floor($n + $n / 2),"\n" ;

    // bomb all the even positions
    for ($i = 2; $i <= $n; $i += 2)
        echo $i ," ";

    // bomb all the odd positions
    for ( $i = 1; $i <= $n; $i += 2)
        echo $i , " ";

    // bomb all the even positions again
    for ( $i = 2; $i <= $n; $i += 2)
        echo $i , " ";
}

    // Driver Code
    $n = 3;
    p_rint($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to find number of bombings
// required to kill all aliens.   
// function to print where to shoot
    function print(n) {

        // no. of bombs required
        document.write(n + parseInt(n / 2) + "<br/>");

        // bomb all the even positions
        for (i = 2; i <= n; i += 2)
            document.write(i + " ");

        // bomb all the odd positions
        for (i = 1; i <= n; i += 2)
            document.write(i + " ");

        // bomb all the even positions again
        for (i = 2; i <= n; i += 2)
            document.write(i + " ");
    }

    // Driver code   
        var n = 3;
        print(n);

// This code is contributed by Rajput-Ji
</script>
```

输出:

```
4
2 1 3 2
```

**时间复杂度:** O(n)
本文由 [**Raj**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 线性丢番图方程

> 原文:[https://www.geeksforgeeks.org/linear-diophantine-equations/](https://www.geeksforgeeks.org/linear-diophantine-equations/)

丢番图方程是一个多项式方程，通常有两个或更多的未知数，因此只需要积分解。积分解是所有未知变量只取整数值的解。
给定三个整数 a、b、c，表示形式为:ax + by = c 的线性方程，确定方程是否有解，使得 x 和 y 都是整数值。
**例:**

```
Input : a = 3, b = 6, c = 9
Output: Possible
Explanation : The Equation turns out to be, 
3x + 6y = 9 one integral solution would be 
x = 1 , y = 1

Input : a = 3, b = 6, c = 8
Output : Not Possible
Explanation : o integral values of x and y 
exists that can satisfy the equation 3x + 6y = 8

Input : a = 2, b = 5, c = 1
Output : Possible
Explanation : Various integral solutions
possible are, (-2,1) , (3,-1) etc.
```

**解:**
对于线性丢番图方程，当且仅当两个变量的系数的 GCD 完美地除了常数项时，才存在积分解。换句话说，如果 GCD(a，b)除以 c，积分解就存在
因此，确定方程是否有积分解的算法非常简单。

*   求 a 和 b 的 GCD
*   检查 c % GCD(a，b)= 0
*   如果是，则打印“可能”
*   否则无法打印

下面是上述方法的实现。

## C++

```
// C++ program to check for solutions of diophantine
// equations
#include <bits/stdc++.h>
using namespace std;

//utility function to find the GCD of two numbers
int gcd(int a, int b)
{
    return (a%b == 0)? abs(b) : gcd(b,a%b);
}

// This function checks if integral solutions are
// possible
bool isPossible(int a, int b, int c)
{
    return (c%gcd(a,b) == 0);
}

//driver function
int main()
{
    // First example
    int a = 3, b = 6, c = 9;
    isPossible(a, b, c)? cout << "Possible\n" :
                        cout << "Not Possible\n";

    // Second example
    a = 3, b = 6, c = 8;
    isPossible(a, b, c)? cout << "Possible\n" :
                       cout << "Not Possible\n";

    // Third example
    a = 2, b = 5, c = 1;
    isPossible(a, b, c)? cout << "Possible\n" :
                       cout << "Not Possible\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check for solutions of
// diophantine equations
import java.io.*;

class GFG {

    // Utility function to find the GCD
    // of two numbers
    static int gcd(int a, int b)
    {
        return (a % b == 0) ?
                Math.abs(b) : gcd(b,a%b);
    }

    // This function checks if integral
    // solutions are possible
    static boolean isPossible(int a,
                            int b, int c)
    {
        return (c % gcd(a, b) == 0);
    }

    // Driver function
    public static void main (String[] args)
    {
        // First example
        int a = 3, b = 6, c = 9;
        if(isPossible(a, b, c))
            System.out.println( "Possible" );
        else
            System.out.println( "Not Possible");

        // Second example
        a = 3; b = 6; c = 8;
        if(isPossible(a, b, c))
            System.out.println( "Possible") ;
        else
            System.out.println( "Not Possible");

        // Third example
        a = 2; b = 5; c = 1;
        if(isPossible(a, b, c))
            System.out.println( "Possible" );
        else
            System.out.println( "Not Possible");
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to check for solutions
# of diophantine equations
from math import gcd

# This function checks if integral
# solutions are possible
def isPossible(a, b, c):
    return (c % gcd(a, b) == 0)

# Driver Code
if __name__ == '__main__':

    # First example
    a = 3
    b = 6
    c = 9
    if (isPossible(a, b, c)):
        print("Possible")
    else:
        print("Not Possible")

    # Second example
    a = 3
    b = 6
    c = 8
    if (isPossible(a, b, c)):
        print("Possible")
    else:
        print("Not Possible")

    # Third example
    a = 2
    b = 5
    c = 1
    if (isPossible(a, b, c)):
        print("Possible")
    else:
        print("Not Possible")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check for
// solutions of diophantine
// equations
using System;

class GFG
{

    // Utility function to find
    // the GCD of two numbers
    static int gcd(int a, int b)
    {
        return (a % b == 0) ?
                Math.Abs(b) :
               gcd(b, a % b);
    }

    // This function checks
    // if integral solutions
    // are possible
    static bool isPossible(int a,
                           int b,
                           int c)
    {
        return (c % gcd(a, b) == 0);
    }

    // Driver Code
    public static void Main ()
    {
        // First example
        int a = 3, b = 6, c = 9;
        if(isPossible(a, b, c))
            Console.WriteLine("Possible");
        else
            Console.WriteLine("Not Possible");

        // Second example
        a = 3; b = 6; c = 8;
        if(isPossible(a, b, c))
            Console.WriteLine("Possible") ;
        else
            Console.WriteLine("Not Possible");

        // Third example
        a = 2; b = 5; c = 1;
        if(isPossible(a, b, c))
            Console.WriteLine("Possible");
        else
            Console.WriteLine("Not Possible");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check for solutions of
// diophantine equations

// utility function to find the
// GCD of two numbers
function gcd($a, $b)
{
    return ($a % $b == 0) ?
                  abs($b) : gcd($b, $a % $b);
}

// This function checks if integral
// solutions are possible
function isPossible($a, $b, $c)
{
    return ($c % gcd($a, $b) == 0);
}

// Driver Code

// First example
$a = 3;
$b = 6;
$c = 9;
if(isPossible($a, $b, $c) == true)
    echo "Possible\n" ;
else
    echo "Not Possible\n";

// Second example
$a = 3;
$b = 6;
$c = 8;

if(isPossible($a, $b, $c) == true)
    echo "Possible\n" ;
else
    echo "Not Possible\n";

// Third example
$a = 2;
$b = 5;
$c = 1;
if(isPossible($a, $b, $c) == true)
    echo "Possible\n" ;
else
    echo "Not Possible\n";

// This code is contributed by ajit..
?>
```

## java 描述语言

```
<script>

// Javascript program to check for solutions of
// diophantine equations

    // Utility function to find the GCD
    // of two numbers
    function gcd(a, b)
    {
        return (a % b == 0) ?
                Math.abs(b) : gcd(b,a%b);
    }

    // This function checks if integral
    // solutions are possible
    function isPossible(a,
                            b, c)
    {
        return (c % gcd(a, b) == 0);
    }

// Driver Code

        // First example
        let a = 3, b = 6, c = 9;
        if(isPossible(a, b, c))
           document.write( "Possible" + "<br/>" );
        else
           document.write( "Not Possible" + "<br/>" );

        // Second example
        a = 3; b = 6; c = 8;
        if(isPossible(a, b, c))
           document.write( "Possible" + "<br/>" ) ;
        else
           document.write( "Not Possible" + "<br/>" );

        // Third example
        a = 2; b = 5; c = 1;
        if(isPossible(a, b, c))
           document.write( "Possible" + "<br/>" );
        else
           document.write( "Not Possible" + "<br/>" );

</script>
```

**输出:**

```
Possible
Not Possible
Possible
```

**这是怎么工作的？**
让‘a’和‘b’的 GCD 为‘g’。g 除 a 和 b，这意味着 g 也除(ax + by)(如果 x 和 y 是整数)。这意味着 gcd 也使用 ax + by = c 的关系来划分“c”。更多细节请参考[这个](https://en.wikipedia.org/wiki/Diophantine_equation#One_equation)维基链接。
本文由**阿舒托什·库马尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息
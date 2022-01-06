# 欧拉四方形恒等式

> 原文:[https://www.geeksforgeeks.org/eulers-four-square-identity/](https://www.geeksforgeeks.org/eulers-four-square-identity/)

根据[欧拉的四个平方恒等式](https://en.wikipedia.org/wiki/Euler%27s_four-square_identity)，如果 a 和 b 都可以单独表示为四个平方之和，那么任意两个数 a 和 b 的乘积都可以表示为四个平方之和。
数学上，如果 a = ![c1^2 + c2^2 + c3^2 + c4^2    ](img/38d2ef83a5c37ba351567e0fec3d37e4.png "Rendered by QuickLaTeX.com")和 b = ![d1^2 + d2^2 + d3^2 + d4^2    ](img/1633897c99985815bfafd49e88894043.png "Rendered by QuickLaTeX.com")
那么，a * b = ![e1^2 + e2^2 + e3^2 + e4^2    ](img/a9b998e622fecfda7cc3e50f556cadff.png "Rendered by QuickLaTeX.com")
其中 c1、c2、c3、c4、d1、d2、d3、d4、e1、e2、e3、e4 是任意整数。

```
Some examples are,

a =  = 30
b =  = 4
ab = a * b = 120 = 
a =  = 15
b =  = 24
ab = a * b = 810 = 
a =  = 15
b =  = 26
ab = a * b = 390 = 
```

**示例:**

```
Input: a = 1 * 1 + 2 * 2 + 3 * 3 + 4 * 4
       b = 1 * 1 + 1 * 1 + 1 * 1 + 1 * 1

Output: i = 0
j = 2
k = 4
l = 10
Product of 30 and 4 can be written as sum of squares of i, j, k, l
120 = 0 * 0 + 2 * 2 + 4 * 4 + 10 * 10

i = 2
j = 4
k = 6
l = 8
Product of 30 and 4 can be written as sum of squares of i, j, k, l
120 = 2 * 2 + 4 * 4 + 6 * 6 + 8 * 8
```

**解释:**
2 个数字 a(30)和 b(4)的乘积可以表示为 4 个平方之和，如欧拉四平方恒等式所述。以上是乘积 a * b 在 4 个平方形式之和下的 2 种表示。示出了乘积 a*b 在四个平方形式的和中的所有可能的表示。

```
Input: a = 1*1 + 2*2 + 3*3 + 1*1
       b = 1*1 + 2*2 + 1*1 + 1*1

Output: i = 0
j = 1
k = 2
l = 10
Product of 15 and 7 can be written as sum of squares of i, j, k, l
105 = 0*0 + 1*1 + 2*2 + 10*10

i = 0
j = 4
k = 5
l = 8
Product of 15 and 7 can be written as sum of squares of i, j, k, l
105 = 0*0 + 4*4 + 5*5 + 8*8

i = 1
j = 2
k = 6
l = 8
Product of 15 and 7 can be written as sum of squares of i, j, k, l
105 = 1*1 + 2*2 + 6*6 + 8*8

i = 2
j = 2
k = 4
l = 9
Product of 15 and 7 can be written as sum of squares of i, j, k, l
105 = 2*2 + 2*2 + 4*4 + 9*9

i = 2
j = 4
k = 6
l = 7
Product of 15 and 7 can be written as sum of squares of i, j, k, l
105 = 2*2 + 4*4 + 6*6 + 7*7

i = 3
j = 4
k = 4
l = 8
Product of 15 and 7 can be written as sum of squares of i, j, k, l
105 = 3*3 + 4*4 + 4*4 + 8*8
```

**逼近:**
**蛮力:**
一个给定的数(a*b)可以用 4 个循环 I、j、k、l 求 4 个正方形的和的形式表示。这给出了所有可能的组合，以形成四个正方形之和的 a*b。在最内循环(l 循环)的每次迭代中，用乘积 a*b 检查和。如果匹配，则打印平方和等于 a*b 的 4 个数字(I、j、k 和 l)。

## C++

```
// CPP code to verify euler's four square identity
#include <bits/stdc++.h>

using namespace std;

#define show(x) cout << #x << " = " << x << "\n";

// function to check euler four square identity
void check_euler_four_square_identity(int a, int b,
                                      int ab)
{
    int s = 0;

    // loops checking the sum of squares
    for (int i = 0;i * i <= ab;i ++)
    {
        s = i * i;
        for (int j = i;j * j <= ab;j ++)
        {
            // sum of 2 squares
            s = j * j + i * i;

            for (int k = j;k * k <= ab;k ++)
            {
                // sum of 3 squares
                s = k * k + j * j + i * i;

                for (int l = k;l * l <= ab;l ++)
                {
                    // sum of 4 squares
                    s = l * l + k * k + j * j + i * i;

                    // product of 2 numbers represented
                    // as sum of four squares i, j, k, l
                    if (s == ab)
                    {
                        // product of 2 numbers a and b
                        // represented as sum of four
                        // squares i, j, k, l
                        show(i);
                        show(j);
                        show(k);
                        show(l);
                        cout <<""
                        << "Product of " << a
                        << " and " << b;
                        cout << " can be written"<<
                        " as sum of squares of i, "<<
                         "j, k, l\n";
                        cout << ab << " = ";
                        cout << i << "*" << i << " + ";
                        cout << j << "*" << j << " + ";
                        cout << k << "*" << k << " + ";
                        cout << l << "*" << l << "\n";
                        cout << "\n";
                    }
                }
            }
        }
    }
}

// Driver code
int main()
{
    // a and b such that they can be expressed
    // as sum of squares of numbers
    int a = 30; // 1*1 + 2*2 + 3*3 + 4*4;
    int b = 4;  // 1*1 + 1*1 + 1*1 + 1*1;

    // given numbers can be represented as
    // sum of 4 squares By euler's four
    // square identity product also can be
    // represented as sum of 4 squares
    int ab = a * b;

    check_euler_four_square_identity(a, b, ab);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to verify euler's
// four square identity
import java.io.*;

class GFG
{

// function to check euler
// four square identity
static void check_euler_four_square_identity(int a,
                                             int b,
                                             int ab)
{
    int s = 0;

    // loops checking the
    // sum of squares
    for (int i = 0;
             i * i <= ab; i ++)
    {
        s = i * i;
        for (int j = i;
                 j * j <= ab; j ++)
        {
            // sum of 2 squares
            s = j * j + i * i;

            for (int k = j;
                     k * k <= ab; k ++)
            {
                // sum of 3 squares
                s = k * k + j *
                    j + i * i;

                for (int l = k;
                         l * l <= ab; l ++)
                {
                    // sum of 4 squares
                    s = l * l + k * k +
                        j * j + i * i;

                    // product of 2 numbers
                    // represented as sum of
                    // four squares i, j, k, l
                    if (s == ab)
                    {
                        // product of 2 numbers
                        // a and b represented
                        // as sum of four squares
                        // i, j, k, l
                        System.out.print("i = " +
                                          i + "\n");
                        System.out.print("j = " +
                                          j + "\n");
                        System.out.print("k = " +
                                          k + "\n");
                        System.out.print("l = " +
                                          l + "\n");
                        System.out.print("Product of " +
                                         a + " and " + b);
                        System.out.print(" can be written"+
                               " as sum of squares of i, "+
                                              "j, k, l\n");
                        System.out.print(ab + " = ");
                        System.out.print(i + "*" +
                                         i + " + ");
                        System.out.print(j + "*" +
                                         j + " + ");
                        System.out.print(k + "*" +
                                         k + " + ");
                        System.out.print(l + "*" +
                                         l + "\n");
                        System.out.println();
                    }
                }
            }
        }
    }
}

// Driver code
public static void main (String[] args)
{
    // a and b such that
    // they can be expressed
    // as sum of squares
    // of numbers
    int a = 30; // 1*1 + 2*2 +
                // 3*3 + 4*4;
    int b = 4;  // 1*1 + 1*1 +
                // 1*1 + 1*1;

    // given numbers can be
    // represented as sum of
    // 4 squares By euler's
    // four square identity
    // product also can be
    // represented as sum
    // of 4 squares
    int ab = a * b;

    check_euler_four_square_identity(a, b, ab);
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 code to verify euler's
# four square identity

# function to check euler
# four square identity
def check_euler_four_square_identity(a, b, ab):

    s = 0;

    # loops checking the sum of squares
    i = 0;
    while (i * i <= ab):

        s = i * i;
        j = i;
        while (j * j <= ab):

            # sum of 2 squares
            s = j * j + i * i;
            k = j;
            while (k * k <= ab):

                # sum of 3 squares
                s = k * k + j * j + i * i;
                l = k;
                while (l * l <= ab):

                    # sum of 4 squares
                    s = l * l + k * k + j * j + i * i;

                    # product of 2 numbers represented
                    # as sum of four squares i, j, k, l
                    if (s == ab):

                        # product of 2 numbers a and b
                        # represented as sum of four
                        # squares i, j, k, l
                        print("i =", i);
                        print("j =", j);
                        print("k =", k);
                        print("l =", l);
                        print("Product of ", a,
                              "and", b, end = "");
                        print(" can be written as sum of",
                                  "squares of i, j, k, l");
                        print(ab, "= ", end = "");
                        print(i, "*", i, "+ ", end = "");
                        print(j, "*", j, "+ ", end = "");
                        print(k, "*", k, "+ ", end = "");
                        print(l, "*", l);
                        print("");
                    l += 1;
                k += 1;
            j += 1;
        i += 1;

# Driver code

# a and b such that they can be expressed
# as sum of squares of numbers
a = 30; # 1*1 + 2*2 + 3*3 + 4*4;
b = 4; # 1*1 + 1*1 + 1*1 + 1*1;

# given numbers can be represented as
# sum of 4 squares By euler's four
# square identity product also can be
# represented as sum of 4 squares
ab = a * b;

check_euler_four_square_identity(a, b, ab);

# This code is contributed
# by mits
```

## C#

```
// C# code to verify euler's
// four square identity
using System;

class GFG
{
    // function to check euler
    // four square identity
    static void check_euler_four_square_identity(int a,
                                                 int b,
                                                 int ab)
    {
        int s = 0;

        // loops checking the
        // sum of squares
        for (int i = 0; i * i <= ab; i ++)
        {
            s = i * i;
            for (int j = i; j * j <= ab; j ++)
            {
                // sum of 2 squares
                s = j * j + i * i;

                for (int k = j; k * k <= ab; k ++)
                {
                    // sum of 3 squares
                    s = k * k + j *
                        j + i * i;

                    for (int l = k; l * l <= ab; l ++)
                    {
                        // sum of 4 squares
                        s = l * l + k * k +
                            j * j + i * i;

                        // product of 2 numbers
                        // represented as sum of
                        // four squares i, j, k, l
                        if (s == ab)
                        {
                            // product of 2 numbers a
                            // and b represented as 
                            // sum of four squares i, j, k, l
                            Console.Write("i = " + i + "\n");
                            Console.Write("j = " + j + "\n");
                            Console.Write("k = " + k + "\n");
                            Console.Write("l = " + l + "\n");
                            Console.Write("Product of " + a +
                                                " and " + b);
                            Console.Write(" can be written"+
                                " as sum of squares of i, "+
                                               "j, k, l\n");
                            Console.Write(ab + " = ");
                            Console.Write(i + "*" + i + " + ");
                            Console.Write(j + "*" + j + " + ");
                            Console.Write(k + "*" + k + " + ");
                            Console.Write(l + "*" + l + "\n");
                            Console.Write("\n");
                        }
                    }
                }
            }
        }
    }

    // Driver code
    static void Main()
    {
        // a and b such that
        // they can be expressed
        // as sum of squares of numbers
        int a = 30; // 1*1 + 2*2 + 3*3 + 4*4;
        int b = 4; // 1*1 + 1*1 + 1*1 + 1*1;

        // given numbers can be
        // represented as sum of
        // 4 squares By euler's
        // four square identity
        // product also can be
        // represented as sum
        // of 4 squares
        int ab = a * b;

        check_euler_four_square_identity(a, b, ab);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to verify euler's
// four square identity

// function to check euler
// four square identity
function check_euler_four_square_identity($a, $b, $ab)
{
    $s = 0;

    // loops checking the sum of squares
    for ($i = 0; $i * $i <= $ab; $i ++)
    {
        $s = $i * $i;
        for ($j = $i; $j * $j <= $ab; $j ++)
        {
            // sum of 2 squares
            $s = $j * $j + $i * $i;

            for ($k = $j; $k * $k <= $ab; $k ++)
            {
                // sum of 3 squares
                $s = $k * $k + $j * $j + $i * $i;

                for ($l = $k; $l * $l <= $ab; $l ++)
                {
                    // sum of 4 squares
                    $s = $l * $l + $k * $k +
                         $j * $j + $i * $i;

                    // product of 2 numbers represented
                    // as sum of four squares i, j, k, l
                    if ($s == $ab)
                    {
                        // product of 2 numbers a and b
                        // represented as sum of four
                        // squares i, j, k, l
                        echo("i = " . $i . "\n");
                        echo("j = " . $j . "\n");
                        echo("k = " . $k . "\n");
                        echo("l = " . $l . "\n");
                        echo "". "Product of " .
                            $a . " and " . $b;
                        echo " can be written".
                             " as sum of squares of i, " .
                                              "j, k, l\n";
                        echo $ab . " = ";
                        echo $i . "*" . $i. " + ";
                        echo $j . "*" . $j . " + ";
                        echo $k . "*" . $k . " + ";
                        echo $l . "*" . $l . "\n";
                        echo "\n";
                    }
                }
            }
        }
    }
}

// Driver code

// a and b such that they can be expressed
// as sum of squares of numbers
$a = 30; // 1*1 + 2*2 + 3*3 + 4*4;
$b = 4; // 1*1 + 1*1 + 1*1 + 1*1;

// given numbers can be represented as
// sum of 4 squares By euler's four
// square identity product also can be
// represented as sum of 4 squares
$ab = $a * $b;

check_euler_four_square_identity($a, $b, $ab);

// This code is contributed
// by Abby_akku
?>
```

## java 描述语言

```
<script>

    // Javascript code to verify euler's
    // four square identity

    // function to check euler
    // four square identity
    function check_euler_four_square_identity(a, b, ab)
    {
        let s = 0;

        // loops checking the
        // sum of squares
        for (let i = 0; i * i <= ab; i ++)
        {
            s = i * i;
            for (let j = i; j * j <= ab; j ++)
            {
                // sum of 2 squares
                s = j * j + i * i;

                for (let k = j; k * k <= ab; k ++)
                {
                    // sum of 3 squares
                    s = k * k + j *
                        j + i * i;

                    for (let l = k; l * l <= ab; l ++)
                    {
                        // sum of 4 squares
                        s = l * l + k * k +
                            j * j + i * i;

                        // product of 2 numbers
                        // represented as sum of
                        // four squares i, j, k, l
                        if (s == ab)
                        {
                            // product of 2 numbers a
                            // and b represented as 
                            // sum of four squares
                            // i, j, k, l
                            document.write("i = " + i +
                            "</br>");
                            document.write("j = " + j +
                            "</br>");
                            document.write("k = " + k +
                            "</br>");
                            document.write("l = " + l +
                            "</br>");
                            document.write("Product of " + a +
                                                " and " + b);
                            document.write(" can be written"+
                                " as sum of squares of i, "+
                                               "j, k, l" +
                                               "</br>");
                            document.write(ab + " = ");
                            document.write(i + "*" + i +
                            " + ");
                            document.write(j + "*" + j +
                            " + ");
                            document.write(k + "*" + k +
                            " + ");
                            document.write(l + "*" + l +
                            "</br>");
                            document.write("</br>");
                        }
                    }
                }
            }
        }
    }

    // a and b such that
    // they can be expressed
    // as sum of squares of numbers
    let a = 30; // 1*1 + 2*2 + 3*3 + 4*4;
    let b = 4; // 1*1 + 1*1 + 1*1 + 1*1;

    // given numbers can be
    // represented as sum of
    // 4 squares By euler's
    // four square identity
    // product also can be
    // represented as sum
    // of 4 squares
    let ab = a * b;

    check_euler_four_square_identity(a, b, ab);

</script>
```

**Output:** 

```
i = 0
j = 2
k = 4
l = 10
Product of 30 and 4 can be written as sum of squares of i, j, k, l
120 = 0*0 + 2*2 + 4*4 + 10*10

i = 2
j = 4
k = 6
l = 8
Product of 30 and 4 can be written as sum of squares of i, j, k, l
120 = 2*2 + 4*4 + 6*6 + 8*8
```

**改进算法:**
上述算法的时间复杂度在最坏情况下为![O((a*b)^4)    ](img/9661efb8b003ef550d71c52db15dad68.png "Rendered by QuickLaTeX.com")。这可以通过从所有(I，j，k)的乘积 a*b 中减去 I，j 和 k 的平方并检查该值是否是一个完美的平方来简化为![O((a*b)^3) ](img/8dd96f41044ff2c529b29d116d9de94e.png "Rendered by QuickLaTeX.com")。如果它是一个完美的正方形，那么我们已经找到了解决方案。

## C++

```
// CPP code to verify Euler's four-square identity
#include<bits/stdc++.h>
using namespace std;

// This function prints the four numbers
// if a solution is found Else prints
// solution doesn't exist
void checkEulerFourSquareIdentity(int a, int b)
{
    // Number for which we want to
    // find a solution
    int ab = a * b;
    bool flag = false;

    int i = 0;
    while(i * i <= ab) // loop for first number
    {
        int j = i;
        while (i * i + j * j <= ab) // loop for second number
        {
            int k = j;
            while(i * i + j * j +
                k * k <= ab) // loop for third number
            {
                // Calculate the fourth number
                // and apply square root
                double l = sqrt(ab - (i * i + j *
                                        j + k * k));

                // Check if the fourthNum is Integer or
                // not. If yes, then solution is found
                if (floor(l) == ceil(l) && l >= k)
                {
                    flag = true;
                    cout<<"i = " << i << "\n";
                    cout<<"j = " << j << "\n";
                    cout<<"k = " << k << "\n";
                    cout<<"l = " << (int)l << "\n";
                    cout<<"Product of " << a << " and "<< b <<
                                " can be written as sum of squares"<<
                                                " of i, j, k, l \n";

                    cout<<ab + " = " << i << "*" << i << " + " <<
                                        j << "*" << j<< " + " << k << "*" <<
                                            k << " + " << (int)l << "*" <<
                                                        (int)l << "\n";

                }
                k += 1;
            }
            j += 1;
        }
        i += 1;
    }

    // Solution cannot be found
    if (flag == false)
    {
        cout<< "Solution doesn't exist!\n";
        return ;
    }
}

// Driver Code
int main()
{
    int a = 30;
    int b = 4;
    checkEulerFourSquareIdentity(a, b);
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to verify Euler's four-square identity
class GFG
{

// This function prints the four numbers
// if a solution is found Else prints
// solution doesn't exist
public static void checkEulerFourSquareIdentity(int a,
                                                int b)
{
    // Number for which we want to
    // find a solution
    int ab = a * b;
    boolean flag = false;

    int i = 0;
    while(i * i <= ab) // loop for first number
    {
        int j = i;
        while (i * i + j * j <= ab) // loop for second number
        {
            int k = j;
            while(i * i + j * j +
                  k * k <= ab) // loop for third number
            {
                // Calculate the fourth number
                // and apply square root
                double l = Math.sqrt(ab - (i * i + j *
                                           j + k * k));

                // Check if the fourthNum is Integer or
                // not. If yes, then solution is found
                if (Math.floor(l) == Math.ceil(l) && l >= k)
                {
                    flag = true;
                    System.out.print("i = "  + i + "\n");
                    System.out.print("j = " + j + "\n");
                    System.out.print("k = " + k + "\n");
                    System.out.print("l = " + (int)l + "\n");
                    System.out.print("Product of " + a + " and "+ b +
                                 " can be written as sum of squares"+
                                                " of i, j, k, l \n");

                    System.out.print(ab + " = " + i + "*" + i + " + " +
                                        j + "*" + j + " + " + k + "*" +
                                             k + " + " + (int)l + "*" +
                                                        (int)l + "\n");

                }
                k += 1;
            }
            j += 1;
        }
        i += 1;
    }

    // Solution cannot be found
    if (flag == false)
    {
        System.out.println("Solution doesn't exist!");
        return ;
    }
}

// Driver Code
public static void main(String[] args)
{
    int a = 30;
    int b = 4;
    checkEulerFourSquareIdentity(a, b);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 code to verify Euler's four-square identity
# This function prints the four numbers if a solution is found
# Else prints solution doesn't exist
def checkEulerFourSquareIdentity(a, b):

    # Number for which we want to find a solution
    ab = a*b
    flag = False

    i = 0
    while i*i <= ab: # loop for first number

        j = i
        while i*i + j*j <= ab: # loop for second number

            k = j
            while i*i + j*j + k*k <= ab: # loop for third number

                # Calculate the fourth number and apply square root
                l = (ab - (i*i + j*j + k*k))**(0.5)

                # Check if the fourthNum is Integer or not
                # If yes, then solution is found
                if l == int(l) and l >= k:
                    flag = True
                    print("i = ",i)
                    print("j = ",j)
                    print("k = ",k)
                    print("l = ",l)
                    print("Product of", a , "and" , b ,
                          "can be written as sum of squares of i, j, k, l" )
                    print(ab," = ",i,"*",i,"+",j,"*",j,"+",
                          k,"*",k,"+",l,"*",l)

                k += 1

            j += 1

        i += 1

    # Solution cannot be found
    if flag == False:
        print("Solution doesn't exist!")
        return

a, b = 30, 4
checkEulerFourSquareIdentity(a,b)
```

## C#

```
// C# code to verify Euler's four-square identity
using System;

class GFG
{

// This function prints the four numbers
// if a solution is found Else prints
// solution doesn't exist
public static void checkEulerFourSquareIdentity(int a,
                                                int b)
{
    // Number for which we want to
    // find a solution
    int ab = a * b;
    bool flag = false;

    int i = 0;
    while(i * i <= ab) // loop for first number
    {
        int j = i;
        while (i * i + j * j <= ab) // loop for second number
        {
            int k = j;
            while(i * i + j * j +
                  k * k <= ab) // loop for third number
            {
                // Calculate the fourth number
                // and apply square root
                double l = Math.Sqrt(ab - (i * i + j *
                                           j + k * k));

                // Check if the fourthNum is Integer or
                // not. If yes, then solution is found
                if (Math.Floor(l) == Math.Ceiling(l) && l >= k)
                {
                    flag = true;
                    Console.Write("i = " + i + "\n");
                    Console.Write("j = " + j + "\n");
                    Console.Write("k = " + k + "\n");
                    Console.Write("l = " + (int)l + "\n");
                    Console.Write("Product of " + a + " and "+ b +
                              " can be written as sum of squares"+
                                             " of i, j, k, l \n");

                    Console.Write(ab + " = " + i + "*" + i + " + " +
                                     j + "*" + j + " + " + k + "*" +
                                          k + " + " + (int)l + "*" +
                                                      (int)l + "\n");

                }
                k += 1;
            }
            j += 1;
        }
        i += 1;
    }

    // Solution cannot be found
    if (flag == false)
    {
        Console.WriteLine("Solution doesn't exist!");
        return ;
    }
}

// Driver Code
public static void Main()
{
    int a = 30;
    int b = 4;
    checkEulerFourSquareIdentity(a, b);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to verify Euler's four-square identity

// This function prints the four numbers
// if a solution is found Else prints
// solution doesn't exist
function checkEulerFourSquareIdentity($a, $b)
{
    // Number for which we want to
    // find a solution
    $ab = $a * $b;
    $flag = false;

    $i = 0;
    while($i * $i <= $ab) // loop for first number
    {
        $j = $i;
        while ($i * $i + $j * $j <= $ab) // loop for second number
        {
            $k = $j;
            while($i * $i + $j * $j +
                  $k * $k <= $ab) // loop for third number
            {
                // Calculate the fourth number
                // and apply square root
                $l = sqrt($ab - ($i * $i + $j *
                                 $j + $k * $k));

                // Check if the fourthNum is Integer or
                // not. If yes, then solution is found
                if (floor($l) == ceil($l) && $l >= $k)
                {
                    $flag = true;
                    print("i = " . $i . "\n");
                    print("j = " . $j . "\n");
                    print("k = " . $k . "\n");
                    print("l = " . $l . "\n");
                    print("Product of " . $a . " and " . $b .
                          " can be written as sum of squares" .
                                          " of i, j, k, l \n");
                    print($ab . " = " . $i . "*" . $i . " + " .
                          $j . "*" . $j . " + " . $k . "*" .
                          $k . " + " . $l . "*" . $l . "\n");

                }
                $k += 1;
            }
            $j += 1;
        }
        $i += 1;
    }
    // Solution cannot be found
    if ($flag == false)
    {
        print("Solution doesn't exist!");
        return 0;
    }
}

// Driver Code
$a = 30;
$b = 4;
checkEulerFourSquareIdentity($a, $b);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript code to verify Euler's four-square identity

    // This function prints the four numbers
    // if a solution is found Else prints
    // solution doesn't exist
    function checkEulerFourSquareIdentity(a, b)
    {
        // Number for which we want to
        // find a solution
        let ab = a * b;
        let flag = false;

        let i = 0;
        while(i * i <= ab) // loop for first number
        {
            let j = i;
            while (i * i + j * j <= ab) // loop for second number
            {
                let k = j;
                while(i * i + j * j +
                      k * k <= ab) // loop for third number
                {
                    // Calculate the fourth number
                    // and apply square root
                    let l = Math.sqrt(ab - (i * i + j * j + k * k));

                    // Check if the fourthNum is Integer or
                    // not. If yes, then solution is found
                    if (Math.floor(l) == Math.ceil(l) && l >= k)
                    {
                        flag = true;
                        document.write("i = " + i + "</br>");
                        document.write("j = " + j + "</br>");
                        document.write("k = " + k + "</br>");
                        document.write("l = " + l + "</br>");
                        document.write("Product of " + a + " and "+ b +
                                  " can be written as sum of squares"+
                                                 " of i, j, k, l " + "</br>");

                        document.write(ab + " = " + i + "*" + i + " + " +
                                         j + "*" + j + " + " + k + "*" +
                                              k + " + " + l + "*" +
                                                          l + "</br>");

                    }
                    k += 1;
                }
                j += 1;
            }
            i += 1;
        }

        // Solution cannot be found
        if (flag == false)
        {
            document.write("Solution doesn't exist!" + "</br>");
            return;
        }
    }

    let a = 30;
    let b = 4;
    checkEulerFourSquareIdentity(a, b);

</script>
```

**输出:**

```

i = 0
j = 2
k = 4
l = 10
Product of 30 and 4 can be written as sum of squares of i, j, k, l
120 = 0*0 + 2*2 + 4*4 + 10*10
i = 2
j = 4
k = 6
l = 8
Product of 30 and 4 can be written as sum of squares of i, j, k, l
120 = 2*2 + 4*4 + 6*6 + 8*8
```
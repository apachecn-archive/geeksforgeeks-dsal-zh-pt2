# 矩阵求幂

> 原文:[https://www.geeksforgeeks.org/matrix-exponentiation/](https://www.geeksforgeeks.org/matrix-exponentiation/)

这是竞争性编程中最常用的技术之一。让我们首先考虑下面这个简单的问题。
寻找第 n 个斐波那契数的最小时间复杂度是多少？
我们可以利用矩阵幂运算找到 O(Log n)时间内的第 n 个斐波那契数。详见[本](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)方法四。在这篇文章中，讨论了矩阵幂运算的一般实现。

```
For solving the matrix exponentiation we are assuming a
linear recurrence equation like below:

F(n) = a*F(n-1) + b*F(n-2) + c*F(n-3)   for n >= 3 
                                 . . . . . Equation (1)
where a, b and c are constants. 

For this recurrence relation, it depends on three previous values. 
Now we will try to represent Equation (1) in terms of the matrix. 

[First Matrix] = [Second matrix] * [Third Matrix]
| F(n)   |     =   Matrix 'C'    *  | F(n-1) |
| F(n-1) |                          | F(n-2) |
| F(n-2) |                          | F(n-3) |

Dimension of the first matrix is 3 x 1 . 
Dimension of the third matrix is also 3 x 1\. 

So the dimension of the second matrix must be 3 x 3 
[For multiplication rule to be satisfied.]

Now we need to fill the Matrix 'C'. 

So according to our equation. 
F(n) = a*F(n-1) + b*F(n-2) + c*F(n-3)
F(n-1) = F(n-1)
F(n-2) = F(n-2)

C = [a b c
     1 0 0
     0 1 0]

Now the relation between matrix becomes : 
[First Matrix]  [Second matrix]       [Third Matrix]
| F(n)   |  =  | a b c |  *           | F(n-1) |
| F(n-1) |     | 1 0 0 |              | F(n-2) |
| F(n-2) |     | 0 1 0 |              | F(n-3) |

Lets assume the initial values for this case :- 
F(0) = 0
F(1) = 1
F(2) = 1

So, we need to get F(n) in terms of these values.

So, for n = 3 Equation (1) changes to 
| F(3) |  =  | a b c |  *           | F(2) |
| F(2) |     | 1 0 0 |              | F(1) |
| F(1) |     | 0 1 0 |              | F(0) |

Now similarly for n = 4 
| F(4) |  =  | a b c |  *           | F(3) |
| F(3) |     | 1 0 0 |              | F(2) |
| F(2) |     | 0 1 0 |              | F(1) |

             - - - -  2 times - - -
| F(4) |  =  | a b c |  * | a b c | *       | F(2) |
| F(3) |     | 1 0 0 |    | 1 0 0 |         | F(1) |
| F(2) |     | 0 1 0 |    | 0 1 0 |         | F(0) |

So for n, the Equation (1) changes to 

                - - - - - - - - n -2 times - - - -  -       
| F(n)   |  =  | a b c | * | a b c | * ... * | a b c | * | F(2) |
| F(n-1) |     | 1 0 0 |   | 1 0 0 |         | 1 0 0 |   | F(1) |
| F(n-2) |     | 0 1 0 |   | 0 1 0 |         | 0 1 0 |   | F(0) |

| F(n)   |  =  [ | a b c | ] ^ (n-2)   *  | F(2) |
| F(n-1) |     [ | 1 0 0 | ]              | F(1) |
| F(n-2) |     [ | 0 1 0 | ]              | F(0) |
```

所以我们可以简单地将我们的第二个矩阵乘以 n-2 倍，然后与第三个矩阵相乘，得到结果。乘法可以用乘幂的分治算法在(log n)时间内完成(见[本](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/)或[本](https://www.geeksforgeeks.org/write-an-iterative-olog-y-function-for-powx-y/) )
让我们考虑用下面的递推公式求出数列的第 n 项的问题。

```
n'th term,
    F(n) = F(n-1) + F(n-2) + F(n-3), n >= 3
Base Cases :
    F(0) = 0, F(1) = 1, F(2) = 1
```

我们可以通过以下方式找到第 n 项:

```
Putting a = 1, b = 1 and c = 1 in above formula

| F(n)   |  =  [ | 1 1 1 | ] ^ (n-2)   *  | F(2) |
| F(n-1) |     [ | 1 0 0 | ]              | F(1) |
| F(n-2) |     [ | 0 1 0 | ]              | F(0) |
```

以下是上述想法的实现。

## C++

```
// C++ program to find value of f(n) where f(n)
// is defined as
//    F(n) = F(n-1) + F(n-2) + F(n-3), n >= 3
// Base Cases :
//    F(0) = 0, F(1) = 1, F(2) = 1
#include<bits/stdc++.h>
using namespace std;

// A utility function to multiply two matrices
// a[][] and b[][].  Multiplication result is
// stored back in b[][]
void multiply(int a[3][3], int b[3][3])
{
    // Creating an auxiliary matrix to store elements
    // of the multiplication matrix
    int mul[3][3];
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            mul[i][j] = 0;
            for (int k = 0; k < 3; k++)
                mul[i][j] += a[i][k]*b[k][j];
        }
    }

    // storing the multiplication result in a[][]
    for (int i=0; i<3; i++)
        for (int j=0; j<3; j++)
            a[i][j] = mul[i][j];  // Updating our matrix
}

// Function to compute F raise to power n-2.
int power(int F[3][3], int n)
{
    int M[3][3] = {{1,1,1}, {1,0,0}, {0,1,0}};

    // Multiply it with initial values i.e with
    // F(0) = 0, F(1) = 1, F(2) = 1
    if (n==1)
        return F[0][0] + F[0][1];

    power(F, n/2);

    multiply(F, F);

    if (n%2 != 0)
        multiply(F, M);

    // Multiply it with initial values i.e with
    // F(0) = 0, F(1) = 1, F(2) = 1
    return F[0][0] + F[0][1] ;
}

// Return n'th term of a series defined using below
// recurrence relation.
// f(n) is defined as
//    f(n) = f(n-1) + f(n-2) + f(n-3), n>=3
// Base Cases :
//    f(0) = 0, f(1) = 1, f(2) = 1
int findNthTerm(int n)
{

    int F[3][3] = {{1,1,1}, {1,0,0}, {0,1,0}} ;

    //Base cases
    if(n==0)
        return 0;
    if(n==1 || n==2)
        return 1;

    return power(F, n-2);
}

// Driver code
int main()
{
   int n = 5;

   cout << "F(5) is " << findNthTerm(n);

   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find value of f(n) where
// f(n) is defined as
// F(n) = F(n-1) + F(n-2) + F(n-3), n >= 3
// Base Cases :
// F(0) = 0, F(1) = 1, F(2) = 1
import java.io.*;

class GFG {

    // A utility function to multiply two
    // matrices a[][] and b[][].
    // Multiplication result is
    // stored back in b[][]
    static void multiply(int a[][], int b[][])
    {
        // Creating an auxiliary matrix to
        // store elements of the
        // multiplication matrix
        int mul[][] = new int[3][3];
        for (int i = 0; i < 3; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                mul[i][j] = 0;
                for (int k = 0; k < 3; k++)
                    mul[i][j] += a[i][k]
                                * b[k][j];
            }
        }

        // storing the multiplication
        // result in a[][]
        for (int i=0; i<3; i++)
            for (int j=0; j<3; j++)

                // Updating our matrix
                a[i][j] = mul[i][j];
    }

    // Function to compute F raise to
    // power n-2.
    static int power(int F[][], int n)
    {
        int M[][] = {{1, 1, 1}, {1, 0, 0},
                               {0, 1, 0}};

        // Multiply it with initial values
        // i.e with F(0) = 0, F(1) = 1,
        // F(2) = 1
        if (n == 1)
            return F[0][0] + F[0][1];

        power(F, n / 2);

        multiply(F, F);

        if (n%2 != 0)
            multiply(F, M);

        // Multiply it with initial values
        // i.e with F(0) = 0, F(1) = 1,
        // F(2) = 1
        return F[0][0] + F[0][1] ;
    }

    // Return n'th term of a series defined
    // using below recurrence relation.
    // f(n) is defined as
    // f(n) = f(n-1) + f(n-2) + f(n-3), n>=3
    // Base Cases :
    // f(0) = 0, f(1) = 1, f(2) = 1
    static int findNthTerm(int n)
    {
        int F[][] = {{1, 1, 1}, {1, 0, 0},
                                  {0, 1, 0}} ;

        return power(F, n-2);
    }

    // Driver code
    public static void main (String[] args) {

        int n = 5;

        System.out.println("F(5) is "
                           + findNthTerm(n));
    }
}

//This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find value of f(n)
# where f(n) is defined as
# F(n) = F(n-1) + F(n-2) + F(n-3), n >= 3
# Base Cases :
# F(0) = 0, F(1) = 1, F(2) = 1

# A utility function to multiply two
# matrices a[][] and b[][]. Multiplication
# result is stored back in b[][]
def multiply(a, b):

    # Creating an auxiliary matrix
    # to store elements of the
    # multiplication matrix
    mul = [[0 for x in range(3)]
              for y in range(3)];
    for i in range(3):
        for j in range(3):
            mul[i][j] = 0;
            for k in range(3):
                mul[i][j] += a[i][k] * b[k][j];

    # storing the multiplication
    # result in a[][]
    for i in range(3):
        for j in range(3):
            a[i][j] = mul[i][j]; # Updating our matrix
    return a;

# Function to compute F raise
# to power n-2.
def power(F, n):

    M = [[1, 1, 1], [1, 0, 0], [0, 1, 0]];

    # Multiply it with initial values i.e
    # with F(0) = 0, F(1) = 1, F(2) = 1
    if (n == 1):
        return F[0][0] + F[0][1];

    power(F, int(n / 2));

    F = multiply(F, F);

    if (n % 2 != 0):
        F = multiply(F, M);

    # Multiply it with initial values i.e
    # with F(0) = 0, F(1) = 1, F(2) = 1
    return F[0][0] + F[0][1] ;

# Return n'th term of a series defined
# using below recurrence relation.
# f(n) is defined as
# f(n) = f(n-1) + f(n-2) + f(n-3), n>=3
# Base Cases :
# f(0) = 0, f(1) = 1, f(2) = 1
def findNthTerm(n):
    F = [[1, 1, 1], [1, 0, 0], [0, 1, 0]];

    return power(F, n - 2);

# Driver code
n = 5;

print("F(5) is",
      findNthTerm(n));

# This code is contributed by mits
```

## C#

```
// C# program to find value of f(n) where
// f(n) is defined as
// F(n) = F(n-1) + F(n-2) + F(n-3), n >= 3
// Base Cases :
// F(0) = 0, F(1) = 1, F(2) = 1
using System;

class GFG {

    // A utility function to multiply two
    // matrices a[][] and b[][]. Multiplication
    // result is stored back in b[][]
    static void multiply(int[, ] a, int[, ] b)
    {

        // Creating an auxiliary matrix to store
        // elements of the multiplication matrix
        int[, ] mul = new int[3, 3];

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                mul[i, j] = 0;
                for (int k = 0; k < 3; k++)
                    mul[i, j] += a[i, k] * b[k, j];
            }
        }

        // storing the multiplication result
        // in a[][]
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)

                // Updating our matrix
                a[i, j] = mul[i, j];
    }

    // Function to compute F raise to power n-2.
    static int power(int[, ] F, int n)
    {

        int[, ] M = { { 1, 1, 1 }, { 1, 0, 0 },
                                   { 0, 1, 0 } };

        // Multiply it with initial values i.e
        // with F(0) = 0, F(1) = 1, F(2) = 1
        if (n == 1)
            return F[0, 0] + F[0, 1];

        power(F, n / 2);

        multiply(F, F);

        if (n % 2 != 0)
            multiply(F, M);

        // Multiply it with initial values i.e
        // with F(0) = 0, F(1) = 1, F(2) = 1
        return F[0, 0] + F[0, 1];
    }

    // Return n'th term of a series defined
    // using below recurrence relation.
    // f(n) is defined as
    // f(n) = f(n-1) + f(n-2) + f(n-3), n>=3
    // Base Cases :
    // f(0) = 0, f(1) = 1, f(2) = 1
    static int findNthTerm(int n)
    {
        int[, ] F = { { 1, 1, 1 }, { 1, 0, 0 },
                                 { 0, 1, 0 } };

        return power(F, n - 2);
    }

    // Driver code
    public static void Main()
    {
        int n = 5;

        Console.WriteLine("F(5) is "
                      + findNthTerm(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find value of f(n) where f(n)
// is defined as
// F(n) = F(n-1) + F(n-2) + F(n-3), n >= 3
// Base Cases :
// F(0) = 0, F(1) = 1, F(2) = 1

// A utility function to multiply two matrices
// a[][] and b[][]. Multiplication result is
// stored back in b[][]
function multiply(&$a, &$b)
{
    // Creating an auxiliary matrix to store
    // elements of the multiplication matrix
    $mul = array_fill(0, 3,
           array_fill(0, 3, 0));
    for ($i = 0; $i < 3; $i++)
    {
        for ($j = 0; $j < 3; $j++)
        {
            $mul[$i][$j] = 0;
            for ($k = 0; $k < 3; $k++)
                $mul[$i][$j] += $a[$i][$k] *
                                $b[$k][$j];
        }
    }

    // storing the multiplication result in a[][]
    for ($i = 0; $i < 3; $i++)
        for ($j = 0; $j < 3; $j++)
            $a[$i][$j] = $mul[$i][$j]; // Updating our matrix
}

// Function to compute F raise to power n-2.
function power($F, $n)
{
    $M = array(array(1, 1, 1),
               array(1, 0, 0),
               array(0, 1, 0));

    // Multiply it with initial values i.e with
    // F(0) = 0, F(1) = 1, F(2) = 1
    if ($n == 1)
        return $F[0][0] + $F[0][1];

    power($F, (int)($n / 2));

    multiply($F, $F);

    if ($n % 2 != 0)
        multiply($F, $M);

    // Multiply it with initial values i.e with
    // F(0) = 0, F(1) = 1, F(2) = 1
    return $F[0][0] + $F[0][1] ;
}

// Return n'th term of a series defined
// using below recurrence relation.
// f(n) is defined as
// f(n) = f(n-1) + f(n-2) + f(n-3), n>=3
// Base Cases :
// f(0) = 0, f(1) = 1, f(2) = 1
function findNthTerm($n)
{
    $F = array(array(1, 1, 1),
               array(1, 0, 0),
               array(0, 1, 0));

    return power($F, $n - 2);
}

// Driver code
$n = 5;

echo "F(5) is " . findNthTerm($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to find value of f(n) where
// f(n) is defined as
// F(n) = F(n-1) + F(n-2) + F(n-3), n >= 3
// Base Cases :
// F(0) = 0, F(1) = 1, F(2) = 1

// A utility function to multiply two
// matrices a and b.
// Multiplication result is
// stored back in b
function multiply(a , b)
{

    // Creating an auxiliary matrix to
    // store elements of the
    // multiplication matrix
    var mul = Array(3).fill(0).map(x => Array(3).fill(0));
    for (i = 0; i < 3; i++)
    {
        for (j = 0; j < 3; j++)
        {
            mul[i][j] = 0;
            for (k = 0; k < 3; k++)
                mul[i][j] += a[i][k]
                            * b[k][j];
        }
    }

    // storing the multiplication
    // result in a
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)

            // Updating our matrix
            a[i][j] = mul[i][j];
}

// Function to compute F raise to
// power n-2.
function power(F , n)
{
    var M = [[1, 1, 1], [1, 0, 0],
                           [0, 1, 0]];

    // Multiply it with initial values
    // i.e with F(0) = 0, F(1) = 1,
    // F(2) = 1
    if (n == 1)
        return F[0][0] + F[0][1];

    power(F, parseInt(n / 2));

    multiply(F, F);

    if (n % 2 != 0)
        multiply(F, M);

    // Multiply it with initial values
    // i.e with F(0) = 0, F(1) = 1,
    // F(2) = 1
    return F[0][0] + F[0][1] ;
}

// Return n'th term of a series defined
// using below recurrence relation.
// f(n) is defined as
// f(n) = f(n-1) + f(n-2) + f(n-3), n>=3
// Base Cases :
// f(0) = 0, f(1) = 1, f(2) = 1
function findNthTerm(n)
{
    var F = [[1, 1, 1], [1, 0, 0],
                              [0, 1, 0]] ;

    return power(F, n-2);
}

    // Driver code
    var n = 5;
    document.write("F(5) is "
                       + findNthTerm(n));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
F(5) is 7
```

**时间复杂度:**O(logN)
T3】辅助空间: O(logN)
本文由 **Abhiraj Smit** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息
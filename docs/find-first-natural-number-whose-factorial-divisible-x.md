# 求第一个阶乘可被 x 整除的自然数

> 原文:[https://www . geeksforgeeks . org/find-first-自然数-其阶乘可除-x/](https://www.geeksforgeeks.org/find-first-natural-number-whose-factorial-divisible-x/)

给定一个数 x，任务是找到阶乘可被 x 整除的第一个自然数 I。
**示例:**

```
Input  : x = 10
Output : 5
5 is the smallest number such that 
(5!) % 10 = 0

Input  : x = 16
Output : 6
6 is the smallest number such that 
(6!) % 16 = 0
```

一个**简单的解决方案**是从 1 迭代到 x-1，对于每个数字，我检查我是否！可被 x 整除

## C++

```
// A simple C++ program to find first natural
// number whose factorial divides x.
#include <bits/stdc++.h>
using namespace std;

// Returns first number whose factorial
// divides x.
int firstFactorialDivisibleNumber(int x)
{
    int i = 1; // Result
    int fact = 1;
    for (i = 1; i < x; i++) {
        fact = fact * i;
        if (fact % x == 0)
            break;
    }

    return i;
}

// Driver code
int main(void)
{
    int x = 16;
    cout << firstFactorialDivisibleNumber(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to find first natural
// number whose factorial divides x
class GFG {

    // Returns first number whose factorial
    // divides x.
    static int firstFactorialDivisibleNumber(int x)
    {
        int i = 1; // Result
        int fact = 1;
        for (i = 1; i < x; i++) {
            fact = fact * i;
            if (fact % x == 0)
                break;
        }

        return i;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 16;
        System.out.print(firstFactorialDivisibleNumber(x));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# A simple python program to find
# first natural number whose
# factorial divides x.

# Returns first number whose
# factorial divides x.
def firstFactorialDivisibleNumber(x):
    i = 1; # Result
    fact = 1;
    for i in range(1, x):
        fact = fact * i
        if (fact % x == 0):
            break
    return i

# Driver code
x = 16
print(firstFactorialDivisibleNumber(x))

# This code is contributed
# by 29AjayKumar
```

## C#

```
// A simple C# program to find first natural
// number whose factorial divides x
using System;

class GFG {

    // Returns first number whose factorial
    // divides x.
    static int firstFactorialDivisibleNumber(int x)
    {
        int i = 1; // Result
        int fact = 1;
        for (i = 1; i < x; i++) {
            fact = fact * i;
            if (fact % x == 0)
                break;
        }

        return i;
    }

    // Driver code
    public static void Main()
    {
        int x = 16;

        Console.Write(
            firstFactorialDivisibleNumber(x));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP program to find
// first natural number whose
// factorial divides x.

// Returns first number whose
// factorial divides x.
function firstFactorialDivisibleNumber($x)
{
    // Result
    $i = 1;
    $fact = 1;
    for ($i = 1; $i < $x; $i++)
    {
        $fact = $fact * $i;
        if ($fact % $x == 0)
            break;
    }

    return $i;
}

// Driver code
$x = 16;
echo(firstFactorialDivisibleNumber($x));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to find first natural
// number whose factorial divides x.

// Returns first number whose factorial
// divides x.
function firstFactorialDivisibleNumber(x)
{
    var i = 1; // Result
    var fact = 1;
    for (i = 1; i < x; i++)
    {
        fact = fact * i;
        if (fact % x == 0)
            break;
    }

    return i;
}

// Driver code
var x = 16;
document.write(firstFactorialDivisibleNumber(x));

// This code is contributed by noob2000.
</script>
```

**输出:**

```
6
```

如果我们采用这种天真的方法，我们不会超过 20 岁！或者 21 岁！(long long int 将有其上限)。
一个**更好的解决方案**避免溢出。该解决方案基于以下观察。

*   如果我！能被 x 整除，那么(i+1)！，(i+2)！，…也能被 x 整除。
*   对于一个数 x，所有的阶乘 I！当 i >= x 时，可被 x 整除。
*   如果一个数 x 是质数，那么 x 以下的阶乘都不能除它，因为 x 不能与较小的数相乘。

下面是算法

```
1) Run a loop for i = 1 to n-1

   a) Remove common factors
      new_x /= gcd(i, new_x);

   b) Check if we found first i.
      if (new_x == 1)
          break;

2) Return i
```

以下是上述思路的实现:

## C++

```
// C++ program to find first natural number
// whose factorial divides x.
#include <bits/stdc++.h>
using namespace std;

// GCD function to compute the greatest
// divisor among a and b
int gcd(int a, int b)
{
    if ((a % b) == 0)
        return b;
    return gcd(b, a % b);
}

// Returns first number whose factorial
// divides x.
int firstFactorialDivisibleNumber(int x)
{
    int i = 1; // Result
    int new_x = x;

    for (i = 1; i < x; i++) {
        // Remove common factors
        new_x /= gcd(i, new_x);

        // We found first i.
        if (new_x == 1)
            break;
    }
    return i;
}

// Driver code
int main(void)
{
    int x = 16;
    cout << firstFactorialDivisibleNumber(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find first
// natural number whose factorial divides x.
class GFG {

    // GCD function to compute the greatest
    // divisor among a and b
    static int gcd(int a, int b)
    {
        if ((a % b) == 0)
            return b;
        return gcd(b, a % b);
    }

    // Returns first number whose factorial
    // divides x.
    static int firstFactorialDivisibleNumber(int x)
    {
        int i = 1; // Result
        int new_x = x;

        for (i = 1; i < x; i++) {

            // Remove common factors
            new_x /= gcd(i, new_x);

            // We found first i.
            if (new_x == 1)
                break;
        }
        return i;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 16;
        System.out.print(firstFactorialDivisibleNumber(x));
    }
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```

#  Python3 program to find first natural number
#  whose factorial divides x.

#  GCD function to compute the greatest
#  divisor among a and b
def gcd(a,  b):
    if ((a % b) == 0):
        return b
    return gcd(b, a % b)

#  Returns first number whose factorial
#  divides x.
def firstFactorialDivisibleNumber(x):
    i = 1 #  Result
    new_x = x

    for i in range(1,x):
        #  Remove common factors
        new_x /= gcd(i, new_x)

        #  We found first i.
        if (new_x == 1):
            break
    return i

#  Driver code
def main():
    x = 16
    print(firstFactorialDivisibleNumber(x))

if __name__ == '__main__':
    main()

# This code is contributed by 29AjayKumar
```

## C#

```
// Efficient C# program to find first
// natural number whose factorial
// divides x.
using System;

class GFG {

    // GCD function to compute the
    // greatest divisor among a
    // and b
    static int gcd(int a, int b)
    {
        if ((a % b) == 0)
            return b;
        return gcd(b, a % b);
    }

    // Returns first number whose
    // factorial divides x.
    static int firstFactorialDivisibleNumber(
                                        int x)
    {
        int i = 1; // Result
        int new_x = x;

        for (i = 1; i < x; i++) {

            // Remove common factors
            new_x /= gcd(i, new_x);

            // We found first i.
            if (new_x == 1)
                break;
        }

        return i;
    }

    // Driver code
    public static void Main()
    {
        int x = 16;
        Console.Write(
            firstFactorialDivisibleNumber(x));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find first
// natural number whose
// factorial divides x.

// GCD function to compute the
// greatest divisor among a and b
function gcd($a, $b)
{
    if (($a % $b) == 0)
        return $b;
    return gcd($b, $a % $b);
}

// Returns first number
// whose factorial divides x.
function firstFactorialDivisibleNumber($x)
{
    // Result
    $i = 1;
    $new_x = $x;

    for ($i = 1; $i < $x; $i++)
    {
        // Remove common factors
        $new_x /= gcd($i, $new_x);

        // We found first i.
        if ($new_x == 1)
            break;
    }
    return $i;
}

// Driver code
$x = 16;
echo(firstFactorialDivisibleNumber($x));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Efficient Javascript program to find first
    // natural number whose factorial
    // divides x.

    // GCD function to compute the
    // greatest divisor among a
    // and b
    function gcd(a, b)
    {
        if ((a % b) == 0)
            return b;
        return gcd(b, a % b);
    }

    // Returns first number whose
    // factorial divides x.
    function firstFactorialDivisibleNumber(x)
    {
        let i = 1; // Result
        let new_x = x;

        for (i = 1; i < x; i++)
        {

            // Remove common factors
            new_x = parseInt(new_x / gcd(i, new_x), 10);

            // We found first i.
            if (new_x == 1)
                break;
        }
        return i;
    }

    let x = 16;
    document.write(firstFactorialDivisibleNumber(x));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
6
```

**使用 boost 库的另一种方法【T1:
**(感谢 ajay0007 贡献了这种方法)**
这里我们使用 boost 库来高效地计算阶乘的值。
先决条件:[助推-多精度-库](https://www.geeksforgeeks.org/factorial-large-number-using-boost-multiprecision-library/)** 

## C++

```
// A cpp program for finding
// the Special Factorial Number
#include <bits/stdc++.h>
#include <boost/multiprecision/cpp_int.hpp>

using boost::multiprecision::cpp_int;
using namespace std;

// function for calculating factorial
cpp_int fact(int n)
{
    cpp_int num = 1;

    for (int i = 1; i <= n; i++)
        num = num * i;

    return num;
}

// function for check Special_Factorial_Number
int Special_Factorial_Number(int k)
{

    for(int i = 1 ; i <= k ; i++ )
    {
        // call fact function and the
        // Modulo with k and check
        // if condition is TRUE then return i
        if ( ( fact (i) % k ) == 0 )
        {
            return i;
        }
    }
}

//driver function
int main()
{
    // taking input
    int k = 16;

    cout<<Special_Factorial_Number(k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding
// the Special Factorial Number
public class GFG {

// function for calculating factorial
    static int fact(int n) {
        int num = 1;

        for (int i = 1; i <= n; i++) {
            num = num * i;
        }

        return num;
    }

// function for check Special_Factorial_Number
    static int Special_Factorial_Number(int k) {

        for (int i = 1; i <= k; i++) {
            // call fact function and the
            // Modulo with k and check
            // if condition is TRUE then return i
            if (fact(i) % k == 0) {
                return i;
            }
        }
        return 0;
    }

//driver function
    public static void main(String[] args) {
        // taking input
        int k = 16;
        System.out.println(Special_Factorial_Number(k));

    }
}

/*This code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python 3 program for finding
# the Special Factorial Number

# function for calculating factorial
def fact( n):
    num = 1
    for i in range(1, n + 1):
        num = num * i
    return num

# function for check Special_Factorial_Number
def Special_Factorial_Number(k):

    for i in range(1, k + 1):

        # call fact function and the
        # Modulo with k and check
        # if condition is TRUE then return i
        if (fact(i) % k == 0):
            return i
    return 0

# Driver Code
if __name__ == '__main__':

    # taking input
    k = 16
    print(Special_Factorial_Number(k))

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for finding
// the Special Factorial Number
using System;
public class GFG{

// function for calculating factorial
    static int fact(int n) {
        int num = 1;

        for (int i = 1; i <= n; i++) {
            num = num * i;
        }

        return num;
    }

// function for check Special_Factorial_Number
    static int Special_Factorial_Number(int k) {

        for (int i = 1; i <= k; i++) {
            // call fact function and the
            // Modulo with k and check
            // if condition is TRUE then return i
            if (fact(i) % k == 0) {
                return i;
            }
        }
        return 0;
    }

//driver function
    public static void Main() {
        // taking input
        int k = 16;
        Console.WriteLine(Special_Factorial_Number(k));

    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding
// the Special Factorial Number

// function for calculating
// factorial
function fact($n)
{
    $num = 1;

    for ($i = 1; $i <= $n; $i++)
        $num = $num * $i;

    return $num;
}

// function for check
// Special_Factorial_Number
function Special_Factorial_Number($k)
{

    for($i = 1 ; $i <= $k ; $i++ )
    {

        // call fact function and the
        // Modulo with k and check
        // if condition is TRUE
        // then return i
        if (( fact ($i) % $k ) == 0 )
        {
            return $i;
        }
    }
}

    // Driver Code
    $k = 16;
    echo Special_Factorial_Number($k);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program for finding the Special Factorial Number

    // function for calculating factorial
    function fact(n) {
        let num = 1;

        for (let i = 1; i <= n; i++) {
            num = num * i;
        }

        return num;
    }

    // function for check Special_Factorial_Number
    function Special_Factorial_Number(k) {

        for (let i = 1; i <= k; i++) {
            // call fact function and the
            // Modulo with k and check
            // if condition is TRUE then return i
            if (fact(i) % k == 0) {
                return i;
            }
        }
        return 0;
    }

    // taking input
    let k = 16;
    document.write(Special_Factorial_Number(k));

</script>
```

**输出:**

```
6
```

本文由 **Shubham Gupta** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
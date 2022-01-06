# 给定一个序列的 F(i)和 F(j)时求 F(n)

> 原文:[https://www . geesforgeks . org/find-fn-when-fi-and-FJ-of-a-sequence-are-given/](https://www.geeksforgeeks.org/find-fn-when-fi-and-fj-of-a-sequence-are-given/)

给定五个整数 **i，F <sub>i</sub> ，j，F <sub>j</sub> 和 N** 。其中 **F <sub>i</sub>** 和 **F <sub>j</sub>** 是**I**和 **j <sup>第</sup>** 项，其顺序遵循[斐波那契循环](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)即**F<sub>N</sub>= F<sub>N–1</sub>+F<sub>任务是找到原序列的 **N <sup>第</sup>** 项。
**举例:**</sub>** 

> **输入:** i = 3，F <sub>3</sub> = 5，j = -1，F <sub>-1</sub> = 4，N = 5
> **输出:** 12
> *斐波那契数列可以用已知值重构:*
> *…，F <sub>-1</sub> = 4，F <sub>0</sub> = -1，F <sub>1</sub> = 3 F <sub>5</sub> = 12、…*
> **输入:** i = 0、F <sub>0</sub> = 1、j = 1、F <sub>1</sub> = 4、N = -2
> **输出:** -2

**方法:**注意，如果斐波那契数列的两个连续项是已知的，那么 **N <sup>第</sup>T5】项可以很容易地确定。假设 **i < j** ，根据斐波那契条件:** 

> 【T0 和+1】= 1 * 2 和+1、+3、+ 0*F、5、
> T7 和+2、= 1*F 和+9 t35<sub>和+5</sub>= t38 和+4 和+3【41】= 5 * f】和+1+3 *之间的关系 -好吧-好吧-好吧" T47 "然后是" T48 "

注意，上述方程组中 **F <sub>i+1</sub>** 和 **F <sub>i</sub>** 的系数不过是[标准斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的项。
所以，考虑标准斐波那契数列即 *f <sub>0</sub> = 0，f <sub>1</sub> = 1，f <sub>2</sub> = 1，f <sub>3</sub> = 2，f <sub>4</sub> = 3，…*；我们可以将上述方程组(对于 k > 0)归纳为:

> F<sub>I+k</sub>= F<sub>k</sub>* F<sub>I+1</sub>+F<sub>k-1</sub>* F<sub>I</sub>**……(1)**

现在考虑一下，

> k = j-I**……(2)**

现在，代入 **eq。②**中的**情商。①**，我们得到:

> F<sub>j</sub>= F<sub>j-I</sub>* F<sub>I+1</sub>+F<sub>j-I-1</sub>* F<sub>I</sub>

因此，我们可以根据已知的**F<sub>I</sub>T7】和**F<sub>j</sub>T11】的值来计算**F<sub>I+1</sub>T3。既然知道了两个连续的顺序项 **F** ，就可以轻松重构 **F** 并确定 **F <sub>N</sub>** 的值。
以下是上述办法的实施:****** 

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>

using namespace std;

// Function to calculate kth Fibonacci number
// in the standard Fibonacci sequence
int fibonacci(int k)
{
    int a = 0, b = 1, c = 0;
    if( k == 0)
        return a;
    if (k == 1)
        return b;
    for(int i = 2; i < k + 1; i++)
    {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}

// Function to determine the value of F(n)
int determineFn(int i, int Fi, int j, int Fj, int n)
{
    if (j < i)
    {
        swap(i, j);
        swap(Fi, Fj);
    }

    // Find the value of F(i + 1)
    // from F(i) and F(j)
    int Fi1 = (Fj - fibonacci(j - i - 1) * Fi) /
                    fibonacci(j - i);

    // When n is equal to i
    int Fn = 0;
    if (n == i)
        Fn = Fi;

    // When n is greater than i
    else if (n > i)
    {
        int b = Fi;
        Fn = Fi1;
        n = n - 1;
        while (n != i)
        {
            n = n - 1;
            int a = b;
            b = Fn;
            Fn = a + b;
        }
    }

    // When n is smaller than i
    else
    {
        int a = Fi;
        int b = Fi1;
        while (n != i)
        {
            n = n + 1;
            Fn = b - a;
            b = a;
            a = Fn;
        }
    }
    return Fn;
}

// Driver code
int main()
{
    int i = 3;
    int Fi = 5;
    int j = -1;
    int Fj = 4;
    int n = 5;
    cout << (determineFn(i, Fi, j, Fj, n));
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to calculate kth Fibonacci number
    // in the standard Fibonacci sequence
    static int fibonacci(int k)
    {
        int a = 0, b = 1, c = 0;
        if (k == 0)
            return a;
        if (k == 1)
            return b;
        for (int i = 2; i < k + 1; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }
        return c;
    }

    // Function to determine the value of F(n)
    static int determineFn(int i, int Fi,      
                           int j, int Fj, int n)
    {
        if (j < i)
        {

            // Swap i, j
            i = i + j;
            j = i - j;
            i = i - j;

            // swap Fi, Fj
            Fi = Fi + Fj;
            Fj = Fi - Fj;
            Fi = Fi - Fj;
        }

        // Find the value of F(i + 1)
        // from F(i) and F(j)
        int Fi1 = (Fj - fibonacci(j - i - 1) * Fi) /
                        fibonacci(j - i);

        // When n is equal to i
        int Fn = 0;
        if (n == i)
            Fn = Fi;

        // When n is greater than i
        else if (n > i)
        {
            int b = Fi;
            Fn = Fi1;
            n = n - 1;
            while (n != i)
            {
                n = n - 1;
                int a = b;
                b = Fn;
                Fn = a + b;
            }
        }

        // When n is smaller than i
        else
        {
            int a = Fi;
            int b = Fi1;
            while (n != i)
            {
                n = n + 1;
                Fn = b - a;
                b = a;
                a = Fn;
            }
        }
        return Fn;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int i = 3;
        int Fi = 5;
        int j = -1;
        int Fj = 4;
        int n = 5;
        System.out.println(determineFn(i, Fi, j, Fj, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to calculate kth Fibonacci number
# in the standard Fibonacci sequence
def fibonacci(k):
    a = 0
    b = 1
    if k == 0:
        return a
    if k == 1:
        return b
    for i in range(2, k + 1):
        c = a + b
        a = b
        b = c
    return c

# Function to determine
# the value of F(n)
def determineFn(i, Fi, j, Fj, n):
    if j<i:
        i, j = j, i
        Fi, Fj = Fj, Fi

    # Find the value of F(i + 1)
    # from F(i) and F(j)
    Fi1 = (Fj - fibonacci(j-i-1)*Fi)\
                      //fibonacci(j-i)

    # When n is equal to i
    if n == i:
        Fn = Fi

    # When n is greater than i
    elif n>i:
        b = Fi
        Fn = Fi1
        n = n - 1
        while n != i:
            n = n - 1
            a = b
            b = Fn
            Fn = a + b

    # When n is smaller than i
    else:
        a = Fi
        b = Fi1
        while n != i:
            n = n + 1
            Fn = b - a
            b = a
            a = Fn
    return Fn

# Driver code
if __name__ == '__main__':
    i = 3
    Fi = 5
    j = -1
    Fj = 4
    n = 5
    print(determineFn(i, Fi, j, Fj, n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to calculate kth Fibonacci number
    // in the standard Fibonacci sequence
    static int fibonacci(int k)
    {
        int a = 0, b = 1, c = 0;
        if (k == 0)
            return a;
        if (k == 1)
            return b;
        for (int i = 2; i < k + 1; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }
        return c;
    }

    // Function to determine the value of F(n)
    static int determineFn(int i, int Fi,    
                           int j, int Fj, int n)
    {
        if (j < i)
        {

            // Swap i, j
            i = i + j;
            j = i - j;
            i = i - j;

            // swap Fi, Fj
            Fi = Fi + Fj;
            Fj = Fi - Fj;
            Fi = Fi - Fj;
        }

        // Find the value of F(i + 1)
        // from F(i) and F(j)
        int Fi1 = (Fj - fibonacci(j - i - 1) * Fi) /
                        fibonacci(j - i);

        // When n is equal to i
        int Fn = 0;
        if (n == i)
            Fn = Fi;

        // When n is greater than i
        else if (n > i)
        {
            int b = Fi;
            Fn = Fi1;
            n = n - 1;
            while (n != i)
            {
                n = n - 1;
                int a = b;
                b = Fn;
                Fn = a + b;
            }
        }

        // When n is smaller than i
        else
        {
            int a = Fi;
            int b = Fi1;
            while (n != i)
            {
                n = n + 1;
                Fn = b - a;
                b = a;
                a = Fn;
            }
        }
        return Fn;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int i = 3;
        int Fi = 5;
        int j = -1;
        int Fj = 4;
        int n = 5;
        Console.WriteLine(determineFn(i, Fi, j, Fj, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to calculate kth Fibonacci number
// in the standard Fibonacci sequence
function fibonacci(k)
{
    let a = 0, b = 1, c = 0;
    if( k == 0)
        return a;
    if (k == 1)
        return b;
    for(let i = 2; i < k + 1; i++)
    {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}

// Function to determine the value of F(n)
function determineFn(i, Fi, j, Fj, n)
{
    if (j < i)
    {
        // Swap i, j
        i = i + j;
        j = i - j;
        i = i - j;

        // swap Fi, Fj
        Fi = Fi + Fj;
        Fj = Fi - Fj;
        Fi = Fi - Fj;
    }

    // Find the value of F(i + 1)
    // from F(i) and F(j)
    let Fi1 = parseInt((Fj - fibonacci(j - i - 1) * Fi) /
                    fibonacci(j - i));

    // When n is equal to i
    let Fn = 0;
    if (n == i)
        Fn = Fi;

    // When n is greater than i
    else if (n > i)
    {
        let b = Fi;
        Fn = Fi1;
        n = n - 1;
        while (n != i)
        {
            n = n - 1;
            let a = b;
            b = Fn;
            Fn = a + b;
        }
    }

    // When n is smaller than i
    else
    {
        let a = Fi;
        let b = Fi1;
        while (n != i)
        {
            n = n + 1;
            Fn = b - a;
            b = a;
            a = Fn;
        }
    }
    return Fn;
}

// Driver code
    let i = 3;
    let Fi = 5;
    let j = -1;
    let Fj = 4;
    let n = 5;
    document.write(determineFn(i, Fi, j, Fj, n));

</script>
```

**Output:** 

```
12
```
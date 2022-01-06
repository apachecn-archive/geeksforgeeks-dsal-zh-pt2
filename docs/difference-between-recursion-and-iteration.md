# 递归和迭代的区别

> 原文:[https://www . geesforgeks . org/递归和迭代的区别/](https://www.geeksforgeeks.org/difference-between-recursion-and-iteration/)

当实体调用自己时，程序被称为递归程序。当存在循环(或重复)时，程序被称为迭代程序。
**例:**程序求一个数的阶乘

## C++

```
// C++ program to find factorial of given number
#include<bits/stdc++.h>
using namespace std;

// ----- Recursion -----
// method to find factorial of given number
int factorialUsingRecursion(int n)
{
    if (n == 0)
        return 1;

    // recursion call
    return n * factorialUsingRecursion(n - 1);
}

// ----- Iteration -----
// Method to find the factorial of a given number
int factorialUsingIteration(int n)
{
    int res = 1, i;

    // using iteration
    for (i = 2; i <= n; i++)
        res *= i;

    return res;
}

// Driver method
int main()
{
    int num = 5;
    cout << "Factorial of " << num <<
            " using Recursion is: " <<
            factorialUsingRecursion(5) << endl;

    cout << "Factorial of " << num <<
            " using Iteration is: " <<
            factorialUsingIteration(5);

    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find factorial of given number
class GFG {

    // ----- Recursion -----
    // method to find factorial of given number
    static int factorialUsingRecursion(int n)
    {
        if (n == 0)
            return 1;

        // recursion call
        return n * factorialUsingRecursion(n - 1);
    }

    // ----- Iteration -----
    // Method to find the factorial of a given number
    static int factorialUsingIteration(int n)
    {
        int res = 1, i;

        // using iteration
        for (i = 2; i <= n; i++)
            res *= i;

        return res;
    }

    // Driver method
    public static void main(String[] args)
    {
        int num = 5;
        System.out.println("Factorial of " + num
                           + " using Recursion is: "
                           + factorialUsingRecursion(5));

        System.out.println("Factorial of " + num
                           + " using Iteration is: "
                           + factorialUsingIteration(5));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find factorial of given number

# ----- Recursion -----
# method to find factorial of given number
def factorialUsingRecursion(n):
    if (n == 0):
        return 1;

    # recursion call
    return n * factorialUsingRecursion(n - 1);

# ----- Iteration -----
# Method to find the factorial of a given number
def factorialUsingIteration(n):
    res = 1;

    # using iteration
    for i in range(2, n + 1):
        res *= i;

    return res;

# Driver method
num = 5;
print("Factorial of",num,"using Recursion is:",
                    factorialUsingRecursion(5));

print("Factorial of",num,"using Iteration is:",
                    factorialUsingIteration(5));

# This code is contributed by mits
```

## C#

```
// C# program to find factorial of
// given number
using System;

class GFG
{

    // ----- Recursion -----
    // method to find factorial of
    // given number
    static int factorialUsingRecursion(int n)
    {
        if (n == 0)
            return 1;

        // recursion call
        return n * factorialUsingRecursion(n - 1);
    }

    // ----- Iteration -----
    // Method to find the factorial of
    // a given number
    static int factorialUsingIteration(int n)
    {
        int res = 1, i;

        // using iteration
        for (i = 2; i <= n; i++)
            res *= i;

        return res;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int num = 5;
        Console.WriteLine("Factorial of " + num +
                          " using Recursion is: " +
                          factorialUsingRecursion(5));

        Console.WriteLine("Factorial of " + num +
                          " using Iteration is: " +
                          factorialUsingIteration(5));
    }
}

// This code has been contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find factorial of given number

    // ----- Recursion -----
    // method to find factorial of given number
    function factorialUsingRecursion($n)
    {
        if ($n == 0)
            return 1;

        // recursion call
        return $n * factorialUsingRecursion($n - 1);
    }

    // ----- Iteration -----
    // Method to find the factorial of a given number
    function factorialUsingIteration($n)
    {
        $res = 1;

        // using iteration
        for ($i = 2; $i <= $n; $i++)
            $res *= $i;

        return $res;
    }

    // Driver method
        $num = 5;
        print("Factorial of ".$num." using Recursion is: ".
                            factorialUsingRecursion(5)."\n");

        print("Factorial of ".$num." using Iteration is: ".
                            factorialUsingIteration(5)."\n");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find factorial of given number
// ----- Recursion -----
// method to find factorial of given number
function factorialUsingRecursion(n)
    {
        if (n == 0)
            return 1;

        // recursion call
        return n * factorialUsingRecursion(n - 1);
    }

    // ----- Iteration -----
    // Method to find the factorial of a given number
    function factorialUsingIteration(n)
    {
        var res = 1, i;

        // using iteration
        for (i = 2; i <= n; i++)
            res *= i;

        return res;
    }

    // Driver method
        var num = 5;
        document.write("Factorial of " + num
                           + " using Recursion is: "
                           + factorialUsingRecursion(5)+"<br>");

        document.write("Factorial of " + num
                           + " using Iteration is: "
                           + factorialUsingIteration(5));

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
Factorial of 5 using Recursion is: 120
Factorial of 5 using Iteration is: 120
```

**下面是详细的例子来说明两者的区别:**

1.  **时间复杂度:**求递归的时间复杂度比求迭代的时间复杂度更难。
    *   **递归**:递归的时间复杂度可以通过根据前面的调用找到第 n 次递归调用的值来找到。因此，根据基本情况找到目的地情况，并根据基本情况求解，给了我们递归方程时间复杂性的概念。详情请见[解决复发](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)。

    *   **迭代**:迭代的时间复杂度可以通过求循环内重复的循环数来找到。

2.  **用法:**这两种技术的使用是时间复杂度和代码大小之间的权衡。如果时间复杂度是焦点，并且递归调用的数量会很大，那么最好使用迭代。然而，如果时间复杂性不是问题，而代码简短才是问题，递归将是解决问题的方法。
    *   **递归**:递归涉及再次调用同一个函数，因此代码长度非常小。然而，正如我们在分析中看到的，当有相当多的递归调用时，递归的时间复杂度可能会变成指数级。因此，递归的使用在较短的代码中是有利的，但是时间复杂度更高。

    *   **迭代**:迭代是一段代码的重复。这涉及到更大规模的代码，但时间复杂度通常比递归要低。

3.  **开销:**与迭代相比，递归有大量开销。
    *   **递归**:递归有重复函数调用的开销，即由于重复调用同一个函数，代码的时间复杂度增加了数倍。

    *   **迭代**:迭代不涉及任何这样的开销。

4.  **无限重复:**递归中的无限重复会导致 CPU 崩溃，但在迭代中，当内存耗尽时就会停止。
    *   **递归**:在递归中，由于在指定基本条件时的一些错误，可能会发生无限递归调用，这种情况永远不会变成假，会不断调用函数，这可能会导致系统 CPU 崩溃。

    *   **迭代**:由于迭代器赋值或者增量错误，或者终止条件错误导致的无限迭代，会导致无限循环，可能导致系统错误，也可能不会导致系统错误，但一定会让程序执行停止。

<figure class="table">

| 财产 | 递归 | 循环 |
| --- | --- | --- |
| **定义** | 函数调用自己。 | 重复执行的一组指令。 |
| **应用** | 为了功能。 | 用于循环。 |
| **终止** | 通过基本案例，在那里不会有函数调用。 | 当迭代器的终止条件不再满足时。 |
| 用法 | 当代码大小需要很小，并且时间复杂度不是问题时使用。 | 当时间复杂度需要与扩展的代码大小相平衡时使用。 |
| **代码大小** | 较小的代码大小 | 更大的代码大小。 |
| **时间复杂度** | 非常高(通常是指数级)的时间复杂度。 | 时间复杂度相对较低(一般为多项式对数)。 |

</figure>
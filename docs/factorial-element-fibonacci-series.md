# 斐波那契数列中每个元素的阶乘

> 原文:[https://www . geesforgeks . org/factorial-element-Fibonacci-series/](https://www.geeksforgeeks.org/factorial-element-fibonacci-series/)

给定上限，打印小于上限的所有[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的阶乘。
**例:**

```
Input : limit = 20
Output : 1 1 1 2 6 120 40320 6227020800
Explanation : 
Fibonacci series in this range is 0, 1, 1, 2, 
3, 5, 8, 13\. Factorials of these numbers are 
output.

Input : 50
Output : 1 1 1 2 6 120 40320 6227020800
         51090942171709440000 
         295232799039604140847618609643520000000
```

我们知道简单的阶乘计算很快会导致溢出。因此，我们使用[大数阶乘](https://www.geeksforgeeks.org/factorial-large-number/)。
一个**简单的解决方案**是逐个生成所有斐波那契数，并使用[大数阶乘](https://www.geeksforgeeks.org/factorial-large-number/)
中讨论的方法计算每个生成数的阶乘**高效的解决方案**是基于斐波那契数按顺序递增的事实。所以我们用之前生成的阶乘来计算下一个阶乘。

## C++

```
// CPP program to find factorial of each element
// of Fibonacci series
#include <iostream>
using namespace std;

// Maximum number of digits in output
#define MAX 500

// Finds and print factorial of n using
// factorial of prev (stored in prevFact[
// 0...size-1]
void factorial(int prevFact[], int &size,
                         int prev, int n);

// Prints factorials of all fibonacci
// numbers smaller than given limit.
void printfibFactorials(int limit)
{
   if (limit < 1)
      return;

   // Initialize first three Fibonacci
   // numbers and print factorials of
   // first two numbers.
   int a = 1, b = 1, c = 2;
   cout << a << " " << b << " ";

   // prevFact[] stores factorial of
   // previous fibonacci number
   int prevFact[MAX];
   prevFact[0] = 1;

   // Size is current size of prevFact[]
   int size = 1;

   // Standard Fibonacci number loop
   while (c < limit)
   {
       factorial(prevFact, size, b, c);
       a = b;
       b = c;
       c = a + b;
   }
}

// Please refer below article for details of
// below two functions.
// https://www.geeksforgeeks.org/factorial-large-number/

// Function used to find factorial
int multiply(int x, int prevFact[], int size)
{
    int carry = 0;
    for (int i = 0; i < size; i++) {
        int prod = prevFact[i] * x + carry;
        prevFact[i] = prod % 10;
        carry = prod / 10;
    }

    // Put carry in res and increase
    // result size
    while (carry) {
        prevFact[size] = carry % 10;
        carry = carry / 10;
        size++;
    }
    return size;
}

// Finds factorial of n using factorial
// "prev" stored in prevFact[]. size is
// size of prevFact[]
void factorial(int prevFact[], int &size,
                         int prev, int n)
{
   for (int x = prev+1; x <= n; x++)
       size = multiply(x, prevFact, size);

    for (int i = size - 1; i >= 0; i--)
        cout << prevFact[i];
    cout << " ";
}

// Driver function
int main()
{
    int limit = 20;
    printfibFactorials(limit);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// factorial of each element
// of Fibonacci series
import java.io.*;

class GFG
{    
    // Maximum number of
    // digits in output
    static int MAX = 500;
    static int size = 1;

    // Finds and print factorial
    // of n using factorial of
    // prev (stored in prevFact[
    // 0...size-1]
    // Finds factorial of n
    // using factorial "prev"
    // stored in prevFact[]. size
    // is size of prevFact[]
    static void factorial(int []prevFact,
                          int prev, int n)
    {
    for (int x = prev + 1;
             x <= n; x++)
        size = multiply(x, prevFact, size);

        for (int i = size - 1;
                 i >= 0; i--)
            System.out.print(prevFact[i]);
        System.out.print(" ");
    }

    // Prints factorials of all
    // fibonacci numbers smaller
    // than given limit.
    static void printfibFactorials(int limit)
    {
        if (limit < 1)
            return;

        // Initialize first three
        // Fibonacci numbers and
        // print factorials of
        // first two numbers.
        int a = 1, b = 1, c = 2;
        System.out.print(a + " " +
                         b + " ");

        // prevFact[] stores factorial
        // of previous fibonacci number
        int []prevFact = new int[MAX];
        prevFact[0] = 1;

        // Standard Fibonacci
        // number loop
        while (c < limit)
        {
            factorial(prevFact, b, c);
            a = b;
            b = c;
            c = a + b;
        }
    }

    // Please refer below
    // article for details of
    // below two functions.
    // https://www.geeksforgeeks.org/factorial-large-number/

    // Function used to
    // find factorial
    static int multiply(int x,
                        int []prevFact,
                        int size)
    {
        int carry = 0;
        for (int i = 0; i < size; i++)
        {
            int prod = prevFact[i] *
                        x + carry;
            prevFact[i] = prod % 10;
            carry = prod / 10;
        }

        // Put carry in
        // res and increase
        // result size
        while (carry != 0)
        {
            prevFact[size] = carry % 10;
            carry = carry / 10;
            size++;
        }
        return size;
    }

    // Driver Code
    public static void main(String args[])
    {
        int limit = 20;
        printfibFactorials(limit);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find
# factorial of each element
# of Fibonacci series

# Maximum number of
# digits in output
MAX = 500
size = 1

# Finds and print factorial
# of n using factorial of
# prev (stored in prevFact[
# 0...size-1]
# Finds factorial of n
# using factorial "prev"
# stored in prevFact[]. size
# is size of prevFact[]
def factorial(prevFact, prev,n) :
    global size
    for x in range((prev + 1), n + 1) :
        size = multiply(x, prevFact, size)

    for i in range((size - 1), -1, -1) :
        print(prevFact[i], end = "")
    print(end = " ")

# Prints factorials of all
# fibonacci numbers smaller
# than given limit.
def printfibFactorials(limit) :
    if (limit < 1) :
        return

    # Initialize first three
    # Fibonacci numbers and
    # print factorials of
    # first two numbers.
    a = 1
    b = 1
    c = 2
    print(a,b , end = " ")

    # prevFact[] stores factorial
    # of previous fibonacci number
    prevFact = [0] * MAX
    prevFact[0] = 1

    # Standard Fibonacci
    # number loop
    while (c < limit) :
        factorial(prevFact, b, c)
        a = b
        b = c
        c = a + b

# Please refer below
# article for details of
# below two functions.
# https://www.geeksforgeeks.org/factorial-large-number/

# Function used to
# find factorial
def multiply(x,prevFact,size) :
    carry = 0
    for i in range(0, size) :
        prod = prevFact[i] *x + carry
        prevFact[i] = prod % 10
        carry = prod // 10

    # Put carry in
    # res and increase
    # result size
    while (carry != 0) :
        prevFact[size] = carry % 10
        carry = carry // 10
        size = size + 1

    return size

# Driver Code
limit = 20
printfibFactorials(limit)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find
// factorial of each element
// of Fibonacci series
using System;

class GFG
{    
    // Maximum number of
    // digits in output
    static int MAX = 500;

    // Finds and print factorial
    // of n using factorial of
    // prev (stored in prevFact[
    // 0...size-1]
    // Finds factorial of n
    // using factorial "prev"
    // stored in prevFact[]. size
    // is size of prevFact[]
    static void factorial(int []prevFact,
                          ref int size,
                          int prev, int n)
    {
    for (int x = prev + 1; x <= n; x++)
        size = multiply(x, prevFact, size);

        for (int i = size - 1; i >= 0; i--)
            Console.Write(prevFact[i]);
        Console.Write(" ");
    }

    // Prints factorials of all fibonacci
    // numbers smaller than given limit.
    static void printfibFactorials(int limit)
    {
    if (limit < 1)
        return;

    // Initialize first three Fibonacci
    // numbers and print factorials of
    // first two numbers.
    int a = 1, b = 1, c = 2;
    Console.Write(a + " " + b + " ");

    // prevFact[] stores factorial of
    // previous fibonacci number
    int []prevFact = new int[MAX];
    prevFact[0] = 1;

    // Size is current size
    // of prevFact[]
    int size = 1;

    // Standard Fibonacci
    // number loop
    while (c < limit)
    {
        factorial(prevFact, ref size, b, c);
        a = b;
        b = c;
        c = a + b;
    }
    }

    // Please refer below
    // article for details of
    // below two functions.
    // https://www.geeksforgeeks.org/factorial-large-number/

    // Function used to find factorial
    static int multiply(int x,
                        int []prevFact, int size)
    {
        int carry = 0;
        for (int i = 0; i < size; i++)
        {
            int prod = prevFact[i] *
                          x + carry;
            prevFact[i] = prod % 10;
            carry = prod / 10;
        }

        // Put carry in
        // res and increase
        // result size
        while (carry != 0)
        {
            prevFact[size] = carry % 10;
            carry = carry / 10;
            size++;
        }
        return size;
    }

    // Driver Code
    static void Main()
    {
        int limit = 20;
        printfibFactorials(limit);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// factorial of each element
// of Fibonacci series

// Maximum number of
// digits in output
$MAX = 500;
$size = 1;
$prevFact = $prevFact =
            array_fill(0, $MAX, 0);

// Finds and print factorial
// of n using factorial of
// prev (stored in prevFact[
// 0...size-1]
// Finds factorial of n
// using factorial "prev"
// stored in prevFact[]. size
// is size of prevFact[]
function factorial($prev, $n)
    {
    global $size, $prevFact;
    for ($x = $prev + 1;
         $x <= $n; $x++)
        $size = multiply($x, $size);

        for ($i = $size - 1;
             $i >= 0; $i--)
            echo $prevFact[$i];
        echo " ";
    }

// Prints factorials of all
// fibonacci numbers smaller
// than given limit.
function printfibFactorials($limit)
    {
        global $MAX, $prevFact;
        if ($limit < 1)
            return;

        // Initialize first three
        // Fibonacci numbers and
        // print factorials of
        // first two numbers.
        $a = 1;
        $b = 1;
        $c = 2;
        echo $a . " " . $b . " ";

        // prevFact[] stores factorial
        // of previous fibonacci number
        $prevFact[0] = 1;

        // Standard Fibonacci
        // number loop
        while ($c < $limit)
        {
            factorial($b, $c);
            $a = $b;
            $b = $c;
            $c = $a + $b;
        }
    }

// Function used to
// find factorial
function multiply($x,$size)
    {
        global $prevFact;
        $carry = 0;
        for ($i = 0;
             $i < $size; $i++)
        {
            $prod = $prevFact[$i] *
                    $x + $carry;
            $prevFact[$i] = $prod % 10;
            $carry = (int)($prod / 10);
        }

        // Put carry in
        // res and increase
        // result size
        while ($carry != 0)
        {
            $prevFact[$size] = $carry % 10;
            $carry = (int)($carry / 10);
            $size++;
        }
        return $size;
    }

// Driver Code
$limit = 20;
printfibFactorials($limit);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// factorial of each element
// of Fibonacci series

    // Maximum number of
    // digits in output
    var MAX = 500;
    var size = 1;

    // Finds and print factorial
    // of n using factorial of
    // prev (stored in prevFact[
    // 0...size-1]
    // Finds factorial of n
    // using factorial "prev"
    // stored in prevFact. size
    // is size of prevFact
    function factorial(prevFact , prev , n) {
        for (x = prev + 1; x <= n; x++)
            size = multiply(x, prevFact, size);

        for (i = size - 1; i >= 0; i--)
            document.write(prevFact[i]);
        document.write(" ");
    }

    // Prints factorials of all
    // fibonacci numbers smaller
    // than given limit.
    function printfibFactorials(limit) {
        if (limit < 1)
            return;

        // Initialize first three
        // Fibonacci numbers and
        // prvar factorials of
        // first two numbers.
        var a = 1, b = 1, c = 2;
        document.write(a + " " + b + " ");

        // prevFact stores factorial
        // of previous fibonacci number
        var prevFact = Array(MAX).fill(0);
        prevFact[0] = 1;

        // Standard Fibonacci
        // number loop
        while (c < limit) {
            factorial(prevFact, b, c);
            a = b;
            b = c;
            c = a + b;
        }
    }

    // Please refer below
    // article for details of
    // below two functions.
    // https://www.geeksforgeeks.org/factorial-large-number/

    // Function used to
    // find factorial
    function multiply(x,  prevFact , size) {
        var carry = 0;
        for (i = 0; i < size; i++) {
            var prod = prevFact[i] * x + carry;
            prevFact[i] = prod % 10;
            carry = parseInt(prod / 10);
        }

        // Put carry in
        // res and increase
        // result size
        while (carry != 0) {
            prevFact[size] = carry % 10;
            carry = parseInt(carry / 10);
            size++;
        }
        return size;
    }

    // Driver Code

        var limit = 20;
        printfibFactorials(limit);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
1 1 2 6 120 40320 6227020800
```
# 数组中的斐波那契数

> 原文:[https://www.geeksforgeeks.org/fibonacci-number-array/](https://www.geeksforgeeks.org/fibonacci-number-array/)

给了我们一个数组，我们的任务是检查数组的元素是否出现在[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)中。如果是，则打印该元素。
**例:**

```
Input : 4, 2, 8, 5, 20, 1, 40, 13, 23
Output : 2 8 5 1 13
Here, Fibonacci series will be 0, 1, 1, 2, 
3, 5, 8, 13, 21, 34, 55\. Numbers that are present 
in array are 2, 8, 5, 1, 13
For 2 -> 5 * 2 * 2  - 4 = 36
36 is a perfect square root of 6.

Input : 4, 7, 6, 25
Output : No Fibonacci number in this array
```

如果(5 * n * n–4)或(5 * n * n + 4)是一个完美的正方形，那么这个数就是斐波那契数列。详情请参考[检查给定的数字是否为斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。
T3】

## C++

```
// CPP program to find Fibonacci series numbers
// in a given array.
#include <bits/stdc++.h>
using namespace std;

// Function to check number is a
// perfect square or not
bool isPerfectSquare(int num)
{
    int n = sqrt(num);
    return (n * n == num);
}

// Function to check if the number
// is in Fibonacci or not
void checkFib(int array[], int n)
{
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (isPerfectSquare(5 * array[i] * array[i] + 4) || isPerfectSquare(5 * array[i] * array[i] - 4)) {
            cout << array[i] << " ";
            count++;
        }
    }
    if (count == 0)
        cout << "None present" << endl;
}

// Driver function
int main()
{
    int array[] = { 4, 2, 8, 5, 20, 1, 40, 13, 23 };
    int n = sizeof(array) / sizeof(array[0]);

    checkFib(array, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Fibonacci series numbers
// in a given array
import java.io.*;
import java.math.*;

class GFG {
    // Function to check number is a
    // perfect square or not
    static boolean isPerfectSquare(int num)
    {
        int n = (int)(Math.sqrt(num));
        return (n * n == num);
    }

    // Function to check if the number
    // is in Fibonacci or not
    static void checkFib(int array[], int n)
    {
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (isPerfectSquare(5 * array[i] * array[i] + 4) || isPerfectSquare(5 * array[i] * array[i] - 4)) {
                System.out.print(array[i] + " ");
                count++;
            }
        }
        if (count == 0)
            System.out.println("None Present");
    }

    // driver program
    public static void main(String[] args)
    {
        int array[] = { 4, 2, 8, 5, 20, 1, 40, 13, 23 };
        int n = array.length;
        checkFib(array, n);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python program to find
# Fibonacci series numbers
# in a given array.

import math

def isPerfectSquare(num):

    n = int(math.sqrt(num))
    return (n * n == num)

# Function to check if the number
# is in Fibonacci or not
def checkFib(array, n):

    count = 0
    for i in range(n):

        if (isPerfectSquare(5 * array[i] * array[i] + 4) or
            isPerfectSquare(5 * array[i] * array[i] - 4)):

            print(array[i], " ", end ="");
            count = count + 1

    if (count == 0):
        print("None present");

# driver code
array = [4, 2, 8, 5, 20, 1, 40, 13, 23]
n = len(array)

checkFib(array, n)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find Fibonacci series
// numbers in a given array
using System;

class GFG {

    // Function to check number is a
    // perfect square or not
    static bool isPerfectSquare(int num)
    {
        int n = (int)(Math.Sqrt(num));
        return (n * n == num);
    }

    // Function to check if the number
    // is in Fibonacci or not
    static void checkFib(int[] array, int n)
    {
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (isPerfectSquare(5 * array[i] * array[i] + 4) ||
                isPerfectSquare(5 * array[i] * array[i] - 4))
            {
                Console.Write(array[i] + " ");
                count++;
            }
        }
        if (count == 0)
            Console.WriteLine("None Present");
    }

    // driver program
    public static void Main()
    {
        int[] array = { 4, 2, 8, 5, 20, 1, 40, 13, 23 };
        int n = array.Length;
        checkFib(array, n);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// Fibonacci series numbers
// in a given array.

// Function to check
// number is a perfect
// square or not
function isPerfectSquare($num)
{
    $n = (int)(sqrt($num));
    return ($n * $n == $num);
}

// Function to check
// if the number is
// in Fibonacci or not
function checkFib($array, $n)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if (isPerfectSquare(5 * $array[$i] *
                                $array[$i] + 4) ||
            isPerfectSquare(5 * $array[$i] *
                                $array[$i] - 4))
        {
            echo $array[$i]." ";
            $count++;
        }
    }
    if ($count == 0)
        echo "None present\n";
}

// Driver Code
$array = array(4, 2, 8, 5, 20,
                1, 40, 13, 23);
$n = sizeof($array);

checkFib($array, $n);

// This code is contributed by mits.

?>
```

## java 描述语言

```
<script>
// Javascript program to find
// Fibonacci series numbers
// in a given array.

// Function to check
// number is a perfect
// square or not
function isPerfectSquare(num)
{
    let n = parseInt(Math.sqrt(num));
    return (n * n == num);
}

// Function to check
// if the number is
// in Fibonacci or not
function checkFib(array, n)
{
    let count = 0;
    for (let i = 0; i < n; i++)
    {
        if (isPerfectSquare(5 * array[i] *
                                array[i] + 4) ||
            isPerfectSquare(5 * array[i] *
                                array[i] - 4))
        {
            document.write(array[i] + " ");
            count++;
        }
    }
    if (count == 0)
        document.write("None present + <br>");
}

// Driver Code
let array = [4, 2, 8, 5, 20,
                1, 40, 13, 23];
let n = array.length;

checkFib(array, n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
2 8 5 1 13
```

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
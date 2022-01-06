# 求一个自然数的所有除数|集合 2

> 原文:[https://www . geeksforgeeks . org/find-自然数集的所有除数-2/](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)

给定一个自然数 n，打印它的所有不同除数。

**示例:**

```
 Input : n = 10       
 Output: 1 2 5 10

 Input:  n = 100
 Output: 1 2 4 5 10 20 25 50 100

 Input:  n = 125
 Output: 1 5 25 125 
```

我们强烈建议将以下文章作为先决条件。
[求一个自然数的所有除数|集合 1](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)
在上面的帖子中，我们已经找到了求 O(sqrt(n))中所有除数的方法。
不过解决方案中还有一个小问题，你能猜到吗？
是的！输出不是我们使用暴力技术得到的有序方式。

**如何按排序顺序打印输出？**
如果我们观察我们得到的输出，我们可以分析除数是以之字形打印的(小的，大的对)。因此，如果我们存储其中的一半，那么我们就可以按排序顺序打印它们。

下面是其实现:

## C++

```
// A O(sqrt(n)) program that prints all divisors
// in sorted order
#include <bits/stdc++.h>
using namespace std;

// function to print the divisors
void printDivisors(int n)
{
    // Vector to store half of the divisors
    vector<int> v;
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {

            // check if divisors are equal
            if (n / i == i)
                printf("%d ", i);
            else {
                printf("%d ", i);

                // push the second divisor in the vector
                v.push_back(n / i);
            }
        }
    }

    // The vector will be printed in reverse
    for (int i = v.size() - 1; i >= 0; i--)
        printf("%d ", v[i]);
}

/* Driver program to test above function */
int main()
{
    printf("The divisors of 100 are: n");
    printDivisors(100);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(sqrt(n)) java program that prints all divisors
// in sorted order

import java.util.Vector;

class Test {
    // method to print the divisors
    static void printDivisors(int n)
    {
        // Vector to store half of the divisors
        Vector<Integer> v = new Vector<>();
        for (int i = 1; i <= Math.sqrt(n); i++) {
            if (n % i == 0) {

                // check if divisors are equal
                if (n / i == i)
                    System.out.printf("%d ", i);
                else {
                    System.out.printf("%d ", i);

                    // push the second divisor in the vector
                    v.add(n / i);
                }
            }
        }

        // The vector will be printed in reverse
        for (int i = v.size() - 1; i >= 0; i--)
            System.out.printf("%d ", v.get(i));
    }

    // Driver method
    public static void main(String args[])
    {
        System.out.println("The divisors of 100 are: ");
        printDivisors(100);
    }
}
```

## 蟒蛇 3

```
# A O(sqrt(n)) java program that prints
# all divisors in sorted order
import math

# Method to print the divisors
def printDivisors(n) :
    list = []

    # List to store half of the divisors
    for i in range(1, int(math.sqrt(n) + 1)) :

        if (n % i == 0) :

            # Check if divisors are equal
            if (n / i == i) :
                print (i, end =" ")
            else :
                # Otherwise print both
                print (i, end =" ")
                list.append(int(n / i))

    # The list will be printed in reverse   
    for i in list[::-1] :
        print (i, end =" ")

# Driver method
print ("The divisors of 100 are: ")
printDivisors(100)

# This code is contributed by Gitanjali
```

## C#

```
// A O(sqrt(n)) C# program that
// prints all divisors in sorted order
using System;

class GFG {

    // method to print the divisors
    static void printDivisors(int n)
    {
        // Vector to store half
        // of the divisors
        int[] v = new int[n];
        int t = 0;
        for (int i = 1;
             i <= Math.Sqrt(n); i++) {
            if (n % i == 0) {

                // check if divisors are equal
                if (n / i == i)
                    Console.Write(i + " ");
                else {
                    Console.Write(i + " ");

                    // push the second divisor
                    // in the vector
                    v[t++] = n / i;
                }
            }
        }

        // The vector will be
        // printed in reverse
        for (int i = t - 1; i >= 0; i--)
            Console.Write(v[i] + " ");
    }

    // Driver Code
    public static void Main()
    {
        Console.Write("The divisors of 100 are: \n");
        printDivisors(100);
    }
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(sqrt(n)) program that
// prints all divisors in
// sorted order

// function to print
// the divisors
function printDivisors($n)
{
    // Vector to store half
    // of the divisors
    $v;
    $t = 0;
    for ($i = 1;
         $i <= (int)sqrt($n); $i++)
    {
        if ($n % $i == 0)
        {
            // check if divisors are equal
            if ((int)$n / $i == $i)
                echo $i . " ";
            else
            {
                echo $i . " ";

                // push the second
                // divisor in the vector
                $v[$t++] = (int)$n / $i;
            }
        }
    }

    // The vector will be
    // printed in reverse
    for ($i = count($v) - 1;
         $i >= 0; $i--)
        echo $v[$i] . " ";
}

// Driver code
echo "The divisors of 100 are: \n";
printDivisors(100);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// A O(sqrt(n)) program that
// prints all divisors in
// sorted order

// function to print
// the divisors
function printDivisors(n)
{
    // Vector to store half
    // of the divisors
    let v = [];
    let t = 0;
    for (let i = 1;
         i <= parseInt(Math.sqrt(n)); i++)
    {
        if (n % i == 0)
        {
            // check if divisors are equal
            if (parseInt(n / i) == i)
                document.write(i + " ");
            else
            {
                document.write(i + " ");

                // push the second
                // divisor in the vector
                v[t++] = parseInt(n / i);
            }
        }
    }

    // The vector will be
    // printed in reverse
    for (let i = v.length - 1;
         i >= 0; i--){
         document.write(v[i] + " ");
    }
}

// Driver code
document.write("The divisors of 100 are: \n");
printDivisors(100);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
The divisors of 100 are: n1 2 4 5 10 20 25 50 100 
```

**时间复杂度:** O(sqrt(n))
**辅助空间:** O(sqrt(n))

**A O(sqrt(n))时间和 O(1)空间解:**

## C++

```
// A O(sqrt(n)) program that prints all divisors
// in sorted order
#include <iostream>
#include <math.h>
using namespace std;

// Function to print the divisors
void printDivisors(int n)
{
    int i;
    for (i = 1; i * i < n; i++) {
        if (n % i == 0)
            cout<<i<<" ";
    }
    if (i - (n / i) == 1) {
        i--;
    }
    for (; i >= 1; i--) {
        if (n % i == 0)
            cout<<n / i<<" ";
    }
}

// Driver code
int main()
{
    cout << "The divisors of 100 are: \n";

    printDivisors(100);

    return 0;
}

// This code is contributed by siteshbiswal
```

## C

```
// A O(sqrt(n)) program that prints all divisors
// in sorted order
#include <stdio.h>
#include <math.h>

// function to print the divisors
void printDivisors(int n)
{ int i;
    for ( i = 1; i*i < n; i++) {
        if (n % i == 0)
            printf("%d ", i);
    }
   if(i-(n/i)==1)
    {
      i--;
    }
    for (; i >= 1; i--) {
        if (n % i == 0)
            printf("%d ", n / i);
    }
}

/* Driver program to test above function */
int main()
{
    printf("The divisors of 100 are: \n");
    printDivisors(100);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(sqrt(n)) program that prints all
// divisors in sorted order
import java.lang.Math;

class GFG{

// Function to print the divisors
public static void printDivisors(int n)
{ int i;
    for( i = 1; i * i < n; i++)
    {
        if (n % i == 0)
            System.out.print(i + " ");
    }
    if(i-(n/i)==1)
    {
      i--;
    }
    for(; i >= 1; i--)
    {
        if (n % i == 0)
            System.out.print(n / i + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    System.out.println("The divisors of 100 are: ");

    printDivisors(100);
}
}

// This code is contributed by Prakash Veer Singh Tomar.
```

## 蟒蛇 3

```
# A O(sqrt(n)) program that prints all divisors
# in sorted order
from math import *

# Function to print the divisors
def printDivisors (n):

    i = 1
    while (i * i < n):
        if (n % i == 0):
            print(i, end = " ")

        i += 1

    for i in range(int(sqrt(n)), 0, -1):
        if (n % i == 0):
            print(n // i, end = " ")

# Driver Code
print("The divisors of 100 are: ")

printDivisors(100)

# This code is contributed by himanshu77
```

## C#

```
// A O(sqrt(n)) program that prints
// all divisors in sorted order
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to print the divisors
static void printDivisors(int n)
{
    for(int i = 1; i * i < n; i++)
    {
        if (n % i == 0)
            Console.Write(i + " ");
    }
    for(int i = (int)Math.Sqrt(n); i >= 1; i--)
    {
        if (n % i == 0)
            Console.Write(n / i + " ");
    }
} 

// Driver code  
public static void Main(string []arg)
{
    Console.Write("The divisors of 100 are: \n");

    printDivisors(100);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// A O(sqrt(n)) program that prints all divisors
// in sorted order

// function to print the divisors
function printDivisors(n)
{
    for (var i = 1; i*i < n; i++) {
        if (n % i == 0)
            document.write(i + " ");
    }
    for (var i = Math.sqrt(n); i >= 1; i--) {
        if (n % i == 0)
            document.write(" " + n / i);
    }
}

// Driver program to test above function

    document.write("The divisors of 100 are: \n");
    printDivisors(100);

// This code is contributed by simranarora5sos

</script>
```

**Output**

```
The divisors of 100 are: 
1 2 4 5 10 20 25 50 100 
```

感谢神秘心灵提出上述解决方案。

当循环条件中的角因子相差 1 时，使用两个循环之间的 if 条件(示例-此处因子为 30 (5，6)，5 将打印两次；要解决这个问题，需要这个步骤。

本文由[阿舒托什·库马尔](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
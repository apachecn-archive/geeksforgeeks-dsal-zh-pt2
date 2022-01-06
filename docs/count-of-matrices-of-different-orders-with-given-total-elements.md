# 给定元素个数的矩阵(不同阶)计数

> 原文:[https://www . geeksforgeeks . org/给定元素总数的不同顺序矩阵计数/](https://www.geeksforgeeks.org/count-of-matrices-of-different-orders-with-given-total-elements/)

给定一个数字 N 表示矩阵中元素的总数，任务是打印矩阵的所有可能顺序。顺序是一对(m，n)整数，其中 m 是行数，n 是列数。例如，如果元素的数量是 8，那么所有可能的顺序是:
(1，8)，(2，4)，(4，2)，(8，1)。
**举例:**

> **输入:** N = 8
> **输出:** (1，2) (2，4) (4，2) (8，1)
> **输入:** N = 100
> **输出:**
> (1，100) (2，50) (4，25) (5，20) (10，10) (20，5) (25，4) (50，2) (100，1)

**方法:**
如果一个矩阵有 m 行 n 列，那么这个矩阵就是 m×n 的。矩阵中元素的总数等于(m*n)。所以我们从 1 开始，逐个检查它是否除以 N(元素总数)。如果它分裂，这将是一个可能的顺序。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to print all possible order
void printAllOrder(int n)
{
    // total number of elements in a matrix
    // of order m * n is equal (m*n)
    // where m is number of rows and n is
    // number of columns
    for (int i = 1; i <= n; i++) {

        // if n is divisible by i then i
        // and n/i will be the one
        // possible order of the matrix
        if (n % i == 0) {

            // print the given format
            cout << i << " " << n / i << endl;
        }
    }
}

// Driver code
int main()
{
    int n = 10;
    printAllOrder(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
    {
    // Function to print all possible order
    static void printAllOrder(int n)
    {
        // total number of elements in a matrix
        // of order m * n is equal (m*n)
        // where m is number of rows and n is
        // number of columns
        for (int i = 1; i <= n; i++) {

            // if n is divisible by i then i
            // and n/i will be the one
            // possible order of the matrix
            if (n % i == 0) {

                // print the given format
                System.out.println( i + " " + n / i );
            }
        }
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 10;
        printAllOrder(n);

    }

}

// This code is contributed by ihritik
```

## 计算机编程语言

```
# Python implementation of the above approach

# Function to print all possible order
def printAllOrder(n):

    # total number of elements in a matrix
    # of order m * n is equal (m*n)
    # where m is number of rows and n is
    # number of columns
    for i in range(1,n+1):

        # if n is divisible by i then i
        # and n/i will be the one
        # possible order of the matrix
        if (n % i == 0) :

            # print the given format
            print( i ,n // i )

# Driver code
n = 10
printAllOrder(n)

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
    {
    // Function to print all possible order
    static void printAllOrder(int n)
    {
        // total number of elements in a matrix
        // of order m * n is equal (m*n)
        // where m is number of rows and n is
        // number of columns
        for (int i = 1; i <= n; i++) {

            // if n is divisible by i then i
            // and n/i will be the one
            // possible order of the matrix
            if (n % i == 0) {

                // print the given format
                Console.WriteLine( i + " " + n / i );
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        printAllOrder(n);

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to print all possible order
function printAllOrder($n)
{
    // total number of elements in a matrix
    // of order m * n is equal (m*n)
    // where m is number of rows and n is
    // number of columns
    for ($i = 1; $i <= $n; $i++)
    {

        // if n is divisible by i then i
        // and n/i will be the one
        // possible order of the matrix
        if ($n % $i == 0)
        {

            // print the given format
            echo $i, " ", ($n / $i), "\n";
        }
    }
}

// Driver code
$n = 10;
printAllOrder($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Java Script implementation of the above approach

    // Function to print all possible order
    function printAllOrder( n)
    {
        // total number of elements in a matrix
        // of order m * n is equal (m*n)
        // where m is number of rows and n is
        // number of columns
        for (let i = 1; i <= n; i++) {

            // if n is divisible by i then i
            // and n/i will be the one
            // possible order of the matrix
            if (n % i == 0) {

                // print the given format
                document.write( i + " " + n / i+"<br>" );
            }
        }
    }

    // Driver code

        let n = 10;
        printAllOrder(n);

// This code is contributed by sravan
</script>
```

**Output:** 

```
1 10
2 5
5 2
10 1
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*
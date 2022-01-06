# 计算数组乘积中尾随零的数量

> 原文:[https://www . geesforgeks . org/count-number-trading-zero-product-array/](https://www.geeksforgeeks.org/count-number-trailing-zeros-product-array/)

给定 n 的数组大小，我们需要找到数组乘积中的零的总数。

示例:

```
Input  : a[] = {100, 20, 40, 25, 4} 
Output : 6
Product is 100 * 20 * 40 * 25 * 4
which is 8000000 and has 6 trailing 0s.

Input  : a[] = {10, 100, 20, 30, 25, 4, 
                43, 25, 50, 90, 12, 80}
Output : 13
```

一个简单的解决方案是简单地乘以并计算乘积中的尾随 0。此解决方案可能会导致整数溢出。更好的解决方案是基于这样一个事实，即 0 是由 2 和 5 的组合形成的。因此，零的数量将取决于可以形成的 2 和 5 对的数量。
Ex。:8 * 3 * 5 * 23 * 17 * 25 * 4 * 11
2<sup>3</sup>* 3<sup>1</sup>* 5<sup>1</sup>* 23<sup>1</sup>* 17<sup>1</sup>* 5<sup>2</sup>* 2<sup>2</sup>* 11<sup>1</sup>

在这个例子中有 5 个二和 3 个五。因此，我们只能形成 3 对(2*5)。因此在乘积中将有 3 个零。

## C++

```
// CPP program for count total zero in product of array
#include <iostream>
using namespace std;

// Returns count of zeros in product of array
int countZeros(int a[], int n)
{
    int count2 = 0, count5 = 0;
    for (int i = 0; i < n; i++) {

        // count number of 2s in each element
        while (a[i] % 2 == 0) {
            a[i] = a[i] / 2;
            count2++;
        }

        // count number of 5s in each element
        while (a[i] % 5 == 0) {
            a[i] = a[i] / 5;
            count5++;
        }
    }
    // return the minimum
    return (count2 < count5) ? count2 : count5;
}

// Driven Program
int main()
{
    int a[] = { 10, 100, 20, 30, 50, 90, 12, 80 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countZeros(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for count total
// zero in product of array
import java.util.*;
import java.lang.*;

public class GfG
{
    // Returns count of zeros in product of array
    public static int countZeroso(int[] a, int n)
    {
        int count2 = 0, count5 = 0;
        for (int i = 0; i < n; i++)
        {

            // count number of 2s
            // in each element
            while (a[i] % 2 == 0)
            {
                a[i] = a[i] / 2;
                count2++;
            }

            // count number of 5s
            // in each element
            while (a[i] % 5 == 0)
            {
                a[i] = a[i] / 5;
                count5++;
            }
        }
        // return the minimum
        return (count2 < count5) ? count2 : count5;
    }

    // Driver function
    public static void main(String argc[])
    {
        int[] a = new int[]{ 10, 100, 20, 30,
                            50, 91, 12, 80 };
        int n = 8;
        System.out.println(countZeroso(a, n));
    }

}

// This code is contributed
// by Sagar Shukla
```

## 蟒蛇 3

```
# Python 3 program for count
# total zero in product of array

# Returns count of zeros
# in product of array
def countZeros(a, n) :
    count2 = 0
    count5 = 0
    for i in range(0, n) :

        # count number of 2s
        # in each element
        while (a[i] % 2 == 0) :
            a[i] = a[i] // 2
            count2 = count2 + 1

        # count number of 5s
        # in each element
        while (a[i] % 5 == 0) :
            a[i] = a[i] // 5
            count5 = count5 + 1

    # return the minimum
    if(count2 < count5) :
        return count2
    else :
        return count5

# Driven Program
a = [ 10, 100, 20, 30, 50, 90, 12, 80 ]
n = len(a)
print(countZeros(a, n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program for count total
// zero in product of array
using System;

public class GfG
{
    // Returns count of zeros in product of array
    public static int countZeroso(int[] a, int n)
    {
        int count2 = 0, count5 = 0;
        for (int i = 0; i < n; i++)
        {

            // count number of 2s
            // in each element
            while (a[i] % 2 == 0)
            {
                a[i] = a[i] / 2;
                count2++;
            }

            // count number of 5s
            // in each element
            while (a[i] % 5 == 0)
            {
                a[i] = a[i] / 5;
                count5++;
            }
        }
        // return the minimum
        return (count2 < count5) ? count2 : count5;
    }

    // Driver function
    public static void Main()
    {
        int[] a = new int[]{ 10, 100, 20, 30,
                            50, 91, 12, 80 };
        int n = 8;
        Console.WriteLine(countZeroso(a, n));
    }

}

// This code is contributed
// by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for count total
// zero in product of array

function countZeros($a, $n)
{

    $count2 = 0; $count5 = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // count number of 2s
        // in each element
        while ($a[$i] % 2 == 0)
        {
            $a[$i] = $a[$i] / 2;
            $count2++;
        }

        // count number of 5s
        // in each element
        while ($a[$i] % 5 == 0)
        {
            $a[$i] = $a[$i] / 5;
            $count5++;
        }
    }

    // return the minimum
    return ($count2 < $count5) ? $count2 : $count5;
}

// Driver Code
$a = array(10, 100, 20, 30, 50, 90, 12, 80);
$n = sizeof($a);
echo(countZeros($a, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program for count total
// zero in product of array

// Returns count of zeros in product of array
function countZeros(a, n)
{
    let count2 = 0, count5 = 0;
    for(let i = 0; i < n; i++)
    {

        // Count number of 2s in each element
        while (a[i] % 2 == 0)
        {
            a[i] = parseInt(a[i] / 2);
            count2++;
        }

        // Count number of 5s in each element
        while (a[i] % 5 == 0)
        {
            a[i] = parseInt(a[i] / 5);
            count5++;
        }
    }

    // Return the minimum
    return (count2 < count5) ? count2 : count5;
}

// Driver code
let a = [ 10, 100, 20, 30, 50, 90, 12, 80 ];
let n = a.length;

document.write(countZeros(a, n));

// This code is contributed by souravmahato348

</script>
```

输出:

```
 9
```
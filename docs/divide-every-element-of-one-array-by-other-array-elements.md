# 将一个数组的每个元素除以其他数组元素

> 原文:[https://www . geeksforgeeks . org/将一个数组中的每个元素除以其他数组元素/](https://www.geeksforgeeks.org/divide-every-element-of-one-array-by-other-array-elements/)

给定两个数组，要执行的操作是 a[]的每个元素都要除以 b[]的所有元素，并且必须计算它们的底值。
**例:**

```
Input : a[] = {5, 100, 8}, b[] = {2, 3}
Output : 0 16 1
Explanation :
Size of a[] is 3.
Size of b[] is 2.
Now 5 has to be divided by the elements of array b[]
i.e. 5 is divided by 2, then the quotient obtained 
is divided by 3 and the floor value of this is 
calculated. The same process is repeated for the other
array elements.
```

**第一种方法**:这个解的复杂度为 O(n * m)，其中 a[]的大小为 n，数组 b[]的大小为 m，在这个解中，我们固定数组 a[]的元素，并用数组 b[]的元素进行迭代。
**第二种方法**:在这个方法中我们使用了简单的数学。我们先求数组 B 的乘积，再除以 a[]
的每个数组元素，这个解的复杂度是 O(n)。

## C++

```
// CPP program to find quotient of array
// elements
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the quotient
// of every element of the array
void calculate(int a[], int b[], int n, int m)
{
    int mul = 1;

    // Calculate the product of all elements
    for (int i = 0 ; i < m ; i++)
        if (b[i] != 0)
            mul = mul * b[i];

    // To calculate the quotient of every
    // array element
    for (int i = 0 ; i < n ; i++)
    {
        int x = floor(a[i] / mul);
        cout << x << " ";
    }
}

// Driver code
int main()
{
    int a[] = {5 , 100 , 8};
    int b[] = {2 , 3};
    int n = sizeof(a)/sizeof(a[0]);
    int m = sizeof(b)/sizeof(b[0]);
    calculate(a, b, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find quotient of array
// elements

import java.io.*;

class GFG {

    // Function to calculate the quotient
    // of every element of the array
    static void calculate(int a[], int b[],
                                int n, int m)
    {

        int mul = 1;

        // Calculate the product of all
        // elements
        for (int i = 0; i < m; i++)
            if (b[i] != 0)
                mul = mul * b[i];

        // To calculate the quotient of every
        // array element
        for (int i = 0; i < n; i++) {
            int x = (int)Math.floor(a[i] / mul);
            System.out.print(x + " ");
        }
    }

    public static void main(String[] args)
    {
        int a[] = { 5, 100, 8 };
        int b[] = { 2, 3 };
        int n = a.length;
        int m = b.length;

        calculate(a, b, n, m);
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python3 program to find
# quotient of arrayelements
import math

# Function to calculate the quotient
# of every element of the array
def calculate(a, b, n, m):

    mul = 1

    # Calculate the product
    # of all elements
    for i in range(m):
        if (b[i] != 0):
            mul = mul * b[i]

    # To calculate the quotient
    # of every array element
    for i in range(n):
        x = math.floor(a[i] / mul)
        print(x, end = " ")

# Driver code
a = [ 5, 100, 8 ]
b = [ 2, 3 ]
n = len(a)
m = len(b)

calculate(a, b, n, m)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find quotient
// of array elements
using System;

class GFG {

    // Function to calculate the quotient
    // of every element of the array
    static void calculate(int []a, int []b,
                              int n, int m)
    {
        int mul = 1;

        // Calculate the product of all
        // elements
        for (int i = 0; i < m; i++)
            if (b[i] != 0)
                mul = mul * b[i];

        // To calculate the quotient of every
        // array element
        for (int i = 0; i < n; i++) {
            int x = (int)Math.Floor((double)(a[i] / mul));
            Console.Write(x + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int []a = { 5, 100, 8 };
        int []b = { 2, 3 };
        int n = a.Length;
        int m = b.Length;

        calculate(a, b, n, m);
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// quotient of array elements

// Function to calculate
// the quotient of every
// element of the array
function calculate( $a, $b,
                    $n, $m)
{
$mul = 1;

    // Calculate the product
    // of all elements
    for ( $i = 0 ; $i < $m ; $i++)
        if ($b[$i] != 0)
            $mul = $mul * $b[$i];

    // To calculate the quotient
    // of every array element
    for ( $i = 0 ; $i < $n ; $i++)
    {
        $x = floor($a[$i] / $mul);
        echo $x , " ";
    }
}

// Driver code
$a = array(5 , 100 , 8);
$b = array(2 , 3);
    $n = count($a);
    $m = count($b);
    calculate($a, $b, $n, $m);

// This code is contributed by anuju_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find quotient of array
// elements

// Function to calculate the quotient
// of every element of the array
function calculate(a, b, n, m)
{
    let mul = 1;

    // Calculate the product of all elements
    for (let i = 0 ; i < m ; i++)
        if (b[i] != 0)
            mul = mul * b[i];

    // To calculate the quotient of every
    // array element
    for (let i = 0 ; i < n ; i++)
    {
        let x = Math.floor(a[i] / mul);
        document.write(x + " ");
    }
}

// Driver code
    let a = [5 , 100 , 8];
    let b = [2 , 3];
    let n = a.length;
    let m = b.length;
    calculate(a, b, n, m);

// This code is contributed by Surbhi Tyagi

</script>
```

**输出:**

```
0 16 1
```
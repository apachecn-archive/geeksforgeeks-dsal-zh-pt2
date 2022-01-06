# 将数组旋转中的每个元素串联起来的最大数量

> 原文:[https://www . geeksforgeeks . org/通过串联数组旋转中的每个元素获得最大数量/](https://www.geeksforgeeks.org/maximum-number-by-concatenating-every-element-in-a-rotation-of-an-array/)

给定一个由 N 个元素组成的数组。任务是通过连接每个旋转中的每个元素来打印最大数量。在每次旋转中，第一个元素将代替每次旋转中的最后一个元素，反之亦然。
**例:**

> **输入:** a[]: {54，546，548，60}
> **输出:** 6054546548
> 第一转:5465486054
> 第二转:5486054546
> 第三转:6054546548
> 第四转:5454654860
> **输入:** a[]

**逼近:**仔细观察，发现所有元素中最左边数字最大的那个数将是这个数的第一个元素。因为连接必须根据数组的旋转来完成。将所有数字从最左边的最大数字索引连接到末尾，然后将元素从第 0 个<sup>索引连接到最左边的最大数字索引。
以下是上述方法的实施:</sup> 

## C++

```
// C++ program to print the
// Maximum number by concatenating
// every element in rotation of array
#include <bits/stdc++.h>
using namespace std;

// Function to print the largest number
void printLargest(int a[], int n)
{

    // store the index of largest
    // left most digit of elements
    int max = -1;
    int ind = -1;

    // Iterate for all numbers
    for (int i = 0; i < n; i++) {

        int num = a[i];

        // check for the last digit
        while (num) {
            int r = num % 10;
            num = num / 10;
            if (num == 0) {
                // check for the largest left most digit
                if (max < r) {
                    max = r;
                    ind = i;
                }
            }
        }
    }

    // print the largest number

    // print the rotation of array
    for (int i = ind; i < n; i++)
        cout << a[i];

    // print the rotation of array
    for (int i = 0; i < ind; i++)
        cout << a[i];
}

// Driver Code
int main()
{
    int a[] = { 54, 546, 548, 60 };
    int n = sizeof(a) / sizeof(a[0]);
    printLargest(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// Maximum number by concatenating
// every element in rotation of array
import java.util.*;
import java.lang.*;

public class GFG {
    // Function to print the largest number
    static void printLargest(int a[], int n)
    {
        // store the index of largest
        // left most digit of elements
        int max = -1;
        int ind = -1;

        // Iterate for all numbers
        for (int i = 0; i < n; i++) {
            int num = a[i];

            // check for the last digit
            while (num > 0) {
                int r = num % 10;
                num = num / 10;
                if (num == 0) {
                    // check for the largest left most digit
                    if (max < r) {
                        max = r;
                        ind = i;
                    }
                }
            }
        }
        // print the largest number

        // print the rotation of array
        for (int i = ind; i < n; i++)
            System.out.print(a[i]);

        // print the rotation of array
        for (int i = 0; i < ind; i++)
            System.out.print(a[i]);
    }

    // Driver Code
    public static void main(String args[])
    {
        int a[] = { 54, 546, 548, 60 };
        int n = a.length;
        printLargest(a, n);
    }
}
```

## 蟒蛇 3

```
# Python program to print the
# Maximum number by concatenating
# every element in rotation of array

# Function to print the largest number
def printLargest(a, n):

    # store the index of largest
    # left most digit of elements
    max =-1
    ind =-1

    # Iterate for all numbers
    for i in range(0, n):
         num = a[i]

        # check for the last digit
         while(num):

            r = num % 10;
            num = num / 10;
            if(num == 0):
                # check for the largest left most digit
                if(max<r):
                    max = r
                    ind = i;

    # print the largest number

    # print the rotation of array
    for i in range(ind, n):
        print(a[i], end =''),

    # print the rotation of array
    for i in range(0, ind) :
        print(a[i], end ='')

# Driver Code
if __name__ == "__main__":
    a = [54, 546, 548, 60]
    n = len(a)
    printLargest(a, n)

# This code is contributed by Shivi_Aggarwal
```

## C#

```
// C# program to print the
// Maximum number by concatenating
// every element in rotation of array
using System;

class GFG {

    // Function to print the largest number
    static void printLargest(int[] a, int n)
    {
        // store the index of largest
        // left most digit of elements
        int max = -1;
        int ind = -1;

        // Iterate for all numbers
        for (int i = 0; i < n; i++) {
            int num = a[i];

            // check for the last digit
            while (num > 0) {
                int r = num % 10;
                num = num / 10;
                if (num == 0) {
                    // check for the largest left most digit
                    if (max < r) {
                        max = r;
                        ind = i;
                    }
                }
            }
        }
        // print the largest number

        // print the rotation of array
        for (int i = ind; i < n; i++)
            Console.Write(a[i]);

        // print the rotation of array
        for (int i = 0; i < ind; i++)
            Console.Write(a[i]);
    }

    // Driver Code
    public static void Main()
    {
        int[] a = { 54, 546, 548, 60 };
        int n = 4;
        printLargest(a, n);
    }
}

// This code is contributed by mohit kumar 29
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// the Maximum number by
// concatenating every
// element in rotation of array

// Function to print
// the largest number
function printLargest($a, $n)
{

    // store the index of largest
    // left most digit of elements
    $max = -1;
    $ind = -1;

    // Iterate for
    // all numbers
    for($i = 0 ; $i < $n; $i++)
    {

        $num = $a[$i];

        // check for the
        // the last digit
        while($num)
        {
            $r = $num % 10;
            $num = (int)$num / 10;
            if($num == 0)
            {
                // check for the largest
                // left most digit
                if($max < $r)
                {
                    $max = $r;
                    $ind = $i;
                }
            }
        }
    }

    // print the largest number

    // print the
    // rotation of array
    for($i = $ind; $i < $n; $i++)
    echo $a[$i];

    // print the
    // rotation of array
    for($i = 0; $i < $ind; $i++)
    echo $a[$i];
}

// Driver Code
$a = array (54, 546,
            548, 60);
$n = sizeof($a);
printLargest($a, $n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to print the
// Maximum number by concatenating
// every element in rotation of array

    // Function to prlet the largest number
    function printLargest(a, n)
    {
        // store the index of largest
        // left most digit of elements
        let max = -1;
        let ind = -1;

        // Iterate for all numbers
        for (let i = 0; i < n; i++) {
            let num = a[i];

            // check for the last digit
            while (num > 0) {
                let r = num % 10;
                num = Math.floor(num / 10);
                if (num == 0) {
                    // check for the largest
                    // left most digit
                    if (max < r) {
                        max = r;
                        ind = i;
                    }
                }
            }
        }
        // print the largest number

        // print the rotation of array
        for (let i = ind; i < n; i++)
            document.write(a[i]);

        // print the rotation of array
        for (let i = 0; i < ind; i++)
            document.write(a[i]);
    }

// driver code

     let a = [ 54, 546, 548, 60 ];
        let n = a.length;
        printLargest(a, n);

</script>
```

**Output:** 

```
6054546548
```

**时间复杂度:** O(n * log <sub>10</sub> (num))，其中 n 为数组的大小，num 为数组最大元素的位数。

**辅助空间:** O(1)
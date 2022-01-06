# 最小化两个子集之和的绝对差

> 原文:[https://www . geesforgeks . org/minimum-绝对差-和-两个子集/](https://www.geeksforgeeks.org/minimize-absolute-difference-sum-two-subsets/)

给定一个数 n，将前 n 个自然数(1，2，…n)分成两个子集，使得两个子集的和之差最小。
示例:

```
Input : n = 4
Output : First subset sum = 5, 
         Second subset sum = 5.
         Difference = 0
Explanation:
Subset 1: 1 4 
Subset 2: 2 3 

Input : n = 6 
Output: First subset sum = 10, 
        Second subset sum = 11.
        Difference = 1
Explanation : 
Subset 1: 1 3 6 
Subset 2: 2 4 5 
```

**方法:**
该方法基于这样一个事实，即将中间两个元素放在一组中，将角元素放在另一组中，可以将任意四个连续的数字分成两组。因此，如果 N 是 4 的倍数，那么它们的差将是 0，因此一个集合的总和将是 N 个元素总和的一半，这可以通过使用 **sum = n*(n+1)/2**
来计算。还有三种情况需要考虑，其中我们不能分成 4 个组，这将留下 1、2 和 3 的余数:
**a)** 如果它留下 1 的余数， 那么所有其他 n-1 个元素被组合成 4 个元素的组，因此它们的和将是 int(sum/2 ),另一半和将是 int(sum/2+1 ),并且它们的差将总是 1。
**b)** 如果 n%4 == 2，将遵循上述步骤。这里我们从 3 开始为元素组成大小为 4 的组。剩下的元素是 1 和 2。1 人在一组，2 人在另一组。
**c)** 当 n%4 == 3 时，再将 n-3 个元素俱乐部成 4 个一组。遗漏的元素将是 1、2 和 3，其中 1 和 2 将进入一个集合，3 将进入另一个集合，最终使差为 0，每个集合的总和为 sum/2。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to Minimize the absolute
// difference of sum of two subsets
#include <bits/stdc++.h>
using namespace std;

// function to print difference
void subsetDifference(int n)
{
    // summation of n elements
    int s = n * (n + 1) / 2;

    // if divisible by 4
    if (n % 4 == 0) {
        cout << "First subset sum = "
             << s / 2;
        cout << "\nSecond subset sum = "
             << s / 2;
        cout << "\nDifference = " << 0;
    }
    else {

        // if remainder 1 or 2\. In case of remainder
        // 2, we divide elements from 3 to n in groups
        // of size 4 and put 1 in one group and 2 in
        // group. This also makes difference 1.
        if (n % 4 == 1 || n % 4 == 2) {

            cout << "First subset sum = "
                 << s / 2;
            cout << "\nSecond subset sum = "
                 << s / 2 + 1;
            cout << "\nDifference = " << 1;
        }

        // We put elements from 4 to n in groups of
        // size 4\. Remaining elements 1, 2 and 3 can
        // be divided as (1, 2) and (3).
        else
        {
            cout << "First subset sum = "
                 << s / 2;
            cout << "\nSecond subset sum = "
                 << s / 2;
            cout << "\nDifference = " << 0;
        }
    }
}

// driver program to test the above function
int main()
{
    int n = 6;
    subsetDifference(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Minimize the absolute
// difference of sum of two subsets
import java.util.*;

class GFG {

    // function to print difference
    static void subsetDifference(int n)
    {
        // summation of n elements
        int s = n * (n + 1) / 2;

        // if divisible by 4
        if (n % 4 == 0) {

                 System.out.println("First subset sum = " + s / 2);
                 System.out.println("Second subset sum = " + s / 2);
                 System.out.println("Difference = " + 0);
        }
        else {

            // if remainder 1 or 2\. In case of remainder
            // 2, we divide elements from 3 to n in groups
            // of size 4 and put 1 in one group and 2 in
            // group. This also makes difference 1.
            if (n % 4 == 1 || n % 4 == 2) {

                  System.out.println("First subset sum = " + s / 2);
                  System.out.println("Second subset sum = " + ((s / 2) + 1));
                  System.out.println("Difference = " + 1);
            }

            // We put elements from 4 to n in groups of
            // size 4\. Remaining elements 1, 2 and 3 can
            // be divided as (1, 2) and (3).
            else
            {
                 System.out.println("First subset sum = " + s / 2);
                 System.out.println("Second subset sum = " + s / 2);
                 System.out.println("Difference = " + 0);
            }
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
         int n = 6;
         subsetDifference(n);
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 code to Minimize the absolute
# difference of sum of two subsets

# function to print difference
def subsetDifference( n ):

    # summation of n elements
    s = int(n * (n + 1) / 2)

    # if divisible by 4
    if n % 4 == 0:
        print("First subset sum = ", int(s / 2))
        print("Second subset sum = ",int(s / 2))
        print("Difference = " , 0)

    else:

        # if remainder 1 or 2\. In case of remainder
        # 2, we divide elements from 3 to n in groups
        # of size 4 and put 1 in one group and 2 in
        # group. This also makes difference 1.
        if n % 4 == 1 or n % 4 == 2:
            print("First subset sum = ",int(s/2))
            print("Second subset sum = ",int(s/2)+1)
            print("Difference = ", 1)

        # We put elements from 4 to n in groups of
        # size 4\. Remaining elements 1, 2 and 3 can
        # be divided as (1, 2) and (3).
        else:
            print("First subset sum = ", int(s / 2))
            print("Second subset sum = ",int(s / 2))
            print("Difference = " , 0)

# driver code to test the above function
n = 6
subsetDifference(n)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program for Minimize the absolute
// difference of sum of two subsets
using System;

class GFG {

    // function to print difference
    static void subsetDifference(int n)
    {

        // summation of n elements
        int s = n * (n + 1) / 2;

        // if divisible by 4
        if (n % 4 == 0) {

            Console.WriteLine("First "
            + "subset sum = " + s / 2);

            Console.WriteLine("Second "
            + "subset sum = " + s / 2);

            Console.WriteLine("Difference"
                              + " = " + 0);
        }
        else {

            // if remainder 1 or 2\. In case
            // of remainder 2, we divide
            // elements from 3 to n in groups
            // of size 4 and put 1 in one
            // group and 2 in group. This
            // also makes difference 1.
            if (n % 4 == 1 || n % 4 == 2) {

                Console.WriteLine("First "
                + "subset sum = " + s / 2);

                Console.WriteLine("Second "
                + "subset sum = " + ((s / 2)
                                      + 1));

                Console.WriteLine("Difference"
                               + " = " + 1);
            }

            // We put elements from 4 to n
            // in groups of size 4\. Remaining
            // elements 1, 2 and 3 can
            // be divided as (1, 2) and (3).
            else
            {
                Console.WriteLine("First "
                + "subset sum = " + s / 2);

                Console.WriteLine("Second "
                 + "subset sum = " + s / 2);

                Console.WriteLine("Difference"
                                + " = " + 0);
            }
        }
    }

    /* Driver program to test above
    function */
    public static void Main()
    {
        int n = 6;

        subsetDifference(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Minimize the absolute
// difference of sum of two subsets

// function to print difference
function subsetDifference($n)
{

    // summation of n elements
    $s = $n * ($n + 1) / 2;

    // if divisible by 4
    if ($n % 4 == 0)
    {
        echo "First subset sum = "
            ,floor($s / 2);
        echo "\nSecond subset sum = "
            ,floor($s / 2);
        echo "\nDifference = " , 0;
    }
    else
    {

        // if remainder 1 or 2.
        // In case of remainder
        // 2, we divide elements
        // from 3 to n in groups
        // of size 4 and put 1 in
        // one group and 2 in
        // group. This also makes
        // difference 1.
        if ($n % 4 == 1 || $n % 4 == 2)
        {

            echo"First subset sum = "
                , floor($s / 2);
            echo "\nSecond subset sum = "
                , floor($s / 2 + 1);
            echo"\nDifference = " ,1;
        }

        // We put elements from 4
        // to n in groups of
        // size 4\. Remaining
        // elements 1, 2 and 3 can
        // be divided as (1, 2)
        // and (3).
        else
        {
            echo "First subset sum = "
                ,floor($s / 2);
            echo "\nSecond subset sum = "
                , floor($s / 2);
            echo"\nDifference = " , 0;
        }
    }
}

    // Driver code
    $n = 6;
    subsetDifference($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to Minimize the absolute
// difference of sum of two subsets

// function to print difference
function subsetDifference(n)
{

    // summation of n elements
    let s = n * (n + 1) / 2;

    // if divisible by 4
    if (n % 4 == 0)
    {
        document.write("First subset sum = " + Math.floor(s / 2));
        document.write("<br> Second subset sum = " + Math.floor(s / 2));
        document.write("<br> Difference = "  +  0);
    }
    else
    {

        // if remainder 1 or 2.
        // In case of remainder
        // 2, we divide elements
        // from 3 to n in groups
        // of size 4 and put 1 in
        // one group and 2 in
        // group. This also makes
        // difference 1.
        if (n % 4 == 1 || n % 4 == 2)
        {

            document.write("First subset sum = " + Math.floor(s / 2));
            document.write("<br> Second subset sum = " + Math.floor(s / 2 + 1));
            document.write("<br> Difference = " + 1);
        }

        // We put elements from 4
        // to n in groups of
        // size 4\. Remaining
        // elements 1, 2 and 3 can
        // be divided as (1, 2)
        // and (3).
        else
        {
            document.write( "First subset sum = " + Math.floor(s / 2));
            document.write( "<br> Second subset sum = " + Math.floor(s / 2));
            document.write("<br> Difference = " + 0);
        }
    }
}

    // Driver code
    let n = 6;
    subsetDifference(n);

// This code is contributed by _saurabh_jaiswal.
</script>
```

输出:

```
First subset sum = 10
Second subset sum = 11
Difference = 1
```
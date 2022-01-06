# 最小元素，其第 n 次幂大于大小为 n 的数组的乘积

> 原文:[https://www . geesforgeks . org/minimum-element-what-n-th-power-great-product-array-size-n/](https://www.geeksforgeeks.org/minimum-element-whose-n-th-power-greater-product-array-size-n/)

给定一组 **n 个**整数。找到最小 x，它将被分配给每个数组元素，这样这个新数组的所有元素的乘积将严格大于初始数组的所有元素的乘积。
示例:

```
Input: 4 2 1 10 6 
Output: 4 

Explanation: Product of elements of initial
array 4*2*1*10*6 = 480\. If x = 4 then 4*4*
4*4*4 = 480, if x = 3 then 3*3*3*3*3=243\. 
So minimal element = 4   

Input: 3 2 1 4 
Output: 3

Explanation: Product of elements of initial
array 3*2*1*4 = 24\. If x = 3 then 3*3*3*3 
= 81, if x = 2 then 2*2*2*2 = 243\. So minimal
element = 3\. 
```

***简单方法:*** 简单方法是从 1 开始循环，直到我们发现乘积大于初始数组乘积。
**时间复杂度** : *O(x^n)* 如果使用了幂函数那么*o(x * log n)*
***数学方法:***

```
Let, x^n = a1 * a2 * a3 * a4 *....* an
we have been given n and value of a1, a2, a3, ..., an.
Now take log on both sides with base e

 n*logex > loge(a1) + loge(a2) +......+ loge(an)
Lets sum = loge(a1) + loge(a2) + ...... + loge(an)
 n*loge x > sum
 loge x > sum/n
Then take antilog on both side
 x > e^(sum/n) 
```

下面是上述方法的实现。

## C++

```
// CPP program to find minimum element whose n-th
// power is greater than product of an array of
// size n
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum element
int findMin(int a[], int n)
{
    // loop to traverse and store the sum of log
    double sum = 0;
    for (int i = 0; i < n; i++)
        sum += log(a[i]); // computes sum

    // calculates the elements according to formula.
    int x = exp(sum / n);

    // returns the minimal element
    return x + 1;
}

// Driver program to test above function
int main()
{
    // initialised array
    int a[] = { 3, 2, 1, 4 };

    // computes the size of array
    int n = sizeof(a) / sizeof(a[0]);

    // prints out the minimal element
    cout << findMin(a, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to find Minimum element whose
// n-th power is greater than product of
// an array of size n
import java.util.*;

class GFG {

    // function to find the minimum element
    static int findMin(int a[], int n)
    {
        // loop to traverse and store the
        // sum of log
        double sum = 0;
        for (int i = 0; i < n; i++)

            // computes sum
            sum += Math.log(a[i]);

        // calculates the elements
        // according to formula.
        int x = (int)Math.exp(sum / n);

        // returns the minimal element
        return x + 1;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        // initialised array
        int a[] = { 3, 2, 1, 4 };

        // computes the size of array
        int n = a.length;

        // prints out the minimal element
        System.out.println(findMin(a, n));

    }
}

// This code is contributed by Arnav Kr. Mandal.   
```

## 蟒蛇 3

```
# Python3 program to find minimum element
# whose n-th power is greater than product
# of an array of size n
import math as m

# function to find the minimum element
def findMin( a, n):

    # loop to traverse and store the
    # sum of log
    _sum = 0
    for i in range(n):
        _sum += m.log(a[i]) # computes sum

    # calculates the elements
    # according to formula.
    x = m.exp(_sum / n)

    # returns the minimal element
    return int(x + 1)

# Driver program to test above function

# initialised array
a = [ 3, 2, 1, 4 ]

# computes the size of array
n = len(a)

# prints out the minimal element
print(findMin(a, n))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# Code to find Minimum element whose
// n-th power is greater than product of
// an array of size n
using System;

class GFG {

    // function to find the minimum element
    static int findMin(int []a, int n)
    {

        // loop to traverse and store the
        // sum of log
        double sum = 0;
        for (int i = 0; i < n; i++)

            // computes sum
            sum += Math.Log(a[i]);

        // calculates the elements
        // according to formula.
        int x = (int)Math.Exp(sum / n);

        // returns the minimal element
        return x + 1;
    }

    /* Driver program to test above function */
    public static void Main()
    {

        // initialised array
        int []a = { 3, 2, 1, 4 };

        // computes the size of array
        int n = a.Length;

        // prints out the minimal element
        Console.WriteLine(findMin(a, n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// element whose n-th power
// is greater than product of
// an array of size n

// function to find the
// minimum element
function findMin($a, $n)
{

    // loop to traverse and
    // store the sum of log
    $sum = 0;
    for ($i = 0; $i < $n; $i++)

        // computes sum
        $sum += log($a[$i]);

    // calculates the elements
    // according to formula.
    $x = exp($sum / $n);

    // returns the minimal element
    return (int)($x + 1);
}

// Driver Code
$a = array( 3, 2, 1, 4 );

// computes the size of array
$n = sizeof($a);

// prints out the minimal element
echo(findMin($a, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript Code to find Minimum element whose
// n-th power is greater than product of
// an array of size n

    // function to find the minimum element
    function findMin(a, n)
    {

        // loop to traverse and store the
        // sum of log
        var sum = 0;
        for (i = 0; i < n; i++)

            // computes sum
            sum += Math.log(a[i]);

        // calculates the elements
        // according to formula.
        var x = parseInt( Math.exp(sum / n));

        // returns the minimal element
        return x + 1;
    }

    /* Driver program to test above function */

        // initialised array
        var a = [ 3, 2, 1, 4 ];

        // computes the size of array
        var n = a.length;

        // prints out the minimal element
        document.write(findMin(a, n));

// This code is contributed by aashish1995
</script>
```

输出:

```
3
```

**时间复杂度:** O(n * log(logn))
**辅助空间:** O(1)
本文由**Raja vikramatitya**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
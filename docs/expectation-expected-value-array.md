# 数组的期望值或期望值

> 原文:[https://www . geesforgeks . org/expect-期望值-array/](https://www.geeksforgeeks.org/expectation-expected-value-array/)

[概率上任意一组数的期望值或期望值](https://www.geeksforgeeks.org/linearity-of-expectation/)是它所代表的实验重复次数的长期平均值。例如，轧制六面模具的期望值是 3.5，因为在极大量的辊中出现的所有数字的平均值接近 3.5。不太粗略地说，大数定律表明，当重复次数接近无穷大时，数值的算术平均值几乎肯定会收敛到期望值。期望值也称为**期望**、**数学期望**、EV 或第一时刻。
给定一个数组，任务是计算数组的**期望值**。
**举例:**

```
Input : [1.0, 2.0, 3.0, 4.0, 5.0, 6.0]
Output : 3.5

Input :[1.0, 9.0, 6.0, 7.0, 8.0, 12.0]
Output :7.16
```

下面是实现:

## C++

```
// CPP code to calculate expected
// value of an array
#include <bits/stdc++.h>
using namespace std;

// Function to calculate expectation
float calc_Expectation(float a[], float n)
{
    /*variable prb is for probability
    of each element which is same for
    each element  */
    float prb = (1 / n);

    // calculating expectation overall
    float sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i] * prb;   

    // returning expectation as sum
    return sum;
}

// Driver program
int main()
{
    float expect, n = 6.0;
    float a[6] = { 1.0, 2.0, 3.0,
                 4.0, 5.0, 6.0 };

    // Function for calculating expectation
    expect = calc_Expectation(a, n);

    // Display expectation of given array
    cout << "Expectation of array E(X) is : "
         << expect << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to calculate expected
// value of an array
import java.io.*;

class GFG
{
    // Function to calculate expectation
    static float calc_Expectation(float a[], float n)
    {
        // Variable prb is for probability of each
        // element which is same for each element
        float prb = (1 / n);

        // calculating expectation overall
        float sum = 0;
        for (int i = 0; i < n; i++)
            sum += a[i] * prb;

        // returning expectation as sum
        return sum;
    }

    // Driver program
    public static void main(String args[])
    {
        float expect, n = 6f;
        float a[] = { 1f, 2f, 3f,
                       4f, 5f, 6f };

        // Function for calculating expectation
        expect = calc_Expectation(a, n);

        // Display expectation of given array
        System.out.println("Expectation of array E(X) is : "
                           + expect);
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# python code to calculate expected
# value of an array

# Function to calculate expectation
def calc_Expectation(a, n):

    # variable prb is for probability
    # of each element which is same for
    # each element
    prb = 1 / n

    # calculating expectation overall
    sum = 0
    for i in range(0, n):
        sum += (a[i] * prb)

    # returning expectation as sum
    return float(sum)

# Driver program
n = 6;
a = [ 1.0, 2.0, 3.0,4.0, 5.0, 6.0 ]

# Function for calculating expectation
expect = calc_Expectation(a, n)

# Display expectation of given array
print( "Expectation of array E(X) is : ",
                                 expect )

# This code is contributed by Sam007
```

## C#

```
// C# code to calculate expected
// value of an array
using System;

class GFG {

    // Function to calculate expectation
    static float calc_Expectation(float []a,
                                    float n)
    {

        // Variable prb is for probability
        // of each element which is same
        // for each element
        float prb = (1 / n);

        // calculating expectation overall
        float sum = 0;

        for (int i = 0; i < n; i++)
            sum += a[i] * prb;

        // returning expectation as sum
        return sum;
    }

    // Driver program
    public static void Main()
    {
        float expect, n = 6f;
        float []a = { 1f, 2f, 3f,
                    4f, 5f, 6f };

        // Function for calculating
        // expectation
        expect = calc_Expectation(a, n);

        // Display expectation of given
        // array
        Console.WriteLine("Expectation"
               + " of array E(X) is : "
                             + expect);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to calculate expected
// value of an array

// Function to calculate expectation
function calc_Expectation($a, $n)
{
    /*variable prb is for probability
    of each element which is same for
    each element */
    $prb = (1 / $n);

    // calculating expectation overall
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $a[$i] * $prb;

    // returning expectation as sum
    return $sum;
}

// Driver Code
$n = 6.0;
$a = array(1.0, 2.0, 3.0,
           4.0, 5.0, 6.0);

// Function for calculating expectation
$expect = calc_Expectation($a, $n);

// Display expectation of given array
echo "Expectation of array E(X) is : ".
                        $expect . "\n";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// Javascript code to calculate expected
// value of an array

   // Function to calculate expectation
    function calc_Expectation(a, n)
    {
        // Variable prb is for probability of each
        // element which is same for each element
        let prb = (1 / n);

        // calculating expectation overall
        let sum = 0;
        for (let i = 0; i < n; i++)
            sum += a[i] * prb;

        // returning expectation as sum
        return sum;
    }

// driver function

        let expect, n = 6;
        let a = [ 1, 2, 3,
                       4, 5, 6 ];

        // Function for calculating expectation
        expect = calc_Expectation(a, n);

        // Display expectation of given array
        document.write("Expectation of array E(X) is : "
                           + expect);

</script>
```

**输出:**

```
Expectation of array E(X) is : 3.5
```

程序的时间复杂度为 **O(n)** 。
我们可以看到期望值实际上是数字的平均值，我们也可以简单的[计算数组的平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)。
本文由 [**希曼舒·冉冉**](https://auth.geeksforgeeks.org/profile.php?user=himanshu_300) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
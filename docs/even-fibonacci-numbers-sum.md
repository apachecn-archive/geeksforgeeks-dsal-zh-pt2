# 偶数斐波那契数和

> 原文:[https://www.geeksforgeeks.org/even-fibonacci-numbers-sum/](https://www.geeksforgeeks.org/even-fibonacci-numbers-sum/)

给定一个极限，求斐波那契数列中低于给定极限的所有偶数项的和。
[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的前几项是，1，1， **2** ，3，5， **8** ，13，21， **34** ，55，89， **144** ，233，…(偶数突出显示)。
**举例:**

```
Input : limit = 8
Output : 10
Explanation : 2 + 8 = 10

Input : limit = 400;
Output : 188.
Explanation : 2 + 8 + 34 + 144 = 188.
```

一个简单的解决方案是迭代所有素数，而下一个数小于或等于给定的极限。对于每个数字，检查它是否为偶数。如果数字是偶数，将其加到结果中。
一个有效的解决方案是基于下面的[偶数斐波那契数的递归公式](https://www.geeksforgeeks.org/nth-even-fibonacci-number/)

```
Recurrence for Even Fibonacci sequence is:
     EFn = 4EFn-1 + EFn-2
with seed values
     EF0 = 0 and EF1 = 2.

EFn represents n'th term in Even Fibonacci sequence.
```

以上公式详见[本](https://www.geeksforgeeks.org/nth-even-fibonacci-number/)。
所以在迭代斐波那契数时，我们只生成偶数斐波那契数。

## C++

```
// Find the sum of all the even-valued terms in
// the Fibonacci sequence which do not exceed
// given limit.
#include<iostream>
using namespace std;

// Returns sum of even Fibonacci numbers which are
// less than or equal to given limit.
int evenFibSum(int limit)
{
    if (limit < 2)
        return 0;

    // Initialize first two even prime numbers
    // and their sum
    long long int ef1 = 0, ef2 = 2;
    long long int sum = ef1 + ef2;

    // calculating sum of even Fibonacci value
    while (ef2 <= limit)
    {
        // get next even value of Fibonacci sequence
        long long int ef3 = 4*ef2 + ef1;

        // If we go beyond limit, we break loop
        if (ef3 > limit)
            break;

        // Move to next even number and update sum
        ef1 = ef2;
        ef2 = ef3;
        sum += ef2;
    }

    return sum;
}

// Driver code
int main()
{
    int limit = 400;
    cout << evenFibSum(limit);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Find the sum of all the even-valued terms in
// the Fibonacci sequence which do not exceed
// given limit.
import java.io.*;

class GFG
{
    // Returns sum of even Fibonacci numbers which are
    // less than or equal to given limit.
    static int evenFibSum(int limit)
    {
        if (limit < 2)
            return 0;

        // Initialize first two even prime numbers
        // and their sum
        long ef1 = 0, ef2 = 2;
        long sum = ef1 + ef2;

        // calculating sum of even Fibonacci value
        while (ef2 <= limit)
        {
            // get next even value of Fibonacci sequence
            long ef3 = 4 * ef2 + ef1;

            // If we go beyond limit, we break loop
            if (ef3 > limit)
                break;

            // Move to next even number and update sum
            ef1 = ef2;
            ef2 = ef3;
            sum += ef2;
        }

        return(int) sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int limit = 400;
        System.out.println(evenFibSum(limit));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Find the sum of all the even-valued
# terms in the Fibonacci sequence which
# do not exceed given limit.

# Returns sum of even Fibonacci numbers which
# are less than or equal to given limit.
def evenFibSum(limit) :
    if (limit < 2) :
        return 0

    # Initialize first two even prime numbers
    # and their sum
    ef1 = 0
    ef2 = 2
    sm= ef1 + ef2

    # calculating sum of even Fibonacci value
    while (ef2 <= limit) :

        # get next even value of Fibonacci
        # sequence
        ef3 = 4 * ef2 + ef1

        # If we go beyond limit, we break loop
        if (ef3 > limit) :
            break

        # Move to next even number and update
        # sum
        ef1 = ef2
        ef2 = ef3
        sm = sm + ef2

    return sm

# Driver code
limit = 400
print(evenFibSum(limit))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to Find the sum of all
// the even-valued terms in the
// Fibonacci sequence which do not
// exceed given limit.given limit.
using System;

class GFG {

    // Returns sum of even Fibonacci
    // numbers which are less than or
    // equal to given limit.
    static int evenFibSum(int limit)
    {
        if (limit < 2)
            return 0;

        // Initialize first two even
        // prime numbers and their sum
        long ef1 = 0, ef2 = 2;
        long sum = ef1 + ef2;

        // calculating sum of even
        // Fibonacci value
        while (ef2 <= limit)
        {

            // get next even value of
            // Fibonacci sequence
            long ef3 = 4 * ef2 + ef1;

            // If we go beyond limit,
            // we break loop
            if (ef3 > limit)
                break;

            // Move to next even number
            // and update sum
            ef1 = ef2;
            ef2 = ef3;
            sum += ef2;
        }

        return(int) sum;
    }

    // Driver code
    public static void Main ()
    {
        int limit = 400;
        Console.Write(evenFibSum(limit));

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Find the sum of all the
// even-valued terms in the
// Fibonacci sequence which
// do not exceed given limit.

// Returns sum of even Fibonacci
// numbers which are less than or
// equal to given limit.
function evenFibSum($limit)
{
    if ($limit < 2)
        return 0;

    // Initialize first two even
    // prime numbers and their sum
    $ef1 = 0; $ef2 = 2;
    $sum = $ef1 + $ef2;

    // calculating sum of
    // even Fibonacci value
    while ($ef2 <= $limit)
    {
        // get next even value of
        // Fibonacci sequence
        $ef3 = 4 * $ef2 + $ef1;

        // If we go beyond limit,
        // we break loop
        if ($ef3 > $limit)
            break;

        // Move to next even number
        // and update sum
        $ef1 = $ef2;
        $ef2 = $ef3;
        $sum += $ef2;
    }

    return $sum;
}

// Driver code
$limit = 400;
echo(evenFibSum($limit));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the sum of all the even-valued terms in
// the Fibonacci sequence which do not exceed
// given limit.

     // Returns sum of even Fibonacci numbers which are
    // less than or equal to given limit.
    function evenFibSum(limit)
    {
        if (limit < 2)
            return 0;

        // Initialize first two even prime numbers
        // and their sum
        let ef1 = 0, ef2 = 2;
        let sum = ef1 + ef2;

        // calculating sum of even Fibonacci value
        while (ef2 <= limit)
        {
            // get next even value of Fibonacci sequence
            let ef3 = 4 * ef2 + ef1;

            // If we go beyond limit, we break loop
            if (ef3 > limit)
                break;

            // Move to next even number and update sum
            ef1 = ef2;
            ef2 = ef3;
            sum += ef2;
        }

        return sum;
    }

// Function call

        let limit = 400;
        document.write(evenFibSum(limit));

</script>
```

**输出:**

```
188
```

本文由 **Nishant_singh(pintu)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
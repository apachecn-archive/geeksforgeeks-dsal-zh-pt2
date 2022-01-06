# 循环数

> 原文:[https://www.geeksforgeeks.org/cyclic-number/](https://www.geeksforgeeks.org/cyclic-number/)

一个[循环数](https://en.wikipedia.org/wiki/Cyclic_number)是一个整数，其中数字的循环排列是该数的连续倍数。最广为人知的是六位数 142857(请参见下面给出的示例解释)。
对于循环数，通常不包括以下小情况。

*   一位数，例如:5
*   重复数字，例如:555
*   重复循环数，例如:142857142857

给定一个数字，检查它是否是循环的。
**例:**

```
Input : 142857
Output : Yes
Explanation
    142857 × 1 = 142857
    142857 × 2 = 285714
    142857 × 3 = 428571
    142857 × 4 = 571428
    142857 × 5 = 714285
    142857 × 6 = 857142 
```

我们生成该数的所有循环排列，并检查每个排列是否除以非。我们还要检查三个条件。如果三个条件中的任何一个为真，我们返回假。

## C++

```
// Program to check if a number is cyclic.
#include <bits/stdc++.h>
using namespace std;

#define ull unsigned long long int

// Function to generate all cyclic permutations
// of a number
bool isCyclic(ull N)
{
    // Count digits and check if all
    // digits are same
    ull num = N;
    int count = 0;
    int digit = num % 10;
    bool allSame = true;
    while (num) {
        count++;
        if (num % 10 != digit)
            allSame = false;
        num = num / 10;
    }

    // If all digits are same, then
    // not considered cyclic.
    if (allSame == true)
        return false;

    // If counts of digits is even and
    // two halves are same, then the
    // number is not considered cyclic.
    if (count % 2 == 0) {
        ull halfPower = pow(10, count / 2);
        ull firstHalf = N % halfPower;
        ull secondHalf = N / halfPower;
        if (firstHalf == firstHalf && isCyclic(firstHalf))
            return false;
    }

    num = N;
    while (1) {

        // Following three lines generates a
        // circular pirmutation of a number.
        ull rem = num % 10;
        ull div = num / 10;
        num = (pow(10, count - 1)) * rem + div;

        // If all the permutations are checked
        // and we obtain original number exit
        // from loop.
        if (num == N)
            break;

        if (num % N != 0)
            return false;
    }

    return true;
}

// Driver Program
int main()
{
    ull N = 142857;
    if (isCyclic(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a number is cyclic

class GFG {
    // Function to generate all cyclic
    // permutations of a number
    static boolean isCyclic(long N)
    {
        // Count digits and check if all
        // digits are same
        long num = N;
        int count = 0;
        int digit = (int)(num % 10);
        boolean allSame = true;
        while (num > 0) {
            count++;
            if (num % 10 != digit)
                allSame = false;
            num = num / 10;
        }

        // If all digits are same, then
        // not considered cyclic.
        if (allSame == true)
            return false;

        // If counts of digits is even and
        // two halves are same, then the
        // number is not considered cyclic.
        if (count % 2 == 0) {
            long halfPower = (long)Math.pow(10, count / 2);
            long firstHalf = N % halfPower;
            long secondHalf = N / halfPower;
            if (firstHalf == firstHalf && isCyclic(firstHalf))
                return false;
        }

        num = N;
        while (true) {
            // Following three lines generates a
            // circular pirmutation of a number.
            long rem = num % 10;
            long div = num / 10;
            num = (long)(Math.pow(10, count - 1))
                      * rem
                  + div;

            // If all the permutations are checked
            // and we obtain original number exit
            // from loop.
            if (num == N)
                break;

            if (num % N != 0)
                return false;
        }

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        long N = 142857;
        if (isCyclic(N))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Program to check if
# a number is cyclic
# Function to generate
# all cyclic permutations
# of a number
def isCyclic(N):

    # Count digits and check if all
    # digits are same
    num = N
    count = 0
    digit =(num % 10)
    allSame = True

    while (num>0):
        count+= 1
        if (num % 10 != digit):
            allSame = False
        num = num // 10

    # If all digits are same, then
    # not considered cyclic.
    if (allSame == True):
        return False

    # If counts of digits is even and
    # two halves are same, then the
    # number is not considered cyclic.
    if (count % 2 == 0):

        halfPower = pow(10, count//2)
        firstHalf = N % halfPower
        secondHalf = N / halfPower
        if (firstHalf == firstHalf and
            isCyclic(firstHalf)):
            return False

    num = N
    while (True):

        # Following three lines
        # generates a
        # circular pirmutation
        # of a number.
        rem = num % 10
        div = num // 10
        num = pow(10, count - 1) * rem + div

        # If all the permutations
        # are checked
        # and we obtain original
        # number exit
        # from loop.
        if (num == N):
            break

        if (num % N != 0):
            return False

    return True

# Driver code

N = 142857
if (isCyclic(N)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Program to check if a number is cyclic
using System;

class GFG {

    // Function to generate all cyclic
    // permutations of a number
    static bool isCyclic(long N)
    {

        // Count digits and check if all
        // digits are same
        long num = N;
        int count = 0;
        int digit = (int)(num % 10);
        bool allSame = true;
        while (num > 0)
        {
            count++;
            if (num % 10 != digit)
                allSame = false;
            num = num / 10;
        }

        // If all digits are same, then
        // not considered cyclic.
        if (allSame == true)
            return false;

        // If counts of digits is even and
        // two halves are same, then the
        // number is not considered cyclic.
        if (count % 2 == 0) {
            long halfPower = (long)Math.Pow(10,
                                    count / 2);

            long firstHalf = N % halfPower;

            // long secondHalf = N / halfPower;
            if (firstHalf == firstHalf &&
                           isCyclic(firstHalf))
                return false;
        }

        num = N;
        while (true)
        {

            // Following three lines generates a
            // circular pirmutation of a number.
            long rem = num % 10;
            long div = num / 10;
            num = (long)(Math.Pow(10, count - 1))
                    * rem + div;

            // If all the permutations are checked
            // and we obtain original number exit
            // from loop.
            if (num == N)
                break;

            if (num % N != 0)
                return false;
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        long N = 142857;

        if (isCyclic(N))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to check if a number is cyclic

// Function to generate all cyclic
// permutations of a number
function isCyclic($N)
{
    // Count digits and check if all
    // digits are same
    $num = $N;
    $count = 0;
    $digit = ($num % 10);
    $allSame = true;

    while ($num > 0)
    {
        $count += 1;
        if ($num % 10 != $digit)
        $allSame = false;
        $num = (int)($num / 10);
    }

    // If all digits are same, then
    // not considered cyclic.
    if ($allSame == true)
        return false;

    // If counts of digits is even and
    // two halves are same, then the
    // number is not considered cyclic.
    if ($count % 2 == 0)
    {
        $halfPower = pow(10, (int)($count / 2));
        $firstHalf = $N % $halfPower;
        $secondHalf = $N / $halfPower;
        if ($firstHalf == $firstHalf &&
                 isCyclic($firstHalf))
            return false;
    }

    $num = $N;
    while (true)
    {

        // Following three lines generates a
        // circular pirmutation of a number.
        $rem = $num % 10;
        $div = (int)($num / 10);
        $num = pow(10, $count - 1) * $rem + $div;

        // If all the permutations are checked
        // and we obtain original number, exit
        // from loop.
        if ($num == $N)
            break;

        if ($num % $N != 0)
            return false;
    }
    return true;
}

// Driver code
$N = 142857;
if (isCyclic($N))
    print("Yes");
else
    print("No");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript Program to check if a number is cyclic

    // Function to generate all cyclic
    // permutations of a number
    function isCyclic(N)
    {
        // Count digits and check if all
        // digits are same
        let num = N;
        let count = 0;
        let digit = Math.floor(num % 10);
        let allSame = true;
        while (num > 0) {
            count++;
            if (num % 10 != digit)
                allSame = false;
            num = Math.floor(num / 10);
        }

        // If all digits are same, then
        // not considered cyclic.
        if (allSame == true)
            return false;

        // If counts of digits is even and
        // two halves are same, then the
        // number is not considered cyclic.
        if (count % 2 == 0) {
            let halfPower = Math.floor(Math.pow(10, count / 2));
            let firstHalf = Math.floor(N % halfPower);
            let secondHalf = Math.floor(N / halfPower);
            if (firstHalf == firstHalf && isCyclic(firstHalf))
                return false;
        }

        num = N;
        while (true) {
            // Following three lines generates a
            // circular pirmutation of a number.
            let rem = num % 10;
            let div = Math.floor(num / 10);
            num = Math.floor(Math.pow(10, count - 1))
                      * rem
                  + div;

            // If all the permutations are checked
            // and we obtain original number exit
            // from loop.
            if (num == N)
                break;

            if (num % N != 0)
                return false;
        }

        return true;
    }

// driver function

        let N = 142857;
        if (isCyclic(N))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**输出:**

```
Yes
```

**参考:**
[【https://en.wikipedia.org/wiki/Cyclic_number】](https://en.wikipedia.org/wiki/Cyclic_number)
本文由 [**Ajay Puri**](https://www.facebook.com/ajaygoswamiint) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现任何不正确的地方，或者你想分享更多关于上述话题的信息，请写评论..
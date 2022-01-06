# 求一个数除以该数的位数

> 原文:[https://www . geesforgeks . org/find-count-digit-number-divide-number/](https://www.geeksforgeeks.org/find-count-digit-number-divide-number/)

给定正整数 **n** 。任务是找出数字的位数，将数字 n 平均分配。
示例:

```
Input : n = 12
Output : 2
1 and 2 divide 12.

Input : n = 1012
Output : 3
1, 1 and 2 divide 1012.
```

这个想法是用模数 10 找到数字 n 的每个数字，然后检查它是否除以 n。相应地，递增计数器。请注意，数字可以是 0，所以请注意这种情况。
以下是该方法的实施:

## C++

```
// C++ program to count number of digits
// that divides the number.
#include <bits/stdc++.h>
using namespace std;

// Return the number of digits that divides
// the number.
int countDigit(int n)
{
    int temp = n, count = 0;
    while (temp != 0) {
        // Fetching each digit of the number
        int d = temp % 10;
        temp /= 10;

        // Checking if digit is greater than 0
        // and can divides n.
        if (d > 0 && n % d == 0)
            count++;
    }

    return count;
}

// Driven Program
int main()
{
    int n = 1012;

    cout << countDigit(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of digits
// that divides the number.

class Test {
    // Return the number of digits that divides
    // the number.
    static int countDigit(int n)
    {
        int temp = n, count = 0;
        while (temp != 0) {
            // Fetching each digit of the number
            int d = temp % 10;
            temp /= 10;

            // Checking if digit is greater than 0
            // and can divides n.
            if (d > 0 && n % d == 0)
                count++;
        }

        return count;
    }

    // Driver method
    public static void main(String args[])
    {
        int n = 1012;
        System.out.println(countDigit(n));
    }
}
```

## 蟒蛇 3

```
# Python3 code to count number of
# digits that divides the number.

# Return the number of digits
# that divides the number.
def countDigit (n):
    temp = n
    count = 0
    while temp != 0:

        # Fetching each digit
        # of the number
        d = temp % 10
        temp //= 10

        # Checking if digit is greater
        # than 0 and can divides n.
        if d > 0 and n % d == 0:
            count += 1
    return count

# Driven Code
n = 1012
print(countDigit(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to count number of digits
// that divides the number.
using System;

class GFG {

    // Return the number of digits that
    // divides the number.
    static int countDigit(int n)
    {
        int temp = n, count = 0;
        while (temp != 0) {

            // Fetching each digit of
            // the number
            int d = temp % 10;
            temp /= 10;

            // Checking if digit is
            // greater than 0 and can
            // divides n.
            if (d > 0 && n % d == 0)
                count++;
        }

        return count;
    }

    // Driver method
    public static void Main()
    {
        int n = 1012;

        Console.Write(countDigit(n));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number of digits
// that divides the number.

// Return the number of
// digits that divides
// the number.
function countDigit($n)
{
    $temp = $n;
    $count = 0;

    while ($temp != 0)
    {

        // Fetching each digit
        // of the number
        $d = $temp % 10;
        $temp /= 10;

        // Checking if digit
        // is greater than 0
        // and can divides n.
        if ($d > 0 && $n % $d == 0)
        $count++;
    }

    return $count;
}

    // Driver Code
    $n = 1012;
    echo countDigit($n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to count number of digits
// that divides the number. 
// Return the number of digits that divides
    // the number.

function countDigit(n)
{
    var temp = n, count = 0;
    while (temp != 0)
    {

        // Fetching each digit of the number
        var d = temp % 10;
        temp /= 10;

        // Checking if digit is greater than 0
        // and can divides n.
        if (d > 0 && n % d == 0)
            count++;
    }

    return count;
}

// Driver method
var n = 1012;
document.write(countDigit(n));

// This code is contributed by Amit Katiyar
</script>
```

输出:

```
3
```

**时间复杂度:** O(d)，其中 d 为数字中的位数。
**辅助空间:** O(1)

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
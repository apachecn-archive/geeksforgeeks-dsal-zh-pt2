# 仅查找由素数(2、3、5 和 7)组成的第 n 个数

> 原文:[https://www . geesforgeks . org/find-n-th-number-made-prime-digits/](https://www.geeksforgeeks.org/finding-n-th-number-made-prime-digits/)

给定一个数字“n”，我们需要找到第 n 个数字，其每个数字都是素数，即 2，3，5，7。换句话说，你必须找到这个序列的第 n 个数字。2、3、5、5、22、23……
假定这样发现的第 n 个数将小于等于 10^18
**例:**

```
Input  : 10
Output : 33
         2, 3, 5, 7, 22, 23, 25, 
         27, 32, 33

Input  : 21
Output : 222
```

有四个质数 2、3、5 和 7。第一个观察是 x 长度的由素数组成的数的数量是![4^x     ](img/a200ddf859b7288a04e10abd040d3598.png "Rendered by QuickLaTeX.com")，因为对于每个位置你有 4 个选择，所以总数是 4^x.
，所以长度= 1 到 len(即 2 或 3 或更多)的数的总数将是 4 *(4<sup>len</sup>–1)/3。
算法主要分为两步。

1.  我们利用上面的观察找到第 n 个数的位数。我们从 len = 0 开始，当它的值小于 4 *(4<sup>len</sup>–1)/3 时，不断递增。
2.  现在我们知道第 n 个数中的位数。我们也知道(len-1)位数的数字的计数。让这个计数为“prev_count”。现在我们一个接一个地在结果中找到数字。首先在第 I 个位置修正 2(假设到 i-1 的所有位置都已经被填充)，我们有 4^(len-I)可能的数字，并检查 2 是否是正确的候选，或者在放入 2 后检查数字计数是否大于或等于 n。如果是真的，那么 2 是正确的候选，如果不是真的，这意味着如果我们在第二个位置固定 2，那么只有 prev_count + 4^(len-i)数字可以被覆盖。所以用 4^(len-i 增加 prev_count ),重复这个步骤 3 次，检查 3 是否适合这个位置。如果不去 5。如果 5 也不合适，那就选 7。如果 2、3 和 5 不匹配，保证 7 会匹配，因为我们确定第 n 个这样的数字的长度是 len only。

下面是上述步骤的实现。

## C++

```
// C++ implementation for finding nth number
// made of prime digits only
#include <bits/stdc++.h>
using namespace std;

// Prints n-th number where each digit is a
// prime number
void nthprimedigitsnumber(long long n)
{
    // Finding the length of n-th number
    long long len = 1;

    // Count of numbers with len-1 digits
    long long prev_count = 0;
    while (true) {
        // Count of numbers with i digits
        long long curr_count = prev_count + pow(4, len);

        // if i is the length of such number
        // then n<4*(4^(i-1)-1)/3 and n>= 4*(4 ^ i-1)/3
        // if a valid i is found break the loop
        if (prev_count < n && curr_count >= n)
            break;

        // check for i + 1
        len++;

        prev_count = curr_count;
    }

    // Till now we have covered 'prev_count' numbers

    // Finding ith digit at ith place
    for (int i = 1; i <= len; i++) {
        // j = 1 means 2 j = 2 means ...j = 4 means 7
        for (long long j = 1; j <= 4; j++) {
            // if prev_count + 4 ^ (len-i) is less
            // than n, increase prev_count by 4^(x-i)
            if (prev_count + pow(4, len - i) < n)
                prev_count += pow(4, len - i);

            // else print the ith digit and break
            else {
                if (j == 1)
                    cout << "2";
                else if (j == 2)
                    cout << "3";
                else if (j == 3)
                    cout << "5";
                else if (j == 4)
                    cout << "7";
                break;
            }
        }
    }
    cout << endl;
}

// Driver function
int main()
{
    nthprimedigitsnumber(10);
    nthprimedigitsnumber(21);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for finding nth number
// made of prime digits only

import static java.lang.Math.pow;

class Test {

    // Prints n-th number where each digit is a
    // prime number
    static void nthprimedigitsnumber(long n)
    {
        // Finding the length of n-th number
        long len = 1;

        // Count of numbers with len-1 digits
        long prev_count = 0;
        while (true) {
            // Count of numbers with i digits
            long curr_count = (long)(prev_count + pow(4, len));

            // if i is the length of such number
            // then n<4*(4^(i-1)-1)/3 and n>= 4*(4 ^ i-1)/3
            // if a valid i is found break the loop
            if (prev_count < n && curr_count >= n)
                break;

            // check for i + 1
            len++;

            prev_count = curr_count;
        }

        // Till now we have covered 'prev_count' numbers

        // Finding ith digit at ith place
        for (int i = 1; i <= len; i++) {
            // j = 1 means 2 j = 2 means ...j = 4 means 7
            for (long j = 1; j <= 4; j++) {
                // if prev_count + 4 ^ (len-i) is less
                // than n, increase prev_count by 4^(x-i)
                if (prev_count + pow(4, len - i) < n)
                    prev_count += pow(4, len - i);

                // else print the ith digit and break
                else {
                    if (j == 1)
                        System.out.print("2");
                    else if (j == 2)
                        System.out.print("3");
                    else if (j == 3)
                        System.out.print("5");
                    else if (j == 4)
                        System.out.print("7");
                    break;
                }
            }
        }
        System.out.println();
    }

    // Driver method
    public static void main(String args[])
    {
        nthprimedigitsnumber(10);
        nthprimedigitsnumber(21);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation for
# finding nth number made of
# prime digits only
import math

# Prints n-th number where
# each digit is a prime number
def nthprimedigitsnumber(n):

    # Finding the length
    # of n-th number
    len = 1;

    # Count of numbers
    # with len-1 digits
    prev_count = 0;
    while(1):

        # Count of numbers
        # with i digits
        curr_count = (prev_count +
                      math.pow(4, len));

        # if i is the length of such
        # number then n<4*(4^(i-1)-1)/3
        # and n>= 4*(4 ^ i-1)/3 if a valid
        # i is found break the loop
        if (prev_count < n and
            curr_count >= n):
            break;

        # check for i + 1
        len += 1;

        prev_count = curr_count;

    # Till now we have covered
    # 'prev_count' numbers

    # Finding ith digit at ith place
    for i in range (1, len + 1):

        # j = 1 means 2 j = 2
        # means ...j = 4 means 7
        for j in range(1, 5):

            # if prev_count + 4 ^ (len-i)
            # is less than n, increase
            # prev_count by 4^(x-i)
            if (prev_count + pow(4, len - i) < n):
                prev_count += pow(4, len - i);

            # else print the ith
            # digit and break
            else:
                if (j == 1):
                    print("2", end = "");
                elif (j == 2):
                    print("3", end = "");
                elif (j == 3):
                    print("5", end = "");
                elif (j == 4):
                    print("7", end = "");
                break;
    print();

# Driver Code
nthprimedigitsnumber(10);
nthprimedigitsnumber(21);

# This code is contributed by mits
```

## C#

```
// C# implementation for finding nth
// number made of prime digits only
using System;

public class GFG {

    // Prints n-th number where each
    // digit is a prime number
    static void nthprimedigitsnumber(long n)
    {
        // Finding the length of n-th number
        long len = 1;

        // Count of numbers with len-1 digits
        long prev_count = 0;
        while (true) {

            // Count of numbers with i digits
            long curr_count = (long)(prev_count +
                               Math.Pow(4, len));

            // if i is the length of such number
            // then n<4*(4^(i-1)-1)/3 and n>= 4*(4 ^ i-1)/3
            // if a valid i is found break the loop
            if (prev_count < n && curr_count >= n)
                break;

            // check for i + 1
            len++;

            prev_count = curr_count;
        }

        // Till now we have covered 'prev_count' numbers

        // Finding ith digit at ith place
        for (int i = 1; i <= len; i++) {

            // j = 1 means 2 j = 2 means ...j = 4 means 7
            for (long j = 1; j <= 4; j++) {

                // if prev_count + 4 ^ (len-i) is less
                // than n, increase prev_count by 4^(x-i)
                if (prev_count + Math.Pow(4, len - i) < n)
                    prev_count += (long)Math.Pow(4, len - i);

                // else print the ith digit and break
                else {
                    if (j == 1)
                        Console.Write("2");
                    else if (j == 2)
                        Console.Write("3");
                    else if (j == 3)
                        Console.Write("5");
                    else if (j == 4)
                        Console.Write("7");
                    break;
                }
            }
        }
        Console.WriteLine();
    }

    // Driver method
    public static void Main()
    {
        nthprimedigitsnumber(10);
        nthprimedigitsnumber(21);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation for finding
// nth number made of prime digits only

// Prints n-th number where
// each digit is a prime number
function nthprimedigitsnumber($n)
{
    // Finding the length
    // of n-th number
    $len = 1;

    // Count of numbers
    // with len-1 digits
    $prev_count = 0;
    while (true)
    {
        // Count of numbers
        // with i digits
        $curr_count = $prev_count +
                      pow(4, $len);

        // if i is the length of such
        // number then n<4*(4^(i-1)-1)/3
        // and n>= 4*(4 ^ i-1)/3 if a valid
        // i is found break the loop
        if ($prev_count < $n &&
            $curr_count >= $n)
            break;

        // check for i + 1
        $len++;

        $prev_count = $curr_count;
    }

    // Till now we have covered
    // 'prev_count' numbers

    // Finding ith digit at ith place
    for ($i = 1; $i <= $len; $i++)
    {
        // j = 1 means 2 j = 2
        // means ...j = 4 means 7
        for ($j = 1; $j <= 4; $j++)
        {
            // if prev_count + 4 ^ (len-i)
            // is less than n, increase
            // prev_count by 4^(x-i)
            if ($prev_count +
                 pow(4, $len - $i) < $n)
                $prev_count += pow(4, $len - $i);

            // else print the ith
            // digit and break
            else
            {
                if ($j == 1)
                    echo "2";
                else if ($j == 2)
                    echo "3";
                else if ($j == 3)
                    echo "5";
                else if ($j == 4)
                    echo "7";
                break;
            }
        }
    }

echo "\n";
}

// Driver Code
nthprimedigitsnumber(10);
nthprimedigitsnumber(21);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript implementation for finding nth number
// made of prime digits only

// Prints n-th number where each digit is a
// prime number
function nthprimedigitsnumber(n)
{
    // Finding the length of n-th number
    var len = 1;

    // Count of numbers with len-1 digits
    var prev_count = 0;
    while (true) {
        // Count of numbers with i digits
        var curr_count = (prev_count + Math.pow(4, len));

        // if i is the length of such number
        // then n<4*(4^(i-1)-1)/3 and n>= 4*(4 ^ i-1)/3
        // if a valid i is found break the loop
        if (prev_count < n && curr_count >= n)
            break;

        // check for i + 1
        len++;

        prev_count = curr_count;
    }

    // Till now we have covered 'prev_count' numbers

    // Finding ith digit at ith place
    for (var i = 1; i <= len; i++) {
        // j = 1 means 2 j = 2 means ...j = 4 means 7
        for (var j = 1; j <= 4; j++) {
            // if prev_count + 4 ^ (len-i) is less
            // than n, increase prev_count by 4^(x-i)
            if (prev_count + Math.pow(4, len - i) < n)
                prev_count += Math.pow(4, len - i);

            // else print the ith digit and break
            else {
                if (j == 1)
                    document.write("2");
                else if (j == 2)
                    document.write("3");
                else if (j == 3)
                    document.write("5");
                else if (j == 4)
                    document.write("7");
                break;
            }
        }
    }
    document.write('<br>');
}

// Driver method
nthprimedigitsnumber(10);
nthprimedigitsnumber(21);

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
33
222
```

**备选方案(在 O(Log n)**T2 工作】

```
In this post, a O(log n) solution is discussed 
which is based on below pattern in numbers. The 
numbers can be seen
                                  ""
      /                |                    |                 \
     2                 3                    5                  7
 / |  | \           / | |  \             /  | | \          /  | |  \ 
22 23 25 27        32 33 35 37         52 53 55 57        72 73 75 77
/||\/||\/||\/||\   /||\/||\/||\/||\   /||\/||\/||\/||\   /||\/||\/||\/||\

We can notice following :
1st. 5th, 9th. 13th, ..... numbers have 2 as last digit.
2nd. 6th, 10th. 14th, ..... numbers have 3 as last digit.
3nd. 7th, 11th. 15th, ..... numbers have 5 as last digit.
4th. 8th, 12th. 16th, ..... numbers have 7 as last digit.
```

## C++

```
// CPP program to find n-th number with
// prime digits 2, 3 and 7
#include <algorithm>
#include <iostream>
#include <string>
using namespace std;

string nthprimedigitsnumber(int number)
{
    int rem;
    string num;
    while (number) {
        // remainder for check element position
        rem = number % 4;
        switch (rem) {

        // if number is 1st position in tree
        case 1:
            num.push_back('2');
            break;

        // if number is 2nd position in tree
        case 2:
            num.push_back('3');
            break;

        // if number is 3rd position in tree
        case 3:
            num.push_back('5');
            break;

        // if number is 4th position in tree
        case 0:
            num.push_back('7');
            break;
        }

        if (number % 4 == 0)
           number--;

        number = number / 4;
    }
    reverse(num.begin(), num.end());
    return num;
}

// Driver code
int main()
{
    int number = 21;
    cout << nthprimedigitsnumber(10) << "\n";
    cout << nthprimedigitsnumber(21) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th number with
// prime digits 2, 3 and 7
import java.util.*;
class GFG{
static String nthprimedigitsnumber(int number)
{
    int rem;
    String num="";
    while (number>0) {
        // remainder for check element position
        rem = number % 4;
        switch (rem) {

        // if number is 1st position in tree
        case 1:
            num+='2';
            break;

        // if number is 2nd position in tree
        case 2:
            num+='3';
            break;

        // if number is 3rd position in tree
        case 3:
            num+='5';
            break;

        // if number is 4th position in tree
        case 0:
            num+='7';
            break;
        }

       if (number % 4 == 0)
           number--;

        number = number / 4;
    }

    return new StringBuilder(num).reverse().toString();
}

// Driver code
public static void main(String[] args)
{
    int number = 21;
    System.out.println(nthprimedigitsnumber(10));
    System.out.println(nthprimedigitsnumber(21));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find n-th number
# with prime digits 2, 3 and 7
def nthprimedigitsnumber(number):

    num = "";
    while (number > 0):

        # remainder for check element position
        rem = number % 4;

        # if number is 1st position in tree
        if (rem == 1):
            num += '2';

        # if number is 2nd position in tree
        if (rem == 2):
            num += '3';

        # if number is 3rd position in tree
        if (rem == 3):
            num += '5';

        # if number is 4th position in tree
        if (rem == 0):
            num += '7';

        if (number % 4 == 0):
            number = number - 1

        number = number // 4;

    return num[::-1];

# Driver code
number = 21;
print(nthprimedigitsnumber(10));
print(nthprimedigitsnumber(number));

# This code is contributed by mits
```

## C#

```
// C# program to find n-th number with
// prime digits 2, 3 and 7
using System;
class GFG{
static string nthprimedigitsnumber(int number)
{
    int rem;
    string num="";
    while (number>0) {
        // remainder for check element position
        rem = number % 4;
        switch (rem) {

        // if number is 1st position in tree
        case 1:
            num+='2';
            break;

        // if number is 2nd position in tree
        case 2:
            num+='3';
            break;

        // if number is 3rd position in tree
        case 3:
            num+='5';
            break;

        // if number is 4th position in tree
        case 0:
            num+='7';
            break;
        }

       if (number % 4 == 0)
           number--;

        number = number / 4;
    }
    char[] st = num.ToCharArray();
    Array.Reverse(st);
    return new string(st);
}

// Driver code
static void Main()
{
    int number = 21;
    Console.WriteLine(nthprimedigitsnumber(10));
    Console.WriteLine(nthprimedigitsnumber(number));
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th number with
// prime digits 2, 3 and 7

function nthprimedigitsnumber($number)
{
    $num = "";
    while ($number > 0)
    {
        // remainder for check element position
        $rem = $number % 4;
        switch ($rem)
        {

            // if number is 1st position in tree
            case 1:
                $num .= '2';
                break;

            // if number is 2nd position in tree
            case 2:
                $num .= '3';
                break;

            // if number is 3rd position in tree
            case 3:
                $num .= '5';
                break;

            // if number is 4th position in tree
            case 0:
                $num .= '7';
                break;
        }

       if ($number % 4 == 0)
           $number--;

        $number = (int)($number / 4);
    }

    return strrev($num);
}

// Driver code
$number = 21;
print(nthprimedigitsnumber(10) . "\n");
print(nthprimedigitsnumber($number));

// This code is contributed by mits
```

## java 描述语言

```
<script>
    // Javascript program to find n-th number with prime digits 2, 3 and 7

    function nthprimedigitsnumber(number)
    {
        let rem;
        let num="";
        while (number>0) {
            // remainder for check element position
            rem = number % 4;
            switch (rem) {

            // if number is 1st position in tree
            case 1:
                num+='2';
                break;

            // if number is 2nd position in tree
            case 2:
                num+='3';
                break;

            // if number is 3rd position in tree
            case 3:
                num+='5';
                break;

            // if number is 4th position in tree
            case 0:
                num+='7';
                break;
            }

           if (number % 4 == 0)
               number--;

            number = parseInt(number / 4, 10);
        }
        let st = num.split('');
        st.reverse();
        return (st.join(""));
    }

    let number = 21;
    document.write(nthprimedigitsnumber(10) + "</br>");
    document.write(nthprimedigitsnumber(number));

</script>
```

**输出:**

```
33
222
```

本文由**阿育什·贾****德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
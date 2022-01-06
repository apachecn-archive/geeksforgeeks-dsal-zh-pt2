# 双基回文

> 原文:[https://www.geeksforgeeks.org/double-base-palindrome/](https://www.geeksforgeeks.org/double-base-palindrome/)

双基回文顾名思义，是一个有 2 个碱基的回文。其中一个基数是 10，即十进制，另一个基数是 k(可以是 2 或其他数字)。
**注:**回文数字，在任一基数中，不得包含前导零。
**例:**十进制数 585 = 1001001001 <sub>2</sub> (二进制)，两个碱基都是回文。

A **回文**是一个单词、短语、数字或其他字符序列，其向后读与向前读相同，如夫人或 12321。

找出所有小于 n 的数字的和，这些数字在 10 和 k 基数上是回文。

**示例:**

```
Input :  10 2
Output : 25
Explanation : (here n = 10 and k = 2)
              1 3 5 7 9 (they are all palindrome 
              in base 10 and 2) so sum is :
              1 + 3 + 5 + 7 + 9 = 25

Input :  100 2
Output : 157
Explanation : 1 + 3 + 5 + 7 + 9 + 33 + 99 = 157
```

**方法 1 :** 此方法简单。对于每一个小于 n 的数字:

*   检查它是否是 10 进制回文
*   如果是，则将其转换为基数 k
*   检查它是否是 k 基数的回文
*   如果是，那就加起来。

这个方法相当长，因为它检查每个数字是否是回文。所以，对于 1000000 这样大的数字，它会检查每个数字。
如果 k = 2，那么基数为 2 的回文只能是奇数，这可能会将比较减少到 1000000 / 2 = 500000(仍然很大)。

下面是上述方法的实现:

## C++

```
// CPP Program for Checking double base
// Palindrome.
#include <bits/stdc++.h>
using namespace std;

// converts number to base k by changing
// it into string.
string integer_to_string(int n, int base)
{
    string str;
    while (n > 0) {
        int digit = n % base;
        n /= base;
        str.push_back(digit + '0');
    }
    return str;
}

// function to check for palindrome
int isPalindrome(int i, int k)
{
    int temp = i;

    // m stores reverse of a number
    int m = 0;
    while (temp > 0) {
        m = temp % 10 + m * 10;
        temp /= 10;
    }

    // if reverse is equal to number
    if (m == i) {

        // converting to base k
        string str = integer_to_string(m, k);
        string str1 = str;

        // reversing number in base k
        reverse(str.begin(), str.end());

        // checking palindrome in base k
        if (str == str1) {
            return i;
        }
    }
    return 0;
}

// function to find sum of palindromes
void sumPalindrome(int n, int k){

    int sum = 0;
    for (int i = 1; i < n; i++) {
        sum += isPalindrome(i, k);
    }
    cout << "Total sum is " << sum;
}

// driver function
int main()
{
    int n = 100;
    int k = 2;

    sumPalindrome(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for Checking double base
// Palindrome.
import java.util.*;

class GFG{
// converts number to base k by changing
// it into string.
static String integer_to_string(int n, int base)
{
    String str="";
    while (n > 0) {
        int digit = n % base;
        n /= base;
        str+=(char)(digit+'0');
    }
    return str;
}

// function to check for palindrome
static int isPalindrome(int i, int k)
{
    int temp = i;

    // m stores reverse of a number
    int m = 0;
    while (temp > 0) {
        m = temp % 10 + m * 10;
        temp /= 10;
    }

    // if reverse is equal to number
    if (m == i) {

        // converting to base k
        String str = integer_to_string(m, k);
        StringBuilder sb = new StringBuilder(str);
        String str1=sb.reverse().toString();
        if (str.equals(str1)) {
            return i;
        }
    }
    return 0;
}

// function to find sum of palindromes
static void sumPalindrome(int n, int k){

    int sum = 0;
    for (int i = 1; i < n; i++) {
        sum += isPalindrome(i, k);
    }
    System.out.println("Total sum is "+sum);
}

// driver function
public static void main(String[] args)
{
    int n = 100;
    int k = 2;

    sumPalindrome(n, k);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 Program for Checking
# double base Palindrome.

# converts number to base
# k by changing it into string.
def integer_to_string(n, base):

    str = "";
    while (n > 0):
        digit = n % base;
        n = int(n / base);
        str = chr(digit + ord('0')) + str;
    return str;

# function to check for palindrome
def isPalindrome(i, k):
    temp = i;

    # m stores reverse of a number
    m = 0;
    while (temp > 0):
        m = (temp % 10) + (m * 10);
        temp = int(temp / 10);

    # if reverse is equal to number
    if (m == i):

        # converting to base k
        str = integer_to_string(m, k);
        str1 = str;

        # reversing number in base k
        # str=str[::-1];

        # checking palindrome
        # in base k
        if (str[::-1] == str1):
            return i;
    return 0;

# function to find sum of palindromes
def sumPalindrome(n, k):

    sum = 0;
    for i in range(n):
        sum += isPalindrome(i, k);
    print("Total sum is", sum);

# Driver code
n = 100;
k = 2;

sumPalindrome(n, k);

# This code is contributed
# by mits
```

## C#

```
// C# Program for Checking double base
// Palindrome.
using System;

class GFG{
// converts number to base k by changing
// it into string.
static string integer_to_string(int n, int base1)
{
    string str="";
    while (n > 0) {
        int digit = n % base1;
        n /= base1;
        str+=(char)(digit+'0');
    }
    return str;
}

// function to check for palindrome
static int isPalindrome(int i, int k)
{
    int temp = i;

    // m stores reverse of a number
    int m = 0;
    while (temp > 0) {
        m = temp % 10 + m * 10;
        temp /= 10;
    }

    // if reverse is equal to number
    if (m == i) {

        // converting to base k
        string str = integer_to_string(m, k);
        char[] ch = str.ToCharArray();
        Array.Reverse(ch);
        string str1=new String(ch);;
        if (str.Equals(str1)) {
            return i;
        }
    }
    return 0;
}

// function to find sum of palindromes
static void sumPalindrome(int n, int k){

    int sum = 0;
    for (int i = 1; i < n; i++) {
        sum += isPalindrome(i, k);
    }
    Console.WriteLine("Total sum is "+sum);
}

// driver function
 static void Main()
{
    int n = 100;
    int k = 2;

    sumPalindrome(n, k);
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program for Checking
// double base Palindrome.

// converts number to base
// k by changing it into string.
function integer_to_string($n, $base)
{
    $str = "";
    while ($n > 0)
    {
        $digit = $n % $base;
        $n = (int)($n / $base);
        $str = ($digit + '0') . $str;
    }
    return $str;
}

// function to check
// for palindrome
function isPalindrome($i, $k)
{
    $temp = $i;

    // m stores reverse
    // of a number
    $m = 0;
    while ($temp > 0)
    {
        $m = ($temp % 10) + ($m * 10);
        $temp = (int)($temp / 10);
    }

    // if reverse is
    // equal to number
    if ($m == $i)
    {

        // converting to base k
        $str = integer_to_string($m, $k);
        $str1 = $str;

        // reversing number in base k
        // $str=strrev($str);

        // checking palindrome
        // in base k
        if (strcmp(strrev($str), $str1) == 0)
        {
            return $i;
        }
    }
    return 0;
}

// function to find
// sum of palindromes
function sumPalindrome($n, $k)
{

    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $sum += isPalindrome($i, $k);
    }
    echo "Total sum is " . $sum;
}

// Driver code
$n = 100;
$k = 2;

sumPalindrome($n, $k);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for checking
// double base Palindrome.

// Converts number to base k by changing
// it into string.
function integer_to_string(n, base1)
{
    let str="";
    while (n > 0)
    {
        let digit = n % base1;
        n = parseInt(n / base1, 10);
        str += String.fromCharCode(digit +
                                   '0'.charCodeAt());
    }
    return str;
}

// Function to check for palindrome
function isPalindrome(i, k)
{
    let temp = i;

    // m stores reverse of a number
    let m = 0;
    while (temp > 0)
    {
        m = temp % 10 + m * 10;
        temp = parseInt(temp / 10, 10);
    }

    // If reverse is equal to number
    if (m == i)
    {

        // Converting to base k
        let str = integer_to_string(m, k);
        let ch = str.split('');
        ch.reverse();
        let str1 = ch.join("");

        if (str == str1)
        {
            return i;
        }
    }
    return 0;
}

// Function to find sum of palindromes
function sumPalindrome(n, k)
{
    let sum = 0;
    for(let i = 1; i < n; i++)
    {
        sum += isPalindrome(i, k);
    }
    document.write("Total sum is " + sum + "</br>");
}

// Driver code
let n = 100;
let k = 2;

sumPalindrome(n, k);

// This code is contributed by decode2207

</script>
```

**输出:**

```
Total sum is 157
```

**方法 2 :** 这个方法理解起来有点复杂，但是比方法 1 更高级。而不是检查回文是否有两个碱基。该方法在给定范围内生成回文。
假设我们有一个形式为 **123321** 的回文，那么前 3 位数字定义回文。但是 3 位数字 **123** 也定义回文 **12321** 。所以 3 位数 **123** 定义了一个 5 位数回文和一个 6 位数回文。由此得出，每个小于 k 的正数 <sup>n</sup> 生成两个小于 k 的回文 <sup>2n</sup> 。这适用于每个基数 k。例如:假设 k = 10，这是十进制。那么对于 n = 1，所有小于 10 的数字 <sup>n</sup> 在 10 <sup>2n</sup> 中有 2 个回文，1 个偶数长度，1 个奇数长度。这些是 1、11 或 2、22 或 3、33 等等。因此，对于 1000000，我们生成大约 2000 个回文，对于 10 <sup>8</sup> 我们生成大约 20000 个回文。

*   从 i=1 开始，生成它的奇数回文。
*   检查这个生成的奇数回文是否也是 k 基数的回文
*   如果是，那就把这个数加起来。
*   通过改变 i=i+1 重复以上三个步骤，直到最后生成的奇数回文已经越过极限。
*   现在，再次从 i=1 开始，生成它的偶数回文。
*   检查这个生成的偶数回文是否也是 k 基数的回文
*   如果是，那就把这个数加起来。
*   通过改变 i=i+1 重复以上三个步骤，直到最后生成的偶数回文已经越过极限。

下面是上述方法的实现:

## C++

```
// CPP Program for Checking double
// base Palindrome.
#include <bits/stdc++.h>
using namespace std;

// generates even and odd palindromes
int makePalindrome(int n, bool odd)
{
    int res = n;
    if (odd)
        n = n / 10;
    while (n > 0) {
        res = 10 * res + n % 10;
        n /= 10;
    }
    return res;
}

// Check if a number is palindrome
// in base k
bool isPalindrome(int n, int base)
{
    int reversed = 0;
    int temp = n;
    while (temp > 0) {
        reversed = reversed * base +
                   temp % base;
        temp /= base;
    }
    return reversed == n;
}

// function to print sum of Palindromes
void sumPalindrome(int n, int k){

    int sum = 0, i = 1;

    int p = makePalindrome(i, true);

    // loop for odd generation of
    // odd palindromes
    while (p < n) {
        if (isPalindrome(p, k))
            sum += p;
        i++;

        // cout << p << " ";
        p = makePalindrome(i, true);
    }

    i = 1;

    // loop for generation of
    // even palindromes
    p = makePalindrome(i, false);
    while (p < n) {
        if (isPalindrome(p, k))
            sum += p;
        i++;
        p = makePalindrome(i, false);
    }

    // result of all palindromes in
    // both bases.
    cout << "Total sum is " << sum
         << endl;
}

// driver code
int main()
{
    int n = 1000000, k = 2;
    sumPalindrome(n ,k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for Checking double
// base Palindrome.

public class GFG {

// generates even and odd palindromes
    static int makePalindrome(int n, boolean odd) {
        int res = n;
        if (odd) {
            n = n / 10;
        }
        while (n > 0) {
            res = 10 * res + n % 10;
            n /= 10;
        }
        return res;
    }

// Check if a number is palindrome
// in base k
    static boolean isPalindrome(int n, int base) {
        int reversed = 0;
        int temp = n;
        while (temp > 0) {
            reversed = reversed * base
                    + temp % base;
            temp /= base;
        }
        return reversed == n;
    }

// function to print sum of Palindromes
    static void sumPalindrome(int n, int k) {

        int sum = 0, i = 1;

        int p = makePalindrome(i, true);

        // loop for odd generation of
        // odd palindromes
        while (p < n) {
            if (isPalindrome(p, k)) {
                sum += p;
            }
            i++;

            // cout << p << " ";
            p = makePalindrome(i, true);
        }

        i = 1;

        // loop for generation of
        // even palindromes
        p = makePalindrome(i, false);
        while (p < n) {
            if (isPalindrome(p, k)) {
                sum += p;
            }
            i++;
            p = makePalindrome(i, false);
        }

        // result of all palindromes in
        // both bases.
        System.out.println("Total sum is " + sum);
    }

// driver code
    public static void main(String[] args) {
        int n = 1000000, k = 2;
        sumPalindrome(n, k);

    }
}
```

## 蟒蛇 3

```
# Python3 Program for Checking double
# base Palindrome.

# Function generates even and
# odd palindromes
def makePalindrome(n, odd):

    res = n;
    if (odd):
        n = int(n / 10);
    while (n > 0):
        res = 10 * res + n % 10;
        n = int(n / 10);
    return res;

# Check if a number is palindrome
# in base k
def isPalindrome(n, base):
    reversed = 0;
    temp = n;
    while (temp > 0):
        reversed = reversed * base + temp % base;
        temp = int(temp / base);

    return reversed == n;

# function to print sum of Palindromes
def sumPalindrome(n, k):

    sum = 0;
    i = 1;

    p = makePalindrome(i, True);

    # loop for odd generation of
    # odd palindromes
    while (p < n):
        if (isPalindrome(p, k)):
            sum += p;
        i += 1;

        p = makePalindrome(i, True);

    i = 1;

    # loop for generation of
    # even palindromes
    p = makePalindrome(i, False);
    while (p < n):
        if (isPalindrome(p, k)):
            sum += p;
        i += 1;
        p = makePalindrome(i, False);

    # result of all palindromes in
    # both bases.
    print("Total sum is", sum);

# Driver code
n = 1000000;
k = 2;
sumPalindrome(n, k);

# This code is contributed by mits
```

## C#

```
// C# Program for Checking double
// base1 Palindrome.

public class GFG {

// generates even and odd palindromes
    static int makePalindrome(int n, bool odd) {
        int res = n;
        if (odd) {
            n = n / 10;
        }
        while (n > 0) {
            res = 10 * res + n % 10;
            n /= 10;
        }
        return res;
    }

// Check if a number is palindrome
// in base1 k
    static bool isPalindrome(int n, int base1) {
        int reversed = 0;
        int temp = n;
        while (temp > 0) {
            reversed = reversed * base1 + temp % base1;
            temp /= base1;
        }
        return reversed == n;
    }

// function to print sum of Palindromes
    static void sumPalindrome(int n, int k) {

        int sum = 0, i = 1;

        int p = makePalindrome(i, true);

        // loop for odd generation of
        // odd palindromes
        while (p < n) {
            if (isPalindrome(p, k)) {
                sum += p;
            }
            i++;

            p = makePalindrome(i, true);
        }

        i = 1;

        // loop for generation of
        // even palindromes
        p = makePalindrome(i, false);
        while (p < n) {
            if (isPalindrome(p, k)) {
                sum += p;
            }
            i++;
            p = makePalindrome(i, false);
        }

        // result of all palindromes in
        // both base1s.
        System.Console.WriteLine("Total sum is " + sum);
    }

// driver code
    public static void Main() {
        int n = 1000000, k = 2;
        sumPalindrome(n, k);

    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program for Checking double
// base Palindrome.

// Function generates even and
// odd palindromes
function makePalindrome($n, $odd)
{
    $res = $n;
    if ($odd)
    {
        $n = (int)($n / 10);
    }
    while ($n > 0)
    {
        $res = 10 * $res + $n % 10;
        $n = (int)($n / 10);
    }
    return $res;
}

// Check if a number is palindrome
// in base k
function isPalindrome($n, $base)
{
    $reversed = 0;
    $temp = $n;
    while ($temp > 0)
    {
        $reversed = $reversed * $base +
                        $temp % $base;
        $temp = (int)($temp / $base);
    }
    return $reversed == $n;
}

// function to print sum of Palindromes
function sumPalindrome($n, $k)
{
    $sum = 0; $i = 1;

    $p = makePalindrome($i, true);

    // loop for odd generation of
    // odd palindromes
    while ($p < $n)
    {
        if (isPalindrome($p, $k))
        {
            $sum += $p;
        }
        $i++;

        $p = makePalindrome($i, true);
    }

    $i = 1;

    // loop for generation of
    // even palindromes
    $p = makePalindrome($i, false);
    while ($p < $n)
    {
        if (isPalindrome($p, $k))
        {
            $sum += $p;
        }
        $i++;
        $p = makePalindrome($i, false);
    }

    // result of all palindromes in
    // both bases.
    echo("Total sum is " . $sum);
}

// Driver code
$n = 1000000; $k = 2;
sumPalindrome($n, $k);

// This code is contributed
// by Mukul Singh.
?>
```

## java 描述语言

```
<script>
// javascript Program for Checking var
// base Palindrome.

// generates even and odd palindromes
    function makePalindrome(n, odd) {
        var res = n;
        if (odd) {
            n = parseInt(n / 10);
        }
        while (n > 0) {
            res = 10 * res + n % 10;
            n = parseInt(n / 10);
        }
        return res;
    }

// Check if a number is palindrome
// in base k
    function isPalindrome(n , base) {
        var reversed = 0;
        var temp = n;
        while (temp > 0) {
            reversed = reversed * base
                    + temp % base;
            temp = parseInt(temp/base);
        }
        return reversed == n;
    }

// function to print sum of Palindromes
    function sumPalindrome(n , k) {

        var sum = 0, i = 1;

        var p = makePalindrome(i, true);

        // loop for odd generation of
        // odd palindromes
        while (p < n) {
            if (isPalindrome(p, k)) {
                sum += p;
            }
            i++;

            // cout << p << " ";
            p = makePalindrome(i, true);
        }

        i = 1;

        // loop for generation of
        // even palindromes
        p = makePalindrome(i, false);
        while (p < n) {
            if (isPalindrome(p, k)) {
                sum += p;
            }
            i++;
            p = makePalindrome(i, false);
        }

        // result of all palindromes in
        // both bases.
        document.write("Total sum is " + sum);
    }

// driver code
var n = 1000000, k = 2;
sumPalindrome(n, k);

// This code contributed by Princi Singh
</script>
```

**输出:**

```
Total sum is 872187 
```

本文由 [**舒巴姆拉纳**](https://auth.geeksforgeeks.org/profile.php?user=shubham_rana_77&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
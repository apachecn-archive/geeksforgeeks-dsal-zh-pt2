# 邪恶号

> 原文:[https://www.geeksforgeeks.org/evil-number/](https://www.geeksforgeeks.org/evil-number/)

恶数是一个非负数，它的二进制展开式中有偶数个 1。(二进制扩展–是二进制数字系统或基数为 2 的数字系统中数字的表示，它使用两个不同的符号来表示数值:通常是 0(零)和 1(一))。

**恶数:**非**非**恶的数称为恶数。给定一个数字，任务是检查它是恶数还是恶数。

**示例:**

```
Input : 3
Output : Evil Number
Explanation: Binary expansion of 3 is 11,
the number of 1s in this is 2 i.e even. 

Input : 16
Output : Odious Number(not an evil number)
Explanation: Binary expansion of 16 = 10000, 
having number of 1s =1 i.e odd.

Input : 23
Output : Evil Number
Explanation: Binary expansion of 23 is 10111,
the number of 1s in this is 4 i.e even. 
```

## C++

```
// C/C++ program to check if a number is
// Evil number or Odious Number
#include <iostream>
using namespace std;
#include <math.h>

// returns number of 1s from the binary number
int count_one(int n)
{
    int c_one = 0;
    while (n != 0) {
        int rem = n % 10;

        // counting 1s
        if (rem == 1)
            c_one = c_one + 1;
        n = n / 10;
    }
    return c_one;
}

// Check if number is evil or not
int checkEvil(int n)
{
    int i = 0, bin = 0, n_one = 0;

    // converting n to binary form
    while (n != 0) {
        // calculating remainder
        int r = n % 2;

        // storing the remainders in binary
        // form as a number
        bin = bin + r * (int)(pow(10, i));
        n = n / 2;
    }

    // Calling the count_one function to count
    // and return number of 1s in bin
    n_one = count_one(bin);
    if (n_one % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver Code
int main(void)
{
    int i, check, num;
    num = 32;
    check = checkEvil(num);
    if (check == 1)
        cout << num << " is Evil Number\n";
    else
        cout << num << " is Odious Number\n";
    return 0;
}

// This code is contributed by Nikita Tiwari.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is
// Evil number or Odious Number

class GFG {
    // returns number of 1s from the binary number
    static int count_one(int n)
    {
        int c_one = 0;
        while (n != 0) {
            int rem = n % 10;

            // counting 1s
            if (rem == 1)
                c_one = c_one + 1;
            n = n / 10;
        }
        return c_one;
    }

    // Check if number is evil or not
    static int checkEvil(int n)
    {
        int i = 0, bin = 0, n_one = 0;

        // converting n to binary form
        while (n != 0) {
            // calculating remainder
            int r = n % 2;

            // storing the remainders in binary
            // form as a number
            bin = bin + r * (int)(Math.pow(10, i));
            n = n / 2;
        }

        // Calling the count_one function to count
        // and return number of 1s in bin
        n_one = count_one(bin);
        if (n_one % 2 == 0)
            return 1;
        else
            return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int i, check, num;
        num = 32;
        check = checkEvil(num);
        if (check == 1)
            System.out.println(num + " is Evil Number");
        else
            System.out.println(num + " is Odious Number");
    }
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 计算机编程语言

```
# Python program to check if a number is
# Evil number or Odious number

# returns number of 1s from the binary number
def count_one(n):
    c_one = 0
    while n != 0:
        rem = n % 10

        # Counting 1s
        if rem == 1:
            c_one = c_one + 1
        n = n / 10

    return c_one

# Check if number is evil or not
def checkEvil(n):
    i = 0
    binary = 0

    # Converting n to binary form
    while n != 0:
        r = n % 2
        # Calculating Remainder
        # Storing the remainders in binary
        # form as a number
        binary = binary + r*(int(10**i))
        n = n / 2

    # Calling the count_one function to count
    # and return number of 1s in bin
    n_one = count_one(binary)
    if n_one % 2 == 0:
        return True
    return False

# Driver Code
num = 32
check = checkEvil(num)
if check:
    print num, "is Evil Number"
else:
    print num, "is Odious Number"       

# Contributed by Harshit Agrawal       
```

## C#

```
// C# program to check if a number is
// Evil number or Odious Number
using System;

class GFG {

    // Returns number of 1s from
    // the binary number
    static int count_one(int n)
    {
        int c_one = 0;
        while (n != 0) {
            int rem = n % 10;

            // counting 1s
            if (rem == 1)
                c_one = c_one + 1;
            n = n / 10;
        }
        return c_one;
    }

    // Check if number is evil or not
    static int checkEvil(int n)
    {
        int i = 0, bin = 0, n_one = 0;

        // converting n to binary form
        while (n != 0) {
            // calculating remainder
            int r = n % 2;

            // storing the remainders in
            // binary form as a number
            bin = bin + r * (int)(Math.Pow(10, i));
            n = n / 2;
        }

        // Calling the count_one function to count
        // and return number of 1s in bin
        n_one = count_one(bin);
        if (n_one % 2 == 0)
            return 1;
        else
            return 0;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int check, num;
        num = 32;
        check = checkEvil(num);
        if (check == 1)
            Console.WriteLine(num + " is Evil Number");
        else
            Console.WriteLine(num + " is Odious Number");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is Evil number
// or Odious Number

// returns number of 1s
// from the binary number
function count_one($n)
{
    $c_one = 0;
    while ($n != 0)
    {
        $rem = $n % 10;

        // counting 1s
        if ($rem == 1)
            $c_one = $c_one + 1;
        $n = $n / 10;
    }
    return $c_one;
}

// Check if number
// is evil or not
function checkEvil($n)
{
    $i = 0; $bin = 0; $n_one = 0;

    // converting n
    // to binary form
    while ($n != 0)
    {
        // calculating remainder
        $r = $n % 2;

        // storing the remainders
        // in binary form as a number
        $bin = $bin + $r * (pow(10, $i));
        $n = $n / 2;
    }

    // Calling the count_one
    // function to count and
    // return number of 1s in bin
    $n_one = count_one($bin);
    if ($n_one % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver Code
$i; $check; $num;
$num = 32;
$check = checkEvil($num);
if ($check == 1)
    echo $num, " is Evil Number\n";
else
    echo $num, " is Odious Number\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number
// is Evil number or Odious Number

// Returns number of 1s from
// the binary number
function count_one(n)
{
    let c_one = 0;

    while (n != 0)
    {
        let rem = n % 10;

        // Counting 1s
        if (rem == 1)
            c_one = c_one + 1;

        n = parseInt(n / 10, 10);
    }
    return c_one;
}

// Check if number is evil or not
function checkEvil(n)
{
    let i = 0, bin = 0, n_one = 0;

    // Converting n to binary form
    while (n != 0)
    {

        // Calculating remainder
        let r = n % 2;

        // Storing the remainders in
        // binary form as a number
        bin = bin + r * (Math.pow(10, i));
        n = parseInt(n / 2, 10);
    }

    // Calling the count_one function to count
    // and return number of 1s in bin
    n_one = count_one(bin);

    if (n_one % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver code
let check, num;
num = 32;
check = checkEvil(num);

if (check == 1)
  document.write(num + " is Evil Number");
else
  document.write(num + " is Odious Number");

// This code is contributed by suresh07  

</script>
```

**输出:**

```
32 is Odius Number
```

本文由**尼基塔·蒂瓦里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
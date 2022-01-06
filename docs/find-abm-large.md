# 发现(a^b)%m 其中‘a’很大

> 原文:[https://www.geeksforgeeks.org/find-abm-large/](https://www.geeksforgeeks.org/find-abm-large/)

给定三个数字 a、b 和 m，其中 1<=b,m<=10^6 和 a 可能非常大，最多包含 10^6 数字。任务是找到(a^b)%m.

示例:

```
Input  : a = 3, b = 2, m = 4
Output : 1
Explanation : (3^2)%4 = 9%4 = 1

Input : a = 987584345091051645734583954832576, b = 3, m = 11
Output: 10
```

这个问题基本上是基于模运算的。我们可以把 **(a^b) % m** 写成**(a % m)*(a % m)*(a % m)*……(a % m)，b 乘以**。下面是解决这个问题的算法:

*   因为“a”很大，所以将“a”读作字符串。
*   现在我们试着减少 a。我们用 m 对 a 取模一次，即:ans = a % m，这样现在 **ans=a%m** 位于 1 到 10^6 的整数范围之间，即；1 < = a%m < = 10^6.
*   现在将 **ans** 乘以 **b-1** 次，同时取中间乘法结果与 m 的模，因为 **ans** 的中间乘法可能超出整数范围，会产生错误答案。

## C++

```
// C++ program to find (a^b) mod m for a large 'a'
#include<bits/stdc++.h>
using namespace std;

// utility function to calculate a%m
unsigned int aModM(string s, unsigned int mod)
{
    unsigned int number = 0;
    for (unsigned int i = 0; i < s.length(); i++)
    {
        // (s[i]-'0') gives the digit value and form
        // the number
        number = (number*10 + (s[i] - '0'));
        number %= mod;
    }
    return number;
}

// Returns find (a^b) % m
unsigned int ApowBmodM(string &a, unsigned int b,
                                  unsigned int m)
{
    // Find a%m
    unsigned int ans = aModM(a, m);
    unsigned int mul = ans;

    // now multiply ans by b-1 times and take
    // mod with m
    for (unsigned int i=1; i<b; i++)
        ans = (ans*mul) % m;

    return ans;
}

// Driver program to run the case
int main()
{
    string a = "987584345091051645734583954832576";
    unsigned int b=3, m=11;
    cout << ApowBmodM(a, b, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find (a^b) mod m for a large 'a'

public class GFG {

    // utility function to calculate a%m
    static int aModM(String s, int mod)
    {
        int number = 0;
        for (int i = 0; i < s.length(); i++)
        {

            // (s[i]-'0') gives the digit
            // value and form the number
            number = (number * 10 );
            int x = Character.getNumericValue(s.charAt(i));
            number = number + x;
            number %= mod;
        }

        return number;
    }

    // Returns find (a^b) % m
    static int ApowBmodM(String a, int b, int m)
    {

        // Find a%m
        int ans = aModM(a, m);
        int mul = ans;

        // now multiply ans by b-1 times
        // and take mod with m
        for (int i = 1; i < b; i++)
            ans = (ans * mul) % m;

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        String a = "987584345091051645734583954832576";
        int b = 3, m = 11;
        System.out.println(ApowBmodM(a, b, m));
    }
}

// This code is contributed by Sam007
```

## 计算机编程语言

```
# Python program to find (a^b) mod m for a large 'a'
def aModM(s, mod):
    number = 0

    # convert string s[i] to integer which gives
    # the digit value and form the number
    for i in range(len(s)):
        number = (number*10 + int(s[i]))
        number = number % m

    return number

# Returns find (a^b) % m
def ApowBmodM(a, b, m):

    # Find a%m   
    ans = aModM(a, m)
    mul = ans

    # now multiply ans by b-1 times and take
    # mod with m
    for i in range(1,b):
        ans = (ans*mul) % m

    return ans

# Driver program to run the case
a = "987584345091051645734583954832576"
b, m = 3, 11
print ApowBmodM(a, b, m)
```

## C#

```
// C# program to find (a^b) mod m
// for a large 'a'
using System;

class GFG {

// utility function to calculate a%m
static int aModM(string s, int mod)
{
    int number = 0;
    for (int i = 0; i < s.Length; i++)
    {

        // (s[i]-'0') gives the digit
        // value and form the number
        number = (number * 10 );
        int x = (int)(s[i] - '0');
        number = number + x;
        number %= mod;
    }
    return number;
}

// Returns find (a^b) % m
static int ApowBmodM(string a, int b,
                              int m)
{

    // Find a%m
    int ans = aModM(a, m);
    int mul = ans;

    // now multiply ans by b-1 times
    // and take mod with m
    for (int i = 1; i < b; i++)
        ans = (ans * mul) % m;

    return ans;
}

// Driver Code
public static void Main()
{
    string a = "987584345091051645734583954832576";
    int b=3, m=11;
    Console.Write(ApowBmodM(a, b, m));

}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find (a^b)
// mod m for a large 'a'

// utility function to
// calculate a%m
function aModM($s, $mod)
{
    $number = 0;
    for ($i = 0; $i < strlen($s); $i++)
    {

        // (s[i]-'0') gives the digit
        // value and form the number
        $number = ($number * 10 +
                  ($s[$i] - '0'));
        $number %= $mod;
    }
    return $number;
}

// Returns find (a^b) % m
function ApowBmodM($a, $b,$m)
{

    // Find a%m
    $ans = aModM($a, $m);
    $mul = $ans;

    // now multiply ans by
    // b-1 times and take
    // mod with m
    for ($i = 1; $i < $b; $i++)
        $ans = ($ans * $mul) % $m;

    return $ans;
}

    // Driver code
    $a = "987584345091051645734583954832576";
    $b = 3;
    $m = 11;
    echo ApowBmodM($a, $b, $m);
    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find (a^b) mod m
// for a large 'a'

// Utility function to calculate a%m
function aModM(s, mod)
{
    let number = 0;
    for(let i = 0; i < s.length; i++)
    {

        // (s[i]-'0') gives the digit
        // value and form the number
        number = (number * 10 );
        let x = (s[i] - '0');
        number = number + x;
        number %= mod;
    }
    return number;
}

// Returns find (a^b) % m
function ApowBmodM(a, b, m)
{

    // Find a%m
    let ans = aModM(a, m);
    let mul = ans;

    // Now multiply ans by b-1 times
    // and take mod with m
    for(let i = 1; i < b; i++)
        ans = (ans * mul) % m;

    return ans;
}

// Driver Code
let a = "987584345091051645734583954832576";
let b = 3, m = 11;

document.write(ApowBmodM(a, b, m));

// This code is contributed by souravghosh0416

</script>
```

**输出:**

```
10
```

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
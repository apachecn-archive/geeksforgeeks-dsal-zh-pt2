# 给定二进制字符串的十进制表示是否能被 10 整除

> 原文:[https://www . geesforgeks . org/十进制-表示-给定-二进制-字符串-可除-10-not/](https://www.geeksforgeeks.org/decimal-representation-given-binary-string-divisible-10-not/)

问题是检查给定二进制数的十进制表示是否能被 10 整除。请注意，这个数字可能非常大，甚至可能不适合 long long int。这种方法应该使得乘法和除法运算的数量为零或最小。输入中没有前导 0。
**例:**

```
Input : 101000
Output : Yes
(101000)<sub>2 = (40)10</sub>
and 40 is divisible by 10.

Input : 11000111001110
Output : Yes
```

**方法:**首先我们需要知道幂(2，i) = 2，4，8，6 最后一位，如果 i % 4 分别等于 1，2，3，0，其中 I 大于等于 1。因此，在二进制表示中，我们需要知道数字“1”从右边的位置，以便知道它将乘以的 2 的完美幂。这将帮助我们获得所需的 2 的完美幂的最后一位。我们可以将这些数字相加，然后检查总和的最后一个数字是否为 0，这意味着该数字是否可被 10 整除。请注意，如果二进制表示中的最后一个数字是“1”，那么它表示奇数，因此不能被 10 整除。

## C++

```
// C++ implementation to check whether decimal
// representation of given binary number is
// divisible by 10 or not
#include <bits/stdc++.h>
using namespace std;

// function to check whether decimal representation
// of given binary number is divisible by 10 or not
bool isDivisibleBy10(string bin)
{
    int n = bin.size();

    // if last digit is '1', then
    // number is not divisible by 10
    if (bin[n-1] == '1')
        return false;

    // to accumulate the sum of last digits
    // in perfect powers of 2
    int sum = 0;

    // traverse from the 2nd last up to 1st digit
    // in 'bin'
    for (int i=n-2; i>=0; i--)   
    {
        // if digit in '1'
        if (bin[i] == '1')
        {
            // calculate digit's position from
            // the right
            int posFromRight = n - i - 1;

            // according to the digit's position,
            // obtain the last digit of the applicable
            // perfect power of 2
            if (posFromRight % 4 == 1)
                sum = sum + 2;
            else if (posFromRight % 4 == 2)
                sum = sum + 4;
            else if (posFromRight % 4 == 3)
                sum = sum + 8;
            else if (posFromRight % 4 == 0)
                sum = sum + 6;           
        }
    }

    // if last digit is 0, then
    // divisible by 10
    if (sum % 10 == 0)
        return true;

    // not divisible by 10   
    return false;   
}

// Driver program to test above
int main()
{
    string bin = "11000111001110";

    if (isDivisibleBy10(bin))
        cout << "Yes";
    else
        cout << "No";   

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether decimal
// representation of given binary number is
// divisible by 10 or not
import java.util.*;

class GFG {

    // function to check whether decimal
    // representation of given binary number
    // is divisible by 10 or not
    static boolean isDivisibleBy10(String bin)
    {
        int n = bin.length();

        // if last digit is '1', then
        // number is not divisible by 10
        if (bin.charAt(n - 1) == '1')
            return false;

        // to accumulate the sum of last
        // digits in perfect powers of 2
        int sum = 0;

        // traverse from the 2nd last up to
        // 1st digit in 'bin'
        for (int i = n - 2; i >= 0; i--)   
        {
            // if digit in '1'
            if (bin.charAt(i) == '1')
            {
                // calculate digit's position
                // from the right
                int posFromRight = n - i - 1;

                // according to the digit's
                // position, obtain the last
                // digit of the applicable
                // perfect power of 2
                if (posFromRight % 4 == 1)
                    sum = sum + 2;
                else if (posFromRight % 4 == 2)
                    sum = sum + 4;
                else if (posFromRight % 4 == 3)
                    sum = sum + 8;
                else if (posFromRight % 4 == 0)
                    sum = sum + 6;           
            }
        }

        // if last digit is 0, then
        // divisible by 10
        if (sum % 10 == 0)
            return true;

        // not divisible by 10   
        return false;   
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        String bin = "11000111001110";

        if (isDivisibleBy10(bin))
            System.out.print("Yes");
        else
            System.out.print("No");  

        }
    }

// This code is contributed by Arnav Kr. Mandal.   
```

## 计算机编程语言

```
# Python implementation to check whether
# decimal representation of given binary
# number is divisible by 10 or not

# function to check whether decimal
# representation of given binary number
# is divisible by 10 or not
def isDivisibleBy10(bin) :
    n = len(bin)

    #if last digit is '1', then
    # number is not divisible by 10
    if (bin[n - 1] == '1') :
        return False

    # to accumulate the sum of last
    # digits in perfect powers of 2
    sum = 0

    #traverse from the 2nd last up to
    # 1st digit in 'bin'

    i = n - 2
    while i >= 0 :

        # if digit in '1'
        if (bin[i] == '1') :
            # calculate digit's position
            # from the right
            posFromRight = n - i - 1

            #according to the digit's
            # position, obtain the last
            # digit of the applicable
            # perfect power of 2
            if (posFromRight % 4 == 1) :
                sum = sum + 2
            elif (posFromRight % 4 == 2) :
                sum = sum + 4
            elif (posFromRight % 4 == 3) :
                sum = sum + 8
            elif (posFromRight % 4 == 0) :
                sum = sum + 6

        i = i - 1

    # if last digit is 0, then
    # divisible by 10
    if (sum % 10 == 0) :
        return True

    # not divisible by 10
    return False

# Driver program to test above function

bin = "11000111001110"
if (isDivisibleBy10(bin)== True) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation to check whether decimal
// representation of given binary number is
// divisible by 10 or not
using System;

class GFG {

    // function to check whether decimal
    // representation of given binary number
    // is divisible by 10 or not
    static bool isDivisibleBy10(String bin)
    {
        int n = bin.Length;

        // if last digit is '1', then
        // number is not divisible by 10
        if (bin[n - 1] == '1')
            return false;

        // to accumulate the sum of last
        // digits in perfect powers of 2
        int sum = 0;

        // traverse from the 2nd last up to
        // 1st digit in 'bin'
        for (int i = n - 2; i >= 0; i--) {

            // if digit in '1'
            if (bin[i] == '1') {

                // calculate digit's position
                // from the right
                int posFromRight = n - i - 1;

                // according to the digit's
                // position, obtain the last
                // digit of the applicable
                // perfect power of 2
                if (posFromRight % 4 == 1)
                    sum = sum + 2;
                else if (posFromRight % 4 == 2)
                    sum = sum + 4;
                else if (posFromRight % 4 == 3)
                    sum = sum + 8;
                else if (posFromRight % 4 == 0)
                    sum = sum + 6;
            }
        }

        // if last digit is 0, then
        // divisible by 10
        if (sum % 10 == 0)
            return true;

        // not divisible by 10
        return false;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        String bin = "11000111001110";

        if (isDivisibleBy10(bin))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// check whether decimal
// representation of given
// binary number is divisible
// by 10 or not

// function to check whether
// decimal representation of
// given binary number is
// divisible by 10 or not
function isDivisibleBy10($bin)
{
    $n = strlen($bin);

    // if last digit is '1',
    // then number is not
    // divisible by 10
    if ($bin[$n - 1] == '1')
        return false;

    // to accumulate the sum
    // of last digits in
    // perfect powers of 2
    $sum = 0;

    // traverse from the 2nd
    // last up to 1st digit
    // in 'bin'
    for ($i = $n - 2; $i >= 0; $i--)
    {
        // if digit in '1'
        if ($bin[$i] == '1')
        {
            // calculate digit's
            // position from the right
            $posFromRight = $n - $i - 1;

            // according to the digit's
            // position, obtain the last
            // digit of the applicable
            // perfect power of 2
            if ($posFromRight % 4 == 1)
                $sum = $sum + 2;
            else if ($posFromRight % 4 == 2)
                $sum = $sum + 4;
            else if ($posFromRight % 4 == 3)
                $sum = $sum + 8;
            else if ($posFromRight % 4 == 0)
                $sum = $sum + 6;        
        }
    }

    // if last digit is 0, then
    // divisible by 10
    if ($sum % 10 == 0)
        return true;

    // not divisible by 10
    return false;
}

// Driver Code
$bin = "11000111001110";
if(isDivisibleBy10($bin))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// Javascript implementation to check whether decimal
// representation of given binary number is
// divisible by 10 or not

    // function to check whether decimal
    // representation of given binary number
    // is divisible by 10 or not
    function isDivisibleBy10(bin)
    {
        let n = bin.length;

        // if last digit is '1', then
        // number is not divisible by 10
        if (bin[n - 1] == '1')
            return false;

        // to accumulate the sum of last
        // digits in perfect powers of 2
        let sum = 0;

        // traverse from the 2nd last up to
        // 1st digit in 'bin'
        for (let i = n - 2; i >= 0; i--)   
        {
            // if digit in '1'
            if (bin[i] == '1')
            {
                // calculate digit's position
                // from the right
                let posFromRight = n - i - 1;

                // according to the digit's
                // position, obtain the last
                // digit of the applicable
                // perfect power of 2
                if (posFromRight % 4 == 1)
                    sum = sum + 2;
                else if (posFromRight % 4 == 2)
                    sum = sum + 4;
                else if (posFromRight % 4 == 3)
                    sum = sum + 8;
                else if (posFromRight % 4 == 0)
                    sum = sum + 6;           
            }
        }

        // if last digit is 0, then
        // divisible by 10
        if (sum % 10 == 0)
            return true;

        // not divisible by 10   
        return false;   
    }

// driver function

        let bin = "11000111001110";

        if (isDivisibleBy10(bin))
            document.write("Yes");
        else
            document.write("No");  

</script>   
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)，其中 n 为二进制数中的位数。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
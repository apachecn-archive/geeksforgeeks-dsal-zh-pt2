# 给定二进制字符串的十进制表示是否可被 5 整除

> 原文:[https://www . geesforgeks . org/十进制-表示-给定-二进制-字符串-可分-5-not/](https://www.geeksforgeeks.org/decimal-representation-given-binary-string-divisible-5-not/)

问题是检查给定二进制数的十进制表示是否能被 5 整除。请注意，这个数字可能非常大，甚至可能不适合 long long int。这种方法应该使得乘法和除法运算的数量为零或最小。输入中没有前导 0。

**示例:**

```
Input : 1010
Output : YES
(1010)<sub>2</sub> = (10)<sub>10</sub>,
and 10 is divisible by 5.

Input : 10000101001
Output : YES

```

**进场:**以下步骤为:

1.  将二进制数转换为基数 4。
2.  基数为 4 的数字只包含 0、1、2、3 作为它们的数字。
3.  基数为 4 的 5 相当于 11。
4.  现在应用[除以 11](https://www.geeksforgeeks.org/check-large-number-divisible-11-not/) 的规则，将奇数位的所有数字相加，偶数位的所有数字相加，然后相减。如果结果能被 11 整除(记住是 5)，那么二进制数就能被 5 整除。

**如何将二进制数转换为 4 进制表示？**

1.  检查二进制字符串的长度是偶数还是奇数。
2.  如果是奇数，则在字符串的开头加上“0”。
3.  现在，从左到右遍历字符串。
4.  一种是提取大小为 2 的子字符串，并将其等效的十进制数添加到结果字符串中。

## C++

```
// C++ implementation to check whether decimal representation 
// of given binary number is divisible by 5 or not
#include <bits/stdc++.h>

using namespace std;

// function to return equivalent base 4 number 
// of the given binary number
int equivalentBase4(string bin)
{
    if (bin.compare("00") == 0) 
        return 0;
    if (bin.compare("01") == 0) 
        return 1;
    if (bin.compare("10") == 0) 
        return 2;
    return 3; 
}

// function to check whether the given binary
// number is divisible by 5 or not
string isDivisibleBy5(string bin)
{
    int l = bin.size();

    if (l % 2 != 0)
    // add '0' in the beginning to make 
    // length an even number
        bin = '0' + bin;

    // to store sum of digits at odd and 
    // even places respectively 
    int odd_sum, even_sum = 0;

    // variable check for odd place and
    // even place digit
    int isOddDigit = 1;
    for (int i = 0; i<bin.size(); i+= 2)
    {
        // if digit of base 4 is at odd place, then
        // add it to odd_sum
        if (isOddDigit)
            odd_sum += equivalentBase4(bin.substr(i, 2));
        // else digit of base 4 is at even place,
        // add it to even_sum 
        else
            even_sum += equivalentBase4(bin.substr(i, 2));

        isOddDigit ^= 1; 
    }

    // if this diff is divisible by 11(which is 5 in decimal)
    // then, the binary number is divisible by 5
    if (abs(odd_sum - even_sum) % 5 == 0)
        return "Yes";

    // else not divisible by 5
    return "No";

}

// Driver program to test above
int main()
{
    string bin = "10000101001";
    cout << isDivisibleBy5(bin);
    return 0;
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation to check whether decimal representation 
//of given binary number is divisible by 5 or not

class GFG 
{
    // Method to return equivalent base 4 number 
    // of the given binary number
    static int equivalentBase4(String bin)
    {
        if (bin.compareTo("00") == 0) 
            return 0;
        if (bin.compareTo("01") == 0) 
            return 1;
        if (bin.compareTo("10") == 0) 
            return 2;
        return 3; 
    }

    // Method to check whether the given binary
    // number is divisible by 5 or not
    static String isDivisibleBy5(String bin)
    {
        int l = bin.length();

        if (l % 2 != 0)
        // add '0' in the beginning to make 
        // length an even number
            bin = '0' + bin;

        // to store sum of digits at odd and 
        // even places respectively 
        int odd_sum=0, even_sum = 0;

        // variable check for odd place and
        // even place digit
        int isOddDigit = 1;
        for (int i = 0; i<bin.length(); i+= 2)
        {
            // if digit of base 4 is at odd place, then
            // add it to odd_sum
            if (isOddDigit != 0)
                odd_sum += equivalentBase4(bin.substring(i, i+2));
            // else digit of base 4 is at even place,
            // add it to even_sum 
            else
                even_sum += equivalentBase4(bin.substring(i, i+2));

            isOddDigit ^= 1; 
        }

        // if this diff is divisible by 11(which is 5 in decimal)
        // then, the binary number is divisible by 5
        if (Math.abs(odd_sum - even_sum) % 5 == 0)
            return "Yes";

        // else not divisible by 5
        return "No";

    }

    public static void main (String[] args)
    {
        String bin = "10000101001";
        System.out.println(isDivisibleBy5(bin));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to check whether 
# decimal representation of given binary 
# number is divisible by 5 or not

# function to return equivalent base 4 
# number of the given binary number 
def equivalentBase4(bin):
    if(bin == "00"):
        return 0
    if(bin == "01"):
        return 1
    if(bin == "10"):
        return 2
    if(bin == "11"):
        return 3

# function to check whether the given 
# binary number is divisible by 5 or not     
def isDivisibleBy5(bin):
    l = len(bin)
    if((l % 2) == 1):

    # add '0' in the beginning to 
    # make length an even number     
        bin = '0' + bin

    # to store sum of digits at odd 
    # and even places respectively 
    odd_sum = 0
    even_sum = 0
    isOddDigit = 1
    for i in range(0, len(bin), 2):

        # if digit of base 4 is at odd place, 
        # then add it to odd_sum 
        if(isOddDigit):
            odd_sum += equivalentBase4(bin[i:i + 2])

        # else digit of base 4 is at
        # even place, add it to even_sum     
        else:
            even_sum += equivalentBase4(bin[i:i + 2])

        isOddDigit = isOddDigit ^ 1

    # if this diff is divisible by 11(which is 
    # 5 in decimal) then, the binary number is
    # divisible by 5 
    if(abs(odd_sum - even_sum) % 5 == 0):
        return "Yes"
    else:
        return "No"

# Driver Code
if __name__=="__main__":
    bin = "10000101001"
    print(isDivisibleBy5(bin))

# This code is contributed 
# by Sairahul Jella 
```

## C#

```
// C# implementation to check whether 
// decimal representation of given
// binary number is divisible by 5 or not 
using System;

class GFG
{
// Method to return equivalent base
// 4 number of the given binary number 
public static int equivalentBase4(string bin)
{
    if (bin.CompareTo("00") == 0)
    {
        return 0;
    }
    if (bin.CompareTo("01") == 0)
    {
        return 1;
    }
    if (bin.CompareTo("10") == 0)
    {
        return 2;
    }
    return 3;
}

// Method to check whether the 
// given binary number is divisible 
// by 5 or not 
public static string isDivisibleBy5(string bin)
{
    int l = bin.Length;

    if (l % 2 != 0)
    {
        // add '0' in the beginning to 
        // make length an even number 
        bin = '0' + bin;
    }

    // to store sum of digits at odd 
    // and even places respectively 
    int odd_sum = 0, even_sum = 0;

    // variable check for odd place 
    // and even place digit 
    int isOddDigit = 1;
    for (int i = 0; i < bin.Length; i += 2)
    {
        // if digit of base 4 is at odd 
        // place, then add it to odd_sum 
        if (isOddDigit != 0)
        {
            odd_sum += equivalentBase4(
                             bin.Substring(i, 2));
        }

        // else digit of base 4 is at even  
        // place, add it to even_sum 
        else
        {
            even_sum += equivalentBase4(
                              bin.Substring(i, 2));
        }

        isOddDigit ^= 1;
    }

    // if this diff is divisible by 
    // 11(which is 5 in decimal) then, 
    // the binary number is divisible by 5 
    if (Math.Abs(odd_sum - even_sum) % 5 == 0)
    {
        return "YES";
    }

    // else not divisible by 5 
    return "NO";

}

// Driver Code
public static void Main(string[] args)
{
    string bin = "10000101001";
    Console.WriteLine(isDivisibleBy5(bin));
}
}

// This code is contributed by Shrikant13
```

**Output:**

```
YES

```

**时间复杂度:** O(n)，其中 n 为二进制数中的位数。

参考文献:[https://stackoverflow . com/questions/18473730/硬件中的算法来找出数字是否能被 5 整除](https://stackoverflow.com/questions/18473730/algorithm-in-hardware-to-find-out-if-number-is-divisible-by-five)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 最少使用算术运算符的十进制到八进制转换

> 原文:[https://www . geesforgeks . org/十进制-八进制-转换-最小使用-算术-运算符/](https://www.geeksforgeeks.org/decimal-octal-conversion-minimum-use-arithmetic-operators/)

给定一个没有浮点的十进制数 **n** 。问题是用最少的算术运算符将十进制数转换成八进制数。

**示例:**

```
Input : n = 10
Output : 12 
12 is octal equivalent of decimal 10.

Input : n = 151
Output : 227
```

**进场:**以下是步骤:

1.  不使用给定数字 **n** 的算术运算符，执行十进制到二进制的转换。参考[这篇](https://www.geeksforgeeks.org/decimal-binary-conversion-without-using-arithmetic-operators/)帖子。让这个数字成为 **bin** 。
2.  将二进制数**仓**转换为八进制。参考[这篇](https://www.geeksforgeeks.org/convert-binary-number-octal/)帖子。

## C++

```
// C++ implementation of decimal to octal conversion
// with minimum use of arithmetic operators
#include <bits/stdc++.h>

using namespace std;

// function for decimal to binary conversion
// without using arithmetic operators
string decToBin(int n)
{
    if (n == 0)
        return "0";

    // to store the binary equivalent of decimal
    string bin = "";   
    while (n > 0)   
    {
        // to get the last binary digit of the
        // number 'n' and accumulate it at the
        // beginning of 'bin'
        bin = ((n & 1) == 0 ? '0' : '1') + bin;

        // right shift 'n' by 1
        n >>= 1;
    }

    // required binary number
    return bin;
}

// Function to find octal equivalent of binary
string convertBinToOct(string bin)
{
    int l = bin.size();

    // add min 0's in the beginning to make
    // string length divisible by 3
    for (int i = 1; i <= (3 - l % 3) % 3; i++)
        bin = '0' + bin;

    // create map between binary and its
    // equivalent octal code
    unordered_map<string, char> bin_oct_map;
    bin_oct_map["000"] = '0';
    bin_oct_map["001"] = '1';
    bin_oct_map["010"] = '2';
    bin_oct_map["011"] = '3';
    bin_oct_map["100"] = '4';
    bin_oct_map["101"] = '5';
    bin_oct_map["110"] = '6';
    bin_oct_map["111"] = '7'; 

    int i = 0;
    string octal = "";     
    while (1)
    {
        // one by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map[bin.substr(i, 3)];
        i += 3;
        if (i == bin.size())
            break;       
    }

    // required octal number
    return octal;   
}

// function to find octal equivalent of decimal
string decToOctal(int n)
{
    // convert decimal to binary
    string bin = decToBin(n);

    // convert binary to octal
    // required octal equivalent of decimal
    return convertBinToOct(bin);
}

// Driver program to test above
int main()
{
    int n = 151;
    cout << decToOctal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of decimal to octal
// conversion with minimum use of
// arithmetic operators
import java.util.*;

class GFG
{

// function for decimal to binary conversion
// without using arithmetic operators
static String decToBin(int n)
{
    if (n == 0)
        return "0";

    // to store the binary equivalent of decimal
    String bin = "";
    while (n > 0)
    {
        // to get the last binary digit of the
        // number 'n' and accumulate it at the
        // beginning of 'bin'
        bin = ((n & 1) == 0 ? '0' : '1') + bin;

        // right shift 'n' by 1
        n >>= 1;
    }

    // required binary number
    return bin;
}

// Function to find octal equivalent of binary
static String convertBinToOct(String bin)
{
    int l = bin.length();

    // add min 0's in the beginning to make
    // string length divisible by 3
    for (int i = 1; i <= (3 - l % 3) % 3; i++)
        bin = '0' + bin;

    // create map between binary and its
    // equivalent octal code
    Map<String,
        Character> bin_oct_map = new HashMap<>();
    bin_oct_map.put("000", '0');
    bin_oct_map.put("001", '1');
    bin_oct_map.put("010", '2');
    bin_oct_map.put("011", '3');
    bin_oct_map.put("100", '4');
    bin_oct_map.put("101", '5');
    bin_oct_map.put("110", '6');
    bin_oct_map.put("111", '7');

    int i = 0;
    String octal = "";    
    while (true)
    {
        // one by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map.get(bin.substring(i, i + 3));
        i += 3;
        if (i == bin.length())
            break;    
    }

    // required octal number
    return octal;
}

// function to find octal equivalent of decimal
static String decToOctal(int n)
{
    // convert decimal to binary
    String bin = decToBin(n);

    // convert binary to octal
    // required octal equivalent of decimal
    return convertBinToOct(bin);
}

// Driver Code
public static void main(String[] args)
{
    int n = 151;
    System.out.println(decToOctal(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of decimal to octal conversion
# with minimum use of arithmetic operators

# function for decimal to binary conversion
# without using arithmetic operators
def decToBin(n):

    if (n == 0):
        return "0"

    # to store the binary equivalent of decimal
    bin = ""

    while (n > 0):

        # to get the last binary digit of the
        # number 'n' and accumulate it at the
        # beginning of 'bin'
        bin = ('0' if(n & 1) == 0 else '1') + bin

        # right shift 'n' by 1
        n >>= 1

    # required binary number
    return bin

# Function to find octal equivalent of binary
def convertBinToOct(bin):

    l = len(bin)

    # add min 0's in the beginning to make
    # string length divisible by 3
    for i in range(1,((3 - l % 3) % 3) + 1):
        bin = '0' + bin

    # create map between binary and its
    # equivalent octal code

    bin_oct_map = dict()

    bin_oct_map["000"] = '0'
    bin_oct_map["001"] = '1'
    bin_oct_map["010"] = '2'
    bin_oct_map["011"] = '3'
    bin_oct_map["100"] = '4'
    bin_oct_map["101"] = '5'
    bin_oct_map["110"] = '6'
    bin_oct_map["111"] = '7'

    i = 0
    octal = ""

    while (True):

        # one by one extract from left, substring
        # of size 3 and add its octal code
        octal += bin_oct_map[bin[i:i + 3]]
        i += 3
        if (i == len(bin)):
            break

    # required octal number
    return octal

# function to find octal equivalent of decimal
def decToOctal(n):

    # convert decimal to binary
    bin = decToBin(n)

    # convert binary to octal
    # required octal equivalent of decimal
    return convertBinToOct(bin)

# Driver program to test above
if __name__=='__main__':

    n = 151
    print(decToOctal(n))

# This code is contributed by pratham76
```

## C#

```
// C# implementation of decimal to octal
// conversion with minimum use of
// arithmetic operators
using System;
using System.Collections.Generic;

class GFG{

// Function for decimal to binary
// conversion without using
// arithmetic operators
static string decToBin(int n)
{
    if (n == 0)
        return "0";

    // To store the binary equivalent
    // of decimal
    string bin = "";
    while (n > 0)
    {

        // To get the last binary digit of the
        // number 'n' and accumulate it at the
        // beginning of 'bin'
        bin = ((n & 1) == 0 ? '0' : '1') + bin;

        // Right shift 'n' by 1
        n >>= 1;
    }

    // Required binary number
    return bin;
}

// Function to find octal equivalent of binary
static string convertBinToOct(string bin)
{
    int l = bin.Length;

    // Add min 0's in the beginning to make
    // string length divisible by 3
    for(int j = 1; j <= (3 - l % 3) % 3; j++)
        bin = '0' + bin;

    // Create map between binary and its
    // equivalent octal code
    Dictionary<string,
               char> bin_oct_map = new Dictionary<string,
                                                  char>();

    bin_oct_map.Add("000", '0');
    bin_oct_map.Add("001", '1');
    bin_oct_map.Add("010", '2');
    bin_oct_map.Add("011", '3');
    bin_oct_map.Add("100", '4');
    bin_oct_map.Add("101", '5');
    bin_oct_map.Add("110", '6');
    bin_oct_map.Add("111", '7');

    int i = 0;
    string octal = ""; 

    while (true)
    {

        // One by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map[bin.Substring(i, 3)];
        i += 3;

        if (i == bin.Length)
            break;    
    }

    // Required octal number
    return octal;
}

// Function to find octal equivalent of decimal
static string decToOctal(int n)
{

    // Convert decimal to binary
    string bin = decToBin(n);

    // Convert binary to octal
    // required octal equivalent
    // of decimal
    return convertBinToOct(bin);
}

// Driver Code
public static void Main(string[] args)
{
    int n = 151;

    Console.Write(decToOctal(n));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of decimal to octal conversion
// with minimum use of arithmetic operators

// function for decimal to binary conversion
// without using arithmetic operators
function decToBin(n)
{
    if (n == 0)
        return "0";

    // to store the binary equivalent of decimal
    var bin = "";   
    while (n > 0)   
    {
        // to get the last binary digit of the
        // number 'n' and accumulate it at the
        // beginning of 'bin'
        bin = ((n & 1) == 0 ? '0' : '1') + bin;

        // right shift 'n' by 1
        n >>= 1;
    }

    // required binary number
    return bin;
}

// Function to find octal equivalent of binary
function convertBinToOct(bin)
{
    var l = bin.length;

    // add min 0's in the beginning to make
    // string length divisible by 3
    for (var i = 1; i <= (3 - l % 3) % 3; i++)
        bin = '0' + bin;

    // create map between binary and its
    // equivalent octal code
    var bin_oct_map = new Map();
    bin_oct_map.set("000",'0');
    bin_oct_map.set("001",'1');
    bin_oct_map.set("010",'2');
    bin_oct_map.set("011",'3');
    bin_oct_map.set("100",'4');
    bin_oct_map.set("101",'5');
    bin_oct_map.set("110",'6');
    bin_oct_map.set("111",'7');

    var i = 0;
    var octal = "";     
    while (1)
    {
        // one by one extract from left, substring
        // of size 3 and add its octal code
        octal += bin_oct_map.get(bin.substring(i, i+3));
        i += 3;
        if (i == bin.length)
            break;       
    }

    // required octal number
    return octal;   
}

// function to find octal equivalent of decimal
function decToOctal(n)
{
    // convert decimal to binary
    var bin = decToBin(n);

    // convert binary to octal
    // required octal equivalent of decimal
    return convertBinToOct(bin);
}

// Driver program to test above
var n = 151;
document.write( decToOctal(n));ing

// This code is contributed by itsok.
</script>
```

**输出:**

```
227
```

时间复杂度:O(n)，其中 n 是二进制字符串的长度。
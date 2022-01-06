# 通过删除重复出现对给定字符串进行解码

> 原文:[https://www . geesforgeks . org/decode-通过删除重复出现的给定字符串/](https://www.geeksforgeeks.org/decode-a-given-string-by-removing-duplicate-occurrences/)

给定编码的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**，使得**‘a’**被写入 1 次，**‘b’**被写入 2 次，以此类推，直到**‘z’**被写入 26 次，任务是解码给定的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**。

**注意:**字母可能包含空格和标点符号，不要忽略这些。

**示例:**

> **输入:** str = "bbadddd"
> **输出:**不良
> **解释:**
> 因为每个字母都是对应英文字母表中出现的次数写的。因此，结果字符串是“坏的”。
> 
> **输入:**【str = " abbbbacccdddd】
> **输出:** abbacd

**方法:**给定的问题可以通过[迭代给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **字符串**来解决，对于每个字符，将该字符推入输出[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)中，并将相应的位置向前移动以检查其他字符。按照以下步骤解决问题:

*   初始化一个变量，比如说**输出**为一个空的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)，存储结果字符串。
*   定义函数**查找重复(char c)** ，并执行以下步骤:
    *   如果 **c** 的值在从 **a** 到 **z 的范围内，**则返回 **c-'a'** 的值。
    *   否则，如果 **c** 的值在 **A** 到 **Z** 的范围内，则返回**c-【Z】**的值。
    *   否则，返回 **0** 。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   将字符串**的**I<sup>th</sup>T3【字符】推入[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)T8【输出】T9。****
    *   调用函数**find repeation(str[I])**来计算步数**I<sup>th</sup>T5】索引必须向前移动。**
*   执行上述步骤后，打印字符串**输出**作为结果字符串。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the appearances
// of each character
int findRepitition(char a)
{
    // If the character is lower case
    if (a <= 'z' && a >= 'a') {
        return a - 'a';
    }

    // If the character is uppercase
    else if (a <= 'Z' && a >= 'A') {
        return a - 'A';
    }

    // If the character is a
    // punctuation mark
    return 0;
}

// Function to decode the given encoded
// string
void decodeString(string str)
{
    string output = "";

    // Iterate the given string str
    for (int i = 0; i < str.length(); i++) {

        output.push_back(str[i]);

        // Find the index of the next
        // character to be printed
        i += findRepitition(str[i]);
    }

    cout << "Decrypted code is {"
         << output << "}" << endl;
}

// Driver Code
int main()
{
    string str = "abbbb acccdddd";
    decodeString(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the appearances
// of each character
static int findRepitition(char a)
{

    // If the character is lower case
    if (a <= 'z' && a >= 'a')
    {
        return a - 'a';
    }

    // If the character is uppercase
    else if (a <= 'Z' && a >= 'A')
    {
        return a - 'A';
    }

    // If the character is a
    // punctuation mark
    return 0;
}

// Function to decode the given encoded
// String
static void decodeString(String str)
{
    String output = "";

    // Iterate the given String str
    for(int i = 0; i < str.length(); i++)
    {
        output += (str.charAt(i));

        // Find the index of the next
        // character to be printed
        i += findRepitition(str.charAt(i));
    }
    System.out.print("Decrypted code is {" +
                     output + "}" + "\n");
}

// Driver Code
public static void main(String[] args)
{
    String str = "abbbb acccdddd";

    decodeString(str);
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the appearances
# of each character
def findRepetition(a):

  # If the character is lower case
    if a <= 'z' and a >= 'a':
        return ord(a)-97

    # If the character is uppercase
    elif a <= 'Z' and a >= 'A':
        return ord(a)-65
    else:

     # If the character is a
    # punctuation mark
        return 0

# Function to decode the given encoded
# string
def decodeString(str_):
    output = ""
    i = 0

    # Iterate the given string str
    while(i < len(str_)):
        output += str_[i]

        # Find the index of the next
        # character to be printed
        i += findRepetition(str_[i]) + 1
    print("Decrypted code is {" + output + "}")

# Driver code
str_ = "abbbb acccdddd"
decodeString(str_)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the appearances
// of each character
static int findRepitition(char a)
{
    // If the character is lower case
    if (a <= 'z' && a >= 'a') {
        return (int)a - 97;
    }

    // If the character is uppercase
    else if (a <= 'Z' && a >= 'A') {
        return (int)a - 65;
    }

    // If the character is a
    // punctuation mark
    return 0;
}

// Function to decode the given encoded
// string
static void decodeString(string str)
{
    string output = "";

    // Iterate the given string str
    for (int i = 0; i < str.Length; i++) {

        output += str[i];

        // Find the index of the next
        // character to be printed
        i += findRepitition(str[i]);
    }

    Console.Write("Decrypted code is {" + output + "}");
}

// Driver Code
public static void Main()
{
    string str = "abbbb acccdddd";
    decodeString(str);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to count the appearances
        // of each character
        function findRepitition(a)
        {

            // If the character is lower case
            if (a.charCodeAt(0) <= 'z'.charCodeAt(0) && a.charCodeAt(0) >= 'a'.charCodeAt(0)) {
                return a.charCodeAt(0) - 'a'.charCodeAt(0);
            }

            // If the character is uppercase
            else if (a <= 'Z' && a >= 'A') {
                return a.charCodeAt(0) - 'A'.charCodeAt(0);
            }

            // If the character is a
            // punctuation mark
            return 0;
        }

        // Function to decode the given encoded
        // string
        function decodeString(str) {
            let output = "";

            // Iterate the given string str
            for (let i = 0; i < str.length; i++) {

                output += (str[i]);

                // Find the index of the next
                // character to be printed
                i += findRepitition(str[i]);
            }

            document.write("Decrypted code is {"
                + output + "}" + "<br>");
        }

        // Driver Code
        let str = "abbbb acccdddd";
        decodeString(str);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Decrypted code is {abb acd}
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
# 计算大写、小写、特殊字符和数值

> 原文:[https://www . geesforgeks . org/count-大写-小写-特殊-字符-数字-数值/](https://www.geeksforgeeks.org/count-uppercase-lowercase-special-character-numeric-values/)

给定一个字符串，编写一个程序来计算小写字符、大写字符、特殊字符和数值的出现次数。
**例:**

```
Input : #GeeKs01fOr@gEEks07
Output : 
Upper case letters : 5
Lower case letters : 8
Numbers : 4
Special Characters : 2

Input : *GeEkS4GeEkS*
Output :
Upper case letters : 6
Lower case letters : 4
Numbers : 1
Special Characters : 2
```

**进场:**

1.  从 0 到长度-1 扫描字符串。
2.  根据 ASCII 值一次检查一个字符
    *   if(str[i] >= 65 且 str[i] <=90), then it is uppercase letter, 

    *   if(str[i] >= 97 且 str[i] <=122), then it is lowercase letter, 

    *   if(str[i] >= 48 且 str[i] <=57), then it is number, 

    *   否则它就是一个特殊的角色
3.  打印所有计数器。

## C++

```
// C++ program to count the uppercase,
// lowercase, special characters
// and numeric values
#include<iostream>
using namespace std;

// Function to count uppercase, lowercase,
// special characters and numbers
void Count(string str)
{
    int upper = 0, lower = 0, number = 0, special = 0;
    for (int i = 0; i < str.length(); i++)
    {
        if (str[i] >= 'A' && str[i] <= 'Z')
            upper++;
        else if (str[i] >= 'a' && str[i] <= 'z')
            lower++;
        else if (str[i]>= '0' && str[i]<= '9')
            number++;
        else
            special++;
    }
    cout << "Upper case letters: " << upper << endl;
    cout << "Lower case letters : " << lower << endl;
    cout << "Number : " << number << endl;
    cout << "Special characters : " << special << endl;
}

// Driver function
int main()
{
    string str = "#GeeKs01fOr@gEEks07";
    Count(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the uppercase,
// lowercase, special characters
// and numeric values
import java.io.*;

class Count
{
    public static void main(String args[])
    {
        String str = "#GeeKs01fOr@gEEks07";
        int upper = 0, lower = 0, number = 0, special = 0;

        for(int i = 0; i < str.length(); i++)
        {
            char ch = str.charAt(i);
            if (ch >= 'A' && ch <= 'Z')
                upper++;
            else if (ch >= 'a' && ch <= 'z')
                lower++;
            else if (ch >= '0' && ch <= '9')
                number++;
            else
                special++;
        }

        System.out.println("Lower case letters : " + lower);
        System.out.println("Upper case letters : " + upper);
        System.out.println("Number : " + number);
        System.out.println("Special characters : " + special);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count the uppercase,
# lowercase, special characters
# and numeric values

# Function to count uppercase, lowercase,
# special characters and numbers
def Count(str):
    upper, lower, number, special = 0, 0, 0, 0
    for i in range(len(str)):
        if str[i].isupper():
            upper += 1
        elif str[i].islower():
            lower += 1
        elif str[i].isdigit():
            number += 1
        else:
            special += 1
    print('Upper case letters:', upper)
    print('Lower case letters:', lower)
    print('Number:', number)
    print('Special characters:', special)

# Driver Code
str = "#GeeKs01fOr@gEEks07"
Count(str)

# This code is contributed
# by Sushma Reddy
```

## C#

```
// C# program to count the uppercase,
// lowercase, special characters
// and numeric values
using System;

class Count {

    public static void Main()
    {

        String str = "#GeeKs01fOr@gEEks07";
        int upper = 0, lower = 0;
        int number = 0, special = 0;

        for(int i = 0; i < str.Length; i++)
        {
            char ch = str[i];
            if (ch >= 'A' && ch <= 'Z')
                upper++;
            else if (ch >= 'a' && ch <= 'z')
                lower++;
            else if (ch >= '0' && ch <= '9')
                number++;
            else
                special++;
        }
        Console.WriteLine("Upper case letters : " + upper);
        Console.WriteLine("Lower case letters : " + lower);
        Console.WriteLine("Number : " + number);
        Console.Write("Special characters : " + special);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the uppercase,
// lowercase, special characters
// and numeric values

// Function to count uppercase, lowercase,
// special characters and numbers
function Countt($str)
{
    $upper = 0;
    $lower = 0;
    $number = 0;
    $special = 0;
    for ($i = 0; $i < strlen($str); $i++)
    {
        if ($str[$i] >= 'A' &&
            $str[$i] <= 'Z')
            $upper++;
        else if ($str[$i] >= 'a' &&
                 $str[$i] <= 'z')
            $lower++;
        else if ($str[$i]>= '0' &&
                 $str[$i]<= '9')
            $number++;
        else
            $special++;
    }
    echo "Upper case letters: " , $upper,"\n" ;
    echo "Lower case letters : " ,$lower,"\n" ;
    echo "Number : " , $number ,"\n";
    echo "Special characters : ", $special ;
}

    // Driver Code
    $str = "#GeeKs01fOr@gEEks07";
    Countt($str);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
      // JavaScript program to count the uppercase,
      // lowercase, special characters
      // and numeric values

      // Function to count uppercase, lowercase,
      // special characters and numbers
      function Count(str)
      {
        var upper = 0,
          lower = 0,
          number = 0,
          special = 0;
        for (var i = 0; i < str.length; i++)
        {
          if (str[i] >= "A" && str[i] <= "Z") upper++;
          else if (str[i] >= "a" && str[i] <= "z") lower++;
          else if (str[i] >= "0" && str[i] <= "9") number++;
          else special++;
        }
        document.write("Upper case letters: " + upper + "<br>");
        document.write("Lower case letters : " + lower + "<br>");
        document.write("Number : " + number + "<br>");
        document.write("Special characters : " + special + "<br>");
      }

      // Driver function
      var str = "#GeeKs01fOr@gEEks07";
      Count(str);

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
Upper case letters: 5
Lower case letters : 8
Number : 4
Special characters : 2
```

**时间复杂度:** O(N)，其中 N 为字符串长度

**辅助空间:** O(1)
本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
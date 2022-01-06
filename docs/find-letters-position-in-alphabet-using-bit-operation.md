# 使用位操作

找到字母在字母表中的位置

> 原文:[https://www . geesforgeks . org/find-letters-position-in-alphabet-using-bit-operation/](https://www.geeksforgeeks.org/find-letters-position-in-alphabet-using-bit-operation/)

给定一串英文字母。任务是，为字符串中的每个字符打印它在英文字母中的位置。
**注意**:字符串中的字符被认为不区分大小写。即‘A’和‘A’都在第一位置。
**示例:**

> **输入:**【极客】
> **输出:**7 5 5 11 19
> 【G】是字母表
> 的第 7 <sup>个</sup>字符，【e】是第 5 <sup>个</sup>字符，依此类推……
> **输入:**【算法】
> **输出:** 1 12 7 15 18 9 20 8 13 19

**方法:**
通过对数字 **31** 进行逻辑**和**运算，很容易找到字母在字母表中的位置。
**注意**这个只适用于字母，不适用特殊字符。
每个字母都有一个 ASCII 值，可以用二进制形式表示。用数字 31 对该值执行按位“与”运算将给出字母在字母表中的位置。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

const int NUM = 31;

// Function to calculate the position
// of characters
void positions(string str, int n)
{
    for (int i = 0; i < n; i++) {

        // Performing AND operation
        // with number 31
        cout << (str[i] & NUM) << " ";
    }
}

// Driver code
int main()
{
    string str = "Geeks";
    int n = str.length();

    positions(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    public static final int NUM = 31;

    // Function to calculate the position
    // of characters
    static void positions(String str, int n)
    {
        for (int i = 0; i < n; i++) {

            // Performing AND operation
            // with number 31
            System.out.print((str.charAt(i) & NUM) + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "Geeks";
        int n = str.length();
        positions(str, n);
    }
}
```

## 计算机编程语言

```
# Python3 implementation of the approach

NUM = 31

# Function to calculate the position
# of characters
def positions(str):
    for i in str:

        # Performing AND operation
        # with number 31
        print((ord(i) & NUM), end =" ")

# Driver code
str = "Geeks"
positions(str)
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    public static int NUM = 31;

    // Function to calculate the position
    // of characters
    static void positions(string str, int n)
    {
        for (int i = 0; i < n; i++) {

            // Performing AND operation
            // with number 31
            Console.Write((str[i] & NUM) + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        string str = "Geeks";
        int n = str.Length;
        positions(str, n);
    }
}

// This code is contributed by AnkitRai01
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to calculate the position
// of characters
function positions($str, $n)
{
    $a = 31;
    for ($i = 0; $i < $n; $i++)
    {

        // Performing AND operation
        // with number 31$
        print((ord($str[$i])&($a))." ");
    }
}

// Driver code
$str = "Geeks";
$n = strlen($str);
positions($str, $n);

// This code is contributed by 29AjayKumar
?>
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach
      const NUM = 31;

      // Function to calculate the position
      // of characters
      function positions(str, n)
      {
        for (i = 0; i < n; i++)
        {
          // Performing AND operation
          // with number 31
          document.write((str[i].charCodeAt(0) & NUM) +
          " ");
        }
      }

      // Driver code
      var str = "Geeks";
      var n = str.length;
      positions(str, n);

</script>
```

**Output:** 

```
7 5 5 11 19
```

时间复杂度:0(n)

辅助空间:0(1)
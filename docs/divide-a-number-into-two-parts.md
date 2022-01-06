# 将一个数字分成两部分

> 原文:[https://www . geesforgeks . org/将数字分成两部分/](https://www.geeksforgeeks.org/divide-a-number-into-two-parts/)

给定一个包含数字 **4** 的整数 **N** 至少一次。任务是将数字分成两部分 **x1** 和 **x2** ，这样:

*   **x1 + x2 = N** 。
*   并且没有一个零件包含数字 **4** 。

**注意**可能有多个答案。
**例:**

> **输入:** N = 4
> **输出:** 1 3
> 1 + 3 = 4
> **输入:** N = 9441
> **输出:**9331 110
> 9331+110 = 9441

**方法:**由于数字可能太大，所以将数字作为字符串。把它分成两串:

*   对于字符串 1，找到字符串中数字 4 的所有位置，将其改为 3，我们也可以将其改为另一个数字。
*   对于第二个字符串，在数字 4 的所有位置放 1，在从数字 4 的第一个位置到字符串末尾的所有剩余位置放 0。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the two parts
void twoParts(string str)
{
    int flag = 0;
    string a = "";

    // Find the position of 4
    for (int i = 0; i < str.length(); i++) {
        if (str[i] == '4') {
            str[i] = '3';
            a += '1';
            flag = 1;
        }

        // If current character is not '4'
        // but appears after the first
        // occurrence of '4'
        else if (flag)
            a += '0';
    }

    // Print both the parts
    cout << str << " " << a;
}

// Driver code
int main()
{
    string str = "9441";
    twoParts(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

    // Function to print the two parts
    static void twoParts(String str)
    {
        int flag = 0;
        String a = "";
        char[] gfg = str.toCharArray();

        // Find the position of 4
        for (int i = 0; i < str.length(); i++)
        {
            if (gfg[i] == '4')
            {
                gfg[i] = '3';
                a += '1';
                flag = 1;
            }

            // If current character is not '4'
            // but appears after the first
            // occurrence of '4'
            else if (flag != 0)
                a += '0';
        }

        str = new String(gfg);

        // Print both the parts
        System.out.print(str + " " + a);
    }

    // Driver code
    public static void main(String []args)
    {
        String str = "9441";
        twoParts(str);
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the two parts
def twoParts(string) :

    flag = 0;
    a = "";

    # Find the position of 4
    for i in range(len(string)) :

        if (string[i] == '4') :
            string[i] = '3';
            a += '1';
            flag = 1;

        # If current character is not '4'
        # but appears after the first
        # occurrence of '4'
        elif (flag) :
            a += '0';

    string = "".join(string);

    # Print both the parts
    print(string, a);

# Driver code
if __name__ == "__main__" :

    string = "9441";

    twoParts(list(string));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to print the two parts
    static void twoParts(string str)
    {
        int flag = 0;
        string a = "";
        char[] gfg = str.ToCharArray();

        // Find the position of 4
        for (int i = 0; i < str.Length; i++)
        {
            if (gfg[i] == '4')
            {
                gfg[i] = '3';
                a += '1';
                flag = 1;
            }

            // If current character is not '4'
            // but appears after the first
            // occurrence of '4'
            else if (flag != 0)
                a += '0';
        }

        str = new String(gfg);

        // Print both the parts
        Console.WriteLine(str + " " + a);
    }

    // Driver code
    static void Main()
    {
        string str = "9441";
        twoParts(str);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the two parts
function twoParts($str)
{
    $flag = 0;
    $a = "";

    // Find the position of 4
    for ($i = 0; $i < strlen($str); $i++)
    {
        if ($str[$i] == '4')
        {
            $str[$i] = '3';
            $a .= '1';
            $flag = 1;
        }

        // If current character is not '4'
        // but appears after the first
        // occurrence of '4'
        else if ($flag)
            $a .= '0';
    }

    // Print both the parts
    echo $str . " " . $a;
}

// Driver code
$str = "9441";
twoParts($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to print the two parts
     function twoParts( str)
    {
        var flag = 0;
        var a = "";
        var gfg = str.split('') ;

        // Find the position of 4
        for (var i = 0; i < str.length; i++)
        {
            if (gfg[i] == '4')
            {
                gfg[i] = '3';
                a += '1';
                flag = 1;
            }

            // If current character is not '4'
            // but appears after the first
            // occurrence of '4'
            else if (flag != 0)
                a += '0';
        }

        // Print both the parts
        document.write(gfg.join('') + " " + a);
    }

    // Driver code

        var str = "9441";
        twoParts(str);

        // This code is contributed by bunnyram19.
        </script>
```

**Output:** 

```
9331 110
```
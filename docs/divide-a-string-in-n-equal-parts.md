# 将一根弦分成 N 等份

> 原文:[https://www . geesforgeks . org/n 等分字符串除法/](https://www.geeksforgeeks.org/divide-a-string-in-n-equal-parts/)

**难度等级:**菜鸟
**提问:**
编写程序打印给定字符串的 N 个等份。
**解法:**
1)使用 string 函数 [strlen()](http://en.wikipedia.org/wiki/Strlen) (出现在 string.h 中)
2)获取零件的尺寸。

```

     part_size = string_length/n 
```

3)循环输入字符串。在循环中，如果索引变成 part_size 的倍数，那么放一个 part 分隔符(" \n")
**实现:**

## C++

```
// C++ program to divide a string
// in n equal parts
#include <iostream>
#include <string.h>

using namespace std;

class gfg {

    // Function to print n equal parts of str
public:
    void divideString(char str[], int n)
    {

        int str_size = strlen(str);
        int i;
        int part_size;

        // Check if string can be divided in
        // n equal parts
        if (str_size % n != 0) {
            cout << "Invalid Input: String size";
            cout << " is not divisible by n";
            return;
        }

        // Calculate the size of parts to
        // find the division points
        part_size = str_size / n;
        for (i = 0; i < str_size; i++) {
            if (i % part_size == 0)
                cout << endl;
            cout << str[i];
        }
    }
};

// Driver code
int main()
{
    gfg g;

    // length od string is 28
    char str[] = "a_simple_divide_string_quest";

    // Print 4 equal parts of the string
    g.divideString(str, 4);
    return 0;
}

// This code is contributed by SoM15242
```

## C

```
// C program to divide a string
// in n equal parts
#include <stdio.h>
#include <string.h>

// Function to print n equal parts of str
void divideString(char* str, int n)
{
    int str_size = strlen(str);
    int i;
    int part_size;

    // Check if string can be divided in
    // n equal parts
    if (str_size % n != 0) {
        printf("Invalid Input: String size");
        printf(" is not divisible by n");
        return;
    }

    // Calculate the size of parts to
    // find the division points
    part_size = str_size / n;
    for (i = 0; i < str_size; i++) {
        if (i % part_size == 0)
            printf("\n");
        printf("%c", str[i]);
    }
}

int main()
{
    // length od string is 28
    char* str = "a_simple_divide_string_quest";

    // Print 4 equal parts of the string
    divideString(str, 4);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to divide a string
// in n equal parts

class GFG {
    // Method to print n equal parts of str
    static void divideString(String str, int n)
    {
        int str_size = str.length();
        int part_size;

        // Check if string can be divided in
        // n equal parts
        if (str_size % n != 0) {
            System.out.println("Invalid Input: String size"
                               + "is not divisible by n");
            return;
        }

        // Calculate the size of parts to find
        // the division points
        part_size = str_size / n;

        for (int i = 0; i < str_size; i++) {
            if (i % part_size == 0)
                System.out.println();
            System.out.print(str.charAt(i));
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // length od string is 28
        String str = "a_simple_divide_string_quest";

        // Print 4 equal parts of the string
        divideString(str, 4);
    }
}
```

## 计算机编程语言

```
# Python program to print n equal parts of string

# Function to print n equal parts of string

def divideString(string, n):
    str_size = len(string)

    # Check if string can be divided in n equal parts
    if str_size % n != 0:
        print "Invalid Input: String size is not divisible by n"
        return

    # Calculate the size of parts to find the division points
    part_size = str_size/n
    k = 0
    for i in string:
        if k % part_size == 0:
            print "\n",
        print i,
        k += 1

# Driver program to test the above function
# Length of string is 28
string = "a_simple_divide_string_quest"

# Print 4 equal parts of the string
divideString(string, 4)

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to divide a string
// in n equal parts
using System;

class GFG {

    // Method to print n
    // equal parts of str
    static void divideString(String str, int n)
    {
        int str_size = str.Length;
        int part_size;

        // Check if string
        // can be divided in
        // n equal parts
        if (str_size % n != 0) {
            Console.Write("Invalid Input: String size"
                          + "is not divisible by n");
            return;
        }

        // Calculate the size
        // of parts to find
        // the division points
        part_size = str_size / n;

        for (int i = 0; i < str_size; i++) {
            if (i % part_size == 0)
                Console.WriteLine();
            Console.Write(str[i]);
        }
    }

    // Driver Code
    static void Main()
    {

        // length od string is 28
        String str = "a_simple_divide_string_quest";

        // Print 4 equal parts of the string
        divideString(str, 4);
    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to divide a string
// in n equal parts

// Function to print n
// equal parts of str
function divideString($str, $n)
{
    $str_size = strlen($str);
    $i;
    $part_size;

// Check if string can be divided
// in n equal parts
if ($str_size % $n != 0)
{
    echo "Invalid Input: String size";
    echo " is not divisible by n";
    return;
}

// Calculate the size of parts to
// find the division point
$part_size = $str_size / $n;
for ($i = 0; $i< $str_size; $i++)
{
    if ($i % $part_size == 0)
        echo "\n";
    echo $str[$i];
}
}

    // Driver Code
    // length od string is 28
    $str = "a_simple_divide_string_quest";

    // Print 4 equal parts of the string
    divideString($str, 4);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to divide a string
    // in n equal parts

    // Method to print n
    // equal parts of str
    function divideString(str, n)
    {
        let str_size = str.length;
        let part_size;

        // Check if string
        // can be divided in
        // n equal parts
        if (str_size % n != 0)
        {
            document.write("Invalid Input: String size" +
                          "is not divisible by n");
            return;
        }

        // Calculate the size
        // of parts to find
        // the division points
        part_size = parseInt(str_size / n, 10);

        for (let i = 0; i< str_size; i++)
        {
            if(i % part_size == 0)
                document.write("</br>");
            document.write(str[i]);
        }
    }

    // length od string is 28
    let str = "a_simple_divide_string_quest";

    // Print 4 equal parts of the string
    divideString(str, 4);

    // This code is contributed by rameshtravel07
</script>
```

**Output**

```
a_simpl
e_divid
e_strin
g_quest
```

在上面的解决方案中，只打印字符串的 n 个相等部分。如果我们希望存储单个部分，我们需要为所有 N 个部分分配 part_size + 1 内存(字符串终止字符' \0 '需要 1 个额外内存)，并将这些部分的地址存储在字符指针数组中。

**另一种方法:**在 C++中使用 STL

## C++

```
#include <iostream>

using namespace std;

void divide(string str, int n)
{

    if (str.length() % n != 0) {
        cout << "Invalid Input: String size";
        cout << " is not divisible by n";
        return;
    }

    int parts = str.length() / n;
    int start = 0;

    while (start < str.length()) {
        cout << str.substr(start, parts) << endl;
        start += parts;
        // if(start < str.length()) cout << endl; to ignore
        // final new line
    }
}

int main()
{
    string str = "a_simple_divide_string_quest";
    divide(str, 4);
}

//Contributed By Jagadeesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG {

    static void divide(String str, int n) {

        if (str.length() % n != 0) {
            System.out.print("Invalid Input: String size");
            System.out.print(" is not divisible by n");
            return;
        }

        int parts = str.length() / n;
        int start = 0;
        int t = parts;
        while (start < str.length()) {
            String temp = new String(str);

            System.out.print(temp.substring(start, parts) + "\n");
            start = parts;
            parts += t;
            // if(start < str.length()) System.out.println(); to ignore
            // final new line
        }
    }

  // Driver code
    public static void main(String[] args) {
        String str = "a_simple_divide_String_quest";
        divide(str, 4);
    }
}

// This code is contributed by umadevi9616
```

**Output**

```
a_simpl
e_divid
e_strin
g_quest
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
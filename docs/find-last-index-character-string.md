# 查找字符串中某个字符的最后一个索引

> 原文:[https://www . geesforgeks . org/find-last-index-character-string/](https://www.geeksforgeeks.org/find-last-index-character-string/)

给定一个字符串和一个字符 x，在字符串中找到 x 的最后一个索引。
**例:**

```
Input : str = "geeks", x = 'e'
Output : 2
Last index of 'e' in "geeks" is: 2 

Input : str = "Hello world!", x = 'o'
Output : 7
Last index of 'o' is: 7 
```

**方法 1(简单:从左开始遍历):**
从左到右遍历给定字符串，并在 x 与当前字符匹配时不断更新索引。

## C++

```
// CPP program to find last index of
// character x in given string.
#include <iostream>
using namespace std;

// Returns last index of x if it is present.
// Else returns -1.
int findLastIndex(string& str, char x)
{
    int index = -1;
    for (int i = 0; i < str.length(); i++)
        if (str[i] == x)
            index = i;
    return index;
}

// Driver code
int main()
{
    // String in which char is to be found
    string str = "geeksforgeeks";

    // char whose index is to be found
    char x = 'e';
    int index = findLastIndex(str, x);
    if (index == -1)
        cout << "Character not found";
    else
        cout << "Last index is " << index;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find last index
// of character x in given string.
import java.io.*;

class GFG {

// Returns last index of x if
// it is present Else returns -1.
static int findLastIndex(String str, Character x)
{
    int index = -1;
    for (int i = 0; i < str.length(); i++)
        if (str.charAt(i) == x)
            index = i;
    return index;
}

// Driver code
public static void main(String[] args)
{
    // String in which char is to be found
    String str = "geeksforgeeks";

    // char whose index is to be found
    Character x = 'e';

    int index = findLastIndex(str, x);
    if (index == -1)
        System.out.println("Character not found");
    else
        System.out.println("Last index is " + index);
}
}

/* This code is contributed by Prerna Saini */
```

## 蟒蛇 3

```
# A Python program to find last
# index of character x in given
# string.

# Returns last index of x if it
# is present. Else returns -1.
def findLastIndex(str, x):
    index = -1
    for i in range(0, len(str)):
        if str[i] == x:
            index = i
    return index

# Driver program

# String in which char is to be found
str = "geeksforgeeks"

# char whose index is to be found
x = 'e'

index = findLastIndex(str, x)

if index == -1:
    print("Character not found")
else:
    print('Last index is', index)

# This code is contributed by shrikant13.
```

## C#

```
// C# program to find last index
// of character x in given string.
using System;

class GFG {

    // Returns last index of x if
    // it is present Else returns -1.
    static int findLastIndex(string str, char x)
    {
        int index = -1;
        for (int i = 0; i < str.Length; i++)
            if (str[i] == x)
                index = i;
        return index;
    }

    // Driver code
    public static void Main()
    {
        // String in which char is to be found
        string str = "geeksforgeeks";

        // char whose index is to be found
        char x = 'e';

        int index = findLastIndex(str, x);
        if (index == -1)
            Console.WriteLine("Character not found");
        else
            Console.WriteLine("Last index is " + index);
    }
}

/* This code is contributed by vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find last index of
// character x in given string.

// Returns last index of
// x if it is present.
// Else returns -1.
function findLastIndex($str, $x)
{
    $index = -1;
    for ($i = 0; $i < strlen($str); $i++)
        if ($str[$i] == $x)
            $index = $i;
    return $index;
}

// Driver code
// String in which
// char is to be found
$str = "geeksforgeeks";

// char whose index
// is to be found
$x = 'e';
$index = findLastIndex($str, $x);
if ($index == -1)
    echo("Character not found");
else
    echo("Last index is " . $index);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to find last index
// of character x in given string.

// Returns last index of x if
// it is present Else returns -1.
function findLastIndex(str, x)
{
    let index = -1;
    for (let i = 0; i < str.length; i++)
        if (str[i] == x)
            index = i;
    return index;
}

// Driver code

    // String in which char is to be found
    let str = "geeksforgeeks";

    // char whose index is to be found
    let x = 'e';

    let index = findLastIndex(str, x);
    if (index == -1)
        document.write("Character not found");
    else
       document.write("Last index is " + index);

     // This code is contributed by sanjoy_62.
</script>
```

输出:

```
Last index is 10
```

时间复杂度:θ(n)
**方法 2(高效:从右遍历):**
在上面的方法 1 中，我们总是遍历完整的字符串。在这种方法中，当 x 存在时，我们可以避免所有这些情况下的完全遍历。这个想法是从右边穿过，一找到角色就停下来。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Simple CPP program to find last index of
// character x in given string.
#include <iostream>
using namespace std;

// Returns last index of x if it is present.
// Else returns -1.
int findLastIndex(string& str, char x)
{
    // Traverse from right
    for (int i = str.length() - 1; i >= 0; i--)
        if (str[i] == x)
            return i;

    return -1;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    char x = 'e';
    int index = findLastIndex(str, x);
    if (index == -1)
        cout << "Character not found";
    else
        cout << "Last index is " << index;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find last index
// character x in given string.
import java.io.*;
class GFG {

// Returns last index of x if
// it is present. Else returns -1.
static int findLastIndex(String str, Character x)
{
    // Traverse from right
    for (int i = str.length() - 1; i >= 0; i--)
        if (str.charAt(i) == x)
            return i;

    return -1;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    Character x = 'e';
    int index = findLastIndex(str, x);
    if (index == -1)
        System.out.println("Character not found");
    else
        System.out.println("Last index is " + index);
}
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Simple Python3 program to find last
# index of character x in given string.

# Returns last index of x if it is
# present. Else returns -1.
def findLastIndex(str, x):

    # Traverse from right
    for i in range(len(str) - 1, -1,-1):
        if (str[i] == x):
            return i

    return -1

# Driver code
str = "geeksforgeeks"
x = 'e'
index = findLastIndex(str, x)

if (index == -1):
    print("Character not found")
else:
    print("Last index is " ,index)

# This code is contributed by Smitha
```

## C#

```
// C# code to find last index
// character x in given string.
using System;

class GFG {

    // Returns last index of x if
    // it is present. Else returns -1.
    static int findLastIndex(string str, char x)
    {
        // Traverse from right
        for (int i = str.Length - 1; i >= 0; i--)
            if (str[i] == x)
                return i;

        return -1;
    }

    // Driver code
    public static void Main()
    {
        string str = "geeksforgeeks";
        char x = 'e';
        int index = findLastIndex(str, x);
        if (index == -1)
            Console.WriteLine("Character not found");
        else
            Console.WriteLine("Last index is " + index);
    }
}
// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find last index
// of character x in given string.

// Returns last index of x if it
// is present. Else returns -1.
function findLastIndex($str, $x)
{

    // Traverse from right
    for ($i = strlen($str) - 1; $i >= 0; $i--)
        if ($str[$i] == $x)
            return $i;

    return -1;
}

// Driver code
$str = "geeksforgeeks";
$x = 'e';
$index = findLastIndex($str, $x);
if ($index == -1)
    echo("Character not found");
else
    echo("Last index is " . $index);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript code to find last index character x in given string.

    // Returns last index of x if
    // it is present. Else returns -1.
    function findLastIndex(str, x)
    {
        // Traverse from right
        for (let i = str.length - 1; i >= 0; i--)
            if (str[i] == x)
                return i;

        return -1;
    }

    let str = "geeksforgeeks";
    let x = 'e';
    let index = findLastIndex(str, x);
    if (index == -1)
      document.write("Character not found");
    else
      document.write("Last index is " + index);

</script>
```

输出:

```
Last index is 10
```

**时间复杂度:** O(n)
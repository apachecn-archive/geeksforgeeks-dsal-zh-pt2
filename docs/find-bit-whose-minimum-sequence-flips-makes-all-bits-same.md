# 查找最小序列翻转使所有位相同的位

> 原文:[https://www . geesforgeks . org/find-bit-what-最小序列翻转-使所有比特相同/](https://www.geeksforgeeks.org/find-bit-whose-minimum-sequence-flips-makes-all-bits-same/)

给定一个仅由 1 和 0 组成的二进制字符串，找到其最小数量的**连续序列翻转**可以使该字符串的所有位相同的位(输出为 1 或 0)。
这里，**连续序列翻转**表示翻转子串或 0 或 1。例如，在字符串“00011110001110”中，在一次翻转中，我们可以将字符串更改为“11111110001110”。前三个连续的零被改为 1。
**注** :

*   在一次翻转中，我们可以改变这个字符串的任何连续序列。
*   如果 0 和 1 都有可能，打印最后一个。
*   任务是简单地打印位 1 或 0，最小顺序翻转将使所有位相同。

**示例** :

> **输入**:str = " 00011110001110 "
> **输出** : 1
> **解释**:有两个 1 的连续序列和三个 0 的连续序列，所以翻转 1 会导致最小的翻转。
> **输入**:str = " 010101100011 "
> **输出** : 1
> **说明**:由于 0 和 1 的组数相同，1 排在最后。

**天真方法**:开始遍历字符串，取名为**的变量**和另一个**的零组**来计算 0 和 1 的组。现在，比较 1 和 0 的组数。计数较少的那个将是答案。
如果两者相等，答案将是字符串的最后一个字符。
**时间复杂度** : O(N)
**高效方法** :

*   仔细观察字符串，字符串最后一个索引处的字符在字符串中将有更多的组(如果字符串的第一个和最后一个字符相等)。所以，答案会是另一个人物。
*   如果第一个和最后一个字符不相等，则两个字符的组数相同。所以，答案将是最后一个索引的字符。

以下是上述方法的实现:

## C++

```
// C++ program to find which bit sequence
// to be flipped

#include <bits/stdc++.h>
using namespace std;

// Function to check which bit is to be flipped
char bitToBeFlipped(string s)
{
    // variable to store first and
    // last character of string
    char last = s[s.length() - 1];
    char first = s[0];

    // Check if first and last characters
    // are equal, if yes, then return
    // the character which is not at last
    if (last == first) {
        if (last == '0') {
            return '1';
        }
        else {
            return '0';
        }
    }

    // else return last
    else if (last != first) {
        return last;
    }
}

// Driver Code
int main()
{
    string s = "1101011000";

    cout << bitToBeFlipped(s) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find which bit sequence
// to be flipped

class GfG {

// Function to check which bit is to be flipped
static char bitToBeFlipped(String s)
{
    // variable to store first and
    // last character of string
    char last = s.charAt(s.length() - 1);
    char first = s.charAt(0);

    // Check if first and last characters
    // are equal, if yes, then return
    // the character which is not at last
    if (last == first) {
        if (last == '0') {
            return '1';
        }
        else {
            return '0';
        }
    }

    // else return last
    else if (last != first) {
        return last;
    }
    return last;
}

// Driver Code
public static void main(String[] args)
{
    String s = "1101011000";

    System.out.println(bitToBeFlipped(s));
}
}
```

## 蟒蛇 3

```
# Python 3 program to find which bit
# sequence to be flipped

# Function to check which bit is
# to be flipped
def bitToBeFlipped( s):

    # variable to store first and
    # last character of string
    last = s[len(s) - 1]
    first = s[0]

    # Check if first and last characters
    # are equal, if yes, then return
    # the character which is not at last
    if (last == first) :
        if (last == '0') :
            return '1'

        else :
            return '0'

    # else return last
    elif (last != first) :
        return last

# Driver Code
if __name__ == "__main__":

    s = "1101011000"

    print(bitToBeFlipped(s))

# This code is contributed by ita_c
```

## C#

```
// C# program to find which bit sequence
// to be flipped
using System;

class GfG {

// Function to check which bit is to be flipped
static char bitToBeFlipped(String s)
{
    // variable to store first and
    // last character of string
    char last = s[s.Length - 1];
    char first = s[0];

    // Check if first and last characters
    // are equal, if yes, then return
    // the character which is not at last
    if (last == first) {
        if (last == '0') {
            return '1';
        }
        else {
            return '0';
        }
    }

    // else return last
    else if (last != first) {
        return last;
    }
    return last;
}

// Driver Code
public static void Main()
{
    string s = "1101011000";

    Console.WriteLine(bitToBeFlipped(s));
}
}
// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find which bit sequence
// to be flipped

// Function to check which bit is to be flipped
function bitToBeFlipped($s)
{
    // variable to store first and
    // last character of string
    $last = $s[strlen($s) - 1];
    $first = $s[0];

    // Check if first and last characters
    // are equal, if yes, then return
    // the character which is not at last
    if ($last == $first)
    {
        if ($last == '0')
        {
            return '1';
        }
        else
        {
            return '0';
        }
    }

    // else return last
    else if ($last != $first)
    {
        return $last;
    }
}

// Driver Code
$s = "1101011000";
echo bitToBeFlipped($s);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// JavaScript program to find which bit sequence
// to be flipped

// Function to check which bit is to be flipped
function bitToBeFlipped(s)
{
    // variable to store first and
    // last character of string
    let last = s[s.length - 1];
    let first = s[0];

    // Check if first and last characters
    // are equal, if yes, then return
    // the character which is not at last
    if (last == first) {
        if (last == '0') {
            return '1';
        }
        else {
            return '0';
        }
    }

    // else return last
    else if (last != first) {
        return last;
    }
}

// Driver Code
let s = "1101011000";
document.write(bitToBeFlipped(s),'<br>');

</script>
```

**Output:** 

```
0
```

**时间复杂度**:O(1)
T3】辅助空间 : O(1)
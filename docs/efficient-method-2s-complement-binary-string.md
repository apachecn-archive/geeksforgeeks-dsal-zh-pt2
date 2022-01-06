# 二进制字符串 2 补码的有效方法

> 原文:[https://www . geesforgeks . org/efficient-method-2s-complex-binary-string/](https://www.geeksforgeeks.org/efficient-method-2s-complement-binary-string/)

给定一个二进制数作为字符串，打印它的 2 的补码。
**二进制数的 2 的补码**是将 1 加到二进制数的 1 的补码上。注意 1 的补码只是给定二进制数的翻转。
**示例:**

```
2's complement of "0111" is  "1001"
2's complement of "1100" is  "0100" 
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/2s-complement3124/1)

我们在下面的帖子中讨论了 1 和 2 的补语。
[二进制数的 1 和 2 的补码。](https://www.geeksforgeeks.org/1s-2s-complement-binary-number/)
上文中讨论的方法遍历二进制字符串两次以找到 2 的补码，首先找到 1 的补码，然后使用 1 的补码找到 2 的补码
在这篇文章中，讨论了一种有效的 2 补码方法，即**只遍历字符串一次**。我们从最后遍历字符串，直到单个 1 没有被遍历，然后翻转字符串的所有值，即 0 到 1 和 1 到 0。
**注意:**在这里处理角情况，即如果字符串中不存在 1，那么只需在字符串的开头追加 1。
**图解:**

```
Input:  str = "1000100"
Output:        0111100
Explanation: Starts traversing the string from last,
we got first '1' at index 4 then just flip the bits 
of 0 to 3 indexes to make the 2's complement. 

Input:  str =  "0000"
Output:        10000
Explanation: As there is no 1 in the string so just 
append '1' at starting.
```

## C++

```
// An efficient C++ program to find 2's complement
#include<bits/stdc++.h>
using namespace std;

// Function to find two's complement
string findTwoscomplement(string str)
{
    int n = str.length();

    // Traverse the string to get first '1' from
    // the last of string
    int i;
    for (i = n-1 ; i >= 0 ; i--)
        if (str[i] == '1')
            break;

    // If there exists no '1' concatenate 1 at the
    // starting of string
    if (i == -1)
        return '1' + str;

    // Continue traversal after the position of
    // first '1'
    for (int k = i-1 ; k >= 0; k--)
    {
        //Just flip the values
        if (str[k] == '1')
            str[k] = '0';
        else
            str[k] = '1';
    }

    // return the modified string
    return str;;
}

// Driver code
int main()
{
    string str = "00000101";
    cout << findTwoscomplement(str);
    return 0;
}             
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to find 2's complement

class Test
{
    // Method to find two's complement
    static String findTwoscomplement(StringBuffer str)
    {
        int n = str.length();

        // Traverse the string to get first '1' from
        // the last of string
        int i;
        for (i = n-1 ; i >= 0 ; i--)
            if (str.charAt(i) == '1')
                break;

        // If there exists no '1' concat 1 at the
        // starting of string
        if (i == -1)
            return "1" + str;

        // Continue traversal after the position of
        // first '1'
        for (int k = i-1 ; k >= 0; k--)
        {
            //Just flip the values
            if (str.charAt(k) == '1')
                str.replace(k, k+1, "0");
            else
                str.replace(k, k+1, "1");
        }

        // return the modified string
        return str.toString();
    }

    // Driver method
    public static void main(String[] args)
    {
        StringBuffer str = new StringBuffer("00000101");
        System.out.println(findTwoscomplement(str));
    }
}
```

## 蟒蛇 3

```
# An efficient Python 3 program to
# find 2's complement

# Function to find two's complement
def findTwoscomplement(str):
    n = len(str)

    # Traverse the string to get first
    # '1' from the last of string
    i = n - 1
    while(i >= 0):
        if (str[i] == '1'):
            break

        i -= 1

    # If there exists no '1' concatenate 1
    # at the starting of string
    if (i == -1):
        return '1'+str

    # Continue traversal after the
    # position of first '1'
    k = i - 1
    while(k >= 0):

        # Just flip the values
        if (str[k] == '1'):
            str = list(str)
            str[k] = '0'
            str = ''.join(str)
        else:
            str = list(str)
            str[k] = '1'
            str = ''.join(str)

        k -= 1

    # return the modified string
    return str

# Driver code
if __name__ == '__main__':
    str = "00000101"
    print(findTwoscomplement(str))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// An efficient c# program to find 2's complement
using System;
using System.Text;

class GFG
{
// Method to find two's complement
public static string findTwoscomplement(StringBuilder str)
{
    int n = str.Length;

    // Traverse the string to get
    // first '1' from the last of string
    int i;
    for (i = n - 1 ; i >= 0 ; i--)
    {
        if (str[i] == '1')
        {
            break;
        }
    }

    // If there exists no '1' concat 1
    // at the starting of string
    if (i == -1)
    {
        return "1" + str;
    }

    // Continue traversal after the
    // position of first '1'
    for (int k = i - 1 ; k >= 0; k--)
    {
        // Just flip the values
        if (str[k] == '1')
        {
            str.Remove(k, k + 1 - k).Insert(k, "0");
        }
        else
        {
            str.Remove(k, k + 1 - k).Insert(k, "1");
        }
    }

    // return the modified string
    return str.ToString();
}

// Driver Code
public static void Main(string[] args)
{
    StringBuilder str = new StringBuilder("00000101");
    Console.WriteLine(findTwoscomplement(str));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program to find 2's
// complement

// Function to find two's complement
function findTwoscomplement($str)
{
    $n = strlen($str);

    // Traverse the string to get first
    // '1' from the last of string
    $i;
    for ($i = $n-1 ; $i >= 0 ; $i--)
        if ($str[$i] == '1')
            break;

    // If there exists no '1' concatenate
    // 1 at the starting of string
    if ($i == -1)
        return '1' + $str;

    // Continue traversal after the
    // position of first '1'
    for ($k = $i-1 ; $k >= 0; $k--)
    {
        // Just flip the values
        if ($str[$k] == '1')
            $str[$k] = '0';
        else
            $str[$k] = '1';
    }

    // return the modified string
    return $str;;
}

// Driver code
$str = "00000101";
echo findTwoscomplement($str);

// This code is contributed by jit.
?>
```

## java 描述语言

```
<script>

// An efficient javascript program to find 2's complement

    // Method to find two's complement
    function findTwoscomplement( str) {
        var n = str.length;

        // Traverse the string to get first '1' from
        // the last of string
        var i;
        for (i = n - 1; i >= 0; i--)
            if (str.charAt(i) == '1')
                break;

        // If there exists no '1' concat 1 at the
        // starting of string
        if (i == -1)
            return "1" + str;

        // Continue traversal after the position of
        // first '1'
        for (k = i - 1; k >= 0; k--) {
            // Just flip the values
            if (str.charAt(k) == '1')
                str = str.substring(0,k)+"0"+str.substring(k+1, str.length);
            else
                str = str.substring(0,k)+"1"+str.substring(k+1, str.length);
        }

        // return the modified string
        return str.toString();
    }

    // Driver method

        var str = "00000101";
        document.write(findTwoscomplement(str));

// This code contributed by umadevi9616
</script>
```

输出:

```
11111011
```

本文由 [**萨希尔·查布拉(akku)**](https://auth.geeksforgeeks.org/?to=https://auth.geeksforgeeks.org/profile.php) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
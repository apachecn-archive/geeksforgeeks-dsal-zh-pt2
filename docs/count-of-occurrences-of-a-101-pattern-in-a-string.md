# 字符串中出现“1(0+)1”模式的次数

> 原文:[https://www . geesforgeks . org/a-101 字符串模式出现次数/](https://www.geeksforgeeks.org/count-of-occurrences-of-a-101-pattern-in-a-string/)

给定一个字母数字字符串，找出模式 1(0+)1 在给定字符串中出现的次数。这里，(0+)表示连续 0 的非空序列的存在。
**示例:**

```
Input : 1001010001
Output : 3
First sequence is in between 0th and 3rd index.
Second sequence is in between 3rd and 5th index.
Third sequence is in between 5th and 9th index.
So total number of sequences comes out to be 3.

Input : 1001ab010abc01001
Output : 2
First sequence is in between 0th and 3rd index.
Second valid sequence is in between 13th and 16th
index. So total number of sequences comes out to 
be 2.
```

解决这个问题的思路是，先找一个‘1’，在字符串中继续向前移动，按下述方式检查:

1.  如果获得了“0”和“1”以外的任何字符，则表示模式无效。因此，我们继续从这个索引中搜索下一个“1”，并再次重复这些步骤。

2.  如果看到“1”，则检查先前位置是否存在“0”，以检查序列的有效性。

以下是上述思路的实现:

## C++

```
// C++ program to calculate number of times
// the pattern occurred in given string
#include<iostream>
using namespace std;

// Returns count of occurrences of "1(0+)1"
// int str.
int countPattern(string str)
{
    int len = str.size();
    bool oneSeen = 0;

    int count = 0;  // Initialize result
    for (int i = 0; i < len ; i++)
    {

        // Check if encountered '1' forms a valid
        // pattern as specified
        if (str[i] == '1' && oneSeen == 1)
            if (str[i - 1] == '0')
                count++;

        // if 1 encountered for first time
        // set oneSeen to 1
        if (str[i] == '1' && oneSeen == 0)
           {
            oneSeen = 1;
            continue;
           }
        // Check if there is any other character
        // other than '0' or '1'. If so then set
        // oneSeen to 0 to search again for new
        // pattern
        if (str[i] != '0' && str[i] != '1')
            oneSeen = 0;

    }

    return count;
}

// Driver program to test above function
int main()
{
    string str = "100001abc101";
    cout << countPattern(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to calculate number of times
//the pattern occurred in given string
public class GFG
{
    // Returns count of occurrences of "1(0+)1"
    // int str.
    static int countPattern(String str)
    {
        int len = str.length();
        boolean oneSeen = false;

        int count = 0;  // Initialize result
        for(int i = 0; i < len ; i++)
        {
            char getChar = str.charAt(i);

            // Check if encountered '1' forms a valid
            // pattern as specified
            if (getChar == '1' && oneSeen == true){
                if (str.charAt(i - 1) == '0')
                    count++;
            }

            // if 1 encountered for first time
            // set oneSeen to 1
            if(getChar == '1' && oneSeen == false)
                oneSeen = true;

            // Check if there is any other character
            // other than '0' or '1'. If so then set
            // oneSeen to 0 to search again for new
            // pattern
            if(getChar != '0' && str.charAt(i) != '1')
                oneSeen = false;

        }
        return count;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
         String str = "100001abc101";
         System.out.println(countPattern(str));
    }

}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to calculate number of times
# the pattern occurred in given string

# Returns count of occurrences of "1(0+)1"
def countPattern(s):
    length = len(s)
    oneSeen = False

    count = 0   # Initialize result
    for i in range(length):

        # Check if encountered '1' forms a valid
        # pattern as specified
        if (s[i] == '1' and oneSeen):
            if (s[i - 1] == '0'):
                count += 1

        # if 1 encountered for first time
        # set oneSeen to 1
        if (s[i] == '1' and oneSeen == 0):
            oneSeen = True

        # Check if there is any other character
        # other than '0' or '1'. If so then set
        # oneSeen to 0 to search again for new
        # pattern
        if (s[i] != '0' and s[i] != '1'):
            oneSeen = False

    return count

# Driver code
s = "100001abc101"
print countPattern(s)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to calculate number
// of times the pattern occurred
// in given string
using System;

class GFG
{
// Returns count of occurrences
// of "1(0+)1" int str.
public static int countPattern(string str)
{
    int len = str.Length;
    bool oneSeen = false;

    int count = 0; // Initialize result
    for (int i = 0; i < len ; i++)
    {
        char getChar = str[i];

        // Check if encountered '1' forms
        // a valid pattern as specified
        if (getChar == '1' &&
                 oneSeen == true)
        {
            if (str[i - 1] == '0')
            {
                count++;
            }
        }

        // if 1 encountered for first
        // time set oneSeen to 1
        if (getChar == '1' &&
            oneSeen == false)
        {
            oneSeen = true;
        }

        // Check if there is any other character
        // other than '0' or '1'. If so then set
        // oneSeen to 0 to search again for new
        // pattern
        if (getChar != '0' &&
                 str[i] != '1')
        {
            oneSeen = false;
        }

    }
    return count;
}

// Driver Code
public static void Main(string[] args)
{
    string str = "100001abc101";
    Console.WriteLine(countPattern(str));
}

}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate number of times
// the pattern occurred in given string

// Returns count of occurrences
// of "1(0+)1"
function countPattern($str)
{
    $len = strlen($str);
    $oneSeen = 0;

    $count = 0; // Initialize result
    for ($i = 0; $i < $len ; $i++)
    {
        // Check if encountered '1' forms a
        // valid pattern as specified
        if ($str[$i] == '1' && $oneSeen == 1)
            if ($str[$i - 1] == '0')
                $count++;

        // if 1 encountered for first
        // time set oneSeen to 1
        if ($str[$i] == '1' && $oneSeen == 0)
            $oneSeen = 1;

        // Check if there is any other character
        // other than '0' or '1'. If so then set
        // oneSeen to 0 to search again for new
        // pattern
        if ($str[$i] != '0' && $str[$i] != '1')
            $oneSeen = 0;

    }

    return $count;
}

// Driver Code
$str = "100001abc101";
echo countPattern($str);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
//Javascript program to calculate number of times
//the pattern occurred in given string

    // Returns count of occurrences of "1(0+)1"
    // int str.
    function countPattern(str)
    {
        let len = str.length;
        let oneSeen = false;

        let count = 0;  // Initialize result
        for(let i = 0; i < len ; i++)
        {
            let getChar = str[i];

            // Check if encountered '1' forms a valid
            // pattern as specified
            if (getChar == '1' && oneSeen == true){
                if (str[i-1] == '0')
                    count++;
            }

            // if 1 encountered for first time
            // set oneSeen to 1
            if(getChar == '1' && oneSeen == false)
                oneSeen = true;

            // Check if there is any other character
            // other than '0' or '1'. If so then set
            // oneSeen to 0 to search again for new
            // pattern
            if(getChar != '0' && str[i] != '1')
                oneSeen = false;

        }
        return count;
    }

    // Driver program to test above function
    let str = "100001abc101";
    document.write(countPattern(str));

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2
```

**时间复杂度** : O( N)，其中 N 为输入字符串的长度。
本文由**释迦牟尼**供稿。如果你喜欢极客(我们知道你喜欢！)并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 通过从给定字符串的前 K 个字符中附加一个字符而形成的字典上最小的字符串

> 原文:[https://www . geeksforgeeks . org/通过从给定字符串的第一个 k 个字符中附加一个字符形成的字典最小字符串/](https://www.geeksforgeeks.org/lexicographically-smallest-string-formed-by-appending-a-character-from-the-first-k-characters-of-a-given-string/)

给定一个由小写字母组成的字符串。任务是找到字典上最小的相同长度的字符串 X，该字符串只能使用下面给出的操作形成:
在单个操作中，从字符串 S 的最多前 K 个字符中选择任意一个字符，将其从字符串 S 中移除并追加到字符串 X 中。根据需要多次应用该操作。
**例:**

> **输入:** str = "gaurang "，k=3
> **输出:**agangur
> 第一步去掉“a”后追加到 X.
> 第二步去掉“g”后追加到 X.
> 第三步去掉“a”后追加到 X.
> 第三步去掉“n”后追加到 X.
> 从前 K 个字符中每一步挑出字典上最小的字符，得到
> 字符串“agangur”

**进场:**

*   在字符串 s 的前 k 个字符中找到最小的字符。
*   删除字符串中最小的字符。
*   将找到的最小字符追加到新字符串 x 中。
*   重复以上步骤，直到字符串 s 为空。

以下是上述方法的实现:

## C++

```
// C++ program to find the new string
// after performing deletions and append
// operation in the string s
#include <bits/stdc++.h>
using namespace std;

// Function to find the new string thus
// formed by removing characters
string newString(string s, int k)
{
    // new string
    string X = "";

    // Remove characters until
    // the string  is empty
    while (s.length() > 0) {

        char temp = s[0];

        // Traverse to find the smallest character in the
        // first k characters
        for (long long i = 1; i < k and i < s.length(); i++) {
            if (s[i] < temp) {
                temp = s[i];
            }
        }

        // append the smallest character
        X = X + temp;

        // removing the lexicographically smallest
        // character from the string
        for (long long i = 0; i < k; i++) {
            if (s[i] == temp) {

                s.erase(s.begin() + i);
                break;
            }
        }
    }

    return X;
}

// Driver Code
int main()
{

    string s = "gaurang";
    int k = 3;

    cout << newString(s, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the new string
// after performing deletions and append
// operation in the string s

class GFG {

// Function to find the new string thus
// formed by removing characters
    static String newString(String s, int k) {
        // new string
        String X = "";

        // Remove characters until
        // the string  is empty
        while (s.length() > 0) {

            char temp = s.charAt(0);

            // Traverse to find the smallest character in the
            // first k characters
            for (int i = 1; i < k && i < s.length(); i++) {
                if (s.charAt(i) < temp) {
                    temp = s.charAt(i);
                }
            }

            // append the smallest character
            X = X + temp;

            // removing the lexicographically smallest
            // character from the string
            for (int i = 0; i < k; i++) {
                if (s.charAt(i) == temp) {

                    s = s.substring(0, i) + s.substring(i + 1);
                    //s.erase(s.begin() + i);
                    break;
                }
            }
        }

        return X;
    }
// Driver code

    public static void main(String[] args) {
        String s = "gaurang";
        int k = 3;

        System.out.println(newString(s, k));

    }
}

// This code contributed by Jajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find the new string
# after performing deletions and append
# operation in the string s

# Function to find the new string thus
# formed by removing characters
def newString(s, k):

    # new string
    X = ""

    # Remove characters until
    # the string is empty
    while (len(s) > 0):
        temp = s[0]

        # Traverse to find the smallest
        # character in the first k characters
        i = 1
        while(i < k and i < len(s)):
            if (s[i] < temp):
                temp = s[i]

            i += 1

        # append the smallest character
        X = X + temp

        # removing the lexicographically
        # smallest character from the string
        for i in range(k):
            if (s[i] == temp):
                s = s[0:i] + s[i + 1:]
                break

    return X

# Driver Code
if __name__ == '__main__':
    s = "gaurang"
    k = 3
    print(newString(s, k))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find the new string
// after performing deletions and
// append operation in the string s
using System;

class GFG
{

// Function to find the new string thus
// formed by removing characters
static String newString(String s, int k)
{
    // new string
    String X = "";

    // Remove characters until
    // the string is empty
    while (s.Length > 0)
    {
        char temp = s[0];

        // Traverse to find the smallest
        // character in the first k characters
        for (int i = 1; i < k && i < s.Length; i++)
        {
            if (s[i] < temp)
            {
                temp = s[i];
            }
        }

        // append the smallest character
        X = X + temp;

        // removing the lexicographically smallest
        // character from the string
        for (int i = 0; i < k; i++)
        {
            if (s[i] == temp)
            {

                s = s.Substring(0, i) + s.Substring(i + 1);
                //s.erase(s.begin() + i);
                break;
            }
        }
    }

    return X;
}

// Driver code
public static void Main(String[] args)
{
    String s = "gaurang";
    int k = 3;

    Console.Write(newString(s, k));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the new string
// after performing deletions and
// append operation in the string s

// Function to find the new string thus
// formed by removing characters
function newString($s, $k)
{
    // new string
    $X = "";

    // Remove characters until
    // the string is empty
    while (strlen($s) > 0)
    {
        $temp = $s[0];

        // Traverse to find the smallest
        // character in the first k characters
        for ($i = 1; $i < $k &&
             $i < strlen($s); $i++)
        {
            if ($s[$i] < $temp)
            {
                $temp = $s[$i];
            }
        }

        // append the smallest character
        $X = $X . $temp;

        // removing the lexicographically smallest
        // character from the string
        for ($i = 0; $i < $k; $i++)
        {
            if ($s[$i] == $temp)
            {

                $s = substr($s, 0, $i) .
                     substr($s, $i + 1, strlen($s));

                //s.erase(s.begin() + i);
                break;
            }
        }
    }

    return $X;
}

// Driver code
$s = "gaurang";
$k = 3;

echo(newString($s, $k));

// This code contributed by mits
?>
```

## java 描述语言

```
<script>

      // JavaScript program to find the new string
      // after performing deletions and
      // append operation in the string s

      // Function to find the new string thus
      // formed by removing characters
      function newString(s, k) {
        // new string
        var X = "";

        // Remove characters until
        // the string is empty
        while (s.length > 0) {
          var temp = s[0];

          // Traverse to find the smallest
          // character in the first k characters
          for (var i = 1; i < k && i < s.length; i++)
          {
            if (s[i] < temp) {
              temp = s[i];
            }
          }

          // append the smallest character
          X = X + temp;

          // removing the lexicographically smallest
          // character from the string
          for (var i = 0; i < k; i++) {
            if (s[i] === temp) {
              s = s.substring(0, i) + s.substring(i + 1);

              break;
            }
          }
        }

        return X;
      }

      // Driver code
      var s = "gaurang";
      var k = 3;

      document.write(newString(s, k));

</script>
```

**Output:** 

```
agangru
```
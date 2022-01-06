# 不同时包含集合{'a '，' b '，' c'}中所有字符的子字符串计数

> 原文:[https://www . geesforgeks . org/不同时包含集合 a-b-c 中所有字符的子字符串计数/](https://www.geeksforgeeks.org/count-of-sub-strings-that-do-not-contain-all-the-characters-from-the-set-a-b-c-at-the-same-time/)

给定仅由字符**【a】****【b】**和**【c】**组成的字符串 **str** ，找出不同时包含所有三个字符的子字符串的数量。
**举例:**

> **输入:** str = "abc"
> **输出:** 5
> 可能的子串有“a”、“b”、“c”、“ab”和“BC”
> **输入:** str = "babac"
> **输出:** 12

**方法:**想法是使用三个变量 **a_index** 、 **b_index** 和 **c_index** 来存储字符 a、b 和 c 的最新出现，使用另一个变量 **ans** 来存储没有 a、b 或 c 中至少一个的子串的数量，并将其值初始化为长度为 n 的子串总数，即 **n*(n+1)/2** ，其中
现在只需从头开始遍历字符串。每次遇到时，将变量值更新为最新值。由于我们用 0 进行索引，所以我们在每一步都将索引更新为 **i+1** 。
同样在每一步，你需要找到当前步骤中没有遇到的剩余两个字符的最小出现索引。
然后简单地从变量**和**中扣除这个指标。这是因为，一旦找到剩余字符中最小字符的索引，您就可以肯定，通过在索引中向下移动而形成的任何子字符串也将包含所有这三个字符。
因此，在该步骤中形成的所有这样的子串(包含所有 a、b 和 c 的子串)的总数是找到的索引。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of valid sub-strings
int CountSubstring(string str, int n)
{

    // Variable ans to store all the possible substrings
    // Initialize its value as total number of substrings
    // that can be formed from the given string
    int ans = (n * (n + 1)) / 2;

    // Stores recent index of the characters
    int a_index = 0;
    int b_index = 0;
    int c_index = 0;

    for (int i = 0; i < n; i++) {

        // If character is a update a's index
        // and the variable ans
        if (str[i] == 'a') {
            a_index = i + 1;
            ans -= min(b_index, c_index);
        }

        // If character is b update b's index
        // and the variable ans
        else if (str[i] == 'b') {
            b_index = i + 1;
            ans -= min(a_index, c_index);
        }

        // If character is c update c's index
        // and the variable ans
        else {
            c_index = i + 1;
            ans -= min(a_index, b_index);
        }
    }

    return ans;
}

// Driver code
int main()
{
    string str = "babac";
    int n = str.length();

    cout << CountSubstring(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count of valid sub-strings
    static int CountSubstring(char str[], int n)
    {

        // Variable ans to store all the possible substrings
        // Initialize its value as total number of substrings
        // that can be formed from the given string
        int ans = (n * (n + 1)) / 2;

        // Stores recent index of the characters
        int a_index = 0;
        int b_index = 0;
        int c_index = 0;

        for (int i = 0; i < n; i++)
        {

            // If character is a update a's index
            // and the variable ans
            if (str[i] == 'a')
            {
                a_index = i + 1;
                ans -= Math.min(b_index, c_index);
            }
            // If character is b update b's index
            // and the variable ans
            else if (str[i] == 'b')
            {
                b_index = i + 1;
                ans -= Math.min(a_index, c_index);
            }
            // If character is c update c's index
            // and the variable ans
            else
            {
                c_index = i + 1;
                ans -= Math.min(a_index, b_index);
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        char str[] = "babac".toCharArray();
        int n = str.length;

        System.out.println(CountSubstring(str, n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# valid sub-Strings
def CountSubString(Str, n):

    # Variable ans to store all the possible subStrings
    # Initialize its value as total number of subStrings
    # that can be formed from the given String
    ans = (n * (n + 1)) // 2

    # Stores recent index of the characters
    a_index = 0
    b_index = 0
    c_index = 0

    for i in range(n):

        # If character is a update a's index
        # and the variable ans
        if (Str[i] == 'a'):
            a_index = i + 1
            ans -= min(b_index, c_index)

        # If character is b update b's index
        # and the variable ans
        elif (Str[i] == 'b'):
            b_index = i + 1
            ans -= min(a_index, c_index)

        # If character is c update c's index
        # and the variable ans
        else:
            c_index = i + 1
            ans -= min(a_index, b_index)

    return ans

# Driver code
Str = "babac"
n = len(Str)

print(CountSubString(Str, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// valid sub-strings
static int CountSubstring(char []str, int n)
{

    // Variable ans to store all the possible substrings
    // Initialize its value as total number of substrings
    // that can be formed from the given string
    int ans = (n * (n + 1)) / 2;

    // Stores recent index of the characters
    int a_index = 0;
    int b_index = 0;
    int c_index = 0;

    for (int i = 0; i < n; i++)
    {

        // If character is a update a's index
        // and the variable ans
        if (str[i] == 'a')
        {
            a_index = i + 1;
            ans -= Math.Min(b_index, c_index);
        }
        // If character is b update b's index
        // and the variable ans
        else if (str[i] == 'b')
        {
            b_index = i + 1;
            ans -= Math.Min(a_index, c_index);
        }
        // If character is c update c's index
        // and the variable ans
        else
        {
            c_index = i + 1;
            ans -= Math.Min(a_index, b_index);
        }
    }

    return ans;
}

// Driver code
public static void Main()
{
    char []str = "babac".ToCharArray();
    int n = str.Length;

    Console.WriteLine(CountSubstring(str, n));
}
}

// This code contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
    // PHP implementation of the approach
    // Function to return the count of valid sub-strings
    function CountSubstring($str,$n)

    {

        // Variable ans to store all the possible substrings
        // Initialize its value as total number of substrings
        // that can be formed from the given string
        $ans = ($n * ($n + 1)) / 2;

        // Stores recent index of the characters
        $a_index = 0;
        $b_index = 0;
        $c_index = 0;

        for ($i = 0; $i < $n; $i++)
    {

            // If character is a update a's index
            // and the variable ans
            if ($str[$i] == 'a')
            {
                $a_index = $i + 1;
                $ans -= min($b_index, $c_index);
            }
            // If character is b update b's index
            // and the variable ans
            else if ($str[$i] == 'b')
            {
                $b_index = $i + 1;
                $ans -= min($a_index, $c_index);
            }
            // If character is c update c's index
            // and the variable ans
            else
            {
                $c_index = $i + 1;
                $ans -= min($a_index, $b_index);
            }
        }

        return $ans;
    }

    // Driver code
    {
        $str = str_split("babac");
        $n = sizeof($str);

        echo(CountSubstring($str, $n));
    }

// This code contributed by Code_Mech.
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the count of
      // valid sub-strings
      function CountSubstring(str, n) {
        // Variable ans to store all the possible substrings
        // Initialize its value as total number of substrings
        // that can be formed from the given string
        var ans = parseInt((n * (n + 1)) / 2);

        // Stores recent index of the characters
        var a_index = 0;
        var b_index = 0;
        var c_index = 0;

        for (var i = 0; i < n; i++) {
          // If character is a update a's index
          // and the variable ans
          if (str[i] === "a") {
            a_index = i + 1;
            ans -= Math.min(b_index, c_index);
          }
          // If character is b update b's index
          // and the variable ans
          else if (str[i] === "b") {
            b_index = i + 1;
            ans -= Math.min(a_index, c_index);
          }
          // If character is c update c's index
          // and the variable ans
          else {
            c_index = i + 1;
            ans -= Math.min(a_index, b_index);
          }
        }

        return ans;
      }

      // Driver code
      var str = "babac".split("");
      var n = str.length;

      document.write(CountSubstring(str, n));
    </script>
```

**Output:** 

```
12
```

**时间复杂度** : O(N)。
**辅助空间:** O(1)
# 不包含任何回文的最长子串的长度

> 原文:[https://www . geesforgeks . org/最长不包含任何回文的子串长度/](https://www.geeksforgeeks.org/length-of-the-longest-substring-that-do-not-contain-any-palindrome/)

给定一个小写的字符串，找到不包含任何回文作为子字符串的最长子字符串的长度。

**示例:**

```
Input : str = "daiict" 
Output : 3
dai, ict are longest substring that do not contain any 
palindrome as substring

Input : str = "a"
Output : 0
a is itself a palindrome 
```

这个想法是观察如果任何字符形成回文，它不能包含在任何子串中。因此，在这种情况下，所需的子字符串将从构成回文的字符之前或之后选取。
因此，一个简单的解决方案是遍历字符串，对于每个字符，检查它是否与其相邻字符形成长度为 2 或 3 的回文。如果没有，则增加子字符串的长度，否则将子字符串的长度重新初始化为零。使用这种方法，找到最大子字符串的长度。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the longest
// substring
int lenoflongestnonpalindrome(string s)
{
    // initializing the variables
    int max1 = 1, len = 0;

    for (int i = 0; i < s.length() - 1; i++) {
        // checking palindrome of size 2
        // example: aa
        if (s[i] == s[i + 1])
            len = 0;
        // checking palindrome of size 3
        // example: aba
        else if (s[i + 1] == s[i - 1] && i > 0)
            len = 1;
        else // incrementing length of substring
            len++;
        max1 = max(max1, len + 1); // finding maximum
    }

    // if there exits single character then
    // it is always palindrome
    if (max1 == 1)
        return 0;
    else
        return max1;
}

// Driver Code
int main()
{
    string s = "synapse";
    cout << lenoflongestnonpalindrome(s) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;
import java.lang.Math;

class GFG {

    // Function to find the length of the longest
    // substring
    public static int lenoflongestnonpalindrome(String s)
    {
        // initializing the variables
        int max1 = 1, len = 0;
        char[] new_str = s.toCharArray();

        for (int i = 0; i < new_str.length - 1; i++) {
            // checking palindrome of size 2
            // example: aa
            if (new_str[i] == new_str[i + 1])
                len = 0;
            // checking palindrome of size 3
            // example: aba
            else if (i > 0 && (new_str[i + 1] == new_str[i - 1]))
                len = 1;
            else // incrementing length of substring
                len++;
            max1 = Math.max(max1, len + 1); // finding maximum
        }

        // if there exits single character then
        // it is always palindrome
        if (max1 == 1)
            return 0;
        else
            return max1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "synapse";
        System.out.println(lenoflongestnonpalindrome(s));
    }
}

// This code is contributed by princiraj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the length
# of the longest substring
def lenoflongestnonpalindrome(s):

    # initializing the variables
    max1, length = 1, 0

    for i in range(0, len(s) - 1):

        # checking palindrome of
        # size 2 example: aa
        if s[i] == s[i + 1]:
            length = 0

        # checking palindrome of
        # size 3 example: aba
        elif s[i + 1] == s[i - 1] and i > 0:
            length = 1
        else: # incrementing length of substring
            length += 1
        max1 = max(max1, length + 1) # finding maximum

    # If there exits single character
    # then it is always palindrome
    if max1 == 1:
        return 0
    else:
        return max1

# Driver Code
if __name__ == "__main__":

    s = "synapse"
    print(lenoflongestnonpalindrome(s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to find the length of the longest
    // substring
    public static int lenoflongestnonpalindrome(String s)
    {
        // initializing the variables
        int max1 = 1, len = 0;
        char[] new_str = s.ToCharArray();

        for (int i = 0; i < new_str.Length - 1; i++)
        {
            // checking palindrome of size 2
            // example: aa
            if (new_str[i] == new_str[i + 1])
                len = 0;

            // checking palindrome of size 3
            // example: aba
            else if (i > 0 && (new_str[i + 1] == new_str[i - 1]))
                len = 1;
            else // incrementing length of substring
                len++;
            max1 = Math.Max(max1, len + 1); // finding maximum
        }

        // if there exits single character then
        // it is always palindrome
        if (max1 == 1)
            return 0;
        else
            return max1;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "synapse";
        Console.WriteLine(lenoflongestnonpalindrome(s));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the length of the longest
// substring
function lenoflongestnonpalindrome($s)
{
    // initializing the variables
    $max1 = 1; $len = 0;

    for ($i = 0; $i < strlen($s) - 1; $i++)
    {
        // checking palindrome of size 2
        // example: aa
        if ($s[$i] == $s[$i + 1])
            $len = 0;

        // checking palindrome of size 3
        // example: aba
        else if ($s[$i + 1] == $s[$i - 1] && $i > 0)
            $len = 1;
        else // incrementing length of substring
            $len++;
        $max1 = max($max1, $len + 1); // finding maximum
    }

    // if there exits single character then
    // it is always palindrome
    if ($max1 == 1)
        return 0;
    else
        return $max1;
}

// Driver Code
$s = "synapse";
echo lenoflongestnonpalindrome($s), "\n";

// This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to find the length of the longest
// substring
function lenoflongestnonpalindrome(s)
{
    // initializing the variables
    let max1 = 1, len = 0;

    for (let i = 0; i < s.length - 1; i++) {
        // checking palindrome of size 2
        // example: aa
        if (s[i] == s[i + 1])
            len = 0;
        // checking palindrome of size 3
        // example: aba
        else if (s[i + 1] == s[i - 1] && i > 0)
            len = 1;
        else // incrementing length of substring
            len++;
        max1 = Math.max(max1, len + 1); // finding maximum
    }

    // if there exits single character then
    // it is always palindrome
    if (max1 == 1)
        return 0;
    else
        return max1;
}

// Driver Code

    let s = "synapse";
    document.write(lenoflongestnonpalindrome(s) + "<br>");

//This code is contributed by Manoj
</script>
```

**Output:** 

```
7
```
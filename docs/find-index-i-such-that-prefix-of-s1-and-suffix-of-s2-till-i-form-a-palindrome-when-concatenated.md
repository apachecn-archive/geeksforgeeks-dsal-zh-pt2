# 找到索引 I，这样 S1 的前缀和 S2 的后缀连接起来就形成了回文

> 原文:[https://www . geesforgeks . org/find-index-I-so-so-前缀为-S1-后缀为-S2-till-I-form-a-回文-当-串联/](https://www.geeksforgeeks.org/find-index-i-such-that-prefix-of-s1-and-suffix-of-s2-till-i-form-a-palindrome-when-concatenated/)

给定两个长度相等的字符串 **A** 和 **B** ，任务是找到一个索引 **i** ，使得**A【0…I】**和**B【I+1…n-1】**在连接在一起时给出一个回文。如果无法找到这样的索引，则打印 **-1** 。
**示例:**

> **输入:**S1 =“abcdf”，S2 =“sfgba”
> T3】输出:1
> S1【0..1] = "ab "，S2[2..n-1]=“GBA”
> S1+S2 =“abgba”这是回文。
> **输入:**S1 =“abcda”，S2 =“bacbs”
> **输出:** -1

**简单方法:**

*   从 **0** 迭代到 **n** (字符串长度)并将**I<sup>th</sup>T7】字符从 **S1** 复制到另一个字符串，比如说 **S** 。**
*   现在取另一个临时字符串 **Temp** ，将 **S2** 的字符从索引 **i +1** 复制到 **n** 。
*   现在检查字符串 **(S + Temp)** 是否回文。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if s is palindrome
bool isPalindrome(string s)
{
    int i = 0;
    int j = s.length() - 1;

    while (i < j) {
        if (s[i] != s[j])
            return false;
        i++;
        j--;
    }

    return true;
}

// Function to return the required index
int getIndex(string S1, string S2, int n)
{

    string S = "";

    for (int i = 0; i < n; i++) {

        // Copy the ith character in S
        S = S + S1[i];
        string Temp = "";

        // Copy all the character of string s2 in Temp
        for (int j = i + 1; j < n; j++)
            Temp += S2[j];

        // Check whether the string is palindrome
        if (isPalindrome(S + Temp)) {
            return i;
        }
    }

    return -1;
}

// Driver code
int main()
{
    string S1 = "abcdf", S2 = "sfgba";
    int n = S1.length();

    cout << getIndex(S1, S2, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if s is palindrome
static boolean isPalindrome(String s)
{
    int i = 0;
    int j = s.length() - 1;

    while (i < j)
    {
        if (s.charAt(i) != s.charAt(j))
            return false;
        i++;
        j--;
    }

    return true;
}

// Function to return the required index
static int getIndex(String S1, String S2, int n)
{

    String S = "";

    for (int i = 0; i < n; i++)
    {

        // Copy the ith character in S
        S = S + S1.charAt(i);
        String Temp = "";

        // Copy all the character of string
        // s2 in Temp
        for (int j = i + 1; j < n; j++)
            Temp += S2.charAt(j);

        // Check whether the string is palindrome
        if (isPalindrome(S + Temp))
        {
            return i;
        }
    }

    return -1;
}

// Driver code
public static void main(String[] args)
{
    String S1 = "abcdf", S2 = "sfgba";
    int n = S1.length();

    System.out.println(getIndex(S1, S2, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if s is palindrome
def isPalindrome(s):
    i = 0;
    j = len(s) - 1;

    while (i < j):
        if (s[i] is not s[j]):
            return False;
        i += 1;
        j -= 1;

    return True;

# Function to return the required index
def getIndex(S1, S2, n):

    S = "";

    for i in range(n):

        # Copy the ith character in S
        S = S + S1[i];
        Temp = "";

        # Copy all the character of string s2 in Temp
        for j in range(i + 1, n):
            Temp += S2[j];

        # Check whether the string is palindrome
        if (isPalindrome(S + Temp)):
            return i;

    return -1;

# Driver code
S1 = "abcdf"; S2 = "sfgba";
n = len(S1);

print(getIndex(S1, S2, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function that returns true if
// s is palindrome
static bool isPalindrome(string s)
{
    int i = 0;
    int j = s.Length - 1;

    while (i < j)
    {
        if (s[i] != s[j])
            return false;
        i++;
        j--;
    }

    return true;
}

// Function to return the required index
static int getIndex(string S1,
                    string S2, int n)
{
    string S = "";

    for (int i = 0; i < n; i++)
    {

        // Copy the ith character in S
        S = S + S1[i];
        string Temp = "";

        // Copy all the character of string
        // s2 in Temp
        for (int j = i + 1; j < n; j++)
            Temp += S2[j];

        // Check whether the string
        // is palindrome
        if (isPalindrome(S + Temp))
        {
            return i;
        }
    }

    return -1;
}

// Driver code
public static void Main()
{
    string S1 = "abcdf", S2 = "sfgba";
    int n = S1.Length;

    Console.WriteLine(getIndex(S1, S2, n));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if s
// is palindrome
function isPalindrome($s)
{
    $i = 0;
    $j = strlen($s) - 1;

    while ($i < $j)
    {
        if ($s[$i] != $s[$j])
            return false;
        $i++;
        $j--;
    }

    return true;
}

// Function to return the required index
function getIndex($S1, $S2, $n)
{
    $S = "";

    for ($i = 0; $i < $n; $i++)
    {

        // Copy the ith character in S
        $S = $S . $S1[$i];
        $Temp = "";

        // Copy all the character of string
        // s2 in Temp
        for ($j = $i + 1; $j < $n; $j++)
            $Temp .= $S2[$j];

        // Check whether the string is palindrome
        if (isPalindrome($S . $Temp))
        {
            return $i;
        }
    }

    return -1;
}

// Driver code
$S1 = "abcdf"; $S2 = "sfgba";
$n = strlen($S1);

echo getIndex($S1, $S2, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function that returns true if
    // s is palindrome
    function isPalindrome(s)
    {
        let i = 0;
        let j = s.length - 1;

        while (i < j)
        {
            if (s[i] != s[j])
                return false;
            i++;
            j--;
        }

        return true;
    }

    // Function to return the required index
    function getIndex(S1, S2, n)
    {
        let S = "";

        for (let i = 0; i < n; i++)
        {

            // Copy the ith character in S
            S = S + S1[i];
            let Temp = "";

            // Copy all the character of string
            // s2 in Temp
            for (let j = i + 1; j < n; j++)
                Temp += S2[j];

            // Check whether the string
            // is palindrome
            if (isPalindrome(S + Temp))
            {
                return i;
            }
        }

        return -1;
    }

    let S1 = "abcdf", S2 = "sfgba";
    let n = S1.length;

    document.write(getIndex(S1, S2, n));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(n <sup>2</sup> )
**高效方法**:高效方法是观察当我们考虑第一个字符串的前缀和第二个字符串的后缀时，如果第一个字符串的第一个字符与第二个字符串的最后一个字符匹配，则串联的字符串将是回文。

*   从开始使用指针开始迭代第一个字符串，比如说 **i** ，从结束使用指针开始迭代第二个字符串，比如说 **j** ，直到 **i < j** 和**S1【I】= = S2【j】**。
*   检查指针 I 和 j 在第一次不匹配时是否相等。
*   如果是，那么返回索引 I，也就是我们可以串联字符串 **s1[0..i]** 和**S2【j..N]** 形成回文。
*   否则，检查**S1【I..j]** 或**S2【I..j]** 是回文。如果是，那么我们仍然可以连接任一**S1【0..j] + s2[j+1，N-1]** 或 **s1[0..i-1] + s2[i..N-1]** 形成回文。
*   否则，返回-1。

以下是上述方法的实现:

## C++

```
// C++ program to implement the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the sub-string
// starting from index i and ending at index j
// is a palindrome
bool isPalindrome(string s, int i, int j)
{
    while (i < j) {
        if (s[i] != s[j])
            return false;
        i++;
        j--;
    }
    return true;
}

// Function to get the required index
int getIndex(string s1, string s2, int len)
{
    int i = 0, j = len - 1;

    // Start comparing the two strings
    // from both ends.
    while (i < j) {
        // Break from the loop at first mismatch
        if (s1[i] != s2[j]) {
            break;
        }

        i++;
        j--;
    }

    // If it is possible to concatenate
    // the strings to form palindrome,
    // return index
    if (i == j) {
        return i - 1;
    }

    // If remaining part for s2
    // is palindrome
    else if (isPalindrome(s2, i, j))
        return i - 1;

    // If remaining part for s1
    // is palindrome
    else if (isPalindrome(s1, i, j))
        return j;

    // If not possible, return -1
    return -1;
}

// Driver Code
int main()
{
    string s1 = "abcdf", s2 = "sfgba";
    int len = s1.length();

    cout << getIndex(s1, s2, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function that returns true if the sub-String
// starting from index i and ending at index j
// is a palindrome
static boolean isPalindrome(String s, int i, int j)
{
    while (i < j)
    {
        if (s.charAt(i) != s.charAt(j))
            return false;
        i++;
        j--;
    }
    return true;
}

// Function to get the required index
static int getIndex(String s1, String s2, int len)
{
    int i = 0, j = len - 1;

    // Start comparing the two Strings
    // from both ends.
    while (i < j)
    {
        // Break from the loop at first mismatch
        if (s1.charAt(i) != s2.charAt(j))
        {
            break;
        }

        i++;
        j--;
    }

    // If it is possible to concatenate
    // the Strings to form palindrome,
    // return index
    if (i == j)
    {
        return i - 1;
    }

    // If remaining part for s2
    // is palindrome
    else if (isPalindrome(s2, i, j))
        return i - 1;

    // If remaining part for s1
    // is palindrome
    else if (isPalindrome(s1, i, j))
        return j;

    // If not possible, return -1
    return -1;
}

// Driver Code
public static void main(String args[])
{
    String s1 = "abcdf", s2 = "sfgba";
    int len = s1.length();

    System.out.println( getIndex(s1, s2, len));

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function that returns true if the sub-string
# starting from index i and ending at index j
# is a palindrome
def isPalindrome(s, i, j) :

    while (i < j) :

        if (s[i] != s[j]) :
            return False;

        i += 1;
        j -= 1;

    return True;

# Function to get the required index
def getIndex(s1, s2, length) :

    i = 0 ; j = length - 1;

    # Start comparing the two strings
    # from both ends.
    while (i < j) :

        # Break from the loop at first mismatch
        if (s1[i] != s2[j]) :
            break;

        i += 1;
        j -= 1;

    # If it is possible to concatenate
    # the strings to form palindrome,
    # return index
    if (i == j) :
        return i - 1;

    # If remaining part for s2
    # is palindrome
    elif (isPalindrome(s2, i, j)) :
        return i - 1;

    # If remaining part for s1
    # is palindrome
    elif (isPalindrome(s1, i, j)) :
        return j;

    # If not possible, return -1
    return -1;

# Driver Code
if __name__ == "__main__" :

    s1 = "abcdf" ;
    s2 = "sfgba";
    length = len(s1) ;

    print(getIndex(s1, s2, length));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function that returns true if the sub-String
// starting from index i and ending at index j
// is a palindrome
static bool isPalindrome(string s,
                         int i, int j)
{
    while (i < j)
    {
        if (s[i] != s[j])

            return false;
        i++;
        j--;
    }
    return true;
}

// Function to get the required index
static int getIndex(string s1, string s2, int len)
{
    int i = 0, j = len - 1;

    // Start comparing the two Strings
    // from both ends.
    while (i < j)
    {
        // Break from the loop at first
        // mismatch
        if (s1[i] != s2[j])
        {
            break;
        }

        i++;
        j--;
    }

    // If it is possible to concatenate
    // the Strings to form palindrome,
    // return index
    if (i == j)
    {
        return i - 1;
    }

    // If remaining part for s2
    // is palindrome
    else if (isPalindrome(s2, i, j))
        return i - 1;

    // If remaining part for s1
    // is palindrome
    else if (isPalindrome(s1, i, j))
        return j;

    // If not possible, return -1
    return -1;
}

// Driver Code
public static void Main()
{
    string s1 = "abcdf", s2 = "sfgba";
    int len = s1.Length;

    Console.WriteLine(getIndex(s1, s2, len));

}
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Function that returns true if the sub-String
    // starting from index i and ending at index j
    // is a palindrome
    function isPalindrome(s, i, j)
    {
        while (i < j)
        {
            if (s[i] != s[j])

                return false;
            i++;
            j--;
        }
        return true;
    }

    // Function to get the required index
    function getIndex(s1, s2, len)
    {
        let i = 0, j = len - 1;

        // Start comparing the two Strings
        // from both ends.
        while (i < j)
        {
            // Break from the loop at first
            // mismatch
            if (s1[i] != s2[j])
            {
                break;
            }

            i++;
            j--;
        }

        // If it is possible to concatenate
        // the Strings to form palindrome,
        // return index
        if (i == j)
        {
            return i - 1;
        }

        // If remaining part for s2
        // is palindrome
        else if (isPalindrome(s2, i, j))
            return i - 1;

        // If remaining part for s1
        // is palindrome
        else if (isPalindrome(s1, i, j))
            return j;

        // If not possible, return -1
        return -1;
    }

    let s1 = "abcdf", s2 = "sfgba";
    let len = s1.length;

    document.write(getIndex(s1, s2, len) + "</br>");

</script>
```

**Output:** 

```
1
```

**时间复杂度** : O(N)，其中 N 为字符串的长度。
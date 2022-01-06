# 计算第一个和最后一个字符相同的子字符串

> 原文:[https://www . geeksforgeeks . org/count-substrings-具有相同的第一个和最后一个字符/](https://www.geeksforgeeks.org/count-substrings-with-same-first-and-last-characters/)

给我们一个字符串，我们需要找到以相同字符开始和结束的所有连续子字符串的计数。

**示例:**

```
Input  : S = "abcab"
Output : 7
There are 15 substrings of "abcab"
a, ab, abc, abca, abcab, b, bc, bca
bcab, c, ca, cab, a, ab, b
Out of the above substrings, there 
are 7 substrings : a, abca, b, bcab, 
c, a and b.

Input  : S = "aba"
Output : 4
The substrings are a, b, a and aba
```

**方法 1(简单):**在这种方法中，我们使用蛮力，找到所有的子字符串，并通过我们的函数 checkEquality 传递它们，看看开始和结束字符是否相同。

## C++

```
// C++ program to count all substrings with same
// first and last characters.
#include <bits/stdc++.h>
using namespace std;

// Returns true if first and last characters
// of s are same.
int checkEquality(string s)
{
    return (s[0] == s[s.size() - 1]);
}

int countSubstringWithEqualEnds(string s)
{
    int result = 0;
    int n = s.length();

    // Starting point of substring
    for (int i = 0; i < n; i++)

       // Length of substring
       for (int len = 1; len <= n-i; len++)

          // Check if current substring has same
          // starting and ending characters.
          if (checkEquality(s.substr(i, len)))
            result++;

    return result;
}

// Driver function
int main()
{
    string s("abcab");
    cout << countSubstringWithEqualEnds(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all substrings with same
// first and last characters.
public class GFG {

    // Returns true if first and last characters
    // of s are same.
    static boolean checkEquality(String s)
    {
        return (s.charAt(0) == s.charAt(s.length() - 1));
    }

    static int countSubstringWithEqualEnds(String s)
    {
        int result = 0;
        int n = s.length();

        // Starting point of substring
        for (int i = 0; i < n; i++)

           // Length of substring
           for (int len = 1; len <= n-i; len++)

              // Check if current substring has same
              // starting and ending characters.
              if (checkEquality(s.substring(i, i + len)))
                result++;

        return result;
    }

    // Driver function
    public static void main(String args[])
    {
        String s = "abcab";
        System.out.println(countSubstringWithEqualEnds(s));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```

# Python program to count all substrings with same
# first and last characters.

# Returns true if first and last characters
# of s are same.
def checkEquality(s):
    return (ord(s[0]) == ord(s[len(s) - 1]));

def countSubstringWithEqualEnds(s):
    result = 0;
    n = len(s);

    # Starting point of substring
    for i in range(n):

    # Length of substring
        for j in range(1,n-i+1):

        # Check if current substring has same
        # starting and ending characters.
            if (checkEquality(s[i:i+j])):
                result+=1;

    return result;

# Driver code
s = "abcab";
print(countSubstringWithEqualEnds(s));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to count all
// substrings with same
// first and last characters.
using System;

class GFG
{

    // Returns true if first and
    //  last characters of s are same.
    static bool checkEquality(string s)
    {
        return (s[0] == s[s.Length - 1]);
    }

    static int countSubstringWithEqualEnds(string s)
    {
        int result = 0;
        int n = s.Length;

        // Starting point of substring
        for (int i = 0; i < n; i++)

        // Length of substring
        for (int len = 1; len <= n-i; len++)

            // Check if current substring has same
            // starting and ending characters.
            if (checkEquality(s.Substring(i, len)))
                result++;

        return result;
    }

    // Driver code
    public static void Main()
    {
        string s = "abcab";
        Console.WriteLine(countSubstringWithEqualEnds(s));
    }
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all substrings
// with same first and last characters.

// Returns true if first and last
// characters of s are same.
function checkEquality($s)
{
    return ($s[0] == $s[strlen($s) - 1]);
}

function countSubstringWithEqualEnds($s)
{
    $result = 0;
    $n = strlen($s);

    // Starting point of substring
    for ($i = 0; $i < $n; $i++)

    // Length of substring
    for ($len = 1; $len <= $n - $i; $len++)

        // Check if current substring has same
        // starting and ending characters.
        if (checkEquality(substr($s, $i, $len)))
            $result++;

    return $result;
}

// Driver Code
$s = "abcab";
print(countSubstringWithEqualEnds($s));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// JavaScript program to count all substrings
// with same first and last characters.

// Returns true if first and last characters
// of s are same.
function checkEquality(s)
{
    return (s.charAt(0) == s.charAt(s.length - 1));
}

function countSubstringWithEqualEnds(s)
{
    var result = 0;
    var n = s.length;

    // Starting point of substring
    for (var i = 0; i < n; i++)

       // Length of substring
       for (var len = 1; len <= n-i; len++)

          // Check if current substring has same
          // starting and ending characters.
          if (checkEquality(s.substring(i, i + len)))
            result++;

    return result;
}

// Driver function

    var s = "abcab";
    document.write(countSubstringWithEqualEnds(s));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
7
```

虽然上面的代码工作正常，但是效率不高，因为它的时间复杂度是 O(n <sup>2</sup> )。请注意，长度为 n 的字符串有 n*(n+1)/2 个子字符串。这个解决方案还需要 O(n)个额外的空间，因为我们一个接一个地创建所有子字符串。

**方法 2(空间效率):**在这种方法中，我们实际上不生成子字符串，而是以这样的方式遍历字符串，以便我们可以轻松地比较第一个和最后一个字符。

## C++

```
// Space efficient C++ program to count all
// substrings with same first and last characters.
#include <bits/stdc++.h>
using namespace std;

int countSubstringWithEqualEnds(string s)
{
    int result = 0;
    int n = s.length();

    // Iterating through all substrings in
    // way so that we can find first and last
    // character easily
    for (int i=0; i<n; i++)
        for (int j=i; j<n; j++)
            if (s[i] == s[j])
                result++;

    return result;
}

// Driver function
int main()
{
    string s("abcab");
    cout << countSubstringWithEqualEnds(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Space efficient Java program to count all
// substrings with same first and last characters.
public class GFG {

    static int countSubstringWithEqualEnds(String s)
    {
        int result = 0;
        int n = s.length();

        // Iterating through all substrings in
        // way so that we can find first and last
        // character easily
        for (int i = 0; i < n; i++)
            for (int j = i; j < n; j++)
                if (s.charAt(i) == s.charAt(j))
                    result++;

        return result;
    }

    // Driver function
    public static void main(String args[])
    {
        String s = "abcab";
        System.out.println(countSubstringWithEqualEnds(s));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Space efficient Python3 program to count all
# substrings with same first and last characters.
def countSubstringWithEqualEnds(s):

    result = 0;
    n = len(s);

    # Iterating through all substrings in
    # way so that we can find first and
    # last character easily
    for i in range(n):
        for j in range(i, n):
            if (s[i] == s[j]):
                result = result + 1

    return result

# Driver Code
s = "abcab";
print(countSubstringWithEqualEnds(s))

# This code is contributed
# by Akanksha Rai
```

## C#

```
// Space efficient C# program to count all
// substrings with same first and last characters.
using System;

public class GFG {

    static int countSubstringWithEqualEnds(string s)
    {
        int result = 0;
        int n = s.Length;

        // Iterating through all substrings in
        // way so that we can find first and last
        // character easily
        for (int i = 0; i < n; i++)
            for (int j = i; j < n; j++)
                if (s[i] == s[j])
                    result++;

        return result;
    }

    // Driver function
    public static void Main()
    {
        string s = "abcab";
        Console.Write(countSubstringWithEqualEnds(s));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Space efficient PHP program to count all
// substrings with same first and last characters.

function countSubstringWithEqualEnds($s)
{
    $result = 0;
    $n = strlen($s);

    // Iterating through all substrings in
    // way so that we can find first and last
    // character easily
    for ($i = 0; $i < $n; $i++)
        for ($j = $i; $j < $n; $j++)
            if ($s[$i] == $s[$j])
                $result++;

    return $result;
}

// Driver Code
$s = "abcab";
echo countSubstringWithEqualEnds($s);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Space efficient javascript program to count all
// substrings with same first and last characters.
function countSubstringWithEqualEnds(s)
{
    var result = 0;
    var n = s.length;

    // Iterating through all substrings in
    // way so that we can find first and last
    // character easily
    for(i = 0; i < n; i++)
        for(j = i; j < n; j++)
            if (s.charAt(i) == s.charAt(j))
                result++;

    return result;
}

// Driver code
var s = "abcab";
document.write(countSubstringWithEqualEnds(s));

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
7
```

在上面的代码中，虽然我们已经将额外的空间减少到 O(1 ),但时间复杂度仍然是 O(n^2).

**方法 3(最佳方法):**现在如果我们仔细观察，那么我们可以意识到答案只是取决于原始字符串中字符的频率。例如在字符串 abcab 中，“a”的频率为 2，有助于回答的子串分别为 a、abca 和 a，共 3 个，由<sup>(频率为“a”+1)</sup>C<sub>2</sub>计算得出。

## C++

```
// Most efficient C++ program to count all 
// substrings with same first and last characters.
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;  // assuming lower case only

int countSubstringWithEqualEnds(string s)
{
    int result = 0;
    int n = s.length();

    // Calculating frequency of each character
    // in the string.
    int count[MAX_CHAR] = {0};
    for (int i=0; i<n; i++)
        count[s[i]-'a']++;

    // Computing result using counts
    for (int i=0; i<MAX_CHAR; i++)
        result += (count[i]*(count[i]+1)/2);

    return result;
}

// Driver function
int main()
{
    string s("abcab");
    cout << countSubstringWithEqualEnds(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Most efficient Java program to count all 
// substrings with same first and last characters.
public class GFG {

      // assuming lower case only
    static final int MAX_CHAR = 26; 

    static int countSubstringWithEqualEnds(String s)
    {
        int result = 0;
        int n = s.length();

        // Calculating frequency of each character
        // in the string.
        int[] count =  new int[MAX_CHAR];
        for (int i = 0; i < n; i++)
            count[s.charAt(i)-'a']++;

        // Computing result using counts
        for (int i = 0; i < MAX_CHAR; i++)
            result += (count[i] * (count[i] + 1) / 2);

        return result;
    }

    // Driver function
    public static void main(String args[])
    {
        String s = "abcab";
        System.out.println(countSubstringWithEqualEnds(s));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Most efficient Python program to count all
# substrings with same first and last characters.

MAX_CHAR = 26; # assuming lower case only

def countSubstringWithEqualEnds(s):
    result = 0;
    n = len(s);

    # Calculating frequency of each character
    # in the string.
    count = [0]*MAX_CHAR;
    for i in range(n):
        count[ord(s[i])-ord('a')]+=1;

    # Computing result using counts
    for i in range(MAX_CHAR):
        result += (count[i]*(count[i]+1)/2);

    return result;

# Driver code
s = "abcab";
print(countSubstringWithEqualEnds(s));

# This code is contributed by 29AjayKumar
```

## C#

```
// Most efficient C# program to count all
// substrings with same first and last characters.
using System;

class GFG {

    // assuming lower case only
    static readonly int MAX_CHAR = 26;

    static int countSubstringWithEqualEnds(String s)
    {
        int result = 0;
        int n = s.Length;

        // Calculating frequency of each character
        // in the string.
        int[] count = new int[MAX_CHAR];
        for (int i = 0; i < n; i++)
            count[s[i] - 'a']++;

        // Computing result using counts
        for (int i = 0; i < MAX_CHAR; i++)
            result += (count[i] * (count[i] + 1) / 2);

        return result;
    }

    // Driver code
    public static void Main()
    {
        String s = "abcab";
        Console.Write(countSubstringWithEqualEnds(s));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Most efficient PHP program to count all
// substrings with same first and last characters.
$MAX_CHAR = 26; // assuming lower case only

function countSubstringWithEqualEnds($s)
{
    global $MAX_CHAR;
    $result = 0;
    $n = strlen($s);

    // Calculating frequency of each
    // character in the string.
    $count = array_fill(0, $MAX_CHAR, 0);
    for ($i = 0; $i < $n; $i++)
        $count[ord($s[$i]) - ord('a')]++;

    // Computing result using counts
    for ($i = 0; $i < $MAX_CHAR; $i++)
        $result += ($count[$i] *
                   ($count[$i] + 1) / 2);

    return $result;
}

// Driver Code
$s = "abcab";
echo countSubstringWithEqualEnds($s);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Most efficient javascript program to count all 
// substrings with same first and last characters.

      // assuming lower case only
    var MAX_CHAR = 26; 

    function countSubstringWithEqualEnds(s)
    {
        var result = 0;
        var n = s.length;

        // Calculating frequency of each character
        // in the string.
        var count =  Array.from({length: MAX_CHAR}, (_, i) => 0);
        for (var i = 0; i < n; i++)
            count[s.charAt(i).charCodeAt(0)-'a'.charCodeAt(0)]++;

        // Computing result using counts
        for (var i = 0; i < MAX_CHAR; i++)
            result += (count[i] * (count[i] + 1) / 2);

        return result;
    }

    // Driver function
    var s = "abcab";
    document.write(countSubstringWithEqualEnds(s));

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
7
```

上述代码的时间复杂度为 O(n)，需要 O(1)个额外空间。
[递归解算首末字符相同的子串](https://www.geeksforgeeks.org/recursive-solution-count-substrings-first-last-characters/)
本文由 [**阿迪蒂亚·古普塔**](https://www.linkedin.com/in/aditya-gupta-437504a7?trk=hp-identity-name) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果您发现任何不正确的地方，或者您想分享更多关于上述主题的信息，请写评论..
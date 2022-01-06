# 在前面添加最少的字符组成字符串回文

> 原文:[https://www . geesforgeks . org/minimum-characters-add-front-make-string-回文/](https://www.geeksforgeeks.org/minimum-characters-added-front-make-string-palindrome/)

给定一个字符串，我们需要告诉最少的字符被添加在字符串前面，使字符串回文。
**例:**

```
Input  : str = "ABC"
Output : 2
We can make above string palindrome as "CBABC"
by adding 'B' and 'C' at front.

Input  : str = "AACECAAAA";
Output : 2
We can make above string palindrome as AAAACECAAAA
by adding two A's at front of string.
```

**天真的做法:**每次开始检查字符串是否是回文，如果不是，则删除最后一个字符，再次检查。当字符串变成一个回文或空字符串时，从末尾到现在删除的字符数将是答案，因为这些字符可以按照使字符串成为回文的顺序插入到原始字符串的开头。
以下是上述办法的实施情况:

## C++

```
// C++ program for getting minimum character to be
// added at front to make string palindrome
#include<bits/stdc++.h>
using namespace std;

// function for checking string is palindrome or not
bool ispalindrome(string s)
{
    int l = s.length();
    int j;

    for(int i = 0, j = l - 1; i <= j; i++, j--)
    {
        if(s[i] != s[j])
            return false;
    }
    return true;
}

// Driver code
int main()
{
    string s = "BABABAA";
    int cnt = 0;
    int flag = 0;

    while(s.length()>0)
    {
        // if string becomes palindrome then break
        if(ispalindrome(s))
        {
            flag = 1;
             break;
        }
        else
        {
        cnt++;

        // erase the last element of the string
        s.erase(s.begin() + s.length() - 1);
        }
    }

    // print the number of insertion at front
    if(flag)
        cout << cnt;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for getting minimum character to be
// added at front to make string palindrome

class GFG {

// function for checking string is palindrome or not
    static boolean ispalindrome(String s) {
        int l = s.length();

        for (int i = 0, j = l - 1; i <= j; i++, j--) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
        }
        return true;
    }

// Driver code
    public static void main(String[] args) {
        String s = "BABABAA";
        int cnt = 0;
        int flag = 0;

        while (s.length() > 0) {
            // if string becomes palindrome then break
            if (ispalindrome(s)) {
                flag = 1;
                break;
            } else {
                cnt++;

                // erase the last element of the string
                s = s.substring(0, s.length() - 1);
                //s.erase(s.begin() + s.length() - 1);
            }
        }

        // print the number of insertion at front
        if (flag == 1) {
            System.out.println(cnt);
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for getting minimum character
# to be added at front to make string palindrome

# function for checking string is
# palindrome or not
def ispalindrome(s):

    l = len(s)

    i = 0
    j = l - 1
    while i <= j:

        if(s[i] != s[j]):
            return False
        i += 1
        j -= 1

    return True

# Driver code
if __name__ == "__main__":

    s = "BABABAA"
    cnt = 0
    flag = 0

    while(len(s) > 0):

        # if string becomes palindrome then break
        if(ispalindrome(s)):
            flag = 1
            break

        else:
            cnt += 1

            # erase the last element of the string
            s = s[:-1]

    # print the number of insertion at front
    if(flag):
        print(cnt)

# This code is contributed by ita_c
```

## C#

```
// C# program for getting minimum character to be
// added at front to make string palindrome

using System;
public class GFG {

// function for checking string is palindrome or not
    static bool ispalindrome(String s) {
        int l = s.Length;

        for (int i = 0, j = l - 1; i <= j; i++, j--) {
            if (s[i] != s[j]) {
                return false;
            }
        }
        return true;
    }

// Driver code
    public static void Main() {
        String s = "BABABAA";
        int cnt = 0;
        int flag = 0;

        while (s.Length > 0) {
            // if string becomes palindrome then break
            if (ispalindrome(s)) {
                flag = 1;
                break;
            } else {
                cnt++;

                // erase the last element of the string
                s = s.Substring(0, s.Length - 1);
                //s.erase(s.begin() + s.length() - 1);
            }
        }

        // print the number of insertion at front
        if (flag == 1) {
            Console.WriteLine(cnt);
        }
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // function for checking string is palindrome or not
        function ispalindrome(s) {
            let l = s.length;
            let j;

            for (let i = 0, j = l - 1; i <= j; i++, j--) {
                if (s[i] != s[j])
                    return false;
            }
            return true;
        }

        // Driver code
        let s = "BABABAA";
        let cnt = 0;
        let flag = 0;

        while (s.length > 0)
        {

            // if string becomes palindrome then break
            if (ispalindrome(s)) {
                flag = 1;
                break;
            }
            else {
                cnt++;

                // erase the last element of the string
                s = s.substring(0, s.length - 1);
            }
        }

        // print the number of insertion at front
        if (flag)
            document.write(cnt);

     // This code is contributed by Potta Lokesh

    </script>
```

**输出:**

```
2
```

感谢马斯聪·库马尔提出这个方法。
**高效途径:**我们可以使用 [lps 数组的 KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)在 O(n)时间内高效解决这个问题**。
首先我们通过连接给定的字符串，一个特殊的字符和给定字符串的反向来连接字符串，然后我们将得到这个连接字符串的 lps 数组，回想一下 lps 数组的每个索引代表最长的适当前缀，也是后缀。我们可以用这个 lps 数组来解决这个问题。** 

```
For string = AACECAAAA
Concatenated String = AACECAAAA$AAAACECAA
LPS array will be {0, 1, 0, 0, 0, 1, 2, 2, 2, 
                   0, 1, 2, 2, 2, 3, 4, 5, 6, 7}
```

这里我们只对 lps 数组的最后一个值感兴趣，因为它向我们显示了与原始字符串前缀匹配的反向字符串的最大后缀，即这些字符已经满足回文属性。最后，使字符串成为回文所需的最小字符数是输入字符串的长度减去 lps 数组的最后一个条目。为了更好的理解
，请看下面的代码

## C++

```
// C++ program for getting minimum character to be
// added at front to make string palindrome
#include <bits/stdc++.h>
using namespace std;

// returns vector lps for given string str
vector<int> computeLPSArray(string str)
{
    int M = str.length();
    vector<int> lps(M);

    int len = 0;
    lps[0] = 0; // lps[0] is always 0

    // the loop calculates lps[i] for i = 1 to M-1
    int i = 1;
    while (i < M)
    {
        if (str[i] == str[len])
        {
            len++;
            lps[i] = len;
            i++;
        }
        else // (str[i] != str[len])
        {
            // This is tricky. Consider the example.
            // AAACAAAA and i = 7\. The idea is similar
            // to search step.
            if (len != 0)
            {
                len = lps[len-1];

                // Also, note that we do not increment
                // i here
            }
            else // if (len == 0)
            {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

// Method returns minimum character to be added at
// front to make string palindrome
int getMinCharToAddedToMakeStringPalin(string str)
{
    string revStr = str;
    reverse(revStr.begin(), revStr.end());

    // Get concatenation of string, special character
    // and reverse string
    string concat = str + "{content}quot; + revStr;

    //  Get LPS array of this concatenated string
    vector<int> lps = computeLPSArray(concat);

    // By subtracting last entry of lps vector from
    // string length, we will get our result
    return (str.length() - lps.back());
}

// Driver program to test above functions
int main()
{
    string str = "AACECAAAA";
    cout << getMinCharToAddedToMakeStringPalin(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for getting minimum character to be
// added at front to make string palindrome
import java.util.*;
class GFG
{

// returns vector lps for given string str
public static int[] computeLPSArray(String str)
{
    int n = str.length();
    int lps[] = new int[n];
    int i = 1, len = 0;
    lps[0] = 0; // lps[0] is always 0

    while (i < n)
    {
        if (str.charAt(i) == str.charAt(len))
        {
            len++;
            lps[i] = len;
            i++;
        }
        else
        {
            // This is tricky. Consider the example.
            // AAACAAAA and i = 7\. The idea is similar
            // to search step.
            if (len != 0)
            {
                len = lps[len - 1];

                // Also, note that we do not increment
                // i here
            }
            else
            {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

// Method returns minimum character to be added at
// front to make string palindrome
static int getMinCharToAddedToMakeStringPalin(String str)
{
    StringBuilder s = new StringBuilder();
    s.append(str);

    // Get concatenation of string, special character
    // and reverse string
    String rev = s.reverse().toString();
    s.reverse().append("{content}quot;).append(rev);

    // Get LPS array of this concatenated string
    int lps[] = computeLPSArray(s.toString());
    return str.length() - lps[s.length() - 1];
}

// Driver Code
public static void main(String args[])
{
    String str = "AACECAAAA";
    System.out.println(getMinCharToAddedToMakeStringPalin(str));
}
}

// This code is contributed by Sparsh Singhal
```

## 蟒蛇 3

```
# Python3 program for getting minimum
# character to be added at the front
# to make string palindrome

# Returns vector lps for given string str
def computeLPSArray(string):

    M = len(string)
    lps = [None] * M

    length = 0
    lps[0] = 0 # lps[0] is always 0

    # the loop calculates lps[i]
    # for i = 1 to M-1
    i = 1
    while i < M:

        if string[i] == string[length]:

            length += 1
            lps[i] = length
            i += 1

        else: # (str[i] != str[len])

            # This is tricky. Consider the example.
            # AAACAAAA and i = 7\. The idea is
            # similar to search step.
            if length != 0:

                length = lps[length - 1]

                # Also, note that we do not
                # increment i here

            else: # if (len == 0)

                lps[i] = 0
                i += 1

    return lps

# Method returns minimum character
# to be added at front to make
# string palindrome
def getMinCharToAddedToMakeStringPalin(string):

    revStr = string[::-1]

    # Get concatenation of string,
    # special character and reverse string
    concat = string + "{content}quot; + revStr

    # Get LPS array of this
    # concatenated string
    lps = computeLPSArray(concat)

    # By subtracting last entry of lps
    # vector from string length, we
    # will get our result
    return len(string) - lps[-1]

# Driver Code
if __name__ == "__main__":

    string = "AACECAAAA"
    print(getMinCharToAddedToMakeStringPalin(string))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program for getting minimum character to be 
// added at front to make string palindrome 
using System;
using System.Text;

public class GFG{

  // returns vector lps for given string str 
  public static int[] computeLPSArray(string str)
  {
    int n = str.Length;
    int[] lps = new int[n];
    int i = 1, len = 0;
    lps[0] = 0; // lps[0] is always 0 

    while (i < n) 
    {
      if (str[i] == str[len])
      {
        len++;
        lps[i] = len;
        i++;
      }
      else
      {
        // This is tricky. Consider the example. 
        // AAACAAAA and i = 7\. The idea is similar 
        // to search step.
        if (len != 0)
        {
          len = lps[len - 1];

          // Also, note that we do not increment 
          // i here 
        }
        else
        {
          lps[i] = 0;
          i++;
        }
      }
    }
    return lps;
  }

  // Method returns minimum character to be added at 
  // front to make string palindrome 
  static int getMinCharToAddedToMakeStringPalin(string str) 
  { 
    char[] s = str.ToCharArray();

    // Get concatenation of string, special character 
    // and reverse string 
    Array.Reverse( s );
    string rev = new string(s);

    string concat=  str + "{content}quot; + rev;

    // Get LPS array of this concatenated string
    int[] lps = computeLPSArray(concat);
    return str.Length - lps[concat.Length - 1];
  }

  // Driver Code
  static public void Main (){
    string str = "AACECAAAA"; 
    Console.WriteLine(getMinCharToAddedToMakeStringPalin(str));
  }
}

// This code is contributed by avanitrachhadiya2155
```

**输出:**

```
2
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
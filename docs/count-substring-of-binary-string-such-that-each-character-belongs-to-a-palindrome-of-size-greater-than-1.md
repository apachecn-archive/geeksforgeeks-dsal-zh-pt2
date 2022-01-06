# 对二进制串的子串进行计数，使每个字符都属于一个大于 1 的回文

> 原文:[https://www . geesforgeks . org/count-substring-of-binary-string-so-每个字符都属于一个大于 1 的回文/](https://www.geeksforgeeks.org/count-substring-of-binary-string-such-that-each-character-belongs-to-a-palindrome-of-size-greater-than-1/)

给定二进制字符串 **str** ，任务是统计给定字符串 **str** 的子字符串数量，使得子字符串的每个字符属于长度至少为 2 的回文子字符串。

**示例:**

> **输入:** S = "00111"
> **输出:** 6
> **解释:**
> 在给定的字符串中有 6 个这样的子串，使得每个字符属于大小大于 1 的回文，如{“00”、“0011”、“00111”、“11”、“111”、“11”}
> 
> **输入:**S = " 0001011 "
> T3】输出: 15

**方法:**想法是统计每个字符不属于回文子串的子串，然后从大小大于 1 的字符串的可能子串总数中减去这个计数。下面是步骤的图示:

*   可以观察到，如果我们取子串 a <sub>2</sub> a <sub>3</sub> …。a <sub>k-1</sub> (即没有起止字符)，那么它的每个字符都可能属于某个回文。**证明:**

```
If ai == ai-1 or ai == ai+1,
Then it belongs to a palindrome of length 2.

Otherwise, If ai != ai-1,
ai != ai+1 and ai+1 == ai-1,
Then, It belongs to a palindrome of size 3.
```

*   因此，有四种子字符串模式，其中每个字符都不属于回文:
    1.  “0111….11”
    2.  “100…..00”
    3.  “111….110”
    4.  “000….001”
*   最后，从长度可能大于 1 的子串总数中减去这个计数。

> Count =(N *(N–1)/2)–(每个字符不属于回文的子串计数)

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// substrings in binary string
// such that every character
// belongs to a palindrome

#include <bits/stdc++.h>
using namespace std;

// Function to to find the
// substrings in binary string
// such that every character
// belongs to a palindrome
int countSubstrings(string s)
{
    int n = s.length();

    // Total substrings
    int answer = (n * (n - 1)) / 2;

    int cnt = 1;
    vector<int> v;

    // Loop to store the count of
    // continuous characters in
    // the given string
    for (int i = 1; i < n; i++) {

        if (s[i] == s[i - 1])
            cnt++;
        else {
            v.push_back(cnt);
            cnt = 1;
        }
    }

    if (cnt > 0)
        v.push_back(cnt);

    // Subtract non special
    // strings from answer
    for (int i = 0;
         i < v.size() - 1; i++) {
        answer -= (v[i]
                   + v[i + 1]
                   - 1);
    }

    return answer;
}

// Driver Code
int main()
{
    // Given string s
    string s = "00111";

    // Function Call
    cout << countSubstrings(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the    
// substrings in binary string    
// such that every character        
// belongs to a palindrome    
import java.util.*;

class GFG{

// Function to to find the        
// substrings in binary string        
// such that every character    
// belongs to a palindrome        
public static int countSubstrings(String s)        
{    
    int n = s.length();        

    // Total substrings        
    int answer = (n * (n - 1)) / 2;        

    int cnt = 1;    
    Vector<Integer> v = new Vector<Integer>();    

    // Loop to store the count of    
    // continuous characters in        
    // the given string        
    for(int i = 1; i < n; i++)
    {    
        if (s.charAt(i) == s.charAt(i - 1))        
            cnt++;    
        else
        {        
            v.add(cnt);        
            cnt = 1;    
        }    
    }    
    if (cnt > 0)        
        v.add(cnt);        

    // Subtract non special        
    // strings from answer        
    for(int i = 0; i < v.size() - 1; i++)
    {        
        answer -= (v.get(i) +
                   v.get(i + 1) - 1);    
    }    
    return answer;        
}

// Driver code
public static void main(String[] args)
{    

    // Given string s    
    String s = "00111";        

    // Function call    
    System.out.print(countSubstrings(s));    
}    
}    

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to find the
# substrings in binary string
# such that every character
# belongs to a palindrome

# Function to find the substrings in
# binary string such that every
# character belongs to a palindrome
def countSubstrings (s):

    n = len(s)

    # Total substrings
    answer = (n * (n - 1)) // 2

    cnt = 1
    v = []

    # Loop to store the count
    # of continuous characters
    # in the given string
    for i in range(1, n):
        if (s[i] == s[i - 1]):
            cnt += 1

        else:
            v.append(cnt)
            cnt = 1

    if (cnt > 0):
        v.append(cnt)

    # Subtract non special strings
    # from answer
    for i in range(len(v) - 1):
        answer -= (v[i] + v[i + 1] - 1)

    return answer

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "00111"

    # Function call
    print(countSubstrings(s))

# This code is contributed by himanshu77
```

## C#

```
// C# implementation to find the    
// substrings in binary string    
// such that every character        
// belongs to a palindrome    
using System;
using System.Collections.Generic;

class GFG{

// Function to to find the        
// substrings in binary string        
// such that every character    
// belongs to a palindrome        
public static int countSubstrings(String s)        
{    
    int n = s.Length;        

    // Total substrings        
    int answer = (n * (n - 1)) / 2;        

    int cnt = 1;    
    List<int> v = new List<int>();    

    // Loop to store the count of    
    // continuous characters in        
    // the given string        
    for(int i = 1; i < n; i++)
    {    
        if (s[i] == s[i-1])        
            cnt++;    
        else
        {        
            v.Add(cnt);        
            cnt = 1;    
        }    
    }    
    if (cnt > 0)        
        v.Add(cnt);        

    // Subtract non special        
    // strings from answer        
    for(int i = 0; i < v.Count - 1; i++)
    {        
        answer -= (v[i] +
                   v[i + 1] - 1);    
    }    
    return answer;        
}

// Driver code
public static void Main(String[] args)
{    

    // Given string s    
    String s = "00111";        

    // Function call    
    Console.Write(countSubstrings(s));    
}    
}    

// This code contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to find the    
// substrings in binary string    
// such that every character        
// belongs to a palindrome    

// Function to to find the        
// substrings in binary string        
// such that every character    
// belongs to a palindrome        
function countSubstrings(s)        
{    
    var n = s.length;        

    // Total substrings        
    var answer = (n * (n - 1)) / 2;        

    var cnt = 1;    
    var v =[];    

    // Loop to store the count of    
    // continuous characters in        
    // the given string        
    for(var i = 1; i < n; i++)
    {    
        if (s.charAt(i) == s.charAt(i - 1))        
            cnt++;    
        else
        {        
            v.push(cnt);        
            cnt = 1;    
        }    
    }    
    if (cnt > 0)        
        v.push(cnt);        

    // Subtract non special        
    // strings from answer        
    for(var i = 0; i < v.length - 1; i++)
    {        
        answer -= (v[i] +
                   v[i + 1] - 1);    
    }    
    return answer;        
}

// Driver code
//Given string s    
var s = "00111";        

// Function call    
document.write(countSubstrings(s));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*
# 由交替的元音和辅音组成的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列-由元音和辅音交替组成/](https://www.geeksforgeeks.org/longest-subsequence-consisting-of-alternate-vowels-and-consonants/)

给定一个非空字符串 **S** ，任务是打印字符串 **S** 中包含交替元音和辅音的最长子序列。
**注意:**如果存在多个长度相同的子序列，打印字符 ASCII 值总和最大的子序列。
**示例:**

> **输入:**S = " geeks forges "
> **输出:**gesore
> **解释:**“gekorek”“gekores”“gekorek”“gekogeges”“gesorek”“gesore”“gesogek”“gesoge”“geforek”“gefores”“gefogek”和“gefoges”是辅音和元音交替出现的可能最长的子序列。“gesores”是字符的 ASCII 值之和最大的子序列，因此它是解决方案。
> 
> **输入:** S = "ababababab"
> **输出:** ababababab
> **说明:**“ababababab”是包含元音和辅音交替的最长可能子序列。

**方法:**
按照以下步骤解决问题:

*   将 **S** 第一个字符的 ASCII 值作为当前块的最大值( **maxi** )和字符类型存储在**标志**中。如果字符是辅音，则设置**标志**为 **0** ，否则设置 **1** 。
*   遍历字符串的其余部分。
*   对于每个字符，检查它是否属于与前一个字符相同的块。
*   如果属于同一个区块，将 **maxi** 更新为 max(第 i <sup>个</sup>字符的 maxi，ASCII 值)。
*   否则，将 ASCII 值 **maxi** 的字符追加到答案中。将当前第一个<sup>字符的 ASCII 值存储为 **maxi** 。将**标志**更新为**(标志+ 1)%2** 表示当前字符的类型。</sup>
*   遍历整个字符串后，将 ASCII 值为 **maxi** 的字符添加到答案中。打印代表子序列的最后一个字符串。

下面的代码是上述方法的实现:

## C++

```
// C++ program to find the longest
// subsequence containing alternating
// vowels and consonants
#include <bits/stdc++.h>
using namespace std;

// Function that return 1 or 0
// if the given character is
// vowel or consonant respectively
int isVowel(char c)
{

    // Returns 1 if c is vowel
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return 1;

    // Returns 0 if
    // c is consonant
    return 0;
}

// Function to find the longest
// subsequence containing
// alternate vowels and
// consonants
string Subsequence(string str)
{

    // Store the length
    // of the string
    int n = str.length();

    // Assume first character
    // to be consonant
    int flag = 0;

    // If first character is vowel
    if (isVowel(str[0]) == 1)
        flag = 1;

    // Store the ASCII value
    int maxi = (int)str[0];

    // Stores the final answer
    string ans = "";
    for(int i = 1; i < n; i++)
    {

        // If the current character belongs
        // to same category (Vowel / Consonant)
        // as the previous character
        if (isVowel(str[i]) == flag)
        {

            // Store the maximum ASCII value
            maxi = max(maxi, (int)str[i]);
        }

        // Otherwise
        else
        {

            // Store the character with
            // maximum ASCII value from
            // the previous block
            ans += (char)(maxi);

            // Store the ASCII of the
            // current character as the
            // maximum of the current block
            maxi = (int)str[i];

            // Switch the type of the
            // current block
            flag = (flag + 1) % 2;
        }
    }

    // Store the character with
    // maximum ASCII value
    // from the last block
    ans += (char)(maxi);

    // Return the result
    return ans;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";

    cout << (Subsequence(str));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest
// subsequence containing alternating
// vowels and consonants
import java.util.*;
import java.lang.*;
import java.io.*;
import java.math.*;

class GFG {

    // Function that return 1 or 0
    // if the given character is
    // vowel or consonant respectively
    static int isVowel(char c)
    {
        // Returns 1 if c is vowel
        if (c == 'a' || c == 'e'
            || c == 'i' || c == 'o'
            || c == 'u')
            return 1;

        // Returns 0 if
        // c is consonant
        return 0;
    }

    // Function to find the longest
    // subsequence containing
    // alternate vowels and
    // consonants
    static String Subsequence(String str)
    {
        // Store the length
        // of the string
        int n = str.length();

        // Assume first character
        // to be consonant
        int flag = 0;
        // If first character is vowel
        if (isVowel(str.charAt(0)) == 1)
            flag = 1;
        // Store the ASCII value
        int maxi = (int)str.charAt(0);
        // Stores the final answer
        String ans = "";
        for (int i = 1; i < n; i++) {
            // If the current character belongs
            // to same category (Vowel / Consonant)
            // as the previous character
            if (isVowel(str.charAt(i)) == flag) {
                // Store the maximum ASCII value
                maxi = Math.max(maxi,
                                (int)str.charAt(i));
            }
            // Otherwise
            else {
                // Store the character with
                // maximum ASCII value from
                // the previous block
                ans += (char)(maxi);
                // Store the ASCII of the
                // current character as the
                // maximum of the current block
                maxi = (int)str.charAt(i);
                // Switch the type of the
                // current block
                flag = (flag + 1) % 2;
            }
        }
        // Store the character with
        // maximum ASCII value
        // from the last block
        ans += (char)(maxi);

        // Return the result
        return ans;
    }

    // Driver Program
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        System.out.println(Subsequence(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the longest
# subsequence containing alternating
# vowels and consonants

def isVowel(c):

    # boolean function that check whether
    # the given char is vowel or not
    # and returns a boolean value respectively
    vowels=['a','e','i','o','u']
    if(c in vowels):
        return True
    return False
def Subsequence(str):

    #string that stores the final result
    ans=''
    flag=(isVowel(str[0]))

    #taking the first character
    #as the maximum ASCII valued char
    maxi=ord(str[0])
    for i in range(1,len(str)):

        # If the current character belongs to
        # same category(Vowel / Consonant) as the
        # previous character
        if (isVowel(str[i]) == flag):

            # choosing a maximum ASCII valued char
            maxi=max(maxi,ord(str[i]))

        #otherwise
        else:
            ans=ans+chr(maxi)
            maxi=ord(str[i])

            #toggling the flag
            flag=not(flag)

    #adding the last char to the answer
    ans=ans+chr(maxi)
    return ans

#Driver program
if __name__ == "__main__":
    input_string ='geeksforgeeks'
    print(Subsequence(input_string))

# Contributed by
# Nvss Maneesh Gupta
```

## C#

```
// C# program to find the longest
// subsequence containing alternating
// vowels and consonants
using System;

class GFG{

// Function that return 1 or 0
// if the given character is
// vowel or consonant respectively
static int isVowel(char c)
{

    // Returns 1 if c is vowel
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return 1;

    // Returns 0 if
    // c is consonant
    return 0;
}

// Function to find the longest
// subsequence containing
// alternate vowels and
// consonants
static String Subsequence(String str)
{

    // Store the length
    // of the string
    int n = str.Length;

    // Assume first character
    // to be consonant
    int flag = 0;

    // If first character is vowel
    if (isVowel(str[0]) == 1)
        flag = 1;

    // Store the ASCII value
    int maxi = (int)str[0];

    // Stores the readonly answer
    String ans = "";

    for(int i = 1; i < n; i++)
    {

    // If the current character belongs
    // to same category (Vowel / Consonant)
    // as the previous character
    if (isVowel(str[i]) == flag)
    {

        // Store the maximum ASCII value
        maxi = Math.Max(maxi, (int)str[i]);
    }

    // Otherwise
    else
    {

        // Store the character with
        // maximum ASCII value from
        // the previous block
        ans += (char)(maxi);

        // Store the ASCII of the
        // current character as the
        // maximum of the current block
        maxi = (int)str[i];

        // Switch the type of the
        // current block
        flag = (flag + 1) % 2;
    }
    }

    // Store the character with
    // maximum ASCII value
    // from the last block
    ans += (char)(maxi);

    // Return the result
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";

    Console.WriteLine(Subsequence(str));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the longest
// subsequence containing alternating
// vowels and consonants

// Function that return 1 or 0
// if the given character is
// vowel or consonant respectively
function isVowel(c)
{

    // Returns 1 if c is vowel
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return 1;

    // Returns 0 if
    // c is consonant
    return 0;
}

// Function to find the longest
// subsequence containing
// alternate vowels and
// consonants
function Subsequence(str)
{

    // Store the length
    // of the string
    var n = str.length;

    // Assume first character
    // to be consonant
    var flag = 0;

    // If first character is vowel
    if (isVowel(str[0]) == 1)
        flag = 1;

    // Store the ASCII value
    var maxi = (str[0].charCodeAt(0));

    // Stores the final answer
    var ans = "";
    for(var i = 1; i < n; i++)
    {

        // If the current character belongs
        // to same category (Vowel / Consonant)
        // as the previous character
        if (isVowel(str[i]) == flag)
        {

            // Store the maximum ASCII value
            maxi = Math.max(maxi, str[i].charCodeAt(0));
        }

        // Otherwise
        else
        {

            // Store the character with
            // maximum ASCII value from
            // the previous block
            ans += String.fromCharCode(maxi);

            // Store the ASCII of the
            // current character as the
            // maximum of the current block
            maxi = str[i].charCodeAt(0);

            // Switch the type of the
            // current block
            flag = (flag + 1) % 2;
        }
    }

    // Store the character with
    // maximum ASCII value
    // from the last block
    ans += String.fromCharCode(maxi);

    // Return the result
    return ans;
}

// Driver code
var str = "geeksforgeeks";
document.write(Subsequence(str));

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
gesores
```

***时间复杂度:**O(N)*T4】
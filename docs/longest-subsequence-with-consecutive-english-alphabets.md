# 具有连续英文字母的最长子序列

> 原文:[https://www . geeksforgeeks . org/最长连续英文字母序列/](https://www.geeksforgeeks.org/longest-subsequence-with-consecutive-english-alphabets/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到连续小写字母的最长子序列的长度。

**示例:**

> ***输入:** S = "acbdcfhg"*
> ***输出:** 3*
> ***解释:***
> *字符串“abc”是连续小写字母的最长子序列。*
> *因此，打印 3 因为它是子序列“abc”的长度。*
> 
> ***输入:***S = " g*abbscdggbe "*
> ***输出:** 5*

**简单方法:**最简单的方法是[生成给定字符串的所有可能的子序列](https://www.geeksforgeeks.org/print-subsequences-string/)，如果给定字符串中存在任何具有连续字符且最大长度的子序列，则打印该长度。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

***高效方法:*** 上述方法也可以通过[从每个小写字母开始生成给定字符串的所有可能的连续子序列](https://www.geeksforgeeks.org/longest-consecutive-subsequence/)并打印找到的所有子序列中的最大值来优化。按照以下步骤解决问题:

*   初始化一个变量，比如说 **ans，**为 **0** ，存储连续子序列的最大长度。
*   对于超出范围**【a，z】**的每个字符 **ch** 执行以下操作:
    *   将变量 **cnt** 初始化为 **0** ，该变量存储从 **ch** 开始的连续字符子序列的长度。
    *   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果当前字符是 **ch** ，那么将 **cnt** 增加 **1** ，并将当前字符 ch 更新为下一个字符 **(ch + 1)** 。
    *   更新**年=最大(年，cnt)**
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of subsequence
// starting with character ch
int findSubsequence(string S, char ch)
{
    // Length of the string
    int N = S.length();

    // Stores the maximum length
    int ans = 0;

    // Traverse the given string
    for (int i = 0; i < N; i++) {

        // If s[i] is required
        // character ch
        if (S[i] == ch) {

            // Increment  ans by 1
            ans++;

            // Increment  character ch
            ch++;
        }
    }

    // Return the current maximum
    // length with character ch
    return ans;
}

// Function to find the maximum length
// of subsequence of consecutive
// characters
int findMaxSubsequence(string S)
{
    // Stores the maximum length of
    // consecutive characters
    int ans = 0;

    for (char ch = 'a'; ch <= 'z'; ch++) {

        // Update ans
        ans = max(ans, findSubsequence(S, ch));
    }

    // Return the maximum length of
    // subsequence
    return ans;
}

// Driver Code
int main()
{
    // Input
    string S = "abcabefghijk";

    // Function Call
    cout << findMaxSubsequence(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C# program for the above approach
import java.io.*;
import java.util.*;
import java.util.Arrays;

class GFG{

// Function to find the length of subsequence
// starting with character ch
static int findSubsequence(String S, char ch)
{

    // Length of the string
    int N = S.length();

    // Stores the maximum length
    int ans = 0;

    // Traverse the given string
    for(int i = 0; i < N; i++)
    {

        // If s[i] is required
        // character ch
         if(S.charAt(i) == ch)
        {

            // Increment  ans by 1
            ans++;

            // Increment  character ch
            ch++;
        }
    }

    // Return the current maximum
    // length with character ch
    return ans;
}

// Function to find the maximum length
// of subsequence of consecutive
// characters
static int findMaxSubsequence(String S)
{

    // Stores the maximum length of
    // consecutive characters
    int ans = 0;

    for(char ch = 'a'; ch <= 'z'; ch++)
    {

        // Update ans
        ans = Math.max(ans, findSubsequence(S, ch));
    }

    // Return the maximum length of
    // subsequence
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    String S = "abcabefghijk";

    // Function Call
    System.out.print(findMaxSubsequence(S));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of subsequence
# starting with character ch
def findSubsequence(S, ch):
    # Length of the string
    N = len(S)

    # Stores the maximum length
    ans = 0

    # Traverse the given string
    for i in range(N):

        # If s[i] is required
        # character ch
        if (S[i] == ch):

            # Increment  ans by 1
            ans += 1

            # Increment  character ch
            ch=chr(ord(ch) + 1)

    # Return the current maximum
    # length with character ch
    return ans

# Function to find the maximum length
# of subsequence of consecutive
# characters
def findMaxSubsequence(S):
    #Stores the maximum length of
    # consecutive characters
    ans = 0

    for ch in range(ord('a'),ord('z') + 1):
        # Update ans
        ans = max(ans, findSubsequence(S, chr(ch)))

    # Return the maximum length of
    # subsequence
    return ans

# Driver Code
if __name__ == '__main__':
    # Input
    S = "abcabefghijk"

    # Function Call
    print (findMaxSubsequence(S))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the length of subsequence
// starting with character ch
static int findSubsequence(string S, char ch)
{

    // Length of the string
    int N = S.Length;

    // Stores the maximum length
    int ans = 0;

    // Traverse the given string
    for(int i = 0; i < N; i++)
    {

        // If s[i] is required
        // character ch
        if (S[i] == ch)
        {

            // Increment  ans by 1
            ans++;

            // Increment  character ch
            ch++;
        }
    }

    // Return the current maximum
    // length with character ch
    return ans;
}

// Function to find the maximum length
// of subsequence of consecutive
// characters
static int findMaxSubsequence(string S)
{

    // Stores the maximum length of
    // consecutive characters
    int ans = 0;

    for(char ch = 'a'; ch <= 'z'; ch++)
    {

        // Update ans
        ans = Math.Max(ans, findSubsequence(S, ch));
    }

    // Return the maximum length of
    // subsequence
    return ans;
}

// Driver Code
public static void Main()
{

    // Input
    string S = "abcabefghijk";

    // Function Call
    Console.Write(findMaxSubsequence(S));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the length of subsequence
// starting with character ch
function findSubsequence(S,ch)
{
    // Length of the string
    let N = S.length;

    // Stores the maximum length
    let ans = 0;

    // Traverse the given string
    for(let i = 0; i < N; i++)
    {

        // If s[i] is required
        // character ch
        if (S[i] == ch)
        {

            // Increment  ans by 1
            ans++;

            // Increment  character ch
            ch=String.fromCharCode(ch.charCodeAt(0)+1);
        }
    }

    // Return the current maximum
    // length with character ch
    return ans;
}

// Function to find the maximum length
// of subsequence of consecutive
// characters
function findMaxSubsequence(S)
{
    // Stores the maximum length of
    // consecutive characters
    let ans = 0;

    for(let ch = 'a'.charCodeAt(0); ch <= 'z'.charCodeAt(0); ch++)
    {

        // Update ans
        ans = Math.max(ans, findSubsequence(S, String.fromCharCode(ch)));
    }

    // Return the maximum length of
    // subsequence
    return ans;
}

// Driver Code
let S = "abcabefghijk";

// Function Call
document.write(findMaxSubsequence(S));

// This code is contributed by patel2127
</script>
```

**Output**

```
7
```

***时间复杂度:** O(26*N)*
***辅助空间:** O(1)*
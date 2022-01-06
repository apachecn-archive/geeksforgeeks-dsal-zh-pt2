# 一个给定字符串需要连接成另一个字符串的子串的最大次数

> 原文:[https://www . geeksforgeeks . org/给定字符串需要连接以形成另一个字符串的子字符串的最大次数/](https://www.geeksforgeeks.org/maximum-number-of-times-a-given-string-needs-to-be-concatenated-to-form-a-substring-of-another-string/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S1** 和 **S2** ，任务是找出字符串 **S2** 需要串联的次数的最大值，使其成为字符串 **S1** 的子串。

**示例:**

> **输入:**S1 =“ababc”，S2 =“ab”
> **输出:** 2
> **解释:**将 S2 恰好串联两次后，字符串修改为“abab”。因此，字符串“abab”是“ababc”的子字符串。因此，结果是 2。
> 
> **输入:**S1 =“ababc”，S2 =“ba”
> **输出:** 1
> **说明:**字符串“ba”已经是“ababc”的子串。因此，结果是 1。

**方法:**要解决给定的问题，想法使用 [KMP 算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**，来存储最大值 **K** ，这样串联**S2**T6】K 次就形成了字符串 **S1** 的子串。
*   初始化一个字符串 **curWord** ，复制 **curWord** 中 **S2** 的内容。
*   将一个字符串可以出现的最大次数存储为 **numWords = N / M** 。
*   在索引**【0，numWords–1】**上遍历字符串，并执行以下步骤:
    *   如果在字符串 **S1** 中找到 **curWord** 的值，那么将 **ans** 加 1，并将 **curWord** 与**单词**连接起来。
    *   否则，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find lps[] for given
// pattern pat[0..M-1]
void computeLPSArray(string pat, int M,
                     int* lps)
{
    // Length of the previous
    // longest prefix suffix
    int len = 0;

    // lps[0] is always 0
    lps[0] = 0;

    // Iterate string to calculate lps[i]
    int i = 1;
    while (i < M) {

        // If the current character
        // of the pattern matches
        if (pat[i] == pat[len]) {
            len++;
            lps[i] = len;
            i++;
        }

        // Otherwise
        else {

            if (len != 0) {

                len = lps[len - 1];
            }

            // Otherwise
            else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

// Function to implement KMP algorithm
int KMPSearch(string pat, string txt)
{
    int M = pat.size();
    int N = txt.size();

    // Stores the longest prefix and
    // suffix values for pattern
    int lps[M];

    // Preprocess the pattern and
    // find the lps[] array
    computeLPSArray(pat, M, lps);

    // Index for txt[]
    int i = 0;

    // Index for pat[]
    int j = 0;
    while (i < N) {

        if (pat[j] == txt[i]) {
            j++;
            i++;
        }

        // If pattern is found return 1
        if (j == M) {
            return 1;
            j = lps[j - 1];
        }

        // Mismatch after j matches
        else if (i < N
                 && pat[j] != txt[i]) {

            // Don't match lps[0, lps[j - 1]]
            // characters they will
            // match anyway
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }

    // Return 0 if the pattern is not found
    return 0;
}

// Function to find the maximum value
// K for which string S2 concatenated
// K times is a substring of string S1
void maxRepeating(string seq, string word)
{
    // Store the required maximum number
    int resCount = 0;

    // Create a temporary string to store
    // string word
    string curWord = word;

    // Store the maximum number of times
    // string S2 can occur in string S1
    int numWords = seq.length() / word.length();

    // Traverse in range[0, numWords-1]
    for (int i = 0; i < numWords; i++) {

        // If curWord is found in sequence
        if (KMPSearch(curWord, seq)) {

            // Concatenate word to curWord
            curWord += word;

            // Increment resCount by 1
            resCount++;
        }

        // Otherwise break the loop
        else
            break;
    }

    // Print the answer
    cout << resCount;
}

// Driver Code
int main()
{
    string S1 = "ababc", S2 = "ab";

    // Function Call
    maxRepeating(S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to find lps[] for given
    // pattern pat[0..M-1]
    static void computeLPSArray(String pat, int M,
                         int []lps)
    {
        // Length of the previous
        // longest prefix suffix
        int len = 0;

        // lps[0] is always 0
        lps[0] = 0;

        // Iterate string to calculate lps[i]
        int i = 1;
        while (i < M)
        {

            // If the current character
            // of the pattern matches
            if (pat.charAt(i) == pat.charAt(len))
            {
                len++;
                lps[i] = len;
                i++;
            }

            // Otherwise
            else
            {
                if (len != 0)
                {   
                    len = lps[len - 1];
                }

                // Otherwise
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }

    // Function to implement KMP algorithm
    static int KMPSearch(String pat, String txt)
    {
        int M = pat.length();
        int N = txt.length();

        // Stores the longest prefix and
        // suffix values for pattern
        int lps[] = new int[M];

        // Preprocess the pattern and
        // find the lps[] array
        computeLPSArray(pat, M, lps);

        // Index for txt[]
        int i = 0;

        // Index for pat[]
        int j = 0;
        while (i < N)
        {   
            if (pat.charAt(j) == txt.charAt(i))
            {
                j++;
                i++;
            }

            // If pattern is found return 1
            if (j == M)
            {
                return 1;
                //j = lps[j - 1];
            }

            // Mismatch after j matches
            else if (i < N
                     && pat.charAt(j) != txt.charAt(i))
            {

                // Don't match lps[0, lps[j - 1]]
                // characters they will
                // match anyway
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }

        // Return 0 if the pattern is not found
        return 0;
    }

    // Function to find the maximum value
    // K for which string S2 concatenated
    // K times is a substring of string S1
    static void maxRepeating(String seq, String word)
    {

        // Store the required maximum number
        int resCount = 0;

        // Create a temporary string to store
        // string word
        String curWord = word;

        // Store the maximum number of times
        // string S2 can occur in string S1
        int numWords = seq.length() / word.length();

        // Traverse in range[0, numWords-1]
        for (int i = 0; i < numWords; i++)
        {

            // If curWord is found in sequence
            if (KMPSearch(curWord, seq) == 1)
            {

                // Concatenate word to curWord
                curWord += word;

                // Increment resCount by 1
                resCount++;
            }

            // Otherwise break the loop
            else
                break;
        }

        // Print the answer
        System.out.print(resCount);
    }

    // Driver Code
    public static void main (String[] args)
    {       
        String S1 = "ababc", S2 = "ab";

        // Function Call
        maxRepeating(S1, S2);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find lps[] for given
# pattern pat[0..M-1]
def computeLPSArray(pat, M, lps):

    # Length of the previous
    # longest prefix suffix
    lenn = 0

    # lps[0] is always 0
    lps[0] = 0

    # Iterate string to calculate lps[i]
    i = 1
    while (i < M):

        # If the current character
        # of the pattern matches
        if (pat[i] == pat[lenn]):
            lenn += 1
            lps[i] = lenn
            i += 1

        # Otherwise
        else:
            if (lenn != 0):
                lenn = lps[lenn - 1]

            # Otherwise
            else:
                lps[i] = 0
                i += 1

# Function to implement KMP algorithm
def KMPSearch(pat, txt):
    M = len(pat)
    N = len(txt)

    # Stores the longest prefix and
    # suffix values for pattern
    lps = [0 for i in range(M)]

    # Preprocess the pattern and
    # find the lps[] array
    computeLPSArray(pat, M, lps)

    # Index for txt[]
    i = 0

    # Index for pat[]
    j = 0
    while (i < N):

        if (pat[j] == txt[i]):
            j += 1
            i += 1

        # If pattern is found return 1
        if (j == M):
            return 1
            j = lps[j - 1]

        # Mismatch after j matches
        elif (i < N and pat[j] != txt[i]):

            # Don't match lps[0, lps[j - 1]]
            # characters they will
            # match anyway
            if (j != 0):
                j = lps[j - 1]
            else:
                i = i + 1

    # Return 0 if the pattern is not found
    return 0

# Function to find the maximum value
# K for which S2 concatenated
# K times is a subof S1
def maxRepeating(seq, word):

    # Store the required maximum number
    resCount = 0

    # Create a temporary to store
    # word
    curWord = word

    # Store the maximum number of times
    # S2 can occur in S1
    numWords = len(seq) // len(word)

    # Traverse in range[0, numWords-1]
    for i in range(numWords):

        # If curWord is found in sequence
        if (KMPSearch(curWord, seq)):

            # Concatenate word to curWord
            curWord += word

            # Increment resCount by 1
            resCount += 1

        # Otherwise break the loop
        else:
            break

    # Print the answer
    print(resCount)

# Driver Code
if __name__ == '__main__':
    S1,S2 = "ababc","ab"

    # Function Call
    maxRepeating(S1, S2)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find lps[] for given
    // pattern pat[0..M-1]
    static void computeLPSArray(String pat, int M,
                         int []lps)
    {
        // Length of the previous
        // longest prefix suffix
        int len = 0;

        // lps[0] is always 0
        lps[0] = 0;

        // Iterate string to calculate lps[i]
        int i = 1;
        while (i < M)
        {

            // If the current character
            // of the pattern matches
            if (pat[i] == pat[len])
            {
                len++;
                lps[i] = len;
                i++;
            }

            // Otherwise
            else
            {
                if (len != 0)
                {   
                    len = lps[len - 1];
                }

                // Otherwise
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }

    // Function to implement KMP algorithm
    static int KMPSearch(String pat, String txt)
    {
        int M = pat.Length;
        int N = txt.Length;

        // Stores the longest prefix and
        // suffix values for pattern
        int []lps = new int[M];

        // Preprocess the pattern and
        // find the lps[] array
        computeLPSArray(pat, M, lps);

        // Index for txt[]
        int i = 0;

        // Index for pat[]
        int j = 0;
        while (i < N)
        {   
            if (pat[j] == txt[i])
            {
                j++;
                i++;
            }

            // If pattern is found return 1
            if (j == M)
            {
                return 1;
                //j = lps[j - 1];
            }

            // Mismatch after j matches
            else if (i < N
                     && pat[j] != txt[i])
            {

                // Don't match lps[0, lps[j - 1]]
                // characters they will
                // match anyway
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }

        // Return 0 if the pattern is not found
        return 0;
    }

    // Function to find the maximum value
    // K for which string S2 concatenated
    // K times is a substring of string S1
    static void maxRepeating(String seq, String word)
    {

        // Store the required maximum number
        int resCount = 0;

        // Create a temporary string to store
        // string word
        String curWord = word;

        // Store the maximum number of times
        // string S2 can occur in string S1
        int numWords = seq.Length / word.Length;

        // Traverse in range[0, numWords-1]
        for (int i = 0; i < numWords; i++)
        {

            // If curWord is found in sequence
            if (KMPSearch(curWord, seq) == 1)
            {

                // Concatenate word to curWord
                curWord += word;

                // Increment resCount by 1
                resCount++;
            }

            // Otherwise break the loop
            else
                break;
        }

        // Print the answer
        Console.Write(resCount);
    }

    // Driver Code
    public static void Main(String[] args)
    {       
        String S1 = "ababc", S2 = "ab";

        // Function Call
        maxRepeating(S1, S2);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find lps[] for given
// pattern pat[0..M-1]
function computeLPSArray(pat, M, lps)
{
    // Length of the previous
    // longest prefix suffix
    var len = 0;

    // lps[0] is always 0
    lps[0] = 0;

    // Iterate string to calculate lps[i]
    var i = 1;
    while (i < M) {

        // If the current character
        // of the pattern matches
        if (pat[i] == pat[len]) {
            len++;
            lps[i] = len;
            i++;
        }

        // Otherwise
        else {

            if (len != 0) {

                len = lps[len - 1];
            }

            // Otherwise
            else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

// Function to implement KMP algorithm
function KMPSearch(pat, txt)
{
    var M = pat.length;
    var N = txt.length;

    // Stores the longest prefix and
    // suffix values for pattern
    var lps = Array(M);

    // Preprocess the pattern and
    // find the lps[] array
    computeLPSArray(pat, M, lps);

    // Index for txt[]
    var i = 0;

    // Index for pat[]
    var j = 0;
    while (i < N) {

        if (pat[j] == txt[i]) {
            j++;
            i++;
        }

        // If pattern is found return 1
        if (j == M) {
            return 1;
            j = lps[j - 1];
        }

        // Mismatch after j matches
        else if (i < N
                 && pat[j] != txt[i]) {

            // Don't match lps[0, lps[j - 1]]
            // characters they will
            // match anyway
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }

    // Return 0 if the pattern is not found
    return 0;
}

// Function to find the maximum value
// K for which string S2 concatenated
// K times is a substring of string S1
function maxRepeating(seq, word)
{
    // Store the required maximum number
    var resCount = 0;

    // Create a temporary string to store
    // string word
    var curWord = word;

    // Store the maximum number of times
    // string S2 can occur in string S1
    var numWords = seq.length / word.length;

    // Traverse in range[0, numWords-1]
    for (var i = 0; i < numWords; i++) {

        // If curWord is found in sequence
        if (KMPSearch(curWord, seq)) {

            // Concatenate word to curWord
            curWord += word;

            // Increment resCount by 1
            resCount++;
        }

        // Otherwise break the loop
        else
            break;
    }

    // Print the answer
    document.write( resCount);
}

// Driver Code
var S1 = "ababc", S2 = "ab";

// Function Call
maxRepeating(S1, S2);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(M)*
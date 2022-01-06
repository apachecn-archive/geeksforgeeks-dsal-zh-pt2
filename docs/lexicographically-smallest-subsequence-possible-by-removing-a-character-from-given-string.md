# 从给定字符串中删除一个字符可能得到的字典上最小的子序列

> 原文:[https://www . geeksforgeeks . org/从给定字符串中删除一个可能的最小子序列/](https://www.geeksforgeeks.org/lexicographically-smallest-subsequence-possible-by-removing-a-character-from-given-string/)

给定一个长度为 **N** 的字符串 **S** ，任务是找到长度为**(N–1)**的字典最小子序列，即从给定字符串中删除一个字符。

**示例:**

> **输入:** S = "geeksforgeeks"
> **输出:**【eeksforgeks "
> **解释:**字典上最小的可能子序列是“eeksforgeks”。
> 
> **输入:** S = "zxvsjas"
> **输出:**【xvsjas "
> **解释:**从词汇学上讲，最小的可能子序列是“xvsjas”。

**简单方法:**最简单的方法是[从给定的字符串生成长度为**(N–1)**的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并将[所有子序列](https://www.geeksforgeeks.org/print-subsequences-string/)存储在[数组](https://www.geeksforgeeks.org/array-data-structure/)中。现在，[对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，并在 **0 <sup>第</sup>个位置**打印出最小的字典顺序子序列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest subsequence of length N-1
void firstSubsequence(string s)
{
    vector<string> allsubseq;

    string k;

    // Generate all subsequence of
    // length N-1
    for (int i = 0; i < s.length(); i++) {

        // Store main value of string str
        k = s;

        // Erasing element at position i
        k.erase(i, 1);
        allsubseq.push_back(k);
    }

    // Sort the vector
    sort(allsubseq.begin(),
         allsubseq.end());

    // Print first element of vector
    cout << allsubseq[0];
}

// Driver Code
int main()
{
    // Given string S
    string S = "geeksforgeeks";

    // Function Call
    firstSubsequence(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the lexicographically
// smallest subsequence of length N-1
static void firstSubsequence(String s)
{
    Vector<String> allsubseq = new Vector<>();

    // Generate all subsequence of
    // length N-1
    for(int i = 0; i < s.length(); i++)
    {
        String k = "";

        // Store main value of String str
        for(int j = 0; j < s.length(); j++)
        {
            if (i != j)
            {
                k += s.charAt(j);
            }
        }
        allsubseq.add(k);
    }

    // Sort the vector
    Collections.sort(allsubseq);

    // Print first element of vector
    System.out.print(allsubseq.get(0));
}

// Driver Code
public static void main(String[] args)
{

    // Given String S
    String S = "geeksforgeeks";

    // Function Call
    firstSubsequence(S);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the lexicographically
# smallest subsequence of length N-1
def firstSubsequence(s):

    allsubseq = []

    k = []

    # Generate all subsequence of
    # length N-1
    for i in range(len(s)):

        # Store main value of string str
        k = [i for i in s]

        # Erasing element at position i
        del k[i]
        allsubseq.append("".join(k))

    # Sort the vector
    allsubseq = sorted(allsubseq)

    # Print first element of vector
    print(allsubseq[0])

# Driver Code
if __name__ == '__main__':

    # Given string S
    S = "geeksforgeeks"

    # Function Call
    firstSubsequence(S)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the lexicographically
// smallest subsequence of length N-1
static void firstSubsequence(string s)
{
    List<string> allsubseq = new List<string>();

    // Generate all subsequence of
    // length N-1
    for(int i = 0; i < s.Length; i++)
    {
        string k = "";

        // Store main value of string str
        for(int j = 0; j < s.Length; j++)
        {
            if (i != j)
            {
                k += s[j];
            }
        }
        allsubseq.Add(k);
    }

    // Sort the vector
    allsubseq.Sort();

    // Print first element of vector
    Console.WriteLine(allsubseq[0]);
}

// Driver Code
public static void Main()
{

    // Given string S
    string S = "geeksforgeeks";

    // Function Call
    firstSubsequence(S);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the lexicographically
// smallest subsequence of length N-1
function firstSubsequence(s)
{
    let allsubseq = [];

    // Generate all subsequence of
    // length N-1
    for(let i = 0; i < s.length; i++)
    {
        let k = "";

        // Store main value of String str
        for(let j = 0; j < s.length; j++)
        {
            if (i != j)
            {
                k += s[j];
            }
        }
        allsubseq.push(k);
    }

    // Sort the vector
    (allsubseq).sort();

    // Print first element of vector
    document.write(allsubseq[0]);
}

// Driver Code

// Given String S
let S = "geeksforgeeks";

// Function Call
firstSubsequence(S);

// This code is contributed by patel2127
</script>
```

**输出:**

```
eeksforgeeks
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*

**高效方法:**优化上述方法，思路是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)检查 **i <sup>第</sup>个字符**是否大于 **(i + 1) <sup>第</sup>个字符**，然后简单删除**I**T14】第个字符，打印剩余字符串。否则，删除最后一个元素并打印所需的子序列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest subsequence of length N-1
void firstSubsequence(string s)
{
    // Store index of character
    // to be deleted
    int isMax = -1;

    // Traverse the string
    for (int i = 0;
         i < s.length() - 1; i++) {

        // If ith character > (i + 1)th
        // character then store it
        if (s[i] > s[i + 1]) {
            isMax = i;
            break;
        }
    }

    // If any character found in non
    // alphabetical order then remove it
    if (isMax >= 0) {
        s.erase(isMax, 1);
    }

    // Otherwise remove last character
    else {
        s.erase(s.length() - 1, 1);
    }

    // Print the resultant subsequence
    cout << s;
}

// Driver Code
int main()
{
    // Given string S
    string S = "geeksforgeeks";

    // Function Call
    firstSubsequence(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the lexicographically
// smallest subsequence of length N-1
static void firstSubsequence(String s)
{

    // Store index of character
    // to be deleted
    int isMax = -1;

    // Traverse the String
    for(int i = 0; i < s.length() - 1; i++)
    {

        // If ith character > (i + 1)th
        // character then store it
        if (s.charAt(i) > s.charAt(i + 1))
        {
            isMax = i;
            break;
        }
    }

    // If any character found in non
    // alphabetical order then remove it
    if (isMax >= 0)
    {
        s = s.substring(0, isMax) +
            s.substring(isMax + 1);
        // s.rerase(isMax, 1);
    }

    // Otherwise remove last character
    else
    {
        //s.erase(s.length() - 1, 1);
        s = s.substring(0, s.length() - 1);

    }

    // Print the resultant subsequence
    System.out.print(s);
}

// Driver Code
public static void main(String[] args)
{

    // Given String S
    String S = "geeksforgeeks";

    // Function Call
    firstSubsequence(S);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the lexicographically
# smallest subsequence of length N-1
def firstSubsequence(s):

    # Store index of character
    # to be deleted
    isMax = -1

    # Traverse the String
    for i in range(len(s)):

        # If ith character > (i + 1)th
        # character then store it
        if (s[i] > s[i + 1]):
            isMax = i
            break

    # If any character found in non
    # alphabetical order then remove it
    if (isMax >= 0):
        s = s[0 : isMax] + s[isMax + 1 : len(s)]

    # s.rerase(isMax, 1);

    # Otherwise remove last character
    else:

        # s.erase(s.length() - 1, 1);
        s = s[0: s.length() - 1]

    # Print the resultant subsequence
    print(s)

# Driver Code
if __name__ == '__main__':

    # Given String S
    S = "geeksforgeeks"

    # Function Call
    firstSubsequence(S)

# This code is contributed by Princi Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the lexicographically
// smallest subsequence of length N-1
static void firstSubsequence(String s)
{

    // Store index of character
    // to be deleted
    int isMax = -1;

    // Traverse the String
    for(int i = 0; i < s.Length - 1; i++)
    {

        // If ith character > (i + 1)th
        // character then store it
        if (s[i] > s[i + 1])
        {
            isMax = i;
            break;
        }
    }

    // If any character found in non
    // alphabetical order then remove it
    if (isMax >= 0)
    {
        s = s.Substring(0, isMax) +
            s.Substring(isMax + 1);
        // s.rerase(isMax, 1);
    }

    // Otherwise remove last character
    else
    {
        //s.erase(s.Length - 1, 1);
        s = s.Substring(0, s.Length - 1);

    }

    // Print the resultant subsequence
    Console.Write(s);
}

// Driver Code
public static void Main(String[] args)
{

    // Given String S
    String S = "geeksforgeeks";

    // Function Call
    firstSubsequence(S);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the lexicographically
// smallest subsequence of length N-1
function firstSubsequence(s)
{
    // Store index of character
    // to be deleted
    let isMax = -1;

    // Traverse the String
    for(let i = 0; i < s.length - 1; i++)
    {

        // If ith character > (i + 1)th
        // character then store it
        if (s[i] > s[i + 1])
        {
            isMax = i;
            break;
        }
    }

    // If any character found in non
    // alphabetical order then remove it
    if (isMax >= 0)
    {
        s = s.substring(0, isMax) +
            s.substring(isMax + 1);
        // s.rerase(isMax, 1);
    }

    // Otherwise remove last character
    else
    {
        //s.erase(s.length() - 1, 1);
        s = s.substring(0, s.length - 1);

    }

    // Print the resultant subsequence
    document.write(s);
}

// Driver Code
// Given String S
let S = "geeksforgeeks";

// Function Call
firstSubsequence(S);

// This code is contributed by unknown2108
</script>
```

**输出:**

```
eeksforgeeks
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
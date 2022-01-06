# 最大重叠串数

> 原文:[https://www . geesforgeks . org/最大重叠字符串数/](https://www.geeksforgeeks.org/maximum-number-of-overlapping-string/)

给定两个字符串 **S** 和 **T** ，任务是统计字符串 S 中重叠的字符串 T 的数量。
T5】注:如果有一些不匹配的单词作为子序列与字符串 T 不匹配，则打印-1。
**示例:**

> **输入:** S =“啾啾”，T =“啾啾”
> **输出:** 0
> **说明:**
> 没有“啾啾”的重叠串。
> **输入:**S =“chcirfirp”，T =“chirp”
> **输出:**2
> T 有两个重叠串:
> 第一个“chirp”可以是 **ch** c **irp** hirp。
> 第二个“唧唧”可以是 ch **c** irp **hirp** 。

**方法:**想法是迭代字符串 **S** 并在字符串 T 的第一个字符出现的瞬间增加重叠计数如果在任何瞬间当前字符等于最后一个字符，则减少重叠计数。同时，如果最大重叠计数大于 2，则更新最大重叠计数。最后，检查每个子序列是否与字符串匹配，检查重叠计数是否等于零。如果是，返回最大重叠计数。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// maximum number of occurrence of
// the overlapping count

#include <bits/stdc++.h>

using namespace std;

// Function to find the maximum
// overlapping strings
int maxOverlap(string S, string T)
{
    string str = T;
    int count[T.length()] = { 0 };
    int overlap = 0;
    int max_overlap = 0;

    for (int i = 0; i <= S.length(); i++) {

        // Get the current character
        int index = str.find(S[i]);

        // Condition to check if the current
        // character is the first character
        // of the string T then increment the
        // overlapping count
        if (index == 0) {
            overlap++;

            if (overlap >= 2)
                max_overlap = max(overlap, max_overlap);

            count[index]++;
        }
        else {
            // Condition to check
            // previous character is also
            // occurred
            if (count[index - 1] <= 0)
                return -1;

            // Update count of previous
            // and current character
            count[index]++;
            count[index - 1]--;
        }

        // Condition to check the current
        // character is the last character
        // of the string T
        if (index == 4)
            overlap--;
    }

    // Condition to check the every
    // subsequence is a valid string T
    if (overlap == 0)
        return max_overlap;
    else
        return -1;
}

// Driver Code
int main()
{
    string S = "chcirphirp";
    string T = "chirp";

    // Function Call
    cout << maxOverlap(S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum number of occurrence of
// the overlapping count
import java.util.*;

class GFG{

// Function to find the maximum
// overlapping Strings
static int maxOverlap(String S, String T)
{
    String str = T;
    int count[] = new int[T.length()];
    int overlap = 0;
    int max_overlap = 0;

    for(int i = 0; i < S.length(); i++)
    {

       // Get the current character
       int index = str.indexOf(S.charAt(i));

       // Condition to check if the current
       // character is the first character
       // of the String T then increment the
       // overlapping count
       if (index == 0)
       {
           overlap++;

           if (overlap >= 2)
               max_overlap = Math.max(overlap,
                                      max_overlap);
           count[index]++;
       }
       else
       {

           // Condition to check
           // previous character is also
           // occurred
           if (count[index - 1] <= 0)
               return -1;

           // Update count of previous
           // and current character
           count[index]++;
           count[index - 1]--;
       }

       // Condition to check the current
       // character is the last character
       // of the String T
       if (index == 4)
           overlap--;

    }

    // Condition to check the every
    // subsequence is a valid String T
    if (overlap == 0)
        return max_overlap;
    else
        return -1;
}

// Driver code
public static void main(String[] args)
{
    String S = "chcirphirp";
    String T = "chirp";

    // Function call
    System.out.print(maxOverlap(S, T));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum number of occurrence of
# the overlapping count

# Function to find the maximum
# overlapping strings
def maxOverlap(S, T):

    str = T
    count = [0 for i in range(len(T))]
    overlap = 0
    max_overlap = 0

    for i in range(0, len(S)):

        # Get the current character
        index = str.find(S[i])

        # Condition to check if
        # the current character is
        # the first character of the
        # string T then increment the
        # overlapping count
        if(index == 0):
            overlap += 1

            if(overlap >= 2):
                max_overlap = max(overlap,
                                  max_overlap)
            count[index] += 1

        else:

            # Condition to check 
            # previous character is also 
            # occurred
            if(count[index - 1] <= 0):
                return -1

            # Update count of previous 
            # and current character
            count[index] += 1
            count[index - 1] -= 1

        # Condition to check the current
        # character is the last character 
        # of the string T
        if(index == 4):
            overlap -= 1

    # Condition to check the every 
    # subsequence is a valid string T
    if(overlap == 0):
        return max_overlap
    else:
        return -1

# Driver Code
S = "chcirphirp"
T = "chirp"

# Function Call
print(maxOverlap(S, T))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to find the
// maximum number of occurrence of
// the overlapping count
using System;

class GFG{

// Function to find the maximum
// overlapping Strings
static int maxOverlap(String S, String T)
{
    String str = T;
    int []count = new int[T.Length];
    int overlap = 0;
    int max_overlap = 0;

    for(int i = 0; i < S.Length; i++)
    {

       // Get the current character
       int index = str.IndexOf(S[i]);

       // Condition to check if the current
       // character is the first character
       // of the String T then increment the
       // overlapping count
       if (index == 0)
       {
           overlap++;

           if (overlap >= 2)
           {
               max_overlap = Math.Max(overlap,
                                      max_overlap);
           }
           count[index]++;
       }
       else
       {

           // Condition to check
           // previous character is also
           // occurred
           if (count[index - 1] <= 0)
               return -1;

           // Update count of previous
           // and current character
           count[index]++;
           count[index - 1]--;
       }

       // Condition to check the current
       // character is the last character
       // of the String T
       if (index == 4)
           overlap--;
    }

    // Condition to check the every
    // subsequence is a valid String T
    if (overlap == 0)
        return max_overlap;
    else
        return -1;
}

// Driver code
public static void Main(String[] args)
{
    String S = "chcirphirp";
    String T = "chirp";

    // Function call
    Console.Write(maxOverlap(S, T));
}
}

// This code is contributed by sapnasingh4991
```

**Output:** 

```
2

```
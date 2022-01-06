# 要删除的最长子串的长度，使一个串等于另一个串

> 原文:[https://www . geeksforgeeks . org/要删除的最长子串长度使一个字符串等于另一个字符串/](https://www.geeksforgeeks.org/length-of-longest-substring-to-be-deleted-to-make-a-string-equal-to-another-string/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **str1** 和 **str2** ，其中 **str2** 是 **str1** 的子序列，任务是找出 **str1** 的最长[子串](https://www.geeksforgeeks.org/python-check-substring-present-given-string/)的长度，该长度在移除后使字符串 **str2** 和 **str1** 相等。

**示例:**

> **输入:**str1 =“programming blods”，str 2 =“ibloods”
> **输出:** 8
> **说明:**
> 要从 str 1 中删除的子字符串是[“program”、“ng”]。因此，删除的最长子串的长度是 8。
> 
> **输入:**str 1 =“GeeksforGeeks”，str 2 =“forks”
> T3】输出: 5

**天真方法:**最简单的方法是[生成 **str1** 的所有可能的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，对于每个子串，从 **str1** 中删除它，并检查结果串是否等于 **str2** 。打印此类最长子字符串的长度。

***时间复杂度:** O(2 <sup>N</sup> )
**辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是在 **str1** 中找到 **str2** 的出现。从左到右遍历两个字符串，检查两个字符是否相等。如果发现是真的，请在两个字符串中向右移动。否则，仅在 **str2** 中向右前进。同样，要在 **str1** 中找到最后一次出现的 **str2** ，请从右向左遍历两个字符串，并以同样的方式继续。按照以下步骤解决问题:

1.  初始化一个变量， **res=0** 来存储最长删除子串的长度。
2.  创建一个数组，**pos【】**存储 **str2** 在 **str1 中第一次出现的位置。**
3.  从左到右遍历两个字符串，通过删除 str1 的一些字符来存储 str2 第一次出现的位置。
4.  初始化一个变量， **lastPos = length(str1)-1** 通过删除 **str1** 的部分字符来存储当前字符在最后一次出现的 **str2** 中的位置。
5.  从右向左遍历两个字符串，检查两个字符是否匹配，然后在**pos【】**中找到 **str2** 当前字符的位置，否则继续。
6.  如果**RES**T42(**last pos**–**pos[I-1]-1)**则更新**RES = last pos–pos[I-1]-1。**
7.  最后，返回 **res** 。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the length
// of longest substring to be deleted
int longDelSub(string str1, string str2)
{
    // Stores the length of string
    int N = str1.size();
    int M = str2.size();

    // Store the position of
    // previous matched
    // character of str1
    int prev_pos = 0;

    // Store the position of first
    // occurrence of str2 in str1
    int pos[M];

    // Find the position of the
    // first occurrence of str2
    for (int i = 0; i < M; i++) {

        // Store the index of str1
        int index = prev_pos;

        // If both characters not matched
        while (index < N
               && str1[index] != str2[i]) {
            index++;
        }

        pos[i] = index;
        prev_pos = index + 1;
    }

    // Store the length of the
    // longest deleted substring
    int res = N - prev_pos;

    prev_pos = N - 1;

    // Store the position of last
    // occurrence of str2 in str1
    for (int i = M - 1; i >= 0; i--) {
        int index = prev_pos;

        // If both characters not matched
        while (index >= 0
               && str1[index] != str2[i]) {
            index--;
        }

        // Update res
        if (i != 0) {
            res = max(
                res,
                index - pos[i - 1] - 1);
        }

        prev_pos = index - 1;
    }

    // Update res.
    res = max(res, prev_pos + 1);

    return res;
}

// Driver Code
int main()
{
    // Given string
    string str1 = "GeeksforGeeks";
    string str2 = "forks";

    // Function Call
    cout << longDelSub(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement 
// the above approach 
import java.io.*;

class GFG{

// Function to print the length
// of longest substring to be deleted
static int longDelSub(String str1, String str2)
{

    // Stores the length of string
    int N = str1.length();
    int M = str2.length();

    // Store the position of
    // previous matched
    // character of str1
    int prev_pos = 0;

    // Store the position of first
    // occurrence of str2 in str1
    int pos[] = new int[M];

    // Find the position of the
    // first occurrence of str2
    for(int i = 0; i < M; i++)
    {

        // Store the index of str1
        int index = prev_pos;

        // If both characters not matched
        while (index < N && 
               str1.charAt(index) != 
               str2.charAt(i))
        {
            index++;
        }

        pos[i] = index;
        prev_pos = index + 1;
    }

    // Store the length of the
    // longest deleted substring
    int res = N - prev_pos;

    prev_pos = N - 1;

    // Store the position of last
    // occurrence of str2 in str1
    for(int i = M - 1; i >= 0; i--)
    {
        int index = prev_pos;

        // If both characters not matched
        while (index >= 0 && 
               str1.charAt(index) != 
               str2.charAt(i)) 
        {
            index--;
        }

        // Update res
        if (i != 0)
        {
            res = Math.max(res, 
                           index - 
                           pos[i - 1] - 1);
        }
        prev_pos = index - 1;
    }

    // Update res.
    res = Math.max(res, prev_pos + 1);

    return res;
}

// Driver Code
public static void main (String[] args)
{

    // Given string
    String str1 = "GeeksforGeeks";
    String str2 = "forks";

    // Function call
    System.out.print(longDelSub(str1, str2));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach 

# Function to print the length
# of longest substring to be deleted
def longDelSub(str1, str2):

    # Stores the length of string
    N = len(str1)
    M = len(str2)

    # Store the position of
    # previous matched
    # character of str1
    prev_pos = 0

    # Store the position of first
    # occurrence of str2 in str1
    pos = [0] * M

    # Find the position of the
    # first occurrence of str2
    for i in range(M):

        # Store the index of str1
        index = prev_pos

        # If both characters not matched
        while (index < N and 
          str1[index] != str2[i]):
            index += 1

        pos[i] = index
        prev_pos = index + 1

    # Store the length of the
    # longest deleted substring
    res = N - prev_pos

    prev_pos = N - 1

    # Store the position of last
    # occurrence of str2 in str1
    for i in range(M - 1, -1, -1):
        index = prev_pos

        # If both characters not matched
        while (index >= 0 and 
          str1[index] != str2[i]):
            index -= 1

        # Update res
        if (i != 0) :
            res = max(res, 
                      index - 
                      pos[i - 1] - 1)

        prev_pos = index - 1

    # Update res.
    res = max(res, prev_pos + 1)

    return res

# Driver Code

# Given string
str1 = "GeeksforGeeks"
str2 = "forks"

# Function call
print(longDelSub(str1, str2))

# This code is contributed by code_hunt
```

## C#

```
// C# program to implement 
// the above approach 
using System;

class GFG{

// Function to print the length
// of longest substring to be deleted
static int longDelSub(string str1,
                      string str2)
{

    // Stores the length of string
    int N = str1.Length;
    int M = str2.Length;

    // Store the position of
    // previous matched
    // character of str1
    int prev_pos = 0;

    // Store the position of first
    // occurrence of str2 in str1
    int[] pos = new int[M];

    // Find the position of the
    // first occurrence of str2
    for(int i = 0; i < M; i++) 
    {

        // Store the index of str1
        int index = prev_pos;

        // If both characters not matched
        while (index < N && 
          str1[index] != str2[i])
        {
            index++;
        }

        pos[i] = index;
        prev_pos = index + 1;
    }

    // Store the length of the
    // longest deleted substring
    int res = N - prev_pos;

    prev_pos = N - 1;

    // Store the position of last
    // occurrence of str2 in str1
    for(int i = M - 1; i >= 0; i--)
    {
        int index = prev_pos;

        // If both characters not matched
        while (index >= 0 && 
          str1[index] != str2[i])
        {
            index--;
        }

        // Update res
        if (i != 0)
        {
            res = Math.Max(res, 
                           index - 
                           pos[i - 1] - 1);
        }
        prev_pos = index - 1;
    }

    // Update res.
    res = Math.Max(res, prev_pos + 1);

    return res;
}

// Driver code
public static void Main()
{

    // Given string
    string str1 = "GeeksforGeeks";
    string str2 = "forks";

    // Function call
    Console.Write(longDelSub(str1, str2));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to print the length
// of longest substring to be deleted
function longDelSub( str1, str2)
{

    // Stores the length of string
    var N = str1.length;
    var M = str2.length;

    // Store the position of
    // previous matched
    // character of str1
    var prev_pos = 0;

    // Store the position of first
    // occurrence of str2 in str1
    var pos = new Array(M);

    // Find the position of the
    // first occurrence of str2
    for (let i = 0; i < M; i++) {

        // Store the index of str1
        var index = prev_pos;

        // If both characters not matched
        while (index < N
            && str1[index] != str2[i]) {
            index++;
        }

        pos[i] = index;
        prev_pos = index + 1;
    }

    // Store the length of the
    // longest deleted substring
    var res = N - prev_pos;

    prev_pos = N - 1;

    // Store the position of last
    // occurrence of str2 in str1
    for (let i = M - 1; i >= 0; i--) {
        var index = prev_pos;

        // If both characters not matched
        while (index >= 0
            && str1[index] != str2[i]) {
            index--;
        }

        // Update res
        if (i != 0) {
            res = Math.max(
                res,
                index - pos[i - 1] - 1);
        }

        prev_pos = index - 1;
    }

    // Update res.
    res = Math.max(res, prev_pos + 1);

    return res;
}

// Driver Code

    // Given string
    var str1 = "GeeksforGeeks";
    var str2 = "forks";

    // Function Call
    console.log(longDelSub(str1, str2));

// This code is contributed by ukasp.

</script>
```

**Output:**

```
5

```

***时间复杂度:** O(N + M)
**辅助空间:** O(M)*
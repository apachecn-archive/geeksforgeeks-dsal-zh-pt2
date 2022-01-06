# 最小化二进制字符串中的删除，删除“0101”

形式的所有子序列

> 原文:[https://www . geeksforgeeks . org/minimum-二进制字符串中的删除-删除-表单的所有子序列-0101/](https://www.geeksforgeeks.org/minimize-deletions-in-a-binary-string-to-remove-all-subsequences-of-the-form-0101/)

给定长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到需要从字符串中删除的最小字符数，使得字符串中不存在形式为**“0101”**的子序列。

**示例:**

> **输入:**S =“0101101”
> T3】输出: 2
> **解释:**去掉 S[1]和 S[5]将字符串修改为 00111。因此，无法从给定的字符串中获得 0101 类型的子序列。
> 
> **输入:**S = " 0110100110 "
> T3】输出: 2

**方法:**按照以下步骤解决问题:

*   所需的有效字符串最多可以由三个相同元素的块组成，即字符串可以是以下模式之一**“00…0”、“11…1”、“00…01…1”、“1…10”..0", "00..01…10..0”、“1…10…01…1”**。
*   使用部分和计算一个块的 **0** s 和 **1** s 的频率。
*   确定 **0** s 和 **1** s 的块的开始和结束索引，并确定计算出的**部分和**需要删除的最小字符数。
*   因此，请检查通过移除给定类型的子序列可以获得的最长字符串的长度。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum characters
// to be removed such that no subsequence
// of the form "0101" exists in the string
int findmin(string s)
{
    int n = s.length();
    int i, j, maximum = 0;

    // Stores the partial sums
    int incr[n + 1] = { 0 };

    for (i = 0; i < n; i++) {

        // Calculate partial sums
        incr[i + 1] = incr[i];

        if (s[i] == '0') {
            incr[i + 1]++;
        }
    }

    for (i = 0; i < n; i++) {
        for (j = i + 1; j < n; j++) {

            // Setting endpoints and
            // deleting characters indices.
            maximum
                = max(maximum, incr[i] + j - i + 1
                                   - (incr[j + 1] - incr[i])
                                   + incr[n] - incr[j + 1]);
        }
    }

    // Return count of deleted characters
    return n - maximum;
}
// Driver Code
int main()
{
    string S = "0110100110";
    int minimum = findmin(S);
    cout << minimum << '\n';
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
class GFG{

// Function to find minimum
// characters to be removed
// such that no subsequence
// of the form "0101" exists
// in the string
static int findmin(String s)
{
  int n = s.length();
  int i, j, maximum = 0;

  // Stores the partial sums
  int[] incr = new int[n + 1];

  for (i = 0; i < n; i++)
  {
    // Calculate partial sums
    incr[i + 1] = incr[i];

    if (s.charAt(i) == '0')
    {
      incr[i + 1]++;
    }
  }

  for (i = 0; i < n; i++)
  {
    for (j = i + 1; j < n; j++)
    {
      // Setting endpoints and
      // deleting characters indices.
      maximum = Math.max(maximum, incr[i] +
                         j - i + 1 -
                        (incr[j + 1] - incr[i]) +
                         incr[n] - incr[j + 1]);
    }
  }

  // Return count of
  // deleted characters
  return n - maximum;
}

// Driver Code
public static void main(String[] args)
{
  String S = "0110100110";
  int minimum = findmin(S);
  System.out.println(minimum);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find minimum
# characters to be removed
# such that no subsequence
# of the form "0101" exists
# in the string
def findmin(s):

    n = len(s)
    maximum = 0

    # Stores the partial sums
    incr = [0] * (n + 1)

    for i in range(0, n):

        # Calculate partial sums
        incr[i + 1] = incr[i]

        if (s[i] == '0'):
            incr[i + 1] = incr[i + 1] + 1

    for i in range(0, n + 1):
        for j in range(i + 1, n):

            # Setting endpoints and
            # deleting characters indices.
            maximum = max(maximum, incr[i] +
                          j - i + 1 -
                         (incr[j + 1] - incr[i]) +
                          incr[n] - incr[j + 1])

    # Return count of
    # deleted characters
    return n - maximum

# Driver Code
if __name__ == "__main__":

    S = "0110100110"
    minimum = findmin(S)
    print(minimum)

# This code is contributed by akhilsaini
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to find minimum
// characters to be removed
// such that no subsequence
// of the form "0101" exists
// in the string
static int findmin(string s)
{
  int n = s.Length;
  int i, j, maximum = 0;

  // Stores the partial sums
  int[] incr = new int[n + 1];

  for (i = 0; i < n; i++)
  {
    // Calculate partial sums
    incr[i + 1] = incr[i];

    if (s[i] == '0')
    {
      incr[i + 1]++;
    }
  }

  for (i = 0; i < n; i++)
  {
    for (j = i + 1; j < n; j++)
    {
      // Setting endpoints and
      // deleting characters indices.
      maximum = Math.Max(maximum, incr[i] +
                         j - i + 1 -
                        (incr[j + 1] - incr[i]) +
                         incr[n] - incr[j + 1]);
    }
  }

  // Return count of
  // deleted characters
  return n - maximum;
}

// Driver Code
public static void Main()
{
  string S = "0110100110";
  int minimum = findmin(S);
  Console.WriteLine(minimum);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to find minimum characters
// to be removed such that no subsequence
// of the form "0101" exists in the string
function findmin(s)
{
    let n = s.length;
    let i, j, maximum = 0;

    // Stores the partial sums

     var incr = new Array(n+1);
      incr.fill(0);
    for (i = 0; i < n; i++) {

        // Calculate partial sums
        incr[i + 1] = incr[i];

        if (s[i] == '0') {
            incr[i + 1]++;
        }
    }

    for (i = 0; i < n; i++) {
        for (j = i + 1; j < n; j++) {

            // Setting endpoints and
            // deleting characters indices.
            maximum
                = Math.max(maximum, incr[i] + j - i + 1
                                - (incr[j + 1] - incr[i])
                                + incr[n] - incr[j + 1]);
        }
    }

    // Return count of deleted characters
    return n - maximum;
}
// Driver Code

    let S = "0110100110";
    let minimum = findmin(S);
    document.write(minimum + '\n');

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
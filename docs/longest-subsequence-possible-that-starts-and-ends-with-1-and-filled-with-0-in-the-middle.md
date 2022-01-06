# 可能的最长子序列，以 1 开始和结束，中间用 0 填充

> 原文:[https://www . geesforgeks . org/最长可能子序列以 1 开头和结尾，中间填充 0/](https://www.geeksforgeeks.org/longest-subsequence-possible-that-starts-and-ends-with-1-and-filled-with-0-in-the-middle/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s** ，任务是找到最长的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)的长度，该子序列可以分为三个子串，使得第一和第三个子串或者为空或者填充为 1，中间的子串或者为空或者填充为 0。

**示例:**

> **输入:** s = "1001"
> **输出:** 4
> **解释:**
> 整个字符串可以分为想要的三个部分:“1”、“00”、“1”。
> 
> **输入:** s = "010"
> **输出:** 2
> **解释:**
> 子序列“00”、“01”和“10”可以拆分为三个所需的部分{“”、“00”、“}、{“”、“0”、“1”}和{“1”、“0”、“}

**方法:**
要解决问题，我们需要遵循下面给出的步骤:

*   首先，在**前缀数组**中预先计算并存储**【1】**和**【0】**的出现次数。
*   初始化两个整数 **i** 和 **j** ，其中 **i** 将是第一个和第二个字符串之间的划分点，j 将是第二个和第三个字符串之间的划分点。
*   迭代**I**&**j**(0<= I<j<= n)的所有可能值，找到满足给定条件的可能子序列的最大可能长度。

下面是上述方法的实现:

## C++

```
// C++ Program to find the
// longest subsequence possible
// that starts and ends with 1
// and filled with 0 in the middle

#include <bits/stdc++.h>
using namespace std;

int longestSubseq(string s, int length)
{
    // Prefix array to store the
    // occurences of '1' and '0'
    int ones[length + 1], zeroes[length + 1];

    // Initialise prefix arrays with 0
    memset(ones, 0, sizeof(ones));
    memset(zeroes, 0, sizeof(zeroes));

    // Iterate over the length of the string
    for (int i = 0; i < length; i++) {

        // If current character is '1'
        if (s[i] == '1') {
            ones[i + 1] = ones[i] + 1;
            zeroes[i + 1] = zeroes[i];
        }

        // If current character is '0'
        else {
            zeroes[i + 1] = zeroes[i] + 1;
            ones[i + 1] = ones[i];
        }
    }

    int answer = INT_MIN;
    int x = 0;

    for (int i = 0; i <= length; i++) {
        for (int j = i; j <= length; j++) {
            // Add '1' available for
            // the first string
            x += ones[i];

            // Add '0' available for
            // the second string
            x += (zeroes[j] - zeroes[i]);

            // Add '1' available for
            // the third string
            x += (ones[length] - ones[j]);

            // Update answer
            answer = max(answer, x);

            x = 0;
        }
    }

    // Print the final result
    cout << answer << endl;
}

// Driver Code
int main()
{

    string s = "10010010111100101";

    int length = s.length();

    longestSubseq(s, length);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// longest subsequence possible
// that starts and ends with 1
// and filled with 0 in the middle
import java.io.*;

class GFG{

static void longestSubseq(String s,
                          int length)
{

    // Prefix array to store the
    // occurences of '1' and '0'
    int[] ones = new int[length + 1];
    int[] zeroes = new int[length + 1];

    // Iterate over the length of
    // the string
    for(int i = 0; i < length; i++)
    {

        // If current character is '1'
        if (s.charAt(i) == '1')
        {
            ones[i + 1] = ones[i] + 1;
            zeroes[i + 1] = zeroes[i];
        }

        // If current character is '0'
        else
        {
            zeroes[i + 1] = zeroes[i] + 1;
            ones[i + 1] = ones[i];
        }
    }

    int answer = Integer.MIN_VALUE;
    int x = 0;

    for(int i = 0; i <= length; i++)
    {
        for(int j = i; j <= length; j++)
        {

            // Add '1' available for
            // the first string
            x += ones[i];

            // Add '0' available for
            // the second string
            x += (zeroes[j] - zeroes[i]);

            // Add '1' available for
            // the third string
            x += (ones[length] - ones[j]);

            // Update answer
            answer = Math.max(answer, x);
            x = 0;
        }
    }

    // Print the final result
    System.out.println(answer);
}

// Driver code
public static void main(String[] args)
{
    String s = "10010010111100101";
    int length = s.length();

    longestSubseq(s, length);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the
# longest subsequence possible
# that starts and ends with 1
# and filled with 0 in the middle
import sys

def longestSubseq(s, length):

    # Prefix array to store the
    # occurences of '1' and '0'
    # Initialise prefix arrays with 0
    ones = [0 for i in range(length + 1)]
    zeroes = [0 for i in range(length + 1)]

    # Iterate over the length of the string
    for i in range(length):

        # If current character is '1'
        if(s[i] == '1'):
            ones[i + 1] = ones[i] + 1
            zeroes[i + 1] = zeroes[i]

        # If current character is '0'
        else:
            zeroes[i + 1] = zeroes[i] + 1
            ones[i + 1] = ones[i]

    answer = -sys.maxsize - 1
    x = 0

    for i in range(length + 1):
        for j in range(i, length + 1):

            # Add '1' available for
            # the first string
            x += ones[i]

            # Add '0' available for
            # the second string
            x += (zeroes[j] - zeroes[i])

            # Add '1' available for
            # the third string
            x += (ones[length] - ones[j])

            # Update answer
            answer = max(answer, x)
            x = 0

    # Print the final result
    print(answer)

# Driver Code
S = "10010010111100101"
length = len(S)

longestSubseq(S, length)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find the
// longest subsequence possible
// that starts and ends with 1
// and filled with 0 in the middle
using System;

class GFG{

static void longestSubseq(String s,
                          int length)
{

    // Prefix array to store the
    // occurences of '1' and '0'
    int[] ones = new int[length + 1];
    int[] zeroes = new int[length + 1];

    // Iterate over the length of
    // the string
    for(int i = 0; i < length; i++)
    {

        // If current character is '1'
        if (s[i] == '1')
        {
            ones[i + 1] = ones[i] + 1;
            zeroes[i + 1] = zeroes[i];
        }

        // If current character is '0'
        else
        {
            zeroes[i + 1] = zeroes[i] + 1;
            ones[i + 1] = ones[i];
        }
    }

    int answer = int.MinValue;
    int x = 0;

    for(int i = 0; i <= length; i++)
    {
        for(int j = i; j <= length; j++)
        {

            // Add '1' available for
            // the first string
            x += ones[i];

            // Add '0' available for
            // the second string
            x += (zeroes[j] - zeroes[i]);

            // Add '1' available for
            // the third string
            x += (ones[length] - ones[j]);

            // Update answer
            answer = Math.Max(answer, x);
            x = 0;
        }
    }

    // Print the readonly result
    Console.WriteLine(answer);
}

// Driver code
public static void Main(String[] args)
{
    String s = "10010010111100101";
    int length = s.Length;

    longestSubseq(s, length);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // JavaScript program to find the
      // longest subsequence possible
      // that starts and ends with 1
      // and filled with 0 in the middle
      function longestSubseq(s, len) {
        // Prefix array to store the
        // occurences of '1' and '0'
        var ones = new Array(len + 1).fill(0);
        var zeroes = new Array(len + 1).fill(0);

        // Iterate over the length of
        // the string
        for (var i = 0; i < len; i++) {
          // If current character is '1'
          if (s[i] === "1") {
            ones[i + 1] = ones[i] + 1;
            zeroes[i + 1] = zeroes[i];
          }

          // If current character is '0'
          else {
            zeroes[i + 1] = zeroes[i] + 1;
            ones[i + 1] = ones[i];
          }
        }

        var answer = -2147483648;
        var x = 0;

        for (var i = 0; i <= len; i++) {
          for (var j = i; j <= len; j++) {
            // Add '1' available for
            // the first string
            x += ones[i];

            // Add '0' available for
            // the second string
            x += zeroes[j] - zeroes[i];

            // Add '1' available for
            // the third string
            x += ones[len] - ones[j];

            // Update answer
            answer = Math.max(answer, x);
            x = 0;
          }
        }

        // Print the readonly result
        document.write(answer);
      }

      // Driver code
      var s = "10010010111100101";
      var len = s.length;

      longestSubseq(s, len);
</script>
```

**Output:** 

```
12
```

**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(N)*
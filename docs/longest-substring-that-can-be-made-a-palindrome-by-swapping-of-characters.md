# 通过字符交换可以成为回文的最长子串

> 原文:[https://www . geesforgeks . org/最长子串-可以通过字符交换来生成回文/](https://www.geeksforgeeks.org/longest-substring-that-can-be-made-a-palindrome-by-swapping-of-characters/)

给定一个[数字串](https://www.geeksforgeeks.org/python-string-isnumeric-application/) **S** ，任务是找到最长的可以成为[回文](https://www.geeksforgeeks.org/tag/palindrome/)的非空子串。

**示例:**

> **输入:** S = "3242415"
> **输出:** 5
> **说明:**“24241”是能转换成回文串“24142”的最长这样的子串。
> 
> **输入:** S = "213123"
> **输出:** 6
> **解释:**“213123”这样的子串可以转换成回文串“231132”。

**天真方法:**解决这个问题最简单的方法是[生成所有可能的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，对于每个子串，通过统计每个子串中的字符来检查它是否可以成为回文，并检查是否只有一个或没有奇数频繁字符存在。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，解决此问题的思路是使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)和[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。如果每个被包含的数(可能除了一个)的计数是偶数，就可以形成回文。按照以下步骤解决问题:

*   初始化一个整型变量，比如**屏蔽**。在我们的**掩码中，如果对应数字的计数为**偶数**，则为 0** ，如果为**奇数**，则为 1。
*   [遍历字符串](https://www.geeksforgeeks.org/how-to-iterate-through-a-string-word-by-word-in-c/)并在遍历字符串时，跟踪变量**掩码**中的**奇数/偶数计数**。
*   如果再次遇到相同的**掩码**，则具有相同掩码的**第一位置**(不含)和**当前位置**(含)之间的子阵列具有偶数计数。
*   让子串的大小存储在一个变量中，比如 **res** 。
*   初始化一个数组，比如说 **dp[]** ，以跟踪每个大小为 1024 的掩码的最小(第一个)位置，因为输入只包含 10 个数字(“0123456789”)，并且只能有 2^10 或 1024 个不同的位掩码。
*   子串的[大小可以通过从当前位置减去来计算。注意**零掩码**的位置是 **-1，**作为第一个要包含的字符。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)
*   此外，通过**位**检查所有与当前掩码不同的掩码。换句话说，如果**两个掩码相差**一位，这意味着子串中有一个**奇数**。
*   打印 **res** 作为最长的这样的子串的长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Longest
// substring that can be made a
// palindrome by swapping of characters
int longestSubstring(string s)
{

    // Initialize dp array of size 1024
    int dp[1024];

    // Initializeing dp array with length of s
    fill(dp, dp + 1024, s.size());

    // Initializing mask and res
    int res = 0, mask = 0;
    dp[0] = -1;

    // Traverse the string
    for (int i = 0; i < s.size(); ++i)
    {

        // Find the mask of the current character
        mask ^= 1 << (s[i] - 48);

        // Finding the length of the longest
        // substring in s which is a
        // palindrome for even count
        res = max(res, i - dp[mask]);

        // Finding the length of the longest
        // substring in s which is a
        // palindrome for one odd count
        for (int j = 0; j <= 9; ++j)

            // Finding maximum length of
            // substring having one odd count
            res = max(res, i - dp[mask ^ (1 << j)]);

        // dp[mask] is minimum of
        // current i and dp[mask]
        dp[mask] = min(dp[mask], i);
    }

    // Return longest length of the substring
    // which forms a palindrome with swaps
    return res;
}

// Driver Code
int main()
{

    // Input String
    string s = "3242415";

    // Function Call
    cout << longestSubstring(s);
    return 0;
}

// This code is contributed by subhammahato348.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the Longest
    // substring that can be made a
    // palindrome by swapping of characters
    public static int longestSubstring(String s)
    {
        // Initialize dp array of size 1024
        int dp[] = new int[1024];

        // Initializeing dp array with length of s
        Arrays.fill(dp, s.length());

        // Initializing mask and res
        int res = 0, mask = 0;
        dp[0] = -1;

        // Traverse the string
        for (int i = 0; i < s.length(); ++i) {

            // Find the mask of the current character
            mask ^= 1 << (s.charAt(i) - '0');

            // Finding the length of the longest
            // substring in s which is a
            // palindrome for even count
            res = Math.max(res, i - dp[mask]);

            // Finding the length of the longest
            // substring in s which is a
            // palindrome for one odd count
            for (int j = 0; j <= 9; ++j)

                // Finding maximum length of
                // substring having one odd count
                res = Math.max(res,
                               i - dp[mask ^ (1 << j)]);

            // dp[mask] is minimum of
            // current i and dp[mask]
            dp[mask] = Math.min(dp[mask], i);
        }

        // Return longest length of the substring
        // which forms a palindrome with swaps
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input String
        String s = "3242415";

        // Function Call
        System.out.println(longestSubstring(s));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the Longest
# substring that can be made a
# palindrome by swapping of characters
def longestSubstring(s):

    # Initialize dp array of size 1024
    dp = [1024 for i in range(1024)]

    # Initializeing dp array with length of s
    # Arrays.fill(dp, s.length());

    # Initializing mask and res
    res, mask = 0, 0
    dp[0] = -1

    # Traverse the string
    for i in range(len(s)):

        # Find the mask of the current character
        mask ^= 1 << (ord(s[i]) - ord('0'))

        # Finding the length of the longest
        # substring in s which is a
        # palindrome for even count
        res = max(res, i - dp[mask])

        # Finding the length of the longest
        # substring in s which is a
        # palindrome for one odd count
        for j in range(10):

            # Finding maximum length of
            # substring having one odd count
            res = max(res, i - dp[mask ^ (1 << j)])

        # dp[mask] is minimum of
        # current i and dp[mask]
        dp[mask] = min(dp[mask], i)

    # Return longest length of the substring
    # which forms a palindrome with swaps
    return res

# Driver Code
if __name__ == '__main__':

    # Input String
    s = "3242415"

    # Function Call
    print(longestSubstring(s))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the Longest
  // substring that can be made a
  // palindrome by swapping of characters
  public static int longestSubstring(string s)
  {
    // Initialize dp array of size 1024
    int []dp = new int[1024];

    // Initializeing dp array with length of s
    for (int i = 0; i < 1024; ++i)
    {
      dp[i] = s.Length;
    }

    // Initializing mask and res
    int res = 0, mask = 0;
    dp[0] = -1;

    // Traverse the string
    for (int i = 0; i < s.Length; i++)
    {

      // Find the mask of the current character
      mask = mask ^ (1 << (s[i] - '0'));

      // Finding the length of the longest
      // substring in s which is a
      // palindrome for even count
      res = Math.Max(res, i - dp[mask]);

      // Finding the length of the longest
      // substring in s which is a
      // palindrome for one odd count
      for (int j = 0; j < 10; j++)
      {

        // Finding maximum length of
        // substring having one odd count
        res = Math.Max(res,i - dp[mask ^ (1 << j)]);
      }

      // dp[mask] is minimum of
      // current i and dp[mask]
      dp[mask] = Math.Min(dp[mask], i);
    }

    // Return longest length of the substring
    // which forms a palindrome with swaps
    return res;
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Input String
    string s = "3242415";

    // Function Call
    Console.WriteLine(longestSubstring(s));
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the Longest
// substring that can be made a
// palindrome by swapping of characters
function longestSubstring(s)
{

    // Initialize dp array of size 1024
    let dp = new Array(1024).fill(1);

    // Initializing mask and res
    let res = 0, mask = 0;
    dp[0] = -1;

    // Traverse the string
    for(let i = 0; i < s.length; ++i)
    {

        // Find the mask of the current character
        mask ^= 1 << (s[i] - '0');

        // Finding the length of the longest
        // substring in s which is a
        // palindrome for even count
        res = Math.max(res, i - dp[mask]);

        // Finding the length of the longest
        // substring in s which is a
        // palindrome for one odd count
        for(let j = 0; j <= 9; ++j)

            // Finding maximum length of
            // substring having one odd count
            res = Math.max(res,
                           i - dp[mask ^ (1 << j)]);

        // dp[mask] is minimum of
        // current i and dp[mask]
        dp[mask] = Math.min(dp[mask], i);
    }

    // Return longest length of the substring
    // which forms a palindrome with swaps
    return res;
}

// Driver Code

// Input String
let s = "3242415";

// Function Call
document.write(longestSubstring(s));

// This code is contributed by splevel62

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(10*N)*
***辅助空间:** O(1024)*
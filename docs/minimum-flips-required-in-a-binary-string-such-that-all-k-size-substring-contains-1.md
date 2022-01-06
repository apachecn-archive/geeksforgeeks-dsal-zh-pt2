# 二进制字符串中所需的最小翻转，使得所有 K 大小的子字符串包含 1

> 原文:[https://www . geesforgeks . org/minimum-flips-required-in-a-binary-string-so-all-k-size-substring-contains-1/](https://www.geeksforgeeks.org/minimum-flips-required-in-a-binary-string-such-that-all-k-size-substring-contains-1/)

给定一个大小为 **N** 的二进制字符串**和一个正整数 **K** ，任务是找到使所有大小为 **K** 的子字符串至少包含一个“1”所需的最小翻转次数。
**举例:**** 

> **输入:** str = "0001 "，K = 2
> **输出:** 1
> **解释:**
> 翻转索引 1 处的位将 str 修改为“0101”。
> 所有大小为 2 的子字符串都是“01”、“10”和“01”。
> 每个子串至少包含一个 1。
> **输入:** str = "101 "，K = 2
> **输出:** 0
> **解释:**
> 所有大小为 2 的子串都是“10”和“01”。
> 因为它们都至少有一个“1”，所以不需要在原来的弦上翻转。

**进场:**
按照以下步骤解决问题:

1.  其思想是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)检查长度为 K 的每个子串是否包含任何‘1’。
2.  维护一个变量 **last_idx** 来存储字符为“1”的窗口的**最后索引**。如果当前窗口中没有**或【1】**，则该变量的值为 **-1** 。
3.  对于任何这样的窗口，我们将通过将当前窗口最后一个索引处的字符翻转到**‘1’**来增加翻转次数，并将索引 **last_idx** 更新到该索引。
4.  翻转当前窗口的最后一个字符可以确保后面的 **K-1** 窗口也至少有一个“1”。因此，这种方法最大限度地减少了所需的翻转次数。
5.  对字符串的其余部分重复此过程，并打印所需翻转的最终计数。

以下是上述方法的实现:

## C++

```
// C++ program to find the
// minimum numbers of flips
// required in a binary string
// such that all substrings of
// size K has atleast one 1

#include <bits/stdc++.h>
using namespace std;

// Function to calculate and
// return the minimum number
// of flips to make string valid
int minimumMoves(string S, int K)
{
    int N = S.length();

    // Stores the count
    // of required flips
    int ops = 0;

    // Stores the last index
    // of '1' in the string
    int last_idx = -1;

    // Check for the first
    // substring of length K
    for (int i = 0; i < K; i++) {

        // If i-th character
        // is '1'
        if (S[i] == '1')
            last_idx = i;
    }

    // If the substring had
    // no '1'
    if (last_idx == -1) {

        // Increase the
        // count of required
        // flips
        ++ops;

        // Flip the last
        // index of the
        // window
        S[K - 1] = '1';

        // Update the last
        // index which
        // contains 1
        last_idx = K - 1;
    }

    // Check for remaining substrings
    for (int i = 1; i < N - K + 1; i++) {

        // If last_idx does not
        // belong to current
        // window make it -1
        if (last_idx < i)
            last_idx = -1;

        // If the last character of
        // the current substring
        // is '1', then update
        // last_idx to i+k-1;
        if (S[i + K - 1] == '1')
            last_idx = i + K - 1;

        // If last_idx == -1, then
        // the current substring
        // has no 1
        if (last_idx == -1) {

            // Increase the count
            // of flips
            ++ops;

            // Update the last
            // index of the
            // current window
            S[i + K - 1] = '1';

            // Store the last
            // index of current
            // window as the
            // index of last '1'
            // in the string
            last_idx = i + K - 1;
        }
    }
    // Return the number
    // of operations
    return ops;
}

// Driver Code
int main()
{
    string S = "001010000";
    int K = 3;
    cout << minimumMoves(S, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum numbers of flips
// required in a binary string
// such that all substrings of
// size K has atleast one 1
class GFG{

// Function to calculate and
// return the minimum number
// of flips to make string valid
public static int minimumMoves(String s, int K)
{
    StringBuilder S = new StringBuilder(s);
    int N = S.length();

    // Stores the count
    // of required flips
    int ops = 0;

    // Stores the last index
    // of '1' in the string
    int last_idx = -1;

    // Check for the first
    // substring of length K
    for(int i = 0; i < K; i++)
    {

    // If i-th character
    // is '1'
    if (S.charAt(i) == '1')
        last_idx = i;
    }

    // If the substring had
    // no '1'
    if (last_idx == -1)
    {

        // Increase the count
        // of required flips
        ++ops;

        // Flip the last index
        // of the window
        S.setCharAt(K - 1, '1');

        // Update the last index
        // which contains 1
        last_idx = K - 1;
    }

    // Check for remaining substrings
    for(int i = 1; i < N - K + 1; i++)
    {

    // If last_idx does not
    // belong to current
    // window make it -1
    if (last_idx < i)
        last_idx = -1;

    // If the last character of
    // the current substring
    // is '1', then update
    // last_idx to i+k-1;
    if (S.charAt(i + K - 1) == '1')
        last_idx = i + K - 1;

    // If last_idx == -1, then
    // the current substring
    // has no 1
    if (last_idx == -1)
    {

        // Increase the count
        // of flips
        ++ops;

        // Update the last index
        // of the current window
        S.setCharAt(i + K - 1, '1');

        // Store the last index
        // of current window as
        // the index of last '1'
        // in the string
        last_idx = i + K - 1;
    }
    }

    // Return the number
    // of operations
    return ops;
}

// Driver Code
public static void main(String[] args)
{
    String S = "001010000";
    int K = 3;

    System.out.println(minimumMoves(S, K));
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# numbers of flips required in a binary
# string such that all substrings of
# size K has atleast one 1

# Function to calculate and
# return the minimum number
# of flips to make string valid
def minimumMoves(S, K):

    N = len(S)

    # Stores the count
    # of required flips
    ops = 0

    # Stores the last index
    # of '1' in the string
    last_idx = -1

    # Check for the first
    # substring of length K
    for i in range(K):

        # If i-th character
        # is '1'
        if (S[i] == '1'):
            last_idx = i

    # If the substring had
    # no '1'
    if (last_idx == -1):

        # Increase the count
        # of required flips
        ops += 1

        # Flip the last index
        # of the window
        S[K - 1] = '1'

        # Update the last index
        # which contains 1
        last_idx = K - 1

    # Check for remaining substrings
    for i in range(N - K + 1):

        # If last_idx does not
        # belong to current
        # window make it -1
        if (last_idx < i):
            last_idx = -1

        # If the last character of
        # the current substring
        # is '1', then update
        # last_idx to i + k-1;
        if (S[i + K - 1] == '1'):
            last_idx = i + K - 1

        # If last_idx == -1, then
        # the current substring
        # has no 1
        if (last_idx == -1):

            # Increase the count
            # of flips
            ops += 1

            # Update the last index
            # of the current window
            S = S[:i + K - 1] + '1' + S[i + K:]

            # Store the last index of
            # current window as the index
            # of last '1' in the string
            last_idx = i + K - 1

    # Return the number
    # of operations
    return ops

# Driver Code
S = "001010000"
K = 3;

print(minimumMoves(S, K))

# This code is contributed by yatinagg
```

## C#

```
// C# program to find the
// minimum numbers of flips
// required in a binary string
// such that all substrings of
// size K has atleast one 1
using System;
using System.Text;

class GFG{

// Function to calculate and
// return the minimum number
// of flips to make string valid
public static int minimumMoves(String s, int K)
{
    StringBuilder S = new StringBuilder(s);
    int N = S.Length;

    // Stores the count
    // of required flips
    int ops = 0;

    // Stores the last index
    // of '1' in the string
    int last_idx = -1;

    // Check for the first
    // substring of length K
    for(int i = 0; i < K; i++)
    {

        // If i-th character
        // is '1'
        if (S[i] == '1')
            last_idx = i;
    }

    // If the substring had
    // no '1'
    if (last_idx == -1)
    {

        // Increase the count
        // of required flips
        ++ops;

        // Flip the last index
        // of the window
        S.Insert(K - 1, '1');

        // Update the last index
        // which contains 1
        last_idx = K - 1;
    }

    // Check for remaining substrings
    for(int i = 1; i < N - K + 1; i++)
    {

        // If last_idx does not
        // belong to current
        // window make it -1
        if (last_idx < i)
            last_idx = -1;

        // If the last character of
        // the current substring
        // is '1', then update
        // last_idx to i+k-1;
        if (S[i + K - 1] == '1')
            last_idx = i + K - 1;

        // If last_idx == -1, then
        // the current substring
        // has no 1
        if (last_idx == -1)
        {

            // Increase the count
            // of flips
            ++ops;

            // Update the last index
            // of the current window
            S.Insert(i + K - 1, '1');

            // Store the last index
            // of current window as
            // the index of last '1'
            // in the string
            last_idx = i + K - 1;
        }
    }

    // Return the number
    // of operations
    return ops;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "001010000";
    int K = 3;

    Console.WriteLine(minimumMoves(S, K));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to find the
// minimum numbers of flips
// required in a binary string
// such that all substrings of
// size K has atleast one 1

// Function to calculate and
// return the minimum number
// of flips to make string valid
function minimumMoves(S, K)
{
    var N = S.length;

    // Stores the count
    // of required flips
    var ops = 0;

    // Stores the last index
    // of '1' in the string
    var last_idx = -1;

    // Check for the first
    // substring of length K
    for (var i = 0; i < K; i++) {

        // If i-th character
        // is '1'
        if (S[i] == '1')
            last_idx = i;
    }

    // If the substring had
    // no '1'
    if (last_idx == -1) {

        // Increase the
        // count of required
        // flips
        ++ops;

        // Flip the last
        // index of the
        // window
        S[K - 1] = '1';

        // Update the last
        // index which
        // contains 1
        last_idx = K - 1;
    }

    // Check for remaining substrings
    for (var i = 1; i < N - K + 1; i++) {

        // If last_idx does not
        // belong to current
        // window make it -1
        if (last_idx < i)
            last_idx = -1;

        // If the last character of
        // the current substring
        // is '1', then update
        // last_idx to i+k-1;
        if (S[i + K - 1] == '1')
            last_idx = i + K - 1;

        // If last_idx == -1, then
        // the current substring
        // has no 1
        if (last_idx == -1) {

            // Increase the count
            // of flips
            ++ops;

            // Update the last
            // index of the
            // current window
            S[i + K - 1] = '1';

            // Store the last
            // index of current
            // window as the
            // index of last '1'
            // in the string
            last_idx = i + K - 1;
        }
    }
    // Return the number
    // of operations
    return ops;
}

// Driver Code
var S = "001010000";
var K = 3;
document.write( minimumMoves(S, K));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
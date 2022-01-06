# 最大化子序列的长度，该子序列由一个字符串中的 K 个增量组成

> 原文:[https://www . geeksforgeeks . org/最大化子序列长度-由单个不同字符组成-可能的 k 个字符串增量/](https://www.geeksforgeeks.org/maximize-length-of-subsequence-consisting-of-single-distinct-character-possible-by-k-increments-in-a-string/)

给定一个由小写字符和整数组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是通过最多增加 **K** 个字符来找到由单个不同字符组成的子序列的最大长度。

**示例:**

> **输入:**S =“acsccca”K = 1
> **输出:** 5
> **解释:**将字符 S[4]从‘b’递增到‘c’，将字符串修改为“acsccca”。因此，相同字符的最长子序列是“ccccccc”。子序列的长度是 5。
> 
> **输入:**S = " adscasr "，K = 2
> T3】输出: 4

**方法:**这个给定的问题可以通过使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)技术和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)来解决。按照以下步骤解决此问题:

*   初始化变量，说**开始**、**结束**、**求和**到 **0** ，存储子序列的开始和结束索引滑动窗口的和。
*   初始化一个变量，比如说**和**到 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，存储结果最长子序列的长度。
*   [对给定的字符串**进行排序**](https://www.geeksforgeeks.org/sort-string-characters/) 。
*   [在**【0，N-1】**范围内穿过管柱](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并执行以下步骤:
    *   将**和**的值增加**(S[end]–‘a’)**。
    *   [迭代一个循环，直到](https://www.geeksforgeeks.org/range-based-loop-c/)**(和+ K)** 的值小于**(S[end]–‘a’)*(end–start+1)**并执行以下步骤:
        *   将**和**的值减( **S【开始】–‘a’)**。
        *   通过 **1** 增加**开始**的值。
    *   经过以上步骤，最多使用 **K** 增量，就可以使**【开始，结束】**范围内的所有字符相等。因此，将 **ans** 的值更新为 **ans** 和**(end–start+1)**的最大值。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
// of a subsequence of same characters
// after at most K increment operations
void maxSubsequenceLen(string S, int K)
{
    // Store the size of S
    int N = S.length();

    int start = 0, end = 0;

    // Sort the given string
    sort(S.begin(), S.end());

    // Stores the maximum length and the
    // sum of the sliding window
    int ans = INT_MIN, sum = 0;

    // Traverse the string S
    for (end = 0; end < N; end++) {

        // Add the current character
        // to the window
        sum = sum + (S[end] - 'a');

        // Decrease the window size
        while (sum + K
               < (S[end] - 'a') * (end - start + 1)) {

            // Update the value of sum
            sum = sum - (S[start] - 'a');

            // Increment the value
            // of start
            start++;
        }

        // Update the maximum window size
        ans = max(ans, end - start + 1);
    }

    // Print the resultant maximum
    // length of the subsequence
    cout << ans;
}

// Driver Code
int main()
{
    string S = "acscbcca";
    int K = 1;
    maxSubsequenceLen(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.math.*;
import java.util.Arrays;

class GFG{

// Function to find the maximum length
// of a subsequence of same characters
// after at most K increment operations
static void maxSubsequenceLen(String s, int K)
{

    // Store the size of s
    int N = s.length();

    int start = 0, end = 0;

    // Sort the given string
    //sort(S.begin(), S.end());
    // convert input string to char array
    char S[] = s.toCharArray();

    // sort tempArray
    Arrays.sort(S);

    // Stores the maximum length and the
    // sum of the sliding window
    int ans = Integer.MIN_VALUE, sum = 0;

    // Traverse the string S
    for(end = 0; end < N; end++)
    {

        // Add the current character
        // to the window
        sum = sum + (S[end] - 'a');

        // Decrease the window size
        while (sum + K < (S[end] - 'a') *
              (end - start + 1))
        {

            // Update the value of sum
            sum = sum - (S[start] - 'a');

            // Increment the value
            // of start
            start++;
        }

        // Update the maximum window size
        ans = Math.max(ans, end - start + 1);
    }

    // Print the resultant maximum
    // length of the subsequence
    System.out.println(ans);
}

// Driver code
public static void main(String args[])
{
    String S = "acscbcca";
    int K = 1;

    maxSubsequenceLen(S, K);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum length
# of a subsequence of same characters
# after at most K increment operations
def maxSubsequenceLen(S, K):

    # Store the size of S
    N = len(S)

    start, end = 0, 0

    # Sort the given string
    S = sorted(S)

    # Stores the maximum length and the
    # sum of the sliding window
    ans, sum =-10**9, 0

    # Traverse the S
    for end in range(N):

        # Add the current character
        # to the window
        sum = sum + (ord(S[end]) - ord('a'))

        # Decrease the window size
        while (sum + K < (ord(S[end]) - ord('a')) *
              (end - start + 1)):

            # Update the value of sum
            sum = sum - (ord(S[start]) - ord('a'))

            # Increment the value
            # of start
            start += 1

        # Update the maximum window size
        ans = max(ans, end - start + 1)

    # Print the resultant maximum
    # length of the subsequence
    print (ans)

# Driver Code
if __name__ == '__main__':

    S = "acscbcca"
    K = 1

    maxSubsequenceLen(S, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

// Function to find the maximum length
// of a subsequence of same characters
// after at most K increment operations
static void maxSubsequenceLen(string s, int K)
{

    // Store the size of s
    int N = s.Length;

    int start = 0, end = 0;

    // Sort the given string
    //sort(S.begin(), S.end());
    // convert input string to char array
    char[] S= s.ToCharArray();

    // sort tempArray
    Array.Sort(S);

    // Stores the maximum length and the
    // sum of the sliding window
    int ans = Int32.MinValue, sum = 0;

    // Traverse the string S
    for(end = 0; end < N; end++)
    {

        // Add the current character
        // to the window
        sum = sum + (S[end] - 'a');

        // Decrease the window size
        while (sum + K < (S[end] - 'a') *
              (end - start + 1))
        {

            // Update the value of sum
            sum = sum - (S[start] - 'a');

            // Increment the value
            // of start
            start++;
        }

        // Update the maximum window size
        ans = Math.Max(ans, end - start + 1);
    }

    // Print the resultant maximum
    // length of the subsequence
    Console.WriteLine(ans);
}

    // Driver Code
    public static void Main()
    {
    string S = "acscbcca";
    int K = 1;

    maxSubsequenceLen(S, K);
    }
}

// This code is contributed by souravghosh0416.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum length
// of a subsequence of same characters
// after at most K increment operations
function maxSubsequenceLen(s, K)
{

    // Store the size of s
    var N = s.length;

    var start = 0, end = 0;

    // Sort the given string
    //sort(S.begin(), S.end());
    // convert input string to char array
    var S = s.split('');

    // sort tempArray
    S.sort();

    // Stores the maximum length and the
    // sum of the sliding window
    var ans = Number.MIN_VALUE, sum = 0;

    // Traverse the string S
    for(end = 0; end < N; end++)
    {

        // Add the current character
        // to the window
        sum = sum + (S[end].charCodeAt(0) -
                        'a'.charCodeAt(0));

        // Decrease the window size
        while (sum + K < (S[end].charCodeAt(0) -
                             'a'.charCodeAt(0)) *
              (end - start + 1))
        {

            // Update the value of sum
            sum = sum - (S[start].charCodeAt(0) -
                              'a'.charCodeAt(0));

            // Increment the value
            // of start
            start++;
        }

        // Update the maximum window size
        ans = Math.max(ans, end - start + 1);
    }

    // Print the resultant maximum
    // length of the subsequence
    document.write(ans);
}

// Driver code
var S = "acscbcca";
var K = 1;

maxSubsequenceLen(S, K);

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*
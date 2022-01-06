# 所有字符至少出现 K 次的最长子串|设置 3

> 原文:[https://www . geesforgeks . org/最长子串-所有字符出现的位置-至少 k 次-set-3/](https://www.geeksforgeeks.org/longest-substring-where-all-the-characters-appear-at-least-k-times-set-3/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**和一个整数 **K** ，任务是找到最长的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/) **S** 的长度，使得 **S** 中的每个字符至少出现 **K** 次。

**示例:**

> **输入:** str = "aabbba "，K = 3
> **输出:** 6
> **说明:**在子串“aabbba”中，每个字符至少重复 K 次，长度为 6。
> 
> **输入:** str = "ababacb "，K = 3
> **输出:** 0
> **说明:**没有每个字符重复至少 K 次的子串。

**天真方法:**解决给定问题的最简单方法在[集 1](https://www.geeksforgeeks.org/largest-sub-string-where-all-the-characters-appear-at-least-k-times/) 中讨论。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(26)*

[**分治法**](https://www.geeksforgeeks.org/divide-and-conquer-introduction/) **法:**给定问题的分治法在[第 2 集](https://www.geeksforgeeks.org/largest-substring-where-all-characters-appear-at-least-k-times-set-2/)中讨论。
***时间复杂度:**O(N * log N)*
***辅助空间:** O(26)*

**高效途径:**以上两种途径可以通过[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)T4 进一步优化。按照以下步骤解决问题:

*   将字符串 **字符串**中的[唯一字符数存储在一个变量中，比如说**唯一的**。](https://www.geeksforgeeks.org/print-all-distinct-characters-of-a-string-in-order-3-methods/)
*   用**{ 0 }**[初始化一个大小为 **26** 的数组 **freq[]** ，并存储该数组中每个字符](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/)的频率。
*   [使用变量 **curr_unique** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，唯一】**。在每次迭代中， **curr_unique** 是窗口中必须出现的唯一字符的最大数量。
    *   用 **{0}** 重新初始化数组 **freq[]** ，以在此窗口中存储每个字符的频率。
    *   初始化**开始**和**结束**为 **0** ，分别存储窗口的起点和终点。
    *   使用两个变量 **cnt** ，用于存储唯一字符的数量， **countK** ，用于存储当前窗口中至少有 **K** 个重复字符的字符数量。
    *   现在，[迭代一个循环，同时**结束<N**T3】，执行以下操作:](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)
        *   如果 **cnt** 的值小于或等于 **curr_unique，**则通过在窗口末尾添加一个字符从右侧扩展窗口。并在**频率[]** 中将其频率增加 **1** 。
        *   否则，通过从**开始**删除一个字符，并在**频率[]** 中将其频率减少 **1** 来缩小左边的窗口。
        *   每一步，更新 **cnt** 和 **countK** 的值。
        *   如果 **cnt** 的值与 **curr_unique** 相同，且每个字符出现**至少 K 次**，则更新整体最大长度并存储在**和**中。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// the longest substring
int longestSubstring(string s, int k)
{
    // Store the required answer
    int ans = 0;

    // Create a frequency map of the
    // characters of the string
    int freq[26] = { 0 };

    // Store the length of the string
    int n = s.size();

    // Traverse the string, s
    for (int i = 0; i < n; i++)

        // Increment the frequency of
        // the current character by 1
        freq[s[i] - 'a']++;

    // Stores count of unique characters
    int unique = 0;

    // Find the number of unique
    // characters in string
    for (int i = 0; i < 26; i++)
        if (freq[i] != 0)
            unique++;

    // Iterate in range [1, unique]
    for (int curr_unique = 1;
         curr_unique <= unique;
         curr_unique++) {

        // Initialize frequency of all
        // characters as 0
        memset(freq, 0, sizeof(freq));

        // Stores the start and the
        // end of the window
        int start = 0, end = 0;

        // Stores the current number of
        // unique characters and characters
        // occuring atleast K times
        int cnt = 0, count_k = 0;

        while (end < n) {
            if (cnt <= curr_unique) {
                int ind = s[end] - 'a';

                // New unique character
                if (freq[ind] == 0)
                    cnt++;

                freq[ind]++;

                // New character which
                // occurs atleast k times
                if (freq[ind] == k)
                    count_k++;

                // Expand window by
                // incrementing end by 1
                end++;
            }
            else {
                int ind = s[start] - 'a';

                // Check if this character
                // is present atleast k times
                if (freq[ind] == k)
                    count_k--;

                freq[ind]--;

                // Check if this character
                // is unique
                if (freq[ind] == 0)
                    cnt--;

                // Shrink the window by
                // incrementing start by 1
                start++;
            }

            // If there are curr_unique
            // characters and each character
            // is atleast k times
            if (cnt == curr_unique
                && count_k == curr_unique)

                // Update the overall
                // maximum length
                ans = max(ans, end - start);
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    string S = "aabbba";
    int K = 3;
    longestSubstring(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the length of
// the longest subString
static void longestSubString(char[] s, int k)
{

    // Store the required answer
    int ans = 0;

    // Create a frequency map of the
    // characters of the String
    int freq[] = new int[26];

    // Store the length of the String
    int n = s.length;

    // Traverse the String, s
    for (int i = 0; i < n; i++)

        // Increment the frequency of
        // the current character by 1
        freq[s[i] - 'a']++;

    // Stores count of unique characters
    int unique = 0;

    // Find the number of unique
    // characters in String
    for (int i = 0; i < 26; i++)
        if (freq[i] != 0)
            unique++;

    // Iterate in range [1, unique]
    for (int curr_unique = 1;
         curr_unique <= unique;
         curr_unique++)
    {

        // Initialize frequency of all
        // characters as 0
        Arrays.fill(freq, 0);

        // Stores the start and the
        // end of the window
        int start = 0, end = 0;

        // Stores the current number of
        // unique characters and characters
        // occuring atleast K times
        int cnt = 0, count_k = 0;
        while (end < n)
        {
            if (cnt <= curr_unique)
            {
                int ind = s[end] - 'a';

                // New unique character
                if (freq[ind] == 0)
                    cnt++;
                freq[ind]++;

                // New character which
                // occurs atleast k times
                if (freq[ind] == k)
                    count_k++;

                // Expand window by
                // incrementing end by 1
                end++;
            }
            else
            {
                int ind = s[start] - 'a';

                // Check if this character
                // is present atleast k times
                if (freq[ind] == k)
                    count_k--;
                freq[ind]--;

                // Check if this character
                // is unique
                if (freq[ind] == 0)
                    cnt--;

                // Shrink the window by
                // incrementing start by 1
                start++;
            }

            // If there are curr_unique
            // characters and each character
            // is atleast k times
            if (cnt == curr_unique
                && count_k == curr_unique)

                // Update the overall
                // maximum length
                ans = Math.max(ans, end - start);
        }
    }

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    String S = "aabbba";
    int K = 3;
    longestSubString(S.toCharArray(), K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of
# the longest substring
def longestSubstring(s, k) :

    # Store the required answer
    ans = 0

    # Create a frequency map of the
    # characters of the string
    freq = [0]*26

    # Store the length of the string
    n = len(s)

    # Traverse the string, s
    for i in range(n) :

        # Increment the frequency of
        # the current character by 1
        freq[ord(s[i]) - ord('a')] += 1

    # Stores count of unique characters
    unique = 0

    # Find the number of unique
    # characters in string
    for i in range(26) :
        if (freq[i] != 0) :
            unique += 1

    # Iterate in range [1, unique]
    for curr_unique in range(1, unique + 1) :

        # Initialize frequency of all
        # characters as 0
        Freq = [0]*26

        # Stores the start and the
        # end of the window
        start, end = 0, 0

        # Stores the current number of
        # unique characters and characters
        # occuring atleast K times
        cnt, count_k = 0, 0

        while (end < n) :
            if (cnt <= curr_unique) :
                ind = ord(s[end]) - ord('a')

                # New unique character
                if (Freq[ind] == 0) :
                    cnt += 1

                Freq[ind] += 1

                # New character which
                # occurs atleast k times
                if (Freq[ind] == k) :
                    count_k += 1

                # Expand window by
                # incrementing end by 1
                end += 1

            else :
                ind = ord(s[start]) - ord('a')

                # Check if this character
                # is present atleast k times
                if (Freq[ind] == k) :
                    count_k -= 1

                Freq[ind] -= 1

                # Check if this character
                # is unique
                if (Freq[ind] == 0) :
                    cnt -= 1

                # Shrink the window by
                # incrementing start by 1
                start += 1

            # If there are curr_unique
            # characters and each character
            # is atleast k times
            if ((cnt == curr_unique) and (count_k == curr_unique)) :

                # Update the overall
                # maximum length
                ans = max(ans, end - start)

    # Print the answer
    print(ans)

S = "aabbba"
K = 3
longestSubstring(S, K)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to find the length of
// the longest substring
static void longestSubstring(string s, int k)
{

    // Store the required answer
    int ans = 0;

    // Create a frequency map of the
    // characters of the string
    int[] freq = new int[26];

    // Store the length of the string
    int n = s.Length;

    // Traverse the string, s
    for (int i = 0; i < n; i++)

        // Increment the frequency of
        // the current character by 1
        freq[s[i] - 'a']++;

    // Stores count of unique characters
    int unique = 0;

    // Find the number of unique
    // characters in string
    for (int i = 0; i < 26; i++)
        if (freq[i] != 0)
            unique++;

    // Iterate in range [1, unique]
    for (int curr_unique = 1;
         curr_unique <= unique;
         curr_unique++)
    {

        // Initialize frequency of all
        // characters as 0
        for (int i = 0; i < freq.Length; i++)
        {
            freq[i] = 0;
        }

        // Stores the start and the
        // end of the window
        int start = 0, end = 0;

        // Stores the current number of
        // unique characters and characters
        // occuring atleast K times
        int cnt = 0, count_k = 0;
        while (end < n)
        {
            if (cnt <= curr_unique)
            {
                int ind = s[end] - 'a';

                // New unique character
                if (freq[ind] == 0)
                    cnt++;
                freq[ind]++;

                // New character which
                // occurs atleast k times
                if (freq[ind] == k)
                    count_k++;

                // Expand window by
                // incrementing end by 1
                end++;
            }
            else
            {
                int ind = s[start] - 'a';

                // Check if this character
                // is present atleast k times
                if (freq[ind] == k)
                    count_k--;
                freq[ind]--;

                // Check if this character
                // is unique
                if (freq[ind] == 0)
                    cnt--;

                // Shrink the window by
                // incrementing start by 1
                start++;
            }

            // If there are curr_unique
            // characters and each character
            // is atleast k times
            if (cnt == curr_unique
                && count_k == curr_unique)

                // Update the overall
                // maximum length
                ans = Math.Max(ans, end - start);
        }
    }

    // Print the answer
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
   string S = "aabbba";
    int K = 3;
    longestSubstring(S, K);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to find the length of
    // the longest substring
    function longestSubstring(s, k)
    {

        // Store the required answer
        let ans = 0;

        // Create a frequency map of the
        // characters of the string
        let freq = new Array(26);
        freq.fill(0);

        // Store the length of the string
        let n = s.length;

        // Traverse the string, s
        for (let i = 0; i < n; i++)

            // Increment the frequency of
            // the current character by 1
            freq[s[i].charCodeAt() -
               'a'.charCodeAt()]++;

        // Stores count of unique characters
        let unique = 0;

        // Find the number of unique
        // characters in string
        for (let i = 0; i < 26; i++)
            if (freq[i] != 0)
                unique++;

        // Iterate in range [1, unique]
        for (let curr_unique = 1;
             curr_unique <= unique;
             curr_unique++)
        {

            // Initialize frequency of all
            // characters as 0
            for (let i = 0; i < freq.length; i++)
            {
                freq[i] = 0;
            }

            // Stores the start and the
            // end of the window
            let start = 0, end = 0;

            // Stores the current number of
            // unique characters and characters
            // occuring atleast K times
            let cnt = 0, count_k = 0;
            while (end < n)
            {
                if (cnt <= curr_unique)
                {
                    let ind = s[end].charCodeAt() -
                              'a'.charCodeAt();

                    // New unique character
                    if (freq[ind] == 0)
                        cnt++;
                    freq[ind]++;

                    // New character which
                    // occurs atleast k times
                    if (freq[ind] == k)
                        count_k++;

                    // Expand window by
                    // incrementing end by 1
                    end++;
                }
                else
                {
                    let ind = s[start].charCodeAt() -
                    'a'.charCodeAt();

                    // Check if this character
                    // is present atleast k times
                    if (freq[ind] == k)
                        count_k--;
                    freq[ind]--;

                    // Check if this character
                    // is unique
                    if (freq[ind] == 0)
                        cnt--;

                    // Shrink the window by
                    // incrementing start by 1
                    start++;
                }

                // If there are curr_unique
                // characters and each character
                // is atleast k times
                if (cnt == curr_unique
                    && count_k == curr_unique)

                    // Update the overall
                    // maximum length
                    ans = Math.max(ans, end - start);
            }
        }

        // Print the answer
        document.write(ans);
    }

    let S = "aabbba";
    let K = 3;
    longestSubstring(S, K);

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
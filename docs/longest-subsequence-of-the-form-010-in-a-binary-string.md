# 二进制字符串中 0*1*0*形式的最长子序列

> 原文:[https://www . geesforgeks . org/最长二进制字符串形式的子序列 010/](https://www.geeksforgeeks.org/longest-subsequence-of-the-form-010-in-a-binary-string/)

给定一个二进制字符串，找到其中形式(0)*(1)*(0)*的最长子序列。基本上，我们需要将字符串分成 3 个不重叠的字符串(这些字符串可能是空的)，而不改变字母的顺序。**第一和第三根**弦仅由**0**组成，第二根弦仅由 1 组成。这些字符串可以通过删除原始字符串中的一些字符来制作**。绳子的**最大尺寸**是多少，我们能拿到吗？**

**示例:**

```
Input : 000011100000 
Output : 12
Explanation : 
First part from 1 to 4.
Second part 5 to 7\. 
Third part from 8 to 12 

Input : 100001100  
Output : 8
Explanation : 
Delete the first letter. 
First part from 2 to 4\. 
Second part from 5 to 6\. 
Last part from 7.

Input : 00000 
Output : 5
Explanation : 
Special Case of Only 0

Input : 111111
Output : 6
Explanation : 
Special Case of Only 1

Input : 0000001111011011110000 
Output : 20
Explanation : 
Second part is from 7 to 18\. 
Remove all the 0 between indices 7 to 18.
```

一个**简单的解决方案**是[生成给定序列](https://www.geeksforgeeks.org/print-subsequences-string/)的所有子序列。对于每个子序列，检查它是否是给定的形式。如果是，将其与迄今为止的结果进行比较，并根据需要更新结果。
通过在 **O(n^2 时间**对数组下方进行预计算，可以有效地**解决这个问题。
让 pre_count_0[i]为字符串前缀中字母 0 的计数直到索引 i.
让 pre_count_1[i]为字符串前缀中字母 1 的计数直到长度 i.
让 post_count_0[i]为从索引 I 到索引 n 的后缀字符串中字母 0 的计数(这里 n 为字符串的大小)。
现在我们固定两个位置 I 和 j，1 < =i < = j < =n。我们将从从索引 I 开始到索引 j 结束的子串中移除所有 0。因此，这使得第二个子串只有 1。在索引 I 之前的前缀和索引 j 之后的后缀中，我们将删除所有 1，因此它将成为字符串的第一和第三部分。
则可获得的最大字符串长度为
pre _ count _ 0[I-1]+(pre _ count _ 1[j]-pre _ count _ 1[I-1])+pre _ count _ 1[j+1]
**特殊情况:**当字符串仅由 0 或 1 组成时，ans 为 n，其中 n 为字符串长度。**

## C++

```
// CPP program to find longest subsequence
// of the form 0*1*0* in a binary string
#include <bits/stdc++.h>
using namespace std;

// Returns length of the longest subsequence
// of the form 0*1*0*
int longestSubseq(string s)
{
    int n = s.length();

    // Precomputing values in three arrays
    // pre_count_0[i] is going to store count
    //             of 0s in prefix str[0..i-1]
    // pre_count_1[i] is going to store count
    //             of 1s in prefix str[0..i-1]
    // post_count_0[i] is going to store count
    //             of 0s in suffix str[i-1..n-1]
    int pre_count_0[n + 2];
    int pre_count_1[n + 1];
    int post_count_0[n + 1];
    pre_count_0[0] = 0;
    post_count_0[n + 1] = 0;
    pre_count_1[0] = 0;
    for (int j = 1; j <= n; j++)
    {
        pre_count_0[j] = pre_count_0[j - 1];
        pre_count_1[j] = pre_count_1[j - 1];
        post_count_0[n - j + 1] = post_count_0[n - j + 2];

        if (s[j - 1] == '0')
            pre_count_0[j]++;
        else
            pre_count_1[j]++;
        if (s[n - j] == '0')
           post_count_0[n - j + 1]++;
    }

    // string is made up of all 0s or all 1s
    if (pre_count_0[n] == n ||
        pre_count_0[n] == 0)
        return n;

    // Compute result using precomputed values
    int ans = 0;
    for (int i = 1; i <= n; i++)
        for (int j = i; j <= n; j++)
            ans = max(pre_count_0[i - 1]
                    + pre_count_1[j]
                    - pre_count_1[i - 1]
                    + post_count_0[j + 1],
                    ans);
    return ans;
}

// driver program
int main()
{
    string s = "000011100000";
    cout << longestSubseq(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest subsequence
// of the form 0*1*0* in a binary string
class GFG
{

    // Returns length of the longest subsequence
    // of the form 0*1*0*
    public static int longestSubseq(String s)
    {
        int n = s.length();

        // Precomputing values in three arrays
        // pre_count_0[i] is going to store count
        // of 0s in prefix str[0..i-1]
        // pre_count_1[i] is going to store count
        // of 1s in prefix str[0..i-1]
        // post_count_0[i] is going to store count
        // of 0s in suffix str[i-1..n-1]
        int[] pre_count_0 = new int[n + 2];
        int[] pre_count_1 = new int[n + 1];
        int[] post_count_0 = new int[n + 2];
        pre_count_0[0] = 0;
        post_count_0[n + 1] = 0;
        pre_count_1[0] = 0;
        for (int j = 1; j <= n; j++)
        {
            pre_count_0[j] = pre_count_0[j - 1];
            pre_count_1[j] = pre_count_1[j - 1];
            post_count_0[n - j + 1] = post_count_0[n - j + 2];

            if (s.charAt(j - 1) == '0')
                pre_count_0[j]++;
            else
                pre_count_1[j]++;

            if (s.charAt(n - j) == '0')
                post_count_0[n - j + 1]++;
        }

        // string is made up of all 0s or all 1s
        if (pre_count_0[n] == n ||
            pre_count_0[n] == 0)
            return n;

        // Compute result using precomputed values
        int ans = 0;
        for (int i = 1; i <= n; i++)
            for (int j = i; j <= n; j++)
                ans = Math.max(pre_count_0[i - 1] +
                               pre_count_1[j] -
                               pre_count_1[i - 1] +
                               post_count_0[j + 1], ans);
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "000011100000";
        System.out.println(longestSubseq(s));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 program to find longest subsequence
# of the form 0*1*0* in a binary string

# Returns length of the longest subsequence
# of the form 0*1*0*
def longestSubseq(s):
    n = len(s)

    # Precomputing values in three arrays
    # pre_count_0[i] is going to store count
    #         of 0s in prefix str[0..i-1]
    # pre_count_1[i] is going to store count
    #         of 1s in prefix str[0..i-1]
    # post_count_0[i] is going to store count
    #         of 0s in suffix str[i-1..n-1]
    pre_count_0 = [0 for i in range(n + 2)]
    pre_count_1 = [0 for i in range(n + 1)]
    post_count_0 = [0 for i in range(n + 2)]
    pre_count_0[0] = 0
    post_count_0[n + 1] = 0
    pre_count_1[0] = 0
    for j in range(1, n + 1):
        pre_count_0[j] = pre_count_0[j - 1]
        pre_count_1[j] = pre_count_1[j - 1]
        post_count_0[n - j + 1] = post_count_0[n - j + 2]

        if (s[j - 1] == '0'):
            pre_count_0[j] += 1
        else:
            pre_count_1[j] += 1
        if (s[n - j] == '0'):
            post_count_0[n - j + 1] += 1

    # string is made up of all 0s or all 1s
    if (pre_count_0[n] == n or
        pre_count_0[n] == 0):
        return n

    # Compute result using precomputed values
    ans = 0
    for i in range(1, n + 1):
        for j in range(i, n + 1, 1):
            ans = max(pre_count_0[i - 1] +
                      pre_count_1[j] -
                      pre_count_1[i - 1] +
                      post_count_0[j + 1], ans)
    return ans

# Driver Code
if __name__ == '__main__':
    s = "000011100000"
    print(longestSubseq(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find longest subsequence
// of the form 0*1*0* in a binary string
using System;

class GFG
{

    // Returns length of the longest subsequence
    // of the form 0*1*0*
    public static int longestSubseq(String s)
    {
        int n = s.Length;

        // Precomputing values in three arrays
        // pre_count_0[i] is going to store count
        // of 0s in prefix str[0..i-1]
        // pre_count_1[i] is going to store count
        // of 1s in prefix str[0..i-1]
        // post_count_0[i] is going to store count
        // of 0s in suffix str[i-1..n-1]
        int[] pre_count_0 = new int[n + 2];
        int[] pre_count_1 = new int[n + 1];
        int[] post_count_0 = new int[n + 2];
        pre_count_0[0] = 0;
        post_count_0[n + 1] = 0;
        pre_count_1[0] = 0;
        for (int j = 1; j <= n; j++)
        {
            pre_count_0[j] = pre_count_0[j - 1];
            pre_count_1[j] = pre_count_1[j - 1];
            post_count_0[n - j + 1] = post_count_0[n - j + 2];

            if (s[j - 1] == '0')
                pre_count_0[j]++;
            else
                pre_count_1[j]++;

            if (s[n - j] == '0')
                post_count_0[n - j + 1]++;
        }

        // string is made up of all 0s or all 1s
        if (pre_count_0[n] == n ||
            pre_count_0[n] == 0)
            return n;

        // Compute result using precomputed values
        int ans = 0;
        for (int i = 1; i <= n; i++)
            for (int j = i; j <= n; j++)
                ans = Math.Max(pre_count_0[i - 1] +
                               pre_count_1[j] -
                               pre_count_1[i - 1] +
                               post_count_0[j + 1], ans);
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "000011100000";
        Console.WriteLine(longestSubseq(s));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find longest subsequence
// of the form 0*1*0* in a binary string

// Returns length of the longest subsequence
// of the form 0*1*0*
function longestSubseq(s)
{
    let n = s.length;

    // Precomputing values in three arrays
    // pre_count_0[i] is going to store count
    // of 0s in prefix str[0..i-1]
    // pre_count_1[i] is going to store count
    // of 1s in prefix str[0..i-1]
    // post_count_0[i] is going to store count
    // of 0s in suffix str[i-1..n-1]
    let pre_count_0 = new Array(n + 2);
    let pre_count_1 = new Array(n + 1);
    let post_count_0 = new Array(n + 2);
    pre_count_0[0] = 0;
    post_count_0[n + 1] = 0;
    pre_count_1[0] = 0;

    for(let j = 1; j <= n; j++)
    {
        pre_count_0[j] = pre_count_0[j - 1];
        pre_count_1[j] = pre_count_1[j - 1];
        post_count_0[n - j + 1] = post_count_0[n - j + 2];

        if (s[j - 1] == '0')
            pre_count_0[j]++;
        else
            pre_count_1[j]++;

        if (s[n - j] == '0')
            post_count_0[n - j + 1]++;
    }

    // String is made up of all 0s or all 1s
    if (pre_count_0[n] == n ||
        pre_count_0[n] == 0)
        return n;

    // Compute result using precomputed values
    let ans = 0;
    for(let i = 1; i <= n; i++)
        for(let j = i; j <= n; j++)
            ans = Math.max(pre_count_0[i - 1] +
                           pre_count_1[j] -
                           pre_count_1[i - 1] +
                           post_count_0[j + 1], ans);
    return ans;
}

// Driver code
let s = "000011100000";

document.write(longestSubseq(s));

// This code is contributed by vaibhavrabadiya3

</script>
```

**输出:**

```
12
```

本文由 [**nikhil ranjan 7**](https://auth.geeksforgeeks.org/profile.php?user=nikhil ranjan 7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
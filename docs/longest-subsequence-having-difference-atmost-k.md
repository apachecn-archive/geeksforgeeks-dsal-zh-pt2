# 具有不同气氛 K 的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列-有差异-atmat-k/](https://www.geeksforgeeks.org/longest-subsequence-having-difference-atmost-k/)

给定一个长度为 **N** 的字符串 **S** 和一个整数 **K** ，任务是找到最长子序列的长度，使得子序列中相邻字符的 ASCII 值之差不超过 K

**示例:**

```
Input: N = 7, K = 2, S = "afcbedg"
Output: 4
Explanation:
Longest special sequence present 
in "afcbedg" is a, c, b, d.
It is special because |a - c| <= 2, 
|c - b| <= 2 and | b-d| <= 2

Input: N = 13, K = 3, S = "geeksforgeeks"
Output: 7
```

**天真的方法:**蛮力的解决方案是生成所有可能的各种长度的子序列，并计算有效子序列的最大长度。时间复杂度将是指数级的。

**高效方法:**高效方法是使用概念 [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/)

*   创建一个 0 的数组 **dp** ，其大小等于字符串的长度。
*   创建一个支持数组**最大长度**，0 的大小为 26。
*   逐个字符地迭代字符串，并为每个字符确定上限和下限。
*   迭代下限和上限范围内的嵌套循环。
*   用当前 **dp** 索引和当前 max_length 索引+1 之间的最大值填充 dp 数组。
*   用当前 **dp** 索引和当前最大长度索引之间的最大值填充最大长度数组。
*   最长子序列长度是 **dp** 数组中的最大值。
*   让我们考虑一个例子:

> 输入字符串 **s** 为“afcbedg”， **k** 为 2
> 
> *   对于第一次迭代，I 的值为“a ”, j 的范围为(0，2)
>     ,当前 dp = [1，0，0，0，0，0，0]
> *   对于第二次迭代，I 的值为‘f’，j 的范围为(3，7)
>     ，当前 dp = [1，1，0，0，0，0，0]
> *   对于第三次迭代，I 的值为“c ”, j 的范围为(0，4)
>     ,当前 dp = [1，1，2，0，0，0，0]
> *   对于第四次迭代，I 的值为“b ”, j 的范围为(0，3)
>     ,当前 dp = [1，1，2，3，0，0，0]
> *   对于第五次迭代，I 的值为“e ”, j 的范围为(2，6)
>     和当前 dp = [1，1，2，3，3，0，0]
> *   对于第六次迭代，I 的值为“d ”, j 的范围为(1，5)
>     ,当前 dp = [1，1，2，3，3，4，0]
> *   对于第 7 次迭代，I 的值为‘g’，j 的范围为(4，8)
>     ，电流 dp = [1，1，2，3，3，4，4]
> 
> 最长长度是 dp 中的最大值，因此最大长度为 4

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find
// the longest Special Sequence
int longest_subseq(int n, int k, string s)
{

    // Creating a list with
    // all 0's of size
    // equal to the length of string
    vector<int> dp(n, 0);

    // Supporting list with
    // all 0's of size 26 since
    // the given string consists
    // of only lower case alphabets
    int max_length[26] = {0};

    for (int i = 0; i < n; i++)
    {

        // Converting the ascii value to
        // list indices
        int curr = s[i] - 'a';

        // Determining the lower bound
        int lower = max(0, curr - k);

        // Determining the upper bound
        int upper = min(25, curr + k);

        // Filling the dp array with values
        for (int j = lower; j < upper + 1; j++)
        {
            dp[i] = max(dp[i], max_length[j] + 1);
        }
        //Filling the max_length array with max
        //length of subsequence till now
        max_length[curr] = max(dp[i], max_length[curr]);
    }

    int ans = 0;

    for(int i:dp) ans = max(i, ans);

    // return the max length of subsequence
    return ans;
}

// Driver Code
int main()
{
    string s = "geeksforgeeks";
    int n = s.size();
    int k = 3;
    cout << (longest_subseq(n, k, s));
    return 0;
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find
// the longest Special Sequence
static int longest_subseq(int n, int k, String s)
{

    // Creating a list with
    // all 0's of size
    // equal to the length of String
    int []dp = new int[n];

    // Supporting list with
    // all 0's of size 26 since
    // the given String consists
    // of only lower case alphabets
    int []max_length = new int[26];

    for (int i = 0; i < n; i++)
    {

        // Converting the ascii value to
        // list indices
        int curr = s.charAt(i) - 'a';

        // Determining the lower bound
        int lower = Math.max(0, curr - k);

        // Determining the upper bound
        int upper = Math.min(25, curr + k);

        // Filling the dp array with values
        for (int j = lower; j < upper + 1; j++)
        {
            dp[i] = Math.max(dp[i], max_length[j] + 1);
        }

        // Filling the max_length array with max
        // length of subsequence till now
        max_length[curr] = Math.max(dp[i], max_length[curr]);
    }

    int ans = 0;

    for(int i:dp) ans = Math.max(i, ans);

    // return the max length of subsequence
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    int n = s.length();
    int k = 3;
    System.out.print(longest_subseq(n, k, s));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Function to find
# the longest Special Sequence
def longest_subseq(n, k, s):

    # Creating a list with
    # all 0's of size
    # equal to the length of string
    dp = [0] * n

    # Supporting list with
    # all 0's of size 26 since
    # the given string consists
    # of only lower case alphabets
    max_length = [0] * 26

    for i in range(n):

        # Converting the ascii value to
        # list indices
        curr = ord(s[i]) - ord('a')
        # Determining the lower bound
        lower = max(0, curr - k)
        # Determining the upper bound
        upper = min(25, curr + k)
        # Filling the dp array with values
        for j in range(lower, upper + 1):

            dp[i] = max(dp[i], max_length[j]+1)
        # Filling the max_length array with max
        # length of subsequence till now
        max_length[curr] = max(dp[i], max_length[curr])

    # return the max length of subsequence
    return max(dp)

# driver code
def main():
  s = "geeksforgeeks"
  n = len(s)
  k = 3
  print(longest_subseq(n, k, s))

main()
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find
// the longest Special Sequence
static int longest_subseq(int n, int k, String s)
{

    // Creating a list with
    // all 0's of size
    // equal to the length of String
    int []dp = new int[n];

    // Supporting list with
    // all 0's of size 26 since
    // the given String consists
    // of only lower case alphabets
    int []max_length = new int[26];

    for (int i = 0; i < n; i++)
    {

        // Converting the ascii value to
        // list indices
        int curr = s[i] - 'a';

        // Determining the lower bound
        int lower = Math.Max(0, curr - k);

        // Determining the upper bound
        int upper = Math.Min(25, curr + k);

        // Filling the dp array with values
        for (int j = lower; j < upper + 1; j++)
        {
            dp[i] = Math.Max(dp[i], max_length[j] + 1);
        }

        // Filling the max_length array with max
        // length of subsequence till now
        max_length[curr] = Math.Max(dp[i], max_length[curr]);
    }

    int ans = 0;

    foreach(int i in dp) ans = Math.Max(i, ans);

    // return the max length of subsequence
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "geeksforgeeks";
    int n = s.Length;
    int k = 3;
    Console.Write(longest_subseq(n, k, s));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find
// the longest Special Sequence
function longest_subseq(n, k, s)
{

    // Creating a list with
    // all 0's of size
    // equal to the length of String
    let dp = new Array(n);

    // Supporting list with
    // all 0's of size 26 since
    // the given String consists
    // of only lower case alphabets
    let max_length = new Array(26);

    for(let i = 0; i < 26; i++)
    {
        max_length[i] = 0;
        dp[i] = 0;
    }
    for (let i = 0; i < n; i++)
    {

        // Converting the ascii value to
        // list indices
        let curr = s[i].charCodeAt(0) - 'a'.charCodeAt(0);

        // Determining the lower bound
        let lower = Math.max(0, curr - k);

        // Determining the upper bound
        let upper = Math.min(25, curr + k);

        // Filling the dp array with values
        for (let j = lower; j < upper + 1; j++)
        {
            dp[i] = Math.max(dp[i], max_length[j] + 1);
        }

        // Filling the max_length array with max
        // length of subsequence till now
        max_length[curr] = Math.max(dp[i], max_length[curr]);
    }

    let ans = 0;
    ans = Math.max(...dp)

    // return the max length of subsequence
    return ans;
}

// Driver Code
let s = "geeksforgeeks";
let n = s.length;
let k = 3;
document.write(longest_subseq(n, k, s));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
7
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
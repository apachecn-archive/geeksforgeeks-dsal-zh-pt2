# 对给定数字串 K 次串联产生的串中的子序列 01 进行计数

> 原文:[https://www . geeksforgeeks . org/count-subseries-01-in-string-by-concation-to-numeric-string-k-times/](https://www.geeksforgeeks.org/count-subsequences-01-in-string-generated-by-concatenation-of-given-numeric-string-k-times/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个正整数 **K** ，任务是在给定的数字字符串 **S** **K 次**拼接生成的字符串中找到子序列**“01”**的个数。

**示例:**

> **输入:**S =“0171”，K = 2
> **输出:** 6
> **说明:**
> 由 S、K 串接而成的字符串次数为“01710171”。共有 6 个可能的子序列，标记为粗体= {“**01**710171”、 **0** 17 **1** 0171”、 **0** 1710 **1** 71”、 **0** 171017 **1** 、【0171 **01**
> 
> **输入:** S = "230013110087 "，K = 2
> T3】输出: 24

**天真方法:**解决给定问题的最简单方法是通过串联 **S** 、 **K** 次生成结果字符串，然后[从字符串中找到所有可能的对(I，j)](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) ，使得 **(i < j)** 和**S【I】= 0**和**S【j】= 1**。

***时间复杂度:**O((N * K)<sup>2</sup>)*
***辅助空间:** O(N*K)*

**高效方法:**也可以通过观察以下两种情况来优化任务:

*   **情况 1:** 子串**“01”**严格在 **P** 中 **S** 的每次出现内。假设 **C** 是 **S** 中**“01”**的出现次数，那么在 **P** 中就是 **C*K** 。
*   **情况二:**当‘**0**位于**内**I<sup>第</sup>次出现的 **S** 和‘**1**位于某 j <sup>次出现的</sup>次出现的内部形成一个子序列“ **01** ”这样 i < j，那么求“ **01** 的出现次数就和选择这两个一样了设该值为 S <sub>i</sub> 和 S <sub>j</sub> ，将其乘以 S <sub>i</sub> 中“0”的出现次数(由 **cnt0** 表示)和 S <sub>j</sub> 中“1”的出现次数(由 **cnt1** 表示)，得出“01”的子序列数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number of
// subsequences of "01"
int countSubsequence(string S, int N,
                     int K)
{
    // Store count of 0's and 1's
    int C = 0, C1 = 0, C0 = 0;

    for (int i = 0; i < N; i++) {
        if (S[i] == '1')
            C1++;
        else if (S[i] == '0')
            C0++;
    }

    // Count of subsequences without
    // concatenation
    int B1 = 0;
    for (int i = 0; i < N; i++) {
        if (S[i] == '1')
            B1++;
        else if (S[i] == '0')
            C = C + (C1 - B1);
    }

    // Case 1
    int ans = C * K;

    // Case 2
    ans += (C1 * C0 * (((K) * (K - 1)) / 2));

    // Return the total count
    return ans;
}

// Driver Code
int main()
{
    string S = "230013110087";
    int K = 2;
    int N = S.length();

    cout << countSubsequence(S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to calculate the number of
    // subsequences of "01"
    static int countSubsequence(String S, int N, int K)
    {
        // Store count of 0's and 1's
        int C = 0, C1 = 0, C0 = 0;

        for (int i = 0; i < N; i++) {
            if (S.charAt(i) == '1')
                C1++;
            else if (S.charAt(i) == '0')
                C0++;
        }

        // Count of subsequences without
        // concatenation
        int B1 = 0;
        for (int i = 0; i < N; i++) {
            if (S.charAt(i) == '1')
                B1++;
            else if (S.charAt(i) == '0')
                C = C + (C1 - B1);
        }

        // Case 1
        int ans = C * K;

        // Case 2
        ans += (C1 * C0 * (((K) * (K - 1)) / 2));

        // Return the total count
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "230013110087";
        int K = 2;
        int N = S.length();

        System.out.println(countSubsequence(S, N, K));
    }
}

// This code  is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach

# Function to calculate the number of
# subsequences of "01"
def countSubsequence(S, N, K):

        # Store count of 0's and 1's
    C = 0
    C1 = 0
    C0 = 0

    for i in range(0, N):

        if (S[i] == '1'):
            C1 += 1
        elif (S[i] == '0'):
            C0 += 1

        # Count of subsequences without
        # concatenation
    B1 = 0

    for i in range(0, N):
        if (S[i] == '1'):
            B1 += 1
        elif (S[i] == '0'):
            C = C + (C1 - B1)

        # Case 1
    ans = C * K

    # Case 2

    ans += (C1 * C0 * (((K) * (K - 1)) // 2))

    # Return the total count
    return ans

# Driver Code
if __name__ == "__main__":

    S = "230013110087"
    K = 2
    N = len(S)

    print(countSubsequence(S, N, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

    // Function to calculate the number of
    // subsequences of "01"
    static int countSubsequence(string S, int N, int K)
    {

        // Store count of 0's and 1's
        int C = 0, C1 = 0, C0 = 0;

        for (int i = 0; i < N; i++) {
            if (S[i] == '1')
                C1++;
            else if (S[i] == '0')
                C0++;
        }

        // Count of subsequences without
        // concatenation
        int B1 = 0;
        for (int i = 0; i < N; i++) {
            if (S[i] == '1')
                B1++;
            else if (S[i] == '0')
                C = C + (C1 - B1);
        }

        // Case 1
        int ans = C * K;

        // Case 2
        ans += (C1 * C0 * (((K) * (K - 1)) / 2));

        // Return the total count
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        string S = "230013110087";
        int K = 2;
        int N = S.Length;

        Console.Write(countSubsequence(S, N, K));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate the number of
// subsequences of "01"
function countSubsequence(S, N, K) {
  // Store count of 0's and 1's
  let C = 0,
    C1 = 0,
    C0 = 0;

  for (let i = 0; i < N; i++) {
    if (S[i] == "1") C1++;
    else if (S[i] == "0") C0++;
  }

  // Count of subsequences without
  // concatenation
  let B1 = 0;
  for (let i = 0; i < N; i++) {
    if (S[i] == "1") B1++;
    else if (S[i] == "0") C = C + (C1 - B1);
  }

  // Case 1
  let ans = C * K;

  // Case 2
  ans += C1 * C0 * ((K * (K - 1)) / 2);

  // Return the total count
  return ans;
}

// Driver Code

let S = "230013110087";
let K = 2;
let N = S.length;

document.write(countSubsequence(S, N, K));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
24
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
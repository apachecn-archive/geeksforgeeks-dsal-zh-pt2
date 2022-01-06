# 大小不超过 N 的回文串计数，由最多出现两次的前 K 个字母组成

> 原文:[https://www . geeksforgeeks . org/count-of-the-of-the-of-the-of-the-of-first-k-alphabets-最多出现两次/](https://www.geeksforgeeks.org/count-of-palindromic-strings-of-size-upto-n-consisting-of-first-k-alphabets-occurring-at-most-twice/)

给定两个整数 **N** 和 **K** ，任务是找到大小为**的回文串的[号，最多 N](https://www.geeksforgeeks.org/number-of-palindromic-permutations-set-1/)** 个，由第一个 **K** 个小写字母组成，这样一个串中的每个字符出现不超过两次。

**示例:**

> **输入:** N = 3，K = 2
> **输出:** 6
> **解释:**
> 可能的字符串有:
> “a”、“b”、“aa”、“bb”、“aba”、“bab”。
> 
> **输入:** N = 4，K = 3
> **输出:** 18
> **解释:**
> 可能的字符串有:
> “a”“b”“c”“aa”“bb”“cc”“ABA”“ACA”“Bab”“BCB”“CAC”“CBC”“ABBA”“acca”“baab”“bccb”“CAAC”“cbbc”。

**方法:**给定的问题可以基于以下观察来解决:

*   让我们尝试构建一个只有前 3 个英文字母( **K = 3** )的 4 位回文( **N = 4** )。因此，我们的想法是创建一个空字符串( **_ _ _ _** )，现在要从中获得一个回文，只能填充一半中的一个中的两位数字，因为其他两位将根据它们来决定，也就是说，如果选择前两个位置来填充所选的字符，那么最后两位将是相同的，因此该字符串应该是回文。
*   在这种情况下，如果第一个位置填充了 **a** ，第二个位置填充了 **b** ，那么第三个和第四个位置剩下的唯一选择就是分别填充 **b** 和 **a** 。
*   所以这意味着，要找出长度为 4 ( **N = 4** )且只有前 3 个字母( **K = 3** )的回文串的数量，统计前 2 位数字(= **N/2** )的所有可能组合，即 **3*2=6** (第一个位置 3 个选择，第二个位置 2 个选择)。
*   上面解释的情况是对于偶数长度的字符串( **N 是偶数**)，对于奇数长度的字符串( **N 是奇数**)， **N/2 + 1** 索引可以填充。

按照以下步骤解决给定的问题:

1.  求长度**最多 N 个**的计数回文串，然后从 **1 到 N 个**对每个长度的回文串进行计数，然后相加。
2.  对于 **N** 的值为:
    *   如果 N 是偶数，那么找到所有可能的组合直到 **N/2** ，因为只有一半的位置可以填充。
    *   如果 N 是奇数，则查找所有可能的组合，直到 **N/2 +1** ，并且元素的 **extra + 1** 作为中间元素。
3.  将它们全部加在一起，并相应地打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function of return the number of
// palindromic strings of length N with
// first K alphabets possible
int lengthNPalindrome(int N, int K)
{
    int half = N / 2;

    // If N is odd, half + 1 position
    // can be filled to cope with the
    // extra middle element
    if (N & 1) {
        half += 1;
    }

    int ans = 1;
    for (int i = 1; i <= half; i++) {
        ans *= K;

        // K is reduced by one, because
        // count of choices for the next
        // position is  reduced by 1 as
        // a element can only once
        K--;
    }

    // Return the possible count
    return ans;
}

// Function to find the count of palindromic
// string of first K characters according
// to the given criteria
int palindromicStrings(int N, int K)
{
    // If N=1, then only K palindromic
    // strings possible.
    if (N == 1) {
        return K;
    }

    // If N=2, the 2*K palindromic strings
    // possible, K for N=1 and K for N=2
    if (N == 2) {
        return 2 * K;
    }

    int ans = 0;

    // Initialize ans with the count of
    // strings possible till N = 2
    ans += (2 * K);

    for (int i = 3; i <= N; i++) {
        ans += lengthNPalindrome(i, K);
    }

    // Return the possible count
    return ans;
}

// Driver Code
int main()
{
    int N = 4, K = 3;
    cout << palindromicStrings(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    // Function of return the number of
    // palindromic strings of length N with
    // first K alphabets possible
    static int lengthNPalindrome(int N, int K)
    {
        int half = N / 2;

        // If N is odd, half + 1 position
        // can be filled to cope with the
        // extra middle element
        if (N % 2 == 1) {
            half += 1;
        }

        int ans = 1;
        for (int i = 1; i <= half; i++) {
            ans *= K;

            // K is reduced by one, because
            // count of choices for the next
            // position is  reduced by 1 as
            // a element can only once
            K--;
        }

        // Return the possible count
        return ans;
    }

    // Function to find the count of palindromic
    // string of first K characters according
    // to the given criteria
    static int palindromicStrings(int N, int K)
    {
        // If N=1, then only K palindromic
        // strings possible.
        if (N == 1) {
            return K;
        }

        // If N=2, the 2*K palindromic strings
        // possible, K for N=1 and K for N=2
        if (N == 2) {
            return 2 * K;
        }

        int ans = 0;

        // Initialize ans with the count of
        // strings possible till N = 2
        ans += (2 * K);

        for (int i = 3; i <= N; i++) {
            ans += lengthNPalindrome(i, K);
        }

        // Return the possible count
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4, K = 3;

        System.out.println(palindromicStrings(N, K));
    }
}
// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function of return the number of
# palindromic strings of length N with
# first K alphabets possible
def lengthNPalindrome(N, K) :

    half = N // 2;

    # If N is odd, half + 1 position
    # can be filled to cope with the
    # extra middle element
    if (N & 1) :
        half += 1;

    ans = 1;
    for i in range(1, half + 1) :
        ans *= K;

        # K is reduced by one, because
        # count of choices for the next
        # position is  reduced by 1 as
        # a element can only once
        K -= 1;

    # Return the possible count
    return ans;

# Function to find the count of palindromic
# string of first K characters according
# to the given criteria
def palindromicStrings(N, K) :

    # If N=1, then only K palindromic
    # strings possible.
    if (N == 1) :
        return K;

    # If N=2, the 2*K palindromic strings
    # possible, K for N=1 and K for N=2
    if (N == 2) :
        return 2 * K;

    ans = 0;

    # Initialize ans with the count of
    # strings possible till N = 2
    ans += (2 * K);

    for i in range(3, N + 1) :
        ans += lengthNPalindrome(i, K);

    # Return the possible count
    return ans;

# Driver Code
if __name__ == "__main__" :

    N = 4; K = 3;
    print(palindromicStrings(N, K));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function of return the number of
    // palindromic strings of length N with
    // first K alphabets possible
    static int lengthNPalindrome(int N, int K)
    {
        int half = N / 2;

        // If N is odd, half + 1 position
        // can be filled to cope with the
        // extra middle element
        if (N % 2 == 1) {
            half += 1;
        }

        int ans = 1;
        for (int i = 1; i <= half; i++) {
            ans *= K;

            // K is reduced by one, because
            // count of choices for the next
            // position is  reduced by 1 as
            // a element can only once
            K--;
        }

        // Return the possible count
        return ans;
    }

    // Function to find the count of palindromic
    // string of first K characters according
    // to the given criteria
    static int palindromicStrings(int N, int K)
    {
        // If N=1, then only K palindromic
        // strings possible.
        if (N == 1) {
            return K;
        }

        // If N=2, the 2*K palindromic strings
        // possible, K for N=1 and K for N=2
        if (N == 2) {
            return 2 * K;
        }

        int ans = 0;

        // Initialize ans with the count of
        // strings possible till N = 2
        ans += (2 * K);

        for (int i = 3; i <= N; i++) {
            ans += lengthNPalindrome(i, K);
        }

        // Return the possible count
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 4, K = 3;

        Console.Write(palindromicStrings(N, K));
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function of return the number of
// palindromic strings of length N with
// first K alphabets possible
function lengthNPalindrome(N,K)
{
    var half = N / 2;

    // If N is odd, half + 1 position
    // can be filled to cope with the
    // extra middle element
    if (N & 1) {
        half += 1;
    }

    var ans = 1;
    var i;
    for(i = 1; i <= half; i++) {
        ans *= K;

        // K is reduced by one, because
        // count of choices for the next
        // position is  reduced by 1 as
        // a element can only once
        K--;
    }

    // Return the possible count
    return ans;
}

// Function to find the count of palindromic
// string of first K characters according
// to the given criteria
function palindromicStrings(N, K)
{
    // If N=1, then only K palindromic
    // strings possible.
    if (N == 1) {
        return K;
    }

    // If N=2, the 2*K palindromic strings
    // possible, K for N=1 and K for N=2
    if (N == 2) {
        return 2 * K;
    }

    ans = 0;

    // Initialize ans with the count of
    // strings possible till N = 2
    ans += (2 * K);

    for (i = 3; i <= N; i++) {
        ans += lengthNPalindrome(i, K);
    }

    // Return the possible count
    return ans;
}

// Driver Code
    var N = 4, K = 3;
    document.write(palindromicStrings(N, K));

// This code is contributed by ipg2016107.
</script>
```

**Output:** 

```
18
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
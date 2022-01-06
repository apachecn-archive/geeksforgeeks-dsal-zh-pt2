# 可通过串联等长前缀和子串获得的回文计数

> 原文:[https://www . geeksforgeeks . org/可通过串联等长前缀和子字符串获得的回文计数/](https://www.geeksforgeeks.org/count-of-palindromes-that-can-be-obtained-by-concatenating-equal-length-prefix-and-substrings/)

**先决条件:** [Z 算法](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是在执行给定的步骤后找到可以形成的回文的最大数量:

1.  选择长度相等的非空前缀 **P** 和非空子串 **T** 。
2.  反转 **P** 或 **T** 并连接它们。

**注意:** P 和 T 可以重叠。

**示例:**

> **输入:** S = "abab"
> **输出** : 6
> **解释:**
> 将前缀视为 **S[0 : 1]** (= " **ab** ")并反转子串 **S[2 : 3]** 。将前缀和反向子串串联后的结果串是**“ABBA”**，是回文。
> 所有可能的前缀都是**【“a”、“ab”、“aba”、“abab”】**。
> 所有可能的后缀都是**[“a”、“b”、“a”、“b”、“ab”、“ba”、“ab”、“aba”、“bab”、“abab”]**。
> 因此，所有可能的回文都是**【“aa”“aa”“ABBA”“ABBA”“abaababa”“ababbaba”】**。
> 
> **输入:**S = " ABCD "
> T3】输出: 4

**天真方法:**生成所有可能的前缀和[所有可能的子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)。连接所有等长前缀和子串(反转后)对，[检查得到的字符串是否是回文](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**上述方法可以基于串联串的长度将总是偶数的观察来优化。因此，只需要考虑前半部分是后半部分镜像的那些字符串。因此，问题简化为计算每个可能前缀的子串，这些子串等于该前缀，这可以使用 [Z 函数](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)来完成。

> 字符串上的 [z 函数](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)将返回一个数组 **Z[]** ，其中 **Z[i]** 表示最长前缀的长度，该长度与子字符串相同，从位置 **i** 开始，到位置 **i+Z[i]** 结束。因此，计数将为![\sum Z[i]+1              ](img/6990049c3ebf67f5b214713f79dcd413.png "Rendered by QuickLaTeX.com")。

按照以下步骤解决问题:

1.  其思想是保持一个区间**【l，r】**，该区间是具有 max **r** 的区间，使得**【l，r】**是前缀子串(子串也是前缀)。
2.  如果 **i ≤ r** ，则 **Z[i]** 等于**r–I+1**和**Z[I–1]的最小值。**
3.  现在，递增 **Z[i]** 直到 **i + Z[i]** 小于 **N** 并且在给定字符串中索引 **Z[i]** 和 **i + Z[i]** 处的字符相等。
4.  现在，如果**I+Z[I]–1>r**，则将 **l** 设置为 **i** ，将 **r** 设置为**I+Z[I]–1**。
5.  对从 **0** 到 **N-1** 的 **i** 重复上述步骤。
6.  答案是每个**I**T4【0≤I≤N-1)的**Z【I】+1**之和。

下面是上述方法的实现:

## C++14

```
// C++ program the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// number of palindromes
int countPalindromes(string S)
{
    int N = (int)S.length();
    vector<int> Z(N);

    // Calculation of Z-array
    int l = 0, r = 0;
    for (int i = 1; i < N; i++) {

        if (i <= r)
            Z[i] = min(r - i + 1, Z[i - l]);

        while (i + Z[i] < N
               && S[Z[i]] == S[i + Z[i]]) {
            Z[i]++;
        }

        if (i + Z[i] - 1 > r) {

            l = i;
            r = i + Z[i] - 1;
        }
    }

    // Calculation of sigma(Z[i]+1)
    int sum = 0;
    for (int i = 0; i < Z.size(); i++) {
        sum += Z[i] + 1;
    }

    // Return the count
    return sum;
}

// Driver Code
int main()
{
    // Given String
    string S = "abab";
    cout << countPalindromes(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
import java.util.*;

class GFG{

// Function to calculate the
// number of palindromes
static int countPalindromes(String S)
{
    int N = (int)S.length();
    int[] Z = new int[(N)];

    // Calculation of Z-array
    int l = 0, r = 0;

    for(int i = 1; i < N; i++)
    {
        if (i <= r)
            Z[i] = Math.min(r - i + 1,
                              Z[i - l]);

        while (i + Z[i] < N &&
               S.charAt(Z[i]) ==
               S.charAt(i + Z[i]))
        {
            Z[i]++;
        }

        if (i + Z[i] - 1 > r)
        {
            l = i;
            r = i + Z[i] - 1;
        }
    }

    // Calculation of sigma(Z[i]+1)
    int sum = 0;

    for(int i = 0; i < Z.length; i++)
    {
        sum += Z[i] + 1;
    }

    // Return the count
    return sum;
}

// Driver Code   
public static void main (String[] args)   
{ 

    // Given String
    String S = "abab";

    System.out.println(countPalindromes(S));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program the above approach

# Function to calculate the
# number of palindromes
def countPalindrome(S):
    N = len(S)
    Z = [0] * N

    # Calculation of Z-array
    l = 0
    r = 0
    for i in range(1, N):
        if i <= r:
            Z[i] = min(r - i + 1, Z[i - 1])
        while((i + Z[i]) < N and (S[Z[i]] == S[i + Z[i]])):
            Z[i] += 1
        if ((i + Z[i] - 1) > r):
            l = ir = i + Z[i] - 1

    # Calculation of sigma(Z[i]+1)
    sum = 0
    for i in range(0, len(Z)):
        sum += Z[i] + 1

    # return the count
    return sum

# Driver code

# Given String
S = "abab"
print(countPalindrome(S))

# This code is contributed by virusbuddah
```

## C#

```
// C# program for the above approach 
using System;

public class GFG{

// Function to calculate the
// number of palindromes
static int countPalindromes(String S)
{
    int N = (int)S.Length;
    int[] Z = new int[(N)];

    // Calculation of Z-array
    int l = 0, r = 0;

    for(int i = 1; i < N; i++)
    {
        if (i <= r)
            Z[i] = Math.Min(r - i + 1,
                              Z[i - l]);
        while (i + Z[i] < N &&
               S[Z[i]] ==
               S[i + Z[i]])
        {
            Z[i]++;
        }

        if (i + Z[i] - 1 > r)
        {
            l = i;
            r = i + Z[i] - 1;
        }
    }

    // Calculation of sigma(Z[i]+1)
    int sum = 0;

    for(int i = 0; i < Z.Length; i++)
    {
        sum += Z[i] + 1;
    }

    // Return the count
    return sum;
}

// Driver Code   
public static void Main(String[] args)   
{ 

    // Given String
    String S = "abab";

    Console.WriteLine(countPalindromes(S));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program the above approach

// Function to calculate the
// number of palindromes
function countPalindromes(S)
{
    var N = S.length;
    var Z = Array(N).fill(0);

    // Calculation of Z-array
    var l = 0, r = 0;
    for (var i = 1; i < N; i++) {

        if (i <= r)
            Z[i] = Math.min(r - i + 1, Z[i - l]);

        while (i + Z[i] < N
            && S[Z[i]] == S[i + Z[i]]) {
            Z[i]++;
        }

        if (i + Z[i] - 1 > r) {

            l = i;
            r = i + Z[i] - 1;
        }
    }

    // Calculation of sigma(Z[i]+1)
    var sum = 0;
    for (var i = 0; i < Z.length; i++) {
        sum += Z[i] + 1;
    }

    // Return the count
    return sum;
}

// Driver Code
// Given String
var S = "abab";
document.write( countPalindromes(S));

</script>
```

**Output:** 

```
6
```

***时间复杂度:*** O(N)
***辅助空间:*** O(N)
# 不是给定字符串子序列的字典最小字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小字符串不是给定字符串的子序列/](https://www.geeksforgeeks.org/lexicographically-smallest-string-which-is-not-a-subsequence-of-given-string/)

给定一个字符串 **S** ，任务是找到字典上最小的字符串，而不是给定字符串 **S** 的子序列。

**示例:**

> **输入:**S = " abcdefghijklmnopqrstuvwxyz "
> **输出:**
> aa
> **解释:**
> 字符串“aa”是字典上最小的字符串，它不作为子序列出现在给定的字符串中。
> 
> **输入:** S = "aaaa"
> **输出:**
> aaab
> **解释:**
> 字符串“aaa”是字典上最小的字符串，它不作为子序列出现在给定的字符串中。

**方法:**解决给定问题的思路是[找到给定字符串中字符](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/)**‘a’**(说 **f** )的频率。如果 **f** 的值小于字符串的[长度，那么答案将是将**‘a’****f+1**的次数串联成 **aaa 的字符串。(f+1 次)**将是所需的字典最小字符串，它不是子序列。否则，答案将是由字符串末尾的“**a”(f-1 次)**和**“b”**串联而成的字符串。](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to find lexicographically smallest string that
// is not a subsequence of S
string smallestNonSubsequence(string S, int N)
{
    // variable to store frequency of 'a'
    int freq = 0;
    // calculate frequency of 'a'
    for (int i = 0; i < N; i++)
        if (S[i] == 'a')
            freq++;
    // Initialize string consisting of freq number of 'a'
    string ans(freq, 'a');
    // change the last digit to 'b'
    if (freq == N)
        ans[freq - 1] = 'b';
    // add another 'a' to the string
    else
        ans += 'a';
    // return tha answer string
    return ans;
}
// Driver code
int main()
{
    // Input
    string S = "abcdefghijklmnopqrstuvwxyz";
    int N = S.length();

    // Function call
    cout << smallestNonSubsequence(S, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to find lexicographically smallest string that
// is not a subsequence of S
static String smallestNonSubsequence(String S, int N)
{

    // variable to store frequency of 'a'
    int freq = 0;

    // calculate frequency of 'a'
    for (int i = 0; i < N; i++)
        if (S.charAt(i) == 'a')
            freq++;

    // Initialize string consisting of freq number of 'a'
 String ans="";
    for(int i = 0; i < f req; i++){
        ans += 'a';
    }

    // change the last digit to 'b'
    if (freq == N)
       ans = ans.replace(ans.charAt(freq - 1), 'b');

    // add another 'a' to the string
    else
        ans += 'a';

    // return tha answer string
    return ans;
}

// Driver Code
public static void main(String args[])
{
    String S = "abcdefghijklmnopqrstuvwxyz";
    int N = S.length();

    // Function call
    System.out.println(smallestNonSubsequence(S, N));
    }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find lexicographically smallest
# string that is not a subsequence of S
def smallestNonSubsequence(S, N):

    # Variable to store frequency of 'a'
    freq = 0

    # Calculate frequency of 'a'
    for i in range(N):
        if (S[i] == 'a'):
            freq += 1

    # Initialize string consisting
    # of freq number of 'a'
    ans = ""
    for i in range(freq):
        ans += 'a'

    # Change the last digit to 'b'
    if (freq == N):
        ans = ans.replace(ans[freq - 1], 'b')

    # Add another 'a' to the string
    else:
        ans += 'a'

    # Return tha answer string
    return ans

# Driver code
if __name__ == '__main__':

    # Input
    S = "abcdefghijklmnopqrstuvwxyz"
    N = len(S)

    # Function call
    print(smallestNonSubsequence(S, N))

# This code is contributed by SURENDRA_GANGWAR
```

**Output**

```
aa
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
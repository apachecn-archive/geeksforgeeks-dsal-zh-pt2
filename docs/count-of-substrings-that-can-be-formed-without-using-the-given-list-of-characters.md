# 不使用给定的字符列表就可以形成的子字符串的数量

> 原文:[https://www . geeksforgeeks . org/不使用给定字符列表就能形成的子字符串计数/](https://www.geeksforgeeks.org/count-of-substrings-that-can-be-formed-without-using-the-given-list-of-characters/)

给定一个字符串 **str** 和一个字符列表 **L** ，任务是计算字符串 **str** 的[子字符串总数](https://www.geeksforgeeks.org/number-substrings-string/)，而不使用列表 **L** 中给定的字符。

**示例:**

> **输入:** str = "abcd "，L[] = {'a '，' b '，' t '，' q'}
> **输出:** 3
> **解释:**
> 在忽略给定字符串中的字符' a '和' b '时，会留下子字符串“cd”。
> 因此，“cd”由:
> (2 * (2 + 1)) / 2 = 3 构成的子串总数
> 
> **输入:** str = "abcpxyz "，L[] = {'a '，' p '，' q'}
> **输出:** 9
> **解释:**
> 在忽略给定字符串中的字符' a '和' p '时，会留下子字符串“bc”和“xyz”。
> 因此，子串构成的子串总数为:
> (2 *(2+1))/2+(3 *(3+1))/2 = 3+6 = 9

**方法:** [给定长度 N 的字符串的子字符串总数](https://www.geeksforgeeks.org/number-substrings-string/)由公式给出

```
(N * (N + 1)) / 2
```

想法是使用上面的公式并按照下面的步骤计算答案:

1.  逐字符遍历字符串**字符串**。
2.  计算在列表 L 中找不到字符的字符数。让计数为 **N**
3.  一旦遇到来自 **L** 的字符，计算 **(N * (N + 1) / 2)** 并将其添加到**答案**中，并将计数 N 重置为零。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Number of sub-strings
// without using given character
int countSubstring(string& S, char L[], int& n)
{
    int freq[26] = { 0 }, ans = 0;

    // Mark the given characters in
    // the freq array
    for (int i = 0; i < n; i++) {
        freq[(int)(L[i] - 'a')] = 1;
    }

    // Count variable to store the count
    // of the characters until a character
    // from given L is encountered
    int count = 0;

    for (auto x : S) {

        // If a character from L is encountered,
        // then the answer variable is incremented by
        // the value obtained by using
        // the mentioned formula and count is set to 0
        if (freq[(int)(x - 'a')]) {
            ans += (count * count + count) / 2;
            count = 0;
        }
        else
            count++;
    }

    // For last remaining characters
    ans += (count * count + count) / 2;

    return ans;
}

// Driver code
int main()
{

    string S = "abcpxyz";
    char L[] = { 'a', 'p', 'q' };
    int n = sizeof(L) / sizeof(L[0]);

    cout << countSubstring(S, L, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to find the Number of sub-Strings
// without using given character
static int countSubString(char []S, char L[], int n)
{
    int []freq = new int[26];
    int ans = 0;

    // Mark the given characters in
    // the freq array
    for (int i = 0; i < n; i++)
    {
        freq[(int)(L[i] - 'a')] = 1;
    }

    // Count variable to store the count
    // of the characters until a character
    // from given L is encountered
    int count = 0;

    for (int x : S)
    {

        // If a character from L is encountered,
        // then the answer variable is incremented by
        // the value obtained by using
        // the mentioned formula and count is set to 0
        if (freq[(int)(x - 'a')] > 0)
        {
            ans += (count * count + count) / 2;
            count = 0;
        }
        else
            count++;
    }

    // For last remaining characters
    ans += (count * count + count) / 2;

    return ans;
}

// Driver code
public static void main(String[] args)
{
    String S = "abcpxyz";
    char L[] = { 'a', 'p', 'q' };
    int n = L.length;

    System.out.print(countSubString(S.toCharArray(), L, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the Number of sub-strings
# without using given character
def countSubstring(S, L,n):
    freq = [0 for i in range(26)]

    # the freq array
    for i in range(n):
        freq[(ord(L[i]) - ord('a'))] = 1

    # Count variable to store the count
    # of the characters until a character
    # from given L is encountered
    count,ans = 0,0

    for x in S:

        # If a character from L is encountered,
        # then the answer variable is incremented by
        # the value obtained by using
        # the mentioned formula and count is set to 0
        if (freq[ord(x) - ord('a')]):
            ans += (count * count + count) // 2
            count = 0
        else:
            count += 1

    # For last remaining characters
    ans += (count * count + count) // 2

    return ans

# Driver code

S = "abcpxyz"
L = ['a', 'p', 'q']
n = len(L)

print(countSubstring(S, L, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to find the Number of sub-Strings
    // without using given character
    static int countSubString(char []S, char []L, int n)
    {
        int []freq = new int[26];
        int ans = 0;

        // Mark the given characters in
        // the freq array
        for (int i = 0; i < n; i++)
        {
            freq[(int)(L[i] - 'a')] = 1;
        }

        // Count variable to store the count
        // of the characters until a character
        // from given L is encountered
        int count = 0;

        foreach (int x in S)
        {

            // If a character from L is encountered,
            // then the answer variable is incremented by
            // the value obtained by using
            // the mentioned formula and count is set to 0
            if (freq[(int)(x - 'a')] > 0)
            {
                ans += (count * count + count) / 2;
                count = 0;
            }
            else
                count++;
        }

        // For last remaining characters
        ans += (count * count + count) / 2;

        return ans;
    }

    // Driver code
    public static void Main()
    {
        string S = "abcpxyz";
        char []L = { 'a', 'p', 'q' };
        int n = L.Length;

        Console.WriteLine(countSubString(S.ToCharArray(), L, n));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
      // JavaScript implementation of the above approach
      // Function to find the Number of sub-Strings
      // without using given character
      function countSubString(S, L, n) {
        var freq = new Array(26).fill(0);
        var ans = 0;

        // Mark the given characters in
        // the freq array
        for (var i = 0; i < n; i++) {
          freq[L[i].charCodeAt(0) - "a".charCodeAt(0)] = 1;
        }

        // Count variable to store the count
        // of the characters until a character
        // from given L is encountered
        var count = 0;

        for (const x of S) {
          // If a character from L is encountered,
          // then the answer variable is incremented by
          // the value obtained by using
          // the mentioned formula and count is set to 0
          if (freq[x.charCodeAt(0) - "a".charCodeAt(0)] > 0) {
            ans = ans + parseInt((count * count + count) / 2);
            count = 0;
          } else count++;
        }

        // For last remaining characters
        ans += parseInt((count * count + count) / 2);

        return ans;
      }

      // Driver code
      var S = "abcpxyz";
      var L = ["a", "p", "q"];
      var n = L.length;

      document.write(countSubString(S.split(""), L, n));
</script>
```

**Output:** 

```
9
```

时间复杂度:O(n + |S|)

辅助空间:O(26)
# 重复 A 的最小次数，使得 B 是它的子串

> 原文:[https://www . geesforgeks . org/a 必须重复的最小次数-b 是它的子串/](https://www.geeksforgeeks.org/minimum-number-of-times-a-has-to-be-repeated-such-that-b-is-a-substring-of-it/)

给定两根弦 **A** 和 **B** 。任务是找出 **A** 重复的最小次数，使得 **B** 是它的一个子串。如果没有这样的解决方案，打印 **-1** 。

**示例:**

> **输入:**A =“ABCD”，B =“cdabcdab”
> T3】输出: 3
> 重复 A 三次(“abcdabcd”)，B 是它的一个子串。重复次数少于 3 次的 b 不是 A 的子串。
> 
> **输入:** A = "ab "，B = "cab"
> **输出:** -1

**方法:**
假设我们写了**S = A+A+A+……**如果 **B** 是 **S** 的子串，我们只需要检查某个索引是 0 还是 1 还是……。长度(A) -1 以 **B** 开始，因为 **S** 足够长，可以容纳 **B** ， **S** 有一段**长度(A)** 。
现在，假设 **ans** 是**长度(B) < =长度(A * ans)** 的最小数。我们只需要检查 **B** 是 **A * ans** 还是 **A * (ans+1)** 的子串即可。如果我们尝试 **k < ans** ，那么 **B** 的长度比 **A * ans** 大，因此不能是子串。当 **k = ans+1** ， **A * k** 已经大到可以尝试**B**(**A【I:I+长度(B)】= = B**对于 i = 0，1，…，长度(A)–1)。

下面是上述方法的实现:

## C++14

```
// CPP program to find Minimum number of times A
// has to be repeated such that B is a substring of it
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is a substring of other or not
bool issubstring(string str2, string rep1)
{
    int M = str2.length();
    int N = rep1.length();

    // Check for substring from starting
    // from i'th index of main string
    for (int i = 0; i <= N - M; i++) {
        int j;

        // For current index i,
        // check for pattern match
        for (j = 0; j < M; j++)
            if (rep1[i + j] != str2[j])
                break;

        if (j == M) // pattern matched
            return true;
    }

    return false; // not a substring
}

// Function to find Minimum number of times A
// has to be repeated such that B is a substring of it
int Min_repetation(string A, string B)
{
    // To store minimum number of repetitions
    int ans = 1;

    // To store repeated string
    string S = A;

    // Until size of S is less than B
    while(S.size() < B.size())
    {
        S += A;
        ans++;
    }

    // ans times repetition makes required answer
    if (issubstring(B, S)) return ans;

    // Add one more string of A  
    if (issubstring(B, S+A))
        return ans + 1;

    // If no such solution exists   
    return -1;
}

// Driver code
int main()
{
    string A = "abcd", B = "cdabcdab";

    // Function call
    cout << Min_repetation(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of times 'A' has to be repeated
// such that 'B' is a substring of it
class GFG
{

// Function to check if a number
// is a substring of other or not
static boolean issubstring(String str2,
                           String rep1)
{
    int M = str2.length();
    int N = rep1.length();

    // Check for substring from starting
    // from i'th index of main string
    for (int i = 0; i <= N - M; i++)
    {
        int j;

        // For current index i,
        // check for pattern match
        for (j = 0; j < M; j++)
            if (rep1.charAt(i + j) != str2.charAt(j))
                break;

        if (j == M) // pattern matched
            return true;
    }

    return false; // not a substring
}

// Function to find Minimum number
// of times 'A' has to be repeated
// such that 'B' is a substring of it
static int Min_repetation(String A, String B)
{
    // To store minimum number of repetitions
    int ans = 1;

    // To store repeated string
    String S = A;

    // Until size of S is less than B
    while(S.length() < B.length())
    {
        S += A;
        ans++;
    }

    // ans times repetition makes required answer
    if (issubstring(B, S)) return ans;

    // Add one more string of A
    if (issubstring(B, S + A))
        return ans + 1;

    // If no such solution exists
    return -1;
}

// Driver code
public static void main(String[] args)
{
    String A = "abcd", B = "cdabcdab";

    // Function call
    System.out.println(Min_repetation(A, B));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find minimum number
# of times 'A' has to be repeated
# such that 'B' is a substring of it

# Method to find Minimum number
# of times 'A' has to be repeated
# such that 'B' is a substring of it
def min_repetitions(a, b):
    len_a = len(a)
    len_b = len(b)

    for i in range(0, len_a):

        if a[i] == b[0]:
            k = i
            count = 1
            for j in range(0, len_b):

                # we are reiterating over A again and
                # again for each value of B
                # Resetting A pointer back to 0 as B
                # is not empty yet
                if k >= len_a:
                    k = 0
                    count = count + 1

                # Resetting A means count
                # needs to be increased
                if a[k] != b[j]:
                    break
                k = k + 1

            # k is iterating over A
            else:
                return count
    return -1

# Driver Code
A = 'abcd'
B = 'cdabcdab'
print(min_repetitions(A, B))

# This code is contributed by satycool
```

## C#

```
// C# program to find minimum number
// of times 'A' has to be repeated
// such that 'B' is a substring of it
using System;

class GFG
{

// Function to check if a number
// is a substring of other or not
static Boolean issubstring(String str2,
                           String rep1)
{
    int M = str2.Length;
    int N = rep1.Length;

    // Check for substring from starting
    // from i'th index of main string
    for (int i = 0; i <= N - M; i++)
    {
        int j;

        // For current index i,
        // check for pattern match
        for (j = 0; j < M; j++)
            if (rep1[i + j] != str2[j])
                break;

        if (j == M) // pattern matched
            return true;
    }

    return false; // not a substring
}

// Function to find Minimum number
// of times 'A' has to be repeated
// such that 'B' is a substring of it
static int Min_repetation(String A, String B)
{
    // To store minimum number of repetitions
    int ans = 1;

    // To store repeated string
    String S = A;

    // Until size of S is less than B
    while(S.Length < B.Length)
    {
        S += A;
        ans++;
    }

    // ans times repetition makes required answer
    if (issubstring(B, S)) return ans;

    // Add one more string of A
    if (issubstring(B, S + A))
        return ans + 1;

    // If no such solution exists
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    String A = "abcd", B = "cdabcdab";

    // Function call
    Console.WriteLine(Min_repetation(A, B));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find Minimum number of times A
// has to be repeated such that B is a substring of it

// Function to check if a number
// is a substring of other or not
function issubstring(str2, rep1)
{
    var M = str2.length;
    var N = rep1.length;

    // Check for substring from starting
    // from i'th index of main string
    for (var i = 0; i <= N - M; i++) {
        var j;

        // For current index i,
        // check for pattern match
        for (j = 0; j < M; j++)
            if (rep1[i + j] != str2[j])
                break;

        if (j == M) // pattern matched
            return true;
    }

    return false; // not a substring
}

// Function to find Minimum number of times A
// has to be repeated such that B is a substring of it
function Min_repetation(A, B)
{
    // To store minimum number of repetitions
    var ans = 1;

    // To store repeated string
    var S = A;

    // Until size of S is less than B
    while(S.length < B.length)
    {
        S += A;
        ans++;
    }

    // ans times repetition makes required answer
    if (issubstring(B, S))
        return ans;

    // Add one more string of A  
    if (issubstring(B, S+A))
        return ans + 1;

    // If no such solution exists   
    return -1;
}

// Driver code
var A = "abcd", B = "cdabcdab";

// Function call
document.write( Min_repetation(A, B));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N * M)
T3】辅助空间 : O(1)。

**方法 2:**

这里的想法是尝试使用强力字符串搜索算法(n * m)来查找字符串。这里唯一的区别是计算当计数器到达字符串末尾时的模数(i % n)。

## C++

```
#include <bits/stdc++.h>
using namespace std;

int repeatedStringMatch(string A, string B)
{
    int m = A.length();
    int n = B.length();

    int count;
    bool found = false;

    for (int i = 0; i < m; i++) {
        int j = i;
        int k = 0;
        count = 1;

        while (k < n && A[j] == B[k]) {
            if (k == n - 1) {
                found = true;
                break;
            }
            j = (j + 1) % m;

            if (j == 0)
                count++;

            k++;
        }
        if (found)
            return count;
    }
    return -1;
}
int main()
{
    string A = "abcd";
    string B = "cdabcdab";

    cout << repeatedStringMatch(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    static int repeatedStringMatch(String A, String B)
    {
        int m = A.length();
        int n = B.length();

        int count;
        boolean found = false;

        for (int i = 0; i < m; ++i) {
            int j = i;

            int k = 0;

            count = 1;

            while (k < n && A.charAt(j) == B.charAt(k)) {

                if (k == n - 1) {
                    found = true;
                    break;
                }

                j = (j + 1) % m;

                // if j = 0, it means we have repeated the
                // string
                if (j == 0)
                    ++count;

                k += 1;
            }

            if (found)
                return count;
        }

        return -1;
    }
    public static void main(String[] args)
    {

        String A = "abcd", B = "cdabcdab";

        // Function call
        System.out.println(repeatedStringMatch(A, B));
    }
}
```

**时间复杂度:O(N * M)**

**辅助空间:O(1)。**
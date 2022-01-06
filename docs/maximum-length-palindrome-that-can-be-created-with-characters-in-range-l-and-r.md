# 可以用范围为 L 和 R 的字符创建的最大长度回文

> 原文:[https://www . geeksforgeeks . org/最大长度-可以用范围内的字符创建的回文-l 和-r/](https://www.geeksforgeeks.org/maximum-length-palindrome-that-can-be-created-with-characters-in-range-l-and-r/)

给定一个字符串**字符串**和 **Q** 查询。每个查询由两个数字组成 **L** 和 **R** 。任务是找到**【L，R】**范围内字符可以创建的最大长度回文。
**举例:**

> **输入:** str = "amim "，Q[] = {{1，4}，{3，4}
> **输出:**
> 3
> 1
> 在范围[1，4]内，只能形成两个回文“mam”和“mim”。
> 在范围[3，4]中，只能使用范围内的字符创建“I”或“m”。
> **输入:**str = " AAAA "，Q[] = {{1，5}，{5，5}
> **输出:**
> 5
> 1

**方法:**让**前缀【I】【j】**是一个数组，表示字符 **char(j+97)** 在 1 到 I 的范围内的频率，对于 L 到 R 的任何范围，计算偶数频率和奇数频率。因为奇数-1 是偶数，所以它也可以对回文串有贡献。还要为奇数频率的字符保留一个标记，可以插入中间。因此，最长回文的长度可能是所有偶数频率和奇数-1 频率之和，如果存在任何奇数频率字符，则加 1。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 4

// Function to return the length of the
// longest palindrome that can be formed
// using the characters in the range [l, r]
int performQueries(int l, int r, int prefix[N][26])
{

    // 0-based indexing
    l--;
    r--;

    // Marks if there is an
    // odd frequency character
    bool flag = false;

    // Length of the longest palindrome
    // possible from characters in range
    int count = 0;

    // Traverse for all characters
    // and count their frequencies
    for (int i = 0; i < 26; i++) {

        // Find the frequency in range 1 - r
        int cnt = prefix[r][i];

        // Exclude the frequencies in range 1 - (l - 1)
        if (l > 0)
            cnt -= prefix[l - 1][i];

        // If frequency is odd, then add 1 less than
        // the original frequency to make it even
        if (cnt % 2 == 1) {
            flag = true;
            count += cnt - 1;
        }
        // Else completely add if even
        else
            count += cnt;
    }

    // If any odd frequency character
    // is present then add 1
    if (flag)
        count += 1;

    return count;
}

// Function to pre-calculate the frequencies
// of the characters to reduce complexity
void preCalculate(string s, int prefix[N][26])
{
    int n = s.size();

    // Iterate and increase the count
    for (int i = 0; i < n; i++) {
        prefix[i][s[i] - 'a']++;
    }

    // Create a prefix type array
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < 26; j++)
            prefix[i][j] += prefix[i - 1][j];
    }
}

// Driver code
int main()
{
    string s = "amim";

    // Pre-calculate prefix array
    int prefix[N][26];
    memset(prefix, 0, sizeof prefix);
    preCalculate(s, prefix);

    int queries[][2] = { { 1, 4 }, { 3, 4 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Perform queries
    for (int i = 0; i < q; i++) {
        cout << performQueries(queries[i][0],
                               queries[i][1], prefix)
             << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int N = 4 ;

// Function to return the length of the
// longest palindrome that can be formed
// using the characters in the range [l, r]
static int performQueries(int l, int r, int prefix[][])
{

    // 0-based indexing
    l--;
    r--;

    // Marks if there is an
    // odd frequency character
    boolean flag = false;

    // Length of the longest palindrome
    // possible from characters in range
    int count = 0;

    // Traverse for all characters
    // and count their frequencies
    for (int i = 0; i < 26; i++)
    {

        // Find the frequency in range 1 - r
        int cnt = prefix[r][i];

        // Exclude the frequencies in range 1 - (l - 1)
        if (l > 0)
            cnt -= prefix[l - 1][i];

        // If frequency is odd, then add 1 less than
        // the original frequency to make it even
        if (cnt % 2 == 1)
        {
            flag = true;
            count += cnt - 1;
        }

        // Else completely add if even
        else
            count += cnt;
    }

    // If any odd frequency character
    // is present then add 1
    if (flag)
        count += 1;

    return count;
}

// Function to pre-calculate the frequencies
// of the characters to reduce complexity
static void preCalculate(String s, int prefix[][])
{
    int n = s.length();

    // Iterate and increase the count
    for (int i = 0; i < n; i++)
    {
        prefix[i][s.charAt(i) - 'a']++;
    }

    // Create a prefix type array
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j < 26; j++)
            prefix[i][j] += prefix[i - 1][j];
    }
}

// Driver code
public static void main(String args[])
{
    String s = "amim";

    // Pre-calculate prefix array
    int prefix[][] = new int[N][26];
    preCalculate(s, prefix);

    int queries[][] = { { 1, 4 }, { 3, 4 } };
    int q = queries.length;

    // Perform queries
    for (int i = 0; i < q; i++)
    {
        System.out.println( performQueries(queries[i][0],
                            queries[i][1], prefix) );
    }
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 4

# Function to return the length of the
# longest palindrome that can be formed
# using the characters in the range [l, r]
def performQueries(l, r, prefix):

    # 0-based indexing
    l -= 1
    r -= 1

    # Marks if there is an
    # odd frequency character
    flag = False

    # Length of the longest palindrome
    # possible from characters in range
    count = 0

    # Traverse for all characters
    # and count their frequencies
    for i in range(26):

        # Find the frequency in range 1 - r
        cnt = prefix[r][i]

        # Exclude the frequencies in range 1 - (l - 1)
        if (l > 0):
            cnt -= prefix[l - 1][i]

        # If frequency is odd, then add 1 less than
        # the original frequency to make it even
        if (cnt % 2 == 1):
            flag = True
            count += cnt - 1

        # Else completely add if even
        else:
            count += cnt

    # If any odd frequency character
    # is present then add 1
    if (flag):
        count += 1

    return count

# Function to pre-calculate the frequencies
# of the characters to reduce complexity
def preCalculate(s, prefix):

    n = len(s)

    # Iterate and increase the count
    for i in range(n):
        prefix[i][ord(s[i]) - ord('a')] += 1

    # Create a prefix type array
    for i in range(1, n):
        for j in range(26):
            prefix[i][j] += prefix[i - 1][j]

# Driver code
s = "amim"

# Pre-calculate prefix array
prefix = [[0 for i in range(26)]
             for i in range(N)]

preCalculate(s, prefix)

queries = [[1, 4] , [3, 4]]
q = len(queries)

# Perform queries
for i in range(q):
    print(performQueries(queries[i][0],
                         queries[i][1],
                         prefix))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N = 4 ;

// Function to return the length of the
// longest palindrome that can be formed
// using the characters in the range [l, r]
static int performQueries(int l, int r, int[,] prefix)
{

    // 0-based indexing
    l--;
    r--;

    // Marks if there is an
    // odd frequency character
    bool flag = false;

    // Length of the longest palindrome
    // possible from characters in range
    int count = 0;

    // Traverse for all characters
    // and count their frequencies
    for (int i = 0; i < 26; i++)
    {

        // Find the frequency in range 1 - r
        int cnt = prefix[r, i];

        // Exclude the frequencies in range 1 - (l - 1)
        if (l > 0)
            cnt -= prefix[l - 1, i];

        // If frequency is odd, then add 1 less than
        // the original frequency to make it even
        if (cnt % 2 == 1)
        {
            flag = true;
            count += cnt - 1;
        }

        // Else completely add if even
        else
            count += cnt;
    }

    // If any odd frequency character
    // is present then add 1
    if (flag)
        count += 1;

    return count;
}

// Function to pre-calculate the frequencies
// of the characters to reduce complexity
static void preCalculate(string s, int[,] prefix)
{
    int n = s.Length;

    // Iterate and increase the count
    for (int i = 0; i < n; i++)
    {
        prefix[i, s[i] - 'a']++;
    }

    // Create a prefix type array
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j < 26; j++)
            prefix[i, j] += prefix[i - 1, j];
    }
}

// Driver code
public static void Main()
{
    string s = "amim";

    // Pre-calculate prefix array
    int[,] prefix = new int[N, 26];
    preCalculate(s, prefix);

    int[,] queries = { { 1, 4 }, { 3, 4 } };
    int q = queries.Length;

    // Perform queries
    for (int i = 0; i < q; i++)
    {
        Console.WriteLine( performQueries(queries[i, 0],
                            queries[i, 1], prefix) );
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
let N = 4 ;

// Function to return the length of the
// longest palindrome that can be formed
// using the characters in the range [l, r]
function performQueries(l, r, prefix)
{

    // 0-based indexing
    l--;
    r--;

    // Marks if there is an
    // odd frequency character
    let flag = false;

    // Length of the longest palindrome
    // possible from characters in range
    let count = 0;

    // Traverse for all characters
    // and count their frequencies
    for (let i = 0; i < 26; i++)
    {

        // Find the frequency in range 1 - r
        let cnt = prefix[r][i];

        // Exclude the frequencies in range 1 - (l - 1)
        if (l > 0)
            cnt -= prefix[l - 1][i];

        // If frequency is odd, then add 1 less than
        // the original frequency to make it even
        if (cnt % 2 == 1)
        {
            flag = true;
            count += cnt - 1;
        }

        // Else completely add if even
        else
            count += cnt;
    }

    // If any odd frequency character
    // is present then add 1
    if (flag)
        count += 1;

    return count;
}

// Function to pre-calculate the frequencies
// of the characters to reduce complexity
function preCalculate(s,prefix)
{
    let n = s.length;

    // Iterate and increase the count
    for (let i = 0; i < n; i++)
    {
        prefix[i][s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    // Create a prefix type array
    for (let i = 1; i < n; i++)
    {
        for (let j = 0; j < 26; j++)
            prefix[i][j] += prefix[i - 1][j];
    }
}

// Driver code
let s = "amim";

    // Pre-calculate prefix array
    let prefix = new Array(N);
    for(let i = 0; i < 26; i++)
    {
        prefix[i] = new Array(26);
        for(let j = 0; j < 26; j++)
        {
            prefix[i][j] = 0;
        }
    }
    preCalculate(s, prefix);

    let queries = [[ 1, 4 ], [ 3, 4 ]];
    let q = queries.length;

    // Perform queries
    for (let i = 0; i < q; i++)
    {
        document.write( performQueries(queries[i][0],
                            queries[i][1], prefix) +"<br>");
    }

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
1
```
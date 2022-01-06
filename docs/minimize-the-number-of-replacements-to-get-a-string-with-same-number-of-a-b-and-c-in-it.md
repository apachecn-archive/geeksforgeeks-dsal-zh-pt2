# 尽量减少替换次数，得到一个“a”、“b”和“c”数量相同的字符串

> 原文:[https://www . geesforgeks . org/最小化替换次数以获得相同数量的 a-b 和 c-in-it/](https://www.geeksforgeeks.org/minimize-the-number-of-replacements-to-get-a-string-with-same-number-of-a-b-and-c-in-it/)

给定一个仅由三个可能的字符“a”、“b”或“c”组成的字符串。任务是用' a '，' b '或' c '替换给定字符串的字符，使得字符串中的' a '，' b '和' c '字符数量相等。任务是最大限度地减少替换的次数，并以最少的替换打印所有这类字符串中字典序上最小的字符串。

如果无法获得这样的字符串，请打印-1。

**例:**

```
Input : s = "bcabba"
Output : bcabca
Number of replacements done is 1 and this is
the lexicographically smallest possible 

Input : "aaaaaa"
Output : aabbcc

Input : "aaaaa"
Output : -1

```

**进场:**

*   计算字符串中“a”、“b”和“c”的数量。
*   如果它们的计数相等，那么相同的字符串将是答案。
*   如果字符串的长度不是 3 的倍数，则不可能。
*   首先，减少字符串中超过 a 的次数。
    1.  如果有额外的“c ”,用“a”替换“c ”,从左边开始使用滑动窗口技术。
    2.  如果索引处没有“c ”,则使用滑动窗口技术从左侧将“b”替换为“a”。
*   其次，通过使用滑动窗口从前面替换“c”，减少字符串中超过 b 的次数。
*   第三，通过使用滑动窗口减少后面额外“a”的数量来减少超过 c 的数量。
*   第四，通过减少后面额外“a”的数量来减少字符串中超过 b 的数量。
*   第五，通过减少后面额外的“b”来减少超过 c 的数量。

为了得到字典上最小的字符串，我们不断地从后面替换。

下面是上述方法的实现:

## c++

```
// CPP program to Minimize the number of
// replacements to get a string with same
// number of ‘a’, ‘b’ and ‘c’ in it

#include <bits/stdc++.h>
using namespace std;

// Function to count numbers
string lexoSmallest(string s, int n)
{
    // Count the number of 'a', 'b' and
    // 'c' in string
    int ca = 0, cb = 0, cc = 0;

    for (int i = 0; i < n; i++) {
        if (s[i] == 'a')
            ca++;
        else if (s[i] == 'b')
            cb++;
        else
            cc++;
    }

    // If equal previously
    if (ca == cb && cb == cc) {
        return s;
    }

    int cnt = n / 3;

    // If not a multiple of 3
    if (cnt * 3 != n) {
        return "-1";
    }

    int i = 0;

    // Increase the number of a's by
    // removing extra 'b' and ;c;
    while (ca < cnt && i < n) {

        // Check if it is 'b' and it more
        // than n/3
        if (s[i] == 'b' && cb > cnt) {
            cb--;
            s[i] = 'a';
            ca++;
        }

        // Check if it is 'c' and it
        // more than n/3
        else if (s[i] == 'c' && cc > cnt) {
            cc--;
            s[i] = 'a';
            ca++;
        }

        i++;
    }

    i = 0;

    // Increase the number of b's by
    // removing extra 'c'
    while (cb < cnt && i < n) {

        // Check if it is 'c' and it more
        // than n/3
        if (s[i] == 'c' && cc > cnt) {
            cc--;
            s[i] = '1';

            cb++;
        }
        i++;
    }

    i = n - 1;

    // Increase the number of c's from back
    while (cc < cnt && i >= 0) {

        // Check if it is 'a' and it more
        // than n/3
        if (s[i] == 'a' && ca > cnt) {
            ca--;
            s[i] = 'c';
            cc++;
        }

        i--;
    }

    i = n - 1;

    // Increase the number of b's from back
    while (cb < cnt && i >= 0) {

        // Check if it is 'a' and it more
        // than n/3
        if (s[i] == 'a' && ca > cnt) {
            ca--;
            s[i] = 'b';
            cb++;
        }

        i--;
    }

    i = n - 1;

    // Increase the number of c's from back
    while (cc < cnt && i >= 0) {

        // Check if it is 'b' and it more
        // than n/3
        if (s[i] == 'b' && cb > cnt) {
            cb--;
            s[i] = 'c';
            cc++;
        }

        i--;
    }

    return s;
}

// Driver Code
int main()
{
    string s = "aaaaaa";
    int n = s.size();

    cout << lexoSmallest(s, n);

    return 0;
}
```

## python 3

```
# Python3 program to Minimize the number of
# replacements to get a string with same
# number of 'a', 'b' and 'c' in it

# Function to count numbers
def lexoSmallest(s, n):

    # Count the number of 'a', 'b' and
    # 'c' in string
    ca = 0
    cb = 0
    cc = 0
    for i in range(n):
        if (s[i] == 'a'):
            ca += 1
        elif (s[i] == 'b'):
            cb += 1
        else:
            cc += 1

    # If equal previously
    if (ca == cb and cb == cc):
        return s

    cnt = n // 3

    # If not a multiple of 3
    if (cnt * 3 != n):
        return "-1"

    i = 0

    # Increase the number of a's by
    # removing extra 'b' and c
    while (ca < cnt and i < n):

        # Check if it is 'b' and it more
        # than n/3
        if (s[i] == 'b' and cb > cnt) :
            cb -= 1
            s[i] = 'a'
            ca += 1

        # Check if it is 'c' and it
        # more than n/3
        elif (s[i] == 'c' and cc > cnt):
            cc -= 1
            s[i] = 'a'
            ca += 1

        i += 1
    i = 0

    # Increase the number of b's by
    # removing extra 'c'
    while (cb < cnt and i < n):

        # Check if it is 'c' and it more
        # than n/3
        if (s[i] == 'c' and cc > cnt):
            cc -= 1
            s[i] = '1'
            cb += 1

        i += 1

    i = n - 1

    # Increase the number of c's from back
    while (cc < cnt and i >= 0):

        # Check if it is 'a' and it more
        # than n/3
        if (s[i] == 'a' and ca > cnt):
            ca -= 1
            s[i] = 'c'
            cc += 1

        i -= 1

    i = n - 1

    # Increase the number of b's from back
    while (cb < cnt and i >= 0):

        # Check if it is 'a' and it more
        # than n/3
        if (s[i] == 'a' and ca > cnt):
            ca -= 1
            s[i] = 'b'
            cb += 1

        i -= 1

    i = n - 1

    # Increase the number of c's from back
    while (cc < cnt and i >= 0):

        # Check if it is 'b' and it more
        # than n/3
        if (s[i] == 'b' and cb > cnt):
            cb -= 1
            s[i] = 'c'
            cc += 1

        i -= 1
    return s

# Driver Code

s = "aaaaaa"
n = len(s)

print(*lexoSmallest(list(s), n),sep="")

# This code is contributed by shivanisinghss2110
```

## c#

```
// C# program to minimize the number of
// replacements to get a string with same
// number of ‘a’, ‘b’ and ‘c’ in it
using System;
using System.Text; 

class GFG{

// Function to count numbers
static string lexoSmallest(string str, int n)
{

    // Count the number of 'a', 'b' and
    // 'c' in string
    int ca = 0, cb = 0, cc = 0;
    StringBuilder s = new StringBuilder(str); 

    for(int j = 0; j < n; j++)
    {
        if (s[j] == 'a')
            ca++;
        else if (s[j] == 'b')
            cb++;
        else
            cc++;
    }

    // If equal previously
    if (ca == cb && cb == cc) 
    {
        return s.ToString();
    }

    int cnt = n / 3;

    // If not a multiple of 3
    if (cnt * 3 != n)
    {
        return "-1";
    }

    int i = 0;

    // Increase the number of a's by
    // removing extra 'b' and ;c;
    while (ca < cnt && i < n)
    {

        // Check if it is 'b' and it more
        // than n/3
        if (s[i] == 'b' && cb > cnt)
        {
            cb--;
            s[i] = 'a';
            ca++;
        }

        // Check if it is 'c' and it
        // more than n/3
        else if (s[i] == 'c' && cc > cnt)
        {
            cc--;
            s[i] = 'a';
            ca++;
        }
        i++;
    }

    i = 0;

    // Increase the number of b's by
    // removing extra 'c'
    while (cb < cnt && i < n)
    {

        // Check if it is 'c' and it more
        // than n/3
        if (s[i] == 'c' && cc > cnt) 
        {
            cc--;
            s[i] = '1';

            cb++;
        }
        i++;
    }

    i = n - 1;

    // Increase the number of c's from back
    while (cc < cnt && i >= 0) 
    {

        // Check if it is 'a' and it more
        // than n/3
        if (s[i] == 'a' && ca > cnt)
        {
            ca--;
            s[i] = 'c';
            cc++;
        }
        i--;
    }

    i = n - 1;

    // Increase the number of b's from back
    while (cb < cnt && i >= 0)
    {

        // Check if it is 'a' and it more
        // than n/3
        if (s[i] == 'a' && ca > cnt)
        {
            ca--;
            s[i] = 'b';
            cb++;
        }
        i--;
    }

    i = n - 1;

    // Increase the number of c's from back
    while (cc < cnt && i >= 0)
    {

        // Check if it is 'b' and it more
        // than n/3
        if (s[i] == 'b' && cb > cnt) 
        {
            cb--;
            s[i] = 'c';
            cc++;
        }
        i--;
    }
    return s.ToString();
} 

// Driver Code
public static void Main(string[] args)
{
    string s = "aaaaaa";
    int n = s.Length;

    Console.Write(lexoSmallest(s, n));
}
}

// This code is contributed by rutvik_56
```

## PHP

```
<?php
// PHP program to Minimize the number of 
// replacements to get a string with same 
// number of ‘a’, ‘b’ and ‘c’ in it 

// Function to count numbers 
function lexoSmallest($s, $n) 
{ 
    // Count the number of 'a', 'b' 
    // and 'c' in string 
    $ca = 0;
    $cb = 0;
    $cc = 0; 

    for ($i = 0; $i < $n; $i++) 
    { 
        if ($s[$i] == 'a') 
            $ca++; 
        else if ($s[$i] == 'b') 
            $cb++; 
        else
            $cc++; 
    } 

    // If equal previously 
    if ($ca == $cb && $cb == $cc)
    { 
        return $s; 
    } 

    $cnt = floor($n / 3); 

    // If not a multiple of 3 
    if ($cnt * 3 != $n) 
    { 
        return "-1"; 
    } 

    $i = 0; 

    // Increase the number of a's by 
    // removing extra 'b' and ;c; 
    while ($ca < $cnt && $i < $n) 
    { 

        // Check if it is 'b' and it is
        // more than n/3 
        if ($s[$i] == 'b' && $cb > $cnt) 
        { 
            $cb--; 
            $s[$i] = 'a'; 
            $ca++; 
        } 

        // Check if it is 'c' and it 
        // more than n/3 
        else if ($s[$i] == 'c' && $cc > $cnt) 
        { 
            $cc--; 
            $s[$i] = 'a'; 
            $ca++; 
        } 

        $i++; 
    } 

    $i = 0; 

    // Increase the number of b's by 
    // removing extra 'c' 
    while ($cb < $cnt && $i < $n) 
    { 

        // Check if it is 'c' and it more 
        // than n/3 
        if ($s[$i] == 'c' && $cc > $cnt) 
        { 
            $cc--; 
            $s[$i] = '1'; 

            $cb++; 
        } 
        $i++; 
    } 

    $i = $n - 1; 

    // Increase the number of c's from back 
    while ($cc < $cnt && $i >= 0) 
    { 

        // Check if it is 'a' and it is 
        // more than n/3 
        if ($s[$i] == 'a' && $ca > $cnt) 
        { 
            $ca--; 
            $s[$i] = 'c'; 
            $cc++; 
        } 

        $i--; 
    } 

    $i = $n - 1; 

    // Increase the number of b's from back 
    while ($cb < $cnt && $i >= 0) 
    { 

        // Check if it is 'a' and it is 
        // more than n/3 
        if ($s[$i] == 'a' && $ca > $cnt) 
        { 
            $ca--; 
            $s[$i] = 'b'; 
            $cb++; 
        } 

        $i--; 
    } 

    $i = $n - 1; 

    // Increase the number of c's from back 
    while ($cc < $cnt && $i >= 0) 
    { 

        // Check if it is 'b' and it more 
        // than n/3 
        if ($s[$i] == 'b' && $cb > $cnt) 
        { 
            $cb--; 
            $s[$i] = 'c'; 
            $cc++; 
        } 

        $i--; 
    } 

    return $s; 
} 

// Driver Code 
$s = "aaaaaa"; 
$n = strlen($s); 

echo lexoSmallest($s, $n);

// This code is contributed by Ryuga.
?>

```

**输出:**

```
aabbcc

```

**时间复杂度** : O(N*6)
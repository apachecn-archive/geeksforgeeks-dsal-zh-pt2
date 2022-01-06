# 给定子序列的字符串的字典最小排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的给定子序列的最小排列/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-a-string-with-given-subsequences/)

给定一个仅由两个小写字符![x    ](img/bd0dd68c093f19d4b996e479298a7648.png "Rendered by QuickLaTeX.com")和![y    ](img/5d35b81612e96adc3a8475aa0ab5498c.png "Rendered by QuickLaTeX.com")以及两个数字![p    ](img/c0e2cd35fad700795d966d19b9f9f054.png "Rendered by QuickLaTeX.com")和![q    ](img/a44cc425692a47a58d7e4d00603ca213.png "Rendered by QuickLaTeX.com")组成的字符串。任务是打印给定字符串的字典最小排列，使得![xy    ](img/736758a6754f1c6cd184d481a2bea914.png "Rendered by QuickLaTeX.com")的子序列计数为![p    ](img/c0e2cd35fad700795d966d19b9f9f054.png "Rendered by QuickLaTeX.com")，而![yx    ](img/bb0237be9ac78345647f6f3c6952abf1.png "Rendered by QuickLaTeX.com")的子序列计数为![q    ](img/a44cc425692a47a58d7e4d00603ca213.png "Rendered by QuickLaTeX.com")。如果不存在这样的字符串，则打印“不可能”(不带引号)。
**举例:**

```
Input: str = "yxxyx", p = 3, q = 3 
Output: xyxyx

Input: str = "yxxy", p = 3, q = 2
Output: Impossible
```

**方法:**首先，通过归纳法可以证明，对于任意给定的字符串，“x”的计数和“y”的计数的乘积应该等于“xy”和“yx”的子序列的计数之和。如果这不成立，那么答案是“不可能”，否则答案永远存在。
现在，对给定的字符串进行排序，使“yx”子序列的计数为零。让 **nx** 为‘x’的计数，让 **ny** 为‘y’的计数。设 **a** 和 **b** 分别为子序列‘xy’和‘yx’的计数，则 **a = nx*ny** 和 **b = 0** 。然后，从字符串的开头开始，找到旁边有“y”的“x”，并交换两者，直到到达字符串的结尾。在每次交换中 **a** 减少 **1** ，而 **b** 增加 **1** 。重复此操作，直到达到“yx”子序列的计数，即:e **a** 变为 **p** 和 **b** 变为 **q** 。
以下是上述方法的实施:

## C++

```
// CPP program to find lexicographically smallest
// string such that count of subsequence 'xy' and
// 'yx' is p and q respectively.
#include <bits/stdc++.h>
using namespace std;

// function to check if answer exits
int nx = 0, ny = 0;

bool check(string s, int p, int q)
{
    // count total 'x' and 'y' in string
    for (int i = 0; i < s.length(); ++i) {
        if (s[i] == 'x')
            nx++;
        else
            ny++;
    }

    // condition to check existence of answer
    if (nx * ny != p + q)
        return 1;
    else
        return 0;
}

// function to find lexicographically smallest string
string smallestPermutation(string s, int p, int q)
{
    // check if answer exist or not
    if (check(s, p, q) == 1) {
        return "Impossible";
    }

    sort(s.begin(), s.end());
    int a = nx * ny, b = 0, i, j;

    // check if count of 'xy' and 'yx' becomes
    // equal to p and q respectively.
    if (a == p && b == q) {
        return s;
    }

    // Repeat until answer is found.
    while (1) {
        // Find index of 'x' to swap with 'y'.
        for (i = 0; i < s.length() - 1; ++i) {
            if (s[i] == 'x' && s[i + 1] == 'y')
                break;
        }

        for (j = i; j < s.length() - 1; j++) {
            if (s[j] == 'x' && s[j + 1] == 'y') {
                swap(s[j], s[j + 1]);
                a--; // 'xy' decrement by 1
                b++; // 'yx' increment by 1

                // check if count of 'xy' and 'yx' becomes
                // equal to p and q respectively.
                if (a == p && b == q) {
                    return s;
                }
            }
        }
    }
}

// Driver code
int main()
{
    string s = "yxxyx";
    int p = 3, q = 3;

    cout<< smallestPermutation(s, p, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find lexicographically
// smallest string such that count of
// subsequence 'xy' and 'yx' is p and
// q respectively.
import java.util.*;

class GFG
{
static int nx = 0, ny = 0;

static boolean check(String s,
                     int p, int q)
{
    // count total 'x' and 'y' in string
    for (int i = 0; i < s.length(); ++i)
    {
        if (s.charAt(i) == 'x')
            nx++;
        else
            ny++;
    }

    // condition to check
    // existence of answer
    if ((nx * ny) != (p + q))
        return true;
    else
        return false;
}

public static String smallestPermutation(String s,
                                         int p, int q)
{
    if (check(s, p, q) == true)
    {
        return "Impossible";
    }

    char tempArray[] = s.toCharArray();
    Arrays.sort(tempArray);

    String str = new String(tempArray);
    int a = nx * ny, b = 0, i = 0, j = 0;

    if (a == p && b == q)
    {
        return str;
    }

    while (1 > 0)
    {

    // Find index of 'x' to swap with 'y'.
    for (i = 0; i < str.length() - 1; ++i)
    {
        if (str.charAt(i) == 'x' &&
            str.charAt(i + 1) == 'y')
            break;
    }

    for (j = i; j < str.length() - 1; j++)
    {
        if (str.charAt(j) == 'x' &&
            str.charAt(j + 1) == 'y')
        {
        StringBuilder sb = new StringBuilder(str);
        sb.setCharAt(j, str.charAt(j + 1));
        sb.setCharAt(j + 1, str.charAt(j));
        str = sb.toString();
        /* char ch[] = str.toCharArray();
            char temp = ch[j+1];
            ch[j+1] = ch[j];
            ch[j] = temp;*/

            a--; // 'xy' decrement by 1
            b++; // 'yx' increment by 1

            // check if count of 'xy' and
            // 'yx' becomes equal to p
            // and q respectively.
            if (a == p && b == q)
            {
                return str;
            }
        }
    }
}
}

// Driver Code
public static void main (String[] args)
{
    String s = "yxxyx";
    int p = 3, q = 3;

    System.out.print(smallestPermutation(s, p, q));
}
}

// This code is contributed by Kirti_Mangal
```

## 蟒蛇 3

```
# Python3 program to find lexicographically
# smallest string such that count of subsequence
# 'xy' and 'yx' is p and q respectively.

# Function to check if answer exits
def check(s, p, q):

    global nx
    global ny

    # count total 'x' and 'y' in string
    for i in range(0, len(s)):
        if s[i] == 'x':
            nx += 1
        else:
            ny += 1

    # condition to check existence of answer
    if nx * ny != p + q:
        return 1
    else:
        return 0

# Function to find lexicographically
# smallest string
def smallestPermutation(s, p, q):

    # check if answer exist or not
    if check(s, p, q) == 1:
        return "Impossible"

    s = sorted(s)
    a, b, i = nx * ny, 0, 0

    # check if count of 'xy' and 'yx' becomes
    # equal to p and q respectively.
    if a == p and b == q:
        return '' . join(s)

    # Repeat until answer is found.
    while True:

        # Find index of 'x' to swap with 'y'.
        for i in range(0, len(s) - 1):
            if s[i] == 'x' and s[i + 1] == 'y':
                break

        for j in range(i, len(s) - 1):
            if s[j] == 'x' and s[j + 1] == 'y':

                s[j], s[j + 1] = s[j + 1], s[j]
                a -= 1 # 'xy' decrement by 1
                b += 1 # 'yx' increment by 1

                # check if count of 'xy' and 'yx' becomes
                # equal to p and q respectively.
                if a == p and b == q:
                    return '' . join(s)

# Driver code
if __name__ == "__main__":

    nx, ny = 0, 0
    s = "yxxyx"
    p, q = 3, 3

    print(smallestPermutation(s, p, q))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find lexicographically
// smallest string such that count of
// subsequence 'xy' and 'yx' is p and
// q respectively.
using System;
using System.Text;

class GFG
{

static int nx = 0, ny = 0;

static Boolean check(String s,
                    int p, int q)
{
    // count total 'x' and 'y' in string
    for (int i = 0; i < s.Length; ++i)
    {
        if (s[i] == 'x')
            nx++;
        else
            ny++;
    }

    // condition to check
    // existence of answer
    if ((nx * ny) != (p + q))
        return true;
    else
        return false;
}

public static String smallestPermutation(String s,
                                        int p, int q)
{
    if (check(s, p, q) == true)
    {
        return "Impossible";
    }

    char []tempArray = s.ToCharArray();
    Array.Sort(tempArray);

    String str = new String(tempArray);
    int a = nx * ny, b = 0, i = 0, j = 0;

    if (a == p && b == q)
    {
        return str;
    }

    while (1 > 0)
    {

    // Find index of 'x' to swap with 'y'.
    for (i = 0; i < str.Length - 1; ++i)
    {
        if (str[i] == 'x' &&
            str[i + 1] == 'y')
            break;
    }

    for (j = i; j < str.Length - 1; j++)
    {
        if (str[j] == 'x' &&
            str[j + 1] == 'y')
        {
            StringBuilder sb = new StringBuilder(str);
            sb.Remove(j,1);
            sb.Insert(j, str[j + 1]);
            sb.Remove(j+1,1);
            sb.Insert(j + 1, str[j]);
            str = sb.ToString();
            /* char ch[] = str.toCharArray();
                char temp = ch[j+1];
                ch[j+1] = ch[j];
                ch[j] = temp;*/

            a--; // 'xy' decrement by 1
            b++; // 'yx' increment by 1

            // check if count of 'xy' and
            // 'yx' becomes equal to p
            // and q respectively.
            if (a == p && b == q)
            {
                return str;
            }
        }
    }
}
}

// Driver Code
public static void Main (String[] args)
{
    String s = "yxxyx";
    int p = 3, q = 3;

    Console.WriteLine(smallestPermutation(s, p, q));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find lexicographically
// smallest string such that count of
// subsequence 'xy' and 'yx' is p and
// q respectively.

let nx = 0, ny = 0;
function check(s, p, q)
{
    // count total 'x' and 'y' in string
    for (let i = 0; i < s.length; ++i)
    {
        if (s[i] == 'x')
            nx++;
        else
            ny++;
    }

    // condition to check
    // existence of answer
    if ((nx * ny) != (p + q))
        return true;
    else
        return false;
}

function smallestPermutation(s,p,q)
{
    if (check(s, p, q) == true)
    {
        return "Impossible";
    }

    let tempArray = s.split("");
    (tempArray).sort();

    let str = (tempArray).join("");
    let a = nx * ny, b = 0, i = 0, j = 0;

    if (a == p && b == q)
    {
        return str;
    }

    while (1 > 0)
    {

    // Find index of 'x' to swap with 'y'.
    for (i = 0; i < str.length - 1; ++i)
    {
        if (str[i] == 'x' &&
            str[i+1] == 'y')
            break;
    }

    for (j = i; j < str.length - 1; j++)
    {
        if (str[j] == 'x' &&
            str[j+1] == 'y')
        {
        let sb = (str).split("");
        sb[j] = str[j+1];
        sb[j + 1] = str[j];
        str = sb.join("");
        /* char ch[] = str.toCharArray();
            char temp = ch[j+1];
            ch[j+1] = ch[j];
            ch[j] = temp;*/

            a--; // 'xy' decrement by 1
            b++; // 'yx' increment by 1

            // check if count of 'xy' and
            // 'yx' becomes equal to p
            // and q respectively.
            if (a == p && b == q)
            {
                return str;
            }
        }
    }
}
}

// Driver Code
let s = "yxxyx";
let p = 3;
let q = 3;

document.write(smallestPermutation(s, p, q));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
xyxyx
```

**时间复杂度:** O(N <sup>2</sup> )
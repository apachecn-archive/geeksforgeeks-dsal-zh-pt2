# 为使所有数字或交替数字相同，需要删除的最少数字

> 原文:[https://www . geeksforgeeks . org/要删除的最少位数-使所有位数或交替位数相同/](https://www.geeksforgeeks.org/minimum-digits-to-be-removed-to-make-either-all-digits-or-alternating-digits-same/)

给定一个数字字符串 **str** ，任务是找到要从字符串中删除的最小位数，使其满足以下任一条件:

*   字符串的所有元素都是相同的。
*   偶数位置的所有元素都是相同的，奇数位置的所有元素都是相同的，这意味着字符串与每个数字的相同出现交替出现。

**示例:**

> **输入:** s = "95831"
> **输出:** 3
> **解释:**
> 在本例中，去掉字符串中的任意三个元素使其交替出现，即“95”在偶数索引处有 9 个，在奇数索引处有 5 个，因此满足第二个条件。
> **输入:** s = "100120013"
> **输出:** 5
> **说明:**
> 这种情况下，要么使字符串 0000，要么使字符串 1010。在这两种情况下，必须从管柱中移除的最小元件是 **5** 。

**进场:**思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)。以下是步骤:

1.  由于结果字符串中的所有字符都是交替且相同的，因此不同数字的[最小子字符串](https://www.geeksforgeeks.org/length-smallest-sub-string-consisting-maximum-distinct-characters/)的长度为 2。
2.  因为，从 **0** 到 **9** 只有 **10** 不同类型的数字。其思想是迭代长度为 2 的每一个可能的字符串，并找到它们组成的子序列的出现。
3.  因此，找到上述两个数字串的串的第一个和第二个字符的所有可能组合，并贪婪地构建从这些字符开始的最长可能的子序列 **s** 。
4.  字符串长度与上述步骤中具有交替数字的子序列的最大长度之间的差值就是所需的结果。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find longest possible
// subsequence of s beginning with x and y
int solve(string s, int x, int y)
{
    int res = 0;

    // Iterate over the string
    for (auto c : s) {
        if (c - '0' == x) {

            // Increment count
            res++;

            // Swap the positions
            swap(x, y);
        }
    }

    if (x != y && res % 2 == 1)
        --res;

    // Return the result
    return res;
}

// Function that finds all the
// possible pairs
int find_min(string s)
{
    int count = 0;
    for (int i = 0; i < 10; i++) {

        for (int j = 0; j < 10; j++) {

            // Update count
            count = max(count,
                        solve(s, i, j));
        }
    }

    // Return the answer
    return count;
}

// Driver Code
int main()
{
    // Given string s
    string s = "100120013";

    // Find the size of the string
    int n = s.size();

    // Function Call
    int answer = find_min(s);

    // This value is the count of
    // minimum element to be removed
    cout << (n - answer);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find longest possible
// subsequence of s beginning with x and y
static int solve(String s, int x, int y)
{
    int res = 0;

    // Iterate over the String
    for (char c : s.toCharArray())
    {
        if (c - '0' == x)
        {

            // Increment count
            res++;

            // Swap the positions
            x = x+y;
            y = x-y;
            x = x-y;
        }
    }

    if (x != y && res % 2 == 1)
        --res;

    // Return the result
    return res;
}

// Function that finds all the
// possible pairs
static int find_min(String s)
{
    int count = 0;
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {

            // Update count
            count = Math.max(count,
                             solve(s, i, j));
        }
    }

    // Return the answer
    return count;
}

// Driver Code
public static void main(String[] args)
{
    // Given String s
    String s = "100120013";

    // Find the size of the String
    int n = s.length();

    // Function Call
    int answer = find_min(s);

    // This value is the count of
    // minimum element to be removed
    System.out.print((n - answer));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find longest possible
# subsequence of s beginning with x and y
def solve(s, x, y):

    res = 0

    # Iterate over the string
    for c in s:
        if(ord(c) - ord('0') == x):

            # Increment count
            res += 1

            # Swap the positions
            x, y = y, x

    if(x != y and res % 2 == 1):
        res -= 1

    # Return the result
    return res

# Function that finds all the
# possible pairs
def find_min(s):

    count = 0
    for i in range(10):
        for j in range(10):

            # Update count
            count = max(count, solve(s, i, j))

    # Return the answer
    return count

# Driver Code

# Given string s
s = "100120013"

# Find the size of the string
n = len(s)

# Function call
answer = find_min(s)

# This value is the count of
# minimum element to be removed
print(n - answer)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find longest possible
// subsequence of s beginning with x and y
static int solve(String s, int x, int y)
{
    int res = 0;

    // Iterate over the String
    foreach (char c in s.ToCharArray())
    {
        if (c - '0' == x)
        {

            // Increment count
            res++;

            // Swap the positions
            x = x + y;
            y = x - y;
            x = x - y;
        }
    }

    if (x != y && res % 2 == 1)
        --res;

    // Return the result
    return res;
}

// Function that finds all the
// possible pairs
static int find_min(String s)
{
    int count = 0;
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {

            // Update count
            count = Math.Max(count,
                             solve(s, i, j));
        }
    }

    // Return the answer
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    // Given String s
    String s = "100120013";

    // Find the size of the String
    int n = s.Length;

    // Function Call
    int answer = find_min(s);

    // This value is the count of
    // minimum element to be removed
    Console.Write((n - answer));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find longest possible
// subsequence of s beginning with x and y
function solve(s, x, y)
{
    let res = 0;

    // Iterate over the string
    for (let c of s) {
        if (c - '0' == x) {

            // Increment count
            res++;

            // Swap the positions
            x = x+y;
            y = x-y;
            x = x-y;
        }
    }

    if (x != y && res % 2 == 1)
        --res;

    // Return the result
    return res;
}

// Function that finds all the
// possible pairs
function find_min(s)
{
    let count = 0;
    for (let i = 0; i < 10; i++) {

        for (let j = 0; j < 10; j++) {

            // Update count
            count = Math.max(count,
                        solve(s, i, j));
        }
    }

    // Return the answer
    return count;
}

// Driver Code
    // Given string s
    let s = "100120013";

    // Find the size of the string
    let n = s.length;

    // Function Call
    let answer = find_min(s);

    // This value is the count of
    // minimum element to be removed
    document.write(n - answer);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
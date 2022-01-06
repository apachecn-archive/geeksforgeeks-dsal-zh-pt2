# 左右旋转相同的数的最长子序列

> 原文:[https://www . geeksforgeeks . org/左右旋转相同的数字的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-of-a-number-having-same-left-and-right-rotation/)

给定一个数字串 **S** ，任务是找到一个子序列的最大长度，它的左旋转等于它的右旋转。

**示例:**

> **输入:** S = "100210601"
> **输出:** 4
> **说明:**
> 子序列“0000”满足必要条件。
> 子序列“1010”在左旋转时生成字符串“0101”，在右旋转时生成字符串“0101”。因为两个旋转是相同的。因此，“1010”也满足条件。
> 因此，这种子序列的最大长度为 4。
> **输入:** S = "252525"
> **输出:** 6
> **解释:**
> 子序列“252525”生成左旋转的字符串“525252”和右旋转的字符串“525252”。因为两个旋转是相同的。因此，“252525”满足要求的条件。

**天真方法:**解决问题最简单的方法是[生成给定字符串的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，对于每个子序列，检查其左旋转是否等于其右旋转。
***时间复杂度:**O(2<sup>N</sup>* N)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，主要观察结果是子序列应该由一个**单个字符**组成，或者应该是由**两个字符交替组成的偶数长度**。

> **插图:**
> str = "2424"
> 左旋转字符串= "4242"
> 右旋转字符串= "4242"
> 我们可以看到，由于数字是偶数长度，有两个字符交替出现，因此，给定数字的左右旋转相等。
> str =“24242”
> 字符串的左旋转=“42422”
> 字符串的右旋转=“22424”
> 我们可以看到，由于数字是奇数长度，有两个字符交替出现，因此，给定数字的左右旋转不相等。

按照以下步骤解决问题:

*   生成所有可能的两位数。
*   对于生成的每个两位数，检查字符串中两位数的交替出现。保持递增计数以存储特定组合的交替子序列的长度。
*   在整个字符串遍历之后，检查两个数字是否相等。如果发现为真，将**计数**更新为所需答案。如果两位数相等，那么如果计数分别为偶数或奇数，则将**计数**或**计数–1**更新为答案。
*   对所有可能的组合重复上述步骤，并打印获得的最大**计数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subsequence
// having equal left and right rotation
int findAltSubSeq(string s)
{
    // Length of the string
    int n = s.size(), ans = INT_MIN;

    // Iterate for all possible combinations
    // of a two-digit numbers
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < 10; j++) {
            int cur = 0, f = 0;

            // Check for alternate occurrence
            // of current combination
            for (int k = 0; k < n; k++) {

                if (f == 0 and s[k] - '0' == i) {
                    f = 1;

                    // Increment the current value
                    cur++;
                }
                else if (f == 1 and s[k] - '0' == j) {
                    f = 0;

                    // Increment the current value
                    cur++;
                }
            }

            // If alternating sequence is
            // obtained of odd length
            if (i != j and cur % 2 == 1)

                // Reduce to even length
                cur--;

            // Update answer to store
            // the maximum
            ans = max(cur, ans);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    string s = "100210601";
    cout << findAltSubSeq(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the longest subsequence
// having equal left and right rotation
static int findAltSubSeq(String s)
{
    // Length of the String
    int n = s.length(), ans = Integer.MIN_VALUE;

    // Iterate for all possible combinations
    // of a two-digit numbers
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {
            int cur = 0, f = 0;

            // Check for alternate occurrence
            // of current combination
            for (int k = 0; k < n; k++)
            {
                if (f == 0 && s.charAt(k) - '0' == i)
                {
                    f = 1;

                    // Increment the current value
                    cur++;
                }
                else if (f == 1 &&
                         s.charAt(k) - '0' == j)
                {
                    f = 0;

                    // Increment the current value
                    cur++;
                }
            }

            // If alternating sequence is
            // obtained of odd length
            if (i != j && cur % 2 == 1)

                // Reduce to even length
                cur--;

            // Update answer to store
            // the maximum
            ans = Math.max(cur, ans);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String s = "100210601";
    System.out.print(findAltSubSeq(s));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the longest subsequence
# having equal left and right rotation
def findAltSubSeq(s):

    # Length of the string
    n = len(s)
    ans = -sys.maxsize - 1

    # Iterate for all possible combinations
    # of a two-digit numbers
    for i in range(10):
        for j in range(10):
            cur, f = 0, 0

            # Check for alternate occurrence
            # of current combination
            for k in range(n):
                if (f == 0 and ord(s[k]) -
                               ord('0') == i):
                    f = 1

                    # Increment the current value
                    cur += 1

                elif (f == 1 and ord(s[k]) -
                                 ord('0') == j):
                    f = 0

                    # Increment the current value
                    cur += 1

            # If alternating sequence is
            # obtained of odd length
            if i != j and cur % 2 == 1:

                # Reduce to even length
                cur -= 1

            # Update answer to store
            # the maximum
            ans = max(cur, ans)

    # Return the answer
    return ans

# Driver code
s = "100210601"

print(findAltSubSeq(s))

# This code is contributed by Stuti Pathak
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to find the longest subsequence
// having equal left and right rotation
static int findAltSubSeq(String s)
{
    // Length of the String
    int n = s.Length, ans = int.MinValue;

    // Iterate for all possible combinations
    // of a two-digit numbers
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {
            int cur = 0, f = 0;

            // Check for alternate occurrence
            // of current combination
            for (int k = 0; k < n; k++)
            {
                if (f == 0 && s[k] - '0' == i)
                {
                    f = 1;

                    // Increment the current value
                    cur++;
                }
                else if (f == 1 &&
                         s[k] - '0' == j)
                {
                    f = 0;

                    // Increment the current value
                    cur++;
                }
            }

            // If alternating sequence is
            // obtained of odd length
            if (i != j && cur % 2 == 1)

                // Reduce to even length
                cur--;

            // Update answer to store
            // the maximum
            ans = Math.Max(cur, ans);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "100210601";
    Console.Write(findAltSubSeq(s));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to find the longest subsequence
// having equal left and right rotation
function findAltSubSeq(s)
{
    // Length of the string
    var n = s.length, ans = -1000000000;

    // Iterate for all possible combinations
    // of a two-digit numbers
    for (var i = 0; i < 10; i++) {
        for (var j = 0; j < 10; j++) {
            var cur = 0, f = 0;

            // Check for alternate occurrence
            // of current combination
            for (var k = 0; k < n; k++) {

                if (f == 0 && s[k] - '0' == i) {
                    f = 1;

                    // Increment the current value
                    cur++;
                }
                else if (f == 1 && s[k] - '0' == j) {
                    f = 0;

                    // Increment the current value
                    cur++;
                }
            }

            // If alternating sequence is
            // obtained of odd length
            if (i != j && cur % 2 == 1)

                // Reduce to even length
                cur--;

            // Update answer to store
            // the maximum
            ans = Math.max(cur, ans);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
var s = "100210601";
document.write( findAltSubSeq(s));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
# 清空一个二进制字符串所需移除的最小替换子序列数

> 原文:[https://www . geeksforgeeks . org/最小数量的替换子序列-需要删除到空的二进制字符串/](https://www.geeksforgeeks.org/minimum-number-of-alternate-subsequences-required-to-be-removed-to-empty-a-binary-string/)

给定由 **N** 个字符组成的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过删除单个字符或删除每个操作中替换字符的任何子序列来打印[从给定字符串 **S**](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-character-in-a-string/) 中删除所有字符所需的最小操作数。

**示例:**

> **输入:** S = "010101"
> **输出:** 1
> **解释:**
> 下面是执行的操作:
> **操作 1:** 考虑子序列 S[0，5]即“010101”，因为它包含交替字符。因此，删除此选项会将字符串修改为“”。
> 因此，所需操作总数为 1。
> 
> **输入:**S = " 00011 "
> T3】输出: 3

**方法:**给定的问题可以通过[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)一次并跟踪剩余的最大数量 **0s** 和 **1s** 来解决。按照以下步骤解决问题:

*   初始化一个变量，比如说 **ans** 存储还有待删除的最大数量 **0s** 和 **1s** ，一个变量 **cnt0** 统计 **0s** 的数量，一个变量 **cnt1** 到[统计 **1s**](https://www.geeksforgeeks.org/total-no-1s-numbers/) 的数量。
*   [从头开始遍历给定的字符串 **S**](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) ，并执行以下步骤:
    *   如果当前字符为 **0** ，那么将 **cnt0** 的值增加 **1** ，如果大于 **0** ，则将 **cnt1** 的值减少 **1** 。
    *   如果当前字符为 **1** ，则 **cnt1** 的值增加 **1** ，如果大于 **0** ，则 **cnt0** 的值减少 **1** 。
    *   将 **ans** 的值更新为 **ans** 、 **cnt1** 和 **cnt0** 的最大值。
*   完成上述步骤后，打印**和**的值，作为移除所有字符所需的最小操作次数。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations to empty a binary string
int minOpsToEmptyString(string s)
{
    // Stores the resultant number of
    // operations
    int ans = INT_MIN;

    // Stores the number of 0s
    int cn0 = 0;

    // Stores the number of 1s
    int cn1 = 0;

    // Traverse the given string
    for (int i = 0;
         i < s.length(); i++) {

        if (s[i] == '0') {

            // To balance 0 with 1
            // if possible
            if (cn1 > 0)
                cn1--;

            // Increment the value
            // of cn0 by 1
            cn0++;
        }
        else {

            // To balance 1 with 0
            // if possible
            if (cn0 > 0)
                cn0--;

            // Increment the value
            // of cn1
            cn1++;
        }

        // Update the maximum number
        // of unused 0s and 1s
        ans = max({ ans, cn0, cn1 });
    }

    // Print the resultant count
    cout << ans;
}

// Driver Code
int main()
{
    string S = "010101";
    minOpsToEmptyString(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum number
// of operations to empty a binary string
static void minOpsToEmptyString(String s)
{

    // Stores the resultant number of
    // operations
    int ans = Integer.MIN_VALUE;

    // Stores the number of 0s
    int cn0 = 0;

    // Stores the number of 1s
    int cn1 = 0;

    // Traverse the given string
    for(int i = 0; i < s.length(); i++)
    {
        if (s.charAt(i) == '0')
        {

            // To balance 0 with 1
            // if possible
            if (cn1 > 0)
                cn1--;

            // Increment the value
            // of cn0 by 1
            cn0++;
        }
        else
        {

            // To balance 1 with 0
            // if possible
            if (cn0 > 0)
                cn0--;

            // Increment the value
            // of cn1
            cn1++;
        }

        // Update the maximum number
        // of unused 0s and 1s
        ans = Math.max(ans, Math.max(cn0, cn1));
    }

    // Print the resultant count
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    String S = "010101";
    minOpsToEmptyString(S);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of operations to empty a binary string
def minOpsToEmptyString(s):

    # Stores the resultant number of
    # operations
    ans = -10**9

    # Stores the number of 0s
    cn0 = 0

    # Stores the number of 1s
    cn1 = 0

    # Traverse the given string
    for i in range(len(s)):
        if (s[i] == '0'):

            # To balance 0 with 1
            # if possible
            if (cn1 > 0):
                cn1 -= 1

            # Increment the value
            # of cn0 by 1
            cn0 += 1
        else:

            # To balance 1 with 0
            # if possible
            if (cn0 > 0):
                cn0 -= 1

            # Increment the value
            # of cn1
            cn1 += 1

        # Update the maximum number
        # of unused 0s and 1s
        ans = max([ans, cn0, cn1])

    # Print resultant count
    print (ans)

# Driver Code
if __name__ == '__main__':
    S = "010101"
    minOpsToEmptyString(S)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum number
// of operations to empty a binary string
static void minOpsToEmptyString(string s)
{

    // Stores the resultant number of
    // operations
    int ans = 0;

    // Stores the number of 0s
    int cn0 = 0;

    // Stores the number of 1s
    int cn1 = 0;

    // Traverse the given string
    for(int i = 0; i < s.Length; i++)
    {
        if (s[i] == '0')
        {

            // To balance 0 with 1
            // if possible
            if (cn1 > 0)
                cn1--;

            // Increment the value
            // of cn0 by 1
            cn0++;
        }
        else
        {

            // To balance 1 with 0
            // if possible
            if (cn0 > 0)
                cn0--;

            // Increment the value
            // of cn1
            cn1++;
        }

        // Update the maximum number
        // of unused 0s and 1s
        ans = Math.Max(ans, Math.Max(cn0, cn1));
    }

    // Print the resultant count
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    string S = "010101";
    minOpsToEmptyString(S);
}
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to find the minimum number
// of operations to empty a binary string
function minOpsToEmptyString(s)
{

    // Stores the resultant number of
    // operations
    var ans = Number.MIN_VALUE;

    // Stores the number of 0s
    var cn0 = 0;

    // Stores the number of 1s
    var cn1 = 0;

    // Traverse the given string
    for(var i = 0; i < s.length; i++)
    {
        if (s.charAt(i) == '0')
        {

            // To balance 0 with 1
            // if possible
            if (cn1 > 0)
                cn1--;

            // Increment the value
            // of cn0 by 1
            cn0++;
        }
        else
        {

            // To balance 1 with 0
            // if possible
            if (cn0 > 0)
                cn0--;

            // Increment the value
            // of cn1
            cn1++;
        }

        // Update the maximum number
        // of unused 0s and 1s
        ans = Math.max(ans, Math.max(cn0, cn1));
    }

    // Print the resultant count
    document.write(ans);
}

// Driver Code
var S = "010101";
minOpsToEmptyString(S);

//This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
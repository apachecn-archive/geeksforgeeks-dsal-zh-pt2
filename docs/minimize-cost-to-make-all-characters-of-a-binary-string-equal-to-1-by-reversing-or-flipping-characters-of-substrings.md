# 通过反转或翻转子字符串的字符使二进制字符串的所有字符等于“1”的成本最小化

> 原文:[https://www . geeksforgeeks . org/通过反转或翻转子字符串字符使二进制字符串的所有字符等于 1 的成本最小化/](https://www.geeksforgeeks.org/minimize-cost-to-make-all-characters-of-a-binary-string-equal-to-1-by-reversing-or-flipping-characters-of-substrings/)

给定一个 [<u>二进制字符串</u>](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，以及两个整数 **A** ，表示[反转一个子串](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/)的代价， **B** ，表示翻转一个子串所有字符的代价，任务是找到**最小代价**将字符串 **S** 缩减为 **1** s 而已。

**示例:**

> **输入:** S = "01100 "，A = 1，B = 5
> **输出:** 6
> **解释:**
> 使所有字符等于‘1’的一种可能方法如下:
> 
> 1.  反转子字符串{S[0]，S[2]}。成本= A (= 1)，字符串修改为“11000”。
> 2.  翻转子串{S[2]，S[4]}的字符。B = 5 的成本。字符串修改为“11111”。
> 
> 因此，总成本= 5+1 = 6(这是可能的最小成本)
> 
> **输入:** S = "1111111 "，A = 2，B = 3
> T3】输出: 0

**方法:**给定的问题可以基于以下观察来解决:

> *   Suppose there are continuous **[0]** s,
> *   The disjoint group of **p** , if **a is less than b** , then it is best to convert the group of **p** into the group of **[1]** of continuous **[0]** s, by performing the first kind of operation at the cost of **Then all **[0]** s are converted into **[1]** s at a cost of **B.****
> *   Otherwise, the best execution.

按照以下步骤解决问题:

*   用 **0** 值初始化一个变量，比如 **P** ，以存储连续 **0** s 的不相交组的计数
*   另外，初始化一个变量，比如说**计数**为 **0** 来存储一个组中 **0** 的临时计数。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并执行以下操作:
    *   如果当前字符是“ **0** ，那么将**计数**增加 **1** 。
    *   否则，如果**计数**大于 **0** ，则以 **1** 递增 **P** ，然后将 **0** 分配给**计数**。
*   如果**计数**大于 **0** ，那么将 **P** 增加 **1。**
*   将获得的最小成本打印为 **(P-1)*A+B.**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum cost to
// convert all the characters of S to '1'
void MinimumCost(string S, int A, int B)
{
    // Stores the result
    int count = 0;

    // Stores the number of groups
    // that have 0 as characters
    int group = 0;

    // Traverse the string S
    for (int i = 0; i < S.size(); i++) {

        // If current character is '0'
        if (S[i] == '0') {
            count += 1;
        }
        else {
            // If count is greater
            // than 0
            if (count > 0) {
                group += 1;
            }

            // Set the count to 0
            count = 0;
        }
    }

    // If the last few consecutive
    // characters are '0'
    if (count > 0)
        group += 1;

    // If string contains
    // all characters as '1'
    if (group == 0) {
        cout << 0 << endl;
    }
    else {
        // Minimum Cost
        cout << min(A, B) * (group - 1) + B;
    }
}

// Driver Code
int main()
{

    // Given Input
    int A = 1;
    int B = 5;
    string S = "01100";

    // Function Call
    MinimumCost(S, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate minimum cost to
// convert all the characters of S to '1'
static void MinimumCost(String S, int A, int B)
{

    // Stores the result
    int count = 0;

    // Stores the number of groups
    // that have 0 as characters
    int group = 0;

    // Traverse the string S
    for(int i = 0; i < S.length(); i++)
    {

        // If current character is '0'
        if (S.charAt(i) == '0')
        {
            count += 1;
        }
        else
        {

            // If count is greater
            // than 0
            if (count > 0)
            {
                group += 1;
            }

            // Set the count to 0
            count = 0;
        }
    }

    // If the last few consecutive
    // characters are '0'
    if (count > 0)
        group += 1;

    // If string contains
    // all characters as '1'
    if (group == 0)
    {
        System.out.println(0);
    }
    else
    {

        // Minimum Cost
        System.out.print(Math.min(A, B) *
                        (group - 1) + B);
    }
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int A = 1;
    int B = 5;
    String S = "01100";

    // Function Call
    MinimumCost(S, A, B);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate minimum cost to
# convert all the characters of S to '1'
def MinimumCost(S, A, B):
    # Stores the result
    count = 0

    # Stores the number of groups
    # that have 0 as characters
    group = 0

    # Traverse the S
    for i in range(len(S)):
        # If current character is '0'
        if (S[i] == '0'):
            count += 1
        else:
            # If count is greater
            # than 0
            if (count > 0):
                group += 1
            # Set the count to 0
            count = 0

    # If the last few consecutive
    # characters are '0'
    if (count > 0):
        group += 1

    # If contains
    # all characters as '1'
    if (group == 0):
        print(0)
    else:
        # Minimum Cost
        print(min(A, B) * (group - 1) + B)

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = 1
    B = 5
    S = "01100"

    # Function Call
    MinimumCost(S, A, B)

     # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate minimum cost to
// convert all the characters of S to '1'
static void MinimumCost(string S, int A, int B)
{

    // Stores the result
    int count = 0;

    // Stores the number of groups
    // that have 0 as characters
    int group = 0;

    // Traverse the string S
    for(int i = 0; i < S.Length; i++)
    {

        // If current character is '0'
        if (S[i] == '0')
        {
            count += 1;
        }
        else
        {

            // If count is greater
            // than 0
            if (count > 0)
            {
                group += 1;
            }

            // Set the count to 0
            count = 0;
        }
    }

    // If the last few consecutive
    // characters are '0'
    if (count > 0)
        group += 1;

    // If string contains
    // all characters as '1'
    if (group == 0)
    {
        Console.WriteLine(0);
    }
    else
    {

        // Minimum Cost
        Console.Write(Math.Min(A, B) *
                      (group - 1) + B);
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    int A = 1;
    int B = 5;
    string S = "01100";

    // Function Call
    MinimumCost(S, A, B);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate minimum cost to
// convert all the characters of S to '1'
function MinimumCost(S, A, B) {
    // Stores the result
    let count = 0;

    // Stores the number of groups
    // that have 0 as characters
    let group = 0;

    // Traverse the string S
    for (let i = 0; i < S.length; i++) {

        // If current character is '0'
        if (S[i] == '0') {
            count += 1;
        }
        else
        {

            // If count is greater
            // than 0
            if (count > 0) {
                group += 1;
            }

            // Set the count to 0
            count = 0;
        }
    }

    // If the last few consecutive
    // characters are '0'
    if (count > 0)
        group += 1;

    // If string contains
    // all characters as '1'
    if (group == 0) {
        document.write(0 + "<br>");
    }
    else {
        // Minimum Cost
        document.write(Math.min(A, B) * (group - 1) + B);
    }
}

// Driver Code

// Given Input
let A = 1;
let B = 5;
let S = "01100";

// Function Call
MinimumCost(S, A, B);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
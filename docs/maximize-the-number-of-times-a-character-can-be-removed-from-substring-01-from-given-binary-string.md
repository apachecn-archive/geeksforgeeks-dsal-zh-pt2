# 最大化从给定二进制字符串的子串 01 中删除字符的次数

> 原文:[https://www . geesforgeks . org/最大化从给定二进制字符串中移除字符的次数-子字符串-01/](https://www.geeksforgeeks.org/maximize-the-number-of-times-a-character-can-be-removed-from-substring-01-from-given-binary-string/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过选择任意子字符串“ **01** ”并在一次移动中移除其中的任意字符，找到可以在 **S** 上执行的最大操作数，从而将字符串的长度减少 **1** 。

**示例:**

> **输入:** S = "001111 "，N = 6
> **输出:** 5
> **解释:**
> 执行操作的一种方式是:
> 
> 1.  选择范围[1，2]内的子字符串“01”，并删除 S[2] ( = '1 ')。字符串修改为“00111”。
> 2.  选择范围[1，2]内的子字符串“01”，并删除 S[2] ( = '1 ')。字符串修改为“0011”。
> 3.  选择范围[1，2]内的子字符串“01”，并删除 S[2] ( = '1 ')。字符串修改为“001”。
> 4.  选择范围[1，2]内的子字符串“01”，并删除 S[1] ( = '0 ')。字符串修改为“01”。
> 5.  选择范围[0，1]内的子字符串“01”，并删除 S[1] ( = '1 ')。字符串修改为“0”。
> 6.  现在没有字符可以删除。
> 
> 因此，执行的操作总数是 5，这是可能的最大值。
> 
> **输入:**S =“0101”，N = 4
> T3】输出: 3

**方法:**给定的问题可以基于以下观察来解决:

> 1.  Any **1s** appearing in the prefix of **s** cannot be removed because they have no **0s** before them.
> 2.  Any **0s** appearing in the suffix of **s** cannot be deleted, because they are not followed by **1s** .
> 3.  All other characters can be removed.
> 4.  If there are **x** removable characters, you can perform **x-1** operation at most, because there is only one character left that cannot be removed.

按照以下步骤解决问题:

*   初始化两个变量，说 **X** 和 **Y** 为 **0** ，分别存储后缀中 **0s** 的个数和前缀中 **1s** 的个数，不能去掉。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并执行以下步骤:
    *   如果当前字符是“**1′**，则用 **1 增加 **Y** 。**
    *   否则，停止遍历。
*   [在中重复字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，颠倒的顺序并执行以下步骤:
    *   如果当前字符为 **0** ，则按 **1** 递增 **X** 。
    *   否则，停止遍历。
*   如果**X****Y**之和等于 **N** ，则打印 **0** ，因为没有可移动字符。
*   否则，打印 **N-(X+Y)-1** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum moves
// that can be performed on a string
int maxOperations(string S, int N)
{
    // Stores 0s in suffix
    int X = 0;
    // Stores 1s in prefix
    int Y = 0;

    // Iterate over the characters of
    // the string
    for (int i = 0; i < N; i++) {
        if (S[i] == '0')
            break;
        Y++;
    }
    // Iterate until i is greater than
    // or equal to 0
    for (int i = N - 1; i >= 0; i--) {
        if (S[i] == '1')
            break;
        X++;
    }

    // If N is equal to x+y
    if (N == X + Y)
        return 0;

    // Return answer
    return N - (X + Y) - 1;
}
// Driver code
int main()
{
    // Input
    string S = "001111";
    int N = S.length();

    // Function call
    cout << maxOperations(S, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the maximum moves
// that can be performed on a string
static int maxOperations(String S, int N)
{

    // Stores 0s in suffix
    int X = 0;

    // Stores 1s in prefix
    int Y = 0;

    // Iterate over the characters of
    // the string
    for(int i = 0; i < N; i++)
    {
        if (S.charAt(i) == '0')
            break;

        Y++;
    }

    // Iterate until i is greater than
    // or equal to 0
    for(int i = N - 1; i >= 0; i--)
    {
        if (S.charAt(i) == '1')
            break;

        X++;
    }

    // If N is equal to x+y
    if (N == X + Y)
        return 0;

    // Return answer
    return N - (X + Y) - 1;
}

// Driver code
public static void main(String[] args)
{

    // Input
    String S = "001111";
    int N = S.length();

    // Function call
    System.out.println(maxOperations(S, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum moves
# that can be performed on a string
def maxOperations(S, N):

    # Stores 0s in suffix
    X = 0

    # Stores 1s in prefix
    Y = 0

    # Iterate over the characters of
    # the string
    for i in range(N):
        if (S[i] == '0'):
            break

        Y += 1

    # Iterate until i is greater than
    # or equal to 0
    i = N - 1
    while(i >= 0):
        if (S[i] == '1'):
            break

        X += 1

    # If N is equal to x+y
    if (N == X + Y):
        return 0

    # Return answer
    return N - (X + Y) - 1

# Driver code
if __name__ == '__main__':

    # Input
    S = "001111"
    N = len(S)

    # Function call
    print(maxOperations(S, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum moves
// that can be performed on a string
static int maxOperations(String S, int N)
{

    // Stores 0s in suffix
    int X = 0;

    // Stores 1s in prefix
    int Y = 0;

    // Iterate over the characters of
    // the string
    for(int i = 0; i < N; i++)
    {
        if (S[i] == '0')
            break;

        Y++;
    }

    // Iterate until i is greater than
    // or equal to 0
    for(int i = N - 1; i >= 0; i--)
    {
        if (S[i] == '1')
            break;

        X++;
    }

    // If N is equal to x+y
    if (N == X + Y)
        return 0;

    // Return answer
    return N - (X + Y) - 1;
}

// Driver code
static void Main()
{

    // Input
    String S = "001111";
    int N = S.Length;

    // Function call
    Console.WriteLine(maxOperations(S, N));
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum moves
// that can be performed on a string
function maxOperations(S, N)
{

    // Stores 0s in suffix
    let X = 0;

    // Stores 1s in prefix
    let Y = 0;

    // Iterate over the characters of
    // the string
    for(let i = 0; i < N; i++)
    {
        if (S[i] == '0')
            break;

        Y++;
    }

    // Iterate until i is greater than
    // or equal to 0
    for(let i = N - 1; i >= 0; i--)
    {
        if (S[i] == '1')
            break;

        X++;
    }

    // If N is equal to x+y
    if (N == X + Y)
        return 0;

    // Return answer
    return N - (X + Y) - 1;
}

// Driver Code

    // Input
    let S = "001111";
    let N = S.length;

    // Function call
    document.write(maxOperations(S, N));

</script>
```

**Output**

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
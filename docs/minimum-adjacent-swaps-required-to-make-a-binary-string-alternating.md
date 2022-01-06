# 使二进制字符串交替所需的最小相邻交换次数

> 原文:[https://www . geesforgeks . org/minimum-邻接权-互换-需要制作二进制字符串-交替/](https://www.geeksforgeeks.org/minimum-adjacent-swaps-required-to-make-a-binary-string-alternating/)

给定大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到使[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)交替所需的最小相邻交换次数。如果不可能，则打印 **-1** 。

**示例:**

> **输入:** S = "10011"
> **输出:** 1
> **解释:**
> 互换索引 2 和索引 3，字符串变为 10101。
> 
> **输入:** S = "110100"
> **输出:** 2
> **解释:**
> 首先，互换索引 1 和索引 2，字符串变为 101100。
> 其次，互换索引 3 和索引 4，字符串变为 101010。

**进场:**为使弦交替，在第一位置取**“1”**或**“0”**。当弦长为**甚至**时，弦长必须以**“0”**或**“1”**开始。当字符串的长度为**奇数**时，有两种**可能的情况——如果字符串中 **1 的**的数量大于字符串中 **0 的**的数量，则字符串必须以“**1”**开头。否则如果**0**的数量大于**1**的数量，则串必须以**“0”**开始。因此，检查二进制字符串以第一个位置的**“1”**和第一个位置的**“0”**开始的两种情况。按照以下步骤解决问题:**

*   将变量**1**和**0**初始化为 **0** 来计算字符串中 0 和 1 的数量。
*   [使用变量 **i** 和](https://www.geeksforgeeks.org/range-based-loop-c/)[遍历范围](https://www.geeksforgeeks.org/c-program-to-count-zeros-and-ones-in-binary-representation-of-a-number/)**【0，N】**，计算二进制字符串中 **0 的**和 **1 的**的数量。
*   检查基本情况，即如果 **N** 是偶数，那么如果**0**等于**1**与否。如果 **N** 是奇数，那么它们之间的差应该是 **1。**如果基本情况不满足，则返回 **-1** 。
*   将变量 **ans_1** 初始化为 **0** ，当字符串以 **1** 和 **j** 开头为 **0 时，存储答案。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，如果**s【I】**等于 **1** ，则将 **abs(j-i)** 的值加到变量 **ans_1** 上，并将 **j** 的值增加 **2** 。
*   同样，将变量 **ans_0** 初始化为 **0** ，当字符串以 **1** 和 **k** 开头为 **0** 时，存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，如果**s【I】**等于 **0** ，则将**ABS(k–I)**的值加到变量 **ans_0** 上，并将 **k** 的值增加 **2** 。
*   如果 **N** 为偶数，则打印 **ans_1** 或 **ans_0** 的最小值作为结果。否则，如果**零**大于**一**，则打印 **ans_0** 。否则，打印 **ans_1** 。

下面是执行上述方法的情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of adjacent swaps to make the string
// alternating
int minSwaps(string s)
{
    // Count the no of zeros and ones
    int ones = 0, zeros = 0;
    int N = s.length();

    for (int i = 0; i < N; i++) {
        if (s[i] == '1')
            ones++;
        else
            zeros++;
    }

    // Base Case
    if ((N % 2 == 0 && ones != zeros)
        || (N % 2 == 1
            && abs(ones - zeros) != 1)) {
        return -1;
    }

    // Store no of min swaps when
    // string starts with "1"
    int ans_1 = 0;

    // Keep track of the odd positions
    int j = 0;

    // Checking for when the string
    // starts with "1"
    for (int i = 0; i < N; i++) {
        if (s[i] == '1') {

            // Adding the no of swaps to
            // fix "1" at odd positions
            ans_1 += abs(j - i);
            j += 2;
        }
    }

    // Store no of min swaps when string
    // starts with "0"
    int ans_0 = 0;

    // Keep track of the odd positions
    int k = 0;

    // Checking for when the string
    // starts with "0"
    for (int i = 0; i < N; i++) {
        if (s[i] == '0') {

            // Adding the no of swaps to
            // fix "1" at odd positions
            ans_0 += abs(k - i);
            k += 2;
        }
    }

    // Returning the answer based on
    // the conditions when string
    // length is even
    if (N % 2 == 0)
        return min(ans_1, ans_0);

    // When string length is odd
    else {

        // When no of ones is greater
        // than no of zeros
        if (ones > zeros)
            return ans_1;

        // When no of ones is greater
        // than no of zeros
        else
            return ans_0;
    }
}

// Driver Code
int main()
{
    string S = "110100";
    cout << minSwaps(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

// Function to find the minimum number
// of adjacent swaps to make the String
// alternating
static int minSwaps(String s)
{
    // Count the no of zeros and ones
    int ones = 0, zeros = 0;
    int N = s.length();

    for (int i = 0; i < N; i++) {
        if (s.charAt(i) == '1')
            ones++;
        else
            zeros++;
    }

    // Base Case
    if ((N % 2 == 0 && ones != zeros)
        || (N % 2 == 1
            && Math.abs(ones - zeros) != 1)) {
        return -1;
    }

    // Store no of min swaps when
    // String starts with "1"
    int ans_1 = 0;

    // Keep track of the odd positions
    int j = 0;

    // Checking for when the String
    // starts with "1"
    for (int i = 0; i < N; i++) {
        if (s.charAt(i) == '1') {

            // Adding the no of swaps to
            // fix "1" at odd positions
            ans_1 += Math.abs(j - i);
            j += 2;
        }
    }

    // Store no of min swaps when String
    // starts with "0"
    int ans_0 = 0;

    // Keep track of the odd positions
    int k = 0;

    // Checking for when the String
    // starts with "0"
    for (int i = 0; i < N; i++) {
        if (s.charAt(i) == '0') {

            // Adding the no of swaps to
            // fix "1" at odd positions
            ans_0 += Math.abs(k - i);
            k += 2;
        }
    }

    // Returning the answer based on
    // the conditions when String
    // length is even
    if (N % 2 == 0)
        return Math.min(ans_1, ans_0);

    // When String length is odd
    else {

        // When no of ones is greater
        // than no of zeros
        if (ones > zeros)
            return ans_1;

        // When no of ones is greater
        // than no of zeros
        else
            return ans_0;
    }
}

// Driver Code
public static void main(String[] args)
{
    String S = "110100";
    System.out.print(minSwaps(S));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum number
# of adjacent swaps to make the string
# alternating
def minSwaps(s):

    # Count the no of zeros and ones
    ones = 0
    zeros = 0
    N = len(s)

    for i in range(N):
        if s[i] == '1':
            ones += 1
        else:
            zeros += 1

    # Base Case
    if ((N % 2 == 0 and ones != zeros) or (N % 2 == 1 and abs(ones - zeros) != 1)):
        return -1

    # Store no of min swaps when
    # string starts with "1"
    ans_1 = 0

    # Keep track of the odd positions
    j = 0

    # Checking for when the string
    # starts with "1"
    for i in range(N):
        if (s[i] == '1'):
            # Adding the no of swaps to
            # fix "1" at odd positions
            ans_1 += abs(j - i)
            j += 2

    # Store no of min swaps when string
    # starts with "0"
    ans_0 = 0

    # Keep track of the odd positions
    k = 0

    # Checking for when the string
    # starts with "0"
    for i in range(N):
        if(s[i] == '0'):

            # Adding the no of swaps to
            # fix "1" at odd positions
            ans_0 += abs(k - i)
            k += 2

    # Returning the answer based on
    # the conditions when string
    # length is even
    if (N % 2 == 0):
        return min(ans_1, ans_0)

    # When string length is odd
    else:

        # When no of ones is greater
        # than no of zeros
        if (ones > zeros):
            return ans_1

        # When no of ones is greater
        # than no of zeros
        else:
            return ans_0

# Driver Code
if __name__ == '__main__':
    S = "110100"
    print(minSwaps(S))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the minimum number
// of adjacent swaps to make the String
// alternating
static int minSwaps(String s)
{
    // Count the no of zeros and ones
    int ones = 0, zeros = 0;
    int N = s.Length;

    for (int i = 0; i < N; i++) {
        if (s[i] == '1')
            ones++;
        else
            zeros++;
    }

    // Base Case
    if ((N % 2 == 0 && ones != zeros)
        || (N % 2 == 1
            && Math.Abs(ones - zeros) != 1)) {
        return -1;
    }

    // Store no of min swaps when
    // String starts with "1"
    int ans_1 = 0;

    // Keep track of the odd positions
    int j = 0;

    // Checking for when the String
    // starts with "1"
    for (int i = 0; i < N; i++) {
        if (s[i] == '1') {

            // Adding the no of swaps to
            // fix "1" at odd positions
            ans_1 += Math.Abs(j - i);
            j += 2;
        }
    }

    // Store no of min swaps when String
    // starts with "0"
    int ans_0 = 0;

    // Keep track of the odd positions
    int k = 0;

    // Checking for when the String
    // starts with "0"
    for (int i = 0; i < N; i++) {
        if (s[i] == '0') {

            // Adding the no of swaps to
            // fix "1" at odd positions
            ans_0 += Math.Abs(k - i);
            k += 2;
        }
    }

    // Returning the answer based on
    // the conditions when String
    // length is even
    if (N % 2 == 0)
        return Math.Min(ans_1, ans_0);

    // When String length is odd
    else {

        // When no of ones is greater
        // than no of zeros
        if (ones > zeros)
            return ans_1;

        // When no of ones is greater
        // than no of zeros
        else
            return ans_0;
    }
}

// Driver Code
public static void Main()
{
    String S = "110100";
    Console.WriteLine(minSwaps(S));

}
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number
        // of adjacent swaps to make the string
        // alternating
        function minSwaps(s)
        {

            // Count the no of zeros and ones
            let ones = 0, zeros = 0;
            let N = s.length;

            for (let i = 0; i < N; i++) {
                if (s.charAt(i) == '1')
                    ones++;
                else
                    zeros++;
            }

            // Base Case
            if ((N % 2 == 0 && ones != zeros)
                || (N % 2 == 1
                    && Math.abs(ones - zeros) != 1)) {
                return -1;
            }

            // Store no of min swaps when
            // string starts with "1"
            let ans_1 = 0;

            // Keep track of the odd positions
            let j = 0;

            // Checking for when the string
            // starts with "1"
            for (let i = 0; i < N; i++) {
                if (s.charAt(i) == '1') {

                    // Adding the no of swaps to
                    // fix "1" at odd positions
                    ans_1 += Math.abs(j - i);
                    j += 2;
                }
            }

            // Store no of min swaps when string
            // starts with "0"
            let ans_0 = 0;

            // Keep track of the odd positions
            let k = 0;

            // Checking for when the string
            // starts with "0"
            for (let i = 0; i < N; i++) {
                if (s.charAt(i) == '0') {

                    // Adding the no of swaps to
                    // fix "1" at odd positions
                    ans_0 += Math.abs(k - i);
                    k += 2;
                }
            }

            // Returning the answer based on
            // the conditions when string
            // length is even
            if (N % 2 == 0)
                return Math.min(ans_1, ans_0);

            // When string length is odd
            else {

                // When no of ones is greater
                // than no of zeros
                if (ones > zeros)
                    return ans_1;

                // When no of ones is greater
                // than no of zeros
                else
                    return ans_0;
            }
        }

        // Driver Code
        let S = "110100";
        document.write(minSwaps(S));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
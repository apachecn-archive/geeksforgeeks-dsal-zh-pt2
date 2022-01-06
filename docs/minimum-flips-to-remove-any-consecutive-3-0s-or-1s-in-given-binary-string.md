# 最小翻转以移除给定二进制字符串中任何连续的 3 个 0 或 1

> 原文:[https://www . geesforgeks . org/minimum-flips-to-remove-any-continuous-3-0s-or-1s-in-给定二进制字符串/](https://www.geeksforgeeks.org/minimum-flips-to-remove-any-consecutive-3-0s-or-1s-in-given-binary-string/)

给定一个由 **N** 个字符组成的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到所需的最小翻转次数，使得不存在三个连续的相同字符。

**示例:**

> **输入:** S = "1100011"
> **输出:** 1
> **解释:**
> 翻转索引 3 处的字符修改没有连续三个相同字符的字符串 S“1101011”。因此，所需的最小翻转次数为 1。
> 
> **输入:**S = " 0001111101 "
> T3】输出: 2

**方法:**给定的问题可以通过考虑每三个连续的字符来解决，如果它们相同，则增加所需翻转的次数，因为需要翻转三个字符中的一个。按照以下步骤解决问题:

*   初始化变量，比如说**将**计数为 **0** ，存储所需的最小翻转次数。
*   如果弦的大小小于或等于 **2、**，则返回 **0** ，因为不需要任何翻转。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–2)**，并执行以下步骤:
    *   如果索引 **i** 、 **(i + 1)** 和 **(i + 2)** 字符处的字符相同，那么将**计数的值**增加 **1** ，将 **i** 的值增加 **3** 。
    *   否则，将 **i** 的值增加 **1** 。
*   执行上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of flips to make all three pairs of
// consecutive characters different
int minFlips(string str)
{
    // Stores resultant count of pairs
    int count = 0;

    // Base Case
    if (str.size() <= 2) {
        return 0;
    }

    // Iterate over the range [0, N - 2]
    for (int i = 0; i < str.size() - 2;) {

        // If the consecutive 3 numbers
        // are the same then increment
        // the count and the counter
        if (str[i] == str[i + 1]
            && str[i + 2] == str[i + 1]) {
            i = i + 3;
            count++;
        }
        else {
            i++;
        }
    }

    // Return the answer
    return count;
}

// Driver Code
int main()
{
    string S = "0011101";
    cout << minFlips(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to find the minimum number
// of flips to make all three pairs of
// consecutive characters different
static int minFlips(String str)
{
    // Stores resultant count of pairs
    int count = 0;

    // Base Case
    if (str.length() <= 2) {
        return 0;
    }

    // Iterate over the range [0, N - 2]
    for (int i = 0; i < str.length() - 2😉 {

        // If the consecutive 3 numbers
        // are the same then increment
        // the count and the counter
        if (str.charAt(i) == str.charAt(i+1)
            && str.charAt(i+2) == str.charAt(i+1)) {
            i = i + 3;
            count++;
        }
        else {
            i++;
        }
    }

    // Return the answer
    return count;
}

// Driver Code
public static void main(String[] args)
{
     String S = "0011101";
   System.out.println(minFlips(S));
}
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python 3 program for the above approach
#
# Function to find the minimum number
# of flips to make all three pairs of
# consecutive characters different
def minFlips(st):

    # Stores resultant count of pairs
    count = 0

    # Base Case
    if (len(st) <= 2):
        return 0

    # Iterate over the range [0, N - 2]
    for i in range(len(st) - 2):

        # If the consecutive 3 numbers
        # are the same then increment
        # the count and the counter
        if (st[i] == st[i + 1]
                and st[i + 2] == st[i + 1]):
            i = i + 3
            count += 1

        else:
            i += 1

    # Return the answer
    return count

# Driver Code
if __name__ == "__main__":

    S = "0011101"
    print(minFlips(S))

    # This code is contributed by ukasp.
```

## java 描述语言

```
  <script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number
        // of flips to make all three pairs of
        // consecutive characters different
        function minFlips(str) {
            // Stores resultant count of pairs
            let count = 0;

            // Base Case
            if (str.length <= 2) {
                return 0;
            }

            // Iterate over the range [0, N - 2]
            for (let i = 0; i < str.length - 2;) {

                // If the consecutive 3 numbers
                // are the same then increment
                // the count and the counter
                if (str[i] == str[i + 1]
                    && str[i + 2] == str[i + 1]) {
                    i = i + 3;
                    count++;
                }
                else {
                    i++;
                }
            }

            // Return the answer
            return count;
        }

        // Driver Code

        let S = "0011101";
        document.write(minFlips(S));

// This code is contributed by Potta Lokesh
    </script>
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to find the minimum number
// of flips to make all three pairs of
// consecutive characters different
static int minFlips(string str)
{
    // Stores resultant count of pairs
    int count = 0;

    // Base Case
    if (str.Length <= 2) {
        return 0;
    }

    // Iterate over the range [0, N - 2]
    for (int i = 0; i < str.Length - 2;) {

        // If the consecutive 3 numbers
        // are the same then increment
        // the count and the counter
        if (str[i] == str[i+1]
            && str[i+2] == str[i+1]) {
            i = i + 3;
            count++;
        }
        else {
            i++;
        }
    }

    // Return the answer
    return count;
}

// Driver Code
public static void Main(string[] args)
{
     string S = "0011101";
     Console.WriteLine(minFlips(S));
}
}

// This code is contributed by AnkThon
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
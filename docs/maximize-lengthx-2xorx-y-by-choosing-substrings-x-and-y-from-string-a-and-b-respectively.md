# 通过分别从字符串 a 和 b 中选择子字符串 x 和 y 来最大化[length(X)/2^(XOR(X，y])

> 原文:[https://www . geesforgeks . org/maximize-length x-2xorx-y-by-choice-substrings-x-和-y-from-string-a-和-b-分别/](https://www.geeksforgeeks.org/maximize-lengthx-2xorx-y-by-choosing-substrings-x-and-y-from-string-a-and-b-respectively/)

给定两个大小分别为 **N** 和 **M** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **A** 和 **B** ，任务是通过从给定字符串 **A** 和**中选择两个长度相等的子字符串 **X** 和 **Y** 来最大化**长度为(X) / 2 <sup>XOR(X，Y)</sup>** 的值**

**示例:**

> **输入:**A =“0110”，B =“1101”
> **输出:** 3
> **解释:**
> 分别从字符串 A 和 B 中选择子字符串“110”和“110”。长度(X) / 2 <sup>XOR(X，Y)</sup> 表达式的值为 3 / 2 <sup>0</sup> = 3，在所有可能的组合中最大。
> 
> **输入:**A =“1111”，B =“0000”
> T3】输出: 0

**方法:**给定的问题可以通过观察需要最大化的表达式来解决，因此分母必须是**最小值**，为了使其最小化，子串 **X** 和 **Y** 的[按位异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)的值必须是最小值，即**零**，并使[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的值为**零**，这两个[子串因此，问题简化为寻找两个](https://www.geeksforgeeks.org/substring-in-cpp/)[字符串](https://www.geeksforgeeks.org/string-data-structure/) **A** 和 **B** 的[最长公共子串](https://www.geeksforgeeks.org/longest-common-substring-dp-29/)。按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说**lcsuf【M+1】【N+1】**来存储[子串](https://www.geeksforgeeks.org/substring-in-cpp/)最长公共后缀的长度。
*   初始化一个变量，将**结果**设为 **0** 来存储给定表达式的结果最大值。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，使用变量 **j** 嵌套迭代范围**【0，N】**，并执行以下步骤:
    *   如果 **i** 等于 **0** 或 **j** 等于 **0** ，则更新**LCSSuff【I】【j】**等于 **0** 的值。
    *   否则，如果**A[I–1]**的值等于**A[j–1]**，则将 **LCSSuff[i][j]** 的值更新为**LCSSuff[I–1][j–1]+1**，将**结果**的值更新为**结果**和 **LCSSuff[i][j]** 的**最大值。**
    *   否则，将 **LCSSuff[i][j]** 的值更新为 **0** 。
*   完成以上步骤后，打印**结果**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest common substring of the
// string X and Y
int LCSubStr(char* A, char* B, int m, int n)
{
    // LCSuff[i][j] stores the lengths
    // of the longest common suffixes
    // of substrings
    int LCSuff[m + 1][n + 1];
    int result = 0;

    // Iterate over strings A and B
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {

            // If first row or column
            if (i == 0 || j == 0)
                LCSuff[i][j] = 0;

            // If matching is found
            else if (A[i - 1] == B[j - 1]) {
                LCSuff[i][j]
                    = LCSuff[i - 1][j - 1]
                      + 1;
                result = max(result,
                             LCSuff[i][j]);
            }

            // Otherwise, if matching
            // is not found
            else
                LCSuff[i][j] = 0;
        }
    }

    // Finally, return the resultant
    // maximum value LCS
    return result;
}

// Driver Code
int main()
{
    char A[] = "0110";
    char B[] = "1101";
    int M = strlen(A);
    int N = strlen(B);

    // Function Call
    cout << LCSubStr(A, B, M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the length of the
// longest common substring of the
// string X and Y
static int lcsubtr(char a[], char b[], int length1,
                   int length2)
{

    // LCSuff[i][j] stores the lengths
    // of the longest common suffixes
    // of substrings
    int dp[][] = new int[length1 + 1][length2 + 1];
    int max = 0;

    // Iterate over strings A and B
    for(int i = 0; i <= length1; ++i)
    {
        for(int j = 0; j <= length2; ++j)
        {

            // If first row or column
            if (i == 0 || j == 0)
            {
                dp[i][j] = 0;
            }

            // If matching is found
            else if (a[i - 1] == b[j - 1])
            {
                dp[i][j] = dp[i - 1][j - 1] + 1;
                max = Math.max(dp[i][j], max);
            }

            // Otherwise, if matching
            // is not found
            else
            {
                dp[i][j] = 0;
            }
        }
    }

    // Finally, return the resultant
    // maximum value LCS
    return max;
}

// Driver Code
public static void main(String[] args)
{
    String m = "0110";
    String n = "1101";
    char m1[] = m.toCharArray();
    char m2[] = n.toCharArray();

    // Function Call
    System.out.println(lcsubtr(m1, m2, m1.length,
                                       m2.length));
}
}

// This code is contributed by zack_aayush
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the length of the
# longest common substring of the
# string X and Y
def LCSubStr(A, B, m, n):

    # LCSuff[i][j] stores the lengths
    # of the longest common suffixes
    # of substrings
    LCSuff = [[0 for i in range(n+1)] for j in range(m+1)]
    result = 0

    # Iterate over strings A and B
    for i in range(m + 1):
        for j in range(n + 1):

            # If first row or column
            if (i == 0 or j == 0):
                LCSuff[i][j] = 0

            # If matching is found
            elif(A[i - 1] == B[j - 1]):
                LCSuff[i][j] = LCSuff[i - 1][j - 1] + 1
                result = max(result,LCSuff[i][j])

            # Otherwise, if matching
            # is not found
            else:
                LCSuff[i][j] = 0

    # Finally, return the resultant
    # maximum value LCS
    return result

# Driver Code
if __name__ == '__main__':
    A = "0110"
    B = "1101"
    M = len(A)
    N = len(B)

    # Function Call
    print(LCSubStr(A, B, M, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the length of the
// longest common substring of the
// string X and Y
static int lcsubtr(char[] a, char[] b, int length1,
                   int length2)
{

    // LCSuff[i][j] stores the lengths
    // of the longest common suffixes
    // of substings
    int[,] dp = new int[length1 + 1, length2 + 1];
    int max = 0;

    // Iterate over strings A and B
    for(int i = 0; i <= length1; ++i)
    {
        for(int j = 0; j <= length2; ++j)
        {

            // If first row or column
            if (i == 0 || j == 0)
            {
                dp[i, j] = 0;
            }

            // If matching is found
            else if (a[i - 1] == b[j - 1])
            {
                dp[i, j] = dp[i - 1, j - 1] + 1;
                max = Math.Max(dp[i, j], max);
            }

            // Otherwise, if matching
            // is not found
            else
            {
                dp[i, j] = 0;
            }
        }
    }

    // Finally, return the resultant
    // maximum value LCS
    return max;
}

// Driver Code
public static void Main()
{
    string m = "0110";
    string n = "1101";
    char[] m1 = m.ToCharArray();
    char[] m2 = n.ToCharArray();

    // Function Call
    Console.Write(lcsubtr(m1, m2, m1.Length,
                                       m2.Length));
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the length of the
        // longest common substring of the
        // string X and Y
        function LCSubStr(A, B, m, n)
        {

            // LCSuff[i][j] stores the lengths
            // of the longest common suffixes
            // of substrings
            let LCSuff = Array(m + 1).fill(Array(n + 1));
            let result = 0;

            // Iterate over strings A and B
            for (let i = 0; i <= m; i++) {
                for (let j = 0; j <= n; j++) {

                    // If first row or column
                    if (i == 0 || j == 0)
                        LCSuff[i][j] = 0;

                    // If matching is found
                    else if (A.charAt(i - 1) == B.charAt(j - 1)) {
                        LCSuff[i][j] = LCSuff[i - 1][j - 1] + 1;
                        if (LCSuff[i][j] > result) {
                            result = LCSuff[i][j];
                        }
                    }

                    // Otherwise, if matching
                    // is not found
                    else
                        LCSuff[i][j] = 0;
                }
            }
            result++;
            // Finally, return the resultant
            // maximum value LCS
            return result;
        }

        // Driver Code

        let A = "0110";
        let B = "1101";
        let M = A.length;
        let N = B.length;

        // Function Call
        document.write(LCSubStr(A, B, M, N));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
3
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(M*N)*
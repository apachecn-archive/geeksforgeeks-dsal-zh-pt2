# 最小化将所有 0 转换为 1 的成本，转换 0 组的成本为 X，转换 1 组的成本为 X/3

> 原文:[https://www . geeksforgeeks . org/最小化将所有 0 转换为 1 的成本-转换 0 的成本-组-be-x-和 1 的那个-be-x-3/](https://www.geeksforgeeks.org/minimize-cost-to-convert-all-0s-to-1s-with-cost-of-converting-0s-group-be-x-and-that-of-1-be-x-3/)

给定二进制字符串 **str** ，仅由两个字符“ **1** ”和“ **0** ”以及一个整数 **X** 组成，任务是计算将所有字符转换为**“1”的最小成本。**将一个**‘0’**转换为**‘1’**的成本为 **X** ，将一个**‘1’**转换为**‘0’**的成本为 **X** **/ 3** 。如果一个**“0”**被转换为**“1”**，那么与其左右相邻的所有 **0** 将被转换为**“1”**而不产生任何费用。

**示例:**

> **输入:**str =“101001”，X = 6
> **输出:** 8
> **说明:**将索引 2 处的字符即‘1’替换为‘0’，这将花费 6 / 3 =2 的成本，然后将其更改回成本为 6 的‘1’，使字符串变为“111111”
> 
> **输入:** str = "10110100 "，X = 3
> T3】输出: 6

**方法:**给定的问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决。可以遵循以下步骤来解决问题:

*   声明一个数组 **dp[]** 来存储计算出的答案
*   用 **INT_MAX** 初始化第一个元素
*   如果字符串的第一个字符是“ **0** ，用 **K** 重新初始化 **dp[]** 的第一个元素。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **字符串**，检查以下情况:
    *   如果字符是“ **1** ”，并且如果 **dp[i-1]** 不等于 **INT_MAX，**将**和**加 1
    *   否则，如果字符是“ **0** ”:
        *   dp[i-1]等于 **INT_MAX** ，设置 **dp[i]** **= k**
        *   如果前一个字符不等于“ **0** ”，计算最小值并将其分配给 **dp[i]**
*   返回 **dp[N]** ，这是期望的答案

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum cost required
// to replace all Bs with As
int replaceZerosWithOnes(string str,
                         int K, int N)
{
    // Declare an array to store
    // the temporary answer
    int dp[N + 1] = { 0 };

    // Initialize the dp[0] with INT_MAX
    dp[0] = INT_MAX;

    int sum = 0;

    // If character is 'B'
    if (str[0] == '0') {

        // Re-initialize dp[0] to K
        dp[0] = K;
    }

    for (int i = 1; i < N; i++) {

        // If current character
        // is equal to A
        if (str[i] == '1') {

            // If dp[i-1] is not equal
            // to INT_MAX
            if (dp[i - 1] != INT_MAX) {

                // Increment sum by 1
                sum++;
            }

            dp[i] = dp[i - 1];
        }

        // If current character is 'B'
        // and dp[i-1] is equal to
        // INT_MAX
        else if (str[i] == '0'
                 && dp[i - 1] == INT_MAX) {

            // Set dp[i] = k
            dp[i] = K;
        }

        // If current character is 'B' and
        // previous character was not 'B'
        else if (str[i] == '0'
                 && str[i - 1] != '0') {

            // Calculate the minimum
            // value and assign it to dp[i]
            dp[i] = min((dp[i - 1] + (sum * K / 3)),
                        dp[i - 1] + K);

            sum = 0;
        }

        // Else move next
        else
            dp[i] = dp[i - 1];
    }

    // Return last element stored in dp
    return dp[N - 1];
}

// Driver Code
int main()
{
    string str = "10110100";
    int N = str.size();
    int K = 3;

    // Print the result of the function
    cout << replaceZerosWithOnes(str, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find minimum cost required
// to replace all Bs with As
static int replaceZerosWithOnes(String str,
                         int K, int N)
{
    // Declare an array to store
    // the temporary answer
    int dp[] = new int[N + 1];

    for (int i = 0; i < N + 1; i++)
            dp[i] = 0;

    // Initialize the dp[0] with INT_MAX
    dp[0] = Integer.MAX_VALUE;

    int sum = 0;

    // If character is 'B'
    if (str.charAt(0) == '0') {

        // Re-initialize dp[0] to K
        dp[0] = K;
    }

    for (int i = 1; i < N; i++) {

        // If current character
        // is equal to A
        if (str.charAt(i) == '1') {

            // If dp[i-1] is not equal
            // to INT_MAX
            if (dp[i - 1] != Integer.MAX_VALUE) {

                // Increment sum by 1
                sum++;
            }

            dp[i] = dp[i - 1];
        }

        // If current character is 'B'
        // and dp[i-1] is equal to
        // INT_MAX
        else if (str.charAt(i) == '0'
                 && dp[i - 1] == Integer.MAX_VALUE) {

            // Set dp[i] = k
            dp[i] = K;
        }

        // If current character is 'B' and
        // previous character was not 'B'
        else if (str.charAt(i) == '0'
                 && str.charAt(i - 1) != '0') {

            // Calculate the minimum
            // value and assign it to dp[i]
            dp[i] = Math.min((dp[i - 1] + (sum * K / 3)),
                        dp[i - 1] + K);

            sum = 0;
        }

        // Else move next
        else
            dp[i] = dp[i - 1];
    }

    // Return last element stored in dp
    return dp[N - 1];
}

// Driver code
public static void main(String args[])
{
    String str = "10110100";
    int N = str.length();
    int K = 3;

    // Print the result of the function
    System.out.println(replaceZerosWithOnes(str, K, N));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python implementation for the above approach

INT_MAX = 2147483647

# Function to find minimum cost required
# to replace all Bs with As

def replaceZerosWithOnes(str, K, N):

    # Declare an array to store
    # the temporary answer
    dp = [0 for _ in range(N + 1)]

    # Initialize the dp[0] with INT_MAX
    dp[0] = INT_MAX

    sum = 0

    # If character is 'B'
    if (str[0] == '0'):

        # Re-initialize dp[0] to K
        dp[0] = K

    for i in range(1, N):

        # If current character
        # is equal to A
        if (str[i] == '1'):

            # If dp[i-1] is not equal
            # to INT_MAX
            if (dp[i - 1] != INT_MAX):

                # Increment sum by 1
                sum += 1

            dp[i] = dp[i - 1]

        # If current character is 'B'
        # and dp[i-1] is equal to
        # INT_MAX
        elif (str[i] == '0' and dp[i - 1] == INT_MAX):

            # Set dp[i] = k
            dp[i] = K

        # If current character is 'B' and
        # previous character was not 'B'
        elif (str[i] == '0' and str[i - 1] != '0'):

            # Calculate the minimum
            # value and assign it to dp[i]
            dp[i] = min((dp[i - 1] + ((sum * K) // 3)), dp[i - 1] + K)

            sum = 0

        # Else move next
        else:
            dp[i] = dp[i - 1]

    # Return last element stored in dp
    return dp[N - 1]

# Driver Code
if __name__ == "__main__":

    str = "10110100"
    N = len(str)
    K = 3

    # Print the result of the function
    print(replaceZerosWithOnes(str, K, N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach

using System;
using System.Collections;
class GFG{

// Function to find minimum cost required
// to replace all Bs with As
static int replaceZerosWithOnes(string str,
                         int K, int N)
{

    // Declare an array to store
    // the temporary answer
    int []dp = new int[N + 1];

    for (int i = 0; i < N + 1; i++)
            dp[i] = 0;

    // Initialize the dp[0] with INT_MAX
    dp[0] = Int32.MaxValue;

    int sum = 0;

    // If character is 'B'
    if (str[0] == '0') {

        // Re-initialize dp[0] to K
        dp[0] = K;
    }

    for (int i = 1; i < N; i++) {

        // If current character
        // is equal to A
        if (str[i] == '1') {

            // If dp[i-1] is not equal
            // to INT_MAX
            if (dp[i - 1] != Int32.MaxValue) {

                // Increment sum by 1
                sum++;
            }

            dp[i] = dp[i - 1];
        }

        // If current character is 'B'
        // and dp[i-1] is equal to
        // INT_MAX
        else if (str[i] == '0'
                 && dp[i - 1] == Int32.MaxValue) {

            // Set dp[i] = k
            dp[i] = K;
        }

        // If current character is 'B' and
        // previous character was not 'B'
        else if (str[i] == '0'
                 && str[i - 1] != '0') {

            // Calculate the minimum
            // value and assign it to dp[i]
            dp[i] = Math.Min((dp[i - 1] + (sum * K / 3)),
                        dp[i - 1] + K);

            sum = 0;
        }

        // Else move next
        else
            dp[i] = dp[i - 1];
    }

    // Return last element stored in dp
    return dp[N - 1];
}

// Driver code
public static void Main()
{
    string str = "10110100";
    int N = str.Length;
    int K = 3;

    // Print the result of the function
    Console.Write(replaceZerosWithOnes(str, K, N));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find minimum cost required
        // to replace all Bs with As
        function replaceZerosWithOnes(str,
            K, N) {

            // Declare an array to store
            // the temporary answer
            let dp = new Array(N + 1).fill(0)

            // Initialize the dp[0] with INT_MAX
            dp[0] = Number.MAX_VALUE;

            let sum = 0;

            // If character is 'B'
            if (str[0] == '0') {

                // Re-initialize dp[0] to K
                dp[0] = K;
            }

            for (let i = 1; i < N; i++) {

                // If current character
                // is equal to A
                if (str[i] == '1') {

                    // If dp[i-1] is not equal
                    // to INT_MAX
                    if (dp[i - 1] != Number.MAX_VALUE) {

                        // Increment sum by 1
                        sum++;
                    }

                    dp[i] = dp[i - 1];
                }

                // If current character is 'B'
                // and dp[i-1] is equal to
                // INT_MAX
                else if (str[i] == '0'
                    && dp[i - 1] == Number.MAX_VALUE) {

                    // Set dp[i] = k
                    dp[i] = K;
                }

                // If current character is 'B' and
                // previous character was not 'B'
                else if (str[i] == '0'
                    && str[i - 1] != '0') {

                    // Calculate the minimum
                    // value and assign it to dp[i]
                    dp[i] = Math.min((dp[i - 1] + (sum * K / 3)),
                        dp[i - 1] + K);

                    sum = 0;
                }

                // Else move next
                else
                    dp[i] = dp[i - 1];
            }

            // Return last element stored in dp
            return dp[N - 1];
        }

        // Driver Code
        let str = "10110100";
        let N = str.length;
        let K = 3;

        // Print the result of the function
        document.write(replaceZerosWithOnes(str, K, N));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
6
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
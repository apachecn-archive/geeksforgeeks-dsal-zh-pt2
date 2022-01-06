# 二进制形式不是给定二进制串的子序列的最小数

> 原文:[https://www . geesforgeks . org/最小数-其二进制形式不是给定二进制字符串的子序列/](https://www.geeksforgeeks.org/minimum-number-whose-binary-form-is-not-a-subsequence-of-given-binary-string/)

给定大小为 **N** 、的[二进制字符串](https://www.geeksforgeeks.org/python-check-if-a-given-string-is-binary-string-or-not/) **S** ，任务是找到最小非负整数，该整数不是给定字符串 **S** 的[二进制形式](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)的[子序列](http://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:** S = "0000"
> **输出:** 1
> **说明:** 1 的二进制表示为“1”是最小的非负整数，它不是给定字符串的二进制形式的子序列。
> 
> **输入:**S = " 10101 "
> T3】输出: 8

**方法:**想法是[把给定的字符串转换成它的十进制表示](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)，比如 **R** 。然后[在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，R】**中迭代，检查每个整数在给定字符串 **S** 中是否作为二进制形式的子序列存在。如果没有，则[断开循环](https://www.geeksforgeeks.org/break-statement-cc/)并打印所需结果。
按照以下步骤解决问题:

*   将二进制字符串、 **S** 的[十进制数存储在变量 **R** 中。](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)
*   将变量**和**初始化为 **R+1** 来存储所需的结果。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，R】**中迭代
    *   [将给定的整数 **i** 转换为其二进制字符串](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)，并存储在[字符串](https://www.geeksforgeeks.org/string-data-structure/)T6【P】T7 中。
    *   [检查字符串 **P** 是否为字符串 **S** 的子序列](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/)。如果不是，那么更新 **ans** 到 **i** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if string str1 is a
// subsequence of string str2
bool isSubsequence(string str1, string str2, int m, int n)
{
    // Store index of str1
    int j = 0;

    // Traverse str2 and str1, and compare
    // current character of str2 with first
    // unmatched char of str1
    for (int i = 0; i < n && j < m; i++)

        // If matched, move ahead in str1
        if (str1[j] == str2[i])
            j++;

    // If all characters of str1 were
    // found in str2
    return (j == m);
}

// Function to find the minimum number which
// is not a subsequence of the given binary
// string in its binary form
void findMinimumNumber(string s)
{
    // Store the decimal number of string, S
    int r = stoi(s, 0, 2);
    // Initialize the required result
    int ans = r + 1;

    // Iterate in the range [0, R]
    for (int i = 0; i <= r; i++) {

        // Convert integer i to binary string
        string p = "";
        int j = i;
        while (j > 0) {
            p += to_string(j % 2);
            j = j / 2;
        }

        int m = p.length();
        int n = s.length();
        reverse(p.begin(), p.end());

        // Check if the string is not a subsequence
        if (!isSubsequence(p, s, m, n)) {

            // Update ans and break
            ans = i;
            break;
        }
    }

    // Print the required result
    cout << ans;
}

// Driver Code
int main()
{

    // Function Call
    string s = "10101";

    // Function Call
    findMinimumNumber(s);

    return 0;
}
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to check if string str1 is a
# subsequence of string str2
def isSubsequence(str1, str2, m, n):
    # Store index of str1
    j = 0

    # Traverse str2 and str1, and compare
    # current character of str2 with first
    # unmatched char of str1
    i = 0
    while(i < n and j < m):
        # If matched, move ahead in str1
        if (str1[j] == str2[i]):
            j += 1
        i += 1

    # If all characters of str1 were
    # found in str2
    return (j == m)

# Function to find the minimum number which
# is not a subsequence of the given binary
# string in its binary form
def findMinimumNumber(s):
    # Store the decimal number of string, S
    r = int(s,2)

    # Initialize the required result
    ans = r + 1

    # Iterate in the range [0, R]
    for i in range(r+1):
        # Convert integer i to binary string
        p = ""
        j = i
        while (j > 0):
            p += str(j % 2)
            j = j // 2

        m = len(p)
        n = len(s)
        p = p[::-1]

        # Check if the string is not a subsequence
        if (isSubsequence(p, s, m, n) == False):
            # Update ans and break
            ans = i
            break

    # Print the required result
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Function Call
    s = "10101"

    # Function Call
    findMinimumNumber(s)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG {
    // Function to check if string str1 is a
    // subsequence of string str2
    static bool isSubsequence(string str1, string str2,
                              int m, int n)
    {
        // Store index of str1
        int j = 0;

        // Traverse str2 and str1, and compare
        // current character of str2 with first
        // unmatched char of str1
        for (int i = 0; i < n && j < m; i++)

            // If matched, move ahead in str1
            if (str1[j] == str2[i])
                j++;

        // If all characters of str1 were
        // found in str2
        return (j == m);
    }

    // Function to find the minimum number which
    // is not a subsequence of the given binary
    // string in its binary form
    static void findMinimumNumber(string s)
    {
        // Store the decimal number of string, S
        int r = Int32.Parse(s);
        // Initialize the required result
        int ans = r + 1;

        // Iterate in the range [0, R]
        for (int i = 0; i <= r; i++) {

            // Convert integer i to binary string
            string p = "";
            int j = i;
            while (j > 0) {
                p += (j % 2).ToString();
                j = j / 2;
            }

            int m = p.Length;
            int n = s.Length;
            char[] stringArray = p.ToCharArray();
            Array.Reverse(stringArray);
            p = new string(stringArray);

            // Check if the string is not a subsequence
            if (!isSubsequence(p, s, m, n)) {

                // Update ans and break
                ans = i;
                break;
            }
        }

        // Print the required result
        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main()
    {

        // Function Call
        string s = "10101";

        // Function Call
        findMinimumNumber(s);
    }
}

// This code is contributed by ukasp.
```

**Output**

```
8
```

***时间复杂度:** O(N*R)，其中 R 是给定二进制字符串的十进制表示， **S***
***辅助空间:** O(N)*
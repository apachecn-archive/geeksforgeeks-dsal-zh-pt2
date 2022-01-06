# 给定字符串数组中超弦的计数

> 原文:[https://www . geesforgeks . org/给定字符串数组中的超弦计数/](https://www.geeksforgeeks.org/count-of-superstrings-in-a-given-array-of-strings/)

给定 2 组[弦](https://www.geeksforgeeks.org/string-data-structure/) **X** 和 **Y** 的数组，任务是找出 X 中超弦的个数。

> 一根弦 **s** 被称为超弦，如果数组中出现的每根弦 **Y** 都是弦 **s** 的子序列。

**示例:**

> **输入**:X = {“ceo”、“alco”、“caaeio”、“ceai”}，Y = {“EC”、“oc”、“CEO”}
> **输出** : 2
> **说明**:字符串“CEO”和“caaeio”都是超弦，因为数组 Y 的每个字符串都是这 2 个字符串的子集。其他字符串不包含在答案中，数组 Y 的所有字符串都不是它们的
> 子集。
> 
> **输入**:x = { " iopo "，" oaai "，" iipo " }，y = { " oo " }
> **输出** : 1

**方法:**思路是利用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)的概念来存储字符的[频率来解决问题。按照以下步骤解决问题:](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)

*   初始化一个大小为 26 的[数组](https://www.geeksforgeeks.org/array-data-structure/)，以存储数组 **Y** 中每个字符串中每个字符【a-z】的最大出现次数。
*   现在考虑 X 中的每个字符串 **s** ，
    *   检查 **s** 中每个字符的频率是否大于或等于从上述步骤获得的频率

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <iostream>
using namespace std;

// Function to find total number of superstrings
int superstring(string X[], string Y[], int N, int M)
{

    // Array to store max frequency
    // Of each letter
    int maxFreq[26];
    for (int i = 0; i < 26; i++)
        maxFreq[i] = 0;

    for (int j = 0; j < M; j++) {
        int temp[26];
        for (int i = 0; i < 26; i++)
            temp[i] = 0;
        for (int k = 0; k < Y[j].size(); k++) {
            temp[Y[j][k] - 'a']++;
        }
        for (int i = 0; i < 26; i++) {
            maxFreq[i] = max(maxFreq[i], temp[i]);
        }
    }

    int ans = 0;
    for (int j = 0; j < N; j++) {

        // Array to find frequency of each letter in string
        // x
        int temp[26];
        for (int i = 0; i < 26; i++)
            temp[i] = 0;
        for (int k = 0; k < X[j].size(); k++) {
            temp[X[j][k] - 'a']++;
        }
        int i = 0;
        for (i = 0; i < 26; i++) {

            // If any frequency is less in string x than
            // maxFreq, then it can't be a superstring
            if (temp[i] < maxFreq[i]) {
                break;
            }
        }
        if (i == 26) {

            // Increment counter of x is a superstring
            ans++;
        }
    }
    return ans;
}

// Driver code
int main()
{
    // Size of array X
    int N = 4;
    // Size of array Y
    int M = 3;

    string X[N] = { "ceo", "alco", "caaeio", "ceai" };
    string Y[M] = { "ec", "oc", "ceo" };

    cout << superstring(X, Y, N, M); // Function call
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;

class GFG {

    // Function to find total number of superstrings
    public static int superString(String X[], String Y[],
                                  int N, int M)
    {

        // Array to store max frequency
        // Of each letter
        int[] maxFreq = new int[26];
        for (int i = 0; i < 26; i++)
            maxFreq[i] = 0;

        for (int j = 0; j < M; j++) {
            int[] temp = new int[26];
            for (int k = 0; k < Y[j].length(); k++) {
                temp[Y[j].charAt(k) - 'a']++;
            }
            for (int i = 0; i < 26; i++) {
                maxFreq[i] = Math.max(maxFreq[i], temp[i]);
            }
        }

        int ans = 0;
        for (int j = 0; j < N; j++) {

            // Array to find frequency of each letter in
            // string x
            int[] temp = new int[26];
            for (int i = 0; i < 26; i++)
                temp[i] = 0;
            for (int k = 0; k < X[j].length(); k++) {
                temp[X[j].charAt(k) - 'a']++;
            }

            int i = 0;
            for (i = 0; i < 26; i++) {

                // If any frequency is less in string x than
                // maxFreq, then it can't be a superstring
                if (temp[i] < maxFreq[i]) {
                    break;
                }
            }
            if (i == 26) {

                // Increment counter of x is a superstring
                ans++;
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        String[] X = new String[] { "ceo", "alco", "caaeio",
                                    "ceai" };
        String[] Y = new String[] { "ec", "oc", "ceo" };

        System.out.println(
            superString(X, Y, X.length, Y.length));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation for the above approach

# Function to find total number of superstrings
def superstring(X, Y, N, M):

    # Array to store max frequency
    # Of each letter
    maxFreq = [0] * 26

    for j in range(M):
        temp = [0] * 26
        for k in range(len(Y[j])):
            temp[ord(Y[j][k]) - ord('a')] += 1
        for i in range(26):
            maxFreq[i] = max(maxFreq[i], temp[i])

    ans = 0
    for j in range(N):

        # Array to find frequency of each letter
        # in string x
        temp = [0] * 26
        for k in range(len(X[j])):
            temp[ord(X[j][k]) - ord('a')] += 1

        i = 0

        while i < 26:

            # If any frequency is less in x than
            # maxFreq, then it can't be a superstring
            if (temp[i] < maxFreq[i]):
                break
            i += 1
        if (i == 26):

            # Increment counter of x is a superstring
            ans += 1

    return ans

# Driver code
if __name__ == '__main__':

    # Size of array X
    N = 4

    # Size of array Y
    M = 3

    X = ["ceo", "alco", "caaeio", "ceai"]
    Y = [ "ec", "oc", "ceo" ]

    print(superstring(X, Y, N, M)) #Function call

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find total number of superstrings
    public static int superString(string[] X, string[] Y,
                                  int N, int M)
    {

        // Array to store max frequency
        // Of each letter
        int[] maxFreq = new int[26];
        for (int i = 0; i < 26; i++)
            maxFreq[i] = 0;

        for (int j = 0; j < M; j++) {
            int[] temp = new int[26];
            for (int k = 0; k < Y[j].Length; k++) {
                temp[Y[j][k] - 'a']++;
            }
            for (int i = 0; i < 26; i++) {
                maxFreq[i] = Math.Max(maxFreq[i], temp[i]);
            }
        }

        int ans = 0;
        for (int j = 0; j < N; j++) {

            // Array to find frequency of each letter in
            // string x
            int[] temp = new int[26];
            int i =0;
            for ( i = 0; i < 26; i++)
                temp[i] = 0;
            for (int k = 0; k < X[j].Length; k++) {
                temp[X[j][k] - 'a']++;
            }

            for ( i = 0; i < 26; i++) {

                // If any frequency is less in string x than
                // maxFreq, then it can't be a superstring
                if (temp[i] < maxFreq[i]) {
                    break;
                }
            }
            if ( i == 26) {

                // Increment counter of x is a superstring
                ans++;
            }
        }
        return ans;
    }

// Driver code
static void Main()
{
    string[] X = new String[] { "ceo", "alco", "caaeio",
                                    "ceai" };
        string[] Y = new String[] { "ec", "oc", "ceo" };

        Console.Write(
            superString(X, Y, X.Length, Y.Length));
}
}

// This code is contributed b sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find total number of superstrings
    function superString(X, Y, N, M)
    {

        // Array to store max frequency
        // Of each letter
        let maxFreq = Array.from({length: 26}, (_, i) => 0);
        for (let i = 0; i < 26; i++)
            maxFreq[i] = 0;

        for (let j = 0; j < M; j++) {
            let temp = Array.from({length: 26}, (_, i) => 0);
            for (let k = 0; k < Y[j].length; k++) {
                temp[Y[j][k].charCodeAt() - 'a'.charCodeAt()]++;
            }
            for (let i = 0; i < 26; i++) {
                maxFreq[i] = Math.max(maxFreq[i], temp[i]);
            }
        }

        let ans = 0;
        for (let j = 0; j < N; j++) {

            // Array to find frequency of each letter in
            // string x
            let temp = Array.from({length: 26}, (_, i) => 0);
            for (let i = 0; i < 26; i++)
                temp[i] = 0;
            for (let k = 0; k < X[j].length; k++) {
                temp[X[j][k].charCodeAt() - 'a'.charCodeAt()]++;
            }

            let i = 0;
            for (i = 0; i < 26; i++) {

                // If any frequency is less in string x than
                // maxFreq, then it can't be a superstring
                if (temp[i] < maxFreq[i]) {
                    break;
                }
            }
            if (i == 26) {

                // Increment counter of x is a superstring
                ans++;
            }
        }
        return ans;
    }

    // Driver Code

        let X = [ "ceo", "alco", "caaeio",
                                    "ceai" ];
        let Y = [ "ec", "oc", "ceo" ];

        document.write(
            superString(X, Y, X.length, Y.length));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N*N1 + M*M1)，其中 N =数组 X 的大小，N1 = Maxlength(x)，M =数组 Y 的大小，M1 = Maxlength(y)，

**空间复杂度:** O(1)
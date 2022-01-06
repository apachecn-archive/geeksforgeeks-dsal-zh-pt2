# 长度为 4 的子序列计数，形式为(x，x，x+1，x+1) |集合 2

> 原文:[https://www . geesforgeks . org/长度为 4 的子序列计数-in-form-x-x-x1-x1-set-2/](https://www.geeksforgeeks.org/count-of-subsequences-of-length-4-in-form-x-x-x1-x1-set-2/)

给定大量大小为 **N** 的字符串 **str** ，任务是[计算长度为 4 的子序列](https://www.geeksforgeeks.org/count-subsequence-of-length-three-in-a-given-string/)，其位数为 **(x，x，x+1，x+1)** 。
**示例:**

> **输入:** str = "1515732322"
> **输出:** 3
> **说明:**
> 对于给定的输入字符串 str = "1515732322 "，有 3 个子序列{1122}、{1122}和{1122}，它们的给定形式为(x，x，x+1，x+1)。
> 
> **输入:** str = "224353"
> **输出:** 1
> **解释:**
> 对于给定的输入字符串 str = "224353 "，给定形式的(x，x，x+1，x+1)只有一个可能的子序列{2233}。

**前缀和方法:**前缀和方法请参考[集 1](https://www.geeksforgeeks.org/count-of-sub-sequences-which-satisfy-the-given-condition/) 。

**动态规划法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。
我们将使用 2 个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)作为 **count1[][j]** 和 **count2[][10]** ，这样 **count1[i][10]** 将存储当前索引处**数字 j** 的连续相等元素的计数 **i** 从左侧遍历字符串，而 **count2[i][j]** 将存储**的连续相等元素的计数以下是步骤:**

*   初始化两个计数数组**从左到右填充表格的计数 1[][10]** 和从右到左填充表格的计数 2[][10] 。
*   遍历输入字符串并填充 count1 和 count2 数组。
*   **计数 1[][]** 的递推关系由下式给出:

> count1[i][j]+= count 1[I–1][j]
> 其中 count 1[I][j]是数字 j 的索引 I 处两个相邻的计数

*   **计数 2[][]** 的递推关系由下式给出:

> count2[i][j]+= count 1[I+1][j]
> 其中 count 2[I][j]是数字 j 的索引 I 处两个相邻的计数

*   初始化一个变量 **ans 为 0** ，该变量存储稳定数字的结果计数。
*   遍历输入字符串，从 **count1[][]** 和 **count2[][]** 数组中获取数字计数，使 **count1[][]** 和 **count2[][]** 数组中的数字之差为 1，并将其存储在变量 **c1** 和 **c2 中。**
*   最后用**(C1 *(C2 *(C2–1)/2))**更新结果(说 **ans** )。
*   打印上面计算的答案**和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the numbers
int countStableNum(string str, int N)
{
    // Array that stores the
    // digits from left to right
    int count1[N][10];

    // Array that stores the
    // digits from right to left
    int count2[N][10];

    // Initially both array store zero
    for (int i = 0; i < N; i++)
        for (int j = 0; j < 10; j++)
            count1[i][j] = count2[i][j] = 0;

    // Fill the table for count1 array
    for (int i = 0; i < N; i++) {
        if (i != 0) {
            for (int j = 0; j < 10; j++) {
                count1[i][j] += count1[i - 1][j];
            }
        }

        // Update the count of current character
        count1[i][str[i] - '0']++;
    }

    // Fill the table for count2 array
    for (int i = N - 1; i >= 0; i--) {
        if (i != N - 1) {
            for (int j = 0; j < 10; j++) {
                count2[i][j] += count2[i + 1][j];
            }
        }

        // Update the count of cuuent character
        count2[i][str[i] - '0']++;
    }

    // Variable that stores the
    // count of the numbers
    int ans = 0;

    // Traverse Input string and get the
    // count of digits from count1 and
    // count2 array such that difference
    // b/w digit is 1 & store it int c1 &c2.
    // And store it in variable c1 and c2
    for (int i = 1; i < N - 1; i++) {

        if (str[i] == '9')
            continue;

        int c1 = count1[i - 1][str[i] - '0'];
        int c2 = count2[i + 1][str[i] - '0' + 1];

        if (c2 == 0)
            continue;

        // Update the ans
        ans = (ans
               + (c1 * ((c2 * (c2 - 1) / 2))));
    }

    // Return the final count
    return ans;
}

// Driver Code
int main()
{
    // Given String
    string str = "224353";
    int N = str.length();

    // Function Call
    cout << countStableNum(str, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the numbers
static int countStableNum(String str, int N)
{

    // Array that stores the
    // digits from left to right
    int count1[][] = new int[N][10];

    // Array that stores the
    // digits from right to left
    int count2[][] = new int[N][10];

    // Initially both array store zero
    for(int i = 0; i < N; i++)
        for(int j = 0; j < 10; j++)
            count1[i][j] = count2[i][j] = 0;

    // Fill the table for count1 array
    for(int i = 0; i < N; i++)
    {
        if (i != 0)
        {
            for(int j = 0; j < 10; j++)
            {
                count1[i][j] += count1[i - 1][j];
            }
        }

        // Update the count of current character
        count1[i][str.charAt(i) - '0']++;
    }

    // Fill the table for count2 array
    for(int i = N - 1; i >= 0; i--)
    {
        if (i != N - 1)
        {
            for(int j = 0; j < 10; j++)
            {
                count2[i][j] += count2[i + 1][j];
            }
        }

        // Update the count of cuuent character
        count2[i][str.charAt(i) - '0']++;
    }

    // Variable that stores the
    // count of the numbers
    int ans = 0;

    // Traverse Input string and get the
    // count of digits from count1 and
    // count2 array such that difference
    // b/w digit is 1 & store it int c1 &c2.
    // And store it in variable c1 and c2
    for(int i = 1; i < N - 1; i++)
    {
        if (str.charAt(i) == '9')
        continue;

        int c1 = count1[i - 1][str.charAt(i) - '0'];
        int c2 = count2[i + 1][str.charAt(i) - '0' + 1];

        if (c2 == 0)
        continue;

        // Update the ans
        ans = (ans + (c1 * ((c2 * (c2 - 1) / 2))));
    }

    // Return the final count
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Given String
    String str = "224353";
    int N = str.length();

    // Function call
    System.out.println(countStableNum(str, N));
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the numbers
def countStableNum(Str, N):

    # Array that stores the
    # digits from left to right
    count1 =  [[0 for j in range(10)]
                  for i in range(N)]

    # Array that stores the
    # digits from right to left
    count2 =  [[0 for j in range(10)]
                  for i in range(N)]

    # Initially both array store zero
    for i in range(N):
        for j in range(10):
            count1[i][j], count2[i][j] = 0, 0

    # Fill the table for count1 array
    for i in range(N):
        if (i != 0):
            for j in range(10):
                count1[i][j] = (count1[i][j] +
                                count1[i - 1][j])

        # Update the count of current character
        count1[i][ord(Str[i]) - ord('0')] += 1

    # Fill the table for count2 array
    for i in range(N - 1, -1, -1):
        if (i != N - 1):
            for j in range(10): 
                count2[i][j] += count2[i + 1][j]

        # Update the count of cuuent character
        count2[i][ord(Str[i]) -
                  ord('0')] = count2[i][ord(Str[i]) -
                                        ord('0')] + 1

    # Variable that stores the
    # count of the numbers
    ans = 0

    # Traverse Input string and get the
    # count of digits from count1 and
    # count2 array such that difference
    # b/w digit is 1 & store it int c1 &c2.
    # And store it in variable c1 and c2
    for i in range(1, N - 1):
        if (Str[i] == '9'):
            continue

        c1 = count1[i - 1][ord(Str[i]) - ord('0')]
        c2 = count2[i + 1][ord(Str[i]) - ord('0') + 1]

        if (c2 == 0):
            continue

        # Update the ans
        ans = (ans + (c1 * ((c2 * (c2 - 1) // 2))))

    # Return the final count
    return ans

# Driver code

# Given String
Str = "224353"
N = len(Str)

# Function call
print(countStableNum(Str, N))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the numbers
static int countStableNum(String str, int N)
{

    // Array that stores the
    // digits from left to right
    int [,]count1 = new int[N, 10];

    // Array that stores the
    // digits from right to left
    int [,]count2 = new int[N, 10];

    // Initially both array store zero
    for(int i = 0; i < N; i++)
        for(int j = 0; j < 10; j++)
            count1[i, j] = count2[i, j] = 0;

    // Fill the table for count1 array
    for(int i = 0; i < N; i++)
    {
        if (i != 0)
        {
            for(int j = 0; j < 10; j++)
            {
                count1[i, j] += count1[i - 1, j];
            }
        }

        // Update the count of current character
        count1[i, str[i] - '0']++;
    }

    // Fill the table for count2 array
    for(int i = N - 1; i >= 0; i--)
    {
        if (i != N - 1)
        {
            for(int j = 0; j < 10; j++)
            {
                count2[i, j] += count2[i + 1, j];
            }
        }

        // Update the count of cuuent character
        count2[i, str[i] - '0']++;
    }

    // Variable that stores the
    // count of the numbers
    int ans = 0;

    // Traverse Input string and get the
    // count of digits from count1 and
    // count2 array such that difference
    // b/w digit is 1 & store it int c1 &c2.
    // And store it in variable c1 and c2
    for(int i = 1; i < N - 1; i++)
    {
        if (str[i] == '9')
        continue;

        int c1 = count1[i - 1, str[i] - '0'];
        int c2 = count2[i + 1, str[i] - '0' + 1];

        if (c2 == 0)
        continue;

        // Update the ans
        ans = (ans + (c1 * ((c2 * (c2 - 1) / 2))));
    }

    // Return the readonly count
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // Given String
    String str = "224353";
    int N = str.Length;

    // Function call
    Console.WriteLine(countStableNum(str, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the numbers
function countStableNum(str, N)
{
    // Array that stores the
    // digits from left to right
    var count1 = Array.from(Array(N), ()=>Array(10));

    // Array that stores the
    // digits from right to left
    var count2 = Array.from(Array(N), ()=>Array(10));

    // Initially both array store zero
    for (var i = 0; i < N; i++)
        for (var j = 0; j < 10; j++)
            count1[i][j] = count2[i][j] = 0;

    // Fill the table for count1 array
    for (var i = 0; i < N; i++) {
        if (i != 0) {
            for (var j = 0; j < 10; j++) {
                count1[i][j] += count1[i - 1][j];
            }
        }

        // Update the count of current character
        count1[i][str[i] - '0']++;
    }

    // Fill the table for count2 array
    for (var i = N - 1; i >= 0; i--) {
        if (i != N - 1) {
            for (var j = 0; j < 10; j++) {
                count2[i][j] += count2[i + 1][j];
            }
        }

        // Update the count of cuuent character
        count2[i][str[i] - '0']++;
    }

    // Variable that stores the
    // count of the numbers
    var ans = 0;

    // Traverse Input string and get the
    // count of digits from count1 and
    // count2 array such that difference
    // b/w digit is 1 & store it var c1 &c2.
    // And store it in variable c1 and c2
    for (var i = 1; i < N - 1; i++) {

        if (str[i] == '9')
            continue;

        var c1 = count1[i - 1][str[i] - '0'];
        var c2 = count2[i + 1][str[i] - '0' + 1];

        if (c2 == 0)
            continue;

        // Update the ans
        ans = (ans
               + (c1 * ((c2 * (c2 - 1) / 2))));
    }

    // Return the final count
    return ans;
}

// Driver Code

// Given String
var str = "224353";
var N = str.length;

// Function Call
document.write( countStableNum(str, N));

</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N)*
T5】辅助空间复杂度: *O(N)*
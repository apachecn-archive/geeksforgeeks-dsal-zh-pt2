# 最小化翻转或交换的成本，使二进制字符串平衡

> 原文:[https://www . geesforgeks . org/最小化翻转或交换成本以使二进制字符串平衡/](https://www.geeksforgeeks.org/minimize-cost-of-flipping-or-swaps-to-make-a-binary-string-balanced/)

给定一个大小为 **N** (其中 **N** 为偶数)的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过以 **1 个单位**为代价翻转一个相邻的不同字符，或者以 **i** 和 **j** 为索引交换字符以使 **(i < j)** 以**为代价，找到使给定二进制字符串平衡的最小成本如果无法使弦平衡，打印**-1”**。**

> 一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)如果可以通过一次删除两个连续的交替字符，然后将剩余的字符串联起来，从而将其简化为一个空字符串，那么这个字符串就是**平衡的**。

**示例:**

> **输入:** S = "110110"
> **输出:** 1
> **解释:**执行以下操作:
> **操作 1:** 由于索引 0 和 1 处的相邻字符不同，翻转 S[0]将 S 修改为“010110”。成本= **1** 。
> 
> 完成上述操作后，给定的字符串会变得平衡，因为可以通过删除两个连续的交替字符将其简化为空字符串。
> 因此，总成本为 1。
> 
> **输入:**S = " 11100 "
> T3】输出: -1

**方法:**基于观察到相邻不同字符的翻转比使用字符交换更优化，并且字符串中 **0s** 和 **1s** 的位置无关紧要，可以解决给定的问题。按照以下步骤解决问题:

*   [如果所有字符相等](https://www.geeksforgeeks.org/check-if-frequency-of-all-characters-can-become-same-by-one-removal/)，那么不可能使字符串平衡。因此，打印**“-1”**。
*   [将 1 和 0 的计数](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)存储在变量中，分别表示**计数 1** 和**计数 0** 。
*   将**计数 1** 和**计数 0** 的[绝对差值](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)存储在变量 **K** 中。
*   现在，翻转 **K/2** 字符，使字符串平衡，并打印 **K/2** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to convert the given string into
// balanced string
void findMinimumCost(string s, int N)
{

    // Stores count of 1's and 0's in
    // the string
    int count_1 = 0, count_0 = 0;

    // Traverse the string
    for (int i = 0; i < N; i++) {
        if (s[i] == '1')

            // Increment count1
            count_1++;
        else

            // Increment count 0
            count_0++;
    }

    // Stores absolute difference of
    // counts of 0's and 1's
    int k = abs(count_0 - count_1);

    // If string consists of only
    // 0's and 1's
    if (count_1 == N || count_0 == N)
        cout << -1 << endl;

    // Print minimum cost
    else
        cout << k / 2 << endl;
}

// Driver Code
int main()
{
    string S = "110110";
    int N = S.length();
    findMinimumCost(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the minimum cost
// to convert the given string into
// balanced string
static void findMinimumCost(String s, int N)
{

    // Stores count of 1's and 0's in
    // the string
    int count_1 = 0, count_0 = 0;

    // Traverse the string
    for (int i = 0; i < N; i++) {
        if (s.charAt(i) == '1')

            // Increment count1
            count_1++;
        else

            // Increment count 0
            count_0++;
    }

    // Stores absolute difference of
    // counts of 0's and 1's
    int k = Math.abs(count_0 - count_1);

    // If string consists of only
    // 0's and 1's
    if (count_1 == N || count_0 == N)
        System.out.println( -1);

    // Print minimum cost
    else
        System.out.println( k / 2);
}

// Driver Code
public static void main(String[] args)
{

    String S = "110110";
    int N = S.length();
    findMinimumCost(S, N);
}
}
// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost
# to convert the given into
# balanced string
def findMinimumCost(s, N):

    # Stores count of 1's and 0's in
    # the string
    count_1, count_0 = 0, 0

    # Traverse the string
    for i in range(N):
        if (s[i] == '1'):

            # Increment count1
            count_1 += 1
        else:

            # Increment count 0
            count_0 += 1

    # Stores absolute difference of
    # counts of 0's and 1's
    k = abs(count_0 - count_1)

    # If consists of only
    # 0's and 1's
    if (count_1 == N or count_0 == N):
        print(-1)

    # Print the minimum cost
    else:
        print(k // 2)

# Driver Code
if __name__ == '__main__':

    S = "110110"
    N = len(S)

    findMinimumCost(S, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum cost
// to convert the given string into
// balanced string
static void findMinimumCost(String s, int N)
{

    // Stores count of 1's and 0's in
    // the string
    int count_1 = 0, count_0 = 0;

    // Traverse the string
    for(int i = 0; i < N; i++)
    {
        if (s[i] == '1')

            // Increment count1
            count_1++;
        else

            // Increment count 0
            count_0++;
    }

    // Stores absolute difference of
    // counts of 0's and 1's
    int k = Math.Abs(count_0 - count_1);

    // If string consists of only
    // 0's and 1's
    if (count_1 == N || count_0 == N)
        Console.WriteLine(-1);

    // Print minimum cost
    else
        Console.WriteLine(k / 2);
}

// Driver Code
static public void Main()
{
    String S = "110110";
    int N = S.Length;

    findMinimumCost(S, N);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum cost
// to convert the given string into
// balanced string
function findMinimumCost(s, N)
{

    // Stores count of 1's and 0's in
    // the string
    let count_1 = 0, count_0 = 0;

    // Traverse the string
    for (let i = 0; i < N; i++) {
        if (s[i] == '1')

            // Increment count1
            count_1++;
        else

            // Increment count 0
            count_0++;
    }

    // Stores absolute difference of
    // counts of 0's and 1's
    let k = Math.abs(count_0 - count_1);

    // If string consists of only
    // 0's and 1's
    if (count_1 == N || count_0 == N)
        document.write( -1);

    // Print minimum cost
    else
        document.write( k / 2);
}

// Driver Code

    let S = "110110";
    let N = S.length;
    findMinimumCost(S, N);

</script>              
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
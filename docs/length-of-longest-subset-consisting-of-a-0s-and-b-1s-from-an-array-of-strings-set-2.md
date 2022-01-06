# 字符串数组中由 A0 和 B1 组成的最长子集的长度|集合 2

> 原文:[https://www . geesforgeks . org/最长子集长度-由-a-0s 和-b-1s 组成-从字符串数组-set-2/](https://www.geeksforgeeks.org/length-of-longest-subset-consisting-of-a-0s-and-b-1s-from-an-array-of-strings-set-2/)

给定一个由**N**T6】二进制字符串和两个整数 **A** 和 **B** 组成的[数组 **arr[]** ，任务是找到最长子集的长度，该子集最多由 **A** **0** s 和 **B** **1** s 组成。](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> ***输入:**arr[]= {“1”、“0”、“0001”、“10”、“111001”}，A = 5，B = 3*
> ***输出:** 4*
> ***解释:***
> *一种可能的方式是选择子集{arr[0]、arr[1]、arr[2]、arr[3]}。*
> *所有这些字符串中 0 和 1 的总数分别为 5 和 3。*
> *同样，4 是可能的最长子集的长度。*
> 
> ***输入:**arr[]= {“0”、“1”、“10”}，A = 1，B = 1*
> ***输出:** 2*
> ***解释:***
> *一种可能的方式是选择子集{arr[0]，arr[1]}。*
> *所有这些字符串中 0 和 1 的总数分别为 1 和 1。*
> *同样，2 是可能的最长子集的长度。*

**天真的做法:**参考本文[之前的帖子](https://www.geeksforgeeks.org/length-of-longest-subset-consisting-of-a-0s-and-b-1s-from-an-array-of-strings/)了解解决问题最简单的方法。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

[**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) **方法:**关于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法，请参考本文[上一篇文章](https://www.geeksforgeeks.org/length-of-longest-subset-consisting-of-a-0s-and-b-1s-from-an-array-of-strings/)。
***时间复杂度:**O(N * a* B)*
***辅助空间:** O(N * A * B)*

**空间优化动态规划方法:**上述方法中的空间复杂度可以基于以下观察来优化:

*   初始化一个 2D 数组， **dp[A][B]** ，其中 **dp[i][j]** 表示最长子集的长度，最多由 **i** 个 **0** s 和 **j** 个 **1** s 组成。
*   为了优化从 **3D 表**到 **2D 表**的辅助空间，想法是以相反的顺序遍历内部循环。
*   这确保了每当 **dp[][]** 中的值改变时，在当前迭代中将不再需要它。
*   因此，递归关系如下所示:

> **dp[i][j] = max (dp[i][j]，DP[I–零][j–一] + 1)**
> 其中零是 0 的计数，1 是当前迭代中 1 的计数。

按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，说**DP【A】【B】**，将其所有条目初始化为 **0** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对每个二进制字符串执行以下步骤:
    *   将当前字符串中 0 和 1 的[计数分别存储在变量**0**和**1**中。](https://www.geeksforgeeks.org/c-program-to-count-zeros-and-ones-in-binary-representation-of-a-number/)
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【A，零】**内迭代，同时[使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【B，1】**内迭代，并将 **dp[i][j]** 的值更新为[最大值](https://www.geeksforgeeks.org/stdmax-in-cpp/)**DP[I][j]**和**(DP[I–零][j–1】**
*   完成以上步骤后，打印**DP【A】【B】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest subset of an array of strings
// with at most A 0s and B 1s
int MaxSubsetlength(vector<string> arr,
                    int A, int B)
{
    // Initialize a 2D array with its
    // entries as 0
    int dp[A + 1][B + 1];
    memset(dp, 0, sizeof(dp));

    // Traverse the given array
    for (auto& str : arr) {

        // Store the count of 0s and 1s
        // in the current string
        int zeros = count(str.begin(),
                          str.end(), '0');
        int ones = count(str.begin(),
                         str.end(), '1');

        // Iterate in the range [A, zeros]
        for (int i = A; i >= zeros; i--)

            // Iterate in the range [B, ones]
            for (int j = B; j >= ones; j--)

                // Update the value of dp[i][j]
                dp[i][j] = max(
                    dp[i][j],
                    dp[i - zeros][j - ones] + 1);
    }

    // Print the result
    return dp[A][B];
}

// Driver Code
int main()
{
    vector<string> arr
        = { "1", "0", "0001",
            "10", "111001" };
    int A = 5, B = 3;
    cout << MaxSubsetlength(arr, A, B);

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

// Function to find the length of the
// longest subset of an array of strings
// with at most A 0s and B 1s
static int MaxSubsetlength(String arr[],
                           int A, int B)
{

    // Initialize a 2D array with its
    // entries as 0
    int dp[][] = new int[A + 1][B + 1];

    // Traverse the given array
    for(String str : arr)
    {

        // Store the count of 0s and 1s
        // in the current string
        int zeros = 0, ones = 0;
        for(char ch : str.toCharArray())
        {
            if (ch == '0')
                zeros++;
            else
                ones++;
        }

        // Iterate in the range [A, zeros]
        for(int i = A; i >= zeros; i--)

            // Iterate in the range [B, ones]
            for(int j = B; j >= ones; j--)

                // Update the value of dp[i][j]
                dp[i][j] = Math.max(
                    dp[i][j],
                    dp[i - zeros][j - ones] + 1);
    }

    // Print the result
    return dp[A][B];
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = { "1", "0", "0001",
                     "10", "111001" };
    int A = 5, B = 3;

    System.out.println(MaxSubsetlength(arr, A, B));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of the
# longest subset of an array of strings
# with at most A 0s and B 1s
def MaxSubsetlength(arr, A, B):

    # Initialize a 2D array with its
    # entries as 0
    dp = [[0 for i in range(B + 1)]
             for i in range(A + 1)]

    # Traverse the given array
    for str in arr:

        # Store the count of 0s and 1s
        # in the current string
        zeros = str.count('0')
        ones = str.count('1')

        # Iterate in the range [A, zeros]
        for i in range(A, zeros - 1, -1):

            # Iterate in the range [B, ones]
            for j in range(B, ones - 1, -1):

                # Update the value of dp[i][j]
                dp[i][j] = max(dp[i][j],
                               dp[i - zeros][j - ones] + 1)

    # Print the result
    return dp[A][B]

# Driver Code
if __name__ == '__main__':

    arr = [ "1", "0", "0001", "10", "111001" ]
    A, B = 5, 3

    print (MaxSubsetlength(arr, A, B))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG {

  // Function to find the length of the
  // longest subset of an array of strings
  // with at most A 0s and B 1s
  static int MaxSubsetlength(string[] arr, int A, int B)
  {

    // Initialize a 2D array with its
    // entries as 0
    int[, ] dp = new int[A + 1, B + 1];

    // Traverse the given array
    foreach(string str in arr)
    {

      // Store the count of 0s and 1s
      // in the current string
      int zeros = 0, ones = 0;
      foreach(char ch in str.ToCharArray())
      {
        if (ch == '0')
          zeros++;
        else
          ones++;
      }

      // Iterate in the range [A, zeros]
      for (int i = A; i >= zeros; i--)

        // Iterate in the range [B, ones]
        for (int j = B; j >= ones; j--)

          // Update the value of dp[i][j]
          dp[i, j] = Math.Max(
          dp[i, j],
          dp[i - zeros, j - ones] + 1);
    }

    // Print the result
    return dp[A, B];
  }

  // Driver Code
  public static void Main(string[] args)
  {
    string[] arr = { "1", "0", "0001", "10", "111001" };
    int A = 5, B = 3;

    Console.WriteLine(MaxSubsetlength(arr, A, B));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the length of the
// longest subset of an array of strings
// with at most A 0s and B 1s
function MaxSubsetlength(arr, A, B)
{

    // Initialize a 2D array with its
    // entries as 0
    var dp = Array.from(Array(A + 1),
         ()=>Array(B + 1).fill(0));

    // Traverse the given array
    arr.forEach(str => {

        // Store the count of 0s and 1s
        // in the current string
        var zeros = [...str].filter(x => x == '0').length;
        var ones = [...str].filter(x => x == '1').length;

        // Iterate in the range [A, zeros]
        for(var i = A; i >= zeros; i--)

            // Iterate in the range [B, ones]
            for(var j = B; j >= ones; j--)

                // Update the value of dp[i][j]
                dp[i][j] = Math.max(dp[i][j],
                    dp[i - zeros][j - ones] + 1);
    });

    // Print the result
    return dp[A][B];
}

// Driver Code
var arr = [ "1", "0", "0001",
            "10", "111001" ];
var A = 5, B = 3;

document.write(MaxSubsetlength(arr, A, B));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * A * B)*
***辅助空间:** O(A * B)*
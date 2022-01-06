# 将给定字符串转换为长度为 K 的相等子字符串的连接所需的最小翻转次数

> 原文:[https://www . geesforgeks . org/minimum-flips-需要将给定字符串转换为长度为 k 的相等子字符串的串联/](https://www.geeksforgeeks.org/minimum-flips-required-to-convert-given-string-into-concatenation-of-equal-substrings-of-length-k/)

给定一个二进制字符串 **S** 和一个整数 **K** ，任务是找到将给定字符串转换为一系列 **K 长度**相等子字符串所需的最小翻转次数。给出了给定的字符串可以拆分成 [**K 长度的子字符串**](https://www.geeksforgeeks.org/python-extract-k-length-substrings/) 。

**示例:**

> **输入:**S =“101100101”，K = 3
> **输出:** 1
> **解释:**
> 将“0”从索引 5 翻转为“1”。
> 结果字符串为 S =“101101101”。
> 是子串“101”的串联。
> 因此，所需的最小翻转次数为 1。
> 
> **输入:** S = "10110111 "，K = 4
> **输出:** 2
> **解释:**
> 分别在索引 4 和索引 5 处翻转‘0’和‘1’。
> 结果字符串为 S =“10111011”。
> 是子串“1011”的串联。
> 因此，所需的最小翻转次数为 2 次。

**进场:**
问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。
按照以下步骤操作:

*   从每个索引中以 **K** 个索引的增量迭代给定的字符串，并记录 **0** 和 **1** 个索引
*   出现次数最少的字符必须翻转并不断增加**计数**。
*   对从 **0** 到 **K-1** 的所有指标执行上述步骤，以获得所需的最小翻转次数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the minimum
// number of flips to convert
// the s into a concatenation
// of K-length sub-string
int minOperations(string S, int K)
{
    // Stores the result
    int ans = 0;

    // Iterate through string index
    for (int i = 0; i < K; i++) {

        // Stores count of 0s & 1s
        int zero = 0, one = 0;

        // Iterate making K jumps
        for (int j = i;
             j < S.size(); j += K) {

            // Count 0's
            if (S[j] == '0')
                zero++;

            // Count 1's
            else
                one++;
        }

        // Add minimum flips
        // for index i
        ans += min(zero, one);
    }

    // Return minimum number
    // of flips
    return ans;
}

// Driver Code
int main()
{
    string S = "110100101";

    int K = 3;

    cout << minOperations(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function that returns the minimum
// number of flips to convert
// the s into a concatenation
// of K-length sub-string
public static int minOperations(String S, int K)
{

    // Stores the result
    int ans = 0;

    // Iterate through string index
    for(int i = 0; i < K; i++)
    {

        // Stores count of 0s & 1s
        int zero = 0, one = 0;

        // Iterate making K jumps
        for(int j = i; j < S.length(); j += K)
        {

            // Count 0's
            if (S.charAt(j) == '0')
                zero++;

            // Count 1's
            else
                one++;
        }

        // Add minimum flips
        // for index i
        ans += Math.min(zero, one);
    }

    // Return minimum number
    // of flips
    return ans;
}

// Driver Code
public static void main(String args[])
{
    String S = "110100101";

    int K = 3;

    System.out.println(minOperations(S, K));
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function that returns the minimum
# number of flips to convert the s
# into a concatenation of K-length
# sub-string
def minOperations(S, K):

    # Stores the result
    ans = 0

    # Iterate through string index
    for i in range(K):

        # Stores count of 0s & 1s
        zero, one = 0, 0

        # Iterate making K jumps
        for j in range(i, len(S), K):

            # Count 0's
            if(S[j] == '0'):
                zero += 1

            # Count 1's
            else:
                one += 1

        # Add minimum flips
        # for index i
        ans += min(zero, one)

    # Return minimum number
    # of flips
    return ans

# Driver code
if __name__ == '__main__':

    s = "110100101"
    K = 3

    print(minOperations(s, K))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function that returns the minimum
// number of flips to convert
// the s into a concatenation
// of K-length sub-string
public static int minOperations(String S, int K)
{

    // Stores the result
    int ans = 0;

    // Iterate through string index
    for(int i = 0; i < K; i++)
    {

        // Stores count of 0s & 1s
        int zero = 0, one = 0;

        // Iterate making K jumps
        for(int j = i; j < S.Length; j += K)
        {

            // Count 0's
            if (S[j] == '0')
                zero++;

            // Count 1's
            else
                one++;
        }

        // Add minimum flips
        // for index i
        ans += Math.Min(zero, one);
    }

    // Return minimum number
    // of flips
    return ans;
}

// Driver Code
public static void Main(String []args)
{
    String S = "110100101";

    int K = 3;

    Console.WriteLine(minOperations(S, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach
      // Function that returns the minimum
      // number of flips to convert
      // the s into a concatenation
      // of K-length sub-string
      function minOperations(S, K) {
        // Stores the result
        var ans = 0;

        // Iterate through string index
        for (var i = 0; i < K; i++) {
          // Stores count of 0s & 1s
          var zero = 0,
            one = 0;

          // Iterate making K jumps
          for (var j = i; j < S.length; j += K) {
            // Count 0's
            if (S[j] === "0")
                zero++;
            // Count 1's
            else
                one++;
          }

          // Add minimum flips
          // for index i
          ans += Math.min(zero, one);
        }

        // Return minimum number
        // of flips
        return ans;
      }

      // Driver Code
      var S = "110100101";
      var K = 3;

      document.write(minOperations(S, K));
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
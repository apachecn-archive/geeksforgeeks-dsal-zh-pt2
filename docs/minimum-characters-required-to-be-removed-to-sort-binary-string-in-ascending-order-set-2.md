# 按升序对二进制字符串排序时需要删除的最少字符–设置 2

> 原文:[https://www . geesforgeks . org/最小字符-需要删除才能排序-二进制字符串-按升序-set-2/](https://www.geeksforgeeks.org/minimum-characters-required-to-be-removed-to-sort-binary-string-in-ascending-order-set-2/)

给定大小为 **N** 的 [二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串** ，任务是从给定的二进制字符串中删除最少数量的字符，使剩余字符串中的字符按排序。

**示例:**

> ***输入:****str = " 1000101 "*
> ***输出:****2*
> ***解释:*** *删除前两次出现的‘1’将字符串修改为“00001”，这是一个排序顺序。该字符串也可以通过执行 2 次删除而变成“00011”。因此，要删除的最小字符数是 2。*
> 
> ***输入:****str = " 001111 "*
> ***输出:****0*
> ***解释:*** *该字符串已经排序完毕。因此，要删除的最小字符数为 0。*

**最后出现法:**本文[集 1](https://www.geeksforgeeks.org/minimum-characters-required-to-be-removed-to-sort-binary-string-in-ascending-order/)讨论了线性时间和常数空间的优化方法。这里，我们讨论的是动态编程方法。

**动态编程方法:**这个问题可以通过使用[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)来解决，通过观察以下事实，如果需要 **K** 删除来使字符串排序到第 i <sup>个</sup>索引

> *   情况 1: **S[i+1] = 1** 那么将字符串排序到第 **(i+1)个**索引所需的最小删除次数也将是 **K** ，因为将 **1** 附加到排序后的字符串将保持字符串排序，因此不再需要删除。
> *   案例 2: **S[i + 1] = 0** 那么我们有两种方法可以将字符串排序到 **(i+1)第**个索引，它们是
>     *   删除第(i+1)个索引前的所有 **1 个**,或者
>     *   删除当前 **0** 。
> 
> 使字符串在第(i+1)个索引之前有效的最小删除次数将是**的最小值(第(i+1)个索引之前的 1 个数，K+1)。**

按照以下步骤解决问题:

*   初始化变量**计数 1** 为 **0** ， **N** 为字符串 **s** **的[长度。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)**
*   [用值 **0 初始化向量**](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)**DP【n+1】**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n)** ，并执行以下任务:
    *   如果 **s[i]** 等于 **0，**则将 **dp[i+1]** 设置为**计数 1** 或 **1 + dp[i]的最小值。**
    *   否则，将 **dp[i+1]** 设置为 **dp[i]** ，并将 **count1** 的值增加 **1。**
*   执行上述步骤后，打印**DP【n】**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of deletions to make
// the string sorted
int minDeletions(string s)
{
    int n = s.size();

    // dp[i+1] stores minimum number of
    // deletion to make
    // substring(0, i) valid
    vector<int> dp(n + 1, 0);
    int count1 = 0;

    for (int i = 0; i < n; i++) {
        if (s[i] == '0') {

            // Case 1: remove current 0
            // Case 2: keep current 0
            // then delete all 1 before it
            dp[i + 1] = min(count1,
                            1 + dp[i]);
        }
        else {

            // Appending 1 is always valid
            // if substring(0, i) is sorted
            dp[i + 1] = dp[i];
            count1++;
        }
    }
    return dp[n];
}

// Driver Code
int main()
{
    string s = "00101101";
    cout << minDeletions(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to find the minimum number
// of deletions to make
// the string sorted
static int minDeletions(String s)
{
    int n = s.length();

    // dp[i+1] stores minimum number of
    // deletion to make
    // substring(0, i) valid
    int []dp = new int[n + 1];
    for(int i = 0; i < n + 1; i++) {
        dp[i] = 0;
    }
    int count1 = 0;

    for (int i = 0; i < n; i++) {
        if (s.charAt(i) == '0') {

            // Case 1: remove current 0
            // Case 2: keep current 0
            // then delete all 1 before it
            dp[i + 1] = Math.min(count1,
                            1 + dp[i]);
        }
        else {

            // Appending 1 is always valid
            // if substring(0, i) is sorted
            dp[i + 1] = dp[i];
            count1++;
        }
    }
    return dp[n];
}

// Driver Code
public static void main(String args[])
{
    String s = "00101101";
    System.out.println(minDeletions(s));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the minimum number
# of deletions to make
# the string sorted
def minDeletions(s):
    n = len(s)

    # dp[i+1] stores minimum number of
    # deletion to make
    # substring(0, i) valid
    dp = [0] * (n + 1)
    count1 = 0

    for i in range(n):
        if (s[i] == '0'):

            # Case 1: remove current 0
            # Case 2: keep current 0
            # then delete all 1 before it
            dp[i + 1] = min(count1, 1 + dp[i])
        else:

            # Appending 1 is always valid
            # if substring(0, i) is sorted
            dp[i + 1] = dp[i]
            count1 += 1
    return dp[n]

# Driver Code
s = "00101101"
print(minDeletions(s))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to find the minimum number
    // of deletions to make
    // the string sorted
    static int minDeletions(string s)
    {
        int n = s.Length;

        // dp[i+1] stores minimum number of
        // deletion to make
        // substring(0, i) valid
        int[] dp = new int[n + 1];
        for (int i = 0; i < n + 1; i++)
        {
            dp[i] = 0;
        }
        int count1 = 0;

        for (int i = 0; i < n; i++)
        {
            if (s[i] == '0')
            {

                // Case 1: remove current 0
                // Case 2: keep current 0
                // then delete all 1 before it
                dp[i + 1] = Math.Min(count1,
                                1 + dp[i]);
            }
            else
            {

                // Appending 1 is always valid
                // if substring(0, i) is sorted
                dp[i + 1] = dp[i];
                count1++;
            }
        }
        return dp[n];
    }

    // Driver Code
    public static void Main()
    {
        string s = "00101101";
        Console.Write(minDeletions(s));

    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find the minimum number
      // of deletions to make
      // the string sorted
      function minDeletions(s) {
          let n = s.length;

          // dp[i+1] stores minimum number of
          // deletion to make
          // substring(0, i) valid
          let dp = new Array(n + 1).fill(0);
          let count1 = 0;

          for (let i = 0; i < n; i++) {
              if (s[i] == '0') {

                  // Case 1: remove current 0
                  // Case 2: keep current 0
                  // then delete all 1 before it
                  dp[i + 1] = Math.min(count1,
                      1 + dp[i]);
              }
              else {

                  // Appending 1 is always valid
                  // if substring(0, i) is sorted
                  dp[i + 1] = dp[i];
                  count1++;
              }
          }
          return dp[n];
      }

      // Driver Code

      let s = "00101101";
      document.write(minDeletions(s));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
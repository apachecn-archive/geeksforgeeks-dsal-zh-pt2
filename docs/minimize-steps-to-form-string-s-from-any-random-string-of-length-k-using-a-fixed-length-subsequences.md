# 使用固定长度的子序列将长度为 K 的任意随机串形成串 S 的步骤减至最少

> 原文:[https://www . geeksforgeeks . org/使用固定长度的子序列从任意长度的随机串 k 中最小化形成串 s 的步骤/](https://www.geeksforgeeks.org/minimize-steps-to-form-string-s-from-any-random-string-of-length-k-using-a-fixed-length-subsequences/)

给定由 **N** 字符和正整数 **K** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是从大小为 **K** 的随机字符串 **temp** 中找到生成字符串 **S** 所需的最小操作数，并将随机字符串中任意固定长度的子序列插入到随机字符串中。如果无法生成字符串 **S** ，则打印**-1”**。

**示例:**

> **输入:** S =“太妃糖”，N = 4
> **输出:** 2 tofe
> **解释:**
> 将随机字符串 temp 视为长度为 K(= 4)的“tofe”，并执行以下步骤:
> **操作 1:** 从字符串 **temp** 中取长度为 1 的子序列作为“f”，在字符串“tofe”中插入子序列后，将字符串修改为“tofe”。
> **操作 2:** 取字符串 **temp** 中长度为 1 的子序列为‘e’，将子序列插入字符串“toffe”后，将字符串修改为“toffe”。
> 
> 因此，所需的最小操作数是 2。
> 
> **输入:** S = "book "，N = 2
> **输出:** -1

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。按照以下步骤解决此问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，说**量[]** ，存储字符串 **S** 每个字符的[频率。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**中迭代，并将数组**中当前字符的频率增加 **1** 个数量[]** 。
*   找到[统计字符串](https://www.geeksforgeeks.org/count-the-number-of-unique-characters-in-a-string-in-python/) **S** 中的唯一字符，并将其存储在一个变量中，比如说，**统计**。
*   如果**计数**大于 **N，**则返回 **-1** 。
*   现在，执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到结果字符串并执行以下步骤:
*   将两个变量**高**初始化为**10<sup>5</sup>T5**低**初始化为 **0** 。**
*   迭代直到**(高–低)**的值大于 **1** ，并执行以下步骤:
    *   将**总计**的值更新为 **0** ，将**中间**更新为**(高+低)/ 2** 。
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，25】**中迭代，如果**数量【I】**的值大于 **0** ，那么将**总数**增加**(数量【I】–1)/中间+ 1** 。
    *   如果****总计**小于等于 **N** ，则将**高**的值更新为**中**。否则，将**低值**更新为**中值**。**
*   **完成以上步骤后，打印**高值**[的值，在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，25】**范围内迭代，打印结果字符串。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of string required to generate
// the original string
void findString(string S, int N)
{
    // Stores the frequency of each
    // character of String S
    int amounts[26];

    // Iterate over the range [0, 25]
    for (int i = 0; i < 26; i++) {
        amounts[i] = 0;
    }

    // Stores the frequency of each
    // character of String S
    for (int i = 0; i < S.length(); i++) {
        amounts[int(S[i]) - 97]++;
    }

    int count = 0;

    // Count unique characters in S
    for (int i = 0; i < 26; i++) {
        if (amounts[i] > 0)
            count++;
    }

    // If unique characters is greater
    // then N, then return -1
    if (count > N) {
        cout << "-1";
    }

    // Otherwise
    else {

        string ans = "";
        int high = 100001;
        int low = 0;
        int mid, total;

        // Perform Binary Search
        while ((high - low) > 1) {

            total = 0;

            // Find the value of mid
            mid = (high + low) / 2;

            // Iterate over the range
            // [0, 26]
            for (int i = 0; i < 26; i++) {

                // If the amount[i] is
                // greater than 0
                if (amounts[i] > 0) {
                    total += (amounts[i] - 1)
                                 / mid
                             + 1;
                }
            }

            // Update the ranges
            if (total <= N) {
                high = mid;
            }
            else {
                low = mid;
            }
        }

        cout << high << " ";

        total = 0;

        // Find the resultant string
        for (int i = 0; i < 26; i++) {

            if (amounts[i] > 0) {
                total += (amounts[i] - 1)
                             / high
                         + 1;

                for (int j = 0;
                     j < ((amounts[i] - 1)
                              / high
                          + 1);
                     j++) {

                    // Generate the subsequence
                    ans += char(i + 97);
                }
            }
        }

        // If the length of resultant
        // string is less than N than
        // add a character 'a'
        for (int i = total; i < N; i++) {
            ans += 'a';
        }

        reverse(ans.begin(), ans.end());

        // Print the string
        cout << ans;
    }
}

// Driver Code
int main()
{
    string S = "toffee";
    int K = 4;
    findString(S, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code for above approach
import java.util.*;

class GFG{

// Function to find the minimum number
// of string required to generate
// the original string
static void findString(String S, int N)
{

    // Stores the frequency of each
    // character of string S
    int[] amounts = new int[26];

    // Iterate over the range [0, 25]
    for (int i = 0; i < 26; i++) {
        amounts[i] = 0;
    }

    // Stores the frequency of each
    // character of string S
    for (int i = 0; i < S.length(); i++) {
        amounts[(int)(S.charAt(i) - 97)]++;
    }

    int count = 0;

    // Count unique characters in S
    for (int i = 0; i < 26; i++) {
        if (amounts[i] > 0)
            count++;
    }

    // If unique characters is greater
    // then N, then return -1
    if (count > N) {
        System.out.print("-1");
    }

    // Otherwise
    else {

        String ans = "";
        int high = 100001;
        int low = 0;
        int mid, total;

        // Perform Binary Search
        while ((high - low) > 1) {

            total = 0;

            // Find the value of mid
            mid = (high + low) / 2;

            // Iterate over the range
            // [0, 26]
            for (int i = 0; i < 26; i++) {

                // If the amount[i] is
                // greater than 0
                if (amounts[i] > 0) {
                    total += (amounts[i] - 1)
                                 / mid
                             + 1;
                }
            }

            // Update the ranges
            if (total <= N) {
                high = mid;
            }
            else {
                low = mid;
            }
        }

        System.out.print(high + " ");

        total = 0;

        // Find the resultant string
        for (int i = 0; i < 26; i++) {

            if (amounts[i] > 0) {
                total += (amounts[i] - 1)
                             / high
                         + 1;

                for (int j = 0;
                     j < ((amounts[i] - 1)
                              / high
                          + 1);
                     j++) {

                    // Generate the subsequence
                    ans += (char)(i + 97);
                }
            }
        }

        // If the length of resultant
        // string is less than N than
        // add a character 'a'
        for (int i = total; i < N; i++) {
            ans += 'a';
        }

        String reverse = "";
        int Len = ans.length() - 1; 
            while(Len >= 0) 
            { 
                reverse = reverse + ans.charAt(Len); 
                Len--; 
            }

        // Print the string
        System.out.print(reverse);
    }
}

// Driver Code
public static void main(String[] args)
{
    String S = "toffee";
    int K = 4;
    findString(S, K);
}
}

// This code is contributed by target_2.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the minimum number
# of string required to generate
# the original string
def findString(S, N):

    # Stores the frequency of each
    # character of String S
    amounts = [0] * 26

    # Stores the frequency of each
    # character of String S
    for i in range(len(S)):
        amounts[ord(S[i]) - 97] += 1

    count = 0

    # Count unique characters in S
    for i in range(26):
        if amounts[i] > 0:
            count += 1

    # If unique characters is greater
    # then N, then return -1
    if count > N:
        print("-1")

    # Otherwise
    else:
        ans = ""
        high = 100001
        low = 0

        # Perform Binary Search
        while (high - low) > 1:
            total = 0

            # Find the value of mid
            mid = (high + low) // 2

            # Iterate over the range
            # [0, 26]
            for i in range(26):

                # If the amount[i] is
                # greater than 0
                if amounts[i] > 0:
                    total += (amounts[i] - 1) // mid + 1

            # Update the ranges
            if total <= N:
                high = mid
            else:
                low = mid

        print(high, end = " ")
        total = 0

        # Find the resultant string
        for i in range(26):
            if amounts[i] > 0:
                total += (amounts[i] - 1) // high + 1
                for j in range((amounts[i] - 1) // high + 1):
                    ans += chr(i + 97)

        # If the length of resultant
        # string is less than N than
        # add a character 'a'            
        for i in range(total, N):
            ans += 'a'

        ans = ans[::-1]

        # Print the string
        print(ans)

# Driver code
S = "toffee"
K = 4

findString(S, K)

# This code is contributed by Parth Manchanda
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of string required to generate
// the original string
static void findString(string S, int N)
{

    // Stores the frequency of each
    // character of string S
    int[] amounts = new int[26];

    // Iterate over the range [0, 25]
    for (int i = 0; i < 26; i++) {
        amounts[i] = 0;
    }

    // Stores the frequency of each
    // character of string S
    for (int i = 0; i < S.Length; i++) {
        amounts[(int)(S[i] - 97)]++;
    }

    int count = 0;

    // Count unique characters in S
    for (int i = 0; i < 26; i++) {
        if (amounts[i] > 0)
            count++;
    }

    // If unique characters is greater
    // then N, then return -1
    if (count > N) {
        Console.Write("-1");
    }

    // Otherwise
    else {

        string ans = "";
        int high = 100001;
        int low = 0;
        int mid, total;

        // Perform Binary Search
        while ((high - low) > 1) {

            total = 0;

            // Find the value of mid
            mid = (high + low) / 2;

            // Iterate over the range
            // [0, 26]
            for (int i = 0; i < 26; i++) {

                // If the amount[i] is
                // greater than 0
                if (amounts[i] > 0) {
                    total += (amounts[i] - 1)
                                 / mid
                             + 1;
                }
            }

            // Update the ranges
            if (total <= N) {
                high = mid;
            }
            else {
                low = mid;
            }
        }

        Console.Write(high + " ");

        total = 0;

        // Find the resultant string
        for (int i = 0; i < 26; i++) {

            if (amounts[i] > 0) {
                total += (amounts[i] - 1)
                             / high
                         + 1;

                for (int j = 0;
                     j < ((amounts[i] - 1)
                              / high
                          + 1);
                     j++) {

                    // Generate the subsequence
                    ans += (char)(i + 97);
                }
            }
        }

        // If the length of resultant
        // string is less than N than
        // add a character 'a'
        for (int i = total; i < N; i++) {
            ans += 'a';
        }

        string reverse = "";
        int Len = ans.Length - 1; 
            while(Len >= 0) 
            { 
                reverse = reverse + ans[Len]; 
                Len--; 
            }

        // Print the string
        Console.Write(reverse);
    }
}

// Driver Code
public static void Main()
{
    string S = "toffee";
    int K = 4;
    findString(S, K);
}
}

// This code is contributed by splevel62.
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to find the minimum number
// of string required to generate
// the original string
function findString(S, N)
{

  // Stores the frequency of each
  // character of String S
  let amounts = new Array(26);

  // Iterate over the range [0, 25]
  for (let i = 0; i < 26; i++) {
    amounts[i] = 0;
  }

  // Stores the frequency of each
  // character of String S
  for (let i = 0; i < S.length; i++) {
    amounts[S[i].charCodeAt(0) - 97]++;
  }

  let count = 0;

  // Count unique characters in S
  for (let i = 0; i < 26; i++) {
    if (amounts[i] > 0) count++;
  }

  // If unique characters is greater
  // then N, then return -1
  if (count > N) {
    document.write("-1");
  }

  // Otherwise
  else {
    let ans = "";
    let high = 100001;
    let low = 0;
    let mid, total;

    // Perform Binary Search
    while (high - low > 1) {
      total = 0;

      // Find the value of mid
      mid = Math.floor((high + low) / 2);

      // Iterate over the range
      // [0, 26]
      for (let i = 0; i < 26; i++) {
        // If the amount[i] is
        // greater than 0
        if (amounts[i] > 0) {
          total += Math.floor((amounts[i] - 1) / mid + 1);
        }
      }

      // Update the ranges
      if (total <= N) {
        high = mid;
      } else {
        low = mid;
      }
    }

    document.write(high + " ");

    total = 0;

    // Find the resultant string
    for (let i = 0; i < 26; i++) {
      if (amounts[i] > 0) {
        total += Math.floor((amounts[i] - 1) / high + 1);

        for (let j = 0; j < Math.floor((amounts[i] - 1) / high + 1); j++) {
          // Generate the subsequence
          ans += String.fromCharCode(i + 97);
        }
      }
    }

    // If the length of resultant
    // string is less than N than
    // add a character 'a'
    for (let i = total; i < N; i++) {
      ans += "a";
    }

    ans =  ans.split("").reverse().join("");

    // Print the string
    document.write(ans);
  }
}

// Driver Code

let S = "toffee";
let K = 4;
findString(S, K);

// This code is contributed by _saurabh_jaiswal.
</script>
```

****Output:** 

```
2 tofe
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**
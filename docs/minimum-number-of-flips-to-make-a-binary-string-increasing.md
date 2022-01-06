# 使二进制字符串增加的最小翻转次数

> 原文:[https://www . geeksforgeeks . org/最小翻转次数使二进制字符串增加/](https://www.geeksforgeeks.org/minimum-number-of-flips-to-make-a-binary-string-increasing/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到使给定二进制字符串增加所需的最小字符数。

**示例:**

> **输入:**S =“00110”
> **输出:** 1
> **解释:**翻转字符串的 S[4]=“0”到“1”将给定字符串修改为“00111”。因此，所需的最小翻转次数为 1。
> 
> **输入:**S = " 010110 "
> T3】输出: 2

**方法:**给定的问题可以通过使用 [贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决，该算法基于这样的观察，即在任何次数的翻转之后，结果单调增加的字符串将具有形式**(‘0’* p+‘1’* q)**，其中 **p** 和 **q** 分别是修改后的字符串中 0 和 1 的计数。其思想是[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，对于每个索引， **i** 将[子串](https://www.geeksforgeeks.org/substring-in-cpp/)**S【0，i)** 修改为 **0s** ，将子串**S【I，N】**修改为 **1s** ，并据此找到所需的最小翻转。按照以下步骤解决问题:

*   [在给定的二进制字符串](https://www.geeksforgeeks.org/given-binary-string-count-number-substrings-start-end-1/) **S** 中找到 **0s** 的计数，并将其存储在变量 **countZero** 中。
*   初始化变量，将**最小翻转**设为**(N–cntZero)**，存储所需的最小翻转次数。
*   初始化变量，将 **cntOne** 设为 **0** ，在遍历字符串时存储字符串中 **1s** 的计数。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   如果字符 **S[i]** 为 **0** ，则**的值递减 0**到 **1** 。
    *   否则，将 **minFlips** 的值更新为 **minFlips** 和 **(countZero + countOne)** 的最小值，并将 **countOne** 的值增加 **1** 。
*   完成以上步骤后，打印 **minFlips** 的值作为结果。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach;

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// flips required to make string increasing
int minimumFlips(string s)
{

  // Length of s
  int n = s.size();

  // Total number of zero in s
  int cnt0 = count(s.begin(), s.end(), '0');

  // Stores count of 1s till ith index
  int cnt1 = 0;

  // stores the minimum count of flip
  int res = n - cnt0;

  // Traverse the given string
  for (int i = 0; i < n; i++) {
    if (s[i] == '0') {
      cnt0 -= 1;
    }

    // Update the value of res
    // and count of 1s
    else if (s[i] == '1') {
      res = min(res, cnt1 + cnt0);
      cnt1++;
    }
  }

  // Return the minimum number
  // of flips
  return res;
}

// Driver code
int main()
{

  // Given string
  string S = "000110";

  // function call
  cout << minimumFlips(S);
  return 0;
}

// This code is contributed by parthmanchanda81
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach;
import java.util.*;

class GFG
{

    // Function to find the minimum number of
    // flips required to make String increasing
    static int minimumFlips(String s) {

        // Length of s
        int n = s.length();

        // Total number of zero in s
        int cnt0 = count(s, '0');

        // Stores count of 1s till ith index
        int cnt1 = 0;

        // stors the minimum count of flip
        int res = n - cnt0;

        // Traverse the given String
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == '0') {
                cnt0 -= 1;
            }

            // Update the value of res
            // and count of 1s
            else if (s.charAt(i) == '1') {
                res = Math.min(res, cnt1 + cnt0);
                cnt1++;
            }
        }

        // Return the minimum number
        // of flips
        return res;
    }

    private static int count(String s, char c) {
        int ans = 0;
        for (char i : s.toCharArray())
            if (c == i)
                ans++;
        return ans;
    }

    // Driver code
    public static void main(String[] args) {

        // Given String
        String S = "000110";

        // function call
        System.out.print(minimumFlips(S));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program for above approachthe

# Function to find the minimum number of
# flips required to make string increasing
def minimumFlips(s):

    # Length of s
    n = len(s)

    # Total number of zero in s
    cnt0 = s.count('0')

    # Stores count of 1s till ith index
    cnt1 = 0

    # Stores the minimum count of flips
    res = n - cnt0

    # Traverse the given string S
    for i in range(n):

        if s[i] == '0':
            cnt0 -= 1

        elif s[i] == '1':

            # Update the value of res
            # and count of 1s
            res = min(res, cnt1 + cnt0)
            cnt1 += 1

    # Return the minimum number
    # of flips
    return res

# Driver Code
S = '000110'

# Function Call
print(minimumFlips(S))
```

## C#

```
using System;

public class GFG {
    // Function to find the minimum number of
    // flips required to make String increasing
    static int minimumFlips(String s)
    {

        // Length of s
        int n = s.Length;

        // Total number of zero in s
        int cnt0 = count(s, '0');

        // Stores count of 1s till ith index
        int cnt1 = 0;

        // stors the minimum count of flip
        int res = n - cnt0;

        // Traverse the given String
        for (int i = 0; i < n; i++) {
            if (s[i] == '0') {
                cnt0 -= 1;
            }

            // Update the value of res
            // and count of 1s
            else if (s[i] == '1') {
                res = Math.Min(res, cnt1 + cnt0);
                cnt1++;
            }
        }

        // Return the minimum number
        // of flips
        return res;
    }

    private static int count(String s, char c)
    {
        int ans = 0;
        for (int j = 0; j < s.Length; j++) {
            char i = s[j];
            if (c == i)
                ans++;
        }
        return ans;
    }

    // Driver code
    static public void Main()
    {
        // Given String
        String S = "000110";

        // function call
        Console.Write(minimumFlips(S));
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to find the minimum number of
        // flips required to make string increasing
        function minimumFlips(s) {

            // Length of s
            let n = s.length;

            // Total number of zero in s
            let i;
            let cnt0 = 0;
            for (i = 0; i < n; i++) {
                if (s[i] == '0')
                    cnt0++;

            }

            // Stores count of 1s till ith index
            let cnt1 = 0

            // Stores the minimum count of flips
            let res = n - cnt0

            // Traverse the given string S
            for (i = 0; i < n; i++)
                if (s[i] == '0') {
                    cnt0 -= 1
                }

                else if (s[i] == '1') {

                    // Update the value of res
                    // and count of 1s
                    res = Math.min(res, cnt1 + cnt0)
                    cnt1 += 1
                }

            // Return the minimum number
            // of flips
            return res
        }

        // Driver Code
        S = '000110'

        // Function Call
        document.write(minimumFlips(S))

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
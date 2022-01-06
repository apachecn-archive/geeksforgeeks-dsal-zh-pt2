# 旋转使二进制字符串交替的最小翻转次数

> 原文:[https://www . geeksforgeeks . org/最小翻转次数旋转使二进制字符串交替/](https://www.geeksforgeeks.org/minimum-number-of-flips-with-rotation-to-make-binary-string-alternating/)

给定一个二进制字符串 **S** 的 **0s** 和 **1s** 。任务是通过以下操作使给定的字符串成为一系列替换字符:

*   从开头去掉一些前缀，并附加到结尾。
*   翻转给定字符串中的部分或所有位。

打印要翻转的最小位数，使给定字符串交替出现。

**示例:**

> **输入:** S = "001"
> **输出:** 0
> **解释:**
> 不需要翻转任何元素我们可以利用左旋转:010 得到交替顺序。
> 
> **输入:** S = "000001100"
> **输出:** 3
> **解释:**
> 以下步骤求最小空翻得到交替串:
> 1。向左旋转弦 6 次后，我们将得到:100000001
> 2。现在我们可以应用翻转操作如下:101000001->101010001->101010101
> 这样，使串交替的最小翻转是 3。

**天真方法:**天真方法是取所有 **N** 个可能的组合，并计算[在每个字符串中翻转](https://www.geeksforgeeks.org/number-flips-make-binary-string-alternate/)的最小位数。打印所有此类组合中的最小计数。
***时间复杂度:** O(N <sup>2</sup> ，其中 N 为弦的长度。*
***辅助空间:** O(N)*

**有效方法:**这可以通过观察最终的字符串将是类型**“101010……”**或**“010101……”**来解决，使得所有 **1s** 将处于奇数位置或偶数位置。按照以下步骤解决问题:

1.  创建一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，其中**pref【I】**表示在索引 I 之前需要进行的一些更改。
2.  为以上两种模式创建前缀数组。
3.  检查每一个 **i** ，如果**子串【0，I】**被附加在末尾，需要翻转多少字符。
4.  打印上述步骤中所有子字符串中的最小翻转次数。

为什么只考虑**奇数长度的弦进行旋转**，为什么**旋转对偶数长度的**弦没有影响？

我将用下面的例子来解释这一点，

假设你有偶数长度的序列 011000。没有旋转，可以改为 010101 或 101010。现在假设您选择在末尾追加 01。序列变为 100001，可以更改为 010101 或 101010。如果你比较每个字符，你会发现这和没有旋转的情况是一样的。在这两种情况下，1000 对应于 0101 或 1010，01 对应于 01 或 10。

但是现在考虑一个奇数长度的情况，01100。没有旋转，可以改为 01010 或 10101。现在假设您选择在末尾追加 01。序列变为 10001，可以更改为 01010 或 10101。现在，如果您比较每个字符，您会看到 100 在两种情况下都对应于 010 或 101，但是当 100 在没有旋转的情况下是 010，在旋转的情况下是 101 时，01 对应于 01。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the minimum
// number of flips to make the
// binary string alternating if
// left circular rotation is allowed
int MinimumFlips(string s, int n)
{
    int a[n];

    for(int i = 0; i < n; i++)
    {
        a[i] = (s[i] == '1' ? 1 : 0);
    }

    // Initialize prefix arrays to store
    // number of changes required to put
    // 1s at either even or odd position
    int oddone[n + 1];
    int evenone[n + 1];

    oddone[0] = 0;
    evenone[0] = 0;

    for(int i = 0; i < n; i++)
    {

        // If i is odd
        if (i % 2 != 0)
        {

            // Update the oddone
            // and evenone count
            oddone[i + 1] = oddone[i] +
                                (a[i] == 1 ? 1 : 0);
            evenone[i + 1] = evenone[i] +
                                  (a[i] == 0 ? 1 : 0);
        }

        // Else i is even
        else
        {

            // Update the oddone
            // and evenone count
            oddone[i + 1] = oddone[i] +
                                (a[i] == 0 ? 1 : 0);
            evenone[i + 1] = evenone[i] +
                                  (a[i] == 1 ? 1 : 0);
        }
    }

    // Initialize minimum flips
    int minimum = min(oddone[n], evenone[n]);

    // Check if substring[0, i] is
    // appended at end how many
    // changes will be required
    for(int i = 0; i < n; i++)
    {
        if (n % 2 != 0)
        {
            minimum = min(minimum,
                          oddone[n] -
                          oddone[i + 1] +
                         evenone[i + 1]);
            minimum = min(minimum,
                          evenone[n] -
                          evenone[i + 1] +
                           oddone[i + 1]);
        }
    }

    // Return minimum flips
    return minimum;
}

// Driver Code
int main()
{

    // Given String
    string S = "000001100";

    // Length of given string
    int n = S.length();

    // Function call
    cout << (MinimumFlips(S, n));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function that finds the minimum
    // number of flips to make the
    // binary string alternating if
    // left circular rotation is allowed
    static int MinimumFlips(String s, int n)
    {
        int[] a = new int[n];

        for (int i = 0; i < n; i++) {
            a[i] = (s.charAt(i) == '1' ? 1 : 0);
        }

        // Initialize prefix arrays to store
        // number of changes required to put
        // 1s at either even or odd position
        int[] oddone = new int[n + 1];
        int[] evenone = new int[n + 1];

        oddone[0] = 0;
        evenone[0] = 0;

        for (int i = 0; i < n; i++) {

            // If i is odd
            if (i % 2 != 0) {

                // Update the oddone
                // and evenone count
                oddone[i + 1]
                    = oddone[i]
                      + (a[i] == 1 ? 1 : 0);
                evenone[i + 1]
                    = evenone[i]
                      + (a[i] == 0 ? 1 : 0);
            }

            // Else i is even
            else {

                // Update the oddone
                // and evenone count
                oddone[i + 1]
                    = oddone[i]
                      + (a[i] == 0 ? 1 : 0);
                evenone[i + 1]
                    = evenone[i]
                      + (a[i] == 1 ? 1 : 0);
            }
        }

        // Initialize minimum flips
        int minimum = Math.min(oddone[n],
                               evenone[n]);

        // Check if substring[0, i] is
        // appended at end how many
        // changes will be required
        for (int i = 0; i < n; i++) {
            if (n % 2 != 0) {
                minimum = Math.min(minimum,
                                   oddone[n]
                                       - oddone[i + 1]
                                       + evenone[i + 1]);
                minimum = Math.min(minimum,
                                   evenone[n]
                                       - evenone[i + 1]
                                       + oddone[i + 1]);
            }
        }

        // Return minimum flips
        return minimum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given String
        String S = "000001100";

        // Length of given string
        int n = S.length();

        // Function call
        System.out.print(MinimumFlips(S, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the minimum
# number of flips to make the
# binary string alternating if
# left circular rotation is allowed
def MinimumFlips(s, n):

    a = [0] * n

    for i in range(n):
        a[i] = 1 if s[i] == '1' else 0

    # Initialize prefix arrays to store
    # number of changes required to put
    # 1s at either even or odd position
    oddone = [0] * (n + 1)
    evenone = [0] * (n + 1)

    for i in range(n):

        # If i is odd
        if(i % 2 != 0):

            # Update the oddone
            # and evenone count
            if(a[i] == 1):
                oddone[i + 1] = oddone[i] + 1
            else:
                oddone[i + 1] = oddone[i] + 0

            if(a[i] == 0):
                evenone[i + 1] = evenone[i] + 1
            else:
                evenone[i + 1] = evenone[i] + 0

        # Else i is even
        else:

            # Update the oddone
            # and evenone count
            if (a[i] == 0):
                oddone[i + 1] = oddone[i] + 1
            else:
                oddone[i + 1] = oddone[i] + 0

            if (a[i] == 1):
                evenone[i + 1] = evenone[i] + 1
            else:
                evenone[i + 1] = evenone[i] + 0

    # Initialize minimum flips
    minimum = min(oddone[n], evenone[n])

    # Check if substring[0, i] is
    # appended at end how many
    # changes will be required
    for i in range(n):
        if(n % 2 != 0):
            minimum = min(minimum,
                          oddone[n] -
                          oddone[i + 1] +
                         evenone[i + 1])

            minimum = min(minimum,
                          evenone[n] -
                          evenone[i + 1] +
                           oddone[i + 1])

    # Return minimum flips
    return minimum

# Driver Code

# Given String
S = "000001100"

# Length of given string
n = len(S)

# Function call
print(MinimumFlips(S, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

  // Function that finds the minimum
  // number of flips to make the
  // binary string alternating if
  // left circular rotation is allowed
  static int MinimumFlips(String s, int n)
  {
    int[] a = new int[n];

    for (int i = 0; i < n; i++)
    {
      a[i] = (s[i] == '1' ? 1 : 0);
    }

    // Initialize prefix arrays to store
    // number of changes required to put
    // 1s at either even or odd position
    int[] oddone = new int[n + 1];
    int[] evenone = new int[n + 1];

    oddone[0] = 0;
    evenone[0] = 0;

    for (int i = 0; i < n; i++)
    {

      // If i is odd
      if (i % 2 != 0)
      {

        // Update the oddone
        // and evenone count
        oddone[i + 1] = oddone[i] +
                         (a[i] == 1 ? 1 : 0);
        evenone[i + 1] = evenone[i] +
                          (a[i] == 0 ? 1 : 0);
      }

      // Else i is even
      else
      {

        // Update the oddone
        // and evenone count
        oddone[i + 1] = oddone[i] +
                         (a[i] == 0 ? 1 : 0);
        evenone[i + 1] = evenone[i] +
                          (a[i] == 1 ? 1 : 0);
      }
    }

    // Initialize minimum flips
    int minimum = Math.Min(oddone[n],
                           evenone[n]);

    // Check if substring[0, i] is
    // appended at end how many
    // changes will be required
    for (int i = 0; i < n; i++)
    {
      if (n % 2 != 0)
      {
        minimum = Math.Min(minimum, oddone[n] -
                                       oddone[i + 1] +
                                    evenone[i + 1]);
        minimum = Math.Min(minimum, evenone[n] -
                                       evenone[i + 1] +
                                       oddone[i + 1]);
      }
    }

    // Return minimum flips
    return minimum;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    // Given String
    String S = "000001100";

    // Length of given string
    int n = S.Length;

    // Function call
    Console.Write(MinimumFlips(S, n));
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program for the
// above approach

    // Function that finds the minimum
    // number of flips to make the
    // binary string alternating if
    // left circular rotation is allowed
    function MinimumFlips(s, n)
    {
        let a = Array.from({length: n+1}, (_, i) => 0);

        for (let i = 0; i < n; i++) {
            a[i] = (s[i] == '1' ? 1 : 0);
        }

        // Initialize prefix arrays to store
        // number of changes required to put
        // 1s at either even or odd position
        let oddone = Array.from({length: n+1}, (_, i) => 0);
        let evenone = Array.from({length: n+1}, (_, i) => 0);

        oddone[0] = 0;
        evenone[0] = 0;

        for (let i = 0; i < n; i++) {

            // If i is odd
            if (i % 2 != 0) {

                // Update the oddone
                // and evenone count
                oddone[i + 1]
                    = oddone[i]
                      + (a[i] == 1 ? 1 : 0);
                evenone[i + 1]
                    = evenone[i]
                      + (a[i] == 0 ? 1 : 0);
            }

            // Else i is even
            else {

                // Update the oddone
                // and evenone count
                oddone[i + 1]
                    = oddone[i]
                      + (a[i] == 0 ? 1 : 0);
                evenone[i + 1]
                    = evenone[i]
                      + (a[i] == 1 ? 1 : 0);
            }
        }

        // Initialize minimum flips
        let minimum = Math.min(oddone[n],
                               evenone[n]);

        // Check if substring[0, i] is
        // appended at end how many
        // changes will be required
        for (let i = 0; i < n; i++) {
            if (n % 2 != 0) {
                minimum = Math.min(minimum,
                                   oddone[n]
                                       - oddone[i + 1]
                                       + evenone[i + 1]);
                minimum = Math.min(minimum,
                                   evenone[n]
                                       - evenone[i + 1]
                                       + oddone[i + 1]);
            }
        }

        // Return minimum flips
        return minimum;
    }

// Driver Code

     // Given String
        let S = "000001100";

        // Length of given string
        let n = S.length;

        // Function call
        document.write(MinimumFlips(S, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)，其中 N 是给定字符串的长度。*
***辅助空间:** O(N)*
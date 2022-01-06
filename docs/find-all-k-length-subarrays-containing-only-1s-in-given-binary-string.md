# 找出给定二进制串中所有只包含 1 的 K 长度子阵

> 原文:[https://www . geesforgeks . org/find-all-k-length-subarrays-只包含给定二进制字符串中的-1s/](https://www.geeksforgeeks.org/find-all-k-length-subarrays-containing-only-1s-in-given-binary-string/)

给定一个[二进制串](https://www.geeksforgeeks.org/tag/binary-string/) **串【】**，任务是找到所有可能的 **K** 长度子阵，只包含 **1s** 并打印它们的开始和结束索引。

**示例:**

> **输入:** str = "0101000 "，K=1
> **输出:**
> 1 1
> 3
> **说明:**位置 1 和 3 的子串是值为 1 的子串。
> 
> **输入:** str = "11111001 "，K=3
> **输出:**
> 0 2
> 1 3
> 2 4

**方法:**借助[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)可以解决给定的问题。创建一个大小为 **K** 的窗口，最初从范围 **0** 到 **K-1** 计算 **1s** 。然后从索引 **1** 到 **N-1** 遍历字符串，减去 **i-1** 的值，将 **i+K** 的值加到当前计数中。如果当前计数等于 **K** ，打印 **i** 和 **i+k-1** 的值作为可能的子阵列之一。按照以下步骤解决问题:

*   将变量**初始化为 **0。****
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K)** ，并执行以下任务:
    *   如果 **s[i]** 等于 **1** ，那么将**的碳纳米管**的值增加 **1。**
*   如果 **cntOf1s** 等于 **K** ，则打印当前子串作为答案之一。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N)** ，并执行以下任务:
    *   如果该位置的字符为 **1，则从左边减少该值，从右边增加变量 **cntOf1s** 。**
    *   如果 **cntOf1s** 的值等于 **K** ，则打印当前子串作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all possible
// k length subarrays
void get(string s, int k)
{
    int n = s.length();

    int cntOf1s = 0;

    // Initial window
    for (int i = 0; i < k; i++)
        if (s[i] == '1')
            cntOf1s++;

    if (cntOf1s == k)
        cout << 0 << " " << k - 1 << endl;

    // Traverse the string
    for (int i = 1; i < n; i++) {

        // Subtract the value from the left and
        // add from the right
        cntOf1s = cntOf1s - (s[i - 1] - '0')
                  + (s[i + k - 1] - '0');

        // Check the condition
        if (cntOf1s == k)
            cout << i << " " << i + k - 1 << endl;
    }
}

// Driver Code
int main()
{
    string str = "0110101110";
    int K = 2;
    get(str, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find all possible
// k length subarrays
static void get(char[] s, int k)
{
    int n = s.length;

    int cntOf1s = 0;

    // Initial window
    for (int i = 0; i < k; i++)
        if (s[i] == '1')
            cntOf1s++;

    if (cntOf1s == k)
        System.out.print(0+ " " +  (k - 1 )+"\n");

    // Traverse the String
    for (int i = 1; i < n && (i + k - 1)<n; i++) {

        // Subtract the value from the left and
        // add from the right
        cntOf1s = cntOf1s - (s[i - 1] - '0')
                  + (s[i + k - 1] - '0');

        // Check the condition
        if (cntOf1s == k)
            System.out.print(i+ " " +  (i + k - 1 )+"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "0110101110";
    int K = 2;
    get(str.toCharArray(), K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python3 program for the above approach

# Function to find all possible
# k length subarrays
def get(s, k):

    n = len(s)
    cntOf1s = 0

    # Initial window
    for i in range(0, k):
        if (s[i] == '1'):
            cntOf1s += 1

    if (cntOf1s == k):
        print(f"{0} {k - 1}")

    # Traverse the string
    for i in range(1, n - k + 1):

        # Subtract the value from the left and
        # add from the right
        cntOf1s = cntOf1s - (ord(s[i - 1]) - ord('0')) + \
            (ord(s[i + k - 1]) - ord('0'))

        # Check the condition
        if (cntOf1s == k):
            print(f"{i} {i + k - 1}")

# Driver Code
if __name__ == "__main__":

    str = "0110101110"
    K = 2
    get(str, K)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find all possible
  // k length subarrays
  static void get(char[] s, int k)
  {
    int n = s.Length;

    int cntOf1s = 0;

    // Initial window
    for (int i = 0; i < k; i++)
      if (s[i] == '1')
        cntOf1s++;

    if (cntOf1s == k)
      Console.Write(0 + " " + (k - 1) + "\n");

    // Traverse the String
    for (int i = 1; i < n && (i + k - 1) < n; i++)
    {

      // Subtract the value from the left and
      // add from the right
      cntOf1s = cntOf1s - (s[i - 1] - '0')
        + (s[i + k - 1] - '0');

      // Check the condition
      if (cntOf1s == k)
        Console.Write(i + " " + (i + k - 1) + "\n");
    }
  }

  // Driver Code
  public static void Main()
  {
    String str = "0110101110";
    int K = 2;
    get(str.ToCharArray(), K);
  }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find all possible
      // k length subarrays
      function get(s, k) {
          let n = s.length;

          let cntOf1s = 0;

          // Initial window
          for (let i = 0; i < k; i++)
              if (s[i] == '1')
                  cntOf1s++;

          if (cntOf1s == k)
              document.write(0 + ' ' + (k - 1) + '<br>');

          // Traverse the string
          for (let i = 1; i < n; i++) {

              // Subtract the value from the left and
              // add from the right
              cntOf1s = cntOf1s - (s[i - 1].charCodeAt(0) - '0'.charCodeAt(0))
                  + (s[i + k - 1].charCodeAt(0) - '0'.charCodeAt(0));

              // Check the condition
              if (cntOf1s == k)
                  document.write(i + ' ' + (i + k - 1) + '<br>');
          }
      }

      // Driver Code
      let str = "0110101110";

      let K = 2;
      get(str, K);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
1 2
6 7
7 8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
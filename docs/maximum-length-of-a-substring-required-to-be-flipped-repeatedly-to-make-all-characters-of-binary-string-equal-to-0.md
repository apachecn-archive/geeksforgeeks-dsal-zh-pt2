# 为使二进制字符串的所有字符都等于 0 需要反复翻转的子字符串的最大长度

> 原文:[https://www . geesforgeks . org/最大长度子字符串-需要反复翻转才能使二进制字符串的所有字符等于 0/](https://www.geeksforgeeks.org/maximum-length-of-a-substring-required-to-be-flipped-repeatedly-to-make-all-characters-of-binary-string-equal-to-0/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到需要反复翻转的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的最大长度，使一个二进制字符串的所有字符等于**“0”**。

**示例:**

> **输入:** S = "010"
> **输出:** 2
> **说明:**
> 以下是 K 值为 2 的至少为 K 的子串的翻转顺序:
> 
> *   翻转长度为 3(>= K)的子字符串 S[0，2]会将字符串 S 修改为“101”。
> *   翻转长度为 2(>= K)的子字符串 S[0，1]会将字符串 S 修改为“011”。
> *   翻转长度为 2(>= K)的子字符串 S[1，2]会将字符串 S 修改为“000”。
> 
> 对于 K 值为 2(这是最大可能值)，字符串的所有字符都可以设为 0。因此，打印 2。
> 
> **输入:**S = " 00001111 "
> T3】输出: 4

**方法:**给定的问题可以通过[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 来解决，现在如果在任何一点相邻的字符不相同，那么翻转一个子字符串 **LHS** 或 **RHS** 。为此，取 **LHS** 和 **RHS** 的最大长度。可以有多个相邻的字符不相等的地方。对于每对[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，所需的最大值会有所不同。现在将所有字符更改为**‘0’**在所有最大值中取最小值。按照以下步骤解决问题:

*   初始化变量，说**和**为 **N** ，存储 **K** 的最大可能值。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1)**，并执行以下步骤:
    *   如果 **s[i]** 和 **s[i + 1]** 的值不相同，那么将 **ans** 的值更新为 **ans** 的最小值或 **(i + 1)** 或**(N–I–1)**的最大值。
*   执行上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value of K
// such that flipping substrings of size
// at least K make all characters 0s
int maximumK(string& S)
{
    int N = S.length();

    // Stores the maximum value of K
    int ans = N;

    int flag = 0;

    // Traverse the given string S
    for (int i = 0; i < N - 1; i++) {

        // Store the minimum of the
        // maximum of LHS and RHS length
        if (S[i] != S[i + 1]) {

            // Flip performed
            flag = 1;
            ans = min(ans, max(i + 1,
                               N - i - 1));
        }
    }

    // If no flips performed
    if (flag == 0)
        return 0;

    // Return the possible value of K
    return ans;
}

// Driver Code
int main()
{
    string S = "010";
    cout << maximumK(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;

class GFG{

// Function to find the maximum value of K
// such that flipping substrings of size
// at least K make all characters 0s
static int maximumK(String S)
{
    int N = S.length();

    // Stores the maximum value of K
    int ans = N;

    int flag = 0;

    // Traverse the given string S
    for (int i = 0; i < N - 1; i++) {

        // Store the minimum of the
        // maximum of LHS and RHS length
        if (S.charAt(i) != S.charAt(i + 1)) {

            // Flip performed
            flag = 1;
            ans = Math.min(ans, Math.max(i + 1,
                               N - i - 1));
        }
    }

    // If no flips performed
    if (flag == 0)
        return 0;

    // Return the possible value of K
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String S = "010";
    System.out.print(maximumK(S));
}
}

// This code is contributed by target_2.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum value of K
# such that flipping substrings of size
# at least K make all characters 0s
def maximumK(S):
    N = len(S)

    # Stores the maximum value of K
    ans = N

    flag = 0

    # Traverse the given string S
    for i in range(N - 1):

        # Store the minimum of the
        # maximum of LHS and RHS length
        if (S[i] != S[i + 1]):

            # Flip performed
            flag = 1
            ans = min(ans, max(i + 1,N - i - 1))

    # If no flips performed
    if (flag == 0):
        return 0

    # Return the possible value of K
    return ans

# Driver Code
if __name__ == '__main__':
    S = "010"
    print(maximumK(S))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# code for the above approach
using System;

public class GFG {
    // Function to find the maximum value of K
    // such that flipping substrings of size
    // at least K make all characters 0s
    static int maximumK(String S)
    {
        int N = S.Length;

        // Stores the maximum value of K
        int ans = N;

        int flag = 0;

        // Traverse the given string S
        for (int i = 0; i < N - 1; i++) {

            // Store the minimum of the
            // maximum of LHS and RHS length
            if (S[i] != S[i + 1]) {

                // Flip performed
                flag = 1;
                ans = Math.Min(ans,
                               Math.Max(i + 1, N - i - 1));
            }
        }

        // If no flips performed
        if (flag == 0)
            return 0;

        // Return the possible value of K
        return ans;
    }

    // Driver Code

    static public void Main()
    {

        // Code
        string S = "010";
        Console.Write(maximumK(S));
    }
}
// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum value of K
// such that flipping substrings of size
// at least K make all characters 0s
function maximumK(S)
{
  let N = S.length;

  // Stores the maximum value of K
  let ans = N;
  let flag = 0;

  // Traverse the given string S
  for (let i = 0; i < N - 1; i++)
  {

    // Store the minimum of the
    // maximum of LHS and RHS length
    if (S[i] != S[i + 1])
    {

      // Flip performed
      flag = 1;
      ans = Math.min(ans, Math.max(i + 1, N - i - 1));
    }
  }

  // If no flips performed
  if (flag == 0) return 0;

  // Return the possible value of K
  return ans;
}

// Driver Code
let S = "010";
document.write(maximumK(S));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
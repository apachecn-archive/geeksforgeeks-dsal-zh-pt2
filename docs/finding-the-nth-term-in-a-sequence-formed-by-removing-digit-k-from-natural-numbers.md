# 在从自然数中去掉数字 K 形成的序列中找到第 n 项

> 原文:[https://www . geeksforgeeks . org/find-通过从自然数中移除数字 k 形成的序列中的第 n 个术语/](https://www.geeksforgeeks.org/finding-the-nth-term-in-a-sequence-formed-by-removing-digit-k-from-natural-numbers/)

给定整数 **N，K** 和一个无限的自然数序列，其中包含数字 **K** (1 < =K < =9)的所有数字都被移除。任务是返回该序列的第 n 个**号**号。

**示例:**

> **输入:** N = 12，K = 2
> **输出:** 14
> **解释:**为上述输入生成的序列如下:1，3，4，5，6，7，8，9，10，11，13，14，15，16，17，直到无穷大
> 
> **输入:** N = 10，K = 1
> T3】输出: 22

**天真方法:**解决上述问题的基本方法是迭代到 N，并保持排除所有包含给定数字 k 的小于 N 的数字。最后，打印获得的第 N 个自然数。
时间复杂度:O(N)
辅助空间:O(1)

**有效方法:**解决这个问题的有效方法是从[第 n 个自然数中去掉所有由数字 9 组成的数字](https://www.geeksforgeeks.org/nth-natural-number-after-removing-all-numbers-consisting-of-the-digit-9/)得到的灵感。
给定问题可以通过将 **K** 的值转换为大于 8 的基础 9 形态来解决。可以遵循以下步骤:

*   计算以 9 为基数的第 n 个自然数
*   从大于或等于 K 的 9 进制数的每一位开始递增 1
*   下一个数字是想要的答案

以下是上述方法的代码:

## C++

```
// C++ implementation for the above approach

#include <iostream>
using namespace std;
long long convertToBase9(long long n)
{
    long long ans = 0;

    // Denotes the digit place
    long long a = 1;

    // Method to convert any number
    // to binary equivalent
    while (n > 0) {
        ans += (a * (n % 9));
        a *= 10;
        n /= 9;
    }
    return ans;
}

long long getNthnumber(long long base9,
                       long long K)
{
    long long ans = 0;

    // denotes the current digits place
    long long a = 1;
    while (base9 > 0) {
        int cur = base9 % 10;

        // If current digit is >= K
        // increment its value by 1
        if (cur >= K) {
            ans += a * (cur + 1);
        }

        // Else add the digit as it is
        else {
            ans += a * cur;
        }
        base9 /= 10;

        // Move to the next digit
        a *= 10;
    }
    return ans;
}

// Driver code
int main()
{
    long long N = 10, K = 1;
    long long base9 = convertToBase9(N);
    cout << getNthnumber(base9, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;

class GFG {

      static long convertToBase9(long n)
    {
        long ans = 0;

        // Denotes the digit place
        long a = 1;

        // Method to convert any number
        // to binary equivalent
        while (n > 0) {
            ans += (a * (n % 9));
            a *= 10;
            n /= 9;
        }
        return ans;
    }

    static long getNthnumber(long base9,
                          long K)
    {
        long ans = 0;

        // denotes the current digits place
        long a = 1;
        while (base9 > 0) {
            int cur = (int)(base9 % 10);

            // If current digit is >= K
            // increment its value by 1
            if (cur >= K) {
                ans += a * (cur + 1);
            }

            // Else add the digit as it is
            else {
                ans += a * cur;
            }
            base9 /= 10;

            // Move to the next digit
            a *= 10;
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args) {
        long N = 10, K = 1;
        long base9 = convertToBase9(N);
        System.out.println(getNthnumber(base9, K));
    }
}

//  This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach
def convertToBase9(n):
    ans = 0

    # Denotes the digit place
    a = 1

    # Method to convert any number
    # to binary equivalent
    while(n > 0):
        ans += (a * (n % 9))
        a *= 10
        n //= 9
    return ans

def getNthnumber(base9, K):
    ans = 0

    # denotes the current digits place
    a = 1
    while (base9 > 0):
        cur = base9 % 10

        # If current digit is >= K
        # increment its value by 1
        if (cur >= K):
            ans += a * (cur + 1)

        # Else add the digit as it is
        else:
            ans += a * cur
        base9 //= 10

        # Move to the next digit
        a *= 10
    return ans

# Driver code
if __name__ == '__main__':
    N = 10
    K = 1
    base9 = convertToBase9(N)
    print(getNthnumber(base9, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# implementation for the above approach
using System;

class GFG {

      static long convertToBase9(long n)
    {
        long ans = 0;

        // Denotes the digit place
        long a = 1;

        // Method to convert any number
        // to binary equivalent
        while (n > 0) {
            ans += (a * (n % 9));
            a *= 10;
            n /= 9;
        }
        return ans;
    }

    static long getNthnumber(long base9,
                          long K)
    {
        long ans = 0;

        // denotes the current digits place
        long a = 1;
        while (base9 > 0) {
            int cur = (int)(base9 % 10);

            // If current digit is >= K
            // increment its value by 1
            if (cur >= K) {
                ans += a * (cur + 1);
            }

            // Else add the digit as it is
            else {
                ans += a * cur;
            }
            base9 /= 10;

            // Move to the next digit
            a *= 10;
        }
        return ans;
    }

    // Driver code
    public static void Main (String[] args) {
        long N = 10, K = 1;
        long base9 = convertToBase9(N);
        Console.Write(getNthnumber(base9, K));
    }
}

//  This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach
function convertToBase9(n)
{
  let ans = 0;

  // Denotes the digit place
  let a = 1;

  // Method to convert any number
  // to binary equivalent
  while (n > 0) {
    ans += a * (n % 9);
    a *= 10;
    n = Math.floor(n / 9);
  }
  return ans;
}

function getNthnumber(base9, K) {
  let ans = 0;

  // denotes the current digits place
  let a = 1;
  while (base9 > 0) {
    let cur = base9 % 10;

    // If current digit is >= K
    // increment its value by 1
    if (cur >= K) {
      ans += a * (cur + 1);
    }

    // Else add the digit as it is
    else {
      ans += a * cur;
    }
    base9 = Math.floor(base9 / 10);

    // Move to the next digit
    a *= 10;
  }
  return ans;
}

// Driver code
let N = 10,
  K = 1;
let base9 = convertToBase9(N);
document.write(getNthnumber(base9, K));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
22
```

**时间复杂度:**O(log<sub>9</sub>N)
T5】辅助空间: O(1)
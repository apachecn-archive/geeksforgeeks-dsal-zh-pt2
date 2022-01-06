# 找到一个三元组(A，B，C)，使得 3*A + 5*B + 7*C 等于 N

> 原文:[https://www . geesforgeks . org/find-a-triple-a-B- c-so-3a-5 B- 7c-等于-n/](https://www.geeksforgeeks.org/find-a-triplet-a-b-c-such-that-3a-5b-7c-is-equal-to-n/)

给定一个整数 **N** ，任务是找出三个正整数 **A** 、 **B** 和 **C** ，使得表达式 **(3*A + 5*B + 7*C)** 的值等于 **N** 。如果不存在这样的三元组，则打印【T12 "-" 1 "。

**示例:**

> **输入:** N = 19
> **输出:**
> A = 3
> B = 2
> C = 0
> **说明:**设置 A、B、C 分别等于 0、1、2，表达式的求值值= 3 * A + 5 * B + 7 * C = 3 * 3 + 5 * 2 + 7 * 0 = 19，与 N = 19 相同。
> 
> **输入:** N = 4
> **输出:** -1

**天真法:**解决问题最简单的方法是[生成所有可能的整数到**N**T5 的三元组，并检查是否存在任何三元组(A，B，C)，使得 **(3*A + 5*B + 7*C)** 的值等于 **N** 。如果发现是真的，那就打印出来。否则，打印**-1”**。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/print-all-triplets-with-given-sum/)

**高效途径:**上述途径可基于以下观察进行优化: **A** 的值位于范围**【0，N/3】**内， **B** 的值位于范围**【0，N/5】**内， **C** 的值位于范围**【0，N/7】**内。按照以下步骤解决问题:

*   [迭代范围](https://www.geeksforgeeks.org/python-program-to-print-all-positive-numbers-in-a-range/)**【0，N/7】**并执行以下操作:
    *   [迭代范围](https://www.geeksforgeeks.org/python-program-to-print-all-positive-numbers-in-a-range/)**【0，N/5】**，求 **A** 的值为**(N–5 * j–7 * I)**。
    *   在上述步骤中，如果 **A** 的值至少为 **0** 和[T5】A 可被**3**T9】整除，则存在一个这样的三元组 **(A/3，I，j)** 。打印此三联体](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)[跳出循环](https://www.geeksforgeeks.org/python-break-statement/)。
*   完成上述步骤后，如果不存在这样的三元组，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a triplet (A, B, C)
// such that 3 * A + 5 * B + 7 * C is N
void CalculateValues(int N){

  int A = 0, B = 0, C = 0;

  // Iterate over the range [0, N//7]
  for (C = 0; C < N/7; C++)
  {

    // Iterate over the range [0, N//5]
    for ( B = 0; B < N/5; B++)
    {

      // Find the value of A
      int A = N - 7 * C - 5 * B;

      // If A is greater than or equal
      // to 0 and divisible by 3
      if (A >= 0 && A % 3 == 0)
      {
        cout << "A = " << A / 3 << ", B = " << B << ", C = "<< C << endl;

        return;
      }
    }
  }

  // Otherwise, print -1
  cout << -1 << endl;

}

// Driver Code
int main()
{
  int N = 19;
  CalculateValues(19);

  return 0;
}

// This code is contributed by susmitakundugoaldanga.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

  // Function to find a triplet (A, B, C)
  // such that 3 * A + 5 * B + 7 * C is N
  static void CalculateValues(int N)
  {
    int A = 0, B = 0, C = 0;

    // Iterate over the range [0, N//7]
    for (C = 0; C < N/7; C++)
    {

      // Iterate over the range [0, N//5]
      for ( B = 0; B < N/5; B++)
      {

        // Find the value of A
        A = N - 7 * C - 5 * B;

        // If A is greater than or equal
        // to 0 and divisible by 3
        if (A >= 0 && A % 3 == 0)
        {
          System.out.print("A = " + A / 3 + ", B = " + B + ", C = "+ C);

          return;
        }
      }
    }

    // Otherwise, print -1
    System.out.println(-1);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 19;
    CalculateValues(19);
  }
}

// This code is contributed by souravghosh0416.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find a triplet (A, B, C)
# such that 3 * A + 5 * B + 7 * C is N
def CalculateValues(N):

    # Iterate over the range [0, N//7]
    for C in range(0, N//7 + 1):

        # Iterate over the range [0, N//5]
        for B in range(0, N//5 + 1):

            # Find the value of A
            A = N - 7 * C - 5 * B

            # If A is greater than or equal
            # to 0 and divisible by 3
            if (A >= 0 and A % 3 == 0):
                print("A =", A / 3, ", B =", B, ", \
                       C =", C, sep =" ")
                return

    # Otherwise, print -1
    print(-1)
    return

# Driver Code
if __name__ == '__main__':

    N = 19
    CalculateValues(19)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to find a triplet (A, B, C)
  // such that 3 * A + 5 * B + 7 * C is N
  static void CalculateValues(int N)
  {
    int A = 0, B = 0, C = 0;

    // Iterate over the range [0, N//7]
    for (C = 0; C < N/7; C++)
    {

      // Iterate over the range [0, N//5]
      for ( B = 0; B < N/5; B++)
      {

        // Find the value of A
        A = N - 7 * C - 5 * B;

        // If A is greater than or equal
        // to 0 and divisible by 3
        if (A >= 0 && A % 3 == 0)
        {
          Console.Write("A = " + A / 3 + ", B = " + B + ", C = "+ C);

          return;
        }
      }
    }

    // Otherwise, print -1
    Console.WriteLine(-1);
  }

  // Driver Code
  static public void Main()
  {
    int N = 19;
    CalculateValues(19);
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find a triplet (A, B, C)
// such that 3 * A + 5 * B + 7 * C is N
function CalculateValues(N){

var A = 0, B = 0, C = 0;

// Iterate over the range [0, N//7]
for (C = 0; C < N/7; C++)
{

    // Iterate over the range [0, N//5]
    for ( B = 0; B < N/5; B++)
    {

    // Find the value of A
    var A = N - 7 * C - 5 * B;

    // If A is greater than or equal
    // to 0 and divisible by 3
    if (A >= 0 && A % 3 == 0)
    {
        document.write( "A = " + A / 3 + ", B = " + B + ", C = "+ C );

        return;
    }
    }
}

// Otherwise, print -1
document.write( -1 );

}

// Driver Code

var N = 19;
CalculateValues(19);

</script>
```

**Output**

```
A = 3, B = 2, C = 0
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
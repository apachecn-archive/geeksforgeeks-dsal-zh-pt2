# 评估表达式(N1 *(N–1)2 *……* 1N)%(109+7)

> 原文:[https://www . geesforgeks . org/evaluate-the-expression-n1-n-12-1n-109-7/](https://www.geeksforgeeks.org/evaluate-the-expression-n1-n-12-1n-109-7/)

给定一个整数 **N** ，任务是求表达式**(N<sup>1</sup>*(N–1)<sup>2</sup>*……* 1<sup>N</sup>)%(10<sup>9</sup>+7)**。

> **输入:** N = 1
> **输出:** 1
> **解释:**
> 1 <sup>1</sup> = 1
> 
> **输入:** N = 4
> **输出:** 288
> **解释:**
> 4<sup>1</sup>*(4–1)<sup>2</sup>*(4–2)<sup>3</sup>*(4-3)<sup>4</sup>
> = 4 * 9 * 8 * 1
> = 288

**天真方法:**解决这个问题最简单的方法就是迭代**【1，N】**的范围。每次 **i <sup>第</sup>** 次迭代，计算**(N–I+1)<sup>I</sup>**的值。最后，打印每次迭代的所有计算值的乘积。
***时间复杂度:**O(N<sup>2</sup>* log<sub>2</sub>(N))*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> f(N)= N<sup>1</sup>*(N–1)<sup>2</sup>*……* 1<sup>N</sup>T6】= N *(N–1)*(N–1)*(N–2)*(N–2)*(N–2)*(N–2)*…1 * 1 * 1
> = N *(N–1)*(N–2)*……* 1 *(N-1)*(N–2)*…* 1…
> = N！*(N–1)！*(N–2)！* … * 1!

按照以下步骤解决问题:

*   使用**阶乘(N) = N *阶乘(N–1)**，预计算从 **1** 到 **N** 的阶乘值。
*   迭代范围**【1，N】**，并使用上述观察值找到范围**【1，N】**内所有阶乘的乘积
*   最后，打印表达式的值。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define mod 1000000007

// Function to find the value of the expression
// ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
int ValOfTheExpression(int n)
{

    // factorial[i]: Stores factorial of i
    int factorial[n] = { 0 };

    // Base Case for factorial
    factorial[0] = factorial[1] = 1;

    // Precompute the factorial
    for (int i = 2; i <= n; i++) {
        factorial[i] = ((factorial[i - 1] % mod)
                        * (i % mod))
                       % mod;
    }

    // dp[N]: Stores the value of the expression
    // ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
    int dp[n] = { 0 };
    dp[1] = 1;

    for (int i = 2; i <= n; i++) {

        // Update dp[i]
        dp[i] = ((dp[i - 1] % mod)
                 * (factorial[i] % mod))
                % mod;
    }

    // Return the answer.
    return dp[n];
}

// Driver Code
int main()
{

    int n = 4;
    // Function call
    cout << ValOfTheExpression(n) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{
  static int mod = 1000000007;

  // Function to find the value of the expression
  // ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
  static int ValOfTheExpression(int n)
  {

    // factorial[i]: Stores factorial of i
    int[] factorial = new int[n + 1];

    // Base Case for factorial
    factorial[0] = factorial[1] = 1;

    // Precompute the factorial
    for (int i = 2; i <= n; i++)
    {
      factorial[i] = ((factorial[i - 1] % mod)
                      * (i % mod)) % mod;
    }

    // dp[N]: Stores the value of the expression
    // ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
    int[] dp = new int[n + 1];
    dp[1] = 1;

    for (int i = 2; i <= n; i++)
    {

      // Update dp[i]
      dp[i] = ((dp[i - 1] % mod)
               * (factorial[i] % mod)) % mod;
    }

    // Return the answer.
    return dp[n];
  }

  // Driver code
  public static void main(String[] args) {
    int n = 4;

    // Function call
    System.out.println(ValOfTheExpression(n));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach
mod = 1000000007

# Function to find the value of the expression
# ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
def ValOfTheExpression(n):
    global mod

    # factorial[i]: Stores factorial of i
    factorial = [0 for i in range(n + 1)]

    # Base Case for factorial
    factorial[0] = 1
    factorial[1] = 1

    # Precompute the factorial
    for i in range(2, n + 1, 1):
        factorial[i] = ((factorial[i - 1] % mod) * (i % mod))%mod

    # dp[N]: Stores the value of the expression
    # ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
    dp = [0 for i in range(n+1)]
    dp[1] = 1
    for i in range(2, n + 1, 1):

        # Update dp[i]
        dp[i] = ((dp[i - 1] % mod)*(factorial[i] % mod)) % mod

    # Return the answer.
    return dp[n]

# Driver Code
if __name__ == '__main__':
    n = 4

    # Function call
    print(ValOfTheExpression(n))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  static int mod = 1000000007;

  // Function to find the value of the expression
  // ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
  static int ValOfTheExpression(int n)
  {

    // factorial[i]: Stores factorial of i
    int[] factorial = new int[n + 1];

    // Base Case for factorial
    factorial[0] = factorial[1] = 1;

    // Precompute the factorial
    for (int i = 2; i <= n; i++)
    {
      factorial[i] = ((factorial[i - 1] % mod)
                      * (i % mod))
        % mod;
    }

    // dp[N]: Stores the value of the expression
    // ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
    int[] dp = new int[n + 1];
    dp[1] = 1;

    for (int i = 2; i <= n; i++)
    {

      // Update dp[i]
      dp[i] = ((dp[i - 1] % mod)
               * (factorial[i] % mod))
        % mod;
    }

    // Return the answer.
    return dp[n];
  }

  // Driver code
  static void Main()
  {
    int n = 4;

    // Function call
    Console.WriteLine(ValOfTheExpression(n));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    let mod = 1000000007;

    // Function to find the value of the expression
    // ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
    function ValOfTheExpression(n)
    {

      // factorial[i]: Stores factorial of i
      let factorial = new Array(n + 1);

      // Base Case for factorial
      factorial[0] = factorial[1] = 1;

      // Precompute the factorial
      for (let i = 2; i <= n; i++)
      {
        factorial[i] = ((factorial[i - 1] % mod) *
                        (i % mod)) % mod;
      }

      // dp[N]: Stores the value of the expression
      // ( N^1 * (N – 1)^2 * … * 1^N) % (109 + 7).
      let dp = new Array(n + 1);
      dp[1] = 1;

      for (let i = 2; i <= n; i++)
      {

        // Update dp[i]
        dp[i] = ((dp[i - 1] % mod) *
                 (factorial[i] % mod)) % mod;
      }

      // Return the answer.
      return dp[n];
    }

    let n = 4;

    // Function call
    document.write(ValOfTheExpression(n));

</script>
```

**Output:** 

```
288
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
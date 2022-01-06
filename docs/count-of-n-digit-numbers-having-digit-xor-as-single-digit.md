# 将数字异或为一位数的 N 位数计数

> 原文:[https://www . geeksforgeeks . org/n 位数计数-以位数为单位进行异或运算/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-having-digit-xor-as-single-digit/)

给定一个整数 **N** ，任务是找出 N 位数字的总数，使得数字的位数的[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为一位数。

**示例:**

> **输入:** N = 1
> **输出:** 9
> **说明:**
> 1、2、3、4、5、6、7、8、9 为数字。
> 
> **输入:** N = 2
> **输出:** 66
> **说明:**
> 有 66 个这样的两位数，其位数的异或是一位数。

**方法:**简单的方法是迭代所有 N 位数字，并检查数字的所有数字的[按位异或是否是一个数字。如果是，则将其包括在计数中，否则，检查下一个数字。](https://www.geeksforgeeks.org/bitwise-operations-on-digits-of-a-number/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of N-digit
// numbers with single digit XOR
void countNums(int N)
{

    // Range of numbers
    int l = (int)pow(10, N - 1);
    int r = (int)pow(10, N) - 1;

    int count = 0;
    for(int i = l; i <= r; i++)
    {
        int xorr = 0, temp = i;

        // Calculate XOR of digits
        while (temp > 0)
        {
            xorr = xorr ^ (temp % 10);
            temp /= 10;
        }

        // If XOR <= 9,
        // then increment count
        if (xorr <= 9)
            count++;
    }

    // Print the count
    cout << count;
}

// Driver Code
int main()
{

    // Given number
    int N = 2;

    // Function call
    countNums(N);
}

// This code is contributed by code_hunt
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find count of N-digit
    // numbers with single digit XOR
    public static void countNums(int N)
    {
        // Range of numbers
        int l = (int)Math.pow(10, N - 1),
            r = (int)Math.pow(10, N) - 1;

        int count = 0;

        for (int i = l; i <= r; i++) {
            int xor = 0, temp = i;

            // Calculate XOR of digits
            while (temp > 0) {
                xor = xor ^ (temp % 10);
                temp /= 10;
            }

            // If XOR <= 9,
            // then increment count
            if (xor <= 9)
                count++;
        }

        // Print the count
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Number
        int N = 2;

        // Function Call
        countNums(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find count of N-digit
# numbers with single digit XOR
def countNums(N):

    # Range of numbers
    l = pow(10, N - 1)
    r = pow(10, N) - 1

    count = 0
    for i in range(l, r + 1):
        xorr = 0
        temp = i

        # Calculate XOR of digits
        while (temp > 0):
            xorr = xorr ^ (temp % 10)
            temp //= 10

        # If XOR <= 9,
        # then increment count
        if (xorr <= 9):
            count += 1

    # Print the count
    print(count)

# Driver Code

# Given number
N = 2

# Function call
countNums(N)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find count of N-digit
// numbers with single digit XOR
public static void countNums(int N)
{

    // Range of numbers
    int l = (int)Math.Pow(10, N - 1),
        r = (int)Math.Pow(10, N) - 1;

    int count = 0;

    for(int i = l; i <= r; i++)
    {
        int xor = 0, temp = i;

        // Calculate XOR of digits
        while (temp > 0)
        {
            xor = xor ^ (temp % 10);
            temp /= 10;
        }

        // If XOR <= 9,
        // then increment count
        if (xor <= 9)
            count++;
    }

    // Print the count
    Console.WriteLine(count);
}

// Driver Code
public static void Main()
{

    // Given number
    int N = 2;

    // Function call
    countNums(N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find count of N-digit
// numbers with single digit XOR
function countNums(N)
{

    // Range of numbers
    let l = Math.floor(Math.pow(10, N - 1));
    let r = Math.floor(Math.pow(10, N)) - 1;

    let count = 0;
    for(let i = l; i <= r; i++)
    {
        let xorr = 0, temp = i;

        // Calculate XOR of digits
        while (temp > 0)
        {
            xorr = xorr ^ (temp % 10);
            temp = Math.floor(temp / 10);
        }

        // If XOR <= 9,
        // then increment count
        if (xorr <= 9)
            count++;
    }

    // Print the count
    document.write(count);
}

// Driver Code

    // Given number
    let N = 2;

    // Function call
    countNums(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
66
```

***时间复杂度:**O(N * 10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。观察可以得到的最大**位异或**为 15。

1.  创建一个**表 dp[][]** ，其中 **dp[i][j]** 存储 I 位数的计数，这样它们的异或就是 **j** 。
2.  对于 i = 1，初始化 dp[][]，对于每个 **i** 从 0 到 9，对每个数字 **j** 进行 2 到 N 的迭代。
3.  对于从 0 到 15 的每一个可能的先前异或 **k** ，通过对先前异或 **k** 和数字 **j** 进行异或运算，找到**值**，并将**DP[I][值]** 的计数增加**DP[I–1][k]**。
4.  通过对**DP【N】【j】**求和，可以得到用一位数异或的 N 位数总数，其中 j 的范围从 **0 到 9** 。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find
// count of N-digit
// numbers with single
// digit XOR
void countNums(int N)
{ 
  // dp[i][j] stores the number
  // of i-digit numbers with
  // XOR equal to j
  int dp[N][16];
  memset(dp, 0,
         sizeof(dp[0][0]) *
                N * 16);

  // For 1-9 store the value
  for (int i = 1; i <= 9; i++)
    dp[0][i] = 1;

  // Iterate till N
  for (int i = 1; i < N; i++)
  {
    for (int j = 0; j < 10; j++)
    {
      for (int k = 0; k < 16; k++)
      {
        // Calculate XOR
        int xo = j ^ k;

        // Store in DP table
        dp[i][xo] += dp[i - 1][k];
      }
    }
  }

  // Initialize count
  int count = 0;
  for (int i = 0; i < 10; i++)
    count += dp[N - 1][i];

  // Print the answer
  cout << (count) << endl;
}

// Driver Code
int main()
{
  // Given number N
  int N = 1;

  // Function Call
  countNums(N);
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find count of N-digit
    // numbers with single digit XOR
    public static void countNums(int N)
    {

        // dp[i][j] stores the number
        // of i-digit numbers with
        // XOR equal to j
        int dp[][] = new int[N][16];

        // For 1-9 store the value
        for (int i = 1; i <= 9; i++)
            dp[0][i] = 1;

        // Iterate till N
        for (int i = 1; i < N; i++) {

            for (int j = 0; j < 10; j++) {

                for (int k = 0; k < 16; k++) {

                    // Calculate XOR
                    int xor = j ^ k;

                    // Store in DP table
                    dp[i][xor] += dp[i - 1][k];
                }
            }
        }

        // Initialize count
        int count = 0;
        for (int i = 0; i < 10; i++)
            count += dp[N - 1][i];

        // Print the answer
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given number N
        int N = 1;

        // Function Call
        countNums(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find count of
# N-digit numbers with single
# digit XOR
def countNums(N):

    # dp[i][j] stores the number
    # of i-digit numbers with
    # XOR equal to j
    dp = [[0 for i in range(16)]
             for j in range(N)];

    # For 1-9 store the value
    for i in range(1, 10):
        dp[0][i] = 1;

    # Iterate till N
    for i in range(1, N):
        for j in range(0, 10):
            for k in range(0, 16):
                # Calculate XOR
                xor = j ^ k;

                # Store in DP table
                dp[i][xor] += dp[i - 1][k];

    # Initialize count
    count = 0;
    for i in range(0, 10):
        count += dp[N - 1][i];

    # Print answer
    print(count);

# Driver Code
if __name__ == '__main__':

    # Given number N
    N = 1;

    # Function Call
    countNums(N);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find count of N-digit
// numbers with single digit XOR
public static void countNums(int N)
{

    // dp[i][j] stores the number
    // of i-digit numbers with
    // XOR equal to j
    int [,]dp = new int[N, 16];

    // For 1-9 store the value
    for(int i = 1; i <= 9; i++)
        dp[0, i] = 1;

    // Iterate till N
    for(int i = 1; i < N; i++)
    {
        for(int j = 0; j < 10; j++)
        {
            for (int k = 0; k < 16; k++)
            {

                // Calculate XOR
                int xor = j ^ k;

                // Store in DP table
                dp[i, xor] += dp[i - 1, k];
            }
        }
    }

    // Initialize count
    int count = 0;
    for(int i = 0; i < 10; i++)
        count += dp[N - 1, i];

    // Print the answer
    Console.Write(count);
}

// Driver Code
public static void Main(string[] args)
{

    // Given number N
    int N = 1;

    // Function call
    countNums(N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Function to find count of N-digit
    // numbers with single digit XOR
    function countNums(N) {

        // dp[i][j] stores the number
        // of i-digit numbers with
        // XOR equal to j
        var dp = Array(N);
        for(var i =0;i<N;i++)
        dp[i] = Array(16).fill(0);

        // For 1-9 store the value
        for (i = 1; i <= 9; i++)
            dp[0][i] = 1;

        // Iterate till N
        for (i = 1; i < N; i++) {

            for (j = 0; j < 10; j++) {

                for (k = 0; k < 16; k++) {

                    // Calculate XOR
                    var xor = j ^ k;

                    // Store in DP table
                    dp[i][xor] += dp[i - 1][k];
                }
            }
        }

        // Initialize count
        var count = 0;
        for (i = 0; i < 10; i++)
            count += dp[N - 1][i];

        // Print the answer
        document.write(count);
    }

    // Driver Code

        // Given number N
        var N = 1;

        // Function Call
        countNums(N);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
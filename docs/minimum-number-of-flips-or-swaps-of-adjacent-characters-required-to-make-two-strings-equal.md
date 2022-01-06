# 使两个字符串相等所需的相邻字符的最小翻转或互换次数

> 原文:[https://www . geeksforgeeks . org/最小翻转次数或相邻字符互换次数-要求两个字符串相等/](https://www.geeksforgeeks.org/minimum-number-of-flips-or-swaps-of-adjacent-characters-required-to-make-two-strings-equal/)

给定长度为 **N** 的两个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) [](https://www.geeksforgeeks.org/python-strings/)**A** 和 **B** ，任务是通过[交换相邻字符](https://www.geeksforgeeks.org/c-program-to-swap-adjacent-characters-of-a-string/)或翻转字符串 **A** 的任意字符来计算使两个给定字符串相等所需的最小操作数。

**示例:**

> **输入:** A = "100 "，B = "001"
> **输出:** 2
> **解释:**翻转字符 A[0](= '1 ')和 A[2](= '0 ')将字符串 A 修改为“001”，等于字符串 B
> 
> **输入:**A =“0101”，B =“0011”
> **输出:** 1
> **解释:**交换字符 A[2](= '0 ')和 A[3](= '1 ')将字符串 A 修改为“0011”，等于字符串 B

**方法:**问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决，因为它有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。
按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，称大小为 **N+1** 的 **dp[]** 为 **{0}** ，其中 **dp[i]** 存储**索引 **i 所需的最小**操作数，**使 **A <sub>i</sub>** 的前缀等于前缀 **B <sub>i</sub>** 。
*   [使用变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，比如 **i** ，并执行以下操作:
    *   如果**A[I–1]**等于**B[I–1]，**则更新 **dp[i]** 为**DP[I–1]**。
    *   否则，将 **dp[i]** 更新为**DP[I–1]+1**。
    *   如果交换是可能的，即 **i > 1** 和**A【I–2】**等于**B【I–1】**和**A【I–1】**等于**B【I–2】，**则更新**DP【I】**到 **min(dp[i]，DP[I–2]+1)。**
*   完成上述步骤后，打印得到的最小操作次数，即数值 **dp[N]。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of operations required
// to make strings A and B equal
int countMinSteps(string A, string B, int N)
{

    // Stores all dp-states
    vector<int> dp(N + 1, 0);

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // If A[i - 1] equals to B[i - 1]
        if (A[i - 1] == B[i - 1]) {

            // Assign Dp[i - 1] to Dp[i]
            dp[i] = dp[i - 1];
        }

        // Otherwise
        else {

            // Update dp[i]
            dp[i] = dp[i - 1] + 1;
        }

        // If swapping is possible
        if (i >= 2 && A[i - 2] == B[i - 1]
            && A[i - 1] == B[i - 2]) {

            // Update dp[i]
            dp[i] = min(dp[i], dp[i - 2] + 1);
        }
    }

    // Return the minimum
    // number of steps required
    return dp[N];
}

// Driver Code
int main()
{
    // Given Input
    string A = "0101";
    string B = "0011";
    int N = A.length();

    // Function Call
    cout << countMinSteps(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the minimum
// number of operations required
// to make strings A and B equal
static int countMinSteps(String A, String B, int N)
{

    // Stores all dp-states
    int[] dp = new int[N + 1];
    for(int i = 1; i <= N; i++)
    {

        // Update the value of A[i]
        dp[i] = 0;
    }

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // If A[i - 1] equals to B[i - 1]
        if (A.charAt(i - 1) == B.charAt(i - 1))
        {

            // Assign Dp[i - 1] to Dp[i]
            dp[i] = dp[i - 1];
        }

        // Otherwise
        else
        {

            // Update dp[i]
            dp[i] = dp[i - 1] + 1;
        }

        // If swapping is possible
        if (i >= 2 && A.charAt(i - 2) == B.charAt(i - 1) &&
                      A.charAt(i - 1) == B.charAt(i - 2))
        {

            // Update dp[i]
            dp[i] = Math.min(dp[i], dp[i - 2] + 1);
        }
    }

    // Return the minimum
    // number of steps required
    return dp[N];
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    String A = "0101";
    String B = "0011";
    int N = A.length();

    // Function Call
    System.out.println(countMinSteps(A, B, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum
# number of operations required
# to make strings A and B equal
def countMinSteps(A, B, N) :

    # Stores all dp-states
    dp = [0] * (N + 1)

    # Iterate rate over the range [1, N]
    for i in range(1, N+1) :

        # If A[i - 1] equals to B[i - 1]
        if (A[i - 1] == B[i - 1]) :

            # Assign Dp[i - 1] to Dp[i]
            dp[i] = dp[i - 1]

        # Otherwise
        else :

            # Update dp[i]
            dp[i] = dp[i - 1] + 1

        # If swapping is possible
        if (i >= 2 and A[i - 2] == B[i - 1]
            and A[i - 1] == B[i - 2]) :

            # Update dp[i]
            dp[i] = min(dp[i], dp[i - 2] + 1)

    # Return the minimum
    # number of steps required
    return dp[N]

# Driver Code

# Given Input
A = "0101"
B = "0011"
N = len(A)

# Function Call
print(countMinSteps(A, B, N))

# This code is contributed by splevel62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the minimum
// number of operations required
// to make strings A and B equal
static int countMinSteps(string A, string B, int N)
{

    // Stores all dp-states
    int[] dp = new int[N + 1];
    for(int i = 1; i <= N; i++)
    {

        // Update the value of A[i]
        dp[i] = 0;
    }

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // If A[i - 1] equals to B[i - 1]
        if (A[i - 1] == B[i - 1])
        {

            // Assign Dp[i - 1] to Dp[i]
            dp[i] = dp[i - 1];
        }

        // Otherwise
        else
        {

            // Update dp[i]
            dp[i] = dp[i - 1] + 1;
        }

        // If swapping is possible
        if (i >= 2 && A[i - 2] == B[i - 1] &&
                      A[i - 1] == B[i - 2])
        {

            // Update dp[i]
            dp[i] = Math.Min(dp[i], dp[i - 2] + 1);
        }
    }

    // Return the minimum
    // number of steps required
    return dp[N];
}

// Driver code
public static void Main(String []args)
{

    // Given Input
    string A = "0101";
    string B = "0011";
    int N = A.Length;

    // Function Call
    Console.Write(countMinSteps(A, B, N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach

       // Function to count the minimum
       // number of operations required
       // to make strings A and B equal
       function countMinSteps(A, B, N) {

           // Stores all dp-states
           let dp = new Array(N + 1).fill(0);

           // Iterate over the range [1, N]
           for (let i = 1; i <= N; i++) {

               // If A[i - 1] equals to B[i - 1]
               if (A[i - 1] == B[i - 1]) {

                   // Assign Dp[i - 1] to Dp[i]
                   dp[i] = dp[i - 1];
               }

               // Otherwise
               else {

                   // Update dp[i]
                   dp[i] = dp[i - 1] + 1;
               }

               // If swapping is possible
               if (i >= 2 && A[i - 2] == B[i - 1]
                   && A[i - 1] == B[i - 2]) {

                   // Update dp[i]
                   dp[i] = Math.min(dp[i], dp[i - 2] + 1);
               }
           }

           // Return the minimum
           // number of steps required
           return dp[N];
       }

       // Driver Code

       // Given Input
       let A = "0101";
       let B = "0011";
       let N = A.length;

       // Function Call
       document.write(countMinSteps(A, B, N));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
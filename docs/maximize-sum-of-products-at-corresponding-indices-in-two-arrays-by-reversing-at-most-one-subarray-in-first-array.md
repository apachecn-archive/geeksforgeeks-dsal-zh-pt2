# 通过反转第一个阵列中最多一个子阵列，最大化两个阵列中相应索引处的乘积之和

> 原文:[https://www . geesforgeks . org/通过最多反转一个阵列中的一个子阵列来最大化两个阵列中相应指数的乘积之和/](https://www.geeksforgeeks.org/maximize-sum-of-products-at-corresponding-indices-in-two-arrays-by-reversing-at-most-one-subarray-in-first-array/)

给定两个大小为 **N** 的阵列 **A** 和 **B** ，任务是通过最多反转阵列 **A** 的一个子阵列，最大化从 **0** 到 **N-1** 的所有 **A[i]*B[i]** 值的总和。

**示例:**

> **输入:** N = 4，A = [5，1，2，3]，B = [1，4，3，2]
> **输出:** 33
> **说明:**阵 A 换向后子阵 A[0，1]将变为[1，5，2，3]。反转后的 A[i]*B[i]之和变为 1*1+5*4+2*3+3*2 = 33。
> 
> **输入:** N = 3，A = [6，7，3]，B = [5，1，7]
> T3】输出: 82

**天真方法:**解决这个问题的一个简单方法是检查 A 的所有可能的子阵列，并逐一反转，以找到总和的最大可能值。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of A[i]*B[i]
// across all values of i from 0 to N-1 by reversing
// at most one subarray of array A
int maxSum(vector<int>& A, vector<int>& B)
{
    int N = A.size();

    // Initialising maximum possible sum variable
    int maxPosSum = 0;

    // Iterating for all subarrays
    for (int L = 0; L < N - 1; L++) {
        for (int R = L; R < N; R++) {

            // Variable for storing the sum after reversing
            // The subarray from L to R
            int curSum = 0;
            for (int i = 0; i < N; i++) {

                // Checking if the current index is in the
                // reversed subarray
                if (i >= L && i <= R)
                    curSum += A[L + R - i] * B[i];
                else
                    curSum += A[i] * B[i];
            }

            // Updating the answer
            maxPosSum = max(maxPosSum, curSum);
        }
    }

    // Returning the Maximum Possible Sum of product
    return maxPosSum;
}

// Driver Code
int main()
{
    // Given Input
    int N = 4;
    vector<int> A = { 5, 1, 2, 3 }, B = { 1, 4, 3, 2 };

    cout << maxSum(A, B);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
public class GFG {

  // Function to find the maximum sum of A[i]*B[i]
  // across all values of i from 0 to N-1 by reversing
  // at most one subarray of array A
  static int maxSum(int []A, int []B)
  {
    int N = A.length;

    // Initialising maximum possible sum variable
    int maxPosSum = 0;

    // Iterating for all subarrays
    for (int L = 0; L < N - 1; L++) {
      for (int R = L; R < N; R++) {

        // Variable for storing the sum after reversing
        // The subarray from L to R
        int curSum = 0;
        for (int i = 0; i < N; i++) {

          // Checking if the current index is in the
          // reversed subarray
          if (i >= L && i <= R)
            curSum += A[L + R - i] * B[i];
          else
            curSum += A[i] * B[i];
        }

        // Updating the answer
        maxPosSum = Math.max(maxPosSum, curSum);
      }
    }

    // Returning the Maximum Possible Sum of product
    return maxPosSum;
  }

  // Driver code
  public static void main(String args[])
  {

    // Given Input
    int N = 4;
    int []A = { 5, 1, 2, 3 };
    int []B = { 1, 4, 3, 2 };
    System.out.println(maxSum(A, B));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the maximum sum of A[i]*B[i]
# across all values of i from 0 to N-1 by reversing
# at most one subarray of array A
def maxSum(A, B):
    N = len(A)

    # Initialising maximum possible sum variable
    maxPosSum = 0

    # Iterating for all subarrays
    for L in range(N - 1):
        for R in range(L, N):

            # Variable for storing the sum after reversing
            # The subarray from L to R
            curSum = 0
            for i in range(N):
                # Checking if the current index is in the
                # reversed subarray
                if (i >= L and i <= R):
                    curSum += A[L + R - i] * B[i]
                else:
                    curSum += A[i] * B[i]

            # Updating the answer
            maxPosSum = max(maxPosSum, curSum)

    # Returning the Maximum Possible Sum of product
    return maxPosSum

# Driver Code

# Given Input
N = 4
A = [5, 1, 2, 3]
B = [1, 4, 3, 2]
print(maxSum(A, B))

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach

   // Function to find the maximum sum of A[i]*B[i]
   // across all values of i from 0 to N-1 by reversing
   // at most one subarray of array A
   function maxSum(A, B)
   {
     let N = A.length;

     // Initialising maximum possible sum variable
     let maxPosSum = 0;

     // Iterating for all subarrays
     for (let L = 0; L < N - 1; L++) {
       for (let R = L; R < N; R++) {

         // Variable for storing the sum after reversing
         // The subarray from L to R
         let curSum = 0;
         for (let i = 0; i < N; i++) {

           // Checking if the current index is in the
           // reversed subarray
           if (i >= L && i <= R)
             curSum += A[L + R - i] * B[i];
           else
             curSum += A[i] * B[i];
         }

         // Updating the answer
         maxPosSum = Math.max(maxPosSum, curSum);
       }
     }

     // Returning the Maximum Possible Sum of product
     return maxPosSum;
   }

   // Driver Code

   // Given Input
   let N = 4;
   let A = [5, 1, 2, 3], B = [1, 4, 3, 2];

   document.write(maxSum(A, B));

 // This code is contributed by Potta Lokesh
 </script>
```

## C#

```
// C# code to implement above approach
using System;
public class GFG {

  // Function to find the maximum sum of A[i]*B[i]
  // across all values of i from 0 to N-1 by reversing
  // at most one subarray of array A
  static int maxSum(int []A, int []B)
  {
    int N = A.Length;

    // Initialising maximum possible sum variable
    int maxPosSum = 0;

    // Iterating for all subarrays
    for (int L = 0; L < N - 1; L++) {
      for (int R = L; R < N; R++) {

        // Variable for storing the sum after reversing
        // The subarray from L to R
        int curSum = 0;
        for (int i = 0; i < N; i++) {

          // Checking if the current index is in the
          // reversed subarray
          if (i >= L && i <= R)
            curSum += A[L + R - i] * B[i];
          else
            curSum += A[i] * B[i];
        }

        // Updating the answer
        maxPosSum = Math.Max(maxPosSum, curSum);
      }
    }

    // Returning the Maximum Possible Sum of product
    return maxPosSum;
  }

  // Driver code
  public static void Main()
  {

    // Given Input
    int []A = { 5, 1, 2, 3 };
    int []B = { 1, 4, 3, 2 };
    Console.Write(maxSum(A, B));

  }
}

// This code is contributed by Saurabh Jaiswal
```

**Output**

```
33
```

**时间复杂度:**O(N<sup>3</sup>)
T5】辅助空间: O(1)

**有效途径:**上述问题可以通过使用动态规划来解决。请按照以下步骤解决此问题:

*   设 dp[L][[R]代表子阵 A[L，R]反转后 A[i]与 B[i]乘积之和。
*   观察如果子阵 A[L，R]反转，子阵 A[L+1，R-1]也反转。因此，dp[L][R]可以通过使用 dp[L+1][R-1]并通过使用以下公式来计算:

> **DP[l][r]= DP[l+1][r-1]+(a[r]* b[l])----(a[l]* b[l])+(a[l]* b[r)](a[r]* b[r]t1]**

*   因为在**DP【L+1】【R-1】**的计算中，增加了**A【L】* B【L】**和**A【R】* B【R】**，而在**DP【L】【R】**的计算中，增加了**A【R】* B【L】**和**A【L】* B【R】**。
*   因此，我们需要减去 **A[L]*B[L]** 和 **A[R]*B[R]** ，并添加 **A[R]*B[L]** 和 **A[L]*B[R]** 到 **dp[L+1][R-1]** 来计算 **dp[L][R]** 。
*   根据以上观察打印答案。

下面是动态编程方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of A[i]*B[i]
// across all values of i from 0 to N-1 by reversing
// at most one subarray of array A
int maxSum(vector<int>& A, vector<int>& B)
{

    int N = A.size();

    // Initialising maximum possible sum variable
    int maxPosSum = 0;
    int dp[N][N];

    // Initialising the dp array
    memset(dp, 0, sizeof(dp));

    // Value of maxPosSum when no subarray is reversed
    for (int i = 0; i < N; i++)
        maxPosSum += A[i] * B[i];

    // Initialising dp for subarray of length 1
    for (int i = 0; i < N; i++)
        dp[i][i] = maxPosSum;

    // Initialising dp for subarray of length 2
    for (int i = 0; i < N - 1; i++) {
        int R = i + 1;
        int L = i;
        dp[L][R] = maxPosSum + (A[R] * B[L]) - (A[L] * B[L])
                   + (A[L] * B[R]) - (A[R] * B[R]);
    }

    // Calculating the complete dp array
    for (int R = 0; R < N; R++) {
        for (int L = 0; L < N; L++) {

            // If length of subarray is less 3, then
            // continuing
            if (R - L + 1 < 3)
                continue;
            dp[L][R] = dp[L + 1][R - 1] + (A[R] * B[L])
                       - (A[L] * B[L]) + (A[L] * B[R])
                       - (A[R] * B[R]);
        }
    }

    // Updating the maxPosSum variable
    for (int L = 0; L < N; L++) {
        for (int R = L; R < N; R++) {
            maxPosSum = max(maxPosSum, dp[L][R]);
        }
    }

    // Returning the maximum possible sum of product
    return maxPosSum;
}

// Driver Code
int main()
{
    // Given Input
    vector<int> A = { 5, 1, 2, 3 }, B = { 1, 4, 3, 2 };

    cout << maxSum(A, B);
    return 0;
}
```

**Output**

```
33
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N <sup>2</sup>
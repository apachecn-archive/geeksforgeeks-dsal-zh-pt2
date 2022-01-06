# 计数在数组元素前放置“+”和“-”的方式，得到总和 K

> 原文:[https://www . geesforgeks . org/count-way-to-place-and-in-front-array-elements-to-get-sum-k/](https://www.geeksforgeeks.org/count-ways-to-place-and-in-front-of-array-elements-to-obtain-sum-k/)

给定一个由 **N** 个非负整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是找出将**+**和**-**个运算符放在数组**A【】**个元素前面的方法数，这样数组的和就变成了 **K** 。

**示例:**

> **输入:** A[] = {1，1，2，3}，N = 4，K = 1
> T3】输出:3
> T6】说明:三种可能的方式是:
> 
> 1.  + 1 + 1 + 2 – 3 = 1
> 2.  + 1 – 1 – 2 + 3 = 1
> 3.  – 1 + 1 – 1 + 3 = 1
> 
> **输入:** A[] = {1，1，1，1，1}，N = 5，K = 3
> T3】输出: 5

**方法:**根据以下观察结果可以解决问题:

1.  将前面有**'+**、前面有**'-**的元素之和存储在变量中，比如说 **P1** 和 **P2** ，这样数组之和就变成了 **K** 。
2.  将数组 **A[]** 的总和存储在一个变量中，比如 **K** 。
3.  因此，出现以下等式:
    1.  **P1 + P2 =总和**
    2.  **P1-P2 = K**T2】
4.  求解上述方程得到 **P1 =(和+ K) / 2** 。
5.  因此，问题转化为[用和 P1](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/) 求子集的个数。
6.  如果 **A** 的一个元素等于 **0** ，则**“+”**和**“-”**操作符都在有效的安排下工作，因此 **0s** 可以安全地忽略并单独计算。

因此，这个问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决。按照以下步骤解决问题:

1.  分别计算并存储数组 **A[]** 的元素之和以及变量 **sum** 和 **c** 中 **A[]** 的 **0s** 的个数。
2.  如果 **K** 大于**和**或**(和+ K)** 为奇数，则返回 **0** 。
3.  将 **K** 加到**和**上，除以 **2，**即**和=(和+ K) / 2** ，即为所需和。[求等于该和的子集数](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/)。
4.  创建一个 2D **dp** 维度数组 **N*sum** 。其中 **dp[i][j]** 代表直到 **i-1** 的子集数量，这些子集具有总和 **j** 。
5.  需要考虑的基本情况如下:
    1.  **dp[0][i] = 0** ，对于 **0 < = i < =总和**，因为没有考虑数组**A【】**中的元素
    2.  **dp[i][0] = 1** ，对于 **0 < = i < = N** ，因为获得总和 **0** 总是可能的。
6.  从 **1** 迭代到 **N** ，对于每个当前索引 **i** ，执行以下操作:
    1.  从 **1** 迭代到**和**，对于每个当前索引 **j** ，执行以下转换:
        1.  如果**A[I–1]**小于 **j** 且**A[I–1]**不等于 **0** ，则设置**DP[I][j]= DP[I–1][j]+DP[I–1][j–A[I–1]]。**
        2.  否则，复制之前的状态，即**DP[I][j]= DP[I–1][j]。**
7.  最后，返回 **dp[N][sum]** 和**2<sup>c</sup>T5 的乘积(占 0)即**DP[N][sum]* 2<sup>c</sup>T9】。****

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of ways
// '+' and '-' operators can be placed
// in front of array elements to make
// the sum of array elements equal to K
int solve(int A[], int N, int K)
{
    // Stores sum of the array
    int sum = 0;

    // Stores count of 0s in A[]
    int c = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update sum
        sum += A[i];

        // Update count of 0s
        if (A[i] == 0)
            c++;
    }
    // Conditions where no arrangements
    // are possible which adds up to K
    if (K > sum || (sum + K) % 2)
        return 0;

    // Required sum
    sum = (sum + K) / 2;

    // Dp array
    int dp[N + 1][sum + 1];
    // Base cases
    for (int i = 0; i <= sum; i++)
        dp[0][i] = 0;

    for (int i = 0; i <= N; i++)
        dp[i][0] = 1;

    // Fill the dp array
    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= sum; j++) {

            if (A[i - 1] <= j && A[i - 1])
                dp[i][j] = dp[i - 1][j]
                           + dp[i - 1][j - A[i - 1]];
            else
                dp[i][j] = dp[i - 1][j];
        }
    }

    // Return answer
    return dp[N][sum] + pow(2, c);
}

// Driver Code
int main()
{
    // Input
    int A[] = { 1, 1, 2, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    int K = 3;

    // Function call
    cout << solve(A, N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count number of ways
// '+' and '-' operators can be placed
// in front of array elements to make
// the sum of array elements equal to K
static int solve(int A[], int N, int K)
{

    // Stores sum of the array
    int sum = 0;

    // Stores count of 0s in A[]
    int c = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update sum
        sum += A[i];

        // Update count of 0s
        if (A[i] == 0)
            c++;
    }
    // Conditions where no arrangements
    // are possible which adds up to K
    if ((K > sum) || (((sum + K) % 2) != 0))
        return 0;

    // Required sum
    sum = (sum + K) / 2;

    // Dp array
    int dp[][] = new int[N + 1][sum + 1];
    // Base cases
    for (int i = 0; i <= sum; i++)
        dp[0][i] = 0;

    for (int i = 0; i <= N; i++)
        dp[i][0] = 1;

    // Fill the dp array
    for (int i = 1; i <= N; i++) {
        for (int j = 1; j <= sum; j++) {

            if ((A[i - 1] <= j)  && (A[i - 1] != 0))
                dp[i][j] = dp[i - 1][j]
                           + dp[i - 1][j - A[i - 1]];
            else
                dp[i][j] = dp[i - 1][j];
        }
    }

    // Return answer
    return dp[N][sum] + (int)Math.pow(2, c);
}

// Driver Code
public static void main(String[] args)
{
    // Input
    int A[] = { 1, 1, 2, 3 };
    int N = A.length;
    int K = 3;

    // Function call
    System.out.print(solve(A, N, K));

}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count number of ways
# '+' and '-' operators can be placed
# in front of array elements to make
# the sum of array elements equal to K
def solve(A, N, K):

    # Stores sum of the array
    sum = 0

    # Stores count of 0s in A[]
    c = 0

    # Traverse the array
    for i in range(N):

        # Update sum
        sum += A[i]

        # Update count of 0s
        if (A[i] == 0):
            c += 1

    # Conditions where no arrangements
    # are possible which adds up to K
    if (K > sum or (sum + K) % 2):
        return 0

    # Required sum
    sum = (sum + K) // 2

    # Dp array
    dp = [[0 for i in range(sum + 1)]
             for j in range(N + 1)]

    # Base cases
    for i in range(sum + 1):
        dp[0][i] = 0

    for i in range(N + 1):
        dp[i][0] = 1

    # Fill the dp array
    for i in range(1, N + 1, 1):
        for j in range(1, sum + 1, 1):
            if (A[i - 1] <= j and A[i - 1]):
                dp[i][j] = (dp[i - 1][j] +
                            dp[i - 1][j - A[i - 1]])
            else:
                dp[i][j] = dp[i - 1][j]

    # Return answer
    return dp[N][sum] + pow(2, c)

# Driver Code
if __name__ == '__main__':

    # Input
    A = [ 1, 1, 2, 3 ]
    N = len(A)
    K = 3

    # Function call
    print(solve(A, N, K))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to count number of ways
  // '+' and '-' operators can be placed
  // in front of array elements to make
  // the sum of array elements equal to K
  static int solve(int[] A, int N, int K)
  {

    // Stores sum of the array
    int sum = 0;

    // Stores count of 0s in A[]
    int c = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Update sum
      sum += A[i];

      // Update count of 0s
      if (A[i] == 0)
        c++;
    }
    // Conditions where no arrangements
    // are possible which adds up to K
    if ((K > sum) || (((sum + K) % 2) != 0))
      return 0;

    // Required sum
    sum = (sum + K) / 2;

    // Dp array
    int[, ] dp= new int[N + 1, sum + 1];

    // Base cases
    for (int i = 0; i <= sum; i++)
      dp[0, i] = 0;

    for (int i = 0; i <= N; i++)
      dp[i,0] = 1;

    // Fill the dp array
    for (int i = 1; i <= N; i++) {
      for (int j = 1; j <= sum; j++) {

        if ((A[i - 1] <= j)  && (A[i - 1] != 0))
          dp[i,j] = dp[i - 1,j]
          + dp[i - 1,j - A[i - 1]];
        else
          dp[i,j] = dp[i - 1,j];
      }
    }

    // Return answer
    return dp[N, sum] + (int)Math.Pow(2, c);
  }

  // Driver code
  static public void Main ()
  {

    // Input
    int[] A = { 1, 1, 2, 3 };
    int N = A.Length;
    int K = 3;

    // Function call
    Console.Write(solve(A, N, K));
  }
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

        // Function to count number of ways
        // '+' and '-' operators can be placed
        // in front of array elements to make
        // the sum of array elements equal to K
        function solve(A, N, K)
        {
            // Stores sum of the array
            let sum = 0;

            // Stores count of 0s in A[]
            let c = 0;

            // Traverse the array
            for (let i = 0; i < N; i++) {

                // Update sum
                sum += A[i];

                // Update count of 0s
                if (A[i] == 0)
                    c++;
            }
            // Conditions where no arrangements
            // are possible which adds up to K
            if (K > sum || (sum + K) % 2)
                return 0;

            // Required sum
            sum = (sum + K) / 2;

            // Dp array
            let dp = new Array(N + 1);
            for (var i = 0; i < dp.length; i++) {
                dp[i] = new Array(sum + 1);
            }
            // Base cases
            for (let i = 0; i <= sum; i++)
                dp[0][i] = 0;

            for (let i = 0; i <= N; i++)
                dp[i][0] = 1;

            // Fill the dp array
            for (let i = 1; i <= N; i++) {
                for (let j = 1; j <= sum; j++) {

                    if (A[i - 1] <= j && A[i - 1])
                        dp[i][j] = dp[i - 1][j]
                            + dp[i - 1][j - A[i - 1]];
                    else
                        dp[i][j] = dp[i - 1][j];
                }
            }

            // Return answer
            return dp[N][sum] + Math.pow(2, c);
        }

        // Driver Code

        // Input
        let A = [1, 1, 2, 3];
        let N = A.length;
        let K = 3;

        // Function call
        document.write(solve(A, N, K));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N *和)*
***辅助空间:** O(N *和)*
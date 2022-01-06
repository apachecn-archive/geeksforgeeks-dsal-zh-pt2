# 最小化给定二进制串中设置位与未设置位交换的成本

> 原文:[https://www . geesforgeks . org/最小化给定二进制字符串中未设置位的交换集位成本/](https://www.geeksforgeeks.org/minimize-cost-of-swapping-set-bits-with-unset-bits-in-a-given-binary-string/)

给定大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过用未设置的位交换每个设置的位来找到最小成本，使得在索引 **i** 和 **j** 处交换位对的成本为**ABS(j–I)**。

**注意:**一个被交换的位不能被交换两次，给定二进制字符串中设置位的[计数最多为 **N/2** 。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)

**示例:**

> **输入:** S = "1010001"
> **输出:** 3
> **解释:**
> 在需要交换字符后:
> 
> 1.  索引(0，1)处的交换字符将字符串修改为“0110001”，此操作的开销为| 1–0 | = 1。
> 2.  索引(2，3)处的交换字符将字符串修改为“0101001”，此操作的开销为| 2–1 | = 1。
> 3.  索引(6，7)处的交换字符将字符串修改为“0101010”，此操作的开销为| 7–6 | = 1。
> 
> 在上述操作之后，所有设置的位被未设置的位替换，并且操作的总成本是 1 + 1 + 1 = 3。
> 
> **输入:**S = " 1100 "
> T3】输出: 4

**方法:**给定的问题可以通过使用 [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/) 来解决，方法是将设置和未设置的位的索引存储在两个辅助[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，比如说 **A[]** 和 **B[]** ，然后找到数组元素 **A[]** 与数组的任意元素**B[**之间的差的和。按照以下步骤解决给定的问题:

*   初始化两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如 **A[]** 和 **B[]** ，并在其中存储设置位和未设置位的索引。
*   初始化尺寸为**K *(N–K)**的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **dp[][]** ，其中 K 是 **S** 中设置位的[计数，使得 **dp[i][j]** 存储将**I<sup>th</sup>T15】数组元素**A[**与 **j <sup>th</sup> 交换的最小成本****](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
*   现在，每个州都有两个选择:
    1.  将 **i <sup>第</sup>T3】阵元 **A[]** 交换至**(j–1)<sup>第</sup>** 阵元 **B[]** 为**DP[I][j]= DP[I][j–1]**。**
    2.  将**(I–1)<sup>第</sup>**阵元 **A[]** 交换到**(j–1)<sup>第</sup>** 阵元 **B[]** 和 **i <sup>第</sup>T15】阵元 **A[]** 与 **j <sup>第</sup>T21】阵元**B[**交换，此状态可以****
*   现在，选择上面两个选项中的最小值来查找当前状态，如下所示:

> dp[i][j] = min(dp[i][j-1]、DP[I-1][j-1]+ABS(a[I]-b[j])

*   完成上述步骤后，打印**DP[K][N–K]**的值，作为最终的最小操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define INF 1000000000

// Function to find the minimum cost
// required to swap every set bit with
// an unset bit
int minimumCost(string s)
{
    int N = s.length();

    // Stores the indices of set and
    // unset bits of the string S
    vector<int> A, B;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Store the indices
        if (s[i] == '1') {
            A.push_back(i);
        }
        else {
            B.push_back(i);
        }
    }

    int n1 = A.size();
    int n2 = B.size();

    // Initialize a dp table of size
    // n1*n2
    int dp[n1 + 1][n2 + 1];

    // Initialize all states to 0
    memset(dp, 0, sizeof(dp));

    // Set unreachable states to INF
    for (int i = 1; i <= n1; i++) {
        dp[i][0] = INF;
    }

    // Fill the dp Table according to
    // the given recurrence relation
    for (int i = 1; i <= n1; i++) {
        for (int j = 1; j <= n2; j++) {

            // Update the value of
            // dp[i][j]
            dp[i][j] = min(
                dp[i][j - 1],
                dp[i - 1][j - 1]
                    + abs(A[i - 1] - B[j - 1]));
        }
    }

    // Return the minimum cost
    return dp[n1][n2];
}

// Driver Code
int main()
{
    string S = "1010001";
    cout << minimumCost(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
static final int INF = 1000000000;

// Function to find the minimum cost
// required to swap every set bit with
// an unset bit
static int minimumCost(String s)
{
    int N = s.length();

    // Stores the indices of set and
    // unset bits of the String S
    Vector<Integer> A = new Vector<Integer>();
    Vector<Integer> B = new Vector<Integer>();

    // Traverse the String S
    for (int i = 0; i < N; i++) {

        // Store the indices
        if (s.charAt(i) == '1') {
            A.add(i);
        }
        else {
            B.add(i);
        }
    }

    int n1 = A.size();
    int n2 = B.size();

    // Initialize a dp table of size
    // n1*n2
    int [][]dp = new int[n1 + 1][n2 + 1];

    // Set unreachable states to INF
    for (int i = 1; i <= n1; i++) {
        dp[i][0] = INF;
    }

    // Fill the dp Table according to
    // the given recurrence relation
    for (int i = 1; i <= n1; i++) {
        for (int j = 1; j <= n2; j++) {

            // Update the value of
            // dp[i][j]
            dp[i][j] = Math.min(
                dp[i][j - 1],
                dp[i - 1][j - 1]
                    + Math.abs(A.get(i - 1) - B.get(j - 1)));
        }
    }

    // Return the minimum cost
    return dp[n1][n2];
}

// Driver Code
public static void main(String[] args)
{
    String S = "1010001";
    System.out.print(minimumCost(S));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach
INF = 1000000000;

# Function to find the minimum cost
# required to swap every set bit with
# an unset bit
def minimumCost(s):
  N = len(s);

  # Stores the indices of set and
  # unset bits of the string S
  A = []
  B = []

  # Traverse the string S
  for i in range(0, N):

    # Store the indices
    if (s[i] == "1"):
      A.append(i);
    else:
      B.append(i);

  n1 = len(A)
  n2 = len(B)

  # Initialize a dp table of size
  # n1*n2
  dp = [[0 for i in range(n2 + 1)] for j in range(n1 + 1)]

  # Set unreachable states to INF
  for i in range(1, n1 + 1):
    dp[i][0] = INF

  # Fill the dp Table according to
  # the given recurrence relation
  for i in range(1, n1 + 1):
    for j in range(1, n2 + 1):

      # Update the value of
      # dp[i][j]
      dp[i][j] = min(
        dp[i][j - 1],
        dp[i - 1][j - 1] + abs(A[i - 1] - B[j - 1])
      );

  # Return the minimum cost
  return dp[n1][n2];

# Driver Code
S = "1010001";
print(minimumCost(S));

# This code is contributed by _saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

public class Program
{

// Function to find the minimum cost
// required to swap every set bit with
// an unset bit
static int minimumCost(string s)
{
    int INF = 1000000000;
    int N = s.Length;

    // Stores the indices of set and
    // unset bits of the string S
    List<int> A = new List<int>();
    List<int> B = new List<int>();

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // Store the indices
        if (s[i] == '1') {
            A.Add(i);
        }
        else {
            B.Add(i);
        }
    }

    int n1 = A.Count;
    int n2 = B.Count;

    // Initialize a dp table of size
    // n1*n2
    int [,]dp = new  int[n1 + 1,n2 + 1];

    // Set unreachable states to INF
    for (int i = 1; i <= n1; i++) {
        dp[i,0] = INF;
    }

    // Fill the dp Table according to
    // the given recurrence relation
    for (int i = 1; i <= n1; i++) {
        for (int j = 1; j <= n2; j++) {

            // Update the value of
            // dp[i][j]
            dp[i,j] = Math.Min(
                dp[i,j - 1],
                dp[i - 1,j - 1]
                    + Math.Abs(A[i - 1] - B[j - 1]));
        }
    }

    // Return the minimum cost
    return dp[n1,n2];
}

    public static void Main()
    {
        string S = "1010001";
        Console.Write(minimumCost(S));
    }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let INF = 1000000000;

// Function to find the minimum cost
// required to swap every set bit with
// an unset bit
function minimumCost(s) {
  let N = s.length;

  // Stores the indices of set and
  // unset bits of the string S
  let A = [],
    B = [];

  // Traverse the string S
  for (let i = 0; i < N; i++) {
    // Store the indices
    if (s[i] == "1") {
      A.push(i);
    } else {
      B.push(i);
    }
  }

  let n1 = A.length;
  let n2 = B.length;

  // Initialize a dp table of size
  // n1*n2
  let dp = new Array(n1 + 1).fill(0).map(() => new Array(n2 + 1).fill(0));

  // Set unreachable states to INF
  for (let i = 1; i <= n1; i++) {
    dp[i][0] = INF;
  }

  // Fill the dp Table according to
  // the given recurrence relation
  for (let i = 1; i <= n1; i++) {
    for (let j = 1; j <= n2; j++) {
      // Update the value of
      // dp[i][j]
      dp[i][j] = Math.min(
        dp[i][j - 1],
        dp[i - 1][j - 1] + Math.abs(A[i - 1] - B[j - 1])
      );
    }
  }

  // Return the minimum cost
  return dp[n1][n2];
}

// Driver Code

let S = "1010001";
document.write(minimumCost(S));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(K *(N–K))其中 K 是 **S** 中* [*设置位*](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/) *的计数。*
***辅助空间:**O(K *(N–K))*
# 选择第一个数组元素

后，通过对整个和求反，可以得到最大子集和

> 原文:[https://www . geeksforgeeks . org/最大子集-选择第一个数组元素后求全和的可能和/](https://www.geeksforgeeks.org/maximum-subset-sum-possible-by-negating-the-entire-sum-after-selecting-the-first-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**，任务是如果数组的第一个元素被包含，所有元素的和被取反，则找到最大可能子集和。也可以考虑空子集(总和为 0)。

**示例:**

> **输入:** N = 5，A[] = {1，10，4，-6，3}
> **输出:** 17
> **解释:**
> 关于排除 A[0]，最大和子集= {10，4，3}，Sum = (10+4+3) = 17
> 关于包含 A[0]，最大和子集= {1，-6}，Sum = (1 + (-6)) = -5，关于否定-(-5 A[] = {3，-5，1，-6}
> **输出:** 8
> **说明:**
> 关于排除 A[0]，最大和子集= {1}，和= 1
> 关于包含 A[0]，最大和子集= {3，-5，-6}，和= (3 + (-5) + (-6)) = -8，关于否定-(-8) = 8
> 以上两个和的最大值为 max(1，8)

**天真方法:**
解决问题最简单的方法是[从数组中生成所有可能的子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，通过将第一个元素作为每个子集的一部分，找到最大子集和 **maxSum** 和最小子集和 **minSum** 。最后打印 **maxSum** 和 **-(minSum)** 的最大值。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**
要优化上述方法，请考虑以下两种情况:

*   排除第一个元素，只需从给定数组中找到所有正整数的和(比如 **maxSum1)** 。
*   求除 A[0]之外的所有元素的反，从数组中找到所有正整数的和(比如 maxSum2)，然后求反，将 A[0]加到和中。
*   打印 **maxSum1** 和 **-maxSum2** 的最大值作为所需答案。

下面列出了每个案例的详细步骤:

**情况 1:** 排除第一个元素 A[0]

*   从 A[1]迭代到 A[N-1]。
*   保持一个变量 **maxSum1** ，以跟踪最初设置为 0 的最大和。
*   如果遇到正元素 **(A[i] > 0)** ，将其包含在子集内，maxSum1 为 **(maxSum1 + A[i])** 。
*   最后，返回 maxSum1。

**情况 2:** 包括第一个元素 A[0]

*   因为包含第一个元素时，整个和将被求反，所以求除 A[0]之外的最小和。
*   使用与情况 1 中相同的步骤可以获得最小和，但是取负值。
    *   否定从 A[1]到 A[N-1]的所有值。
    *   执行与案例 1 中相同的步骤。
*   一旦得到总和(比如 **maxSum2** ，求其反****加 A【0】。****
*   ****再次否定 maxSum2。****

****最终，**最大(maxSum1，maxsum2)** 将是所需答案。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function returns maximum subset sum
// from the given array=
int maxSubset(vector<int>& A, bool flag)
{
    int n = A.size();
    int sum = 0;

    // Case 2: Negate values
    // from A[1] to A[N-1]
    if (flag) {
        for (int i = 1; i < n; i++)
            A[i] = -A[i];
    }

    for (int i = 1; i < n; i++) {

        // Include only positives
        // for max subset sum
        if (A[i] > 0) {
            sum += A[i];
        }
    }

    // Return max sum obtained
    return sum;
}

// Function to return maximum of the
// maximum subset sum calculated
// for the two cases
int findBest(vector<int> A)
{
    // Case 1
    int x = maxSubset(A, 0);

    // Case 2
    int y = maxSubset(A, 1);

    // Modifying the sum
    y = -y;

    // Including first element
    y += A[0];

    // Negating again
    y = -y;

    // Return the required answer
    return max(x, y);
}

// Driver Code
int main()
{
    vector<int> A = { 1, 10, 4, -6, 3 };

    cout << findBest(A) << endl;
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function returns maximum subset sum
// from the given array=
static int maxSubset(int []A, boolean flag)
{
    int n = A.length;
    int sum = 0;

    // Case 2: Negate values
    // from A[1] to A[N-1]
    if (flag)
    {
        for (int i = 1; i < n; i++)
            A[i] = -A[i];
    }

    for (int i = 1; i < n; i++)
    {
        // Include only positives
        // for max subset sum
        if (A[i] > 0)
        {
            sum += A[i];
        }
    }

    // Return max sum obtained
    return sum;
}

// Function to return maximum of the
// maximum subset sum calculated
// for the two cases
static int findBest(int []A)
{
    // Case 1
    int x = maxSubset(A, false);

    // Case 2
    int y = maxSubset(A, true);

    // Modifying the sum
    y = -y;

    // Including first element
    y += A[0];

    // Negating again
    y = -y;

    // Return the required answer
    return Math.max(x, y);
}

// Driver Code
public static void main(String[] args)
{
    int []A = {1, 10, 4, -6, 3};
    System.out.print(findBest(A) + "\n");
}
}

// This code is contributed by 29AjayKumar**
```

## ****蟒蛇 3****

```
**# Python3 program to implement
# the above approach

# Function returns maximum subset
# sum from the given array=
def maxSubset(A, flag):

    n = len(A)
    sum = 0;

    # Case 2: Negate values
    # from A[1] to A[N-1]
    if (flag):
        for i in range(1, n):
            A[i] = -A[i]

    for i in range(1, n):

        # Include only positives
        # for max subset sum
        if (A[i] > 0):
            sum += A[i]

    # Return max sum obtained
    return sum

# Function to return maximum of the
# maximum subset sum calculated
# for the two cases
def findBest(A):

    # Case 1
    x = maxSubset(A, 0)

    # Case 2
    y = maxSubset(A, 1)

    # Modifying the sum
    y = -y

    # Including first element
    y += A[0]

    # Negating again
    y = -y

    # Return the required answer
    return max(x, y)

# Driver Code
if __name__ == "__main__":

    A = [ 1, 10, 4, -6, 3 ]

    print (findBest(A))

# This code is contributed by chitranayal**
```

## ****C#****

```
**// C# Program to implement
// the above approach
using System;
class GFG{

// Function returns maximum
// subset sum from the given array
static int maxSubset(int []A,
                     bool flag)
{
  int n = A.Length;
  int sum = 0;

  // Case 2: Negate values
  // from A[1] to A[N-1]
  if (flag)
  {
    for (int i = 1; i < n; i++)
      A[i] = -A[i];
  }

  for (int i = 1; i < n; i++)
  {
    // Include only positives
    // for max subset sum
    if (A[i] > 0)
    {
      sum += A[i];
    }
  }

  // Return max sum obtained
  return sum;
}

  // Function to return maximum of the
  // maximum subset sum calculated
  // for the two cases
  static int findBest(int []A)
  {
    // Case 1
    int x = maxSubset(A, false);

    // Case 2
    int y = maxSubset(A, true);

    // Modifying the sum
    y = -y;

    // Including first element
    y += A[0];

    // Negating again
    y = -y;

    // Return the required answer
    return Math.Max(x, y);
}

// Driver Code
public static void Main(String[] args)
{
  int []A = {1, 10, 4, -6, 3};
  Console.Write(findBest(A) + "\n");
}
}

// This code is contributed by 29AjayKumar**
```

## ****java 描述语言****

```
**<script>
// JavaScript program for the above approach

// Function returns maximum subset sum
// from the given array=
function maxSubset(A, flag)
{
    let n = A.length;
    let sum = 0;

    // Case 2: Negate values
    // from A[1] to A[N-1]
    if (flag)
    {
        for (let i = 1; i < n; i++)
            A[i] = -A[i];
    }

    for (let i = 1; i < n; i++)
    {
        // Include only positives
        // for max subset sum
        if (A[i] > 0)
        {
            sum += A[i];
        }
    }

    // Return max sum obtained
    return sum;
}

// Function to return maximum of the
// maximum subset sum calculated
// for the two cases
function findBest(A)
{
    // Case 1
    let x = maxSubset(A, false);

    // Case 2
    let y = maxSubset(A, true);

    // Modifying the sum
    y = -y;

    // Including first element
    y += A[0];

    // Negating again
    y = -y;

    // Return the required answer
    return Math.max(x, y);
}

// Driver Code

    let A = [ 1, 10, 4, -6, 3 ];
    document.write(findBest(A) + "\n");

</script>**
```

******Output:** 

```
17
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(1)****
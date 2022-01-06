# 将所有 1 放在一个索引处所需的最小步数

> 原文:[https://www . geeksforgeeks . org/按单次索引放置全 1 所需的最小步骤数/](https://www.geeksforgeeks.org/minimum-number-of-steps-required-to-place-all-1s-at-a-single-index/)

给定大小为 **N** 的二进制[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，其中所有 **1** s 都可以移动到其相邻位置，任务是打印大小为 **N** 的数组**RES【】**，其中**RES【I】**包含在**I<sup>th</sup>T19 处移动所有 **1** s 所需的最小步数**

**示例:**

> **输入:** A[] = {1，0，1，0}
> **输出:** {2，2，2，4}
> **解释:**
> 对于 i = 0，将全 1 移动到 0 <sup>第</sup>个索引需要 2 步，即 ABS(0–0)+ABS(0–2)= 2。
> 对于 i = 1，将全 1 移动到 1 <sup>st</sup> 索引需要 2 步，即 ABS(1–0)+ABS(1–2)= 2。
> 对于 i = 2，将全 1 移动到 2 <sup>nd</sup> 索引需要 2 步，即 ABS(2–0)+ABS(2–2)= 2。
> 对于 i = 3，将所有 1 移动到 3 <sup>rd</sup> 索引需要 4 步，即 ABS(3–0)+ABS(3–2)= 4。
> 因此，res[]是{2，2，2，4}
> 
> **输入:** A[] = {0，0，1，0，0，1}
> **输出:** {7，5，3，3，3，}
> **解释:**
> 对于 i = 0，将全 1 移动到 0 <sup>th</sup> 索引需要 7 步，即 ABS(2–0)+ABS(5–0)= 7。
> 对于 i = 1，将全 1 移动到 1 <sup>st</sup> 索引需要 5 步，即 ABS(2–1)+ABS(5–1)= 5。
> 对于 i = 2，将全 1 移动到 2 <sup>nd</sup> 索引需要 3 步，即 ABS(2–2)+ABS(5–2)= 3。
> 对于 i = 3，将所有 1 移动到第三个索引将需要 3 步，即 ABS(2–2)+ABS(5–3)= 3。
> 对于 i = 4，将全 1 移动到第 4 个<sup>指数将采取 3 个步骤，即 ABS(2–4)+ABS(5–4)= 3。
> 对于 i = 5，将全 1 移动到第 5 个<sup>指数需要 3 步，即 ABS(2–5)+ABS(5–5)= 3。
> 因此，res[]是{7，5，3，3，3，3}</sup></sup>

**幼稚的做法**:按照步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
2.  对于每一个**I**T2 指数，计算将所有 **1** s 移动到**I**T8 指数所需的步数。
3.  使用一个变量迭代范围**【0，N–1】**，比如 **i.**
    *   初始化**步= 0。**
    *   使用变量 **j.** 在范围**【0，N–1】**内迭代
    *   如果 **A[j]** 等于 **1，**将**ABS(I–j)**加到**步。**
4.  打印最小步数**。**

*****时间复杂度:**O(N<sup>2</sup>)*
*T8】辅助空间: O(1***

****高效途径:**优化上述途径，思路是使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。按照以下步骤解决此问题:**

1.  **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。**
2.  **初始化一个数组，说**左[]，**并初始化**计数= A[0]。****
3.  **迭代范围**【1，N–1】**，更新**左[i] =左[I–1]+计数**，其中**计数**为 **i.** 左侧 **1** s 的个数**
4.  **初始化一个数组，说**右[]，**并初始化**计数= A[N–1]。****
5.  **迭代范围**【N–2，0】**，更新**右[i] =右[i + 1] +计数**，其中**计数**为 **i.** 右侧 **1** s 的个数**
6.  **计算并更新 **res[]** 中的最终答案，其中 **res[i]** 为左右两侧步数之和，即 **res[i] =右[i] +左[i]****
7.  **[打印阵列](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)T2【RES】。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print minimum steps
// required to shift all 1s to a
// single index in a binary array
void minsteps(vector<int>& A)
{
    // Size of array
    int n = A.size();

    // Used to store cumulative sum
    vector<int> left(n, 0), right(n, 0), res(n, 0);

    // Initialize count
    int count = A[0];

    // Traverse the array in
    // forward direction
    for (int i = 1; i < n; i++) {
        // Steps needed to store all
        // previous ones to ith index
        left[i] = left[i - 1] + count;

        // Count number of 1s
        // present till i-th index
        count += A[i];
    }

    // Initialize count
    count = A[n - 1];

    // Traverse the array in
    // backward direction
    for (int i = n - 2; i >= 0; i--) {
        // Steps needed to store all 1s to
        // the right of i at current index
        right[i] = right[i + 1] + count;

        // Count number of 1s
        // present after i-th index
        count += A[i];
    }

    // Print the number of steps required
    for (int i = 0; i < n; i++) {
        res[i] = left[i] + right[i];
        cout << res[i] << " ";
    }
    cout << "\n";
}

// Driver Code
int main()
{
    vector<int> A = { 1, 0, 1, 0 };
    minsteps(A);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
class GFG
{

  // Function to print minimum steps
  // required to shift all 1s to a
  // single index in a binary array
  static void minsteps(int[] A)
  {

    // Size of array
    int n = A.length;

    // Used to store cumulative sum
    int[] left = new int [n];
    Arrays.fill(left, 0);
    int[] right = new int [n];
    Arrays.fill(right, 0);
    int[] res = new int [n];
    Arrays.fill(res, 0);

    // Initialize count
    int count = A[0];

    // Traverse the array in
    // forward direction
    for (int i = 1; i < n; i++) {
      // Steps needed to store all
      // previous ones to ith index
      left[i] = left[i - 1] + count;

      // Count number of 1s
      // present till i-th index
      count += A[i];
    }

    // Initialize count
    count = A[n - 1];

    // Traverse the array in
    // backward direction
    for (int i = n - 2; i >= 0; i--) {
      // Steps needed to store all 1s to
      // the right of i at current index
      right[i] = right[i + 1] + count;

      // Count number of 1s
      // present after i-th index
      count += A[i];
    }

    // Print the number of steps required
    for (int i = 0; i < n; i++) {
      res[i] = left[i] + right[i];
      System.out.print(res[i] + " ");
    }
    System.out.println();
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] A = { 1, 0, 1, 0 };
    minsteps(A);
  }
}

// This code is contributed by souravghosh0416.
```

## **蟒蛇 3**

```
# Python3 implementation of
# the above approach

# Function to print minimum steps
# required to shift all 1s to a
# single index in a binary array
def minsteps(A):

    # Size of array
    n = len(A)

    # Used to store cumulative sum
    left, right, res =[0]*n, [0]*n, [0]*n

    # Initialize count
    count = A[0]

    # Traverse the array in
    # forward direction
    for i in range(1, n):

        # Steps needed to store all
        # previous ones to ith index
        left[i] = left[i - 1] + count

        # Count number of 1s
        # present till i-th index
        count += A[i]

    # Initialize count
    count = A[n - 1]

    # Traverse the array in
    # backward direction
    for i in range(n - 2, -1, -1):

        # Steps needed to store all 1s to
        # the right of i at current index
        right[i] = right[i + 1] + count

        # Count number of 1s
        # present after i-th index
        count += A[i]

    # Print the number of steps required
    for i in range(n):
        res[i] = left[i] + right[i]
        print(res[i], end = " ")
    print()

# Driver Code
if __name__ == '__main__':
    A = [1, 0, 1, 0]
    minsteps(A)

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# Program to implement
// the above approach
using System;
class GFG
{

  // Function to print minimum steps
  // required to shift all 1s to a
  // single index in a binary array
  static void minsteps(int[] A)
  {

    // Size of array
    int n = A.Length;

    // Used to store cumulative sum
    int[] left = new int [n];
    for (int i = 1; i < n; i++) {
      left[i] = 0;
    }

    int[] right = new int [n];
    for (int i = 1; i < n; i++) {
      right[i] = 0;
    }

    int[] res = new int [n];
    for (int i = 1; i < n; i++) {
      res[i] = 0;
    }

    // Initialize count
    int count = A[0];

    // Traverse the array in
    // forward direction
    for (int i = 1; i < n; i++) {
      // Steps needed to store all
      // previous ones to ith index
      left[i] = left[i - 1] + count;

      // Count number of 1s
      // present till i-th index
      count += A[i];
    }

    // Initialize count
    count = A[n - 1];

    // Traverse the array in
    // backward direction
    for (int i = n - 2; i >= 0; i--) {
      // Steps needed to store all 1s to
      // the right of i at current index
      right[i] = right[i + 1] + count;

      // Count number of 1s
      // present after i-th index
      count += A[i];
    }

    // Print the number of steps required
    for (int i = 0; i < n; i++) {
      res[i] = left[i] + right[i];
      Console.Write(res[i] + " ");
    }
    Console.WriteLine();
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] A = { 1, 0, 1, 0 };
    minsteps(A);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## **java 描述语言**

```
<script>

// JavaScript program to implement
// the above approach

  // Function to print minimum steps
  // required to shift all 1s to a
  // single index in a binary array
  function minsteps(A)
  {

    // Size of array
    let n = A.length;

    // Used to store cumulative sum
    let left = Array.from({length: n}, (_, i) => 0);
    let right = Array.from({length: n}, (_, i) => 0);
    let res = Array.from({length: n}, (_, i) => 0);

    // Initialize count
    let count = A[0];

    // Traverse the array in
    // forward direction
    for (let i = 1; i < n; i++) {
      // Steps needed to store all
      // previous ones to ith index
      left[i] = left[i - 1] + count;

      // Count number of 1s
      // present till i-th index
      count += A[i];
    }

    // Initialize count
    count = A[n - 1];

    // Traverse the array in
    // backward direction
    for (let i = n - 2; i >= 0; i--) {
      // Steps needed to store all 1s to
      // the right of i at current index
      right[i] = right[i + 1] + count;

      // Count number of 1s
      // present after i-th index
      count += A[i];
    }

    // Print the number of steps required
    for (let i = 0; i < n; i++) {
      res[i] = left[i] + right[i];
      document.write(res[i] + " ");
    }
    document.write("<br/>");
  }

// Driver code   
    let A = [ 1, 0, 1, 0 ];
    minsteps(A);

// This code is contributed by sanjoy_62.
</script>
```

****Output:** 

```
2 2 2 4
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**
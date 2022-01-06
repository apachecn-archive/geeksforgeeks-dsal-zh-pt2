# 使用数字 A 或 B

可以将 X 和 Y 的最大次数减少到接近 0

> 原文:[https://www . geesforgeks . org/maximum-times-x-and-y-可以使用数字-a-或-b/](https://www.geeksforgeeks.org/maximum-times-x-and-y-can-be-reduced-to-near-0-using-numbers-a-or-b/) 减少到接近 0

给定 4 个整数 **X，Y，A，B** 。在一次移动中，或者将 **X** 减少 **A** 和 **Y** 减少 **B** 或者将 **X** 减少 **B** 和 **Y** 减少 **A** 。计算最大可能移动量。给定 4 个整数 **X，Y，A，B** 。一步到位我们就能做出**X**=**X**–**A**和**Y**=**Y**–**B**或者 X =**X**–**B**和**Y**=**Y**–**A**。计算最大可能移动总数。

**示例:**

> **输入:** X = 10，Y = 12，A = 2，B = 5
> **输出:** 3
> **解释**:第一步:A 减 X，B 减 Y 后 X = 8，Y = 7
> 第二步:A 减 X，B 减 Y 后 X = 6，Y = 2
> 第三步:B 减 X，A 减 Y 后 X = 1，Y = 0
> 这样一共可以进行 3 步。
> 
> **输入:** X = 1，Y = 1，A = 2，B = 2
> T3】输出: 0

**天真法:**在 **X** 和 **Y** 的每个值上，我们可以从 **X** 和 **Y** 的最大值中减去 **A** 和 **B** 的最大值，从 **X** 和 **Y** 的最小值中减去 **A** 和 **B** 的最小值，直到 X 和 Y 保持大于零。

**有效方法:**给定的问题可以在答题技巧上使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决。

*   这里的关键思想是，如果对于任意数量的移动 **N** 如果可以执行这么多移动，那么我们也可以执行**N**–1 个移动。
*   所以我们可以对答案做一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。固定范围 **L** = 1 和 **R** = 10000000(如果有大的整数值，请更改此值)并且对于每个值 mid = ( **L** + **R** )/2 检查我们是否可以执行如此多的移动。如果可能的话，将 **L** =中间+ 1，否则 **R** =中间-1。返回最大可能值。
*   要检查任何数字 mid，我们必须至少减少 X 和 Y mid * min(**A**、 **B** )，对于剩余元素，我们可以计算|**A**–**B**|。如果这些值大于中间值，则增加我们的右边范围，否则减少左边范围。

**实施:**

## C++

```
// C++ Program to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Helper function to check if
// we can perform Mid number of moves
#define MAXN 10000000 // MAXN = 1e7

bool can(int Mid, int X, int Y, int A, int B)
{
    // Remove atleast Mid * B from both X and Y
    int p1 = X - Mid * B;
    int p2 = Y - Mid * B;

    // If any value is negative return false.
    if (p1 < 0 || p2 < 0) {
        return false;
    }

    // Calculate remaining values
    int k = A - B;
    if (k == 0) {
        return true;
    }

    int val = p1 / k + p2 / k;

    // If val >= Mid then it is possible
    // to perform this much moves
    if (val >= Mid) {
        return true;
    }

    // else return false
    return false;
}

int maxPossibleMoves(int X, int Y, int A, int B)
{
    // Initialize a variable to store the answer
    int ans = 0;

    // Fix the left and right range
    int L = 1, R = MAXN;

    // Binary Search over the answer
    while (L <= R) {

        // Check for the middle
        // value as the answer
        int Mid = (L + R) / 2;
        if (can(Mid, X, Y, A, B)) {

            // It is possible to perform
            // this much moves
            L = Mid + 1;

            // Maximise the answer
            ans = max(ans, Mid);
        }
        else {
            R = Mid - 1;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
int main()
{

    int X = 10, Y = 12, A = 2, B = 5;
    // Generalise that A >= B
    if (A < B) {
        swap(A, B);
    }
    cout << maxPossibleMoves(X, Y, A, B);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.io.*;

class GFG{

// Helper function to check if
// we can perform Mid number of moves
static int MAXN = 10000000;

static boolean can(int Mid, int X, int Y,
                   int A, int B)
{

    // Remove atleast Mid * B from both X and Y
    int p1 = X - Mid * B;
    int p2 = Y - Mid * B;

    // If any value is negative return false.
    if (p1 < 0 || p2 < 0)
    {
        return false;
    }

    // Calculate remaining values
    int k = A - B;
    if (k == 0)
    {
        return true;
    }

    int val = p1 / k + p2 / k;

    // If val >= Mid then it is possible
    // to perform this much moves
    if (val >= Mid)
    {
        return true;
    }

    // Else return false
    return false;
}

static int maxPossibleMoves(int X, int Y, int A, int B)
{

    // Initialize a variable to store the answer
    int ans = 0;

    // Fix the left and right range
    int L = 1, R = MAXN;

    // Binary Search over the answer
    while (L <= R)
    {

        // Check for the middle
        // value as the answer
        int Mid = (L + R) / 2;

        if (can(Mid, X, Y, A, B))
        {

            // It is possible to perform
            // this much moves
            L = Mid + 1;

            // Maximise the answer
            ans = Math.max(ans, Mid);
        }
        else
        {
            R = Mid - 1;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int X = 10, Y = 12, A = 2, B = 5;

    // Generalise that A >= B
    if (A < B)
    {
        int temp = A;
        A = B;
        B = temp;
    }

    System.out.println(maxPossibleMoves(X, Y, A, B));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python Program to implement the above approach

# Helper function to check if
# we can perform Mid number of moves
MAXN = 10000000

def can(Mid, X, Y, A, B):

    # Remove atleast Mid * B from both X and Y
    p1 = X - Mid * B
    p2 = Y - Mid * B

    # If any value is negative return false.
    if (p1 < 0 or p2 < 0):
        return False

    # Calculate remaining values
    k = A - B
    if (k == 0):
        return True

    val = p1 // k + p2 // k

    # If val >= Mid then it is possible
    # to perform this much moves
    if (val >= Mid):
        return True

    # else return false
    return False

def maxPossibleMoves(X, Y, A, B):

    # Initialize a variable to store the answer
    ans = 0

    # Fix the left and right range
    L = 1
    R = MAXN

    # Binary Search over the answer
    while (L <= R):

        # Check for the middle
        # value as the answer
        Mid = (L + R) // 2
        if (can(Mid, X, Y, A, B)):

            # It is possible to perform
            # this much moves
            L = Mid + 1

            # Maximise the answer
            ans = max(ans, Mid)
        else:
            R = Mid - 1

    # Return answer
    return ans

# Driver Code
X = 10
Y = 12
A = 2
B = 5
# Generalise that A >= B
if (A < B):
    tmp = A
    A = B
    B = tmp

print(maxPossibleMoves(X, Y, A, B))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to implement the above approach
using System;

class GFG{

// Helper function to check if
// we can perform Mid number of moves
static int MAXN = 10000000;

static Boolean can(int Mid, int X, int Y,
                   int A, int B)
{

    // Remove atleast Mid * B from both X and Y
    int p1 = X - Mid * B;
    int p2 = Y - Mid * B;

    // If any value is negative return false.
    if (p1 < 0 || p2 < 0)
    {
        return false;
    }

    // Calculate remaining values
    int k = A - B;
    if (k == 0)
    {
        return true;
    }

    int val = p1 / k + p2 / k;

    // If val >= Mid then it is possible
    // to perform this much moves
    if (val >= Mid)
    {
        return true;
    }

    // Else return false
    return false;
}

static int maxPossibleMoves(int X, int Y, int A, int B)
{

    // Initialize a variable to store the answer
    int ans = 0;

    // Fix the left and right range
    int L = 1, R = MAXN;

    // Binary Search over the answer
    while (L <= R)
    {

        // Check for the middle
        // value as the answer
        int Mid = (L + R) / 2;

        if (can(Mid, X, Y, A, B))
        {

            // It is possible to perform
            // this much moves
            L = Mid + 1;

            // Maximise the answer
            ans = Math.Max(ans, Mid);
        }
        else
        {
            R = Mid - 1;
        }
    }

    // Return answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int X = 10, Y = 12, A = 2, B = 5;

    // Generalise that A >= B
    if (A < B)
    {
        int temp = A;
        A = B;
        B = temp;
    }

    Console.Write(maxPossibleMoves(X, Y, A, B));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript Program to implement the above approach

// Helper function to check if
// we can perform Mid number of moves
let MAXN = 10000000; // MAXN = 1e7

function can(Mid, X, Y, A, B)
{

  // Remove atleast Mid * B from both X and Y
  let p1 = X - Mid * B;
  let p2 = Y - Mid * B;

  // If any value is negative return false.
  if (p1 < 0 || p2 < 0) {
    return false;
  }

  // Calculate remaining values
  let k = A - B;
  if (k == 0) {
    return true;
  }

  let val = Math.floor(p1 / k) + Math.floor(p2 / k);

  // If val >= Mid then it is possible
  // to perform this much moves
  if (val >= Mid) {
    return true;
  }

  // else return false
  return false;
}

function maxPossibleMoves(X, Y, A, B)
{

  // Initialize a variable to store the answer
  let ans = 0;

  // Fix the left and right range
  let L = 1,
    R = MAXN;

  // Binary Search over the answer
  while (L <= R)
  {

    // Check for the middle
    // value as the answer
    let Mid = Math.floor((L + R) / 2);
    if (can(Mid, X, Y, A, B))
    {

      // It is possible to perform
      // this much moves
      L = Mid + 1;

      // Maximise the answer
      ans = Math.max(ans, Mid);
    } else {
      R = Mid - 1;
    }
  }

  // Return answer
  return ans;
}

// Driver Code
let X = 10,
  Y = 12,
  A = 2,
  B = 5;

// Generalise that A >= B
if (A < B) {
  let temp = A;
  A = B;
  B = temp;
}
document.write(maxPossibleMoves(X, Y, A, B));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(log(MAXN))，其中 MAXN 为最大移动次数
T3】辅助空间: O(1)
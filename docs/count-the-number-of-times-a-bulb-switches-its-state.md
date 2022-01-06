# 统计灯泡切换状态的次数

> 原文:[https://www . geeksforgeeks . org/count-灯泡切换状态的次数/](https://www.geeksforgeeks.org/count-the-number-of-times-a-bulb-switches-its-state/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **开关[]** ，由表示开关是**开(0)** 还是**关(1)** 的二进制整数和**查询[]** 组成，其中**查询[i]** 表示要切换的开关。完成所有开关切换后的任务是打印灯泡改变状态的次数，即从**开**到**关**或反之。

**示例:**

> **输入**:开关[] ={1，1，0}，查询[] = {3，2，1}
> **输出:** 1
> **解释:**
> 开关{1，1，0}的初始状态。由于 1 的计数= 2 ( > = ceil(N / 2))，灯泡会发光。
> 查询[0] = 3
> 开关{1，1，1}的下一个状态。由于 1 的计数= 3 ( > = ceil(N / 2))，灯泡会发光。
> 查询[1] = 2
> 开关{1，0，1}的下一个状态。由于 1 的计数= 2 ( > = ceil(N / 2))，灯泡会发光。
> 查询[2] = 1
> 开关{0，0，1}的下一个状态..由于 1 的计数= 1 ( < ceil(N / 2))，灯泡关闭。
> 因此，灯泡女巫从发光到不发光的状态只有一次。
> 
> **输入**:开关[] = { 1，1，0，0，1，1 }
> 查询[] = { 4，3，6 }
> **输出** : 0

**接近**:按照以下步骤解决问题:

1.  [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。
2.  计数 **1** s 的数量，以记录灯泡的初始状态。
3.  遍历数组**查询[]。**
4.  每次**查询【I】**，更新**arr【】**和 **1** s 的计数，相应检查灯泡的当前状态。
5.  如果发现前一状态和当前状态不同，则增加**计数。**
6.  最后，打印**计数的值。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// times a bulb switches its state
int solve(int A[], int n,
          int Q[], int q)
{

  // Count of 1s
  int one = 0;

  // Traverse the array
  for (int i = 0; i < n; i++)

    // Update count of 1s
    if (A[i] == 1)
      one++;

  // Update the status of bulb
  int glows = 0, count = 0;

  if (one >= ceil(n / 2))
    glows = 1;

  // Traverse the array Q[]
  for (int i = 0; i < q; i++) {

    // Stores previous state
    // of the bulb
    int prev = glows;

    // Toggle the switch and
    // update count of 1s
    if (A[Q[i] - 1] == 1)
      one--;
    if (A[Q[i] - 1] == 0)
      one++;

    A[Q[i] - 1] ^= 1;

    if (one >= ceil(n / 2.0)) {
      glows = 1;
    }
    else {
      glows = 0;
    }

    // If the bulb switches state
    if (prev != glows)
      count++;
  }

  // Return count
  return count;
}

// Driver Code
int main()
{

  // Input
  int n = 3;
  int arr[] = { 1, 1, 0 };
  int q = 3;

  // Queries
  int Q[] = { 3, 2, 1 };

  // Function call to find number
  // of times the bulb toggles
  cout << solve(arr, n, Q, q);

  return 0;
}

// This code is contributed by splevel62.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach

import java.util.*;
public class Main {

    // Function to find the number of
    // times a bulb switches its state
    static int solve(int[] A, int n,
                     int Q[], int q)
    {
        // Count of 1s
        int one = 0;

        // Traverse the array
        for (int i = 0; i < n; i++)

            // Update count of 1s
            if (A[i] == 1)
                one++;

        // Update the status of bulb
        int glows = 0, count = 0;

        if (one >= (int)Math.ceil(n / 2))
            glows = 1;

        // Traverse the array Q[]
        for (int i = 0; i < q; i++) {

            // Stores previous state
            // of the bulb
            int prev = glows;

            // Toggle the switch and
            // update count of 1s
            if (A[Q[i] - 1] == 1)
                one--;
            if (A[Q[i] - 1] == 0)
                one++;

            A[Q[i] - 1] ^= 1;

            if (one >= (int)Math.ceil(n / 2.0)) {
                glows = 1;
            }
            else {
                glows = 0;
            }

            // If the bulb switches state
            if (prev != glows)
                count++;
        }

        // Return count
        return count;
    }

    // Driver Code
    public static void main(String args[])
    {
        // Input
        int n = 3;
        int arr[] = { 1, 1, 0 };
        int q = 3;

        // Queries
        int Q[] = { 3, 2, 1 };

        // Function call to find number
        // of times the bulb toggles
        System.out.println(
            solve(arr, n, Q, q));
    }
}
```

## 蟒蛇 3

```
# Python program for
# the above approach
import math

# Function to find the number of
# times a bulb switches its state
def solve(A, n, Q, q):

    # count of 1's
    one = 0

    # Traverse the array
    for i in range(0, n):

        # update the array
        if (A[i] == 1):
            one += 1

    # update the status of bulb
    glows = 0
    count = 0
    if (one >= int(math.ceil(n / 2))):
        glows = 1

    # Traverse the array Q[]
    for i in range(0, q):

        # stores previous state of
        # the bulb
        prev = glows

        # Toggle the switch and
        # update the count of 1's
        if (A[Q[i] - 1] == 1):
            one -= 1
        if (A[Q[i] - 1] == 0):
            one += 1
        A[Q[i] - 1] ^= 1
        if (one >= int(math.ceil(n/2.0))):
            glows = 1
        else:
            glows = 0
        # if the bulb switches state
        if (prev != glows):
            count += 1

    # Return count
    return count

# Driver code

# Input
n = 3
arr = [1, 1, 0]
q = 3

# Queries
Q = [3, 2, 1]

# Function call to find number
# of times the bulb toggles
print(solve(arr, n, Q, q))

# This code id contributed by Virusbuddah
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the number of
  // times a bulb switches its state
  static int solve(int[] A, int n,
                   int[] Q, int q)
  {

    // Count of 1s
    int one = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)

      // Update count of 1s
      if (A[i] == 1)
        one++;

    // Update the status of bulb
    int glows = 0, count = 0;

    if (one >= (int)Math.Ceiling((double)n / 2))
      glows = 1;

    // Traverse the array Q[]
    for (int i = 0; i < q; i++) {

      // Stores previous state
      // of the bulb
      int prev = glows;

      // Toggle the switch and
      // update count of 1s
      if (A[Q[i] - 1] == 1)
        one--;
      if (A[Q[i] - 1] == 0)
        one++;

      A[Q[i] - 1] ^= 1;

      if (one >= (int)Math.Ceiling((double)n / 2.0)) {
        glows = 1;
      }
      else {
        glows = 0;
      }

      // If the bulb switches state
      if (prev != glows)
        count++;
    }

    // Return count
    return count;
  }

  // Driver Code
  static public void Main ()
  {

    // Input
    int n = 3;
    int[] arr = { 1, 1, 0 };
    int q = 3;

    // Queries
    int[] Q = { 3, 2, 1 };

    // Function call to find number
    // of times the bulb toggles
    Console.WriteLine(
      solve(arr, n, Q, q));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the number of
// times a bulb switches its state
function solve(A, n, Q, q)
{

  // Count of 1s
  var one = 0;

  // Traverse the array
  for (var i = 0; i < n; i++)

    // Update count of 1s
    if (A[i] == 1)
      one++;

  // Update the status of bulb
  var glows = 0, count = 0;

  if (one >= Math.ceil(n / 2))
    glows = 1;

  // Traverse the array Q[]
  for (var i = 0; i < q; i++) {

    // Stores previous state
    // of the bulb
    var prev = glows;

    // Toggle the switch and
    // update count of 1s
    if (A[Q[i] - 1] == 1)
      one--;
    if (A[Q[i] - 1] == 0)
      one++;

    A[Q[i] - 1] ^= 1;

    if (one >= Math.ceil(n / 2.0)) {
      glows = 1;
    }
    else {
      glows = 0;
    }

    // If the bulb switches state
    if (prev != glows)
      count++;
  }

  // Return count
  return count;
}

// Driver Code
// Input
var n = 3;
var arr = [1, 1, 0];
var q = 3;

// Queries
var Q = [3, 2, 1];

// Function call to find number
// of times the bulb toggles
document.write( solve(arr, n, Q, q));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
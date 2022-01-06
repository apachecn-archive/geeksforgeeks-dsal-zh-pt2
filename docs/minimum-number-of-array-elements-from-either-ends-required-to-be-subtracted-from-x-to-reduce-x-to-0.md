# 要求从 X 中减去任一端的最小数组元素数，以将 X 减少到 0

> 原文:[https://www . geeksforgeeks . org/最小数组元素数-从任意一端-需要从 x 中减去-减少-x-到-0/](https://www.geeksforgeeks.org/minimum-number-of-array-elements-from-either-ends-required-to-be-subtracted-from-x-to-reduce-x-to-0/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **nums[]** 和一个整数 **X** ，任务是通过移除最左边或最右边的数组元素并从 **X、**中减去其值的最小次数，将 **X** 减少到 **0** 。如果可以将 **X** 减少到 **0** ，打印所需操作的次数。否则，返回-1。

**示例:**

> **输入:** nums[] = {3，2，20，1，1，3}，X = 10
> **输出:** 5
> **解释:**X =(10)–3–1–3–2 = 0。因此，所需的操作数为 5。
> 
> **输入:** nums[] = {1，1，4，2，3}，X = 5
> **输出:** 2
> **解释:**X(= 5)–3–2 = 0。因此，所需的操作数为 2。

**方法:**给定的问题可以使用[两点](https://www.geeksforgeeks.org/two-pointers-technique/)技术来解决。按照以下步骤解决问题。

*   保持 t *两个指针**左**和**右，**T5】指向从 **X** 中排除的左右子阵列的末端。*
*   初始化**左**考虑整个数组，**右**不包含任何内容。
*   因此，用数组的[和来减少 **X** 。](https://www.geeksforgeeks.org/python-program-to-find-sum-of-array/)
*   现在，迭代直到**左侧**到达数组的前面。
    *   如果**左**和**右**子阵列的总和超过 **X** ( *即 **X** < 0* ，则将**左**向左移动一个索引并增加 **X** 该元素。
    *   如果**左**和**右**子阵列之和小于 **X** ( *即**X**T12】0*，则将**右**指针向左移动一个索引，并以该元素减少 X。
    *   如果在任何时候发现 X 为 0，请更新所需的最小操作数。
*   打印所需的最小操作数。
*   下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of operations required
// to reduce x to 0
static int minOperations(int nums[], int N,
                         int x)
{

    // If sum of the array
    // is less than x
    int sum = 0;

    for(int i = 0; i < x; i++)
        sum += nums[i];

    if (sum < x)
        return -1;

    // Stores the count
    // of operations
    int ans = INT_MAX;

    // Two pointers to traverse the array
    int l = N - 1, r = N;

    // Reduce x by the sum
    // of the entire array
    x -= sum;

    // Iterate until l reaches
    // the front of the array
    while (l >= 0)
    {

        // If sum of elements from
        // the front exceeds x
        if (x <= 0)
        {

            // Shift towards left
            x += nums[l];
            l -= 1;
        }

        // If sum exceeds 0
        if (x > 0)
        {

            // Reduce x by elements
            // from the right
            r -= 1;
            x -= nums[r];
        }

        // If x is reduced to 0
        if (x == 0)
        {

            // Update the minimum count
            // of operations required
            ans = min(ans,
            (l + 1) + (N - r));
        }
    }

    if (ans < INT_MAX)
        return ans;
    else
        return -1;
}

// Driver Code
int main()
{
    int nums[] = { 1, 1, 4, 2, 3 };

     // Size of the array
    int N = sizeof(nums) / sizeof(nums[0]);

    int x = 5;
    cout << minOperations(nums, N, x);

    return 0;
}

// This code is contributed by code_hunt
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

  // Function to count the minimum
  // number of operations required
  // to reduce x to 0
  static int minOperations(int nums[], int x)
  {

    // If sum of the array
    // is less than x
    int sum = 0;
    for (int i = 0; i < x; i++)
      sum += nums[i];
    if (sum < x)
      return -1;

    // Stores the count
    // of operations
    int ans = Integer.MAX_VALUE;

    // Two pointers to traverse the array
    int l = nums.length - 1, r = nums.length;

    // Reduce x by the sum
    // of the entire array
    x -= sum;

    // Iterate until l reaches
    // the front of the array
    while (l >= 0) {

      // If sum of elements from
      // the front exceeds x
      if (x <= 0) {

        // Shift towards left
        x += nums[l];
        l -= 1;
      }

      // If sum exceeds 0
      if (x > 0) {

        // Reduce x by elements
        // from the right
        r -= 1;
        x -= nums[r];
      }

      // If x is reduced to 0
      if (x == 0) {

        // Update the minimum count
        // of operations required
        ans = Math.min(ans,
                       (l + 1) + (nums.length - r));
      }
    }
    if (ans < Integer.MAX_VALUE)
      return ans;
    else
      return -1;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] nums = { 1, 1, 4, 2, 3 };
    int x = 5;
    System.out.println(minOperations(nums, x));
  }
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

import math

# Function to count the minimum
# number of operations required
# to reduce x to 0
def minOperations(nums, x):

    # If sum of the array
    # is less than x
    if sum(nums) < x:
        return -1

    # Stores the count
    # of operations
    ans = math.inf

    # Two pointers to traverse the array
    l, r = len(nums)-1, len(nums)

    # Reduce x by the sum
    # of the entire array
    x -= sum(nums)

    # Iterate until l reaches
    # the front of the array
    while l >= 0:

        # If sum of elements from
        # the front exceeds x
        if x <= 0:

            # Shift towards left
            x += nums[l]
            l -= 1

        # If sum exceeds 0
        if x > 0:

            # Reduce x by elements
            # from the right
            r -= 1
            x -= nums[r]

        # If x is reduced to 0
        if x == 0:

            # Update the minimum count
            # of operations required
            ans = min(ans, (l+1) + (len(nums)-r))

    return ans if ans < math.inf else -1

# Driver Code
nums = [1, 1, 4, 2, 3]
x = 5
print(minOperations(nums, x))
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG {

  // Function to count the minimum
  // number of operations required
  // to reduce x to 0
  static int minOperations(int[] nums, int x)
  {

    // If sum of the array
    // is less than x
    int sum = 0;
    for (int i = 0; i < x; i++)
      sum += nums[i];
    if (sum < x)
      return -1;

    // Stores the count
    // of operations
    int ans = Int32.MaxValue;

    // Two pointers to traverse the array
    int l = nums.Length - 1, r = nums.Length;

    // Reduce x by the sum
    // of the entire array
    x -= sum;

    // Iterate until l reaches
    // the front of the array
    while (l >= 0) {

      // If sum of elements from
      // the front exceeds x
      if (x <= 0) {

        // Shift towards left
        x += nums[l];
        l -= 1;
      }

      // If sum exceeds 0
      if (x > 0) {

        // Reduce x by elements
        // from the right
        r -= 1;
        x -= nums[r];
      }

      // If x is reduced to 0
      if (x == 0) {

        // Update the minimum count
        // of operations required
        ans = Math.Min(ans,
                       (l + 1) + (nums.Length - r));
      }
    }
    if (ans < Int32.MaxValue)
      return ans;
    else
      return -1;
  }

  // Driver Code
  public static void Main()
  {
    int[] nums = { 1, 1, 4, 2, 3 };
    int x = 5;
    Console.Write(minOperations(nums, x));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the minimum
// number of operations required
// to reduce x to 0
function minOperations(nums, x)
{

    // If sum of the array
    // is less than x
    let sum = 0;
    for(let i = 0; i < x; i++)
        sum += nums[i];

    if (sum < x)
        return -1;

    // Stores the count
    // of operations
    let ans = Number.MAX_VALUE;

    // Two pointers to traverse the array
    let l = nums.length - 1, r = nums.length;

    // Reduce x by the sum
    // of the entire array
    x -= sum;

    // Iterate until l reaches
    // the front of the array
    while (l >= 0)
    {

        // If sum of elements from
        // the front exceeds x
        if (x <= 0)
        {

            // Shift towards left
            x += nums[l];
            l -= 1;
        }

        // If sum exceeds 0
        if (x > 0)
        {

            // Reduce x by elements
            // from the right
            r -= 1;
            x -= nums[r];
        }

        // If x is reduced to 0
        if (x == 0)
        {

            // Update the minimum count
            // of operations required
            ans = Math.min(ans,
                          (l + 1) +
                          (nums.length - r));
        }
    }

    if (ans < Number.MAX_VALUE)
        return ans;
    else
        return -1;
}

// Driver code
let nums = [ 1, 1, 4, 2, 3 ];
let x = 5;

document.write(minOperations(nums, x));

// This code is contributed by target_2

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
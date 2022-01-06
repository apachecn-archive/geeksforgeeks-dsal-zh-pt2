# 形成算术级数(AP)的子阵列的计数

> 原文:[https://www . geesforgeks . org/子阵计数-形成算术级数-ap/](https://www.geeksforgeeks.org/count-of-subarrays-forming-an-arithmetic-progression-ap/)

给定大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到至少长度为 2 的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，使得这些子阵列的连续元素之间的差异始终保持不变，即子阵列的元素形成一个 AP。
**示例:**

> **输入:** arr[] = {8，7，4，1，0}
> **输出:** 5
> **解释:**
> 所有大于 1 的子阵列组成一个 AP，它们是[8，7]，[7，4]，[4，1]，[1，0]，[7，4，1]
> 
> **输入:** arr[] = {4，2 }
> T3】输出: 1

**方法:**想法是[从给定阵列生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，检查相邻元素之间的差异对于生成的子阵列是否相同。以下是步骤:

1.  使用两个循环迭代每个长度至少为 2 的子数组。
2.  设 **i** 为子阵的起始指标， **j** 为子阵的结束指标。
3.  如果数组中从索引 I 到 j 的每对相邻元素之间的差值相同，则增加总计数。
4.  否则，对下一个子阵列重复上述过程。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <iostream>
using namespace std;

// Function to find the
// total count of subarrays
int calcSubarray(int A[], int N)
{

    int count = 0;

    // Iterate over each subarray
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N; j++) {

            bool flag = true;

            // Difference between first
            // two terms of subarray
            int comm_diff = A[i + 1] - A[i];

            // Iterate over the subarray
            // from i to j
            for (int k = i; k < j; k++) {

                // Check if the difference
                // of all adjacent elements
                // is same
                if (A[k + 1] - A[k] == comm_diff) {
                    continue;
                }
                else {
                    flag = false;
                    break;
                }
            }

            if (flag) {
                count++;
            }
        }
    }

    return count;
}

// Driver Code
int main()
{
    // Given array
    int A[5] = { 8, 7, 4, 1, 0 };
    int N = sizeof(A) / sizeof(int);

    // Function Call
    cout << calcSubarray(A, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to find the
// total count of subarrays
static int calcSubarray(int A[],
                        int N)
{
  int count = 0;

  // Iterate over each subarray
  for (int i = 0; i < N; i++)
  {
    for (int j = i + 1; j < N; j++)
    {
      boolean flag = true;

      // Difference between first
      // two terms of subarray
      int comm_diff = A[i + 1] - A[i];

      // Iterate over the subarray
      // from i to j
      for (int k = i; k < j; k++)
      {
        // Check if the difference
        // of all adjacent elements
        // is same
        if (A[k + 1] - A[k] == comm_diff)
        {
          continue;
        }
        else
        {
          flag = false;
          break;
        }
      }

      if (flag)
      {
        count++;
      }
    }
  }

  return count;
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int []A = {8, 7, 4, 1, 0};
  int N = A.length;

  // Function Call
  System.out.print(calcSubarray(A, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to find the
# total count of subarrays
def calcSubarray(A, N):

    count = 0

    # Iterate over each subarray
    for i in range(N):
        for j in range(i + 1, N):
            flag = True

            # Difference between first
            # two terms of subarray
            comm_diff = A[i + 1] - A[i]

            # Iterate over the subarray
            # from i to j
            for k in range(i, j):

                # Check if the difference
                # of all adjacent elements
                # is same
                if (A[k + 1] - A[k] == comm_diff):
                    continue
                else:
                    flag = False
                    break

            if (flag):
                count += 1

    return count

# Driver Code
if __name__ == '__main__':

    # Given array
    A = [ 8, 7, 4, 1, 0 ]
    N = len(A)

    # Function call
    print(calcSubarray(A, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to find the
// total count of subarrays
static int calcSubarray(int []A,
                        int N)
{
  int count = 0;

  // Iterate over each subarray
  for (int i = 0; i < N; i++)
  {
    for (int j = i + 1; j < N; j++)
    {
      bool flag = true;

      // Difference between first
      // two terms of subarray
      int comm_diff = A[i + 1] - A[i];

      // Iterate over the subarray
      // from i to j
      for (int k = i; k < j; k++)
      {
        // Check if the difference
        // of all adjacent elements
        // is same
        if (A[k + 1] - A[k] == comm_diff)
        {
          continue;
        }
        else
        {
          flag = false;
          break;
        }
      }

      if (flag)
      {
        count++;
      }
    }
  }

  return count;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int []A = {8, 7, 4, 1, 0};
  int N = A.Length;

  // Function Call
  Console.Write(calcSubarray(A, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to find the
// total count of subarrays
function calcSubarray(A, N)
{

    let count = 0;

    // Iterate over each subarray
    for (let i = 0; i < N; i++) {
        for (let j = i + 1; j < N; j++) {

            let flag = true;

            // Difference between first
            // two terms of subarray
            let comm_diff = A[i + 1] - A[i];

            // Iterate over the subarray
            // from i to j
            for (let k = i; k < j; k++) {

                // Check if the difference
                // of all adjacent elements
                // is same
                if (A[k + 1] - A[k] == comm_diff) {
                    continue;
                }
                else {
                    flag = false;
                    break;
                }
            }

            if (flag) {
                count++;
            }
        }
    }

    return count;
}

// Driver Code

    // Given array
    let A = [ 8, 7, 4, 1, 0 ];
    let N = A.length;

    // Function Call
    document.write(calcSubarray(A, N));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*
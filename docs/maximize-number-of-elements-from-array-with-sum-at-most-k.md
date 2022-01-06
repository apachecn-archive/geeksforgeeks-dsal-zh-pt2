# 最大化数组中元素的数量，总和最多为 K

> 原文:[https://www . geeksforgeeks . org/从最多 k 个和的数组中最大化元素数/](https://www.geeksforgeeks.org/maximize-number-of-elements-from-array-with-sum-at-most-k/)

给定一个由 N 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和一个整数 **K** ，任务是从数组中选择最大数量的元素，其和最多为 **K** 。

**示例:**

> **输入:** A[] = {1，12，5，111，200，1000，10}，K = 50
> **输出:** 4
> **说明:**
> 最大选择数将为1，12，5，10 即 1 + 12 + 5 + 10 = 28 < 50。
> 
> **输入:** A[] = {3，7，2，9，4}，K = 15
> **输出:** 3
> **说明:**
> 最大选择数为 3，2，4 即 3 + 2 + 4 =9 < 15。

**天真方法:**思路是[生成数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)并找到所有生成的子序列的元素之和。找到长度最大且和小于或等于 **K** 的子序列。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** (1)*

**有效方法:**有效方法可以使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。以下是步骤:

1.  [给定数组排序](https://www.geeksforgeeks.org/sorting-algorithms/)。
2.  在数组中迭代，保持对元素之和的跟踪，直到**之和小于或等于 K** 。
3.  如果在上述步骤中迭代的总和超过 **K** ，则中断循环并打印计数值直到该索引。

以下是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to select a maximum number of
// elements in array whose sum is at most K
int maxSelections(int A[], int n, int k)
{
    // Sort the array
    sort(A, A + n);

    // Calculate the sum and count while
    // iterating the sorted array
    int sum = 0;
    int count = 0;

    // Iterate for all the
    // elements in the array
    for (int i = 0; i < n; i++) {

        // Add the current element to sum
        sum = sum + A[i];

        if (sum > k) {
            break;
        }

        // Increment the count
        count++;
    }
    // Return the answer
    return count;
}

// Driver Code
int main()
{
    // Given array
    int A[] = { 3, 7, 2, 9, 4 };

    // Given sum k
    int k = 15;
    int n = sizeof(A) / sizeof(A[0]);

    // Function Call
    cout << maxSelections(A, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to select a maximum number of
// elements in array whose sum is at most K
static int maxSelections(int A[], int n, int k)
{

    // Sort the array
    Arrays.sort(A);

    // Calculate the sum and count while
    // iterating the sorted array
    int sum = 0;
    int count = 0;

    // Iterate for all the
    // elements in the array
    for(int i = 0; i < n; i++)
    {

        // Add the current element to sum
        sum = sum + A[i];

        if (sum > k)
        {
            break;
        }

        // Increment the count
        count++;
    }

    // Return the answer
    return count;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int A[] = { 3, 7, 2, 9, 4 };

    // Given sum k
    int k = 15;
    int n = A.length;

    // Function call
    System.out.print(maxSelections(A, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to select a maximum
# number of elements in array
# whose sum is at most K
def maxSelections(A, n, k):

  # Sort the array
  A.sort();

  # Calculate the sum and
  # count while iterating
  # the sorted array
  sum = 0;
  count = 0;

  # Iterate for all the
  # elements in the array
  for i in range(n):

    # Add the current element to sum
    sum = sum + A[i];

    if (sum > k):
      break;

      # Increment the count
      count += 1;

      # Return the answer
      return count;

# Driver Code
if __name__ == '__main__':

  # Given array
  A = [3, 7, 2, 9, 4];

  # Given sum k
  k = 15;
  n = len(A);

  # Function call
  print(maxSelections(A, n, k));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to select a maximum number of
// elements in array whose sum is at most K
static int maxSelections(int[] A, int n, int k)
{

    // Sort the array
    Array.Sort(A);

    // Calculate the sum and count while
    // iterating the sorted array
    int sum = 0;
    int count = 0;

    // Iterate for all the
    // elements in the array
    for(int i = 0; i < n; i++)
    {

        // Add the current element to sum
        sum = sum + A[i];

        if (sum > k)
        {
            break;
        }

        // Increment the count
        count++;
    }

    // Return the answer
    return count;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int[] A = { 3, 7, 2, 9, 4 };

    // Given sum k
    int k = 15;
    int n = A.Length;

    // Function call
    Console.Write(maxSelections(A, n, k));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to select a maximum number of
// elements in array whose sum is at most K
function maxSelections( A, n, k)
{
    // Sort the array
    A.sort();

    // Calculate the sum and count while
    // iterating the sorted array
    let sum = 0;
    let count = 0;

    // Iterate for all the
    // elements in the array
    for (let i = 0; i < n; i++) {

        // Add the current element to sum
        sum = sum + A[i];

        if (sum > k) {
            break;
        }

        // Increment the count
        count++;
    }
    // Return the answer
    return count;
}

// Driver Code

// Given array
let A = [ 3, 7, 2, 9, 4 ];

// Given sum k
let k = 15;
let n = A.length;

// Function Call
document.write(maxSelections(A, n, k));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*
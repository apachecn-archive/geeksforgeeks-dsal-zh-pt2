# 大小为 K 的子阵列中出现的完全数的最大数量

> 原文:[https://www . geeksforgeeks . org/最大数目的完美数字-出现在 k 大小的子阵列中/](https://www.geeksforgeeks.org/maximum-number-of-perfect-numbers-present-in-a-subarray-of-size-k/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，任务是确定任意大小的子数组 **K** 中[个完全数](https://www.geeksforgeeks.org/perfect-number/)的最大数量。

**示例:**

> **输入:** arr[ ] = {28，2，3，6，496，99，8128，24}，K = 4
> **输出:** 3
> **说明:**子阵{6，496，99，8128}有 3 个最大的完全数。
> 
> **输入:** arr[ ]= {1，2，3，6}，K = 2
> T3】输出: 1

**天真方法:**该方法是[生成所有可能的大小为 **K** 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，计算作为[完全数](https://www.geeksforgeeks.org/perfect-number/)的元素数量。打印任何子阵列获得的最大计数。

**时间复杂度**:*T3】O(N * K)
T5】辅助空间: O(1)*

**高效方法:**
要优化上述方法，请将给定数组 **arr[ ]** 转换为**二进制数组**，其中第 i <sup>个</sup>元素是 **1** ，如果它是[完全数](https://www.geeksforgeeks.org/perfect-number/)。否则，第 I<sup>元素为 **0** 。因此，问题简化为使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)在二进制数组中找到大小为 **K** 的[最大和子数组。按照以下步骤解决问题:](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)</sup>

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于数组**arr【】**的每个元素，检查它是否是[完全数](https://www.geeksforgeeks.org/perfect-number/)。
2.  如果 **arr[i]** 是[完全数](https://www.geeksforgeeks.org/perfect-number/)，那么将 **arr[i]** 转换为等于 **1。**否则，将 **arr[i]** 转换为等于 **0** 。
3.  到[检查一个数是否是完全数](https://www.geeksforgeeks.org/php-check-number-perfect-number/):
    1.  初始化一个变量**和**来存储除数的[和。](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)
    2.  遍历范围**【1，arr[I]–1】**中的每个数字，检查它是否是 **arr[i]** 的除数。把所有除数加起来。
    3.  如果所有除数之和等于**arr【I】**，那么这个数就是一个**完全数**。否则，该号码不是**完全数**。
4.  计算修改后阵列中第一个子阵列尺寸 **K** 的总和。
5.  使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)，从所有可能的子阵列大小 **K** 中找到子阵列的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check a number
// is Perfect Number or not
int isPerfect(int N)
{
    // Stores sum of divisors
    int sum = 1;

    // Find all divisors and add them
    for (int i = 2; i < sqrt(N); i++)
    {

        if (N % i == 0) {

            if (i == N / i)
            {

                sum += i;
            }
            else
            {

                sum += i + N / i;
            }
        }
    }

    // If sum of divisors
    // is equal to N
    if (sum == N && N != 1)
        return 1;

    return 0;
}

// Function to return maximum
// sum of a subarray of size K
int maxSum(int arr[], int N, int K)
{
    // If k is greater than N
    if (N < K)
    {

        cout << "Invalid";
        return -1;
    }

    // Compute sum of first window of size K
    int res = 0;
    for (int i = 0; i < K; i++)
    {

        res += arr[i];
    }

    // Compute sums of remaining windows by
    // removing first element of previous
    // window and adding last element of
    // current window
    int curr_sum = res;
    for (int i = K; i < N; i++)
    {

        curr_sum += arr[i] - arr[i - K];
        res = max(res, curr_sum);
    }

    // return the answer
    return res;
}

// Function to find all the
// perfect numbers in the array
int max_PerfectNumbers(int arr[], int N, int K)
{
    // The given array is converted into binary array
    for (int i = 0; i < N; i++)
    {

        arr[i] = isPerfect(arr[i]) ? 1 : 0;
    }

    return maxSum(arr, N, K);
}

// Driver Code
int main()
{
    int arr[] = { 28, 2, 3, 6, 496, 99, 8128, 24 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << max_PerfectNumbers(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to check a number
// is Perfect Number or not
static int isPerfect(int N)
{
  // Stores sum of divisors
  int sum = 1;

  // Find all divisors and
  // add them
  for (int i = 2;
           i < Math.sqrt(N); i++)
  {
    if (N % i == 0)
    {
      if (i == N / i)
      {
        sum += i;
      }
      else
      {
        sum += i + N / i;
      }
    }
  }

  // If sum of divisors
  // is equal to N
  if (sum == N && N != 1)
    return 1;

  return 0;
}

// Function to return maximum
// sum of a subarray of size K
static int maxSum(int arr[],
                  int N, int K)
{
  // If k is greater than N
  if (N < K)
  {
    System.out.print("Invalid");
    return -1;
  }

  // Compute sum of first
  // window of size K
  int res = 0;

  for (int i = 0; i < K; i++)
  {
    res += arr[i];
  }

  // Compute sums of remaining windows by
  // removing first element of previous
  // window and adding last element of
  // current window
  int curr_sum = res;

  for (int i = K; i < N; i++)
  {
    curr_sum += arr[i] - arr[i - K];
    res = Math.max(res, curr_sum);
  }

  // return the answer
  return res;
}

// Function to find all the
// perfect numbers in the array
static int max_PerfectNumbers(int arr[],
                              int N, int K)
{
  // The given array is converted
  // into binary array
  for (int i = 0; i < N; i++)
  {
    arr[i] = isPerfect(arr[i]) ==
             1 ? 1 : 0;
  }

  return maxSum(arr, N, K);
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {28, 2, 3, 6, 496,
               99, 8128, 24};
  int K = 4;
  int N = arr.length;
  System.out.print(max_PerfectNumbers(arr,
                                      N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check a number
# is Perfect Number or not
def isPerfect(N):

    # Stores sum of divisors
    sum = 1

    # Find all divisors and add them
    for i in range(2, N):
        if i * i > N:
            break

        if (N % i == 0):
            if (i == N // i):
                sum += i
            else:
                sum += i + N // i

    # If sum of divisors
    # is equal to N
    if (sum == N and N != 1):
        return 1

    return 0

# Function to return maximum
# sum of a subarray of size K
def maxSum(arr, N, K):

    # If k is greater than N
    if (N < K):
        print("Invalid")
        return -1

    # Compute sum of first
    # window of size K
    res = 0

    for i in range(K):
        res += arr[i]

    # Compute sums of remaining windows by
    # removing first element of previous
    # window and adding last element of
    # current window
    curr_sum = res

    for i in range(K, N):
        curr_sum += arr[i] - arr[i - K]
        res = max(res, curr_sum)

    # print(res)

    # Return the answer
    return res

# Function to find all the
# perfect numbers in the array
def max_PerfectNumbers(arr, N, K):

    # The given array is converted
    # into binary array
    for i in range(N):
        if isPerfect(arr[i]):
            arr[i] = 1
        else:
            arr[i] = 0

    return maxSum(arr, N, K)

# Driver Code
if __name__ == '__main__':

    arr = [ 28, 2, 3, 6,
            496, 99, 8128, 24 ]
    K = 4
    N = len(arr)

    print(max_PerfectNumbers(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to check a number
// is Perfect Number or not
static int isPerfect(int N)
{
  // Stores sum of divisors
  int sum = 1;

  // Find all divisors and
  // add them
  for (int i = 2;
           i < Math.Sqrt(N); i++)
  {
    if (N % i == 0)
    {
      if (i == N / i)
      {
        sum += i;
      }
      else
      {
        sum += i + N / i;
      }
    }
  }

  // If sum of divisors
  // is equal to N
  if (sum == N && N != 1)
    return 1;

  return 0;
}

// Function to return maximum
// sum of a subarray of size K
static int maxSum(int []arr,
                  int N, int K)
{
  // If k is greater than N
  if (N < K)
  {
    Console.Write("Invalid");
    return -1;
  }

  // Compute sum of first
  // window of size K
  int res = 0;

  for (int i = 0; i < K; i++)
  {
    res += arr[i];
  }

  // Compute sums of remaining
  // windows by removing first
  // element of previous window
  // and adding last element of
  // current window
  int curr_sum = res;

  for (int i = K; i < N; i++)
  {
    curr_sum += arr[i] - arr[i - K];
    res = Math.Max(res, curr_sum);
  }

  // return the answer
  return res;
}

// Function to find all the
// perfect numbers in the array
static int max_PerfectNumbers(int []arr,
                              int N, int K)
{
  // The given array is converted
  // into binary array
  for (int i = 0; i < N; i++)
  {
    arr[i] = isPerfect(arr[i]) ==
             1 ? 1 : 0;
  }

  return maxSum(arr, N, K);
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {28, 2, 3, 6, 496,
               99, 8128, 24};
  int K = 4;
  int N = arr.Length;
  Console.Write(max_PerfectNumbers(arr,
                                   N, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check a number
// is Perfect Number or not
function isPerfect(N)
{

    // Stores sum of divisors
    let sum = 1;

    // Find all divisors and
    // add them
    for(let i = 2;
            i < Math.sqrt(N); i++)
    {
        if (N % i == 0)
        {
            if (i == N / i)
            {
                sum += i;
            }
            else
            {
                sum += i + N / i;
            }
        }
    }

    // If sum of divisors
    // is equal to N
    if (sum == N && N != 1)
        return 1;

    return 0;
}

// Function to return maximum
// sum of a subarray of size K
function maxSum(arr, N, K)
{

    // If k is greater than N
    if (N < K)
    {
        document.write("Invalid");
        return -1;
    }

    // Compute sum of first
    // window of size K
    let res = 0;

    for(let i = 0; i < K; i++)
    {
        res += arr[i];
    }

    // Compute sums of remaining windows by
    // removing first element of previous
    // window and adding last element of
    // current window
    let curr_sum = res;

    for(let i = K; i < N; i++)
    {
        curr_sum += arr[i] - arr[i - K];
        res = Math.max(res, curr_sum);
    }

    // Return the answer
    return res;
}

// Function to find all the
// perfect numbers in the array
function max_PerfectNumbers(arr, N, K)
{

    // The given array is converted
    // into binary array
    for(let i = 0; i < N; i++)
    {
        arr[i] = isPerfect(arr[i]) ==
                  1 ? 1 : 0;
    }
    return maxSum(arr, N, K);
}

// Driver Code
let arr = [ 28, 2, 3, 6, 496,
            99, 8128, 24 ];
let K = 4;
let N = arr.length;

document.write(max_PerfectNumbers(arr, N, K));

// This code is contributed by target_2   

</script>
```

**输出:**

```
3
```

**时间复杂度:** O( N * sqrt(N) )
**辅助空间:** O(1)
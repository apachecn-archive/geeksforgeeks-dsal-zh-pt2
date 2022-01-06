# 将数组元素的个数除以 2，使至少 K 个元素相等

> 原文:[https://www . geeksforgeeks . org/要被 2 除以使至少 k 个元素相等的数组元素计数/](https://www.geeksforgeeks.org/count-of-array-elements-to-be-divided-by-2-to-make-at-least-k-elements-equal/)

给定一个大小为 **N** 的整数数组 **arr[]** ，任务是找到需要除以 2 的最小数组元素数，使数组中至少 **K** 个元素相等。
**例:**

> **输入:** arr[] = {1，2，2，4，5}，N = 5，K = 3
> **输出:** 1
> **解释:**
> 将 4 除以 2 将数组修改为具有 3 个相等元素的{1，2，2，2，5}。
> **输入:** arr[] = {1，2，3，4，5}，N = 5，K = 3
> **输出:** 1
> **解释:**
> 2 和 3 除以 2 将数组修改为具有 3 个相等元素的{1，1，1，4，5}。

**逼近:**
每一个整数 **X** 可以除以 2 **log <sub>2</sub> (X)** 次得到一个非零值。因此，我们需要对每个数组元素 arr[i]执行这些 **log <sub>2</sub> (arr[i])** 运算，对于除法后获得的每个值，存储达到相应值所需的运算次数。一旦对所有数组元素执行了所有操作，对于至少 **K** 个数组元素在某一点上已经减少到的每个值，找到所有这些元素中所需的最小 **K** 个操作的总和。在所有这样的实例中找到所需的最小操作数。

> **图解:**
> arr[] = {1，2，2，4，5}，N = 5，K = 3
> 只有 1 个元素可以有值 5，所以忽略。
> 只有 1 个元素可以有值 4，所以忽略。
> 任何元素都不能有值 3。
> 4 个元素可以有值 2。
> {1，2，2，(4/2)，(5/2) } - > {1，2，2，2，2}
> 既然，可能性数超过 K，求最小 K 次运算的和。
> arr[1]—>0 运算
> arr[2]—>0 运算
> arr[3]—>1 运算
> arr[4]—>1 运算
> 因此，最小的 3 个运算之和= (0 + 0 + 1) = 1
> 所有 5 个元素都可以简化为 1。
> {1，2/2，2/2，(4/2)/2，(5/2)/2} - > {1，1，1，1，1}
> 因此，最小的 3 个运算之和= (0 + 1 + 1) = 2
> 因此，使至少 K 个元素相等所需的最小运算数为 1。

按照以下步骤使用上述方法解决问题:

1.  创建一个矩阵**val[][]**，这样**val[X][j]**将存储从数组元素中获取值 **X** 所需的操作数。
2.  遍历数组，对于每个数组元素:
    *   初始化 x = arr[i]。初始化操作计数**将**设为 0。
    *   每一步，更新 **x = x/2** 和**增量 cur 1**。将**曲线**插入 val【x】中，作为获得 **x** 当前值所需的分割数。
3.  现在，所有可能的值都存储在 **vals[][]** 矩阵中，这些值可以通过重复将每个 arr[i]除以 2 并加上获得该值所需的除法次数来获得。
4.  现在，遍历矩阵**val[][]**，并对每一行执行以下操作:
    *   检查当前行**val[I]**是否至少包含 **K** 元素。如果**val[I]<K**，则忽略，因为至少有 K 个数组元素不能简化为 **i** 。
    *   如果**val[I]。size()** 为 **≥ K** ，计算排 **i** 之和。更新 **ans = min(ans，val[I]之和)**。
5.  **和**的最终值给了我们想要的答案。

以下是上述方法的实现:

## C++

```
// C++ program to make atleast
// K elements of the given array
// equal by dividing by 2

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// minimum number of divisions
// required
int get_min_opration(int arr[], int N,
                     int K)
{
    vector<vector<int> > vals(200001);
    for (int i = 0; i < N; ++i) {
        int x = arr[i];

        int cur = 0;
        while (x > 0) {
            // cur: number of
            // times a[i] is
            // divided by 2
            // to obtain x
            vals[x].push_back(cur);
            x /= 2;
            ++cur;
        }
    }

    int ans = INT_MAX;
    for (int i = 0; i <= 200000; ++i) {
        // To obtain minimum
        // number of operations
        sort(vals[i].begin(),
             vals[i].end());
    }
    for (int i = 0; i <= 200000; ++i) {

        // If it is not possible
        // to make at least K
        // elements equal to vals[i]
        if (int(vals[i].size()) < K)
            continue;
        // Store the number
        // of operations
        int sum = 0;
        for (int j = 0; j < K; j++) {
            sum += vals[i][j];
        }
        // Update the minimum
        // number of operations
        // required
        ans = min(ans, sum);
    }

    return ans;
}
// Driver Program
int main()
{
    int N = 5, K = 3;

    int arr[] = { 1, 2, 2, 4, 5 };
    cout << get_min_opration(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make atleast
// K elements of the given array
// equal by dividing by 2
import java.util.*;
class GFG{

// Function to return the
// minimum number of divisions
// required
static int get_min_opration(int arr[],
                            int N, int K)
{
  Vector<Integer> []vals = new Vector[200001];

  for (int i = 0; i < vals.length; i++)
    vals[i] = new Vector<Integer>();

  for (int i = 0; i < N; ++i)
  {
    int x = arr[i];
    int cur = 0;

    while (x > 0)
    {
      // cur: number of
      // times a[i] is
      // divided by 2
      // to obtain x
      vals[x].add(cur);
      x /= 2;
      ++cur;
    }
  }

  int ans = Integer.MAX_VALUE;

  for (int i = 0; i <= 200000; ++i)
  {
    // To obtain minimum
    // number of operations
    Collections.sort(vals[i]);
  }

  for (int i = 0; i <= 200000; ++i)
  {
    // If it is not possible
    // to make at least K
    // elements equal to vals[i]
    if ((vals[i].size()) < K)
      continue;

    // Store the number
    // of operations
    int sum = 0;

    for (int j = 0; j < K; j++)
    {
      sum += vals[i].get(j);
    }

    // Update the minimum
    // number of operations
    // required
    ans = Math.min(ans, sum);
  }

  return ans;
}

// Driver code
public static void main(String[] args)
{
  int N = 5, K = 3;
  int arr[] = {1, 2, 2, 4, 5};
  System.out.print(get_min_opration(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to make atleast
# K elements of the given array
# equal by dividing by 2
import sys

# Function to return the
# minimum number of divisions
# required
def get_min_opration(arr, N, K):

    vals = [[] for _ in range(200001)]
    for i in range(N):
        x = arr[i]

        cur = 0
        while (x > 0):

            # cur: number of times a[i]
            # is divided by 2 to obtain x
            vals[x].append(cur)
            x //= 2
            cur += 1

    ans = sys.maxsize
    for i in range(200001):

        # To obtain minimum
        # number of operations
        vals[i] = sorted(vals[i])

    for i in range(200001):

        # If it is not possible
        # to make at least K
        # elements equal to vals[i]
        if (int(len(vals[i])) < K):
            continue

        # Store the number
        # of operations
        sum = 0
        for j in range(K):
            sum += vals[i][j]

        # Update the minimum
        # number of operations
        # required
        ans = min(ans, sum)

    return ans

# Driver code
if __name__ == '__main__':

    N = 5
    K = 3
    arr = [ 1, 2, 2, 4, 5 ]

    print(get_min_opration(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to make atleast
// K elements of the given array
// equal by dividing by 2
using System;
using System.Collections.Generic;
class GFG{

// Function to return the
// minimum number of divisions
// required
static int get_min_opration(int []arr,
                            int N, int K)
{
  List<int> []vals =
              new List<int>[200001];

  for (int i = 0; i < vals.Length; i++)
    vals[i] = new List<int>();

  for (int i = 0; i < N; ++i)
  {
    int x = arr[i];
    int cur = 0;

    while (x > 0)
    {
      // cur: number of
      // times a[i] is
      // divided by 2
      // to obtain x
      vals[x].Add(cur);
      x /= 2;
      ++cur;
    }
  }

  int ans = int.MaxValue;

  for (int i = 0; i <= 200000; ++i)
  {
    // If it is not possible
    // to make at least K
    // elements equal to vals[i]
    if ((vals[i].Count) < K)
      continue;

    // Store the number
    // of operations
    int sum = 0;

    for (int j = 0; j < K; j++)
    {
      sum += vals[i][j];
    }

    // Update the minimum
    // number of operations
    // required
    ans = Math.Min(ans, sum);
  }

  return ans;
}

// Driver code
public static void Main(String[] args)
{
  int N = 5, K = 3;
  int []arr = {1, 2, 2, 4, 5};
  Console.Write(get_min_opration(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

      // JavaScript program to make atleast
      // K elements of the given array
      // equal by dividing by 2

      // Function to return the
      // minimum number of divisions
      // required
      function get_min_opration(arr, N, K) {
        var vals = new Array(200001);

        for (var i = 0; i < vals.length; i++) vals[i] = [];

        for (var i = 0; i < N; ++i) {
          var x = arr[i];
          var cur = 0;

          while (x > 0) {
            // cur: number of
            // times a[i] is
            // divided by 2
            // to obtain x
            vals[x].push(cur);
            x = parseInt(x / 2);
            ++cur;
          }
        }

        //Max integer value
        var ans = 2147483648;

        for (var i = 0; i <= 200000; ++i) {
          // If it is not possible
          // to make at least K
          // elements equal to vals[i]
          if (vals[i].length < K) continue;

          // Store the number
          // of operations
          var sum = 0;

          for (var j = 0; j < K; j++) {
            sum += vals[i][j];
          }

          // Update the minimum
          // number of operations
          // required
          ans = Math.min(ans, sum);
        }

        return ans;
      }

      // Driver code
      var N = 5,
        K = 3;
      var arr = [1, 2, 2, 4, 5];
      document.write(get_min_opration(arr, N, K));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O (N * log N)*
***辅助空间:** O (N * log N)*
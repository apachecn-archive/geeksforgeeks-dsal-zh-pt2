# 去除谷值后给定数组的和最大化

> 原文:[https://www . geeksforgeeks . org/最大化移除谷值后给定数组的总和/](https://www.geeksforgeeks.org/maximize-sum-of-given-array-after-removing-valleys/)

给定一个大小为 **N、**的整数数组 **arr[]** ，当只允许减少一个元素的值时，任务是在从数组中移除谷之后最大化数组的和，即新形成的数组不应该包含任何在修改之后具有更大值的元素。

> **谷值** :-如果 **arr[i] > arr[j]** 和 **arr[ k ] > arr[ j ]** ，则**指数 j** 被视为谷值点，因为( **i < j < k** )。

**示例**:

> **输入** : arr[] = { 5，10，15 }
> **输出** : 30
> **说明**:由于阵中不包含**任何谷，**所以不需要减少任何元素。
> 
> **输入** : arr[] = { 8，1，10，1，8 }
> **输出** : 14
> **说明:**new_arr =>【1，1，10，1，1】和 sum = 14，new _ arr 也可以构造为【8，1，1，1，1，1】，但和会少一些。

**天真法**:将每个元素视为一个峰元素，在峰元素的两个方向上按降序开始。

> 如果 arr = [8，1，10，1，8 ]
> 将 10 视为峰值元素，那么最终的数组将是[ 1，1，10，1，1]

***时间复杂度***:O(N<sup>2</sup>)
***辅助空间*** : O(1)

**高效方法**:不要把每个指标作为一个峰值点。计算每个索引(idx)的**前缀和后缀和数组**。前缀数组可用于存储从 **0 开始的**高度总和**。。。满足左侧无谷条件的 idx** ， **idx** 有峰元素。后缀和数组也满足索引 **idx** 后缀的相同条件。

假设当前元素是最高的元素，索引处的元素可以向左移动，直到找到更小的元素。使用堆栈概念的[下一个更小的元素可以在这里使用，只需稍加修改。](https://www.geeksforgeeks.org/next-smaller-element/)

遵循以下步骤:

*   构建前缀和**(左)**、后缀和**(右)**数组。构建数组时会有两种情况。考虑以下前缀和数组的情况。同样也适用于后缀和数组。
    1.  目前的元素是迄今为止所有元素中最小的。
        所以，**左[ curr_idx ] = ( i +1 ) * arr[i]** 。这里(i + 1)表示范围。
    2.  左侧有一个较小的元素 **small_idx** 。
        所以，**左[ curr_idx] =左[small _ idx]+(current _ idx–small _ idx)* arr[I]**T5【使用**相同的方法右和数组**可以计算出来。
*   现在，遍历每个索引并计算答案=左[idx] +右[idx]–arr[idx]

**注:**减去 arr[ idx ]，因为在**左[]** 以及**右[]** 数组中增加了 arr[idx]。

为了更好地理解，请参见下图。

> 插图:
> 
> 考虑示例 **arr[]** = { 5，1，8 }
> 在构建前缀和数组
> 时**索引= 0:** 左侧没有元素【0】= 5。
> **Index = 1:** 1 是从左至右所有中最小的。所以，左[1] = 1 * 2 = 2。
> **索引= 2:** 8 在索引 1 处有较小的元素 1。所以 left[2]= left[1]+8 *(2–1)= 2+8 = 10。
> 所以左[] = {5，2，10}。类似地右[] = {7，2，8}。
> 现在，在遍历计算答案时，索引 0、1 和 2 的值分别为(5+7–5)、(2+2–1)、(10+8–8)。其中最大值为 10。所以答案是 10。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get get the maximum cost
int solve(vector<int>& arr)
{
  int n = arr.size();
  vector<int> left(n, 0);
  vector<int> right(n, 0);
  vector<int> stack;

  // Calculate left array
  for (int i = 0; i < n; i++) {
    int curr = arr[i];
    while (stack.size() != 0
           && arr[stack[stack.size() - 1]] >= curr) {
      stack.pop_back();
    }
    // Case 1
    if (stack.size() == 0)
      left[i] = (i + 1) * (arr[i]);

    // Case 2
    else {
      int small_idx = stack[stack.size() - 1];
      left[i] = left[small_idx]
        + (i - small_idx) * (arr[i]);
    }
    stack.push_back(i);
  }
  stack.clear();

  // Calculate suffix sum array
  for (int i = n - 1; i > -1; i--) {
    int curr = arr[i];
    while (stack.size() != 0
           && arr[stack[stack.size() - 1]] >= curr) {
      stack.pop_back();
    }

    if (stack.size() == 0)
      right[i] = (n - i) * (arr[i]);

    else {
      int small_idx = stack[stack.size() - 1];
      right[i] = right[small_idx]
        + (small_idx - i) * (arr[i]);
    }
    stack.push_back(i);
  }
  int ans = 0;

  for (int i = 0; i < n; i++) {
    int curr = left[i] + right[i] - arr[i];
    ans = max(ans, curr);
  }
  return (ans);
}

// Driver code
int main()
{
  vector<int> arr = { 5, 1, 8 };
  cout << solve(arr);

  return 0;
}

// This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;
class GFG{

// Function to get get the maximum cost
static int solve(int[] arr)
{
  int n = arr.length;
  int []left = new int[n];
  int []right = new int[n];
  Vector<Integer> stack = new Vector<Integer>();

  // Calculate left array
  for (int i = 0; i < n; i++) {
    int curr = arr[i];
    while (stack.size() != 0
           && arr[stack.get(stack.size() - 1)] >= curr) {
      stack.remove(stack.size() - 1);
    }
    // Case 1
    if (stack.size() == 0)
      left[i] = (i + 1) * (arr[i]);

    // Case 2
    else {
      int small_idx = stack.get(stack.size() - 1);
      left[i] = left[small_idx]
        + (i - small_idx) * (arr[i]);
    }
    stack.add(i);
  }
  stack.clear();

  // Calculate suffix sum array
  for (int i = n - 1; i > -1; i--) {
    int curr = arr[i];
    while (stack.size() != 0
           && arr[stack.get(stack.size() - 1)] >= curr) {
        stack.remove(stack.size() - 1);
    }

    if (stack.size() == 0)
      right[i] = (n - i) * (arr[i]);

    else {
      int small_idx = stack.get(stack.size() - 1);
      right[i] = right[small_idx]
        + (small_idx - i) * (arr[i]);
    }
    stack.add(i);
  }
  int ans = 0;

  for (int i = 0; i < n; i++) {
    int curr = left[i] + right[i] - arr[i];
    ans = Math.max(ans, curr);
  }
  return (ans);
}

// Driver code
public static void main(String[] args)
{
  int[] arr = { 5, 1, 8 };
  System.out.print(solve(arr));

}
}

// This code is contributed by 29AjayKumar.
```

## 蟒蛇 3

```
# Python code to implement above approach

# Function to get get the maximum cost
def solve(arr):
    n = len(arr)
    left = [0]*(n)
    right = [0]*(n)
    stack = []

    # Calculate left array
    for i in range(n):
        curr = arr[i]
        while(stack and
              arr[stack[-1]] >= curr):
            stack.pop()

        # Case 1
        if (len(stack) == 0):
            left[i] = (i + 1)*(arr[i])

        # Case 2
        else:
            small_idx = stack[-1]
            left[i] = left[small_idx] \
                     + (i - small_idx)*(arr[i])
        stack.append(i)

    stack.clear()

    # Calculate suffix sum array
    for i in range(n-1, -1, -1):
        curr = arr[i]
        while(stack and
              arr[stack[-1]] >= curr):
            stack.pop()

        if (len(stack) == 0):
            right[i] = (n-i)*(arr[i])

        else:
            small_idx = stack[-1]
            right[i] = right[small_idx] \
                     + (small_idx - i)*(arr[i])

        stack.append(i)

    ans = 0

    for i in range(n):
        curr = left[i] + right[i] - arr[i]
        ans = max(ans, curr)

    return (ans)

# Driver code
if __name__ == "__main__":
    arr = [5, 1, 8]
    print(solve(arr))
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to get get the maximum cost
  static int solve(int[] arr)
  {
    int n = arr.Length;
    int[] left = new int[n];
    int[] right = new int[n];
    List<int> stack = new List<int>();

    // Calculate left array
    for (int i = 0; i < n; i++) {
      int curr = arr[i];
      while (stack.Count != 0
             && arr[stack[stack.Count - 1]] >= curr) {
        stack.RemoveAt(stack.Count - 1);
      }

      // Case 1
      if (stack.Count == 0)
        left[i] = (i + 1) * (arr[i]);

      // Case 2
      else {
        int small_idx = stack[stack.Count - 1];
        left[i] = left[small_idx]
          + (i - small_idx) * (arr[i]);
      }
      stack.Add(i);
    }
    stack.Clear();

    // Calculate suffix sum array
    for (int i = n - 1; i > -1; i--) {
      int curr = arr[i];
      while (stack.Count != 0
             && arr[stack[stack.Count - 1]] >= curr) {
        stack.RemoveAt(stack.Count - 1);
      }

      if (stack.Count == 0)
        right[i] = (n - i) * (arr[i]);

      else {
        int small_idx = stack[stack.Count - 1];
        right[i] = right[small_idx]
          + (small_idx - i) * (arr[i]);
      }
      stack.Add(i);
    }
    int ans = 0;

    for (int i = 0; i < n; i++) {
      int curr = left[i] + right[i] - arr[i];
      ans = Math.Max(ans, curr);
    }
    return (ans);
  }

  // Driver code
  public static void Main(string[] args)
  {
    int[] arr = { 5, 1, 8 };
    Console.WriteLine(solve(arr));
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach

        // Function to get get the maximum cost
        function solve(arr) {
            let n = arr.length
            let left = new Array(n).fill(0)
            let right = new Array(n).fill(0)
            let stack = []

            // Calculate left array
            for (let i = 0; i < n; i++) {
                curr = arr[i]
                while (stack.length != 0 &&
                    arr[stack[stack.length - 1]] >= curr) {
                    stack.pop()
                }
                // Case 1
                if (stack.length == 0)
                    left[i] = (i + 1) * (arr[i])

                // Case 2
                else {
                    small_idx = stack[stack.length - 1]
                    left[i] = left[small_idx]
                        + (i - small_idx) * (arr[i])
                }
                stack.push(i)
            }
            stack = []

            // Calculate suffix sum array
            for (let i = n - 1; i > -1; i--) {
                curr = arr[i]
                while (stack.length != 0 &&
                    arr[stack[stack.length - 1]] >= curr) {
                    stack.pop()
                }

                if (stack.length == 0)
                    right[i] = (n - i) * (arr[i])

                else {
                    small_idx = stack[stack.length - 1]
                    right[i] = right[small_idx]
                        + (small_idx - i) * (arr[i])
                }
                stack.push(i)
            }
            ans = 0

            for (let i = 0; i < n; i++) {
                curr = left[i] + right[i] - arr[i]
                ans = Math.max(ans, curr)
            }
            return (ans)
        }

        // Driver code
        arr = [5, 1, 8]
        document.write(solve(arr))

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
10
```

***时间复杂度*** : O(N)
***辅助空间*** : O(N)
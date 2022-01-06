# 增加最多 K 个元素后，将数组和最大化，然后将数组除以 X

> 原文:[https://www . geesforgeks . org/maximize-array-sum-递增后最多 k 个元素-后跟除以-array-x/](https://www.geeksforgeeks.org/maximize-array-sum-after-incrementing-at-most-k-elements-followed-by-dividing-array-by-x/)

给定一个[数组](https://www.geeksforgeeks.org/array-class-c/)， **arr[]** 和两个整数， **K** 和 **X，**的任务是最多在任何元素的 **K** 增量之后最大化数组元素的总和，然后将所有元素除以 **X**

**示例:**

> **输入:** arr = {16，15，17}，K = 8，X = 10
> **输出:** 5
> **说明:**最多允许 8 个增量。因此，将索引 0 处的元素增加 4，索引 2 处的元素增加 3。因此修改后的数组变成{20/10，15/10，20/10} = {2，1，2}，因此总和为 2+1+2 = 5
> 
> **输入:** arr = {8，13，2，4，7}，K = 6，X = 5
> **输出:** 7

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。这个想法是[通过调整](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)[比较器](https://www.geeksforgeeks.org/comparator-interface-java/)对数组进行排序，使得最不需要增量就能被 **X** 整除的元素首先被遇到。按照以下步骤解决问题:

*   [按照先遇到被 **X** 除后余数较大的元素的顺序，对数组列表](https://www.geeksforgeeks.org/how-to-sort-arraylist-using-comparator/)进行排序
*   [迭代数组列表](https://www.geeksforgeeks.org/iterating-arraylists-java/)，每次迭代:
    *   找到剩余值 **rem** 添加到**arr【I】，**中，使其成为 **X** 的倍数
        *   如果 **K <雷姆，**那么打破这个循环
        *   否则用 **rem** 增加**arr【I】**，用 **rem** 减少 **K**
*   将变量**和**初始化为 0
*   [遍历数组列表](https://www.geeksforgeeks.org/traverse-through-arraylist-in-forward-direction-in-java/)并在每次迭代时:
    *   将**加到**和**上**

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;
int x = 5;
static bool cmp(int a, int b) { return (b % x) < (a % x); }

int maxSumIncDiv(vector<int> nums, int k)
{

    // Sort in such a way that the
    // numbers needing least increment
    // to become multiple of x are
    // encountered first
    sort(nums.begin(), nums.end(), cmp);
    // Iterate the ArrayList
    for (int i = 0; i < nums.size(); i++) {

        int rem = nums[i] % x;

        // Find the value to increment
        // current element such that it
        // becomes a multiple of x
        rem = x - rem;

        // Incrementing any element with
        // the remaining value of k will
        // have no effect
        if (k < rem) {

            break;
        }
        else {

            // Increment element so that
            // it becomes multiple of x
            nums[i] = nums[i] + rem;

            // Decrement k by the
            // remaining value
            k -= rem;
        }
    }

    // Initialize sum
    int sum = 0;

    // Traverse the ArrayList
    for (int i = 0; i < nums.size(); i++) {

        // calculate sum of elements
        // divided by x
        sum += nums[i] / x;
    }

    // Return the answer
    return sum;
}

int main()
{

    // Initializing list of nums
    vector<int> nums = { 8, 13, 2, 4, 7 };

    int K = 6;

    // Call the function and
    // print the answer
    cout << (maxSumIncDiv(nums, K));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.util.*;
import java.io.*;

class GFG {
    public static int maxSumIncDiv(
        List<Integer> nums, int k, int x)
    {

        // Sort in such a way that the
        // numbers needing least increment
        // to become multiple of x are
        // encountered first
        Collections.sort(
            nums,
            (a, b) -> b % x - a % x);

        // Iterate the ArrayList
        for (int i = 0; i < nums.size(); i++) {

            int rem = nums.get(i) % x;

            // Find the value to increment
            // current element such that it
            // becomes a multiple of x
            rem = x - rem;

            // Incrementing any element with
            // the remaining value of k will
            // have no effect
            if (k < rem) {

                break;
            }
            else {

                // Increment element so that
                // it becomes multiple of x
                nums.set(i, nums.get(i) + rem);

                // Decrement k by the
                // remaining value
                k -= rem;
            }
        }

        // Initialize sum
        int sum = 0;

        // Traverse the ArrayList
        for (int i = 0; i < nums.size(); i++) {

            // calculate sum of elements
            // divided by x
            sum += nums.get(i) / x;
        }

        // Return the answer
        return sum;
    }
    public static void main(String[] args)
    {

        // Initializing list of nums
        List<Integer> nums = new ArrayList<>();

        int K = 6, X = 5;
        nums.add(8);
        nums.add(13);
        nums.add(2);
        nums.add(4);
        nums.add(7);

        // Call the function and
        // print the answer
        System.out.println(
            maxSumIncDiv(nums, K, X));
    }
}
```

## 蟒蛇 3

```
# Python implementation for the above approach
import math

def maxSumIncDiv(nums, k, x):

  # Sort in such a way that the
  # numbers needing least increment
  # to become multiple of x are
  # encountered first
  nums.sort();

  # Iterate the ArrayList
  for i in range(len(nums)):

      rem = nums[i] % x;

      # Find the value to increment
      # current element such that it
      # becomes a multiple of x
      rem = x - rem;

      # Incrementing any element with
      # the remaining value of k will
      # have no effect
      if (k < rem):
        break;
      else:

        # Increment element so that
        # it becomes multiple of x
        nums[i] = nums[i] + rem;

        # Decrement k by the
        # remaining value
        k -= rem;

  # Initialize sum
  sum = 0;

  # Traverse the ArrayList
  for i in range(len(nums)):

    # calculate sum of elements
    # divided by x
    sum += nums[i] / x;

  # Return the answer
  return math.floor(sum)

# Initializing list of nums
nums = [];
K = 6
X = 5
nums.append(8);
nums.append(13);
nums.append(2);
nums.append(4);
nums.append(7);

# Call the function and
# print the answer
print(maxSumIncDiv(nums, K, X));

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{
    public static int maxSumIncDiv(
        List<int> nums, int k, int x)
    {

        // Sort in such a way that the
        // numbers needing least increment
        // to become multiple of x are
        // encountered first
        nums.Sort((a, b) => b % x - a % x);

        // Iterate the ArrayList
        for (int i = 0; i < nums.Count; i++) {

            int rem = nums[i] % x;

            // Find the value to increment
            // current element such that it
            // becomes a multiple of x
            rem = x - rem;

            // Incrementing any element with
            // the remaining value of k will
            // have no effect
            if (k < rem) {

                break;
            }
            else {

                // Increment element so that
                // it becomes multiple of x
                nums[i] = nums[i] + rem;

                // Decrement k by the
                // remaining value
                k -= rem;
            }
        }

        // Initialize sum
        int sum = 0;

        // Traverse the ArrayList
        for (int i = 0; i < nums.Count; i++) {

            // calculate sum of elements
            // divided by x
            sum += nums[i] / x;
        }

        // Return the answer
        return (sum);
    }

// Driver Code
public static void Main(String[] args)
{

    // Initializing list of nums
        List<int> nums = new List<int>();

        int K = 6, X = 5;
        nums.Add(8);
        nums.Add(13);
        nums.Add(2);
        nums.Add(4);
        nums.Add(7);

        // Call the function and
        // print the answer
        Console.Write(
            maxSumIncDiv(nums, K, X));
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript implementation for the above approach

function maxSumIncDiv(nums, k, x)
    {

        // Sort in such a way that the
        // numbers needing least increment
        // to become multiple of x are
        // encountered first
        nums.sort((a, b) => b % x - a % x);

        // Iterate the ArrayList
        for (var i = 0; i < nums.length; i++) {

            var rem = nums[i] % x;

            // Find the value to increment
            // current element such that it
            // becomes a multiple of x
            rem = x - rem;

            // Incrementing any element with
            // the remaining value of k will
            // have no effect
            if (k < rem) {

                break;
            }
            else {

                // Increment element so that
                // it becomes multiple of x
                nums[i] = nums[i] + rem;

                // Decrement k by the
                // remaining value
                k -= rem;
            }
        }

        // Initialize sum
        var sum = 0;

        // Traverse the ArrayList
        for (var i = 0; i < nums.length; i++) {

            // calculate sum of elements
            // divided by x
            sum += nums[i] / x;
        }

        // Return the answer
        return parseInt(sum);
    }

// Initializing list of nums
var nums = [];
var K = 6, X = 5;
nums.push(8);
nums.push(13);
nums.push(2);
nums.push(4);
nums.push(7);
// Call the function and
// print the answer
document.write(
    maxSumIncDiv(nums, K, X));

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
7
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(N)
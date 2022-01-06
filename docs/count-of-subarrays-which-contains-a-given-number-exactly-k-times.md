# 包含给定数目的子阵列的计数精确到 K 倍

> 原文:[https://www . geeksforgeeks . org/subarrays-count-其中包含给定的精确 k 次次数/](https://www.geeksforgeeks.org/count-of-subarrays-which-contains-a-given-number-exactly-k-times/)

给定一个由从 1 到 N 的重复值组成的 N 个元素的数组 **A[]** ，任务是找出包含给定数量**数**的子数组的总数正好是 **K** 次。

**示例:**

> **输入:** A[] = {1，2，1，5，1}，num = 1，K = 2
> **输出:** 2
> **解释:**
> 子阵{1，2，1，5}，{1，2，1}，{2，1，5，1}和{1，5，1}恰好包含 1 两次。
> 
> **输入:** A[] = {1，5，3，5，7，5，6，5，10，5，12，5}，num = 5，K = 3
> **输出:** 14

**天真方法:**一个简单的解决方法是生成给定数组的所有子数组，并计算给定个数恰好出现 K 次的子数组个数。

**时间复杂度:** *O(N <sup>2</sup> )* 其中 N 是给定数组的大小。

**有效方法:**

*   存储包含给定编号**编号**的**索引**。
*   遍历**索引[]** 数组，计算每个 **K** 索引可能的子数组数量。
*   **数**的任何 **K** 指数的可能子阵列数等于

> (i <sup>第</sup>指数–(I-1)<sup>第</sup>指数)和((i + K) <sup>第</sup>指数–(I+(K-1)】<sup>第</sup>指数)
> 的乘积

*   所有这些子阵列的计数给出了给定阵列中所有可能的子阵列的计数。

下面是上述方法的实现:

## C++

```
// C++ program to count subarrays
// which contains a given number
// exactly K times

#include <bits/stdc++.h>
using namespace std;

// Function to return
// the count of subarrays
// which contains given
// number exactly K times
int countSubarrays(int A[], int num,
                   int K, int size)
{
    // Store the indices
    // containing num
    vector<int> indices;
    for (int i = 0; i < size; i++) {
        if (A[i] == num)
            indices.push_back(i);
    }

    // If the occurrence of num
    // in the entire array
    // is less than K
    if (indices.size() < K)

        // No such subarrays are possible
        return 0;

    // Store the previous
    // index of num
    int prev = -1;

    // Store the count of
    // total subarrays
    int ans = 0;

    // Store the count of
    // subarrays for current
    // K occurrences
    int ctr = 0;

    for (int i = 0;
         i <= indices.size() - K;
         i++) {

        ctr = indices[i] - prev;

        if (i < indices.size() - K) {

            ctr *= (indices[i + K]
                    - indices[i + K - 1]);
        }
        else {
            ctr *= ((size - 1)
                    - indices[i + K - 1] + 1);
        }

        ans += ctr;
        prev = indices[i];
    }

    return ans;
}

// Driver code
int main()
{
    int A[] = { 1, 5, 3, 5, 7, 5, 6,
                5, 10, 5, 12, 5 };

    int num = 5;

    int K = 3;

    int size = sizeof(A) / sizeof(int);

    cout << countSubarrays(A, num, K, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subarrays
// which contains a given number
// exactly K times

import java.util.*;
public class Main {

    // Function to return
    // the count of subarrays
    // which contains given
    // number exactly K times
    public static int countSubarrays(
        int A[], int num,
        int K, int size)
    {
        // Store the indices
        // containing num
        ArrayList<Integer> indices
            = new ArrayList<Integer>();

        for (int i = 0; i < size; i++) {
            if (A[i] == num) {
                indices.add(i);
            }
        }

        if (indices.size() < K) {
            return 0;
        }

        // Store the previous
        // index of num
        int prev = -1;

        // Store the count of
        // total subarrays
        int ans = 0;

        // Store the count of
        // subarrays for current
        // K occurrences
        int ctr = 0;

        for (int i = 0;
             i <= indices.size() - K;
             i++) {

            ctr = indices.get(i) - prev;

            if (i < indices.size() - K) {

                ctr *= (indices.get(i + K)
                        - indices.get(i + K - 1));
            }
            else {
                ctr *= ((size - 1)
                        - indices.get(i + K - 1) + 1);
            }

            ans += ctr;
            prev = indices.get(i);
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {

        int A[] = { 1, 5, 3, 5, 7, 5,
                    6, 5, 10, 5, 12, 5 };

        int num = 5;

        int K = 3;

        int size = A.length;

        System.out.println(
            countSubarrays(A, num, K, size));
    }
}
```

## 蟒蛇 3

```
# Python3 program to
# count subarrays which
# contains a given number
# exactly K times

# Function to return
# the count of subarrays
# which contains given
# number exactly K times
def countSubarrays(A, num,
                   K, size):
  # Store the indices
  # containing num
  indices = []
  for i in range (size):
    if (A[i] == num):
      indices.append(i)

  # If the occurrence of num
  # in the entire array
  # is less than K
  if (len(indices) < K):

    # No such subarrays are possible
    return 0

  # Store the previous
  # index of num
  prev = -1

  # Store the count of
  # total subarrays
  ans = 0

  # Store the count of
  # subarrays for current
  # K occurrences
  ctr = 0

  for i in range (len(indices) - K + 1):
    ctr = indices[i] - prev
    if (i < len(indices) - K):
      ctr *= (indices[i + K] -
              indices[i + K - 1])       
    else:
      ctr *= ((size - 1) -
               indices[i + K - 1] + 1)
    ans += ctr
    prev = indices[i]
  return ans

# Driver code
if __name__ == "__main__":
  A = [1, 5, 3, 5, 7, 5,
       6, 5, 10, 5, 12, 5]
  num = 5
  K = 3
  size = len(A)
  print(countSubarrays(A, num, K, size))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to count subarrays
// which contains a given number
// exactly K times
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to return the count of subarrays
// which contains given number exactly K times
public static int countSubarrays(int[] A, int num,
                                 int K, int size)
{

    // Store the indices
    // containing num
    ArrayList indices = new ArrayList();

    for(int i = 0; i < size; i++)
    {
        if (A[i] == num)
        {
            indices.Add(i);
        }
    }

    if (indices.Count < K)
    {
        return 0;
    }

    // Store the previous
    // index of num
    int prev = -1;

    // Store the count of
    // total subarrays
    int ans = 0;

    // Store the count of
    // subarrays for current
    // K occurrences
    int ctr = 0;

    for(int i = 0;
            i <= indices.Count - K;
            i++)
    {
        ctr = (int)indices[i] - prev;
        if (i < indices.Count - K)
        {
            ctr *= ((int)indices[i + K] -
                    (int)indices[i + K - 1]);
        }
        else
        {
            ctr *= ((size - 1) -
                    (int)indices[i + K - 1] + 1);
        }
        ans += ctr;
        prev = (int)indices[i];
    }
    return ans;
}

// Driver code
static public void Main()
{
    int[] A = { 1, 5, 3, 5, 7, 5,
                6, 5, 10, 5, 12, 5 };

    int num = 5;
    int K = 3;
    int size = A.Length;

    Console.WriteLine(countSubarrays(A, num, K, size));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program to count subarrays
// which contains a given number
// exactly K times

// Function to return the count of subarrays
// which contains given number exactly K times
function countSubarrays(A, num, K, size)
{

    // Store the indices
    // containing num
    let indices = [];

    for(let i = 0; i < size; i++)
    {
        if (A[i] == num)
        {
            indices.push(i);
        }
    }

    if (indices.length < K)
    {
        return 0;
    }

    // Store the previous
    // index of num
    let prev = -1;

    // Store the count of
    // total subarrays
    let ans = 0;

    // Store the count of
    // subarrays for current
    // K occurrences
    let ctr = 0;

    for(let i = 0;
            i <= indices.length - K;
            i++)
    {
        ctr = indices[i] - prev;
        if (i < indices.length - K)
        {
            ctr *= (indices[i + K] -
                    indices[i + K - 1]);
        }
        else
        {
            ctr *= ((size - 1) -
                    indices[i + K - 1] + 1);
        }
        ans += ctr;
        prev = indices[i];
    }
    return ans;
}

  // Driver Code

    let A = [ 1, 5, 3, 5, 7, 5,
                6, 5, 10, 5, 12, 5 ];

    let num = 5;
    let K = 3;
    let size = A.length;

    document.write(countSubarrays(A, num, K, size));

</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(N)* ，其中 N 是数组的大小。
***空间复杂度:** O(N)*
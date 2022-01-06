# 从范围[1，M]的给定数组中找出 K 个缺失的数字，使得总平均值为 X

> 原文:[https://www . geesforgeks . org/find-k-从给定数组中缺失数字-范围-1-m-这样-总平均值为-x/](https://www.geeksforgeeks.org/find-k-missing-numbers-from-given-array-in-range-1-m-such-that-total-average-is-x/)

给定大小为 **N** 的整数数组 **arr[]** ，其中每个元素可以在范围**【1，M】**和两个整数 **X** 和 **K** 内。任务是在**【1，M】**范围内找到 **K** 个可能的数字，使得所有(N + K)个数字的平均值等于 x，如果有多个有效答案，任何一个都可以接受。

**示例:**

> **输入:** arr[] = {3，2，4，3}，M = 6，K = 2，X = 4
> **输出:** 6 6
> **说明:**所有元素的平均值为(3 + 2 + 4 + 3 + 6 + 6) / 6 = 4。
> 
> **输入:** arr[] = {1}，M = 8，K = 1，X = 4
> **输出:** 7
> **说明:**所有元素的平均值为(1 + 7) / 2 = 4。
> 
> **输入:** arr[] = {1，2，3，4}，M = 6，K = 4，X = 6
> **输出:** []
> **解释:**无论缺失的 4 个元素是什么，平均值都不可能是 6。

**进场:**进场基于以下数学观察。如果相加 M 个元素后的总期望和使得相加的 M 个元素的和需要小于 M 或大于 K*M，则不可能有解。否则，总有一个可能的解决办法。

1.  求缺失元素的**和** (Y)，即= X *(K+N)–和(arr)。
2.  如果**小于 K** 或**大于 K*M** ，则无法创建数组。所以返回一个空数组。
3.  否则，尽量在 K 个元素中等分 Y 值，即给所有 K 个元素赋 Y/K 值。
4.  如果还有一些值需要分配，那么在平均分配每个元素之后，剩下的值将是= (Y%K)。所以给新数组的(Y%K)个元素加 1。

下面是上述方法的实现:

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the missing elements
vector<int> missing(vector<int>& arr,
                    int M, int X, int K)
{
    int N = arr.size(),
        sum = accumulate(arr.begin(),
                         arr.end(), 0),
        newsum = 0;
    newsum = X * (K + N) - sum;
    // If this newsum is less than M
    // or greater than K*M then
    // no array can be created.
    if (newsum < K || newsum > K * M)
        return {};

    int mod = newsum % K;
    vector<int> ans(K, newsum / K);
    for (int i = 0; i < mod; i++)
        ans[i] += 1;
    return ans;
}

// Driver code
int main()
{
    vector<int> arr{ 3, 2, 4, 3 };
    int X = 4;
    int K = 2;
    int M = 6;

    // Vector to store resultant list
    vector<int> ans = missing(arr, M, X, K);

    for (auto i : ans)
        cout << i << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
class GFG{

// Function to get the missing elements
static  int []missing(int []arr,
                    int M, int X, int K)
{
    int N = arr.length,
        sum = accumulate(arr,0,N),
        newsum = 0;
    newsum = X * (K + N) - sum;

    // If this newsum is less than M
    // or greater than K*M then
    // no array can be created.
    if (newsum < K || newsum > K * M)
        return new int[]{};

    int mod = newsum % K;
    int []ans = new int[K];
    Arrays.fill(ans, newsum / K);
    for (int i = 0; i < mod; i++)
        ans[i] += 1;
    return ans;
}
static int accumulate(int[] arr, int start, int end){
    int sum=0;
    for(int i= 0; i < arr.length; i++)
        sum+=arr[i];
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int[]arr = { 3, 2, 4, 3 };
    int X = 4;
    int K = 2;
    int M = 6;

    // Vector to store resultant list
    int []ans = missing(arr, M, X, K);

    for (int i : ans)
        System.out.print(i+ " ");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to get the missing elements
def missing(arr, M, X, K):
    N = len(arr)
    sum = 0
    for i in range(len(arr)):
        sum += arr[i]
    newsum = 0
    newsum = X * (K + N) - sum

    # If this newsum is less than M
    # or greater than K*M then
    # no array can be created.
    if (newsum < K or newsum > K * M):
        return []

    mod = newsum % K
    ans = [newsum // K] * K

    for i in range(mod):
        ans[i] += 1
    return ans

# Driver code
arr = [3, 2, 4, 3]
X = 4
K = 2
M = 6

# Vector to store resultant list
ans = missing(arr, M, X, K)

for i in ans:
    print(i, end=" ")

# This code is contributed by gfgking
```

## C#

```
// C# code to implement above approach
using System;

class GFG {

    // Function to get the missing elements
    static int[] missing(int[] arr, int M, int X, int K)
    {
        int N = arr.Length, sum = accumulate(arr, 0, N),
            newsum = 0;
        newsum = X * (K + N) - sum;

        // If this newsum is less than M
        // or greater than K*M then
        // no array can be created.
        if (newsum < K || newsum > K * M)
            return new int[] {};

        int mod = newsum % K;
        int[] ans = new int[K];
        Array.Fill(ans, newsum / K);
        for (int i = 0; i < mod; i++)
            ans[i] += 1;
        return ans;
    }
    static int accumulate(int[] arr, int start, int end)
    {
        int sum = 0;
        for (int i = 0; i < arr.Length; i++)
            sum += arr[i];
        return sum;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] arr = { 3, 2, 4, 3 };
        int X = 4;
        int K = 2;
        int M = 6;

        // Vector to store resultant list
        int[] ans = missing(arr, M, X, K);

        foreach(int i in ans) Console.Write(i + " ");
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
  <script>
      // JavaScript code for the above approach

      // Function to get the missing elements
      function missing(arr,
          M, X, K) {
          let N = arr.length;
          let sum = 0;
          for (let i = 0; i < arr.length; i++) {
              sum += arr[i];
          }
          newsum = 0;
          newsum = X * (K + N) - sum;

          // If this newsum is less than M
          // or greater than K*M then
          // no array can be created.
          if (newsum < K || newsum > K * M)
              return [];

          let mod = newsum % K;

          let ans = new Array(K).fill(Math.floor(newsum / K))

          for (let i = 0; i < mod; i++)
              ans[i] += 1;
          return ans;
      }

      // Driver code
      let arr = [3, 2, 4, 3];
      let X = 4;
      let K = 2;
      let M = 6;

      // Vector to store resultant list
      let ans = missing(arr, M, X, K);

      for (let i of ans)
          document.write(i + " ");

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
6 6 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)当不考虑结果列表的空间时
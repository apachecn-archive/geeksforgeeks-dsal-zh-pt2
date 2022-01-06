# 从矩阵中选择的 K 个元素的最大和

> 原文:[https://www . geesforgeks . org/k 元素最大和-从矩阵中选择/](https://www.geeksforgeeks.org/maximum-sum-of-k-elements-selected-from-a-matrix/)

给定一个正整数 **K** 和一个由整数组成的维度 **N*M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，任务是从给定的矩阵中找到 **K** 元素的最大可能和。

**示例:**

> **输入:** arr[][] = {10，10，100，30}，{80，50，10，50}}，K = 5
> **输出:** 310
> **说明:**
> 从矩阵中选择 K(= 5)个元素作为{100，30，80，50，50}，那么和就是 100 + 30 + 80 + 50 + 50 = 310，这是最大值
> 
> **输入:** arr[][] = {80，80，15，50，20，10}，K = 3
> **输出:** 210

**天真法:**解决问题最简单的方法是[从矩阵中生成**大小为 K** 的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，并从这些子集计算最大可能和。按照以下步骤解决给定的问题:

1.  [在给定矩阵**mat【】**中按降序排列所有数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
2.  初始化一个矩阵， **prefixSum[][]** ，存储给定矩阵每行的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-2d-array/)
3.  定义一个函数，**maximum()**[递归地](https://www.geeksforgeeks.org/recursion/)创建 **K** 元素的所有组合，并使用以下步骤返回最大和:
    *   初始化两个变量，把 **id** 表示为 **0** ，把 **rem** 表示为 **p** ，分别表示需要包含的元素和元素个数。
    *   现在在每个递归调用中执行以下步骤:
        *   遍历**前缀【id】**中的每个元素，递归调用两个[递归调用](https://www.geeksforgeeks.org/recursive-functions/)，包括或不包括当前值。
        *   如果它包含当前元素，则检查下面数组中的所有组合。
        *   最后，它将返回取一个元素后和不取它后的最大重量。
4.  完成上述步骤后，通过功能**maximum()**打印返回值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of K
// elements from the matrix
int maximumSum(vector<vector<int> >& prefixSum,
               int K, int N, int rem, int id)
{
    // Stores the maximum sum of K elements
    int ans = INT_MIN;

    // Base Case
    if (rem == 0)
        return 0;

    if (id >= N || rem < 0)
        return INT_MIN;

    // Iterate over K elements and find
    // the maximum sum
    for (int i = 0; i <= K; i++) {
        ans = max(ans, prefixSum[id][i]
                           + maximumSum(prefixSum, K, N,
                                        rem - i, id + 1));
    }

    // Return the maximum sum obtained
    return ans;
}

// Function to find the maximum sum of K
// element from the given matrix
void findSum(vector<vector<int> >& arr,
             int N, int K, int P)
{

    // Stores the prefix sum of the matrix
    vector<vector<int> > prefixSum(N,
                                   vector<int>(K + 1, 0));

    // Sorting the arrays
    for (int i = 0; i < arr.size(); i++) {
        sort(arr[i].begin(), arr[i].end(),
             greater<int>());
    }

    // Storing prefix sum in matrix prefixSum
    for (int i = 0; i < N; i++) {
        int sum = 0;
        for (int j = 1; j <= K; j++) {
            sum += arr[i][j - 1];
            prefixSum[i][j] = sum;
        }
    }

    // Print the maximum sum
    cout << maximumSum(prefixSum, K, N, P, 0);
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 80, 80 }, { 15, 50 }, { 20, 10 } };
    int N = arr.size();
    int M = arr[0].size();
    int K = 3;

    findSum(arr, N, M, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the maximum sum of K
# elements from the matrix
def maximumSum(prefixSum, K, N, rem, Id):

    # Stores the maximum sum of K elements
    ans = -sys.maxsize

    # Base Case
    if rem == 0:
        return 0

    if Id >= N or rem < 0:
        return -sys.maxsize

    # Iterate over K elements and find
    # the maximum sum
    for i in range(K + 1):
        ans = max(ans, prefixSum[Id][i] + maximumSum(prefixSum, K, N, rem - i, Id + 1))

    # Return the maximum sum obtained
    return ans

# Function to find the maximum sum of K
# element from the given matrix
def findSum(arr, N, K, P):
    # Stores the prefix sum of the matrix
    prefixSum = [[0 for i in range(K + 1)] for j in range(N)]

    # Sorting the arrays
    for i in range(len(arr)):
        arr[i].sort()
        arr[i].reverse()

    # Storing prefix sum in matrix prefixSum
    for i in range(N):
        Sum = 0
        for j in range(1, K + 1):
            Sum += arr[i][j - 1]
            prefixSum[i][j] = Sum

    # Print the maximum sum
    print(maximumSum(prefixSum, K, N, P, 0))

arr = [ [ 80, 80 ], [ 15, 50 ], [ 20, 10 ] ]
N = len(arr)
M = len(arr[0])
K = 3

findSum(arr, N, M, K)

# This code is contributed by rameshtravel07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the maximum sum of K
    // elements from the matrix
    static int maximumSum(int[,] prefixSum, int K, int N, int rem, int id)
    {

      // Stores the maximum sum of K elements
      int ans = Int32.MinValue;

      // Base Case
      if (rem == 0) return 0;

      if (id >= N || rem < 0) return Int32.MinValue;

      // Iterate over K elements and find
      // the maximum sum
      for (int i = 0; i <= K; i++) {
        ans = Math.Max(ans, prefixSum[id,i] + maximumSum(prefixSum, K, N, rem - i, id + 1));
      }

      // Return the maximum sum obtained
      return ans;
    }

    // Function to find the maximum sum of K
    // element from the given matrix
    static void findSum(List<List<int>> arr, int N, int K, int P)
    {

      // Stores the prefix sum of the matrix
      int[,] prefixSum = new int[N,K + 1];
      for(int i = 0; i < N; i++)
      {
        for(int j = 0; j < K + 1; j++)
        {
            prefixSum[i,j] = 0;
        }
      }

      // Sorting the arrays
      for (int i = 0; i < arr.Count; i++) {
        arr[i].Sort();
        arr[i].Reverse();
      }

      // Storing prefix sum in matrix prefixSum
      for (int i = 0; i < N; i++) {
        int sum = 0;
        for (int j = 1; j <= K; j++) {
          sum += arr[i][j - 1];
          prefixSum[i,j] = sum;
        }
      }

      // Print the maximum sum
      Console.Write(maximumSum(prefixSum, K, N, P, 0));
    }

  static void Main() {
    List<List<int>> arr = new List<List<int>>();
    arr.Add(new List<int>(new int[]{80, 80}));
    arr.Add(new List<int>(new int[]{15, 50}));
    arr.Add(new List<int>(new int[]{20, 10}));
    int N = arr.Count;
    int M = arr[0].Count;
    int K = 3;

    findSum(arr, N, M, K);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum sum of K
// elements from the matrix
function maximumSum(prefixSum, K, N, rem, id)
{

  // Stores the maximum sum of K elements
  let ans = Number.MIN_SAFE_INTEGER;

  // Base Case
  if (rem == 0) return 0;

  if (id >= N || rem < 0) return Number.MIN_SAFE_INTEGER;

  // Iterate over K elements and find
  // the maximum sum
  for (let i = 0; i <= K; i++) {
    ans = Math.max(
      ans,
      prefixSum[id][i] + maximumSum(prefixSum, K, N, rem - i, id + 1)
    );
  }

  // Return the maximum sum obtained
  return ans;
}

// Function to find the maximum sum of K
// element from the given matrix
function findSum(arr, N, K, P)
{

  // Stores the prefix sum of the matrix
  let prefixSum = new Array(N).fill(0).map(() => new Array(K + 1).fill(0));

  // Sorting the arrays
  for (let i = 0; i < arr.length; i++) {
    arr[i].sort((a, b) => -a + b);
  }

  // Storing prefix sum in matrix prefixSum
  for (let i = 0; i < N; i++) {
    let sum = 0;
    for (let j = 1; j <= K; j++) {
      sum += arr[i][j - 1];
      prefixSum[i][j] = sum;
    }
  }

  // Print the maximum sum
  document.write(maximumSum(prefixSum, K, N, P, 0));
}

// Driver Code
let arr = [
  [80, 80],
  [15, 50],
  [20, 10],
];
let N = arr.length;
let M = arr[0].length;
let K = 3;

findSum(arr, N, M, K);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
210
```

***时间复杂度:**O(M<sup>N</sup>)*
*T8】辅助空间: O(N*M)*

**有效方法:**上述方法也可以通过将[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)存储在 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)中并使用循环状态的结果来降低时间复杂度来进行优化。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of K
// elements from the matrix
int maximumSum(vector<vector<int> >& prefixSum,
               vector<vector<int> >& dp,
               int K, int N, int rem, int id)
{
    // Stores the maximum sum of K elements
    int ans = INT_MIN;

    // Base Case
    if (rem == 0)
        return 0;

    if (id >= N || rem < 0)
        return INT_MIN;

    if (dp[id][rem] != -1)
        return dp[id][rem];

    // Iterate over K elements and find
    // the maximum sum
    for (int i = 0; i <= K; i++) {
        ans = max(ans, prefixSum[id][i]
                           + maximumSum(prefixSum, dp, K, N,
                                        rem - i, id + 1));
    }

    // Return the maximum sum obtained
    return ans;
}

// Function to find the maximum sum of K
// element from the given matrix
void findSum(vector<vector<int> >& arr,
             int N, int K, int P)
{

    // Stores the prefix sum of the matrix
    vector<vector<int> > prefixSum(N,
                                   vector<int>(K + 1, 0));
    vector<vector<int> > dp(N, vector<int>(P + 1, -1));

    // Sorting the arrays
    for (int i = 0; i < arr.size(); i++) {
        sort(arr[i].begin(), arr[i].end(),
             greater<int>());
    }

    // Storing prefix sum in matrix prefixSum
    for (int i = 0; i < N; i++) {
        int sum = 0;
        for (int j = 1; j <= K; j++) {
            sum += arr[i][j - 1];
            prefixSum[i][j] = sum;
        }
    }

    // Print the maximum sum
    cout << maximumSum(prefixSum, dp, K, N, P, 0);
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 80, 80 }, { 15, 50 }, { 20, 10 } };
    int N = arr.size();
    int M = arr[0].size();
    int K = 3;

    findSum(arr, N, M, K);

    return 0;
}
```

**Output:** 

```
210
```

***时间复杂度:** O(N*M*K)*
***辅助空间:** O(K*N <sup>2</sup> )*

**优化方法:**上述方法也可以通过将所有矩阵元素存储在另一个数组**arr【】**中，然后[按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)并打印前 **K** 个元素的总和作为结果来优化。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of K
// element from the given matrix
void maximumSum(vector<vector<int> >& arr,
                int N, int M, int K)
{

    vector<int> allArr(N * M, 0);

    // Store all matrix elements
    int id = 0;

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < K; j++) {
            allArr[id] = arr[i][j];
            id++;
        }
    }

    // Sort the array
    sort(allArr.begin(), allArr.end(),
         greater<int>());

    // Stores the maximum sum
    int ans = 0;

    // Find the maximum sum
    for (int i = 0; i < K; i++) {
        ans += allArr[i];
    }

    // Print the maximum sum
    cout << ans;
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 80, 80 }, { 15, 50 }, { 20, 10 } };
    int N = arr.size();
    int M = arr[0].size();
    int K = 3;

    maximumSum(arr, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{
    static int[][] arr = { { 80, 80 }, { 15, 50 }, { 20, 10 } };

    // Function to find the maximum sum of K
    // element from the given matrix
    static void maximumSum(int N, int M, int K)
    {

        int[] allArr = new int[N * M];

        // Store all matrix elements
        int id = 0;

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                allArr[id] = arr[i][j];
                id++;
            }
        }

        // Sort the array
        Arrays.sort(allArr);
        for(int i = 0; i < allArr.length/2; i++)
        {
            int temp = allArr[i];
            allArr[i] = allArr[allArr.length -i-1];
            allArr[allArr.length -i-1] = temp;
        }

        // Stores the maximum sum
        int ans = 0;

        // Find the maximum sum
        for (int i = 0; i < K; i++) {
            ans += allArr[i];
        }

        // Print the maximum sum
        System.out.print(ans);
    }

  // Driver code
    public static void main(String[] args) {
        int N = 3;
        int M = 2;
        int K = 3;

        maximumSum(N, M, K);
    }
}

// This code is contributed by decode2207.
```

## 蟒蛇 3

```
# Python3 program for the above approach
arr = [ [ 80, 80 ], [ 15, 50 ], [ 20, 10 ] ]

# Function to find the maximum sum of K
# element from the given matrix
def maximumSum(N, M, K):
    allArr = [0]*(N * M)

    # Store all matrix elements
    Id = 0

    for i in range(N):
        for j in range(M):
            allArr[Id] = arr[i][j]
            Id += 1

    # Sort the array
    allArr.sort()
    allArr.reverse()

    # Stores the maximum sum
    ans = 0

    # Find the maximum sum
    for i in range(K):
        ans += allArr[i]

    # Print the maximum sum
    print(ans)

    # Driver code
N = 3
M = 2
K = 3

maximumSum(N, M, K)

# This code is contributed by suresh07.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static int[,] arr = { { 80, 80 }, { 15, 50 }, { 20, 10 } };

    // Function to find the maximum sum of K
    // element from the given matrix
    static void maximumSum(int N, int M, int K)
    {

        int[] allArr = new int[N * M];

        // Store all matrix elements
        int id = 0;

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                allArr[id] = arr[i,j];
                id++;
            }
        }

        // Sort the array
        Array.Sort(allArr);
        Array.Reverse(allArr);

        // Stores the maximum sum
        int ans = 0;

        // Find the maximum sum
        for (int i = 0; i < K; i++) {
            ans += allArr[i];
        }

        // Print the maximum sum
        Console.Write(ans);
    }

  // Driver code
  static void Main() {
    int N = 3;
    int M = 2;
    int K = 3;

    maximumSum(N, M, K);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach
    let arr = [ [ 80, 80 ], [ 15, 50 ], [ 20, 10 ] ];

    // Function to find the maximum sum of K
    // element from the given matrix
    function maximumSum(N, M, K)
    {

        let allArr = new Array(N * M);
        allArr.fill(0);

        // Store all matrix elements
        let id = 0;

        for (let i = 0; i < N; i++) {
            for (let j = 0; j < M; j++) {
                allArr[id] = arr[i][j];
                id++;
            }
        }

        // Sort the array
        allArr.sort(function(a, b){return a - b});
        allArr.reverse();

        // Stores the maximum sum
        let ans = 0;

        // Find the maximum sum
        for (let i = 0; i < K; i++) {
            ans += allArr[i];
        }

        // Print the maximum sum
        document.write(ans);
    }

    let N = 3;
    let M = 2;
    let K = 3;

    maximumSum(N, M, K);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
210
```

***时间复杂度:**O(N * M * log(N * M))*
***辅助空间:** O(N*M)*
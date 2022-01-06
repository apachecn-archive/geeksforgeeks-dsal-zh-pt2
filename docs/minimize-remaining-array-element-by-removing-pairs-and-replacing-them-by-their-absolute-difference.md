# 通过移除对并用它们的绝对差替换它们来最小化剩余的数组元素

> 原文:[https://www . geeksforgeeks . org/通过移除对并以它们的绝对差替换它们来最小化剩余的数组元素/](https://www.geeksforgeeks.org/minimize-remaining-array-element-by-removing-pairs-and-replacing-them-by-their-absolute-difference/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过重复移除一对数组元素并用它们的绝对差替换它们来最小化剩余的数组元素。

**示例:**

> **输入:** arr[] ={ 2，7，4，1，8，1 }
> **输出:** 1
> **解释:**
> 从 arr[]中移除对(arr[0]，arr[2])并将 ABS(arr[0]–arr[2])插入 arr[]将 arr[]修改为{ 2，7，1，8，1 }。
> 从 arr[]中移除对(arr[1]，arr[3])并将 ABS(arr[1]–arr[3])插入 arr[]将 arr[]修改为{ 2，1，1，1 }。
> 从 arr[]中移除对(arr[0]，arr[1])并将 ABS(arr[0]–arr[1])插入 arr[]将 arr[]修改为{ 1，1，1 }。
> 从 arr[]中移除对(arr[0]，arr[1])会将 arr[]修改为{ 1 }。
> 因此，要求的输出为 1。
> 
> **输入:** arr[] = { 1，1，4，2，2 }
> **输出:** 0

**方法:**基于以下观察，使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决该问题:

> 考虑一个数组 arr[] = { a，b，c，d }。
> 如果 a > b，则移除对(a，b)将 arr[]修改为{ a–b，c，d }
> 如果 c > d，则移除对(c，d)将 arr[]修改为{ a–b，c–d }
> 如果(a–b)>(c–d)，则移除对(a–b，c–d)将 arr[]修改为{(a+d)–(b+c)}
> 根据上述观察， 可以观察到，问题是[将阵列划分为两个子集，它们的子集和](https://www.geeksforgeeks.org/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum/)的差最小。

以下是循环关系:

> min_diff(i，sum)= min(min _ diff(I–1，sum+arr[I–1])，min _ diff(I–1，sum))
> 其中，I:数组元素的索引
> sum:第一个子集的元素之和

按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)，比如说 **dp[][]** ，以存储直到第 I 个<sup>元素可以获得的子集和的最小差。</sup>
*   利用上述递推关系，计算 **dp[N][sum]** 的值。
*   最后，打印 **dp[N][sum]** 的值作为所需的和。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest element
// left in the array by the given operations
int smallestLeft(int arr[], int total,
     int sum, int i, vector<vector<int> > &dp)
{

    // Base Case
    if (i == 0) {
        return abs(total - 2 * sum);
    }

    // If this subproblem
    // has occurred previously
    if (dp[i][sum] != -1)
        return dp[i][sum];

    // Including i-th array element
    // into the first subset
    int X = smallestLeft(arr, total,
        sum + arr[i - 1], i - 1, dp);

    // If i-th array element is not selected               
    int Y = smallestLeft(arr, total,
                    sum, i - 1, dp);

     // Update dp[i][sum]
     return dp[i][sum] = min(X, Y);               
}

// Utility function to find smallest element
// left in the array by the given operations
int UtilSmallestElement(int arr[], int N)
{
    // Stores sum of
    // the array elements
    int total = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update total
        total += arr[i];
    }

    // Stores overlapping
    // subproblems
    vector<vector<int> > dp(N + 1,
          vector<int>(total, -1));

    cout<< smallestLeft(arr, total,
                         0, N, dp);

}

// Driver Code
int main()
{

    int arr[] = { 2, 7, 4, 1, 8, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);
    UtilSmallestElement(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class GFG
{

  // Function to find the smallest element
  // left in the array by the given operations
  static int smallestLeft(int arr[], int total,
                          int sum, int i, int[][] dp)
  {

    // Base Case
    if (i == 0)
    {
      return Math.abs(total - 2 * sum);
    }

    // If this subproblem
    // has occurred previously
    if (dp[i][sum] != -1)
      return dp[i][sum];

    // Including i-th array element
    // into the first subset
    int X = smallestLeft(arr, total,
                         sum + arr[i - 1], i - 1, dp);

    // If i-th array element is not selected               
    int Y = smallestLeft(arr, total,
                         sum, i - 1, dp);

    // Update dp[i][sum]
    return dp[i][sum] = Math.min(X, Y);               
  }

  // Utility function to find smallest element
  // left in the array by the given operations
  static void UtilSmallestElement(int arr[], int N)
  {

    // Stores sum of
    // the array elements
    int total = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Update total
      total += arr[i];
    }

    // Stores overlapping
    // subproblems
    int[][] dp = new int[N + 1][total];
    for(int[] k:dp)
      Arrays.fill(k, -1);  
    System.out.println(smallestLeft(arr, total,
                                    0, N, dp));
  }

  // Driver function
  public static void main (String[] args)
  {
    int arr[] = { 2, 7, 4, 1, 8, 1 };
    int N = arr.length;
    UtilSmallestElement(arr, N);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# function to find the smallest element
# left in the array by the given operations
def smallestLeft( arr, total, sum, i, dp):

    # Base Case
    if (i == 0):
        return abs(total - 2 * sum)

    # If this subproblem
    # has occurred previously
    if (dp[i][sum] != -1):
        return dp[i][sum]

    # Including i-th array element
    # into the first subset
    X = smallestLeft(arr, total, sum + arr[i - 1], i - 1, dp)

    # If i-th array element is not selected               
    Y = smallestLeft(arr, total, sum, i - 1, dp)

    #  Update dp[i][sum]
    dp[i][sum] = min(X, Y)
    return dp[i][sum]

# Utility function to find smallest element
# left in the array by the given operations
def UtilSmallestElement(arr, N):

    # Stores sum of
    # the array elements
    total = 0

    # Traverse the array
    for i in range (0, N):

        # Update total
        total += arr[i]

    # Stores overlapping
    # subproblems
    dp = [[-1 for y in range(total)] for x in range(N+1)]       
    print(smallestLeft(arr, total, 0, N, dp))

# Driver Code
arr = [2, 7, 4, 1, 8, 1 ]
N = len(arr)
UtilSmallestElement(arr, N)

# This code is contributed by amreshkumar3.
```

## C#

```
// C# program for above approach
using System;
public class GFG
{

  // Function to find the smallest element
  // left in the array by the given operations
  static int smallestLeft(int []arr, int total,
                          int sum, int i, int[,] dp)
  {

    // Base Case
    if (i == 0)
    {
      return Math.Abs(total - 2 * sum);
    }

    // If this subproblem
    // has occurred previously
    if (dp[i,sum] != -1)
      return dp[i,sum];

    // Including i-th array element
    // into the first subset
    int X = smallestLeft(arr, total,
                         sum + arr[i - 1], i - 1, dp);

    // If i-th array element is not selected               
    int Y = smallestLeft(arr, total,
                         sum, i - 1, dp);

    // Update dp[i,sum]
    return dp[i,sum] = Math.Min(X, Y);               
  }

  // Utility function to find smallest element
  // left in the array by the given operations
  static void UtilSmallestElement(int []arr, int N)
  {

    // Stores sum of
    // the array elements
    int total = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Update total
      total += arr[i];
    }

    // Stores overlapping
    // subproblems
    int[,] dp = new int[N + 1,total];
    for(int i = 0; i < N + 1; i++)
    {
      for (int j = 0; j < total; j++)
      {
        dp[i, j] = -1;
      }
    }
    Console.WriteLine(smallestLeft(arr, total,
                                   0, N, dp));
  }

  // Driver function
  public static void Main(String[] args)
  {
    int []arr = { 2, 7, 4, 1, 8, 1 };
    int N = arr.Length;
    UtilSmallestElement(arr, N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// javascript program of the above approach

let M = 6;
let N  = 7;

  // Function to find the smallest element
  // left in the array by the given operations
  function smallestLeft(arr, total,
                          sum, i, dp)
  {

    // Base Case
    if (i == 0)
    {
      return Math.abs(total - 2 * sum);
    }

    // If this subproblem
    // has occurred previously
    if (dp[i][sum] != -1)
      return dp[i][sum];

    // Including i-th array element
    // into the first subset
    let X = smallestLeft(arr, total,
                         sum + arr[i - 1], i - 1, dp);

    // If i-th array element is not selected               
    let Y = smallestLeft(arr, total,
                         sum, i - 1, dp);

    // Update dp[i][sum]
    return dp[i][sum] = Math.min(X, Y);               
  }

  // Utility function to find smallest element
  // left in the array by the given operations
  function UtilSmallestElement(arr, N)
  {

    // Stores sum of
    // the array elements
    let total = 0;

    // Traverse the array
    for (let i = 0; i < N; i++)
    {

      // Update total
      total += arr[i];
    }

    // Stores overlapping
    // subproblems
    let dp = new Array(N + 1);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    for (var i = 0; i < dp.length; i++) {
        for (var j = 0; j < dp.length; j++) {
        dp[i][j] = 1;
    }
    } 
    document.write(smallestLeft(arr, total,
                                    0, N, dp));
  }

    // Driver Code
    let arr = [ 2, 7, 4, 1, 8, 1 ];
    let n = arr.length;
    UtilSmallestElement(arr, n);

// This code is contributed by target_2.
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N * sum)，其中 **sum** 为数组元素的和*
***辅助空间:** O(N * sum)*

**空间优化法:**对上述方法进行优化，思路是采用[制表法](https://www.geeksforgeeks.org/tabulation-vs-memoization/)。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说 **dp[]** ，其中 **dp[i]** 检查总和 **i** 是否可以作为给定数组子集的总和获得。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)计算数组元素的[和，并存储在变量中，比如 **totalSum** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   利用上述递推关系，求**(totalSum/2)**的最近值，说 **X** ，这样**DP【X】**为真。
*   最后，打印**(total sum–2 * X)**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimize the remaining
// array element by removing pairs and
// replacing them by their absolute difference
int SmallestElementLeft(int arr[], int N)
{

    // Stores sum of array elements
    int totalSum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update totalSum
        totalSum += arr[i];
    }

    // Stores half of totalSum
    int req = totalSum / 2;

    // dp[i]: True if sum i can be
// obtained as a subset sum
    bool dp[req + 1];

    // Initialize dp[] array
    memset(dp, false, sizeof(dp));

    // Base case          
    dp[0] = true;

    // Stores closest sum that can
    // be obtained as a subset sum
    int reach = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Iterate over all possible value of sum
        for (int j = req; j - arr[i] >= 0; j--) {

            // Update dp[j]
            dp[j] = dp[j] || dp[j - arr[i]];

            // If sum i can be obtained
            // from array elements
            if (dp[j]) {

                // Update reach
                reach = max(reach, j);
            }
        }
    }

    return totalSum - (2 * reach);
}

// Driver Code
int main()
{

    int arr[] = { 2, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout<< SmallestElementLeft(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find minimize the remaining
// array element by removing pairs and
// replacing them by their absolute difference
static int SmallestElementLeft(int arr[], int N)
{

    // Stores sum of array elements
    int totalSum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update totalSum
        totalSum += arr[i];
    }

    // Stores half of totalSum
    int req = totalSum / 2;

    // dp[i]: True if sum i can be
    // obtained as a subset sum
    boolean[] dp = new boolean[req + 1];

    // Initialize dp[] array
    Arrays.fill(dp, false);

    // Base case          
    dp[0] = true;

    // Stores closest sum that can
    // be obtained as a subset sum
    int reach = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Iterate over all possible value of sum
        for(int j = req; j - arr[i] >= 0; j--)
        {

            // Update dp[j]
            dp[j] = dp[j] || dp[j - arr[i]];

            // If sum i can be obtained
            // from array elements
            if (dp[j])
            {

                // Update reach
                reach = Math.max(reach, j);
            }
        }
    }
    return totalSum - (2 * reach);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 2, 2 };
    int N = arr.length;

    System.out.print(SmallestElementLeft(arr, N));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimize the remaining
# array element by removing pairs and
# replacing them by their absolute difference
def SmallestElementLeft(arr, N):

    # Stores sum of array elements
    totalSum = 0

    # Traverse the array
    for i in range(N):

        # Update totalSum
        totalSum += arr[i]

    # Stores half of totalSum
    req = totalSum // 2

    # dp[i]: True if sum i can be
# obtained as a subset sum
    dp = [False for i in range(req + 1)]

    # Initialize dp[] array
    # memset(dp, false, sizeof(dp));

    # Base case
    dp[0] = True

    # Stores closest sum that can
    # be obtained as a subset sum
    reach = 0

    # Traverse the array
    for i in range(N):

        # Iterate over all possible value of sum
        j = req
        while j>=arr[i]:

            # Update dp[j]
            dp[j] = dp[j] or dp[j - arr[i]]

            # If sum i can be obtained
            # from array elements
            if (dp[j]):

                # Update reach
                reach = max(reach, j)
            j -= 1

    return totalSum - (2 * reach)

# Driver Code
if __name__ == '__main__':

    arr = [2, 2, 2]
    N = len(arr)

    print(SmallestElementLeft(arr, N))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System; 
class GFG
{

// Function to find minimize the remaining
// array element by removing pairs and
// replacing them by their absolute difference
static int SmallestElementLeft(int[] arr, int N)
{

    // Stores sum of array elements
    int totalSum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update totalSum
        totalSum += arr[i];
    }

    // Stores half of totalSum
    int req = totalSum / 2;

    // dp[i]: True if sum i can be
    // obtained as a subset sum
    bool[] dp = new bool[req + 1];

    // Initialize dp[] array
    for(int i = 0; i < req + 1; i++)
    {
        dp[i] = false;
    }

    // Base case          
    dp[0] = true;

    // Stores closest sum that can
    // be obtained as a subset sum
    int reach = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Iterate over all possible value of sum
        for(int j = req; j - arr[i] >= 0; j--)
        {

            // Update dp[j]
            dp[j] = dp[j] || dp[j - arr[i]];

            // If sum i can be obtained
            // from array elements
            if (dp[j])
            {

                // Update reach
                reach = Math.Max(reach, j);
            }
        }
    }
    return totalSum - (2 * reach);
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 2, 2 };
    int N = arr.Length;    
    Console.Write(SmallestElementLeft(arr, N));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to find minimize the remaining
    // array element by removing pairs and
    // replacing them by their absolute difference
    function SmallestElementLeft(arr , N)
    {

        // Stores sum of array elements
        var totalSum = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {

            // Update totalSum
            totalSum += arr[i];
        }

        // Stores half of totalSum
        var req = totalSum / 2;

        // dp[i]: True if sum i can be
        // obtained as a subset sum
        var dp =Array(req + 1).fill(false);

        // Base case
        dp[0] = true;

        // Stores closest sum that can
        // be obtained as a subset sum
        var reach = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {

            // Iterate over all possible value of sum
            for (j = req; j - arr[i] >= 0; j--) {

                // Update dp[j]
                dp[j] = dp[j] || dp[j - arr[i]];

                // If sum i can be obtained
                // from array elements
                if (dp[j]) {

                    // Update reach
                    reach = Math.max(reach, j);
                }
            }
        }
        return totalSum - (2 * reach);
    }

    // Driver Code

        var arr = [ 2, 2, 2 ];
        var N = arr.length;

        document.write(SmallestElementLeft(arr, N));

// This code contributed by aashish1995

</script>
```

**输出:**

```
2
```

***时间复杂度:** O(N * sum)，其中 **sum** 为阵元之和*
***辅助空间:** O(sum)*
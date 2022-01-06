# 所有非空子集和的中位数

> 原文:[https://www . geesforgeks . org/所有非空子集和的中位数/](https://www.geeksforgeeks.org/median-of-all-non-empty-subset-sums/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是找到给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的所有可能子集[之和的](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/)[中值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)。

**示例:**

> **输入:** arr = {2，3，3}
> **输出:** 5
> **解释:**
> 给定数组的非空子集为:{ {2}、{3}、{3}、{2，3}、{2，3}、{3，3}、{2，3}、{2，3，3} }。
> 每个子集的可能和为:
> { {2}、{3}、{3}、{5}、{5}、{6}、{8} }
> 因此，每个子集的所有可能和的中值为 5。
> 
> **输入:** arr = {1，2，1 }
> T3】输出: 2

**天真法:**解决这个问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的所有可能子集，并求出每个子集的元素之和。最后，打印所有可能子集和的中间值。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N * 2 <sup>N</sup> )*

**高效方法:**优化上述方法的思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。下面是动态编程状态和基本情况之间的关系:

> DP 状态之间的关系:
> 如果 **j ≥ arr[i]** ，则**DP[I][j]= DP[I–1][j]+DP[I–1][j–arr[I]]**
> 否则，**DP[I][j]= DP[I–1][j]**
> 其中 **dp[i][j]** 表示通过选择 **i 获得 **j** 之和的方式总数**
> 
> **基本情况:** dp[i][0] = 1

按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，说 **DP[][]** 来存储上面提到的 DP 状态。
*   使用上述 dp 状态之间的关系，以自下而上的方式填充所有 **dp[][]** 状态。
*   初始化一个数组，比如 **sumSub[]** 来存储每个子集的所有可能的和。
*   [遍历 **dp[][]** 数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将所有可能子集的[和存储在数组 **sumSub[]** 中。](https://www.geeksforgeeks.org/print-sums-subsets-given-set/)
*   [排序](https://www.geeksforgeeks.org/sorting-algorithms/)**宿子[]** 阵。
*   最后打印 **sumSub[]** 数组的中间元素。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate the median of all 
// possible subsets by given operations
int findMedianOfsubSum(int arr[], int N)
{   

    // Stores sum of elements
    // of arr[]
    int sum=0;

    // Traverse the array arr[]
    for(int i=0; i < N; i++) {

       // Update sum
       sum += arr[i];
    }

    // Sort the array
    sort(arr, arr + N);

    // DP[i][j]: Stores total number of ways
    // to form the sum j by either selecting
    // ith element or not selecting ith item.
    int dp[N][sum+1];

    // Initialize all 
    // the DP states
    memset(dp, 0, sizeof(dp));

    // Base case
    for(int i=0; i < N; i++) {

       // Fill dp[i][0]
       dp[i][0] = 1;
    }

    // Base case
    dp[0][arr[0]] = 1;

    // Fill all the DP states based 
    // on the mentioned DP relation
    for(int i = 1; i < N; i++) {

        for(int j = 1; j <= sum; j++) {

            // If j is greater than
            // or equal to arr[i]
            if(j >= arr[i]) {

                // Update dp[i][j]    
                dp[i][j] = dp[i-1][j] + 
                      dp[i-1][j-arr[i]];
            }
            else {

                // Update dp[i][j]
                dp[i][j] = dp[i-1][j];
            }
        }
    }

    // Stores all possible
    // subset sum
    vector<int> sumSub;

    // Traverse all possible subset sum
    for(int j=1; j <= sum; j++) {

       // Stores count of subsets 
       // whose sum is j
        int M = dp[N - 1][j];

       // Iterate over the range [1, M]
        for(int i = 1; i <= M; i++) {

            // Insert j into sumSub
            sumSub.push_back(j);
        }
    }

    // Stores middle element of sumSub 
    int mid = sumSub[sumSub.size() / 2];

    return mid; 
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findMedianOfsubSum(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to calculate the median of all 
// possible subsets by given operations
static int findMedianOfsubSum(int arr[], int N)
{

    // Stores sum of elements
    // of arr[]
    int sum = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update sum
        sum += arr[i];
    }

    // Sort the array
    Arrays.sort(arr);

    // DP[i][j]: Stores total number of ways
    // to form the sum j by either selecting
    // ith element or not selecting ith item.
    int [][]dp = new int[N][sum + 1];

    // Initialize all 
    // the DP states
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < sum + 1; j++)
            dp[i][j] = 0;
    }

    // Base case
    for(int i = 0; i < N; i++)
    {

        // Fill dp[i][0]
        dp[i][0] = 1;
    }

    // Base case
    dp[0][arr[0]] = 1;

    // Fill all the DP states based 
    // on the mentioned DP relation
    for(int i = 1; i < N; i++)
    {
        for(int j = 1; j <= sum; j++)
        {

            // If j is greater than
            // or equal to arr[i]
            if (j >= arr[i])
            {

                // Update dp[i][j]    
                dp[i][j] = dp[i - 1][j] + 
                           dp[i - 1][j - arr[i]];
            }
            else
            {

                // Update dp[i][j]
                dp[i][j] = dp[i - 1][j];
            }
        }
    }

    // Stores all possible
    // subset sum
    Vector<Integer> sumSub = new Vector<Integer>();

    // Traverse all possible subset sum
    for(int j = 1; j <= sum; j++)
    {

        // Stores count of subsets 
        // whose sum is j
        int M = dp[N - 1][j];

        // Iterate over the range [1, M]
        for(int i = 1; i <= M; i++)
        {

            // Insert j into sumSub
            sumSub.add(j);
        }
    }

    // Stores middle element of sumSub 
    int mid = sumSub.get(sumSub.size() / 2);

    return mid; 
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 2, 3, 3 };
    int N = arr.length;

    System.out.print(findMedianOfsubSum(arr, N));
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach 

# Function to calculate the
# median of all possible subsets
# by given operations
def findMedianOfsubSum(arr, N):

    # Stores sum of elements
    # of arr[]
    sum = 0     

    # Traverse the array arr[]
    for i in range(N):

        # Update sum
        sum += arr[i]     

    # Sort the array
    arr.sort(reverse = False)      

    # DP[i][j]: Stores total number
    # of ways to form the sum j by
    # either selecting ith element
    # or not selecting ith item.
    dp = [[0 for i in range(sum + 1)]
             for j in range(N)]     

    # Base case
    for i in range(N):

        # Fill dp[i][0]
        dp[i][0] = 1     

    # Base case
    dp[0][arr[0]] = 1     

    # Fill all the DP states based 
    # on the mentioned DP relation
    for i in range(1, N, 1):
        for j in range(1, sum + 1, 1):

            # If j is greater than
            # or equal to arr[i]
            if(j >= arr[i]):

                # Update dp[i][j]    
                dp[i][j] = (dp[i - 1][j] +
                            dp[i - 1][j - arr[i]])
            else:

                # Update dp[i][j]
                dp[i][j] = dp[i - 1][j]

    # Stores all possible
    # subset sum
    sumSub = []     

    # Traverse all possible
    # subset sum
    for j in range(1, sum + 1, 1):

        # Stores count of subsets
        # whose sum is j
        M = dp[N - 1][j]         

        # Iterate over the
        # range [1, M]
        for i in range(1, M + 1, 1):

            # Insert j into sumSub
            sumSub.append(j)     

    # Stores middle element
    # of sumSub 
    mid = sumSub[len(sumSub) // 2]

    return mid 

# Driver Code
if __name__ == '__main__':

    arr = [2, 3, 3]
    N = len(arr)
    print(findMedianOfsubSum(arr, N))

# This code is contributed by bgangwar59
```

## C#

```
// C# program to implement
// the above approach 
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate the median of all 
// possible subsets by given operations
static int findMedianOfsubSum(int[] arr, int N)
{

    // Stores sum of elements
    // of arr[]
    int sum = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update sum
        sum += arr[i];
    }

    // Sort the array
    Array.Sort(arr);

    // DP[i][j]: Stores total number of ways
    // to form the sum j by either selecting
    // ith element or not selecting ith item.
    int [,]dp = new int[N, sum + 1];

    // Initialize all 
    // the DP states
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < sum + 1; j++)
            dp[i, j] = 0;
    }

    // Base case
    for(int i = 0; i < N; i++)
    {

        // Fill dp[i][0]
        dp[i, 0] = 1;
    }

    // Base case
    dp[0, arr[0]] = 1;

    // Fill all the DP states based 
    // on the mentioned DP relation
    for(int i = 1; i < N; i++)
    {
        for(int j = 1; j <= sum; j++)
        {

            // If j is greater than
            // or equal to arr[i]
            if (j >= arr[i])
            {

                // Update dp[i][j]    
                dp[i, j] = dp[i - 1, j] + 
                           dp[i - 1, j - arr[i]];
            }
            else
            {

                // Update dp[i][j]
                dp[i, j] = dp[i - 1, j];
            }
        }
    }

    // Stores all possible
    // subset sum
    List<int> sumSub = new List<int>();

    // Traverse all possible subset sum
    for(int j = 1; j <= sum; j++)
    {

        // Stores count of subsets 
        // whose sum is j
        int M = dp[N - 1, j];

        // Iterate over the range [1, M]
        for(int i = 1; i <= M; i++)
        {

            // Insert j into sumSub
            sumSub.Add(j);
        }
    }

    // Stores middle element of sumSub 
    int mid = sumSub[sumSub.Count / 2];

    return mid; 
}

// Driver code
public static void Main()
{
    int[] arr = { 2, 3, 3 };
    int N = arr.Length;

    Console.Write(findMedianOfsubSum(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to calculate the median of all 
// possible subsets by given operations
function findMedianOfsubSum(arr, N)
{

    // Stores sum of elements
    // of arr[]
    var sum = 0;

    // Traverse the array arr[]
    for(var i = 0; i < N; i++)
    {

        // Update sum
        sum += arr[i];
    }

    // Sort the array
    arr.sort((a, b) => a - b)

    // DP[i][j]: Stores total number of ways
    // to form the sum j by either selecting
    // ith element or not selecting ith item.
    var dp = Array.from(
        Array(N), () => Array(sum + 1).fill(0));

    // Base case
    for(var i = 0; i < N; i++)
    {

        // Fill dp[i][0]
        dp[i][0] = 1;
    }

    // Base case
    dp[0][arr[0]] = 1;

    // Fill all the DP states based 
    // on the mentioned DP relation
    for(var i = 1; i < N; i++)
    {
        for(var j = 1; j <= sum; j++)
        {

            // If j is greater than
            // or equal to arr[i]
            if(j >= arr[i])
            {

                // Update dp[i][j]    
                dp[i][j] = dp[i - 1][j] + 
                           dp[i - 1][j - arr[i]];
            }
            else
            {

                // Update dp[i][j]
                dp[i][j] = dp[i - 1][j];
            }
        }
    }

    // Stores all possible
    // subset sum
    var sumSub = [];

    // Traverse all possible subset sum
    for(var j = 1; j <= sum; j++)
    {

        // Stores count of subsets 
        // whose sum is j
        var M = dp[N - 1][j];

        // Iterate over the range [1, M]
        for(var i = 1; i <= M; i++)
        {

            // Insert j into sumSub
            sumSub.push(j);
        }
    }

    // Stores middle element of sumSub 
    var mid = sumSub[parseInt(sumSub.length / 2)];

    return mid; 
}

// Driver Code
var arr = [ 2, 3, 3 ];
var N = arr.length

document.write(findMedianOfsubSum(arr, N));

// This code is contributed by importantly

</script>
```

**Output**

```
5
```
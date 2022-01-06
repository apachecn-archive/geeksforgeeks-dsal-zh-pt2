# 分配给数值连续且不同的数组元素的子序列的最大分数

> 原文:[https://www . geeksforgeeks . org/最大分数分配给数字连续且不同的数组元素的子序列/](https://www.geeksforgeeks.org/maximum-score-assigned-to-a-subsequence-of-numerically-consecutive-and-distinct-array-elements/)

给定大小为 **N** 的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和 **brr[]** ，使得数组 **brr[]** 由与数组 **arr[]** 的相应元素相关联的分数组成。任务是找到数组中数值连续且不同元素的子序列的最大可能分配分数总和 **arr[]** 。
**示例:**

> **输入:** arr[] = {1，2，3，3，3，1}，brr[] = {-1，2，10，20，-10，-9}
> **输出:** 22
> **解释:**
> 数组中的不同值= {1，2，3}
> 分配给每个元素的最大值= {1: -1，2: 2，3: 20}
> 选择 arr[]中索引 2 和 4 处的元素，它们是
> 最高分= 2 + 20 = 22。
> 
> **输入:** arr[] = {1，2，3，2，3，1}，brr[] = {-1，2，10，20，-10，-9}
> **输出:** 32
> **解释:**选择的子序列是{arr[1]，arr[2]，arr[3]} = {2，3，2}

**天真方法:**解决问题最简单的方法就是使用[递归](https://www.geeksforgeeks.org/recursion/)。按照以下步骤解决问题:

1.  [生成给定数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/) **arr[]** ，使得子集具有唯一且连续的元素。
2.  在上述步骤中生成子集时，每个元素都有两种添加到子序列或不添加到子序列的可能性。因此，请遵循以下步骤:
    *   如果当前元素与先前选择的元素相差 1，则将该元素添加到子序列中。
    *   否则，继续下一个元素。
3.  综合考虑以上两种可能性，更新**最大 _ 得分**。
4.  打印数组完全遍历后得到的**max _ score**的最终值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum score
// with unique element in the subset
int maximumSum(int a[], int b[], int n,
               int index, int lastpicked)
{

    // Base Case
    if (index == n)
        return 0;

    int option1 = 0, option2 = 0;

    // Check if the previously picked
    // element differs by 1 from the
    // current element
    if (lastpicked == -1 ||
      a[lastpicked] != a[index])

        // Calculate score by including
        // the current element
        option1 = b[index] + maximumSum(
                             a, b, n,
                             index + 1,
                             index);

    // Calculate score by excluding
    // the current element
    option2 = maximumSum(a, b, n,
                         index + 1,
                         lastpicked);

    // Return maximum of the
    // two possibilities
    return max(option1, option2);
}

// Driver code
int main()
{

    // Given arrays
    int arr[] = { 1, 2, 3, 3, 3, 1 };
    int brr[] = { -1, 2, 10, 20, -10, -9 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << (maximumSum(arr, brr, N, 0, -1));
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find the maximum score
    // with unique element in the subset
    public static int maximumSum(
        int[] a, int[] b, int n, int index,
        int lastpicked)
    {
        // Base Case
        if (index == n)
            return 0;

        int option1 = 0, option2 = 0;

        // Check if the previously picked
        // element differs by 1 from the
        // current element
        if (lastpicked == -1
            || a[lastpicked] != a[index])

            // Calculate score by including
            // the current element
            option1
                = b[index]
                  + maximumSum(a, b, n,
                               index + 1,
                               index);

        // Calculate score by excluding
        // the current element
        option2 = maximumSum(a, b, n,
                             index + 1,
                             lastpicked);

        // Return maximum of the
        // two possibilities
        return Math.max(option1, option2);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given arrays
        int arr[] = { 1, 2, 3, 3, 3, 1 };
        int brr[] = { -1, 2, 10, 20, -10, -9 };

        int N = arr.length;

        // Function Call
        System.out.println(
            maximumSum(arr, brr,
                       N, 0, -1));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum score
# with unique element in the subset
def maximumSum(a, b, n, index, lastpicked):

    # Base Case
    if (index == n):
        return 0

    option1 = 0
    option2 = 0

    # Check if the previously picked
    # element differs by 1 from the
    # current element
    if (lastpicked == -1 or
      a[lastpicked] != a[index]):

        # Calculate score by including
        # the current element
        option1 = b[index] + maximumSum(a, b, n,
                                        index + 1,
                                        index)

    # Calculate score by excluding
    # the current element
    option2 = maximumSum(a, b, n, index + 1,
                         lastpicked)

# Return maximum of the
# two possibilities
    return max(option1, option2)

# Driver Code
if __name__ == '__main__':

    # Given arrays
    arr = [ 1, 2, 3, 3, 3, 1 ]
    brr = [ -1, 2, 10, 20, -10, -9 ]

    N = len(arr)

    # Function call
    print(maximumSum(arr, brr, N, 0, -1))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find the maximum score
// with unique element in the subset
public static int maximumSum(int[] a, int[] b,
                             int n, int index,
                             int lastpicked)
{
  // Base Case
  if (index == n)
    return 0;

  int option1 = 0, option2 = 0;

  // Check if the previously picked
  // element differs by 1 from the
  // current element
  if (lastpicked == -1 ||
      a[lastpicked] != a[index])

    // Calculate score by including
    // the current element
    option1 = b[index] + maximumSum(a, b, n,
                                    index + 1,
                                    index);

  // Calculate score by excluding
  // the current element
  option2 = maximumSum(a, b, n,
                       index + 1,
                       lastpicked);

  // Return maximum of the
  // two possibilities
  return Math.Max(option1, option2);
}   

// Driver Code
public static void Main(String[] args)
{
  // Given arrays
  int []arr = {1, 2, 3, 3, 3, 1};
  int []brr = {-1, 2, 10, 20, -10, -9};

  int N = arr.Length;

  // Function Call
  Console.WriteLine(maximumSum(arr, brr,
                               N, 0, -1));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Function to find the maximum score
    // with unique element in the subset
    function maximumSum(
        a, b, n, index,
        lastpicked)
    {
        // Base Case
        if (index == n)
            return 0;

        let option1 = 0, option2 = 0;

        // Check if the previously picked
        // element differs by 1 from the
        // current element
        if (lastpicked == -1
            || a[lastpicked] != a[index])

            // Calculate score by including
            // the current element
            option1
                = b[index]
                  + maximumSum(a, b, n,
                               index + 1,
                               index);

        // Calculate score by excluding
        // the current element
        option2 = maximumSum(a, b, n,
                             index + 1,
                             lastpicked);

        // Return maximum of the
        // two possibilities
        return Math.max(option1, option2);
    }

// Driver code

        // Given arrays
        let arr = [ 1, 2, 3, 3, 3, 1 ];
        let brr = [ -1, 2, 10, 20, -10, -9 ];

        let N = arr.length;

        // Function Call
        document.write(
            maximumSum(arr, brr,
                       N, 0, -1));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
22
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**由于问题存在[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，因此可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)对上述方法进行优化。以下是步骤:

1.  将**索引**初始化为 **0** ，将**上次选择的**初始化为 **-1** 。
2.  初始化一个 2D 数组，比如说 **dp[][]** 来存储子问题的结果。
3.  **dp[][]** 的状态将是当前索引和最后选择的整数。
4.  计算两个可能选项的得分:
    *   如果最后选取的整数不同于当前整数，请选择当前元素。
    *   跳过当前元素，转到下一个元素。
5.  将当前状态存储为上述两种状态计算值的最大值。
6.  在所有递归调用结束后，打印**DP[index][lastspick+1]**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// score possible
int maximumSum(int a[], int b[], int n,
               int index, int lastpicked,
               vector<vector<int>> dp)
{

    // Base Case
    if (index == n)
        return 0;

    // If previously occurred subproblem
    // occurred
    if (dp[index][lastpicked + 1] != -1)
        return dp[index][lastpicked + 1];

    int option1 = 0, option2 = 0;

    // Check if lastpicked element differs
    // by 1 from the current element
    if (lastpicked == -1 ||
      a[lastpicked] != a[index])
    {

        // Calculate score by including
        // the current element
        option1 = b[index] + maximumSum(a, b, n,
                                        index + 1,
                                        index, dp);
    }

    // Calculate score by excluding
    // the current element
    option2 = maximumSum(a, b, n,
                         index + 1,
                         lastpicked, dp);

    // Return maximum score from
    // the two possibilities
    return dp[index][lastpicked + 1] = max(option1,
                                           option2);
}

// Function to print maximum score
void maximumPoints(int arr[], int brr[], int n)
{
    int index = 0, lastPicked = -1;

    // DP array to store results
    // Initialise dp with -1
    vector<vector<int>> dp(n + 5, vector<int>(n + 5, -1));

    // Function call
    cout << maximumSum(arr, brr, n, index,
                       lastPicked, dp)
         << endl;
}

// Driver code   
int main()
{

    // Given arrays
    int arr[] = { 1, 2, 3, 3, 3, 1 };
    int brr[] = { -1, 2, 10, 20, -10, -9 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    maximumPoints(arr, brr, N);

   return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the maximum
    // score possible
    public static int maximumSum(
        int[] a, int[] b, int n, int index,
        int lastpicked, int[][] dp)
    {
        // Base Case
        if (index == n)
            return 0;

        // If previously occurred subproblem
        // occurred
        if (dp[index][lastpicked + 1] != -1)
            return dp[index][lastpicked + 1];

        int option1 = 0, option2 = 0;

        // Check if lastpicked element differs
        // by 1 from the current element
        if (lastpicked == -1
            || a[lastpicked] != a[index]) {

            // Calculate score by including
            // the current element
            option1 = b[index]
                      + maximumSum(a, b, n,
                                   index + 1,
                                   index, dp);
        }

        // Calculate score by excluding
        // the current element
        option2 = maximumSum(a, b, n,
                             index + 1,
                             lastpicked, dp);

        // Return maximum score from
        // the two possibilities
        return dp[index][lastpicked + 1]
            = Math.max(option1, option2);
    }

    // Function to print maximum score
    public static void maximumPoints(
        int arr[], int brr[], int n)
    {
        int index = 0, lastPicked = -1;

        // DP array to store results
        int dp[][] = new int[n + 5][n + 5];

        // Initialise dp with -1
        for (int i[] : dp)
            Arrays.fill(i, -1);

        // Function call
        System.out.println(
            maximumSum(arr, brr, n,
                       index, lastPicked, dp));
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given arrays
        int arr[] = { 1, 2, 3, 3, 3, 1 };
        int brr[] = { -1, 2, 10, 20, -10, -9 };

        int N = arr.length;

        // Function Call
        maximumPoints(arr, brr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the
# maximum score possible
def maximumSum(a, b, n, index,
               lastpicked, dp):

    # Base Case
    if (index == n):
        return 0

    # If previously occurred
    # subproblem occurred
    if (dp[index][lastpicked + 1] != -1):
        return dp[index][lastpicked + 1]

    option1, option2 = 0, 0

    # Check if lastpicked element differs
    # by 1 from the current element
    if (lastpicked == -1 or
        a[lastpicked] != a[index]):

        # Calculate score by including
        # the current element
        option1 = (b[index] +
                   maximumSum(a, b, n,
                              index + 1,
                              index, dp))

    # Calculate score by excluding
    # the current element
    option2 = maximumSum(a, b, n,
                         index + 1,
                         lastpicked, dp)

    # Return maximum score from
    # the two possibilities
    dp[index][lastpicked + 1] = max(option1,
                                    option2)
    return dp[index][lastpicked + 1]

# Function to print maximum score
def maximumPoints(arr, brr, n):

    index = 0
    lastPicked = -1

    # DP array to store results
    dp =[[ -1 for x in range (n + 5)]
              for y in range (n + 5)]

    # Function call
    print (maximumSum(arr, brr,
                      n, index,
                      lastPicked, dp))

# Driver Code
if __name__ == "__main__":

    # Given arrays
    arr = [1, 2, 3, 3, 3, 1]
    brr = [-1, 2, 10, 20, -10, -9]

    N = len(arr)

    # Function Call
    maximumPoints(arr, brr, N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find the maximum
// score possible
public static int maximumSum(int[] a, int[] b,
                             int n, int index,
                             int lastpicked,
                             int[,] dp)
{
  // Base Case
  if (index == n)
    return 0;

  // If previously occurred
  // subproblem occurred
  if (dp[index, lastpicked + 1] != -1)
    return dp[index, lastpicked + 1];

  int option1 = 0, option2 = 0;

  // Check if lastpicked element differs
  // by 1 from the current element
  if (lastpicked == -1 ||
      a[lastpicked] != a[index])
  {
    // Calculate score by including
    // the current element
    option1 = b[index] + maximumSum(a, b, n,
                                    index + 1,
                                    index, dp);
  }

  // Calculate score by excluding
  // the current element
  option2 = maximumSum(a, b, n,
                       index + 1,
                       lastpicked, dp);

  // Return maximum score from
  // the two possibilities
  return dp[index, lastpicked + 1] =
         Math.Max(option1, option2);
}

// Function to print maximum score
public static void maximumPoints(int []arr,
                                 int []brr,
                                 int n)
{
  int index = 0, lastPicked = -1;

  // DP array to store results
  int [,]dp = new int[n + 5, n + 5];

  // Initialise dp with -1
  for(int i = 0; i < n + 5; i++)
  {
    for (int j = 0; j < n + 5; j++)
    {
      dp[i, j] = -1;
    }
  }
  // Function call
  Console.WriteLine(maximumSum(arr, brr, n,
                               index, lastPicked,
                               dp));
}

// Driver Code
public static void Main(String[] args)
{
  // Given arrays
  int []arr = {1, 2, 3, 3, 3, 1};
  int []brr = {-1, 2, 10, 20, -10, -9};

  int N = arr.Length;

  // Function Call
  maximumPoints(arr, brr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the maximum
    // score possible
    function maximumSum(
        a, b, n, index,
        lastpicked, dp)
    {
        // Base Case
        if (index == n)
            return 0;

        // If previously occurred subproblem
        // occurred
        if (dp[index][lastpicked + 1] != -1)
            return dp[index][lastpicked + 1];

        let option1 = 0, option2 = 0;

        // Check if lastpicked element differs
        // by 1 from the current element
        if (lastpicked == -1
            || a[lastpicked] != a[index]) {

            // Calculate score by including
            // the current element
            option1 = b[index]
                      + maximumSum(a, b, n,
                                   index + 1,
                                   index, dp);
        }

        // Calculate score by excluding
        // the current element
        option2 = maximumSum(a, b, n,
                             index + 1,
                             lastpicked, dp);

        // Return maximum score from
        // the two possibilities
        return dp[index][lastpicked + 1]
            = Math.max(option1, option2);
    }

    // Function to print maximum score
    function maximumPolets(
        arr, brr, n)
    {
        let index = 0, lastPicked = -1;

        // DP array to store results
        let dp = new Array(n + 5);
        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

        // Initialise dp with -1
        for (var i = 0; i < dp.length; i++) {
            for (var j = 0; j < dp.length; j++) {
            dp[i][j] = -1;
        }
        }

        // Function call
        document.write(
            maximumSum(arr, brr, n,
                       index, lastPicked, dp));
    }

// Driver Code

   // Given arrays
        let arr = [ 1, 2, 3, 3, 3, 1 ];
        let brr = [ -1, 2, 10, 20, -10, -9 ];

        let N = arr.length;

        // Function Call
        maximumPolets(arr, brr, N);

</script>
```

**Output:** 

```
22
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*
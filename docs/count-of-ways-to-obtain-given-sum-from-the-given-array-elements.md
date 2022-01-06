# 从给定数组元素获得给定和的方法计数

> 原文:[https://www . geeksforgeeks . org/从给定数组元素中获取给定和的方法计数/](https://www.geeksforgeeks.org/count-of-ways-to-obtain-given-sum-from-the-given-array-elements/)

给定一个由 **N** 非负整数和一个整数 **S** 组成的数组**arr【】**，任务是找出通过*加减*数组元素得到和 **S** 的方法数。

**注意:**所有的数组元素都需要参与和的生成。

**示例:**

> **输入:** arr[] = {1，1，1，1，1}，S = 3
> **输出:** 5
> **解释:**
> 以下是获取 S 之和的可能方法:
> 
> *   -1 + 1 + 1 + 1 + 1 = 3
> *   1 -1 + 1 + 1 + 1 = 3
> *   1 + 1 – 1 + 1 + 1 = 3
> *   1 + 1 + 1 – 1 + 1 = 3
> *   1 + 1 + 1 + 1 – 1 = 3
> 
> **输入:** arr[] = {1，2，3，4，5}，S = 3
> **输出:** 3
> **解释:**
> 以下是获取 S 之和的可能方法:
> 
> *   -1 -2 -3 + 4 + 5 = 3
> *   -1 + 2 + 3 + 4 – 5 = 3
> *   1 – 2 + 3 – 4 + 5 = 3

[**递归**](https://www.geeksforgeeks.org/recursion/) **逼近:**可以观察到，每个数组元素可以相加，也可以相减得到和。因此，对于每个数组元素，递归检查两种可能性，并在到达数组末尾后获得总和 **S** 时增加**计数**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count the number of ways
int dfs(int nums[], int S, int curr_sum,
        int index, int n)
{

    // Base Case: Reached the
    // end of the array
    if (index == n)
    {

        // Sum is equal to the
        // required sum
        if (S == curr_sum)
            return 1;
        else
            return 0;
    }

    // Recursively check if required sum
    // can be obtained by adding current
    // element or by subtracting the
    // current index element
    return dfs(nums, S, curr_sum + nums[index],
               index + 1, n) +
           dfs(nums, S, curr_sum - nums[index],
               index + 1, n);
}

// Function to call dfs() to
// calculate the number of ways
int findWays(int nums[], int S, int n)
{
    return dfs(nums, S, 0, 0, n);
}

// Driver Code
int main()
{
    int S = 3;
    int arr[] = { 1, 2, 3, 4, 5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    int answer = findWays(arr, S, n);

    cout << (answer);
    return 0;
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;

class GFG {

    // Function to call dfs() to
    // calculate the number of ways
    static int findWays(int[] nums, int S)
    {
        return dfs(nums, S, 0, 0);
    }

    // Function to count the number of ways
    static int dfs(int[] nums, int S,
                   int curr_sum, int index)
    {
        // Base Case: Reached the
        // end of the array
        if (index == nums.length) {

            // Sum is equal to the
            // required sum
            if (S == curr_sum)
                return 1;
            else
                return 0;
        }

        // Recursively check if required sum
        // can be obtained by adding current
        // element or by subtracting the
        // current index element
        return dfs(nums, S, curr_sum + nums[index],
                   index + 1)
            + dfs(nums, S, curr_sum - nums[index],
                  index + 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int S = 3;
        int[] arr = new int[] { 1, 2, 3, 4, 5 };
        int answer = findWays(arr, S);
        System.out.println(answer);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the number of ways
def dfs(nums, S, curr_sum, index):

    # Base Case: Reached the
    # end of the array
    if (index == len(nums)):

        # Sum is equal to the
        # required sum
        if (S == curr_sum):
            return 1;
        else:
            return 0;

    # Recursively check if required sum
    # can be obtained by adding current
    # element or by subtracting the
    # current index element
    return (dfs(nums, S, curr_sum + nums[index],
                            index + 1) +
            dfs(nums, S, curr_sum - nums[index],
                            index + 1));

# Function to call dfs() to
# calculate the number of ways
def findWays(nums, S):

    return dfs(nums, S, 0, 0);

# Driver Code
if __name__ == '__main__':

    S = 3;
    arr = [1, 2, 3, 4, 5];
    answer = findWays(arr, S);

    print(answer);

# This code is contributed by amal kumar choubey
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{
// Function to call dfs() to
  // calculate the number of ways
  static int findWays(int[] nums, int S)
  {
    return dfs(nums, S, 0, 0);
  }

  // Function to count the number of ways
  static int dfs(int[] nums, int S,
                 int curr_sum, int index)
  {
    // Base Case: Reached the
    // end of the array
    if (index == nums.Length)
    {

      // Sum is equal to the
      // required sum
      if (S == curr_sum)
        return 1;
      else
        return 0;
    }

    // Recursively check if required sum
    // can be obtained by adding current
    // element or by subtracting the
    // current index element
    return dfs(nums, S, curr_sum +
               nums[index], index + 1) +
             dfs(nums, S, curr_sum -
               nums[index], index + 1);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int S = 3;
    int[] arr = new int[] { 1, 2, 3, 4, 5 };
    int answer = findWays(arr, S);
    Console.WriteLine(answer);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript Program to implement
    // the above approach

    // Function to call dfs() to
    // calculate the number of ways
    function findWays(nums, S)
    {
      return dfs(nums, S, 0, 0);
    }

    // Function to count the number of ways
    function dfs(nums, S, curr_sum, index)
    {
      // Base Case: Reached the
      // end of the array
      if (index == nums.length)
      {

        // Sum is equal to the
        // required sum
        if (S == curr_sum)
          return 1;
        else
          return 0;
      }

      // Recursively check if required sum
      // can be obtained by adding current
      // element or by subtracting the
      // current index element
      return dfs(nums, S, curr_sum +
                 nums[index], index + 1) +
               dfs(nums, S, curr_sum -
                 nums[index], index + 1);
    }

    let S = 3;
    let arr = [ 1, 2, 3, 4, 5 ];
    let answer = findWays(arr, S);
    document.write(answer);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

[**【动态规划】**](https://www.geeksforgeeks.org/dynamic-programming/) **方法:**上述递归方法可以通过使用[记忆化](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)进行优化。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the DFS to calculate the
// number of ways
int dfs(vector<vector<int>> memo, int nums[], int S,
               int curr_sum, int index, int sum, int N)
{
    // Base case: Reached the end of array
    if (index == N) {

        // If current sum is obtained
        if (S == curr_sum)
            return 1;

        // Otherwise
        else
            return 0;
    }

    // If previously calculated
    // subproblem occurred
    if (memo[index][curr_sum + sum]
        != INT_MIN) {
        return memo[index][curr_sum + sum];
    }

    // Check if the required sum can
    // be obtained by adding current
    // element or by subtracting the
    // current index element
    int ans = dfs(memo, nums, index + 1,
                  curr_sum + nums[index], S, sum, N)
              + dfs(memo, nums, index + 1,
                    curr_sum - nums[index], S, sum, N);

    // Store the count of ways
    memo[index][curr_sum + sum] = ans;

    return ans;
}

// Function to call dfs
// to calculate the number of ways
int findWays(int nums[], int S, int N)
{
    int sum = 0;

    // Iterate till the length of array
    for (int i = 0; i < N; i++)
        sum += nums[i];

    // Initialize the memorization table
    vector<vector<int>> memo(N + 1, vector<int> (2 * sum + 1, INT_MIN));

    return dfs(memo, nums, S, 0, 0, sum, N);
}

// Driver code
int main()
{
    int S = 3;
    int arr[] ={ 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int answer = findWays(arr, S, N);
    cout << answer << endl;

    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to call dfs
    // to calculate the number of ways
    static int findWays(int[] nums, int S)
    {
        int sum = 0;

        // Iterate till the length of array
        for (int i = 0; i < nums.length; i++)
            sum += nums[i];

        // Initialize the memorization table
        int[][] memo
            = new int[nums.length + 1][2 * sum + 1];

        for (int[] m : memo) {
            Arrays.fill(m, Integer.MIN_VALUE);
        }

        return dfs(memo, nums, S, 0, 0, sum);
    }

    // Function to perform the DFS to calculate the
    // number of ways
    static int dfs(int[][] memo, int[] nums, int S,
                   int curr_sum, int index, int sum)
    {
        // Base case: Reached the end of array
        if (index == nums.length) {

            // If current sum is obtained
            if (S == curr_sum)
                return 1;

            // Otherwise
            else
                return 0;
        }

        // If previously calculated
        // subproblem occurred
        if (memo[index][curr_sum + sum]
            != Integer.MIN_VALUE) {
            return memo[index][curr_sum + sum];
        }

        // Check if the required sum can
        // be obtained by adding current
        // element or by subtracting the
        // current index element
        int ans = dfs(memo, nums, index + 1,
                      curr_sum + nums[index], S, sum)
                  + dfs(memo, nums, index + 1,
                        curr_sum - nums[index], S, sum);

        // Store the count of ways
        memo[index][curr_sum + sum] = ans;

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int S = 3;
        int[] arr = new int[] { 1, 2, 3, 4, 5 };
        int answer = findWays(arr, S);
        System.out.println(answer);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to call dfs to
# calculate the number of ways
def findWays(nums, S):

    sum = 0

    # Iterate till the length of array
    for i in range(len(nums)):
        sum += nums[i]

    # Initialize the memorization table
    memo = [[-sys.maxsize - 1 for i in range(2 * sum + 1)]
                              for j in range(len(nums) + 1)]

    return dfs(memo, nums, S, 0, 0, sum)

# Function to perform the DFS to calculate the
# number of ways
def dfs(memo, nums, S, curr_sum, index, sum):

    # Base case: Reached the end of array
    if (index == len(nums)):

        # If current sum is obtained
        if (S == curr_sum):
            return 1

        # Otherwise
        else:
            return 0

    # If previously calculated
    # subproblem occurred
    if (memo[index][curr_sum + sum] != -sys.maxsize - 1):
        return memo[index][curr_sum + sum]

    # Check if the required sum can
    # be obtained by adding current
    # element or by subtracting the
    # current index element
    ans = (dfs(memo, nums, index + 1,
               curr_sum + nums[index], S, sum) +
           dfs(memo, nums, index + 1,
               curr_sum - nums[index], S, sum))

    # Store the count of ways
    memo[index][curr_sum + sum] = ans

    return ans

# Driver Code
if __name__ == '__main__':

    S = 3
    arr = [ 1, 2, 3, 4, 5 ]
    answer = findWays(arr, S)

    print(answer)

# This code is contributed by bgangwar59
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to call dfs
// to calculate the number of ways
static int findWays(int[] nums, int S)
{
    int sum = 0;

    // Iterate till the length of array
    for(int i = 0; i < nums.Length; i++)
        sum += nums[i];

    // Initialize the memorization table
    int[,] memo = new int[nums.Length + 1,
                              2 * sum + 1];

    for(int i = 0; i < memo.GetLength(0); i++)
    {
        for(int j = 0; j < memo.GetLength(1); j++)
        {
            memo[i, j] = int.MinValue;
        }
    }
    return dfs(memo, nums, S, 0, 0, sum);
}

// Function to perform the DFS to calculate the
// number of ways
static int dfs(int[,] memo, int[] nums, int S,
               int curr_sum, int index, int sum)
{

    // Base case: Reached the end of array
    if (index == nums.Length)
    {

        // If current sum is obtained
        if (S == curr_sum)
            return 1;

        // Otherwise
        else
            return 0;
    }

    // If previously calculated
    // subproblem occurred
    if (memo[index, curr_sum + sum] != int.MinValue)
    {
        return memo[index, curr_sum + sum];
    }

    // Check if the required sum can
    // be obtained by adding current
    // element or by subtracting the
    // current index element
    int ans = dfs(memo, nums, index + 1,
                  curr_sum + nums[index], S, sum) +
              dfs(memo, nums, index + 1,
                  curr_sum - nums[index], S, sum);

    // Store the count of ways
    memo[index, curr_sum + sum] = ans;

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int S = 3;
    int[] arr = new int[] { 1, 2, 3, 4, 5 };
    int answer = findWays(arr, S);

    Console.WriteLine(answer);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to call dfs
// to calculate the number of ways
function findWays(nums, S)
{
     let sum = 0;

    // Iterate till the length of array
    for(let i = 0; i < nums.length; i++)
        sum += nums[i];

    // Initialize the memorization table
    let memo = new Array([nums.length + 1][2 * sum + 1]);

     for(let i = 0; i < nums.length + 1; i++)
    {
        memo[i] = new Array(2 * sum + 1);
        for(let j = 0; j < 2 * sum + 1; j++)
        {
            memo[i][j] = Number.MIN_VALUE;
        }
    }
    return dfs(memo, nums, S, 0, 0, sum);
}

// Function to perform the DFS to calculate
// the number of ways
function dfs(memo, nums, S, curr_sum, index, sum)
{

    // Base case: Reached the end of array
    if (index == nums.length)
    {

        // If current sum is obtained
        if (S == curr_sum)
            return 1;

        // Otherwise
        else
            return 0;
    }

    // If previously calculated
    // subproblem occurred
    if (memo[index][curr_sum + sum] !=
        Number.MIN_VALUE)
    {
        return memo[index][curr_sum + sum];
    }

    // Check if the required sum can
    // be obtained by adding current
    // element or by subtracting the
    // current index element
    let ans = dfs(memo, nums, index + 1,
                  curr_sum + nums[index], S, sum) +
              dfs(memo, nums, index + 1,
                  curr_sum - nums[index], S, sum);

    // Store the count of ways
    memo[index][curr_sum + sum] = ans;

    return ans;
}

// Driver Code
let S = 3;
let arr = [ 1, 2, 3, 4, 5 ];
let answer = findWays(arr, S);

document.write(answer);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * S)*
***辅助空间:** O(N * S)*

**背包法:**思路是实现 [0/1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)问题。请遵循以下步骤:

*   最初的问题简化为寻找 arr[]的子集的方法数，该子集全部为正，其余元素为负，这样它们的和等于 **S** 。
*   因此，问题是从给定的数组中找出不具有和 **(S + totalSum)/2 的子集。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to call dfs
// to calculate the number of ways
int knapSack(int nums[], int S, int n)
{
    int sum = 0;
    for(int i = 0; i < n; i++)
        sum += nums[i];

    // If target + sum is odd or
    // S exceeds sum
    if (sum < S || -sum > -S ||
       (S + sum) % 2 == 1)

        // No sultion exists
        return 0;

    int dp[(S + sum) / 2 + 1];
    for(int i = 0; i <= (S + sum) / 2; i++)
        dp[i] = 0;

    dp[0] = 1;

    for(int j = 0; j < n; j++)
    {
        for(int i = (S + sum) / 2;
                i >= nums[j]; i--)
        {
            dp[i] += dp[i - nums[j]];
        }
    }

    // Return the answer
    return dp[(S + sum) / 2];
}

// Driver Code
int main()
{
    int S = 3;
    int arr[] = { 1, 2, 3, 4, 5 };
    int answer = knapSack(arr, S, 5);

    cout << answer << endl;
}

// This code is contributed by amal kumar choubey
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;

class GFG {

    // Function to call dfs
    // to calculate the number of ways
    static int knapSack(int[] nums, int S)
    {
        int sum = 0;
        for (int i : nums)
            sum += i;

        // If target + sum is odd or S exceeds sum
        if (sum < S || -sum > -S || (S + sum) % 2 == 1)

            // No sultion exists
            return 0;

        int[] dp = new int[(S + sum) / 2 + 1];
        dp[0] = 1;

        for (int num : nums) {
            for (int i = dp.length - 1; i >= num; i--) {
                dp[i] += dp[i - num];
            }
          }

        // Return the answer
        return dp[dp.length - 1];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int S = 3;
        int[] arr = new int[] { 1, 2, 3, 4, 5 };
        int answer = knapSack(arr, S);
        System.out.println(answer);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to call dfs
# to calculate the number of ways
def knapSack(nums, S):
    sum = 0;
    for i in range(len(nums)):
        sum += nums[i];

    # If target + sum is odd or S exceeds sum
    if (sum < S or -sum > -S or
       (S + sum) % 2 == 1):

        # No sultion exists
        return 0;

    dp = [0]*(((S + sum) // 2) + 1);
    dp[0] = 1;
    for j in range(len(nums)):
        for i in range(len(dp) - 1, nums[j] - 1, -1):
            dp[i] += dp[i - nums[j]];

    # Return the answer
    return dp[len(dp) - 1];

# Driver Code
if __name__ == '__main__':
    S = 3;
    arr = [1, 2, 3, 4, 5 ];
    answer = knapSack(arr, S);
    print(answer);

# This code is contributed by Princi Singh
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to call dfs
  // to calculate the number of ways
  static int knapSack(int[] nums, int S)
  {
    int sum = 0;
    foreach (int i in nums)
      sum += i;

    // If target + sum is odd or S exceeds sum
    if (sum < S || -sum > -S ||
       (S + sum) % 2 == 1)

      // No sultion exists
      return 0;

    int[] dp = new int[(S + sum) / 2 + 1];
    dp[0] = 1;

    foreach (int num in nums)
    {
      for (int i = dp.Length - 1; i >= num; i--)
      {
        dp[i] += dp[i - num];
      }
    }

    // Return the answer
    return dp[dp.Length - 1];
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int S = 3;
    int[] arr = new int[] { 1, 2, 3, 4, 5 };
    int answer = knapSack(arr, S);
    Console.WriteLine(answer);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript Program to implement
    // the above approach

    // Function to call dfs
    // to calculate the number of ways
    function knapSack(nums, S)
    {
        let sum = 0;
        for (let i = 0; i < nums.length; i++)
            sum += nums[i];

        // If target + sum is odd or S exceeds sum
        if (sum < S || -sum > -S || (S + sum) % 2 == 1)

            // No sultion exists
            return 0;

        let dp = new Array(parseInt((S + sum) / 2, 10) + 1);
        dp.fill(0);
        dp[0] = 1;

        for (let num = 0; num < nums.length; num++) {
            for (let i = dp.length - 1; i >= nums[num]; i--) {
                dp[i] += dp[i - nums[num]];
            }
          }

        // Return the answer
        return dp[dp.length - 1];
    }

    let S = 3;
    let arr = [ 1, 2, 3, 4, 5 ];
    let answer = knapSack(arr, S);
    document.write(answer);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(n*(和+ S))，其中**和**表示数组的和*
***辅助空间:** O(S +和)*
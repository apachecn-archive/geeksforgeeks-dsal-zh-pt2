# 每次移除数组一半后，最大化剩余元素的总和，取较大的总和

> 原文:[https://www . geeksforgeeks . org/最大化每次移除大和后剩余元素的总和/](https://www.geeksforgeeks.org/maximize-sum-of-remaining-elements-after-every-removal-of-the-array-half-with-greater-sum/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在每次移除带有最大和的数组一半后，将剩余元素相加后得到的结果和最大化。

> 数组可以分为两个非空的部分**左[]** 和**右[]** ，其中**左[]** 包含来自索引**【0，N/2】**的元素，而**右[**包含来自索引**【N/2，N】**的元素

**示例:**

> **输入:** arr[] = {6，2，3，4，5，5}
> **输出:** 18
> **解释:**
> 给定数组是 arr[] = {6，2，3，4，5，5}
> 第 1 步:
> 左半部分之和= 6 + 2 + 3 = 11
> 右半部分之和= 4 + 5 + 5 = 12
> 合成和 S = 11。
> 第二步:
> 修改后的数组是 arr[] = {6，2，3}
> 左半部分之和= 6
> 右半部分之和= 2 + 3 = 5
> 合成和 S = 11 + 5 = 16
> 第三步:
> 修改后的数组是 arr[] = {2，3}
> 左半部分之和= 2
> 右半部分之和= 3
> 合成和 S = 16 + 2 = 18。
> 因此，结果和为 18。
> 
> **输入:**arr[]= { 4 }
> T3】输出: 0

**天真方法:**解决问题最简单的方法就是使用[递归](https://www.geeksforgeeks.org/recursion/)。以下是步骤:

1.  使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念，初始化一个变量，比如说 **res** 来存储最终的**结果**。
2.  创建[词典](https://www.geeksforgeeks.org/python-dictionary/)。
3.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将所有[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)存储在字典中。
4.  现在，迭代范围**【0，N】**，将数组左右半部分的前缀和分别存储为**左**和**右**。
5.  现在，有三种可能的情况:
    *   左>右
    *   左
    *   左==右
6.  对于以上所有条件，忽略最大和，将**左**和**右**之和中的最小值加到结果和上，继续递归调用。
7.  所有递归调用结束后，打印结果**和**的最大值。

下面是上述方法的实现:

## C++14

```
// C++14 program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
int maxweight(int s, int e,
  unordered_map<int, int>& pre)
{

    // Base case
    // len of array is 1
    if (s == e)
        return 0;

    // Stores the final result
    int ans = 0;

    // Traverse the array
    for(int i = s; i < e; i++)
    {

        // Store left prefix sum
        int left = pre[i] - pre[s - 1];

        // Store right prefix sum
        int right = pre[e] - pre[i];

        // Compare the left and right
        if (left < right)
            ans = max(ans, left +
                      maxweight(s, i, pre));

        // If both are equal apply
        // the optimal method
        if (left == right)
        {
            // Update with minimum
            ans = max({ans, left +
                       maxweight(s, i, pre),
                             right +
                       maxweight(i + 1, e, pre)});
        }

        if (left > right)
            ans = max(ans, right +
                     maxweight(i + 1, e, pre));
    }    

    // Return the final ans
    return ans;
}

// Function to print maximum sum
void maxSum(vector<int> arr)
{

    // Dictionary to store prefix sums
    unordered_map<int, int> pre;
    pre[-1] = 0;
    pre[0] = arr[0];

    // Traversing the array
    for(int i = 1; i < arr.size(); i++)
    {

        // Add prefix sum of the array
        pre[i] = pre[i - 1] + arr[i];
    }
    cout << maxweight(0, arr.size() - 1, pre);
}

// Driver Code
int main()
{
    vector<int> arr = { 6, 2, 3, 4, 5, 5 };

    // Function call
    maxSum(arr);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the maximum sum
static int maxweight(int s, int e,
                     Map<Integer, Integer> pre)
{

    // Base case
    // len of array is 1
    if (s == e)
        return 0;

    // Stores the final result
    int ans = 0;

    // Traverse the array
    for(int i = s; i < e; i++)
    {

        // Store left prefix sum
        int left = pre.get(i) - pre.get(s - 1);

        // Store right prefix sum
        int right = pre.get(e) - pre.get(i);

        // Compare the left and right
        if (left < right)
            ans = Math.max(ans, left +
                           maxweight(s, i, pre));

        // If both are equal apply
        // the optimal method
        if (left == right)
        {

            // Update with minimum
            ans = Math.max(ans, Math.max(left +
                           maxweight(s, i, pre),
                           right + maxweight(i + 1,
                                             e, pre)));
        }

        if (left > right)
            ans = Math.max(ans, right +
                           maxweight(i + 1, e, pre));
    }    

    // Return the final ans
    return ans;
}

// Function to print maximum sum
static void maxSum(List<Integer> arr)
{

    // To store prefix sums
    Map<Integer, Integer> pre = new HashMap<>();
    pre.put(-1, 0);
    pre.put(0, arr.get(0));

    // Traversing the array
    for(int i = 1; i < arr.size(); i++)
    {

        // Add prefix sum of the array
        pre.put(i, pre.getOrDefault(i - 1, 0) +
                   arr.get(i));
    }
    System.out.println(maxweight(0,
                arr.size() - 1, pre));
}

// Driver code
public static void main (String[] args)
{
    List<Integer> arr = Arrays.asList(6, 2, 3,
                                      4, 5, 5);

    // Function call
    maxSum(arr);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum
def maxweight(s, e, pre):

    # Base case
    # len of array is 1
    if s == e:
        return 0

    # Stores the final result
    ans = 0

    # Traverse the array
    for i in range(s, e):

        # Store left prefix sum
        left = pre[i] - pre[s - 1]

        # Store right prefix sum
        right = pre[e] - pre[i]

        # Compare the left and right
        if left < right:
            ans = max(ans, left \
            + maxweight(s, i, pre))

        # If both are equal apply
        # the optimal method
        if left == right:

            # Update with minimum
            ans = max(ans, left \
                  + maxweight(s, i, pre),
                    right \
                  + maxweight(i + 1, e, pre))

        if left > right:
            ans = max(ans, right \
                  + maxweight(i + 1, e, pre))

    # Return the final ans
    return ans

# Function to print maximum sum
def maxSum(arr):

    # Dictionary to store prefix sums
    pre = {-1: 0, 0: arr[0]}

    # Traversing the array
    for i in range(1, len(arr)):

        # Add prefix sum of the array
        pre[i] = pre[i - 1] + arr[i]

    print(maxweight(0, len(arr) - 1, pre))

# Drivers Code

arr = [6, 2, 3, 4, 5, 5]

# Function Call
maxSum(arr)
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the maximum sum
static int maxweight(int s, int e,
                     Dictionary<int,
                     int> pre)
{
  // Base case
  // len of array is 1
  if (s == e)
    return 0;

  // Stores the
  // readonly result
  int ans = 0;

  // Traverse the array
  for(int i = s; i < e; i++)
  {
    // Store left prefix sum
    int left = pre[i] - pre[s - 1];

    // Store right prefix sum
    int right = pre[e] - pre[i];

    // Compare the left and right
    if (left < right)
      ans = Math.Max(ans, left +
            maxweight(s, i, pre));

    // If both are equal apply
    // the optimal method
    if (left == right)
    {
      // Update with minimum
      ans = Math.Max(ans, Math.Max(left +
                          maxweight(s, i, pre),
                          right + maxweight(i + 1,
                                            e, pre)));
    }

    if (left > right)
      ans = Math.Max(ans, right +
            maxweight(i + 1, e, pre));
  }    

  // Return the readonly ans
  return ans;
}

// Function to print maximum sum
static void maxSum(List<int> arr)
{

  // To store prefix sums
  Dictionary<int,
             int> pre = new Dictionary<int,
                                       int>();
  pre.Add(-1, 0);
  pre.Add(0, arr[0]);

  // Traversing the array
  for(int i = 1; i < arr.Count; i++)
  {
    // Add prefix sum of the array
    if(pre[i - 1] != 0)
      pre.Add(i, pre[i - 1] + arr[i]);
    else
      pre.Add(i, arr[i]);
  }
  Console.WriteLine(maxweight(0,
                    arr.Count - 1, pre));
}

// Driver code
public static void Main(String[] args)
{
  List<int> arr = new List<int>();
  arr.Add(6);
  arr.Add(2);
  arr.Add(3);
  arr.Add(4);
  arr.Add(5);
  arr.Add(5);

  // Function call
  maxSum(arr);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// js program to implement
// the above approach

// Function to find the maximum sum
function maxweight(s, e, pre){
    // Base case
    // len of array is 1
    if (s == e)
        return 0;

    // Stores the final result
    let ans = 0;

    // Traverse the array
    for(let i = s; i < e; i++)
    {

        // Store left prefix sum
        if(!pre[i])
           pre[i] = 0;
        if(!pre[e])
           pre[e] = 0;
        if(!pre[s-1])
           pre[s-1] = 0;
        let left = pre[i] - pre[s - 1];

        // Store right prefix sum
        let right = pre[e] - pre[i];

        // Compare the left and right
        if (left < right)
            ans = Math.max(ans, left +
                      maxweight(s, i, pre));

        // If both are equal apply
        // the optimal method
        if (left == right)
        {
            // Update with minimum
            ans = Math.max(ans, Math.max(left +
                       maxweight(s, i, pre),
                             right +
                       maxweight(i + 1, e, pre)));
        }

        if (left > right)
            ans = Math.max(ans, right +
                     maxweight(i + 1, e, pre));
    }    

    // Return the final ans
    return ans;
}

// Function to print maximum sum
function maxSum(arr)
{

    // Dictionary to store prefix sums
    let pre = new Map;
    pre[-1] = 0;
    pre[0] = arr[0];

    // Traversing the array
    for(let i = 1; i < arr.length; i++)
    {

        // Add prefix sum of the array
        pre[i] = pre[i - 1] + arr[i];
    }
   document.write( maxweight(0, arr.length - 1, pre));
}

// Driver Code
arr = [ 6, 2, 3, 4, 5, 5 ];
// Function call
 maxSum(arr);

</script>
```

**Output:** 

```
18
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**对上述方法进行优化，思路是观察有多个重复的[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。
因此，为了优化，使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。其思想是使用字典并跟踪结果值，以便在进一步计算中需要它们时，无需再次计算即可访问它们。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[100][100];

// Function to find the maximum sum
int maxweight(int s, int e,
          map<int, int> pre)
{

    // Base Case
    if (s == e)
        return 0;

    // Create a key to map
    // the values

    // Check if (mapped key is
    // found in the dictionary
    if (dp[s][e] != -1)
        return dp[s][e];

    int ans = 0;

    // Traverse the array
    for(int i = s; i < e; i++)
    {

        // Store left prefix sum
        int left = pre[i] - pre[s - 1];

        // Store right prefix sum
        int right = pre[e] - pre[i];

        // Compare the left and
        // right values
        if (left < right)
            ans = max(
                ans, (int)(left +
                           maxweight(s, i, pre)));

        if (left == right)
            ans = max(
                ans, max(left + maxweight(s, i,
                                          pre),
                         right + maxweight(i + 1,
                                           e, pre)));

        if (left > right)
            ans = max(
                ans, right + maxweight(i + 1, e, pre));

        // Store the value in dp array
        dp[s][e] = ans;
    }

    // Return the final answer
    return dp[s][e];
}

// Function to print maximum sum
void maxSum(int arr[], int n)
{

    // Stores prefix sum
    map<int, int> pre;
    pre[-1] = 0;
    pre[0] = arr[0];

    // Store results of subproblems
    memset(dp, -1, sizeof dp);

    // Traversing the array
    for(int i = 0; i < n; i++)

        // Add prefix sum of array
        pre[i] = pre[i - 1] + arr[i];

    // Print the answer
    cout << (maxweight(0, n - 1, pre));
}

// Driver Code
int main()
{
    int arr[] = { 6, 2, 3, 4, 5, 5 };

    // Function call
    maxSum(arr, 6);
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class solution{

static int[][] dp = new int[100][100];

// Function to find the maximum sum
static int maxweight(int s, int e,
                     HashMap<Integer, Integer> pre)
{

    // Base Case
    if (s == e)
        return 0;

    // Create a key to map
    // the values

    // Check if (mapped key is
    // found in the dictionary
    if (dp[s][e] != -1)
        return dp[s][e];

    int ans = 0;

    // Traverse the array
    for(int i = s; i < e; i++)
    {

        // Store left prefix sum
        int left = pre.get(i) -
                   pre.get(s - 1);

        // Store right prefix sum
        int right = pre.get(e) -
                    pre.get(i);

        // Compare the left and
        // right values
        if (left < right)
            ans = Math.max(ans, (int)(left +
                           maxweight(s, i, pre)));

        if (left == right)
            ans = Math.max(ans,
                           Math.max(left + maxweight(s, i,
                                                     pre),
                                    right + maxweight(i + 1,
                                                      e, pre)));

        if (left > right)
            ans = Math.max(ans, right + maxweight(i + 1,
                                                  e, pre));

        // Store the value in dp array
        dp[s][e] = ans;
    }

    // Return the final answer
    return dp[s][e];
}

// Function to print maximum sum
static void maxSum(int arr[], int n)
{

    // Stores prefix sum
    HashMap<Integer,
            Integer> pre = new HashMap<Integer,
                                       Integer>();
    pre.put(-1, 0);
    pre.put(0, arr[0]);

    // Store results of subproblems
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < 100; j++)
          dp[i][j] = -1;
    }

    // Traversing the array
    for(int i = 0; i < n; i++)

        // Add prefix sum of array
        pre.put(i, pre.get(i - 1) + arr[i]);

    // Print the answer
    System.out.print((maxweight(0, n - 1, pre)));
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 6, 2, 3, 4, 5, 5 };

    // Function call
    maxSum(arr, 6);
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum
def maxweight(s, e, pre, dp):

    # Base Case 
    if s == e:
        return 0

    # Create a key to map
    # the values
    key = (s, e)

    # Check if mapped key is
    # found in the dictionary
    if key in dp:
        return dp[key]

    ans = 0

    # Traverse the array
    for i in range(s, e):

         # Store left prefix sum
        left = pre[i] - pre[s-1]

        # Store right prefix sum
        right = pre[e] - pre[i]

        # Compare the left and
        # right values
        if left < right:
            ans = max(ans, left \
                + maxweight(s, i, pre, dp))

        if left == right:

            # Update with minimum
            ans = max(ans, left \
                  + maxweight(s, i, pre, dp),
                  right \
                  + maxweight(i + 1, e, pre, dp))

        if left > right:
           ans = max(ans, right \
                 + maxweight(i + 1, e, pre, dp))

        # Store the value in dp array
        dp[key] = ans

    # Return the final answer
    return dp[key]

# Function to print maximum sum
def maxSum(arr):

    # Stores prefix sum
    pre = {-1: 0, 0: arr[0]}

    # Store results of subproblems
    dp = {}

    # Traversing the array
    for i in range(1, len(arr)):

        # Add prefix sum of array
        pre[i] = pre[i - 1] + arr[i]

    # Print the answer
    print(maxweight(0, len(arr) - 1, pre, dp))

# Driver Code

arr = [6, 2, 3, 4, 5, 5]

# Function Call
maxSum(arr)
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static int[,] dp = new int[100, 100];

// Function to find the maximum sum
static int maxweight(int s, int e,
          Dictionary<int, int> pre)
{

    // Base Case
    if (s == e)
        return 0;

    // Create a key to map
    // the values

    // Check if (mapped key is
    // found in the dictionary
    if (dp[s, e] != -1)
        return dp[s, e];

    int ans = 0;

    // Traverse the array
    for(int i = s; i < e; i++)
    {

        // Store left prefix sum
        int left = pre[i] -
                   pre[s - 1];

        // Store right prefix sum
        int right = pre[e] -
                    pre[i];

        // Compare the left and
        // right values
        if (left < right)
            ans = Math.Max(ans, (int)(left +
                           maxweight(s, i, pre)));

        if (left == right)
            ans = Math.Max(ans,
                           Math.Max(left + maxweight(s, i,
                                                     pre),
                                   right + maxweight(i + 1,
                                                     e, pre)));

        if (left > right)
            ans = Math.Max(ans, right + maxweight(i + 1,
                                                  e, pre));

        // Store the value in dp array
        dp[s, e] = ans;
    }

    // Return the readonly answer
    return dp[s, e];
}

// Function to print maximum sum
static void maxSum(int []arr, int n)
{

    // Stores prefix sum
    Dictionary<int,
               int> pre = new Dictionary<int,
                                         int>();
    pre.Add(-1, 0);
    pre.Add(0, arr[0]);

    // Store results of subproblems
    for(int i = 0; i < 100; i++)
    {
        for(int j = 0; j < 100; j++)
          dp[i, j] = -1;
    }

    // Traversing the array
    for(int i = 1; i < n; i++)

        // Add prefix sum of array
        pre.Add(i, pre[i - 1] + arr[i]);

    // Print the answer
    Console.Write((maxweight(0, n - 1, pre)));
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 6, 2, 3, 4, 5, 5 };

    // Function call
    maxSum(arr, 6);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// js program to implement
// the above approach
let dp=[];
for(let i = 0;i<100;i++){
dp[i] = [];
for(let j = 0;j<100;j++){
dp[i][j] = 0;
}
}

// Function to find the maximum sum
function maxweight( s,  e, pre)
{

    // Base Case
    if (s == e)
        return 0;

    // Create a key to map
    // the values

    // Check if (mapped key is
    // found in the dictionary
    if (dp[s][e] != -1)
        return dp[s][e];

    let ans = 0;

    // Traverse the array
    for(let i = s; i < e; i++)
    {

        // Store left prefix sum
        let left = pre[i] - pre[s - 1];

        // Store right prefix sum
        let right = pre[e] - pre[i];

        // Compare the left and
        // right values
        if (left < right)
            ans = Math.max(
                ans, Number(left +
                           maxweight(s, i, pre)));

        if (left == right)
            ans = Math.max(
                ans,Math. max(left + maxweight(s, i,
                                          pre),
                         right + maxweight(i + 1,
                                           e, pre)));

        if (left > right)
            ans = Math.max(
                ans, right + maxweight(i + 1, e, pre));

        // Store the value in dp array
        dp[s][e] = ans;
    }

    // Return the final answer
    return dp[s][e];
}

// Function to print maximum sum
function maxSum(arr, n)
{

    // Stores prefix sum
    let pre = new Map();
    pre[-1] = 0;
    pre[0] = arr[0];

    // Store results of subproblems

    for(let i = 0;i<100;i++){
    for(let j = 0;j<100;j++){
     dp[i][j] = -1;
}
}
    // Traversing the array
    for(let i = 0; i < n; i++)

        // Add prefix sum of array
        pre[i] = pre[i - 1] + arr[i];

    // Print the answer
    document.write(maxweight(0, n - 1, pre));
}

// Driver Code
let arr= [ 6, 2, 3, 4, 5, 5 ];

    // Function call
    maxSum(arr, 6);

</script>
```

**Output:** 

```
18
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*
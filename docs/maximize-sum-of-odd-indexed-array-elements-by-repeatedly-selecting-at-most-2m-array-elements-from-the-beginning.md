# 从开始重复选择最多 2*M 个数组元素，最大化奇数索引数组元素的和

> 原文:[https://www . geesforgeks . org/通过从头开始重复选择最多 2m 个数组元素来最大化奇数索引数组元素的总和/](https://www.geeksforgeeks.org/maximize-sum-of-odd-indexed-array-elements-by-repeatedly-selecting-at-most-2m-array-elements-from-the-beginning/)

给定一个由 **N** 个整数和一个整数 **M** ( *最初为 **1*** )组成的[阵**arr【】**，任务是当两个玩家 **A** 和 **B** 按照以下规则进行最佳游戏时，找到**玩家 A** 选择的阵元](https://www.geeksforgeeks.org/introduction-to-arrays/)的最大[和:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   **玩家 A** 开始游戏。
*   每一次机会，都可以从数组的开始处选择 **X** 个元素，其中 **X** 在范围内包含**【1，2 * M】**由各自的玩家依次选择。
*   在以上步骤中选择数组元素后，从数组中移除这些元素，并将 **M** 的值更新为 **X** 和 **M** 的最大值。
*   上述过程将[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)直到所有阵列元素被选择。

**示例:**

> **输入:** arr[] = {2，7，9，4，4}
> **输出:** 10
> **解释:**
> 最初数组是 arr[] = {2，7，9，4，4}，M 的值= 1，下面是双方玩家使用数组元素的顺序:
> **玩家 A:** 元素的数量可以在【1，2*M】的范围内选择，即:
> 所以，选择元素 **{2}** 并将其移除。现在数组修改为{7，9，4，4}，M 的值为 max(M，X) = max(1，1) = 1(X 为 1)。
> **玩家 B:** 元素数量可以在【1，2*M】即【1，2】的范围内选择。所以，选择元素 **{7，9}** 将其移除。现在数组修改为{4，4}，M 的值为 max(M，X) = max(1，2) = 2(X 为 2)。
> **玩家 A:** 元素数量可以在【1，2*2】即【1，1】的范围内选择。所以，选择元素 **{4，4}** 将其移除。现在数组变成空的。
> 
> 因此，玩家 A 选择的元素之和为 2 + 4 + 4 = 10。
> 
> **输入:**arr[]= { 1 }
> T3】输出: 1

**天真法:**解决给定问题最简单的方法就是使用[递归](https://www.geeksforgeeks.org/recursion/)按照给定的规则从一开始就为双方玩家生成所有可能的选择元素组合，并打印出为**玩家 A** 获得的选择元素最大和。按照以下步骤解决给定的问题:

*   声明一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，说**recursivechosing(arr，start，M)** ，取参数数组，当前数组的起始索引， **M** 的初始值，在这个函数中执行如下操作:
    *   如果**开始**的值大于 **N** ，则返回 **0** 。
    *   如果**(N–start)**的值最多为 **2*M** ，则从索引**开始**返回[数组元素的和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)给玩家各自的分数。
    *   将 **maxSum** 初始化为 **0** ，存储**玩家 A** 选择的数组元素的最大[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
    *   从开始计算数组元素的[总和，并将其存储在一个变量中，比如**总和**。](https://www.geeksforgeeks.org/sum-function-python/)
    *   迭代范围**【1，2 * M】**，执行以下步骤:
        *   对于每个元素 **X** ，从**开始选择 **X** 元素，**递归调用从剩余的**(N–X)**元素中选择元素。让这个调用返回的值存储在 **maxSum** 中。
        *   上述递归调用结束后，将 **maxSum** 的值更新为 **maxSum** 和**(总计–maxSum)**的最大值。
    *   在每次递归调用中返回 **maxSum** 的值。
*   完成上述步骤后，打印函数**recursivechosing(arr，0，1)** 返回的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Sum of all numbers in the array
// after start index
int sum(int arr[], int start, int N)
{
    int sum1 = 0;
    for(int i = start; i < N; i++)
    {
        sum1 += arr[i];
    }
    return sum1;
}

// Function to find the maximum sum of
// array elements chosen by Player A
// according to the given criteria
int recursiveChoosing(int arr[], int start,
                      int M, int N)
{

    // Corner Case
    if (start >= N)
    {
        return 0;
    }

    // Check if all the elements can
    // be taken
    if (N - start <= 2 * M)
    {

        // If the difference is less than
        // or equal to the available
        // chances then pick all numbers
        return sum(arr, start, N);
    }

    int psa = 0;

    // Sum of all numbers in the array
    int total = sum(arr, start, N);

    // Explore each element X

    // Skipping the k variable as per
    // the new updated chance of utility
    for(int x = 1; x < 2 * M + 1; x++)
    {

        // Sum of elements for Player A
        int psb = recursiveChoosing(arr, start + x,
                                    max(x, M), N);

        // Even chance sum can be obtained
        // by subtracting the odd chances
        // sum - total and picking up the
        // maximum from that
        psa = max(psa, total - psb);
    }

    // Return the maximum sum of odd chances
    return psa;
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 2, 7, 9, 4, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << recursiveChoosing(arr, 0, 1, N);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the maximum sum of
// array elements chosen by Player A
// according to the given criteria
static int recursiveChoosing(int arr[], int start,
                             int M, int N)
{

    // Corner Case
    if (start >= N)
    {
        return 0;
    }

    // Check if all the elements can
    // be taken
    if (N - start <= 2 * M)
    {

        // If the difference is less than
        // or equal to the available
        // chances then pick all numbers
        return sum(arr, start);
    }

    int psa = 0;

    // Sum of all numbers in the array
    int total = sum(arr, start);

    // Explore each element X

    // Skipping the k variable as per
    // the new updated chance of utility
    for(int x = 1; x < 2 * M + 1; x++)
    {

        // Sum of elements for Player A
        int psb = recursiveChoosing(arr, start + x,
                                    Math.max(x, M), N);

        // Even chance sum can be obtained
        // by subtracting the odd chances
        // sum - total and picking up the
        // maximum from that
        psa = Math.max(psa, total - psb);
    }

    // Return the maximum sum of odd chances
    return psa;
}

// Sum of all numbers in the array after start index
static int sum(int arr[], int start)
{
    int sum = 0;
    for(int i = start; i < arr.length; i++)
    {
        sum += arr[i];
    }
    return sum;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 7, 9, 4, 4 };
    int N = arr.length;

    // Function Call
    System.out.print(recursiveChoosing(
        arr, 0, 1, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum sum of
# array elements chosen by Player A
# according to the given criteria
def recursiveChoosing(arr, start, M):

    # Corner Case
    if start >= N:
        return 0

    # Check if all the elements can
    # be taken
    if N - start <= 2 * M:

        # If the difference is less than
        # or equal to the available
        # chances then pick all numbers
        return sum(arr[start:])

    psa = 0

    # Sum of all numbers in the array
    total = sum(arr[start:])

    # Explore each element X

    # Skipping the k variable as per
    # the new updated chance of utility
    for x in range(1, 2 * M + 1):

        # Sum of elements for Player A
        psb = recursiveChoosing(arr,
                            start + x, max(x, M))

        # Even chance sum can be obtained
        # by subtracting the odd chances
        # sum - total and picking up the
        # maximum from that
        psa = max(psa, total - psb) 

    # Return the maximum sum of odd chances
    return psa

# Driver Code

# Given array arr[]
arr = [2, 7, 9, 4, 4]
N = len(arr)

# Function Call
print(recursiveChoosing(arr, 0, 1))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum sum of
// array elements chosen by Player A
// according to the given criteria
static int recursiveChoosing(int[] arr, int start,
                             int M, int N)
{

    // Corner Case
    if (start >= N)
    {
        return 0;
    }

    // Check if all the elements can
    // be taken
    if (N - start <= 2 * M)
    {

        // If the difference is less than
        // or equal to the available
        // chances then pick all numbers
        return sum(arr, start);
    }

    int psa = 0;

    // Sum of all numbers in the array
    int total = sum(arr, start);

    // Explore each element X

    // Skipping the k variable as per
    // the new updated chance of utility
    for(int x = 1; x < 2 * M + 1; x++)
    {

        // Sum of elements for Player A
        int psb = recursiveChoosing(arr, start + x,
                                    Math.Max(x, M), N);

        // Even chance sum can be obtained
        // by subtracting the odd chances
        // sum - total and picking up the
        // maximum from that
        psa = Math.Max(psa, total - psb);
    }

    // Return the maximum sum of odd chances
    return psa;
}

// Sum of all numbers in the array after start index
static int sum(int[] arr, int start)
{
    int sum = 0;
    for(int i = start; i < arr.Length; i++)
    {
        sum += arr[i];
    }
    return sum;
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 2, 7, 9, 4, 4 };
    int N = arr.Length;

    // Function Call
    Console.WriteLine(recursiveChoosing(
        arr, 0, 1, N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Sum of all numbers in the array
// after start index
function sum(arr, start, N)
{
    var sum1 = 0;
    for(var i = start; i < N; i++)
    {
        sum1 += arr[i];
    }
    return sum1;
}

// Function to find the maximum sum of
// array elements chosen by Player A
// according to the given criteria
function recursiveChoosing(arr, start, M, N)
{

    // Corner Case
    if (start >= N)
    {
        return 0;
    }

    // Check if all the elements can
    // be taken
    if (N - start <= 2 * M)
    {

        // If the difference is less than
        // or equal to the available
        // chances then pick all numbers
        return sum(arr, start, N);
    }

    var psa = 0;

    // Sum of all numbers in the array
    var total = sum(arr, start, N);

    // Explore each element X

    // Skipping the k variable as per
    // the new updated chance of utility
    for(var x = 1; x < 2 * M + 1; x++)
    {

        // Sum of elements for Player A
        var psb = recursiveChoosing(arr, start + x,
                                    Math.max(x, M), N);

        // Even chance sum can be obtained
        // by subtracting the odd chances
        // sum - total and picking up the
        // maximum from that
        psa = Math.max(psa, total - psb);
    }

    // Return the maximum sum of odd chances
    return psa;
}

// Driver Code

// Given array arr[]
var arr = [ 2, 7, 9, 4, 4 ];
var N = arr.length

// Function Call
document.write(recursiveChoosing(arr, 0, 1, N));

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(K*2 <sup>N</sup> ，其中 **K** 超出范围**【1，2 * M】***
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**上述方法也可以通过使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为它具有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)，可以在相同的递归调用中存储和进一步使用。

因此，想法是使用[字典](https://www.geeksforgeeks.org/python-dictionary/)来存储每个递归调用的状态，以便可以更快地访问已经计算的状态，从而降低时间复杂度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// array elements chosen by Player A
// according to the given criteria
int recursiveChoosing(int arr[], int start, int M, map<pair<int,int>,int> dp, int N)
{

    // Store the key
    pair<int,int> key(start, M);

    // Corner Case
    if(start >= N)
    {
        return 0;
    }

    // Check if all the elements can
    // be taken or not
    if(N - start <= 2 * M)
    {
        // If the difference is less than
        // or equal to the available
        // chances then pick all numbers
        int Sum = 0;
        for(int i = start; i < N; i++)
        {
            Sum = Sum + arr[i];
        }
        return Sum;
    }

    int sum = 0;
    for(int i = start; i < N; i++)
    {
      sum = sum + arr[i];
    }
    // Find the sum of array elements
    // over the range [start, N]
    int total = sum;

    // Checking if the current state is
    // previously calculated or not

    // If yes then return that value
    if(dp.find(key) != dp.end())
    {
        return dp[key];
    }
    int psa = 0;
    // Traverse over the range [1, 2 * M]
    for(int x = 1; x < 2 * M + 1; x++)
    {
        // Sum of elements for Player A
        int psb = recursiveChoosing(arr, start + x, max(x, M), dp, N);
        // Even chance sum can be obtained
        // by subtracting the odd chances
        // sum - total and picking up the
        // maximum from that
        psa = max(psa, total - psb);
    }

    // Storing the value in dictionary
    dp[key] = psa;

    // Return the maximum sum of odd chances
    return dp[key];
}

int main()
{
    int arr[] = {2, 7, 9, 4, 4};
    int N = sizeof(arr) / sizeof(arr[0]);

    // Stores the precomputed values
    map<pair<int,int>,int> dp;

    // Function Call
    cout << recursiveChoosing(arr, 0, 1, dp, N);

    return 0;
}

// This code is contributed by rameshtravel07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.awt.Point;
public class GFG
{
    // Function to find the maximum sum of
    // array elements chosen by Player A
    // according to the given criteria
    static int recursiveChoosing(int[] arr, int start, int M,
                                 HashMap<Point,Integer> dp)
    {

        // Store the key
        Point key = new Point(start, M);

        // Corner Case
        if(start >= arr.length)
        {
            return 0;
        }

        // Check if all the elements can
        // be taken or not
        if(arr.length - start <= 2 * M)
        {

            // If the difference is less than
            // or equal to the available
            // chances then pick all numbers
            int Sum = 0;
            for(int i = start; i < arr.length; i++)
            {
                Sum = Sum + arr[i];
            }
            return Sum;
        }

        int sum = 0;
        for(int i = start; i < arr.length; i++)
        {
          sum = sum + arr[i];
        }

        // Find the sum of array elements
        // over the range [start, N]
        int total = sum;

        // Checking if the current state is
        // previously calculated or not

        // If yes then return that value
        if(dp.containsKey(key))
        {
            return dp.get(key);
        }
        int psa = 0;

        // Traverse over the range [1, 2 * M]
        for(int x = 1; x < 2 * M + 1; x++)
        {

            // Sum of elements for Player A
            int psb = recursiveChoosing(arr, start + x, Math.max(x, M), dp);

            // Even chance sum can be obtained
            // by subtracting the odd chances
            // sum - total and picking up the
            // maximum from that
            psa = Math.max(psa, total - psb);
        }

        // Storing the value in dictionary
        dp.put(key, psa);

        // Return the maximum sum of odd chances
        return dp.get(key);
    }

    public static void main(String[] args) {
        int[] arr = {2, 7, 9, 4, 4};
        int N = arr.length;

        // Stores the precomputed values
        HashMap<Point,Integer> dp = new HashMap<Point,Integer>();

        // Function Call
        System.out.print(recursiveChoosing(arr, 0, 1, dp));
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum sum of
# array elements chosen by Player A
# according to the given criteria
def recursiveChoosing(arr, start, M, dp):

    # Store the key
    key = (start, M)

    # Corner Case
    if start >= N:
        return 0

    # Check if all the elements can
    # be taken or not
    if N - start <= 2 * M:

        # If the difference is less than
        # or equal to the available
        # chances then pick all numbers
        return sum(arr[start:])

    psa = 0

    # Find the sum of array elements
    # over the range [start, N]
    total = sum(arr[start:])

    # Checking if the current state is
    # previously calculated or not

    # If yes then return that value
    if key in dp:
        return dp[key]

    # Traverse over the range [1, 2 * M]
    for x in range(1, 2 * M + 1):

        # Sum of elements for Player A
        psb = recursiveChoosing(arr,
                          start + x, max(x, M), dp)

        # Even chance sum can be obtained
        # by subtracting the odd chances
        # sum - total and picking up the
        # maximum from that
        psa = max(psa, total - psb)

    # Storing the value in dictionary
    dp[key] = psa 

    # Return the maximum sum of odd chances
    return dp[key] 

# Driver Code

# Given array arr[]
arr = [2, 7, 9, 4, 4] 
N = len(arr) 

# Stores the precomputed values
dp = {} 

# Function Call
print(recursiveChoosing(arr, 0, 1, dp))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the maximum sum of
    // array elements chosen by Player A
    // according to the given criteria
    static int recursiveChoosing(int[] arr, int start, int M,
                                 Dictionary<Tuple<int,int>,int> dp)
    {

        // Store the key
        Tuple<int,int> key = new Tuple<int,int>(start, M);

        // Corner Case
        if(start >= arr.Length)
        {
            return 0;
        }

        // Check if all the elements can
        // be taken or not
        if(arr.Length - start <= 2 * M)
        {
            // If the difference is less than
            // or equal to the available
            // chances then pick all numbers
            int Sum = 0;
            for(int i = start; i < arr.Length; i++)
            {
                Sum = Sum + arr[i];
            }
            return Sum;
        }

        int sum = 0;
        for(int i = start; i < arr.Length; i++)
        {
          sum = sum + arr[i];
        }
        // Find the sum of array elements
        // over the range [start, N]
        int total = sum;

        // Checking if the current state is
        // previously calculated or not

        // If yes then return that value
        if(dp.ContainsKey(key))
        {
            return dp[key];
        }
        int psa = 0;
        // Traverse over the range [1, 2 * M]
        for(int x = 1; x < 2 * M + 1; x++)
        {
            // Sum of elements for Player A
            int psb = recursiveChoosing(arr, start + x, Math.Max(x, M), dp);
            // Even chance sum can be obtained
            // by subtracting the odd chances
            // sum - total and picking up the
            // maximum from that
            psa = Math.Max(psa, total - psb);
        }

        // Storing the value in dictionary
        dp[key] = psa;

        // Return the maximum sum of odd chances
        return dp[key];
    }

  // Driver code
  static void Main()
  {
    int[] arr = {2, 7, 9, 4, 4};
    int N = arr.Length;

    // Stores the precomputed values
    Dictionary<Tuple<int,int>,int> dp = new Dictionary<Tuple<int,int>,int>();

    // Function Call
    Console.Write(recursiveChoosing(arr, 0, 1, dp));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the maximum sum of
    // array elements chosen by Player A
    // according to the given criteria
    function recursiveChoosing(arr, start, M, dp)
    {
        // Store the key
        let key = [start, M];

        // Corner Case
        if(start >= N)
        {
            return 0;
        }

        // Check if all the elements can
        // be taken or not
        if(N - start <= 2 * M)
        {
            // If the difference is less than
            // or equal to the available
            // chances then pick all numbers
            let sum = 0;
            for(let i = start; i < arr.length; i++)
            {
                sum = sum + arr[i];
            }
            return sum;
        }

        let psa = 0;
        let sum = 0;
        for(let i = start; i < arr.length; i++)
        {
          sum = sum + arr[i];
        }
        // Find the sum of array elements
        // over the range [start, N]
        let total = sum;

        // Checking if the current state is
        // previously calculated or not

        // If yes then return that value
        if(dp.has(key))
        {
            return dp[key];
        }

        // Traverse over the range [1, 2 * M]
        for(let x = 1; x < 2 * M + 1; x++)
        {
            // Sum of elements for Player A
            let psb = recursiveChoosing(arr,
                              start + x, Math.max(x, M), dp)

            // Even chance sum can be obtained
            // by subtracting the odd chances
            // sum - total and picking up the
            // maximum from that
            psa = Math.max(psa, total - psb);
        }

        // Storing the value in dictionary
        dp[key] = psa;

        // Return the maximum sum of odd chances
        return dp[key];
    }

    let arr = [2, 7, 9, 4, 4];
    let N = arr.length;

    // Stores the precomputed values
    let dp = new Map();

    // Function Call
    document.write(recursiveChoosing(arr, 0, 1, dp))

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(K*N <sup>2</sup> ，其中 **K** 超出范围**【1，2 * M】***
***辅助空间:** O(N <sup>2</sup> )*
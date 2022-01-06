# 可领取批量分发的 K 号新鲜甜甜圈的最大组数

> 原文:[https://www . geeksforgeeks . org/最大可接收组数-新鲜甜甜圈-批量分发-大小-k/](https://www.geeksforgeeks.org/maximum-number-of-groups-that-can-receive-fresh-donuts-distributed-in-batches-of-size-k/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，使得**arr【I】**表示坐在甜甜圈店中的 **i <sup>第</sup>** 组的大小，以及一个正整数 **K** ，它表示一批可以提供的最大甜甜圈数量，任务是找到如果同一组的顾客一起提供，可以获得新鲜甜甜圈的最大组数。

***注:**一组的所有顾客都不会收到上一批吃剩的甜甜圈。*

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，K = 3
> **输出:** 4
> **解释:**组排序的一种可能方式是{6，2，4，5，1，3}。
> 
> 1.  商店供应两批 3 个甜甜圈。所以每个人都能吃到新鲜的甜甜圈。
> 2.  这家商店供应 3 个新鲜的甜甜圈，其中 1 个被漏掉了。所以每个人都能吃到新鲜的甜甜圈。
> 3.  这家商店先供应 1 个剩余的甜甜圈，然后供应 3 个新鲜的甜甜圈。
> 4.  这家商店供应 6 个新鲜的甜甜圈，其中 1 个被遗漏了。所以每个人都能吃到新鲜的甜甜圈。
> 5.  这家商店供应 1 个剩余的甜甜圈。
> 6.  这家商店供应 3 个新鲜的甜甜圈。所以每个人都能吃到新鲜的甜甜圈。
> 
> 因此，总共有 4 组获得新鲜的甜甜圈，这是最大可能的组数。
> 
> **输入:** arr[] = {1，3，2，5，2，2，1，6}，K = 4
> **输出:** 4

**天真方法:**给定的问题可以通过使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决所有可能的排序，这是基于观察到每个组大小的剩余部分只需要考虑 **K** 。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如说 **K** 大小的 **V[]** ，其中 **V[i]** 表示剩余 **i** 人的组数。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，对于每个 **arr[i]、**将**V【arr[I]% K】**的值增加 **1** 。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)说 **dfs(V，左)**到**离开的地方**是前一批剩下的甜甜圈的数量:
    *   初始化一个变量，将 **res** 设为 **0** ，以存储当前状态的结果。
    *   如果**左侧**的值为 **0** ，则[使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，K–1】**内迭代，并执行以下步骤:
        *   将**V【I】**的值减 **1** 并递归调用带参数**左-i.** 的函数
        *   将 **res** 更新为最大 **dfs(V，左–I)+1**和 **res** 。
        *   对于回溯步骤，将 **V[i]** 的值增加 **1** 。
    *   否则，重复与上述相同的步骤，但在这种情况下，不要将 **1** 添加到结果中，因为选定的组将获得剩余的甜甜圈。
    *   返回 **res** 的值。
*   调用上面定义为 **dfs(V，0)** 的递归函数，并将返回值存储在一个变量中，比如 **X** 。
*   最后，完成上述步骤后，打印**V【0】**和 **X** 的和作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find the
// maximum number of groups that
// will receive fresh donuts
int dfs(int arr[], int left, int K)
{

    // Store the result for the
    // current state
    int q = 0;

    // Check if the leftover donuts
    // from the previous batch is 0
    if (left == 0) {

        // If true, then one by one
        // give the fresh donuts
        // to each group
        for (int i = 1; i < K; ++i) {
            if (arr[i] > 0) {

                // Decrement arr[i]
                arr[i]--;

                // Update the maximum
                // number of groups
                q = max(q, 1 + dfs(arr, K - i, K));

                // Increment arr[i]
                arr[i]++;
            }
        }
    }

    // Otherwise, traverse the given
    // array, arr[]
    else {

        for (int i = 1; i < K; ++i) {
            if (arr[i] > 0) {

                // Decrement arr[i]
                arr[i]--;

                int nleft
                    = (i <= left ? left - i : K + left - i);

                // Update the maximum
                // number of groups
                q = max(q, dfs(arr, nleft, K));

                // Increment arr[i]
                arr[i]++;
            }
        }
    }

    // Return the value of q
    return q;
}

// Function to find the maximum
// number of groups that will
// receive fresh donuts
int maxGroups(int K, int arr[], int n)
{

    // Stores count of remainder
    // by K
    int V[K] = { 0 };

    // Traverse the array arr[]
    for (int x = 0; x < n; x++)
        V[arr[x] % K]++;

    // Stores maximum number of groups
    int ans = V[0] + dfs(V, 0, K);

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    cout << maxGroups(K, arr, n);

    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Recursive function to find the
    // maximum number of groups that
    // will receive fresh donuts
    public static int dfs(int[] arr,
                          int left, int K)
    {
        // Store the result for the
        // current state
        int q = 0;

        // Check if the leftover donuts
        // from the previous batch is 0
        if (left == 0) {

            // If true, then one by one
            // give the fresh donuts
            // to each group
            for (int i = 1; i < K; ++i) {
                if (arr[i] > 0) {

                    // Decrement arr[i]
                    arr[i]--;

                    // Update the maximum
                    // number of groups
                    q = Math.max(
                        q, 1 + dfs(arr, K - i, K));

                    // Increment arr[i]
                    arr[i]++;
                }
            }
        }

        // Otherwise, traverse the given
        // array, arr[]
        else {

            for (int i = 1; i < K; ++i) {
                if (arr[i] > 0) {

                    // Decrement arr[i]
                    arr[i]--;

                    int nleft = (i <= left ? left - i
                                           : K + left - i);

                    // Update the maximum
                    // number of groups
                    q = Math.max(q, dfs(arr, nleft, K));

                    // Increment arr[i]
                    arr[i]++;
                }
            }
        }

        // Return the value of q
        return q;
    }

    // Function to find the maximum
    // number of groups that will
    // receive fresh donuts
    public static int maxGroups(int K,
                                int[] arr)
    {
        // Stores count of remainder
        // by K
        int V[] = new int[K];

        // Traverse the array arr[]
        for (int x : arr)
            V[x % K]++;

        // Stores maximum number of groups
        int ans = V[0] + dfs(V, 0, K);

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int K = 3;
        System.out.println(
            maxGroups(K, arr));
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Recursive function to find the
# maximum number of groups that
# will receive fresh donuts
def dfs(arr, left, K):

    # Store the result for the
    # current state
    q = 0

    # Check if the leftover donuts
    # from the previous batch is 0
    if (left == 0):

        # If true, then one by one
        # give the fresh donuts
        # to each group
        for i in range(1,K,1):
            if (arr[i] > 0):

                # Decrement arr[i]
                arr[i] -= 1

                # Update the maximum
                # number of groups
                q = max(q, 1 + dfs(arr, K - i, K))

                # Increment arr[i]
                arr[i] += 1

    # Otherwise, traverse the given
    # array, arr[]
    else:

        for i in range(1,K,1):
            if (arr[i] > 0):

                # Decrement arr[i]
                arr[i] -= 1

                nleft = left - i if i <= left else K + left - i

                # Update the maximum
                # number of groups
                q = max(q, dfs(arr, nleft, K))

                # Increment arr[i]
                arr[i] += 1

    # Return the value of q
    return q

# Function to find the maximum
# number of groups that will
# receive fresh donuts
def maxGroups(K, arr, n):

    # Stores count of remainder
    # by K
    V = [0 for i in range(K)]

    # Traverse the array arr[]
    for x in range(n):
        V[arr[x] % K] += 1

    # Stores maximum number of groups
    ans = V[0] + dfs(V, 0, K)

    # Return the answer
    return ans

# Driver Code
if __name__ == '__main__':
    arr= [1, 2, 3, 4, 5, 6]
    n = len(arr)
    K = 3

    print(maxGroups(K, arr, n))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Recursive function to find the
// maximum number of groups that
// will receive fresh donuts
public static int dfs(int[] arr,
                      int left, int K)
{

    // Store the result for the
    // current state
    int q = 0;

    // Check if the leftover donuts
    // from the previous batch is 0
    if (left == 0)
    {

        // If true, then one by one
        // give the fresh donuts
        // to each group
        for(int i = 1; i < K; ++i)
        {
            if (arr[i] > 0)
            {

                // Decrement arr[i]
                arr[i]--;

                // Update the maximum
                // number of groups
                q = Math.Max(q, 1 + dfs(arr, K - i, K));

                // Increment arr[i]
                arr[i]++;
            }
        }
    }

    // Otherwise, traverse the given
    // array, arr[]
    else
    {
        for(int i = 1; i < K; ++i)
        {
            if (arr[i] > 0)
            {

                // Decrement arr[i]
                arr[i]--;

                int nleft = (i <= left ? left - i :
                             K + left - i);

                // Update the maximum
                // number of groups
                q = Math.Max(q, dfs(arr, nleft, K));

                // Increment arr[i]
                arr[i]++;
            }
        }
    }

    // Return the value of q
    return q;
}

// Function to find the maximum
// number of groups that will
// receive fresh donuts
public static int maxGroups(int K, int[] arr)
{

    // Stores count of remainder
    // by K
    int[] V = new int[K];

    // Traverse the array arr[]
    foreach(int x in arr)
        V[x % K]++;

    // Stores maximum number of groups
    int ans = V[0] + dfs(V, 0, K);

    // Return the answer
    return ans;
}

// Driver code
public static void Main(string[] args)
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int K = 3;

    Console.WriteLine(maxGroups(K, arr));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Recursive function to find the
// maximum number of groups that
// will receive fresh donuts
function dfs(arr, left, K)
{

    // Store the result for the
    // current state
    let q = 0;

    // Check if the leftover donuts
    // from the previous batch is 0
    if (left == 0)
    {

        // If true, then one by one
        // give the fresh donuts
        // to each group
        for(let i = 1; i < K; ++i)
        {
            if (arr[i] > 0)
            {

                // Decrement arr[i]
                arr[i]--;

                // Update the maximum
                // number of groups
                q = Math.max(q, 1 + dfs(arr, K - i, K));

                // Increment arr[i]
                arr[i]++;
            }
        }
    }

    // Otherwise, traverse the given
    // array, arr[]
    else
    {
        for(let i = 1; i < K; ++i)
        {
            if (arr[i] > 0)
            {

                // Decrement arr[i]
                arr[i]--;

                let nleft = (i <= left ? left - i :
                              K + left - i);

                // Update the maximum
                // number of groups
                q = Math.max(q, dfs(arr, nleft, K));

                // Increment arr[i]
                arr[i]++;
            }
        }
    }

    // Return the value of q
    return q;
}

// Function to find the maximum
// number of groups that will
// receive fresh donuts
function maxGroups(K, arr, n)
{

    // Stores count of remainder
    // by K
    let V = new Array(K).fill(0);

    // Traverse the array arr[]
    for(let x = 0; x < n; x++)
        V[arr[x] % K]++;

    // Stores maximum number of groups
    let ans = V[0] + dfs(V, 0, K);

    // Return the answer
    return ans;
}

// Driver Code
let arr = [ 1, 2, 3, 4, 5, 6 ];
let n = arr.length;
let K = 3;

document.write(maxGroups(K, arr, n))

// This code is contributed by _Saurabh_jaiswal

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N+K<sup>K</sup>)*
***辅助空间:** O(K)*

**高效方法:**上述方法具有[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，因此，上述方法也可以通过[在](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/) [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中记忆相同的[递归调用](https://www.geeksforgeeks.org/recursion/)并在递归调用相同问题时使用该状态来优化。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the result of the same
// recursive calls
map<string, int> memo;

// Recursive function to find the
// maximum number of groups that
// will receive fresh donuts
int dfs(int V[], int left, int K)
{

    // Store the result for the
    // current state
    int q = 0;

    // Store the key and check
    // if it is present in the
    // hashmap
    string key = "";
    for(int i = 0; i < K; i++)
    {
        key = key + to_string(V[i]);
    }
    key += to_string(left);
    // If already calculated
    if (memo.find(key) != memo.end())
        return memo[key];

    // If left is 0
    else if (left == 0) {

        // Traverse the array []arr
        for (int i = 1; i < K; ++i)
            if (V[i] > 0) {

                // Decrement arr[i]
                V[i]--;

                // Update the maximum
                // number of groups
                q = max(q, 1 + dfs(V, K - i, K));

                // Increment arr[i] by 1
                V[i]++;
            }
    }

    // Otherwise, traverse the given
    // array []arr
    else {

        for (int i = 1; i < K; ++i) {
            if (V[i] > 0) {

                // Decrement arr[i]
                V[i]--;

                int nleft = i <= left ? left - i : K + left - i;

                // Update the maximum
                // number of groups
                q = max(q, dfs(V, nleft, K));

                // Increment arr[i] by 1
                V[i]++;
            }
        }
    }

    // Memoize the result and
    // return it
    if(memo.find(key) != memo.end())
        memo[key] = q;
    else
        memo[key] = q;

    return q;
}

// Function to find the maximum
// number of groups that will
// receive fresh donuts
int maxGroups(int K, int arr[])
{

    // Stores count of remainder by K
    int V[K];
    memset(V, 0, sizeof(V));

    // Traverse the array []arr
    for (int i = 0; i < 6; i++)
        V[arr[i] % K]++;

    // Store the maximum number
    // of groups
    int ans = V[0] + dfs(V, 0, K);

    // Return the answer
    return ans;
}

int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int K = 3;
    cout << maxGroups(K, arr);

    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Stores the result of the same
    // recursive calls
    static HashMap<String, Integer> memo;

    // Recursive function to find the
    // maximum number of groups that
    // will receive fresh donuts
    public static int dfs(int[] V,
                          int left, int K)
    {
        // Store the result for the
        // current state
        int q = 0;

        // Store the key and check
        // if it is present in the
        // hashmap
        String key = Arrays.toString(V);
        key += Integer.toString(left);

        // If already calculated
        if (memo.containsKey(key))
            return memo.get(key);

        // If left is 0
        else if (left == 0) {

            // Traverse the array arr[]
            for (int i = 1; i < K; ++i)
                if (V[i] > 0) {

                    // Decrement arr[i]
                    V[i]--;

                    // Update the maximum
                    // number of groups
                    q = Math.max(
                        q, 1 + dfs(V, K - i, K));

                    // Increment arr[i] by 1
                    V[i]++;
                }
        }

        // Otherwise, traverse the given
        // array arr[]
        else {

            for (int i = 1; i < K; ++i) {
                if (V[i] > 0) {

                    // Decrement arr[i]
                    V[i]--;

                    int nleft = i <= left ? left - i
                                          : K + left - i;

                    // Update the maximum
                    // number of groups
                    q = Math.max(q, dfs(V, nleft, K));

                    // Increment arr[i] by 1
                    V[i]++;
                }
            }
        }

        // Memoize the result and
        // return it
        memo.put(key, q);

        return q;
    }

    // Function to find the maximum
    // number of groups that will
    // receive fresh donuts
    public static int maxGroups(int K, int[] arr)
    {
        // Stores count of remainder by K
        int V[] = new int[K];

        // Traverse the array arr[]
        for (int x : arr)
            V[x % K]++;

        // Hashmap to memoize the results
        memo = new HashMap<String, Integer>();

        // Store the maximum number
        // of groups
        int ans = V[0] + dfs(V, 0, K);

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int K = 3;
        System.out.println(
            maxGroups(K, arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the result of the same
# recursive calls
memo = {}

# Recursive function to find the
# maximum number of groups that
# will receive fresh donuts
def dfs(V, left, K):

    # Store the result for the
    # current state
    q = 0

    # Store the key and check
    # if it is present in the
    # hashmap
    v = [str(int) for int in V]
    key = ",".join(v)

    key += str(left)

    # If already calculated
    if key in memo:
        return memo[key]

    # If left is 0
    elif left == 0:

        # Traverse the array []arr
        for i in range(1, K):
            if V[i] > 0:

                # Decrement arr[i]
                V[i]-=1

                # Update the maximum
                # number of groups
                q = max(q, 1 + dfs(V, K - i, K))

                # Increment arr[i] by 1
                V[i]+=1

    # Otherwise, traverse the given
    # array []arr
    else:
        for i in range(1, K):
            if V[i] > 0:
                # Decrement arr[i]
                V[i]-=1

                if i <= left:
                    nleft = left - i
                else:
                    nleft = K + left - i

                # Update the maximum
                # number of groups
                q = max(q, dfs(V, nleft, K))

                # Increment arr[i] by 1
                V[i]+=1

    # Memoize the result and
    # return it
    if key in memo:
        memo[key] = q
    else:
        memo[key] = q

    return q

# Function to find the maximum
# number of groups that will
# receive fresh donuts
def maxGroups(K, arr):

    # Stores count of remainder by K
    V = [0]*(K)

    # Traverse the array []arr
    for x in range(len(arr)):
        V[arr[x] % K] += 1

    # Hashmap to memoize the results
    memo = {}

    # Store the maximum number
    # of groups
    ans = V[0] + dfs(V, 0, K)

    # Return the answer
    return ans

arr = [ 1, 2, 3, 4, 5, 6 ]
K = 3
print(maxGroups(K, arr))

# This code is contributed by divyesh072019.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Stores the result of the same
    // recursive calls
    static Dictionary<String, int> memo;

    // Recursive function to find the
    // maximum number of groups that
    // will receive fresh donuts
    public static int dfs(int[] V,
                          int left, int K)
    {
        // Store the result for the
        // current state
        int q = 0;

        // Store the key and check
        // if it is present in the
        // hashmap
        String key = string.Join(",", V);
        key += left.ToString();
        // If already calculated
        if (memo.ContainsKey(key))
            return memo[key];

        // If left is 0
        else if (left == 0) {

            // Traverse the array []arr
            for (int i = 1; i < K; ++i)
                if (V[i] > 0) {

                    // Decrement arr[i]
                    V[i]--;

                    // Update the maximum
                    // number of groups
                    q = Math.Max(
                        q, 1 + dfs(V, K - i, K));

                    // Increment arr[i] by 1
                    V[i]++;
                }
        }

        // Otherwise, traverse the given
        // array []arr
        else {

            for (int i = 1; i < K; ++i) {
                if (V[i] > 0) {

                    // Decrement arr[i]
                    V[i]--;

                    int nleft = i <= left ? left - i
                                          : K + left - i;

                    // Update the maximum
                    // number of groups
                    q = Math.Max(q, dfs(V, nleft, K));

                    // Increment arr[i] by 1
                    V[i]++;
                }
            }
        }

        // Memoize the result and
        // return it
        if(memo.ContainsKey(key))
            memo[key] = q;
        else
            memo.Add(key, q);

        return q;
    }

    // Function to find the maximum
    // number of groups that will
    // receive fresh donuts
    public static int maxGroups(int K, int[] arr)
    {

        // Stores count of remainder by K
        int []V = new int[K];

        // Traverse the array []arr
        foreach (int x in arr)
            V[x % K]++;

        // Hashmap to memoize the results
        memo = new Dictionary<String, int>();

        // Store the maximum number
        // of groups
        int ans = V[0] + dfs(V, 0, K);

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int K = 3;
        Console.WriteLine(
            maxGroups(K, arr));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Stores the result of the same
    // recursive calls
    let memo;

    // Recursive function to find the
    // maximum number of groups that
    // will receive fresh donuts
    function dfs(V, left, K)
    {

        // Store the result for the
        // current state
        let q = 0;

        // Store the key and check
        // if it is present in the
        // hashmap
        let key = V.join(",");
        key += left.toString();

        // If already calculated
        if (memo.has(key))
            return memo[key];

        // If left is 0
        else if (left == 0) {

            // Traverse the array []arr
            for (let i = 1; i < K; ++i)
                if (V[i] > 0) {

                    // Decrement arr[i]
                    V[i]--;

                    // Update the maximum
                    // number of groups
                    q = Math.max(q, 1 + dfs(V, K - i, K));

                    // Increment arr[i] by 1
                    V[i]++;
                }
        }

        // Otherwise, traverse the given
        // array []arr
        else {

            for (let i = 1; i < K; ++i) {
                if (V[i] > 0) {

                    // Decrement arr[i]
                    V[i]--;

                    let nleft = i <= left ? left - i : K + left - i;

                    // Update the maximum
                    // number of groups
                    q = Math.max(q, dfs(V, nleft, K));

                    // Increment arr[i] by 1
                    V[i]++;
                }
            }
        }

        // Memoize the result and
        // return it
        if(memo.has(key))
            memo[key] = q;
        else
            memo[key] = q;

        return q;
    }

    // Function to find the maximum
    // number of groups that will
    // receive fresh donuts
    function maxGroups(K, arr)
    {

        // Stores count of remainder by K
        let V = new Array(K);
        V.fill(0);

        // Traverse the array []arr
        for(let x = 0; x < arr.length; x++)
            V[arr[x] % K]++;

        // Hashmap to memoize the results
        memo = new Map();

        // Store the maximum number
        // of groups
        let ans = V[0] + dfs(V, 0, K);

        // Return the answer
        return ans;
    }

    let arr = [ 1, 2, 3, 4, 5, 6 ];
      let K = 3;
      document.write(maxGroups(K, arr));

    // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N+K<sup>2</sup>)*
***辅助空间:** O(K)*
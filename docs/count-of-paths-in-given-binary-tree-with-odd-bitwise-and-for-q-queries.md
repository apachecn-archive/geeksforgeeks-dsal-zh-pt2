# 给定二叉树中 Q 查询的奇数位“与”路径计数

> 原文:[https://www . geeksforgeeks . org/给定二叉树中带有 q 查询的奇数位运算路径计数/](https://www.geeksforgeeks.org/count-of-paths-in-given-binary-tree-with-odd-bitwise-and-for-q-queries/)

给定一个代表查询数量的整数 Q 和一个数组，其中每个查询都有一个整数 N。我们的任务是迭代每个查询并找到路径的数量，使得该路径上所有节点的按位“与”为奇数。

> 二叉树由编号为 1 到 N 的 N 个顶点构成，对于每个 I，从 2 到 N，在**顶点 I 和顶点 i / 2(四舍五入)**之间有一条边。

**示例:**

```
Input: Q = 2, [5, 2]
Output: 1 0
Explanation: 
For first query the binary tree will be 
        1
      /   \ 
     2     3
   /   \
  4     5
The path which satisfies
the condition is 1 -> 3.
Hence only 1 path.
For the second query,
the binary tree will be 
        1
       /
      2 
There no such path that
satisfies the condition.

Input: Q = 3, [3, 7, 13]
Output: 1 3 4 
```

**方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和**对查询中从 1 到最大值 N 的所有值的答案进行预计算**。

*   首先，观察如果路径的按位“与”是奇数，那么该路径的所有元素都不能是偶数。因此，所需的路径应该具有奇数元素。
*   我们知道，对于第 i <sup>个</sup>节点(除了节点 1)，父节点将是 i/2(四舍五入)。维护一个 **dp 数组**，用于存储第 i <sup>个</sup>节点的答案。另一个数组将用于存储当前节点的奇数个元素，直到父节点为奇数。
*   在计算 dp 数组时，第一个条件是如果第 i <sup>个</sup>节点值为偶数，那么**dp[i]= DP[I–1]**因为第 i <sup>个</sup>节点不会对答案有贡献，所以 DP[I]将是第(i-1) <sup>个</sup>节点的答案。其次，如果第 i <sup>个</sup>节点是奇数，那么 dp[i] = dp[i-1] + nC2 -(n-1)C2。关于简化 **dp[i] = dp[i-1] +(至今奇数元素数)–1。**

下面是上述方法的实现:

## C++

```
// C++ implementation to count
// paths in Binary Tree
// with odd bitwise AND

#include <bits/stdc++.h>
using namespace std;

// Function to count number of paths
// in binary tree such that bitwise
// AND of all nodes is Odd
void compute(vector<int> query)
{
    // vector v for storing
    // the count of odd numbers

    // vector dp to store the
    // count of bitwise odd paths
    // till that vertex
    vector<int> v(100001), dp(100001);

    v[1] = 1, v[2] = 0;
    dp[1] = 0, dp[2] = 0;

    // Precomputing for each value
    for (int i = 3; i < 100001; i++) {
        // check for odd value
        if (i % 2 != 0) {
            if ((i / 2) % 2 == 0) {
                v[i] = 1;
                dp[i] = dp[i - 1];
            }

            else {
                // Number of odd elements will
                // be +1 till the parent node
                v[i] = v[i / 2] + 1;
                dp[i] = dp[i - 1] + v[i] - 1;
            }
        }

        // For even case
        else {
            // Since node is even
            // Number of odd elements
            // will be 0
            v[i] = 0;

            // Even value node will
            // not contribute in answer
            // hence dp[i] = previous answer
            dp[i] = dp[i - 1];
        }
    }
    // Printing the answer
    // for each query
    for (auto x : query)
        cout << dp[x] << endl;
}

// Driver code
int main()
{
    // vector to store queries
    vector<int> query = { 5, 2 };
    compute(query);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// paths in Binary Tree
// with odd bitwise AND
class GFG{

// Function to count number of paths
// in binary tree such that bitwise
// AND of all nodes is Odd
static void compute(int[] query)
{

    // v for storing the count
    // of odd numbers

    // dp to store the count of
    // bitwise odd paths
    // till that vertex
    int []v = new int[100001];
    int []dp = new int[100001];

    v[1] = 1; v[2] = 0;
    dp[1] = 0; dp[2] = 0;

    // Precomputing for each value
    for(int i = 3; i < 100001; i++)
    {

       // Check for odd value
       if (i % 2 != 0)
       {
           if ((i / 2) % 2 == 0)
           {
               v[i] = 1;
               dp[i] = dp[i - 1];
           }
           else
           {

               // Number of odd elements will
               // be +1 till the parent node
               v[i] = v[i / 2] + 1;
               dp[i] = dp[i - 1] + v[i] - 1;
           }
       }

       // For even case
       else
       {

           // Since node is even
           // Number of odd elements
           // will be 0
           v[i] = 0;

           // Even value node will
           // not contribute in answer
           // hence dp[i] = previous answer
           dp[i] = dp[i - 1];
       }
    }

    // Printing the answer
    // for each query
    for(int x : query)
       System.out.print(dp[x] + "\n");
}

// Driver code
public static void main(String[] args)
{

    // To store queries
    int []query = { 5, 2 };

    compute(query);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to count
# paths in Binary Tree with odd
# bitwise AND

# Function to count number of paths
# in binary tree such that bitwise
# AND of all nodes is Odd
def compute(query):

    # vector v for storing
    # the count of odd numbers

    # vector dp to store the
    # count of bitwise odd paths
    # till that vertex
    v = [None] * 100001
    dp = [None] * 100001

    v[1] = 1
    v[2] = 0
    dp[1] = 0
    dp[2] = 0

    # Precomputing for each value
    for i in range(3, 100001):

        # Check for odd value
        if (i % 2 != 0):
            if ((i // 2) % 2 == 0):
                v[i] = 1
                dp[i] = dp[i - 1]

            else:

                # Number of odd elements will
                # be +1 till the parent node
                v[i] = v[i // 2] + 1
                dp[i] = dp[i - 1] + v[i] - 1

        # For even case
        else:

            # Since node is even
            # Number of odd elements
            # will be 0
            v[i] = 0

            # Even value node will
            # not contribute in answer
            # hence dp[i] = previous answer
            dp[i] = dp[i - 1]

    # Printing the answer
    # for each query
    for x in query:
        print(dp[x])

# Driver code

# Vector to store queries
query = [ 5, 2 ]

compute(query)

# This code is contributed by sanjoy_62
```

## C#

```
// C# implementation to count
// paths in Binary Tree
// with odd bitwise AND
using System;

class GFG{

// Function to count number of paths
// in binary tree such that bitwise
// AND of all nodes is Odd
static void compute(int[] query)
{

    // v for storing the count
    // of odd numbers

    // dp to store the count of
    // bitwise odd paths
    // till that vertex
    int []v = new int[100001];
    int []dp = new int[100001];

    v[1] = 1; v[2] = 0;
    dp[1] = 0; dp[2] = 0;

    // Precomputing for each value
    for(int i = 3; i < 100001; i++)
    {

        // Check for odd value
        if (i % 2 != 0)
        {
            if ((i / 2) % 2 == 0)
            {
                v[i] = 1;
                dp[i] = dp[i - 1];
            }
            else
            {

                // Number of odd elements will
                // be +1 till the parent node
                v[i] = v[i / 2] + 1;
                dp[i] = dp[i - 1] + v[i] - 1;
            }
        }

        // For even case
        else
        {

            // Since node is even
            // Number of odd elements
            // will be 0
            v[i] = 0;

            // Even value node will
            // not contribute in answer
            // hence dp[i] = previous answer
            dp[i] = dp[i - 1];
        }
    }

    // Printing the answer
    // for each query
    foreach(int x in query)
    Console.Write(dp[x] + "\n");
}

// Driver code
public static void Main(String[] args)
{

    // To store queries
    int []query = { 5, 2 };

    compute(query);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to count
// paths in Binary Tree
// with odd bitwise AND

// Function to count number of paths
// in binary tree such that bitwise
// AND of all nodes is Odd
function compute(query)
{
    // vector v for storing
    // the count of odd numbers

    // vector dp to store the
    // count of bitwise odd paths
    // till that vertex
    var v = Array(100001).fill(0);
    var dp = Array(100001).fill(0);

    v[1] = 1, v[2] = 0;
    dp[1] = 0, dp[2] = 0;

    // Precomputing for each value
    for (var i = 3; i < 100001; i++) {
        // check for odd value
        if (i % 2 != 0) {
            if (parseInt(i / 2) % 2 == 0) {
                v[i] = 1;
                dp[i] = dp[i - 1];
            }

            else {
                // Number of odd elements will
                // be +1 till the parent node
                v[i] = v[parseInt(i / 2)] + 1;
                dp[i] = dp[i - 1] + v[i] - 1;
            }
        }

        // For even case
        else {
            // Since node is even
            // Number of odd elements
            // will be 0
            v[i] = 0;

            // Even value node will
            // not contribute in answer
            // hence dp[i] = previous answer
            dp[i] = dp[i - 1];
        }
    }
    // Printing the answer
    // for each query
    query.forEach(x => {

        document.write( dp[x] + "<br>");
    });
}

// Driver code
// vector to store queries
var query = [5, 2];
compute(query);

</script>
```

**Output:** 

```
1
0
```

***时间复杂度:** O( Nmax + Q*(1) )* ，其中 Nmax 是 N. Q*(1)的最大值，因为我们正在预计算每个查询。
***辅助空间** : O(Nmax)*
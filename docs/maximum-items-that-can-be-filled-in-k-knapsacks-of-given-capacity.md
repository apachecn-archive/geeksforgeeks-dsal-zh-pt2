# 给定容量的 K 个背包中能装的最大项目数

> 原文:[https://www . geeksforgeeks . org/给定容量的 k 个背包中可填充的最大物品数/](https://www.geeksforgeeks.org/maximum-items-that-can-be-filled-in-k-knapsacks-of-given-capacity/)

给定一个由物品重量和容量为“C”的“K”个背包组成的整数数组 W[]，如果不允许打破物品，找到我们能放入背包的最大重量。

**示例:**

> **输入:** w[] = {3，9，8}，k = 1，c = 11
> **输出:** 11
> 所需子集将为{3，8}
> ，其中 3+8 = 11
> 
> **输入:** w[] = {3，9，8}，k = 1，c = 10
> T3】输出: 9

我们将用 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 来解决这个问题。
我们将使用两个变量来表示差压的状态。

1.  I’–我们正在研究的当前指数。
2.  它包含每个背包的剩余容量。

现在，单个变量将如何存储每个背包的剩余容量？
为此，我们将把“r”初始化为 r = c+c *(c+1)+c*(c+1)^2+c*(c+1)^3..+ C*(C+1)^(k-1)
这将使用容量“c”初始化所有“k”背包。

现在，我们需要执行两个查询:

*   读取 jth 背包剩余空间:(r/(c+1)^(j-1))%(c+1).
*   将 jth 背包剩余空间减少 x:集合 r = r–x*(c+1)^(j-1).

现在，在每一步，我们将有 k+1 个选择。

1.  拒绝索引“I”。
2.  将物品“I”放入背包 1。
3.  将物品“I”放入背包 2。
4.  将物品“I”放入背包 3。

我们将选择最大化结果的道路。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// 2-d array to store states of DP
vector<vector<int> > dp;

// 2-d array to store if a state
// has been solved
vector<vector<bool> > v;

// Vector to store power of variable 'C'.
vector<int> exp_c;

// function to compute the states
int FindMax(int i, int r, int w[],
            int n, int c, int k)
{

    // Base case
    if (i >= n)
        return 0;

    // Checking if a state has been solved
    if (v[i][r])
        return dp[i][r];

    // Setting a state as solved
    v[i][r] = 1;
    dp[i][r] = FindMax(i + 1, r, w, n, c, k);

    // Recurrence relation
    for (int j = 0; j < k; j++) {
        int x = (r / exp_c[j]) % (c + 1);
        if (x - w[i] >= 0)
            dp[i][r] = max(dp[i][r], w[i] +
            FindMax(i + 1, r - w[i] * exp_c[j], w, n, c, k));
    }

    // Returning the solved state
    return dp[i][r];
}

// Function to initialize global variables
// and find the initial value of 'R'
int PreCompute(int n, int c, int k)
{

    // Resizing the variables
    exp_c.resize(k);
    exp_c[0] = 1;

    for (int i = 1; i < k; i++){
        exp_c[i] = (exp_c[i - 1] * (c + 1));
    }
    dp.resize(n);
    for (int i = 0; i < n; i++){
        dp[i].resize(exp_c[k - 1] * (c + 1), 0);
    }
    v.resize(n);
    for (int i = 0; i < n; i++){
        v[i].resize(exp_c[k - 1] * (c + 1), 0);
    }

    // Variable to store the initial value of R
    int R = 0;
    for (int i = 0; i < k; i++){
        R += exp_c[i] * c;
    }
    return R;
}

// Driver Code
int main()
{
    // Input array
    int w[] = { 3, 8, 9 };

    // number of knapsacks and capacity
    int k = 1, c = 11;

    int n = sizeof(w) / sizeof(int);

    // Performing required pre-computation
    int r = PreCompute(n, c, k);

    // finding the required answer
    cout << FindMax(0, r, w, n, c, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.util.*;
class GFG
{

    // 2-d array to store if a state
    // has been solved
    static ArrayList<ArrayList<Boolean>> v =
      new ArrayList<ArrayList<Boolean>>();

    // 2-d array to store states of DP
    static ArrayList<ArrayList<Integer>> dp =
      new ArrayList<ArrayList<Integer>>();

    // Vector to store power of variable 'C'.
    static ArrayList<Integer> exp_c =
      new ArrayList<Integer>();

    // function to compute the states
    static int FindMax(int i, int r, int w[],
                       int n, int c, int k)
    {

        // Base case
        if (i >= n)
        {
            return 0;
        }

        // Checking if a state has been solved
        if(v.get(i).get(r))
        {
            return dp.get(i).get(r);
        }

        // Setting a state as solved
        v.get(i).set(r, true);
        dp.get(i).set(r,FindMax(i + 1, r,
                                w, n, c, k));

        // Recurrence relation
        for (int j = 0; j < k; j++)
        {
            int x = (r / exp_c.get(j)) % (c + 1);
            if (x - w[i] >= 0)
            {
                dp.get(i).set(r,Math.max(dp.get(i).get(r),w[i] +
                                         FindMax(i + 1, r - w[i] *
                                                 exp_c.get(j), w, n, c, k)));     
            } 
        }

        // Returning the solved state
        return dp.get(i).get(r);
    }

    // Function to initialize global variables
    // and find the initial value of 'R'
    static int PreCompute(int n, int c, int k)
    {

        // Resizing the variables
        for(int i = 0; i < k; i++)
        {
            exp_c.add(0);
        }
        exp_c.set(0, 1);
        for (int i = 1; i < k; i++)
        {
            exp_c.set(i,(exp_c.get(i - 1) * (c + 1)));

        }
        for (int i = 0; i < n; i++)
        {
            dp.add(new ArrayList<Integer>());
        }
        for (int i = 0; i < n; i++)
        {
            for(int j = 0; j < (exp_c.get(k-1) * (c + 1)) ; j++ )
            {
                dp.get(i).add(0);
            }
        }
        for (int i = 0; i < n; i++)
        {
            v.add(new ArrayList<Boolean>(Arrays.asList(
              new Boolean[(exp_c.get(k-1) * (c + 1))])));
        }
        for (int i = 0; i < n; i++)
        {
            Collections.fill(v.get(i), Boolean.FALSE);
        }

        // Variable to store the initial value of R
        int R = 0;
        for(int i = 0; i < k; i++)
        {
            R += exp_c.get(i) * c;           
        }
        return R;
    }

    // Driver Code
    public static void main (String[] args)
    {

        // Input array
        int w[] = { 3, 8, 9 };

        // number of knapsacks and capacity
        int k = 1, c = 11;
        int n = w.length;

        // Performing required pre-computation
        int r = PreCompute(n, c, k);

        // finding the required answer
        System.out.println(FindMax(0, r, w, n, c, k));
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# 2-d array to store states of DP
x = 100
dp = [[0 for i in range(x)]
         for i in range(x)]

# 2-d array to store if a state
# has been solved
v = [[0 for i in range(x)] 
        for i in range(x)]

# Vector to store power of variable 'C'.
exp_c = []

# function to compute the states
def FindMax(i, r, w, n, c, k):

    # Base case
    if (i >= n):
        return 0

    # Checking if a state has been solved
    if (v[i][r]):
        return dp[i][r]

    # Setting a state as solved
    v[i][r] = 1
    dp[i][r] = FindMax(i + 1, r, w, n, c, k)

    # Recurrence relation
    for j in range(k):
        x = (r // exp_c[j]) % (c + 1)
        if (x - w[i] >= 0):
            dp[i][r] = max(dp[i][r], w[i] +
            FindMax(i + 1, r - w[i] * exp_c[j],
                                   w, n, c, k))

    # Returning the solved state
    return dp[i][r]

# Function to initialize global variables
# and find the initial value of 'R'
def PreCompute(n, c, k):

    # Resizing the variables
    exp_c.append(1)

    for i in range(1, k):
        exp_c[i] = (exp_c[i - 1] * (c + 1))

    # Variable to store the initial value of R
    R = 0
    for i in range(k):
        R += exp_c[i] * c

    return R

# Driver Code

# Input array
w =[3, 8, 9]

# number of knapsacks and capacity
k = 1
c = 11

n = len(w)

# Performing required pre-computation
r = PreCompute(n, c, k)

# finding the required answer
print(FindMax(0, r, w, n, c, k))

# This code is contributed by Mohit Kumar
```

## C#

```
using System;
using System.Collections.Generic;

class GFG{

// 2-d array to store if a state
// has been solved
static List<List<bool>> v = new List<List<bool>>();

// 2-d array to store states of DP
static List<List<int>> dp = new List<List<int>>();

// Vector to store power of variable 'C'.
static List<int> exp_c = new List<int>();

// Function to compute the states
static int FindMax(int i, int r, int[] w,
                   int n, int c, int k)
{

    // Base case
    if (i >= n)
    {
        return 0;
    }

    // Checking if a state has been solved
    if (v[i][r])
    {
        return dp[i][r];
    }

    // Setting a state as solved
    v[i][r] = true;
    dp[i][r] = FindMax(i + 1, r, w, n, c, k);

    // Recurrence relation
    for(int j = 0; j < k; j++)
    {
        int x = (r / exp_c[j]) % (c + 1);

        if (x - w[i] >= 0)
        {
            dp[i][r] = Math.Max(dp[i][r], w[i] +
                                FindMax(i + 1,
                                        r - w[i] *
                                        exp_c[j],
                                        w, n, c, k));
        }
    }

    // Returning the solved state
    return dp[i][r];
}

// Function to initialize global variables
// and find the initial value of 'R'
static int PreCompute(int n, int c, int k)
{

    // Resizing the variables
    for(int i = 0; i < k; i++)
    {
        exp_c.Add(0);
    }

    exp_c[0] = 1;
    for(int i = 1; i < k; i++)
    {
        exp_c[i] = (exp_c[i - 1] * (c + 1));
    }

    for(int i = 0; i < n; i++)
    {
        dp.Add(new List<int>());
    }

    for(int i = 0; i < n; i++)
    {
        for(int j = 0;
                j < (exp_c[k - 1] * (c + 1));
                j++ )
        {
            dp[i].Add(0);
        }
    }

    for(int i = 0; i < n; i++)
    {
        v.Add(new List<bool>());
    }

    for(int i = 0; i < n; i++)
    {
        for(int j = 0;
                j < (exp_c[k - 1] * (c + 1));
                j++ )
        {
            v[i].Add(false);
        }
    }

    // Variable to store the initial value of R
    int R = 0;
    for(int i = 0; i < k; i++)
    {
        R += exp_c[i] * c;
    }
    return R;
}

// Driver code
static public void Main()
{

    // Input array
    int[] w = { 3, 8, 9 };

    // number of knapsacks and capacity
    int k = 1, c = 11;
    int n = w.Length;

    // Performing required pre-computation
    int r = PreCompute(n, c, k);

    // finding the required answer
    Console.WriteLine(FindMax(0, r, w, n, c, k));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
    // 2-d array to store if a state
    // has been solved
    let v =[];

    // 2-d array to store states of DP
    let dp =[];

    // Vector to store power of variable 'C'.
    let  exp_c =[];

    // function to compute the states
    function FindMax(i,r,w,n,c,k)
    {
        // Base case
        if (i >= n)
        {
            return 0;
        }

        // Checking if a state has been solved
        if(v[i][r])
        {
            return dp[i][r];
        }

        // Setting a state as solved
        v[i][r] = true;
        dp[i][r] =FindMax(i + 1, r,
                                w, n, c, k);

        // Recurrence relation
        for (let j = 0; j < k; j++)
        {
            let x = (r / exp_c[j]) % (c + 1);
            if (x - w[i] >= 0)
            {
                dp[i][r] = Math.max(dp[i][r],w[i] +
                                         FindMax(i + 1, r - w[i] *
                                                 exp_c[j], w, n, c, k));    
            }
        }

        // Returning the solved state
        return dp[i][r];
    }

     // Function to initialize global variables
    // and find the initial value of 'R'
    function PreCompute(n,c,k)
    {
        // Resizing the variables
        for(let i = 0; i < k; i++)
        {
            exp_c.push(0);
        }
        exp_c[0]= 1;
        for (let i = 1; i < k; i++)
        {
            exp_c[i]=(exp_c[i - 1] * (c + 1));

        }
        for (let i = 0; i < n; i++)
        {
            dp.push([]);
        }
        for (let i = 0; i < n; i++)
        {
            for(let j = 0; j < (exp_c[k-1] * (c + 1)) ; j++ )
            {
                dp[i][0];
            }
        }
        for (let i = 0; i < n; i++)
        {
            v.push([(exp_c[k-1] * (c + 1))]);
        }
        for (let i = 0; i < n; i++)
        {
            for(let j=0;j<v[i].length;j++)
            {
                v[i][j]=false;
            }
        }

        // Variable to store the initial value of R
        let R = 0;
        for(let i = 0; i < k; i++)
        {
            R += exp_c[i] * c;          
        }
        return R;
    }

    // Driver Code
    // Input array
    let w=[3, 8, 9];

    // number of knapsacks and capacity
        let k = 1, c = 11;
        let n = w.length;

        // Performing required pre-computation
        let r = PreCompute(n, c, k);

        // finding the required answer
        document.write(FindMax(0, r, w, n, c, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
11
```

**时间复杂度:** O(N*k*C^k).
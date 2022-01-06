# 从 1 到 N 的没有相邻元素的整数子集的计数

> 原文:[https://www . geesforgeks . org/从 1 到 n 的无相邻元素整数子集计数/](https://www.geeksforgeeks.org/count-of-subsets-of-integers-from-1-to-n-having-no-adjacent-elements/)

给定一个整数 **N** ，任务是统计从 **1** 到不包含相邻元素的 **N** 的整数数组形成的**子集**的数量。满足**不相邻**元素条件的子集不能选择，但可以添加更多元素。
**举例:**

```
Input: N = 4
Output: 3
Explanation:
Array is {1, 2, 3, 4}
So to satisfy the condition, the subsets formed are :
{1, 3}, {2, 4}, {1, 4}

Input: N = 5
Output: 4
```

**方法:**
这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。对于最后一个元素，我们有两个选择，要么包含它，要么排除它。假设 **DP[i]** 是以索引 **i** 结束的理想子集的数量。
所以下一个子问题变成 **DP[i-3]**
所以 DP 关系变成:

```
DP[i] = DP[i-2] + DP[i-3]  
```

但是，我们需要观察基本情况:

*   当 **N=0** 时，我们不能用 **0** 数组成任何子集。
*   当 **N=1** 时，我们可以形成 1 个子集， **{1}**
*   当 **N=2** 时，我们可以形成 2 个子集， **{1}** ， **{2}**
*   当 **N=3** 时，我们可以形成 2 个子集， **{1，3}** ， **{2}**

以下是上述方法的实现:

## C++

```
// C++ Code to count subsets not containing
// adjacent elements from 1 to N

#include <bits/stdc++.h>
using namespace std;

// Function to count subsets
int countSubsets(int N)
{

    if(N <= 2)
        return N;

    if(N == 3)
        return 2;

    int DP[N + 1] = {0};

    DP[0] = 0, DP[1] = 1, DP[2] = 2, DP[3] = 2;

    for (int i = 4; i <= N; i++) {

        DP[i] = DP[i - 2] + DP[i - 3];
    }

    return DP[N];
}

// Driver Code
int main()
{
    int N = 20;

    cout << countSubsets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count subsets not containing
// adjacent elements from 1 to N
class GFG{

// Function to count subsets
static int countSubsets(int N)
{
    if(N <= 2)
       return N;

    if(N == 3)
       return 2;

    int []DP = new int[N + 1];

    DP[0] = 0;
    DP[1] = 1;
    DP[2] = 2;
    DP[3] = 2;

    for(int i = 4; i <= N; i++)
    {
       DP[i] = DP[i - 2] + DP[i - 3];
    }
    return DP[N];
}

// Driver code
public static void main(String[] args)
{
    int N = 20;

    System.out.print(countSubsets(N));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 Code to count subsets
# not containing adjacent elements
# from 1 to N

# Function to count subsets
def countSubsets(N):

    if(N <= 2):
        return N

    if(N == 3):
        return 2

    DP = [0] * (N + 1)

    DP[0] = 0
    DP[1] = 1
    DP[2] = 2
    DP[3] = 2

    for i in range(4, N + 1):

        DP[i] = DP[i - 2] + DP[i - 3]

    return DP[N]

# Driver Code
if __name__ == '__main__':
    N = 20

    print(countSubsets(N))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# code to count subsets not containing
// adjacent elements from 1 to N
using System;
class GFG{

// Function to count subsets
static int countSubsets(int N)
{
    if(N <= 2)
        return N;

    if(N == 3)
        return 2;

    int []DP = new int[N + 1];

    DP[0] = 0;
    DP[1] = 1;
    DP[2] = 2;
    DP[3] = 2;

    for(int i = 4; i <= N; i++)
    {
        DP[i] = DP[i - 2] + DP[i - 3];
    }
    return DP[N];
}

// Driver code
public static void Main(String[] args)
{
    int N = 20;

    Console.Write(countSubsets(N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// javascript code to count subsets not containing
// adjacent elements from 1 to N   
// Function to count subsets
    function countSubsets(N) {
        if (N <= 2)
            return N;

        if (N == 3)
            return 2;

        var DP = Array(N + 1).fill(0);

        DP[0] = 0;
        DP[1] = 1;
        DP[2] = 2;
        DP[3] = 2;

        for (i = 4; i <= N; i++) {
            DP[i] = DP[i - 2] + DP[i - 3];
        }
        return DP[N];
    }

    // Driver code

        var N = 20;

        document.write(countSubsets(N));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
265
```
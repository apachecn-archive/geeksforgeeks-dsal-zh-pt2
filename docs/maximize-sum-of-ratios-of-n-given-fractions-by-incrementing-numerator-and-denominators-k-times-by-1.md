# 通过将分子和分母乘以 1

使 N 个给定分数的比值之和最大化

> 原文:[https://www . geeksforgeeks . org/n 给定分数的比率之和最大化乘以分子和分母乘以 k 乘以 1/](https://www.geeksforgeeks.org/maximize-sum-of-ratios-of-n-given-fractions-by-incrementing-numerator-and-denominators-k-times-by-1/)

给定一个正整数 **K** 和一个由 **N** 个分数的**{分子，分母}** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过 **1** ， **K 次**来求给定分数的比值之和。

**示例:**

> **输入:** arr[][] = {{1，2}，{3，5}，{2，2}}，K = 2
> **输出:** 0.78333
> **说明:**
> 最优的选择是递增第一个分数 K(= 2)的次数。所以比值之和是(3/4 + 3/5 + 2/2) / 3 = 0.78333，这是最大可能。
> 
> **输入:** arr[][] = {{1，1}，{4，5}}，K = 5
> T3】输出 : 0.95

**方法:**给定的问题可以通过[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，其思想是在给定的分数中增加那个分数，其增量使分数的比率之和最大化。这个想法可以使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)来实现。按照以下步骤解决问题:

*   初始化一个[最大堆](https://www.geeksforgeeks.org/binary-heap/)，比如说 **PQ** ，使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)，如果对 **i** 在**【0，N)** 范围内的所有值在**I<sup>th</sup>T9】索引上执行操作，该队列存储的值将以总平均比率递增。**
*   将数组 **arr[]** 中分数的所有索引插入优先级队列 **PQ** 中，分数的值递增。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K–1】**，并执行以下步骤:
    *   [弹出**PQ**T3】的顶元素。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)
    *   增加当前弹出索引的分数。
    *   将数组 **arr[]** 中的所有当前分数插入优先级队列 **PQ** 中，分数值递增。
*   完成以上步骤后，打印 priority_queue **PQ** 中存储的所有分数的比值之和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to increment the K fractions
// from the given array to maximize the
// sum of ratios of the given fractions
double maxAverageRatio(
    vector<vector<int> >& arr, int K)
{
    // Size of the array
    int N = arr.size();

    // Max priority queue
    priority_queue<pair<double, int> > q;

    // Iterate through the array
    for (int i = 0; i < N; i++) {

        // Insert the incremented value
        // if an operation is performed
        // on the ith index
        double extra
            = (((double)arr[i][0] + 1)
               / ((double)arr[i][1] + 1))
              - ((double)arr[i][0]
                 / (double)arr[i][1]);
        q.push(make_pair(extra, i));
    }

    // Loop to perform K operations
    while (K--) {
        int i = q.top().second;
        q.pop();

        // Increment the numerator and
        // denominator of ith fraction
        arr[i][0] += 1;
        arr[i][1] += 1;

        // Add the incremented value
        double extra
            = (((double)arr[i][0] + 1)
               / ((double)arr[i][1] + 1))
              - ((double)arr[i][0]
                 / (double)arr[i][1]);

        q.push(make_pair(extra, i));
    }

    // Stores the average ratio
    double ans = 0;
    for (int i = 0; i < N; i++) {
        ans += ((double)arr[i][0]
                / (double)arr[i][1]);
    }

    // Return the ratio
    return ans / N;
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 1, 2 }, { 3, 5 }, { 2, 2 } };
    int K = 2;

    cout << maxAverageRatio(arr, K);

    return 0;
}
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to increment the K fractions
// from the given array to maximize the
// sum of ratios of the given fractions
function maxAverageRatio(arr, K)
{

    // Size of the array
    var N = arr.length;

    // Max priority queue
    var q = [];

    // Iterate through the array
    for (var i = 0; i < N; i++) {

        // Insert the incremented value
        // if an operation is performed
        // on the ith index
        var extra
            = ((arr[i][0] + 1)
               / (arr[i][1] + 1))
              - (arr[i][0]
                 / arr[i][1]);
        q.push([extra, i]);
    }
    q.sort();
    // Loop to perform K operations
    while (K--) {
        var i = q[q.length-1][1];
        q.pop();

        // Increment the numerator and
        // denominator of ith fraction
        arr[i][0] += 1;
        arr[i][1] += 1;

        // Add the incremented value
        var extra
            = ((arr[i][0] + 1)
               / (arr[i][1] + 1))
              - (arr[i][0]
                 / arr[i][1]);

        q.push([extra, i]);
        q.sort();
    }

    // Stores the average ratio
    var ans = 0;
    for (var i = 0; i < N; i++) {
        ans += (arr[i][0]
                / arr[i][1]);
    }

    // Return the ratio
    return ans / N;
}

// Driver Code
var arr = [[1, 2 ], [3, 5], [2, 2 ]];
var K = 2;
document.write(maxAverageRatio(arr, K).toFixed(6));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
0.783333
```

***时间复杂度:** O(K*log N)*
***辅助空间:** O(N)*
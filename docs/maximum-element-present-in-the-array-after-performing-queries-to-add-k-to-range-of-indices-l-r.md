# 在执行查询以将 K 添加到索引范围[L，R]

后，数组中存在的最大元素

> 原文:[https://www . geeksforgeeks . org/执行查询后数组中出现的最大元素-将 k 添加到索引范围-l-r/](https://www.geeksforgeeks.org/maximum-element-present-in-the-array-after-performing-queries-to-add-k-to-range-of-indices-l-r/)

给定由 **N** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**(*初始设置为 0* )和由形式为 **{l，r，k}** 的查询组成的数组**Q【】**，每个查询的任务是将 **K** 添加到索引 **l** 到 **r** (包括两者)。执行完所有查询后，返回[数组中出现的最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。

**示例:**

> **输入:** **N** =10， **q** [] = {{1，5，3}，{4，8，7}，{6，9，1}}
> **输出:** 10
> **解释:**
> 最初数组为→ [0，0，0，0，0，0，0，0，0，0]
> **Query1 {1，5，3}结果为 7，0，0]
> **查询 2 {6，9，1}得到**【3，3，3，10，10，8，8，8，1，0】
> 更新数组中的最大值= 10**

**方法:**按照以下步骤解决问题。

*   [<u>遍历查询的向量</u>](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) ，对于每个查询 **{l，r，k}**
    *   将 **k** 加到**a【l】**上，将**a【r+1】**减去 k
*   初始化变量 **x = 0** 存储运行总和， **m = INT_MIN** 存储最大值
*   [<u>遍历阵</u>](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，给 **x** 添加元素，更新 **m.**
*   打印最大值 **m**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
// Function to find the max sum
// after processing q queries
int max_sum(int a[],
            vector<pair<pair<int, int>, int> > v,
            int q, int n)
{
    // Store the cumulative sum
    int x = 0;
    // Store the maximum sum
    int m = INT_MIN;

    // Iterate over the range 0 to q
    for (int i = 0; i < q; i++) {

        // Variables to extract
        // values from vector
        int p, q, k;

        p = v[i].first.first;
        q = v[i].first.second;
        k = v[i].second;
        a[p] += k;

        if (q + 1 <= n)

            a[q + 1] -= k;
    }

    // Iterate over the range [1, n]
    for (int i = 1; i <= n; i++)

    {
        // Calculate cumulative sum
        x += a[i];

        // Calculate maximum sum
        m = max(m, x);
    }
    // Return the maximum sum after q queries
    return m;
}

// Driver code
int main()
{

    // Stores the size of array
    // and number of queries
    int n = 10, q = 3;

    // Stores the sum
    int a[n + 5] = { 0 };

    // Storing input queries
    vector<pair<pair<int, int>, int> > v(q);
    v[0].first.first = 1;
    v[0].first.second = 5;
    v[0].second = 3;
    v[1].first.first = 4;
    v[1].first.second = 8;
    v[1].second = 7;
    v[2].first.first = 6;
    v[2].first.second = 9;
    v[2].second = 1;

    // Function call to find the maximum sum
    cout << max_sum(a, v, q, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the max sum
// after processing q queries
static int max_sum(int a[],
                   ArrayList<ArrayList<Integer>> v,
                   int q, int n)
{

    // Store the cumulative sum
    int x = 0;

    // Store the maximum sum
    int m = Integer.MIN_VALUE;

    // Iterate over the range 0 to q
    for(int i = 0; i < q; i++)
    {

        // Variables to extract
        // values from vector
        int p, qq, k;

        p = v.get(i).get(0);
        qq = v.get(i).get(1);
        k = v.get(i).get(2);
        a[p] += k;

        if (qq + 1 <= n)
            a[qq + 1] -= k;
    }

    // Iterate over the range [1, n]
    for(int i = 1; i <= n; i++)
    {

        // Calculate cumulative sum
        x += a[i];

        // Calculate maximum sum
        m = Math.max(m, x);
    }

    // Return the maximum sum after q queries
    return m;
}

// Driver code
public static void main(String[] args)
{

    // Stores the size of array
    // and number of queries
    int n = 10, q = 3;

    // Stores the sum
    int[] a = new int[n + 5];

    // Storing input queries
    ArrayList<ArrayList<Integer>> v= new ArrayList<>();

    for(int i = 0; i < q; i++)
        v.add(new ArrayList<>());

    v.get(0).add(1);
    v.get(0).add(5);
    v.get(0).add(3);
    v.get(1).add(4);
    v.get(1).add(8);
    v.get(1).add(7);
    v.get(2).add(6);
    v.get(2).add(9);
    v.get(2).add(1);

    // Function call to find the maximum sum
    System.out.println(max_sum(a, v, q, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the max sum
# after processing q queries
def max_sum(a, v, q, n):

    # Store the cumulative sum
    x = 0;

    # Store the maximum sum
    m = -10**9;

    # Iterate over the range 0 to q
    for i in range(q):

        # Variables to extract
        # values from vector
        p = v[i][0][0];
        q = v[i][0][1];
        k = v[i][1];
        a[p] += k;

        if (q + 1 <= n):
            a[q + 1] -= k;

    # Iterate over the range [1, n]
    for i in range(1, n + 1):
        # Calculate cumulative sum
        x += a[i];

        # Calculate maximum sum
        m = max(m, x);

    # Return the maximum sum after q queries
    return m;

# Driver code

# Stores the size of array
# and number of queries
n = 10
q = 3;

# Stores the sum
a = [0] * (n + 5);

# Storing input queries
v = [[[0 for i in range(2)] for x in range(2)] for z in range(q)]
v[0][0][0] = 1;
v[0][0][1] = 5;
v[0][1] = 3;
v[1][0][0] = 4;
v[1][0][1] = 8;
v[1][1] = 7;
v[2][0][0] = 6;
v[2][0][1] = 9;
v[2][1] = 1;

# Function call to find the maximum sum
print(max_sum(a, v, q, n));

# This code is contributed by _saurabh_jaiswal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the max sum
// after processing q queries
function max_sum(a, v, q, n) {
    // Store the cumulative sum
    let x = 0;
    // Store the maximum sum
    let m = Number.MIN_SAFE_INTEGER;

    // Iterate over the range 0 to q
    for (let i = 0; i < q; i++) {

        // Variables to extract
        // values from vector
        let p, q, k;

        p = v[i][0][0];
        q = v[i][0][1];
        k = v[i][1];
        a[p] += k;

        if (q + 1 <= n)

            a[q + 1] -= k;
    }

    // Iterate over the range [1, n]
    for (let i = 1; i <= n; i++) {
        // Calculate cumulative sum
        x += a[i];

        // Calculate maximum sum
        m = Math.max(m, x);
    }
    // Return the maximum sum after q queries
    return m;
}

// Driver code

// Stores the size of array
// and number of queries
let n = 10, q = 3;

// Stores the sum
let a = new Array(n + 5).fill(0);

// Storing input queries
let v = new Array(q).fill(0).map(() => new Array(2).fill(0).map(() => new Array(2).fill(0)));
v[0][0][0] = 1;
v[0][0][1] = 5;
v[0][1] = 3;
v[1][0][0] = 4;
v[1][0][1] = 8;
v[1][1] = 7;
v[2][0][0] = 6;
v[2][0][1] = 9;
v[2][1] = 1;

// Function call to find the maximum sum
document.write(max_sum(a, v, q, n));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(N+K)其中 N 是数组的大小，K 是多个查询
T3】空间复杂度: O(1)
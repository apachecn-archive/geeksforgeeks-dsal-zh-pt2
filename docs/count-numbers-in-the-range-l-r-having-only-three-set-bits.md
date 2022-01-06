# 计数范围[L，R]内只有三个设定位的数字

> 原文:[https://www . geesforgeks . org/count-numbers-in-range-l-r-only-set-三位/](https://www.geeksforgeeks.org/count-numbers-in-the-range-l-r-having-only-three-set-bits/)

给定一个由 **N** [对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)组成的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，其中每个数组元素表示一个形式为 **{L，R}，**的查询，任务是查找范围**【L，R】**中的数字计数，每个查询只有 3- [个设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/){ L，R}。

**示例:**

> **输入:** arr[] = {{11，19}，{14，19}}
> **输出:** 4
> 2
> **解释:**
> 
> 1.  查询(11，19):范围[11，19]中具有三个设置位的数字是{11，13，14，19}。
> 2.  查询(14，19):范围[14，19]中具有三个设置位的数字是{14，19}。
> 
> **输入:** arr[] = {{1，10}，{6，12}}
> **输出:** 1
> 2
> **解释:**
> 
> 1.  查询(1，10):范围[1，10]中有三个设置位的数字是{7}。
> 2.  查询(6，12):范围[6，12]中具有三个设置位的数字是{7，12}。

**做法:**解决这个问题的思路是做一个预算，只在**【1，10<sup>18</sup>**范围内设置 **3** 位，存储所有数字，然后用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到 **L** 的[下界](https://www.geeksforgeeks.org/lower_bound-in-cpp/)和[上界](https://www.geeksforgeeks.org/upper_bound-in-cpp/)R 的位置，返回答案为按照以下步骤解决给定的问题:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **V** ，存储范围**【1，10<sup>18</sup>**内的所有数字，只设置三位。
*   使用变量 **i、j** 、**和 **k** 迭代由[关系](https://www.geeksforgeeks.org/relations-and-their-types/)**【0，63】×【0，63】×【0，63】**形成的每个三元组，并执行以下步骤:

    *   如果 **i、j** 和 **k** 不同，则用**T5**I<sup>th</sup>、j <sup>th</sup> 、**和 **k <sup>th</sup>** 位组计算该数，如果该数小于 **10 <sup>18</sup> 、** <sup>将该数推入向量 **V**</sup>**** 
*   **[将向量 V 按升序排序。](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)**
*   **[使用变量 **i、**遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]、**，并执行以下步骤:

    *   将查询的边界存储在变量中，分别说 **L** 和 **R** 。
    *   在矢量 **V** 中找到 **L** 的[下弦](https://www.geeksforgeeks.org/lower_bound-in-cpp/)和 **R** 的[上弦](https://www.geeksforgeeks.org/upper_bound-in-cpp/)的位置。
    *   打印 **R** 的上限和 **L** 的下限的位置差，作为结果。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to precompute
void precompute(vector<long long>& v)
{
    // Iterate over the range [0, 64]
    for (long long i = 0; i < 64; i++) {
        // Iterate over the range [0, 64]
        for (long long j = i + 1; j < 64; j++) {
            // Iterate over the range [0, 64]
            for (long long k = j + 1; k < 64; k++) {

                // Stores the number with set bits
                // i, j, and k
                long long int x
                    = (1LL << i) | (1LL << j) | (1LL << k);

                // Check if the number is less
                // than 1e18
                if (x <= 1e18 && x > 0)
                    v.push_back(x);
            }
        }
    }

    // Sort the computed vector
    sort(v.begin(), v.end());
}

// Function to count number in the range
// [l, r] having three set bits
long long query(long long l, long long r,
                vector<long long>& v)
{
    // Find the lowerbound of l in v
    auto X = lower_bound(v.begin(), v.end(), l);

    // Find the upperbound of l in v
    auto Y = upper_bound(v.begin(), v.end(), r);

    // Return the difference
    // in their positions
    return (Y - X);
}
void PerformQuery(vector<pair<long long, long long> > arr,
                  int N)
{

    // Stores all the numbers in the range
    // [1, 1e18] having three set bits
    vector<long long> V;

    // Function call to perform the
    // precomputation
    precompute(V);

    // Iterate through each query
    for (auto it : arr) {
        long long L = it.first;
        long long R = it.second;

        // Print the answer
        cout << query(L, R, V) << "\n";
    }
}

// Driver Code
int main()
{

    // Input
    vector<pair<long long, long long> > arr
        = { { 11, 19 }, { 14, 19 } };
    int N = arr.size();

    // Function call
    PerformQuery(arr, N);

    return 0;
}
```

****Output**

```
4
2
```** 

*****时间复杂度:****O(N * log(63**<sup>3</sup>**)+63<sup>3</sup>)*
*T21】辅助空间: O(63 <sup>3</sup> )***
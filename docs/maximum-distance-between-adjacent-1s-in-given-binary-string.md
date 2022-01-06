# 给定二进制字符串中相邻 1 之间的最大距离

> 原文:[https://www . geesforgeks . org/给定二进制字符串中相邻 1 之间的最大距离/](https://www.geeksforgeeks.org/maximum-distance-between-adjacent-1s-in-given-binary-string/)

给定一个包含 N 个字符的二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出两个相邻 **1 的**之间的最大距离。

**示例:**

> **输入:** S = "1010010"
> **输出:** 3
> **说明:**在给定的索引中，索引{0，2}和{2，5}上有 2 组相邻的 1。
> 其中距离最大的是{2，5}，距离为 3 个单位。
> 
> **输入:** S = "100000"
> **输出:** -1
> **说明:**给定字符串中不存在相邻 1 的集合。

**逼近**:给定的问题是基于实现的问题。其思想是将 **1 的**的所有指数以递增的顺序存储在[T5】向量 T7】中。因此可以观察到，所需的答案将是索引向量中连续整数的**差的**最大值**。**](https://www.geeksforgeeks.org/vector-in-cpp-stl/)

下面是上述方法的实现:

## C++14

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// distance between two adjacent
// 1's in a given binary string
int maxDist(string S)
{
    // Stores the required answer
    int maxLen = INT_MIN;

    // Vector to store indices
    vector<int> indices;

    // Loop to traverse string
    for (int i = 0; i < S.length(); i++) {
        if (S[i] == '1')
            indices.push_back(i);
    }

    // Loop to reaverse the
    // index vector
    for (int i = 1; i < indices.size(); i++)

        // Update maximum distance
        maxLen = max(maxLen, indices[i] - 
                     indices[i - 1]);

    // Return Answer
    return maxLen == INT_MIN ? -1 : maxLen;
}

// Driver Code
int main()
{
    string S = "1010010";
    cout << maxDist(S);
    return 0;
}
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
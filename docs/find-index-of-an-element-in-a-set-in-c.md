# 在 C++中找到集合中某个元素的索引

> 原文:[https://www . geeksforgeeks . org/find-index-a-in-a-set-in-c/](https://www.geeksforgeeks.org/find-index-of-an-element-in-a-set-in-c/)

给定一个由 **N** 个整数和一个元素 **K** 组成的[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/) **S** ，任务是在集合 **S** 中找到元素 **K** 的索引。如果 **S** 中没有该元素，打印 **-1** 。

**示例:**

> **输入:** N = 5，S = {1，2，3，4，6} K = 6
> **输出:** 5
> **说明:** 6 是 S 中的第 5 个元素
> 
> **输入:** N = 5，S = {1，2，3，4，6}，K = 5
> **输出:** -1
> **说明:** 5 不在此集合中，因此我们给出输出为-1。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，将**索引**设为 **1** ，以存储所需元素的索引。
*   [遍历集合](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/) **S** 并执行以下操作:
*   如果当前元素为 **K** ，打印**索引**和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   否则，增加**索引。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate index
// of element in a Set
int GetIndex(set<int> S, int K)
{

    // To store the index of K
    int Index = 1;

    // Traverse the Set
    for (auto u : S) {

        if (u == K)
            return Index;

        Index++;
    }

    // If K is not present
    // in the set
    return -1;
}

// Driver Code
int main()
{
    // Input
    set<int> S;
    S.insert(1);
    S.insert(6);
    S.insert(2);
    S.insert(3);
    S.insert(4);
    int K = 6;

    cout << GetIndex(S, K) << endl;
    return 0;
}
```

**Output:** 

```
5
```

***时间复杂度** : O(N)*
***辅助空间:** O(1)*
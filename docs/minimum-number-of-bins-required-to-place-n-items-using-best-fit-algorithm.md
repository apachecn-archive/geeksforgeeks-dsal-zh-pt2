# 放置 N 个物品所需的最小箱数(使用最佳拟合算法)

> 原文:[https://www . geeksforgeeks . org/最小箱数-需要放置 n 个物品-使用最佳匹配算法/](https://www.geeksforgeeks.org/minimum-number-of-bins-required-to-place-n-items-using-best-fit-algorithm/)

给定一个由 **N** 项的权重和一个代表每个箱柜容量的正整数 **C** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **权重[]** ，任务是找到所需的最小箱柜数量，以便将所有项分配给其中一个箱柜。

**示例:**

> **输入:**重量[] = {4，8，1，4，2，1}，C = 10
> **输出:** 2
> **说明:**容纳所有物品所需的最小箱数为 2 个。
> 第一个箱子包含重量为{4，4，2}的物品。
> 第二个箱子包含重量为{8，1，1}的物品。
> 
> **输入:**权重[] = {9，8，2，2，5，4}，C = 10
> T3】输出: 4

**方法:**给定的问题可以通过使用[最佳拟合算法](https://www.geeksforgeeks.org/program-best-fit-algorithm-memory-management/)来解决。这个想法是把下一个项目放在垃圾箱里，在那里留下最小的空白空间。按照以下步骤解决问题:

*   初始化一个变量，比如说**把**算作 **0** ，它存储所需的最小箱数。
*   [按降序排列给定数组**权重[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   初始化一个[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)，比如 **M** 来存储当前已占用的垃圾箱中剩余的空间。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **权重[]** ，对每个元素执行以下步骤:
    *   如果在 **M** 中存在至少为**arr【I】**的最小空白空间，则[从 **M**](https://www.geeksforgeeks.org/multiset-erase-in-c-stl/) 中删除该空间，并将剩余的自由空间插入到 **M** 中。
    *   否则，将**计数**增加 **1** ，并将新仓的空位插入 **M** 中。
*   完成上述步骤后，打印**计数**的值作为所需的最小箱数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of bins required to fill all items
void bestFit(int arr[], int n, int W)
{
    // Stores the required number
    // of bins
    int count = 0;

    // Sort the array in decreasing order
    sort(arr, arr + n, greater<int>());

    // Stores the empty spaces in
    // existing bins
    multiset<int> M;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // Check if exact space is
        // present in the set M
        auto x = M.find(arr[i]);

        // Store the position of the
        // upperbound of arr[i] in M
        auto y = M.upper_bound(arr[i]);

        // If arr[i] is present, then
        // use this space and erase it
        // from the map M
        if (x != M.end()) {
            M.erase(x);
        }

        // If upper bound of arr[i] is
        // present, use this space and
        // insert the left space
        else if (y != M.end()) {
            M.insert(*y - arr[i]);
            M.erase(y);
        }

        // Otherwise, increment the count
        // of bins and insert the
        // empty space in M
        else {
            count++;
            M.insert(W - arr[i]);
        }
    }

    // Print the result
    cout << count;
}

// Driver Code
int main()
{
    int items[] = { 4, 8, 1, 4, 2, 1 };
    int W = 10;
    int N = sizeof(items) / sizeof(items[0]);

    // Function Call
    bestFit(items, N, W);

    return 0;
}
```

**Output:**

```
2

```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*
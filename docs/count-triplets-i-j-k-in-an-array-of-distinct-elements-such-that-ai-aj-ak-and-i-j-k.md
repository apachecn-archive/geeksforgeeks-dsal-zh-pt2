# 计数不同元素数组中的三元组(I，j，k)，使得 a[i] < a[j] > a[k]和 i < j < k

> 原文:[https://www . geesforgeks . org/count-triples-I-j-k-in-array-of-distinct-elements-so-ai-aj-AK-and-I-j-k/](https://www.geeksforgeeks.org/count-triplets-i-j-k-in-an-array-of-distinct-elements-such-that-ai-aj-ak-and-i-j-k/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算数组**arr【】**中可能的三元组 **(i，j，k)** 的数量，使得 **i < j < k** 和**arr【I】<arr【j】>arr【k】**。

**示例:**

> **输入:** arr[] = {2，3，1，-1}
> **输出:** 2
> **解释:**从给定数组中，满足属性(I，j，k)和 arr[i] < arr[j] > arr[k]的所有可能三元组为:
> 
> 1.  **(0，1，2):**arr[0](= 2)<arr[1](= 3)>arr[2](= 1)。
> 2.  **(0，1，3):**arr[0](= 2)<arr[1](= 3)>arr[3](=-1)。
> 
> 因此，三胞胎的数量是 2。
> 
> **输入:** arr[] = {2，3，4，6，7，9，1，12，10，8}
> **输出:** 41

**天真方法:**解决这个问题最简单的方法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素**arr【I】**，在**arr【I】**T9】左侧的较小元素的[计数和在**arr【I】**右侧的较小元素的](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)[计数的乘积给出了元素**arr【I】**的三元组计数为每个索引获得的所有计数的总和是所需的有效三元组的数量。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side/)

**高效方法:**上述方法也可以通过使用[基于策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/) ( **PBDS)** 查找较小元素的计数来优化。按照以下步骤解决问题:

*   初始化变量，说 **ans** 到 **0** ，存储可能的对的总数。
*   初始化[基于策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/)的两个[容器](https://www.geeksforgeeks.org/sequence-vs-associative-containers-cpp/)，比如 **P** 和 **Q** 。
*   初始化[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **V** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，其中**V【I】。首先**和**V【I】。第二个**在每个数组元素**arr【I】**的左侧和右侧存储较小元素的计数。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素**arr【I】**，更新**V【I】的值。首先将**作为 **P.order_of_key(arr[i])** ，并将 **arr[i]** 插入[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/) **P** 。
*   [从右到左遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素**arr【I】**，更新**V【I】的值。首先将**作为 **P.order_of_key(arr[i])** ，并将 **arr[i]** 插入[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/) **Q** 。
*   [遍历对的向量**V**T3】并加上**V【I】的值。第一个* V[i]。第二个**到变量**和**。](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)
*   完成上述步骤后，打印**和**的值作为总对数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <functional>
#include <iostream>
using namespace __gnu_pbds;
using namespace std;

// Function to find the count of triplets
// satisfying the given conditions
void findTriplets(int arr[], int n)
{
    // Stores the total count of pairs
    int ans = 0;

    // Declare the set
    tree<int, null_type, less<int>, rb_tree_tag,
         tree_order_statistics_node_update>
        p, q;

    // Declare the vector of pairs
    vector<pair<int, int> > v(n);

    // Iterate over the array from
    // left to right
    for (int i = 0; i < n; i++) {

        // Find the index of element
        // in sorted array
        int index = p.order_of_key(arr[i]);

        // Assign to the left
        v[i].first = index;

        // Insert into the set
        p.insert(arr[i]);
    }

    // Iterate from right to left
    for (int i = n - 1; i >= 0; i--) {

        // Find the index of element
        // in the sorted array
        int index = q.order_of_key(arr[i]);

        // Assign to the right
        v[i].second = index;

        // Insert into the set
        q.insert(arr[i]);
    }

    // Traverse the vector of pairs
    for (int i = 0; i < n; i++) {
        ans += (v[i].first * v[i].second);
    }

    // Print the total count
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 1, -1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findTriplets(arr, N);

    return 0;
}
```

**Output:**

```
2

```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*
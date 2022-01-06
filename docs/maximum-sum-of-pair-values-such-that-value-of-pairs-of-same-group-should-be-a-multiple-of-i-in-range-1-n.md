# 配对值的最大和，使得同一组的配对值应该是范围[1，N]

中 I 的倍数

> 原文:[https://www . geesforgeks . org/最大对值总和-同组对值应该是 1-n 范围内 I 的倍数/](https://www.geeksforgeeks.org/maximum-sum-of-pair-values-such-that-value-of-pairs-of-same-group-should-be-a-multiple-of-i-in-range-1-n/)

给定一个大小为 **N、**的配对数组[T1，其中配对的第一个元素是配对的值，第二个元素是这个配对所属的组，任务是找到配对值的最大和，这样对于范围**【1，N】**内的所有 **i** 来说，同一个组的配对数量应该是 **i** 的倍数。](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> **输入:** arr[] = {{5，3}，{9，3}，{6，3}，{7，3}，{9，3}，{7，3}}，N = 6
> **输出:** {43，43，43，32，38，43}
> **说明:**
> 有 6 对组 3。
> 对于 i = 1，选择组 3 的所有对，因为 6 % 1 = 0，那么总和将是 5 + 9 + 6 + 7 + 9 + 7 = 43。
> 对于 i = 2，从 6 % 2 = 0 开始选择组 3 的所有对，那么总和将是 5 + 9 + 6 + 7 + 9 + 7 = 43。
> 对于 i = 3，从 6 % 3 = 0 开始选择组 3 的所有对，那么总和将是 5 + 9 + 6 + 7 + 9 + 7 = 43。
> 对于 i = 4，选择 4 对值之和最大的组 3，则和为 9 + 9 + 7 + 7 = 32。
> 对于 i = 5，选择取值之和最大的 5 对组 3，则和为 9 + 9 + 7 + 7 + 6 = 38。
> 对于 i = 6，从 6 % 6 = 0 开始选择组 3 的所有对，那么总和将是 5 + 9 + 6 + 7 + 9 + 7 = 43。
> 
> **输入:** arr[] = {{6，1}，{8，2}，{3，1}，{1，2}，{5，1}，{1，2}，{5，1}}，N = 7
> **输出:** {29，28，26，19，0，0，0}

**方法:**解决问题最简单的思路是在组的基础上隔离数组的元素，然后使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)在 **O(1)** 中找到每组元素的和。按照以下步骤解决问题:

*   初始化一个 [](https://www.geeksforgeeks.org/hashing-data-structure/) [哈希图 **m** ，第一个元素为整数，第二个元素为向量](https://www.geeksforgeeks.org/map-of-vectors-in-c-stl-with-examples/)。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**中迭代，并将所有对的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)插入到它们各自的组中。
*   [将](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)[哈希图](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)中的所有向量按升序排序，并将其存储在一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，比如 **v** 。
*   初始化[向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)比如说， **ans** 大小为 **N** 和 **it** 分别为每组存储**【1，N】**和范围内所有 **i** 的答案[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，v . size()-1】**中迭代，并执行以下步骤:
    *   初始化一个[向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) **c** 和[在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，v[i]范围内迭代。尺寸()-1]** 使用变量 **j** 并执行以下步骤:
        *   如果 **j** 等于 **0** ，则将 **v[i][j]** 追加到[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **c，**否则追加 **c.back() + v[i][j]。**
    *   在向量**中插入[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**c**it**。
*   现在，[使用变量 **i** 遍历向量](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **it** ，并执行以下步骤:
    *   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，它【我】。尺寸()]** 使用变量 **j** 并执行以下步骤:
        *   将从向量**中选择 **j** 元素时无法获取的元素数量存储在变量**左侧**中。**
        *   加上**它【I】。back()–它[i][left-1]** (减去左边最小的数字)在 **ans[j-1]** 中。
*   执行上述步骤后，打印[矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)和 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// pair values, such that the number of
// pairs of the same group should be a
// multiple of i for all i in the
// range [1, N]
void findMaximumSumValue(vector<pair<int, int> > arr, int n)
{

    // Map for storing elements of same group
    // together
    map<int, vector<int> > mp;

    // Segregate students on the basis of group
    for (int i = 0; i < n; i++) {

        mp[arr[i].second - 1].push_back(arr[i].first);
    }

    vector<vector<int> > v;

    // Pushing all the vectors in the map to v
    for (auto i : mp) {
        v.push_back(i.second);

        // Sort all the groups in ascending order
        sort(v.back().begin(), v.back().end());
    }

    // Vector to store answer
    vector<int> ans(n, 0);

    // Vector to store prefix sum array
    // for each group
    vector<vector<int> > it;

    // Traverse through the groups
    for (auto i : v) {
        vector<int> c;

        // Save prefix sum array in vector C
        for (int j = 0; j < (int)i.size(); j++) {
            if (j == 0) {
                c.push_back(i[j]);
            }
            else {
                c.push_back(c.back() + i[j]);
            }
        }

        // Insert the prefix sum c in it
        it.push_back(c);
    }

    // Traverse through the prefix function of each group
    for (auto i : it) {

        // Traverse for all number of elements in i
        for (int j = 1; j <= (int)i.size(); j++) {

            // Check the number students to be left.
            int left = (int)i.size() % j;
            int del = 0;

            // If left is greater than 0 subtract the
            // value of left smallest elements
            if (left > 0)
                del = i[left - 1];
            ans[j - 1] += (i.back() - del);
        }
    }

    // Print the answer list for every
    // possible size
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }

    cout << endl;
}

// Driver Code
int main()
{
    // Given Input
    vector<pair<int, int> > arr
        = { { 5, 3 }, { 9, 3 }, { 6, 3 },
            { 7, 3 }, { 9, 3 }, { 7, 3 } };

    int N = arr.size();

    // Function Call
    findMaximumSumValue(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum sum of
# pair values, such that the number of
# pairs of the same group should be a
# multiple of i for all i in the
# range [1, N]
def findMaximumSumValue(arr, n):

    # Map for storing elements of same group
    # together
    mp = {}

    # Segregate students on the basis of group
    for i in range(n):
        if (arr[i][1]-1) not in mp:
            mp[arr[i][1] - 1] = []

        mp[arr[i][1] - 1].append(arr[i][0])

    v = []

    # Pushing all the vectors in the map to v
    for i in mp:
        v.append(mp[i])

        # Sort all the groups in ascending order
        v[0].sort()

    # Vector to store answer
    ans = [0]*(n)

    # Vector to store prefix sum array
    # for each group
    it = []

    # Traverse through the groups
    for i in v:
        c = []

        # Save prefix sum array in vector C
        for j in range(len(i)):
            if (j == 0):
                c.append(i[j])

            else:
                c.append(c[-1] + i[j])

        # Insert the prefix sum c in it
        it.append(c)

    # Traverse through the prefix function of each group
    for i in it:

        # Traverse for all number of elements in i
        for j in range(1, len(i) + 1):

            # Check the number students to be left.
            left = len(i) % j
            dele = 0

            # If left is greater than 0 subtract the
            # value of left smallest elements
            if (left > 0):
                dele = i[left - 1]
            ans[j - 1] += (i[-1] - dele)

    # Print the answer list for every
    # possible size
    for i in range(n):
        print(ans[i], end=" ")

    print()

# Driver Code
if __name__ == "__main__":

    # Given Input
    arr = [[5, 3], [9, 3], [6, 3],
           [7, 3], [9, 3], [7, 3]]

    N = len(arr)

    # Function Call
    findMaximumSumValue(arr, N)

    # This code is contributed by ukasp.
```

**Output:** 

```
43 43 43 32 38 43
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
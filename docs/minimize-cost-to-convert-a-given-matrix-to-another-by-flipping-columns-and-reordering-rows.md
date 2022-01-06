# 通过翻转列和重新排序行，将给定矩阵转换为另一个矩阵的成本降至最低

> 原文:[https://www . geeksforgeeks . org/通过翻转列并重新排序行来最小化将给定矩阵转换为另一个矩阵的成本/](https://www.geeksforgeeks.org/minimize-cost-to-convert-a-given-matrix-to-another-by-flipping-columns-and-reordering-rows/)

给定尺寸为 **N * M** 的两个二进制矩阵 **mat[][]** 和 **target[][]** ，任务是通过以下操作找到将矩阵 **mat[][]** 转换为 **target[][]** 的最小成本:

*   翻转**mat【】【】**中的特定列，使所有 **1s** 变为 **0s** ，反之亦然。本次手术费用为 **1** 。
*   重新排列**垫子[][]** 的行。此操作的成本为 0。

如果无法将矩阵 **mat[][]** 转换为 **target[][]** ，则打印**-1”**。

**示例:**

> **输入:** mat[][] = {{0，0}，{1，0}，{1，1}}，target[][] = {{0，1}，{1，0}，{1，1}}
> **输出:** 1
> **解释:**
> 步骤 1:重新排序 2 <sup>nd</sup> 和 3 <sup>rd</sup> 行，将 mat[][]修改为{{0，0}，{1，1}，{ 2 }成本= 0
> 第二步:翻转第二列。mat[][]修改为{{0，1}，{1，0}，{1，1}}，等于 target[][]。成本= 1
> 
> **输入:** mat[][] = {{0，0，0}，{1，0，1}，{1，1，0}}，target[][] = {{0，0，1}，{1，0，1}，{1，1，1}}
> **输出:** -1

**方法:**思想是将给定矩阵的行转换成[位集](https://www.geeksforgeeks.org/c-bitset-and-its-application/)，然后找到使矩阵相等的最小运算成本。以下是步骤:

1.  首先，使用位集将 **mat[][]** 的行转换为二进制数。
2.  完成上述步骤后，找到所有可能成为目标矩阵第一行的行。
3.  将一行 **mat[][]** 转换为 **tar[][]** 所需的翻转次数是位集的 **[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)** 值中的设置位计数。
4.  使用翻转模式计算每行的按位异或，并检查新矩阵在排序时是否等于排序后的**目标[][]** 矩阵。
5.  如果它们相同，则存储翻转次数。
6.  计算以上步骤中所有这样的翻转次数，并返回其中的最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Custom comparator to sort vector
// of bitsets
bool static cmp(bitset<105>& p1,
                bitset<105>& p2)
{
    return p1.to_string() < p2.to_string();
}

// Function to convert the given
// matrix into the target matrix
int minCost(vector<vector<int> >& a,
            vector<vector<int> >& t)
{

    // Number of rows and columns
    int n = a.size();
    int m = a[0].size();

    vector<bitset<105> > mat(n), tar(n);

    // Iterate over rows
    for (int i = 0; i < n; i++) {
        string s;

        for (int j = 0; j < m; j++) {
            s += char(a[i][j] + '0');
        }
        mat[i] = bitset<105>(s);
    }

    // Iterate over rows
    for (int i = 0; i < n; i++) {
        string s;

        for (int j = 0; j < m; j++) {
            s += char(t[i][j] + '0');
        }
        tar[i] = bitset<105>(s);
    }

    // Sort the matrix
    sort(tar.begin(), tar.end(), cmp);

    int ans = INT_MAX;

    // Check all possible rows as the
    // first row of target
    for (int i = 0; i < n; i++) {

        vector<bitset<105> > copy(mat);

        // Get the flip pattern
        auto flip = copy[i] ^ tar[0];

        for (auto& row : copy)
            row ^= flip;

        sort(copy.begin(), copy.end(), cmp);

        // Number of flip operations
        // is the count of set bits in flip
        if (copy == tar)
            ans = min(ans, (int)flip.count());
    }

    // If it is not possible
    if (ans == INT_MAX)
        return -1;

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Given matrices
    vector<vector<int> > matrix{ { 0, 0 },
                                 { 1, 0 },
                                 { 1, 1 } };

    vector<vector<int> > target{ { 0, 1 },
                                 { 1, 0 },
                                 { 1, 1 } };

    // Function Call
    cout << minCost(matrix, target);
}
```

**Output:**

```
1

```

 ***时间复杂度:**O(N * M)
T5】辅助空间: O(N * M)*
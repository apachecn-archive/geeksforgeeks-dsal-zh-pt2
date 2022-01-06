# 最小化给定数组中的分裂，以找到最多 2 个元素的子集，且总和最多为 K

> 原文:[https://www . geeksforgeeks . org/最小化-给定数组中的拆分-查找最多 2 个元素的子集-最多 k 个元素之和/](https://www.geeksforgeeks.org/minimize-splits-in-given-array-to-find-subsets-of-at-most-2-elements-with-sum-at-most-k/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是计算该数组可以划分的几乎 2 个元素的子集的最小数量，使得每个子集的元素之和几乎为 **K** 。

**示例:**

> **输入:** arr[] = {1，2，3}，K = 3
> **输出:** 2
> **说明:**给定数组可以分为{1，2}和{3}两个子集，两个子集的和为 Atmos K，因此，子集的个数为 2，这是最小的可能。
> 
> **输入:** arr[] = {3，2，2，3，1}，K = 3
> T3】输出: 4
> 
> **输入:** arr[] = {3，2，2，3，1}，K = 2
> **输出:** -1

**方法:**在[两个指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)的帮助下，使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决给定的问题。想法是将具有最小值的整数和最大可能值组合在一起，使得它们的总和不超过 **K** 。按照以下步骤解决给定的问题:

*   [按非递减顺序对给定数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序。
*   创建两个变量， **i = 0** 和**j = N–1**，其中 **i** 代表第一个索引， **j** 代表数组的最后一个索引。
*   如果 **arr[i]** 和 **arr[j]** 之和几乎为 **K** ，则增加 I 并减少 j。同样，将子集计数增加 **1** 。
*   如果**arr【I】****arr【j】**之和大于 **K** ，则递减 **j** 并增加子集计数。

下面是上述方法的实现:

## C++14

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split array into minimum
// subsets of at most 2 elements with
// sum of each subset at most K
int minSubsetCnt(vector<int>& arr, int K)
{
    // Sort arr in increasing order
    sort(arr.begin(), arr.end());

    // If it is impossible
    if (arr[arr.size() - 1] > K) {
        return -1;
    }

    // Stores the count of subsets
    int cnt = 0;

    // Starting pointer
    int i = 0;

    // End pointer
    int j = arr.size() - 1;

    // Loop for the two
    // pointer approach
    while (i <= j) {
        if (arr[i] + arr[j] <= K) {
            cnt++;
            i++;
            j--;
        }
        else {
            cnt++;
            j--;
        }
    }

    // Return Answer
    return cnt;
}
// Driver Code
int main()
{
    vector<int> arr{ 3, 2, 2, 3, 1 };
    int K = 3;
    cout << minSubsetCnt(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to split array into minimum
// subsets of at most 2 elements with
// sum of each subset at most K
static int minSubsetCnt(int[] arr, int K)
{

    // Sort arr in increasing order
    Arrays.sort(arr);

    // If it is impossible
    if (arr[arr.length - 1] > K)
    {
        return -1;
    }

    // Stores the count of subsets
    int cnt = 0;

    // Starting pointer
    int i = 0;

    // End pointer
    int j = arr.length - 1;

    // Loop for the two
    // pointer approach
    while (i <= j)
    {
        if (arr[i] + arr[j] <= K)
        {
            cnt++;
            i++;
            j--;
        }
        else
        {
            cnt++;
            j--;
        }
    }

    // Return Answer
    return cnt;
}

// Driver Code
public static void main(String args[])
{
    int[] arr = { 3, 2, 2, 3, 1 };
    int K = 3;

    System.out.print(minSubsetCnt(arr, K));
}
}

// This code is contributed by sanjoy_62
```

**Output**

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*
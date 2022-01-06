# 覆盖给定范围所需选择的最小对数

> 原文:[https://www . geesforgeks . org/最小配对数-需要选择以覆盖给定范围/](https://www.geeksforgeeks.org/minimum-number-of-pairs-required-to-be-selected-to-cover-a-given-range/)

给定一个由 **N** 对和正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是选择最小的对数，使其覆盖整个范围**【0，K】**。如果无法覆盖范围**【0，K】**，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {{0，3}、{2，5}、{5，6}、{6，8}、{6，10}}，K = 10
> **输出:** 4
> **说明:**最佳方法之一是选择覆盖整个范围[0，10]的范围{{0，3}、{2，5}、{5，6}、{6，10}。
> 
> **输入:** arr[] = {{0，4}，{1，5}，{5，6}，{8，10}}，N = 10
> **输出:** -1

**天真方法:**解决问题最简单的方法是[生成所有可能的子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)并检查每个子集，不管它是否覆盖整个范围。

***时间复杂度:**O(2<sup>N</sup>×N)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过[在左元素](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的基础上对数组进行升序排序来优化，对于左元素相等的对，按照其右元素的降序对元素进行排序。现在，选择最佳配对。

按照以下步骤解决问题:

*   [按左元素递增的顺序对向量对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) **arr[]** 进行排序，如果左元素相等，则按对的右元素递减的顺序对数组进行排序。
*   检查**是否为[0][0]！= 0** 然后打印 **-1** 。
*   初始化一个变量，说 **R** 为**arr【0】【1】**存储范围的右边界， **ans** 为 **1** 存储覆盖范围所需的范围数**【0，K】**。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   如果 **R == K** ，终止循环。
    *   初始化一个变量，比如说 **maxr** 为 **R** ，它存储最大右界，其中左界 **≤ R** 。
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N-1】**中迭代，并执行以下步骤:
        *   如果 **arr[j][0] ≤ R** ，则将 **maxr** 的值修改为 **max(maxr，arr[j][1])** 。
    *   将 **i** 的值修改为 **j-1** ，将 **R** 的值修改为 **maxr** ，并将 **ans** 的值增加 1。
*   如果 **R** 不等于 **K** ，则打印 **-1** 。
*   否则，打印**和**的值。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort the elements in
// increasing order of left element and
// sort pairs with equal left element in
// decreasing order of right element
static bool cmp(pair<int, int> a, pair<int, int> b)
{
    if (a.first == b.first) {
        return a.second > b.second;
    }
    else {
        return b.first > a.first;
    }
}

// Function to select minimum number of pairs
// such that it covers the entire range [0, K]
int MinimumPairs(vector<pair<int, int> > arr, int K)
{
    int N = arr.size();

    // Sort the array using comparator
    sort(arr.begin(), arr.end(), cmp);

    // If the start element
    // is not equal to 0
    if (arr[0].first != 0) {
        return -1;
    }

    // Stores the minimum
    // number of pairs required
    int ans = 1;

    // Stores the right bound of the range
    int R = arr[0].second;

    // Iterate in the range[0, N-1]
    for (int i = 0; i < N; i++) {
        if (R == K) {
            break;
        }

        // Stores the maximum right bound
        // where left bound ≤ R
        int maxr = R;

        int j;

        // Iterate in the range [i+1, N-1]
        for (j = i + 1; j < N; j++) {

            // If the starting point of j-th
            // element is less than equal to R
            if (arr[j].first <= R) {

                maxr = max(maxr, arr[j].second);
            }

            // Otherwise
            else {
                break;
            }
        }

        i = j - 1;
        R = maxr;
        ans++;
    }

    // If the right bound
    // is not equal to K
    if (R != K) {
        return -1;
    }

    // Otherwise
    else {
        return ans;
    }
}

// Driver Code
int main()
{
    // Given Input
    int K = 4;
    vector<pair<int, int> > arr{ { 0, 6 } };

    // Function Call
    cout << MinimumPairs(arr, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.io.*;
import java.lang.*;
import java.util.*;

// User defined Pair class
class Pair
{
    int x;
    int y;

    // Constructor
    public Pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}
// class to sort the elements in
// increasing order of left element and
// sort pairs with equal left element in
// decreasing order of right element
class cmp implements Comparator<Pair>
{

    public int compare(Pair p1, Pair p2)
    {
        if (p1.x == p2.x)
        {
            return p1.y - p2.y;
        }
        else
        {
            return p2.x - p1.x;
        }
    }
}

class GFG
{
    // Function to select minimum number of pairs
    // such that it covers the entire range [0, K]
    public static int MinimumPairs(Pair arr[], int K)
    {
        int N = arr.length;
        // Sort the array using comparator
        Arrays.sort(arr, new cmp());

        // If the start element
        // is not equal to 0
        if (arr[0].x != 0)
        {
            return -1;
        }

        // Stores the minimum
        // number of pairs required
        int ans = 1;

        // Stores the right bound of the range
        int R = arr[0].y;

        // Iterate in the range[0, N-1]
        for (int i = 0; i < N; i++)
        {
            if (R == K)
            {
                break;
            }

            // Stores the maximum right bound
            // where left bound is less than equal to R
            int maxr = R;
            int j;

            // Iterate in the range [i+1, N-1]
            for (j = i + 1; j < N; j++)
            {

                // If the starting point of j-th
                // element is less than equal to R
                if (arr[j].x <= R)
                {

                    maxr = Math.max(maxr, arr[j].y);
                }

                // Otherwise
                else
                {
                    break;
                }
            }

            i = j - 1;
            R = maxr;
            ans++;
        }

        // If the right bound
        // is not equal to K
        if (R != K)
        {
            return -1;
        }

        // Otherwise
        else
        {
            return ans;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int K = 4;
        int n = 1; // length of array
        Pair arr[] = new Pair[n];
        arr[0] = new Pair(0, 6);

        System.out.println(MinimumPairs(arr, K));
    }
}

// This code is contributed by rj13to.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to select minimum number of pairs
# such that it covers the entire range [0, K]
def MinimumPairs(arr, K):

    N = len(arr)

    # Sort the array using comparator
    arr.sort()

    # If the start element
    # is not equal to 0
    if (arr[0][0] != 0):
        return -1

    # Stores the minimum
    # number of pairs required
    ans = 1

    # Stores the right bound of the range
    R = arr[0][1]

    # Iterate in the range[0, N-1]
    for i in range(N):
        if (R == K):
            break

        # Stores the maximum right bound
        # where left bound ≤ R
        maxr = R

        j = 0

        # Iterate in the range [i+1, N-1]
        for j in range(i + 1, N, 1):

            # If the starting point of j-th
            # element is less than equal to R
            if (arr[j][0] <= R):
                maxr = max(maxr, arr[j][1])

            # Otherwise
            else:
                break

        i = j - 1
        R = maxr
        ans += 1

    # If the right bound
    # is not equal to K
    if (R != K):
        return -1

    # Otherwise
    else:
        return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    K = 4
    arr = [ [ 0, 6 ] ]

    # Function Call
    print(MinimumPairs(arr, K))

# This code is contributed by bgangwar59
```

**Output**

```
-1
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*
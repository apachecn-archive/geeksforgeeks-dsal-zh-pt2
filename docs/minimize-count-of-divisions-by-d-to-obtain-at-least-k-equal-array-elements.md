# 将除法次数减少 D，得到至少 K 个相等的数组元素

> 原文:[https://www . geeksforgeeks . org/最小化按 d 划分的计数以获得至少 k 个相等的数组元素/](https://www.geeksforgeeks.org/minimize-count-of-divisions-by-d-to-obtain-at-least-k-equal-array-elements/)

给定一个大小为 **N** 的数组**A【】**和两个整数 **K** 和 **D** ，任务是计算获得至少 **K** 个相等数组元素所需的最小可能操作数。每个操作包括用 **A[i] / D** 替换一个元素 **A[i]** 。该操作可以执行任意次数。

**示例:**

> **输入:** N = 5，A[ ] = {1，2，3，4，5}，K = 3，D = 2
> **输出:** 2
> **说明:**
> 第一步:用 A[3] / D 替换 A[3]，即(4 / 2) = 2。因此，数组修改为{1，2，3，2，5}
> 步骤 2:用 A[4] / D 替换 A[4]，即(5 / 2) = 2。因此，数组修改为{1，2，3，2，2}
> 因此，修改后的数组具有 K(= 3)个相等的元素。
> 因此，所需的最小操作数是 2。
> 
> **输入:** N = 4，A[ ] = {1，2，3，6}，K = 2，D = 3
> **输出:** 1
> **说明:**
> 用 A[3] / D 代替 A[3]，即(6 / 3) = 2。因此，数组修改为{1，2，3，2}。
> 因此，修改后的数组具有 K(= 2)个相等的元素。
> 因此，所需的最小操作数为 1。

**天真方法:**
解决问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/print-subsets-given-size-set/)的每个可能子集，并对该子集的所有元素执行给定操作。每个子集所需的操作数将等于子集的大小。对于每个子集，**计数**相等元素的数量，检查**计数**是否等于 **K** 。如果是，将当时的**计数**与目前获得的最小移动量进行比较，并相应更新。最后，打印最小移动量。

**时间复杂度:**O(2<sup>N</sup>* N)
T5】辅助空间: O(N)

**高效方法:**
按照以下步骤解决问题:

*   初始化一个 2D 向量 **V** ，其中，一行的大小**V【I】**表示已经减少到 A【I】的数组元素的数量，并且该行的每个元素表示对数组元素执行的除以 D 的计数，以获得数量 **i** 。
*   遍历数组。对于每个元素**A【I】**，继续除以 **D** ，直到它减少到 **0** 。
*   对于在上述步骤中获得的 A[i]的每个中间值，将所需的分割数插入 **V[A[i]]** 。
*   一旦完成了整个数组的上述步骤，迭代数组 **V[ ]** 。
*   对于每个 V[i]，检查 **V[i] ≥ K** (最多 K)的大小。
*   如果 **V[i] ≥ K** ，则表示数组中至少有 **K** 元素已经减少到 **i** 。排序**V【I】**并添加第一个 **K** 值，即使数组中 **K** 元素相等所需的最小 K 个移动。
*   将 **K** 移动的总和与所需的最小移动进行比较，并相应更新。
*   一旦完成数组 **V[]** 的遍历，打印最终获得的最小移动次数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum
// number of moves required
int getMinimumMoves(int n, int k, int d,
                    vector<int> a)
{
    int MAX = 100000;

    // Stores the number of moves
    // required to obtain respective
    // values from the given array
    vector<int> v[MAX];

    // Traverse the array
    for (int i = 0; i < n; i++) {
        int cnt = 0;

        // Insert 0 into V[a[i]] as
        // it is the initial state
        v[a[i]].push_back(0);

        while (a[i] > 0) {
            a[i] /= d;
            cnt++;

            // Insert the moves required
            // to obtain current a[i]
            v[a[i]].push_back(cnt);
        }
    }

    int ans = INT_MAX;

    // Traverse v[] to obtain
    // minimum count of moves
    for (int i = 0; i < MAX; i++) {

        // Check if there are at least
        // K equal elements for v[i]
        if (v[i].size() >= k) {

            int move = 0;

            sort(v[i].begin(), v[i].end());

            // Add the sum of minimum K moves
            for (int j = 0; j < k; j++) {

                move += v[i][j];
            }

            // Update answer
            ans = min(ans, move);
        }
    }

    // Return the final answer
    return ans;
}

// Driver Code
int main()
{
    int N = 5, K = 3, D = 2;
    vector<int> A = { 1, 2, 3, 4, 5 };

    cout << getMinimumMoves(N, K, D, A);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to return minimum
// number of moves required
@SuppressWarnings("unchecked")
static int getMinimumMoves(int n, int k,
                           int d, int[] a)
{
    int MAX = 100000;

    // Stores the number of moves
    // required to obtain respective
    // values from the given array
    Vector<Integer> []v = new Vector[MAX];
    for(int i = 0; i < v.length; i++)
        v[i] = new Vector<Integer>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        int cnt = 0;

        // Insert 0 into V[a[i]] as
        // it is the initial state
        v[a[i]].add(0);

        while (a[i] > 0)
        {
            a[i] /= d;
            cnt++;

            // Insert the moves required
            // to obtain current a[i]
            v[a[i]].add(cnt);
        }
    }

    int ans = Integer.MAX_VALUE;

    // Traverse v[] to obtain
    // minimum count of moves
    for(int i = 0; i < MAX; i++)
    {

        // Check if there are at least
        // K equal elements for v[i]
        if (v[i].size() >= k)
        {
            int move = 0;

            Collections.sort(v[i]);

            // Add the sum of minimum K moves
            for(int j = 0; j < k; j++)
            {
                move += v[i].get(j);
            }

            // Update answer
            ans = Math.min(ans, move);
        }
    }

    // Return the final answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 5, K = 3, D = 2;
    int []A = { 1, 2, 3, 4, 5 };

    System.out.print(getMinimumMoves(N, K, D, A));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return minimum
# number of moves required
def getMinimumMoves(n, k, d, a):

    MAX = 100000

    # Stores the number of moves
    # required to obtain respective
    # values from the given array
    v = []
    for i in range(MAX):
        v.append([])

    # Traverse the array
    for i in range(n):
        cnt = 0

        # Insert 0 into V[a[i]] as
        # it is the initial state
        v[a[i]] += [0]

        while(a[i] > 0):
            a[i] //= d
            cnt += 1

            # Insert the moves required
            # to obtain current a[i]
            v[a[i]] += [cnt]

    ans = float('inf')

    # Traverse v[] to obtain
    # minimum count of moves
    for i in range(MAX):

        # Check if there are at least
        # K equal elements for v[i]
        if(len(v[i]) >= k):
            move = 0
            v[i].sort()

            # Add the sum of minimum K moves
            for j in range(k):
                move += v[i][j]

            # Update answer
            ans = min(ans, move)

    # Return the final answer
    return ans

# Driver Code
if __name__ == '__main__':

    N = 5
    K = 3
    D = 2
    A = [ 1, 2, 3, 4, 5 ]

    # Function call
    print(getMinimumMoves(N, K, D, A))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return minimum
// number of moves required

static int getMinimumMoves(int n, int k,
                           int d, int[] a)
{
    int MAX = 100000;

    // Stores the number of moves
    // required to obtain respective
    // values from the given array
    List<int> []v = new List<int>[MAX];
    for(int i = 0; i < v.Length; i++)
        v[i] = new List<int>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        int cnt = 0;

        // Insert 0 into V[a[i]] as
        // it is the initial state
        v[a[i]].Add(0);

        while (a[i] > 0)
        {
            a[i] /= d;
            cnt++;

            // Insert the moves required
            // to obtain current a[i]
            v[a[i]].Add(cnt);
        }
    }

    int ans = int.MaxValue;

    // Traverse v[] to obtain
    // minimum count of moves
    for(int i = 0; i < MAX; i++)
    {

        // Check if there are at least
        // K equal elements for v[i]
        if (v[i].Count >= k)
        {
            int move = 0;

            v[i].Sort();

            // Add the sum of minimum K moves
            for(int j = 0; j < k; j++)
            {
                move += v[i][j];
            }

            // Update answer
            ans = Math.Min(ans, move);
        }
    }

    // Return the final answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5, K = 3, D = 2;
    int []A = { 1, 2, 3, 4, 5 };

    Console.Write(getMinimumMoves(N, K, D, A));
}
}

// This code is contributed by 29AjayKumar
```

**Output**

```
2
```

**时间复杂度:** O(MlogM)，其中 M 为最大摄数
T3】辅助空间: O(M)
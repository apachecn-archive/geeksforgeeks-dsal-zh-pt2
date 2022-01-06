# 通过执行给定的操作

最大化移除的数组元素的总和

> 原文:[https://www . geeksforgeeks . org/最大化数组元素的总和-通过执行给定的操作移除/](https://www.geeksforgeeks.org/maximize-sum-of-array-elements-removed-by-performing-the-given-operations/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和 **min[]** ，由 **N** 个整数和一个整数 **K** 组成。对于每个指标 **i** ，arr[i]最多可以减少到 **min[i]** 。考虑一个变量，说 **S** ( *最初 **0*** )。任务是通过执行以下操作找到 **S** 的最大值:

*   选择一个索引 **i** 并将 **max(arr[i]，min[i])添加到 **S** 中。**
*   从 **arr[]** 及其对应的最小值中移除所选元素。
*   如果每个剩余值大于其相应的最小值(单位为**分钟)【】**，则减少 **K** 。

**示例:**

> **输入:** arr[] = {2，4，5，8}，min[] = {1，4，5，5}，K = 3
> **输出:** 18
> **解释:**
> 按照以下顺序选择元素:
> 第一步:选择元素 8。现在，S = 8 和 arr[] = {-1，4，5}和 min[] = {1，4，5}
> 步骤 2:选择元素 5。现在，S = 8 + 5 = 13 和 arr[] = {-1，4}和 min[] = {1，4}
> 第三步:选择元素 5。现在，S = 8 + 5 + 4 = 17 和 arr[] = {-1}和 min[] = {1}
> 第四步:选择元素-1，但是-1 < min[0]。因此，选择 1。
> 因此，S = 8 + 5 + 4 + 1 = 18。
> 
> **输入:** arr[] = {3，5，2，1}，min[] = {3，2，1，3}，K = 2
> **输出:** 12
> **解释:**
> 按照以下顺序选择元素:
> 第一步:选择元素 5。现在，S = 5 和 arr[] = {3，0，1}和 min[] = {3，1，3}
> 步骤 2:选择元素 3。现在，S = 5 + 3 = 8 和 arr[] = {0，1}和 min[] = {1，3}
> 第三步:从 min[]中选择元素 3。现在，S = 5 + 3 + 3 = 11，arr[] = {0}和 min[] = {1}
> 步骤 4:从 min[]中选择元素 1。
> 因此，S = 5 + 3 + 3 + 1 = 12。

**天真方法:**最简单的方法是[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并在数组本身中执行给定的操作。按照以下步骤解决问题:

1.  [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[找到最大阵元](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。
2.  将 **S** 中的最大值相加，去掉最大值。
3.  如果满足以上条件，将剩余元素减少 **K** 。
4.  重复以上步骤，直到给定的数组变成空的。
5.  穿越后，打印 **S** 。

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为给定数组的长度。*
***辅助空间:** O(N)*

**有效方法:**想法是[按照降序对给定数组进行排序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。然后贪婪地选择元素，打印出 **S** 的最大值。按照以下步骤解决问题:

1.  将数组的元素 **arr[]** 与它们在 **min[]** 中的对应值配对。
2.  [根据数组 **arr[]** 对数组](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行降序排序。
3.  最初，选择最大元素，并将其初始值增加 **K** 。
4.  现在，通过当前 **K** 减少其值来选择下一个最大元素。
5.  重复以上步骤，直到遍历完所有数组元素，打印 **S** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// the array arr[] where each element
// can be reduced to at most min[i]
void findMaxSum(vector<int> arr, int n,
                vector<int> min, int k,
                int& S)
{
    // Stores the pair of arr[i] & min[i]
    vector<pair<int, int> > A;

    for (int i = 0; i < n; i++) {
        A.push_back({ arr[i], min[i] });
    }

    // Sorting vector of pairs
    sort(A.begin(), A.end(),
        greater<pair<int, int> >());

    int K = 0;

    // Traverse the vector of pairs
    for (int i = 0; i < n; i++) {

        // Add to the value of S
        S += max(A[i].first - K,
                A[i].second);

        // Update K
        K += k;
    }
}

// Driver Code
int main()
{
    vector<int> arr, min;

    // Given array arr[], min[]
    arr = { 3, 5, 2, 1 };
    min = { 3, 2, 1, 3 };

    int N = arr.size();

    // Given K
    int K = 3;

    int S = 0;

    // Function Call
    findMaxSum(arr, N, min, K, S);

    // Print the value of S
    cout << S;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG{

static int S;

// Function to find the maximum sum of
// the array arr[] where each element
// can be reduced to at most min[i]
static void findMaxSum(int[] arr, int n,
                       int[] min, int k)
{

    // Stores the pair of arr[i] & min[i]
    ArrayList<int[]> A = new ArrayList<>();

    for(int i = 0; i < n; i++)
    {
        A.add(new int[]{arr[i], min[i]});
    }

    // Sorting vector of pairs
    Collections.sort(A, (a, b) -> b[0] - a[0]);

    int K = 0;

    // Traverse the vector of pairs
    for(int i = 0; i < n; i++)
    {

        // Add to the value of S
        S += Math.max(A.get(i)[0] - K,
                      A.get(i)[1]);

        // Update K
        K += k;
    }
}

// Driver code
public static void main (String[] args)
{

    // Given array arr[], min[]
    int[] arr = { 3, 5, 2, 1 };
    int[] min = { 3, 2, 1, 3 };

    int N = arr.length;

    // Given K
    int K = 3;

     S = 0;

    // Function Call
    findMaxSum(arr, N, min, K);

    // Print the value of S
    System.out.println(S);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum of
# the array arr[] where each element
# can be reduced to at most min[i]
def findMaxSum(arr, n, min, k, S):

    # Stores the pair of arr[i] & min[i]
    A = []

    for i in range(n):
        A.append((arr[i], min[i]))

    # Sorting vector of pairs
    A = sorted(A)
    A = A[::-1]

    K = 0

    # Traverse the vector of pairs
    for i in range(n):

        # Add to the value of S
        S += max(A[i][0] - K, A[i][1])

        # Update K
        K += k

    return S

# Driver Code
if __name__ == '__main__':

    arr, min = [], []

    # Given array arr[], min[]
    arr = [ 3, 5, 2, 1 ]
    min = [ 3, 2, 1, 3 ]

    N = len(arr)

    # Given K
    K = 3

    S = 0

    # Function Call
    S = findMaxSum(arr, N, min, K, S)

    # Print the value of S
    print(S)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

static int S;

// Function to find the maximum sum of
// the array arr[] where each element
// can be reduced to at most min[i]
static void findMaxSum(int[] arr, int n,
                       int[] min, int k)
{

    // Stores the pair of arr[i] & min[i]
    List<List<int>> A = new List<List<int>>();
    for(int i = 0; i < n; i++)
    {
        A.Add(new List<int>());
        A[i].Add(arr[i]);
        A[i].Add(min[i]);
    }

    // Sorting vector of pairs
    A = A.OrderBy(lst => lst[0]).ToList();
    A.Reverse();

    int K = 0;

    // Traverse the vector of pairs
    for(int i = 0; i < n; i++)
    {

        // Add to the value of S
        S += Math.Max(A[i][0] - K, A[i][1]);

        // Update K
        K += k;
    }
}

// Driver code
static public void Main()
{

    // Given array arr[], min[]
    int[] arr = { 3, 5, 2, 1 };
    int[] min = { 3, 2, 1, 3 };

    int N = arr.Length;

    // Given K
    int K = 3;

    S = 0;

    // Function Call
    findMaxSum(arr, N, min, K);

    // Print the value of S
    Console.WriteLine(S);
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program for the above approach

var S =0;

// Function to find the maximum sum of
// the array arr[] where each element
// can be reduced to at most min[i]
function findMaxSum(arr, n, min, k)
{
    // Stores the pair of arr[i] & min[i]
    var A = [];

    for (var i = 0; i < n; i++) {
        A.push([arr[i], min[i] ]);
    }

    // Sorting vector of pairs
    A.sort((a,b)=> b[0]-a[0]);

    var K = 0;

    // Traverse the vector of pairs
    for (var i = 0; i < n; i++) {

        // Add to the value of S
        S += Math.max(A[i][0] - K,
                A[i][1]);

        // Update K
        K += k;
    }
}

// Driver Code
var arr = [], min = [];
// Given array arr[], min[]
arr = [3, 5, 2, 1];
min = [3, 2, 1, 3];
var N = arr.length;
// Given K
var K = 3;
// Function Call
findMaxSum(arr, N, min, K, S);
// Print the value of S
document.write( S);

</script>
```

**Output:** 

```
12
```

***时间复杂度:** O(N*log N)，其中 N 为给定数组的长度。*
***辅助空间:** O(N)*
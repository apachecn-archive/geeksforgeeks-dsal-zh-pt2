# 任何大小的最大和子序列交替递减-递增

> 原文:[https://www . geeksforgeeks . org/任何大小的最大和子序列-递减-递增-交替/](https://www.geeksforgeeks.org/maximum-sum-subsequence-of-any-size-which-is-decreasing-increasing-alternatively/)

给定一个整数数组 **arr[]** ，求**子序列**的**最大和**，其元素先减少，后增加，反之亦然，子序列**可以在主序列的任何地方**开始，不一定在主序列的第一个元素。

> 一个序列 **{x1，x2，..xn}** 是一个交替序列，如果它的元素满足以下关系之一(如文章 [**中所述的最长交替子序列** )](https://www.geeksforgeeks.org/longest-alternating-subsequence/) :
> 
> 两个相邻的**相等的元素不算交替**。
> 
> x1 < x2 > x3 < x4 > x5 < …. xn 
> 或
> x1>x2<x3>x4<X5>…。数列

**示例:**

> **输入:** arr[] = {4，8，2，5，6，8}
> **输出:** 26
> **解释:**最大和的交替子序列为{4，8，6，8}。总和= 4 + 8 + 6 + 8 = 26
> 
> **输入:** arr[] = {0，1，1，1，3，2，5}
> **输出:** 11
> **解释:**最大和的交替子序列为{1，3，2，5}。总和= 1 + 3 + 2 + 5 = 11
> 
> **输入:** arr[] = {1，4，5}
> **输出:** 9
> **解释:**最大和的交替子序列为{4，5}。总和= 4 + 5 = 9
> 
> **输入:** arr[] = {1，0，1，0，0，3}
> **输出:** 5
> **说明:**最大和的交替子序列为{1，0，1，0，3}。总和= 1 + 0 + 1 + 0 + 3 = 5
> 
> **输入:** arr[] = {5，5 }
> T3】输出:5
> T6】说明:最大和的交替子序列为{5}。总和= 5

这个问题是 [**最大和交替子序列**](https://www.geeksforgeeks.org/maximum-sum-alternating-subsequence-sum/) 问题的延伸。与前面的问题不同，现在我们需要计算交替子序列**的最大和，不管它在主序列**中的什么位置，也不管它是以**两个元素上升**还是**两个元素下降**开始。

**方法:**这个问题可以通过 [**动态规划**](http://www.geeksforgeeks.org/dynamic-programming/) 结合**回溯**来解决。假设我们有一个数组 **arr[]** 带有任何 **N** 元素。

*   我们可以将每个 arr[i]元素视为交替序列的终止元素。
*   可以有许多交替的子序列，它们的**最后一个元素是 arr[i]** ，但是其中肯定有一个是具有最大和的序列。
*   此外，以 arr[i] 结束的交替子序列**的**最大和**不一定大于以 arr[i-1]结束的交替子序列**的**最大和**。**这是根据 [**回溯**](http://www.geeksforgeeks.org/backtracking-algorithms/) 技术实现算法的基础。**
*   让一个数组说出长度为 **N** 的 **maxSum[]** ，它将存储数组中每个元素结束的所有最大和 **arr[]** 。具体来说，maxSum[i]将存储以值 arr[i]结束的交替子序列的最大和。
*   我们将在[]之前使用另一个数组**来存储每个具有最大和的交替子序列的最后一个元素之前的值。**

> **例如**，数组 **arr[] = {1，5，7，3，4，5}** 将有一个交替的子序列{5，7，3，4}，其最大和为 5 + 7 + 3 + 4 = 19。
> 子序列{5，7，3，4}在值 4 处结束，该值在数组 **arr[]中有索引 4。**
> 所以我们有 arr[4] = 4，maxSum[4] = 19，在[4] = 3 之前(因为 arr[3] = 3)。
> 在计算过程中，这些值将被计算并保存到两个数组 maxSum[]和 before[]中，并且可以根据需要重用。

使用以下步骤实施该方法:

*   使用循环迭代数组 arr[]的每个元素。每次遍历 arr[i]元素时，我们都会查看它前面的元素:

> **i** 从 **1** 到 **N-1** 的循环遍历(不需要从位置 0 开始，因为那是基本情况):
> **j** 从 **0** 到 **i-1** 的循环遍历:

*   在每个状态 **i** 和 **j** 下，我们将根据动态规划的原理，使用 **0 < = j < i** 重用任何 maxSum[j]:

> if:
> (arr[I]>arr[j]&&arr[在[j]] > arr[j]之前)
> 或
> (arr[I]<arr[j]&&arr[在[j]] < arr[j]之前)
> 
> 然后:
> sum = arr[i] + maxSum[j]

*   如果 maxSum[j] **不满足**上述条件，则可以是**两个相等的元素**。因为两个相等的元素不被视为交替序列，所以我们只取其中的一个。

> if:
> arr[i] == arr[j]
> 
> 然后:
> sum = maxSum[j]

*   或者它可以不是上面的任何一个，例如具有多于两个的递增元素或者具有多于两个的递减元素。

> **例** {1，5，7， **3，4，5** }。假设我们在 **i = 5，j = 4** 。
> 
> *   那么【4】之前的**就是**第三元素**，并且(arr[在[j]之前]，arr[j]，arr[I])=(arr[在[4]之前]，arr[4]，arr[5]) = (arr[3]，arr[4]，arr[5]) = (3，4，5)。**
> *   上面一个是**不是有效的**交替子序列，意思是【j】之前的**是**不是**有效值的**指标。****
> *   我们将看一下 **arr 的**前置元素**【在[j]之前】**的交替顺序:在[在[j]之前] =在[3]之前= 2，arr[2]与 arr[4]和 arr[5]形成一个有效的子序列(7，4，5)。
> *   所以我们得到一个 arr[5] + arr[4] + maxSum[2]的值，这是状态{i = 5，j = 4}的最终和。
> *   我们需要**将其与**其他{i 和 j}** 状态(如{i = 5，j = 3}，{i = 5，j = 2 }……)进行比较，以获得 maxSum[5]的最终结果。**
> *   然后将 j 保存到 before[5]中，如果它在 arr[5]之前，并且有助于 arr[5]形成一个有效的子序列，其最大和在状态 5。

看一下下面的插图，把想法弄清楚。

> **索引**:0 1 2 3 4 5 | | N = 6
> **arr【】**:1，5，7，3，4，5
> 
> —————————————————————————————————-
> 
> maxSum[0]:**1**0 0 0 0 =**1**底壳
> 前[-1] : **-1** _ _ _ _ _
> 
> maxSum[1]:1**6**0 0 0 =**6**因为 1 + 5
> 先于[1] : -1 **0** _ _ _ _
> 
> maxSum[2]:1 6**12**0 0 0 =**12**因为 1，5，7 **不是交替的子序列**，在[2]之前只有 5&7
> :-1 0**1**_ _ _ 有效，所以我们在索引 2 处使用回溯，所以
> 我们将遍历以下子序列:{1，7}，{5，7}。我们有{5，7}是因为在[1]之前是索引 0，
> 我们继续在[before[1]] = -1 处寻找值，它的值是 0，所以 0 + 5 + 7 = 12 > 1 + 7。
> 
> maxSum[3]:1 6 12**15**0 0 =**15**因为 5，7，3 是有效的交替子序列，
> 在[3]之前:-1 0 1**2**_ _ so 3+max(maxSum[2]，maxSum[1]，maxSum[0]) = 3 + 12。
> 
> maxSum[4]:1 6 12 15**19**0 =**19**因为 5，7，3，4 是有效的交替子序列，
> 在[4]之前:-1 0 1 2**3**so _ 4+max(maxSum[3]，maxSum[2]，… maxSum[0]) = 4 + 15。
> 
> maxSum[5]:1 6 12 15 19**21**=**21**，arr[5]不能是 maxSum[4]的下一个元素，因为[5]之前的 3，4，5
> :-1 0 1 2 3**2**不是交替子序列。所以我们需要在这里使用回溯。
> 对于以 arr[5]结尾的交替子序列，我们将把值 3 视为无效值。
> 我们需要递归地在 maxSum[4]的和中找到 before[arr[4]]的前一个元素，
> 即索引 2。现在 7，4，5 已经形成了一个有效的交替子序列。
> 那么我们有 5 + max(回溯(索引 4)，maxSum[3]，maxSum[2]，…) = 5 + 16(因为 4 + 7 + 5)
> 那么，arr 的交替子序列的最终最大和就是“maxSum”数组的 max 元素。
> 
> **输出:** 21

下面是上述方法的实现:

## C++

```
// C++ code to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function for backtracking
int backtracking(int arr[], int maxSum[], int before[],
                 int N, int root, int bef_root,
                 int bbef_root)
{
    // {root, bef_root} represents state{i, j}
    // bbef_root represent before[before[j]]
    // We ignore the invalid before[j] index

    // Base case:
    if (bbef_root == -1)
        return arr[bef_root];

    // The case of a subsequence with
    // alternating parts:
    if ((arr[root] > arr[bef_root]
         && arr[bbef_root] > arr[bef_root])
        || (arr[root] < arr[bef_root]
            && arr[bbef_root] < arr[bef_root])) {
        return arr[bef_root] + maxSum[bbef_root];
    }

    // case (arr[bef_root] == arr[bbef_root])
    else {
        return backtracking(arr, maxSum, before, N, root,
                            bef_root, before[bbef_root]);
    }
}

int maxSumAlternatingSubsequence(int arr[], int N)
{

    // Max alternating subsequence sum
    // ending at arr[i].
    int maxSum[N];

    // Array to store the index of the element
    // preceeding the last element at maxSum[i]
    int before[N];

    // Value initialization for arrays:
    fill_n(&maxSum[0], N, 0);
    maxSum[0] = arr[0];
    before[0] = -1;

    // Iterate over the array:
    for (int i = 1; i < N; i++)
        for (int j = 0; j < i; j++) {
            int currentMax = 0;
            if ((arr[i] > arr[j]
                 && arr[before[j]] > arr[j])
                || (arr[i] < arr[j]
                    && arr[before[j]] < arr[j])
                || before[j] == -1) {

                // Whenever an element is
                // between two smaller elements
                //  or between two larger elements,
                //  it is an alternating sequence.
                //  When the preceding index of j is -1,
                //  we need to treat it explicitly,
                // because -1 is not a valid index.
                currentMax = (arr[i] == arr[j])
                                 ? maxSum[j]
                                 : arr[i] + maxSum[j];
            }

            else if (arr[i] == arr[j]) {
                // If arr[i] is equal to arr[j] then
                // only take it once,
                // before[j] cannot be equal to -1.
                currentMax = maxSum[j];
            }

            else {
                // Perform backtracking
                // If three adjacent elements
                // are increasing or decreasing.
                currentMax = arr[i]
                             + backtracking(
                                 arr, maxSum, before, N, i,
                                 j, before[before[j]]);
            }

            if (currentMax >= maxSum[i]) {
                // Stores the maximum sum and
                // the index preceding
                // the last element
                // at position i of
                // current alternating subsequence
                // after each iteration.
                maxSum[i] = currentMax;
                before[i] = j;
            }
        }

    // get max result in array
    return *max_element(maxSum, maxSum + N);
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 7, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(int);

    // Maximum sum of alternating subsequence
    // of array arr[]
    cout << maxSumAlternatingSubsequence(arr, N)
      << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.io.*;

class GFG{

// Function for backtracking
static int backtracking(int arr[], int maxSum[],
                        int before[], int N, int root,
                        int bef_root, int bbef_root)
{

    // {root, bef_root} represents state{i, j}
    // bbef_root represent before[before[j]]
    // We ignore the invalid before[j] index

    // Base case:
    if (bbef_root == -1)
        return arr[bef_root];

    // The case of a subsequence with
    // alternating parts:
    if ((arr[root] > arr[bef_root] &&
    arr[bbef_root] > arr[bef_root]) ||
        (arr[root] < arr[bef_root] &&
    arr[bbef_root] < arr[bef_root]))
    {
        return arr[bef_root] + maxSum[bbef_root];
    }

    // case (arr[bef_root] == arr[bbef_root])
    else
    {
        return backtracking(arr, maxSum, before, N,
                            root, bef_root,
                            before[bbef_root]);
    }
}

static int maxSumAlternatingSubsequence(int arr[],
                                        int N)
{

    // Max alternating subsequence sum
    // ending at arr[i].
    int maxSum[] = new int[N];

    // Array to store the index of the element
    // preceeding the last element at maxSum[i]
    int before[] = new int[N];

    // Value initialization for arrays:
    maxSum[0] = arr[0];
    before[0] = -1;

    // Iterate over the array:
    for(int i = 1; i < N; i++)
        for(int j = 0; j < i; j++)
        {
            int currentMax = 0;
            if ((arr[i] > arr[j] && before[j] != -1 &&
                   arr[before[j]] > arr[j]) ||
                          (arr[i] < arr[j] && before[j] != -1 &&
                   arr[before[j]] < arr[j]) || before[j] == -1)
            {

                // Whenever an element is
                // between two smaller elements
                // or between two larger elements,
                // it is an alternating sequence.
                // When the preceding index of j is -1,
                // we need to treat it explicitly,
                // because -1 is not a valid index.
                currentMax = (arr[i] == arr[j]) ? maxSum[j] :
                              arr[i] + maxSum[j];
            }

            else if (arr[i] == arr[j])
            {

                // If arr[i] is equal to arr[j] then
                // only take it once,
                // before[j] cannot be equal to -1.
                currentMax = maxSum[j];
            }
            else
            {

                // Perform backtracking
                // If three adjacent elements
                // are increasing or decreasing.
                currentMax = arr[i] + backtracking(arr, maxSum,
                                                   before, N, i, j,
                                                   before[before[j]]);
            }

            if (currentMax >= maxSum[i])
            {

                // Stores the maximum sum and the index
                // preceding the last element at position
                // i of current alternating subsequence
                // after each iteration.
                maxSum[i] = currentMax;
                before[i] = j;
            }
        }

    // get max result in array
    int maxi = 0;

    for(int i = 0; i < N; i++)
    {
        maxi = Math.max(maxSum[i], maxi);
    }
    return maxi;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 7, 3, 4, 5 };
    int N = arr.length;

    // Maximum sum of alternating subsequence
    // of array arr[]
    System.out.println(
        maxSumAlternatingSubsequence(arr, N));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python code to implement the above approach

# Function for backtracking
def backtracking(arr, maxSum, before, N, root, bef_root, bbef_root):

    # {root, bef_root} represents state{i, j}
    # bbef_root represent before[before[j]]
    # We ignore the invalid before[j] index

    # Base case:
    if (bbef_root == -1):
        return arr[bef_root]

    # The case of a subsequence with
    # alternating parts:
    if (arr[root] > arr[bef_root] and arr[bbef_root] > arr[bef_root]) or (arr[root] < arr[bef_root] and arr[bbef_root] < arr[bef_root]):
        return arr[bef_root] + maxSum[bbef_root]

    # case (arr[bef_root] == arr[bbef_root])
    else:
        return backtracking(arr, maxSum, before, N,
                            root, bef_root,
                            before[bbef_root])

def maxSumAlternatingSubsequence(arr, N):

    # Max alternating subsequence sum
    # ending at arr[i].
    maxSum = [0] * N

    # Array to store the index of the element
    # preceeding the last element at maxSum[i]
    before = [0] * N

    # Value initialization for arrays:
    maxSum[0] = arr[0]
    before[0] = -1

    # Iterate over the array:
    for i in range(N):
        for j in range(i):
            currentMax = 0
            if (arr[i] > arr[j] and before[j] != -1 and arr[before[j]] > arr[j]) or (arr[i] < arr[j] and before[j] != -1 and arr[before[j]] < arr[j]) or before[j] == -1:

                # Whenever an element is
                # between two smaller elements
                # or between two larger elements,
                # it is an alternating sequence.
                # When the preceding index of j is -1,
                # we need to treat it explicitly,
                # because -1 is not a valid index.
                currentMax = maxSum[j] if (
                    arr[i] == arr[j]) else arr[i] + maxSum[j]

            elif (arr[i] == arr[j]):

                # If arr[i] is equal to arr[j] then
                # only take it once,
                # before[j] cannot be equal to -1.
                currentMax = maxSum[j]
            else:

                # Perform backtracking
                # If three adjacent elements
                # are increasing or decreasing.
                currentMax = arr[i] + backtracking(arr, maxSum,
                                                   before, N, i, j,
                                                   before[before[j]])

            if (currentMax >= maxSum[i]):

                # Stores the maximum sum and the index
                # preceding the last element at position
                # i of current alternating subsequence
                # after each iteration.
                maxSum[i] = currentMax
                before[i] = j

    # get max result in array
    maxi = 0

    for i in range(N):
        maxi = max(maxSum[i], maxi)
    return maxi

# Driver code
arr = [1, 5, 7, 3, 4, 5]
N = len(arr)

# Maximum sum of alternating subsequence
# of array arr
print(maxSumAlternatingSubsequence(arr, N))

# This code is contributed by gfgking
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Function for backtracking
static int backtracking(int []arr, int []maxSum,
                        int []before, int N, int root,
                        int bef_root, int bbef_root)
{

    // {root, bef_root} represents state{i, j}
    // bbef_root represent before[before[j]]
    // We ignore the invalid before[j] index

    // Base case:
    if (bbef_root == -1)
        return arr[bef_root];

    // The case of a subsequence with
    // alternating parts:
    if ((arr[root] > arr[bef_root] &&
    arr[bbef_root] > arr[bef_root]) ||
        (arr[root] < arr[bef_root] &&
    arr[bbef_root] < arr[bef_root]))
    {
        return arr[bef_root] + maxSum[bbef_root];
    }

    // case (arr[bef_root] == arr[bbef_root])
    else
    {
        return backtracking(arr, maxSum, before, N,
                            root, bef_root,
                            before[bbef_root]);
    }
}

static int maxSumAlternatingSubsequence(int []arr,
                                        int N)
{

    // Max alternating subsequence sum
    // ending at arr[i].
    int []maxSum = new int[N];

    // Array to store the index of the element
    // preceeding the last element at maxSum[i]
    int []before = new int[N];

    // Value initialization for arrays:
    maxSum[0] = arr[0];
    before[0] = -1;

    // Iterate over the array:
    for(int i = 1; i < N; i++)
        for(int j = 0; j < i; j++)
        {
            int currentMax = 0;
            if ((arr[i] > arr[j] && before[j] != -1 &&
                   arr[before[j]] > arr[j]) ||
                          (arr[i] < arr[j] && before[j] != -1 &&
                   arr[before[j]] < arr[j]) || before[j] == -1)
            {

                // Whenever an element is
                // between two smaller elements
                // or between two larger elements,
                // it is an alternating sequence.
                // When the preceding index of j is -1,
                // we need to treat it explicitly,
                // because -1 is not a valid index.
                currentMax = (arr[i] == arr[j]) ? maxSum[j] :
                              arr[i] + maxSum[j];
            }

            else if (arr[i] == arr[j])
            {

                // If arr[i] is equal to arr[j] then
                // only take it once,
                // before[j] cannot be equal to -1.
                currentMax = maxSum[j];
            }
            else
            {

                // Perform backtracking
                // If three adjacent elements
                // are increasing or decreasing.
                currentMax = arr[i] + backtracking(arr, maxSum,
                                                   before, N, i, j,
                                                   before[before[j]]);
            }

            if (currentMax >= maxSum[i])
            {

                // Stores the maximum sum and the index
                // preceding the last element at position
                // i of current alternating subsequence
                // after each iteration.
                maxSum[i] = currentMax;
                before[i] = j;
            }
        }

    // get max result in array
    int maxi = 0;

    for(int i = 0; i < N; i++)
    {
        maxi = Math.Max(maxSum[i], maxi);
    }
    return maxi;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 5, 7, 3, 4, 5 };
    int N = arr.Length;

    // Maximum sum of alternating subsequence
    // of array arr[]
    Console.Write(
        maxSumAlternatingSubsequence(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// javascript code to implement the above approach

// Function for backtracking
function backtracking(arr , maxSum, before , N , root, bef_root , bbef_root)
{

    // {root, bef_root} represents state{i, j}
    // bbef_root represent before[before[j]]
    // We ignore the invalid before[j] index

    // Base case:
    if (bbef_root == -1)
        return arr[bef_root];

    // The case of a subsequence with
    // alternating parts:
    if ((arr[root] > arr[bef_root] &&
    arr[bbef_root] > arr[bef_root]) ||
        (arr[root] < arr[bef_root] &&
    arr[bbef_root] < arr[bef_root]))
    {
        return arr[bef_root] + maxSum[bbef_root];
    }

    // case (arr[bef_root] == arr[bbef_root])
    else
    {
        return backtracking(arr, maxSum, before, N,
                            root, bef_root,
                            before[bbef_root]);
    }
}

function maxSumAlternatingSubsequence(arr,N)
{

    // Max alternating subsequence sum
    // ending at arr[i].
    var maxSum = Array.from({length: N}, (_, i) => 0);

    // Array to store the index of the element
    // preceeding the last element at maxSum[i]
    var before = Array.from({length: N}, (_, i) => 0);

    // Value initialization for arrays:
    maxSum[0] = arr[0];
    before[0] = -1;

    // Iterate over the array:
    for(var i = 1; i < N; i++)
        for(var j = 0; j < i; j++)
        {
            var currentMax = 0;
            if ((arr[i] > arr[j] && before[j] != -1 &&
                   arr[before[j]] > arr[j]) ||
                          (arr[i] < arr[j] && before[j] != -1 &&
                   arr[before[j]] < arr[j]) || before[j] == -1)
            {

                // Whenever an element is
                // between two smaller elements
                // or between two larger elements,
                // it is an alternating sequence.
                // When the preceding index of j is -1,
                // we need to treat it explicitly,
                // because -1 is not a valid index.
                currentMax = (arr[i] == arr[j]) ? maxSum[j] :
                              arr[i] + maxSum[j];
            }

            else if (arr[i] == arr[j])
            {

                // If arr[i] is equal to arr[j] then
                // only take it once,
                // before[j] cannot be equal to -1.
                currentMax = maxSum[j];
            }
            else
            {

                // Perform backtracking
                // If three adjacent elements
                // are increasing or decreasing.
                currentMax = arr[i] + backtracking(arr, maxSum,
                                                   before, N, i, j,
                                                   before[before[j]]);
            }

            if (currentMax >= maxSum[i])
            {

                // Stores the maximum sum and the index
                // preceding the last element at position
                // i of current alternating subsequence
                // after each iteration.
                maxSum[i] = currentMax;
                before[i] = j;
            }
        }

    // get max result in array
    var maxi = 0;

    for(var i = 0; i < N; i++)
    {
        maxi = Math.max(maxSum[i], maxi);
    }
    return maxi;
}

// Driver code
var arr = [ 1, 5, 7, 3, 4, 5 ];
var N = arr.length;

// Maximum sum of alternating subsequence
// of array arr
document.write(
maxSumAlternatingSubsequence(arr, N));

// This code is contributed by 29AjayKumar
</script>
```

**Output**

```
21
```

**时间复杂度** : O(N <sup>2</sup> )，其中 N 为数组长度。
**辅助空间:** O(N)
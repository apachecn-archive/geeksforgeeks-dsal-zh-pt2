# 最小化将阵列划分为 K 个组的成本

> 原文:[https://www . geeksforgeeks . org/最小化将阵列划分为 k 个组的成本/](https://www.geeksforgeeks.org/minimize-the-cost-of-partitioning-an-array-into-k-groups/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是将数组划分为 **K** 个非空组，其中每个组都是给定数组的一个子数组，并且数组的每个元素都只是一个组的一部分。给定组中的所有元素必须具有相同的值。您可以多次执行以下操作:
从数组中选择一个元素，并将其值更改为任意值。打印分区阵列所需的最小操作数。
**示例:**

> **输入:** arr[] = {3，1，3，3，2，1，8，5}，K = 3
> **输出:** 3
> 通过将第 2 <sup>和第</sup>元素更改为 3，将第 6 <sup>元素更改为 2，将最后一个元素更改为 8，可以将数组划分为{3，3，3，2}和{8，8}
> 。
> **输入:** arr[] = {3，3，9，10}，K = 3
> **输出:** 0
> 将数组分成{3，3}、{9}和{10}
> 组，不执行任何操作。</sup>

**观察:**

*   如果 **K = 1** ，那么该组就是完整的数组本身。为了最大限度地减少所需的操作次数，最直观的做法是更改数组的所有元素，使其等于数组的[模式](https://www.geeksforgeeks.org/find-the-maximum-repeating-number-in-ok-time/)(频率最高的元素)。
*   对于 **K** 组，数组的最后一个元素将始终属于**K<sup>th</sup>T5】组，而**1<sup>ST</sup>T9】元素将属于**1<sup>ST</sup>T13】组。******
*   如果已经正确地找到了第**K**组，那么问题将简化为使用最小运算将剩余阵列划分为**K–1**组。

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。

1.  让 **DP(i，j)** 表示分割**数组【1】所需的最小运算..i]** 进 **j** 组。
2.  现在，任务是找到 **DP(N，K)** ，这是分割**阵列【1】所需的最小操作..n】**进入 **K** 组。
3.  基本情况 **DP(i，j)** 其中 **j = 1** 可以很容易回答。**自全阵【1..i]** 只需划分为一个组。根据观察，找到**阵列的模式[1..i]** 并更改**数组中的所有元素[1..i]** 到模式。如果模式发生了 **x** 次，那么**I–x**元素必须改变，即**I–x**操作。
4.  此后， **K <sup>第</sup>** 组在最后一个元素结束。然而，它可能从各种可能的位置开始。假设 **K <sup>第</sup>** 组从某个指标 **it** 开始，然后**数组【it..N]** 需要划分成单个组和**数组[1..(it–1)】**需要划分为**K–1**组。划分**数组的成本[1..(it–1)】**分成**K–1**组是**DP(it–1，K–1)**和划分**数组的成本【it..N]** 在单个组中可以使用模式和它的频率观测来计算。
5.  找出一个范围内出现频率最高的元素**【它..i]** 我们可以使用一个 hashmap 和一个整型变量。整数变量表示当前最高频率。该地图存储了迄今为止看到的所有元素及其频率。每当看到一个元素，它的频率就会在地图中增加，如果现在这个元素的频率高于当前最高频率，我们会将当前最高频率更新为刚才看到的元素的频率。方法参见[本](https://www.geeksforgeeks.org/median-and-mode-using-counting-sort/)。
6.  因此 **DP(i，j)** 是**DP(it–1，j–1)+分区数组[it]成本的最小值..我】进入 1 组**为所有可能的值**它**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of operations needed to partition
// the array in k contiguous groups
// such that all elements of a
// given group are identical
int getMinimumOps(vector<int> ar, int k)
{
    // n is the size of the array
    int n = ar.size();

    // dp(i, j) represents the minimum cost for
    // partitioning the array[0..i] into j groups
    int dp[n][k + 1];

    // Base case, cost is 0 for parititoning the
    // array[0..0] into 1 group
    dp[0][1] = 0;

    // Fill dp(i, j) and the answer will
    // be stored at dp(n-1, k)
    for (int i = 1; i < n; i++) {

        // The maximum groups that the segment 0..i can
        // be divided in is represented by maxGroups
        int maxGroups = min(k, i + 1);

        for (int j = 1; j <= maxGroups; j++) {

            // Initialize dp(i, j) to infinity
            dp[i][j] = INT_MAX;

            // Divide segment 0..i in 1 group
            if (j == 1) {

                // map and freqOfMode are together used to
                // keep track of the frequency of the most
                // occurring element in [0..i]
                unordered_map<int, int> freq;
                int freqOfMode = 0;
                for (int it = 0; it <= i; it++) {
                    freq[ar[it]]++;
                    int newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;
                }

                // Change all the elements in the range
                // 0..i to the most frequent element
                // in this range
                dp[i][1] = (i + 1) - freqOfMode;
            }
            else {
                unordered_map<int, int> freq;
                int freqOfMode = 0;

                // If the jth group is the segment from
                // it..i, we change all the elements in this
                // range to this range's most occurring element
                for (int it = i; it >= j - 1; it--) {
                    freq[ar[it]]++;
                    int newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;

                    // Number of elements we need to change
                    // in the jth group i.e. the range it..i
                    int elementsToChange = i - it + 1;
                    elementsToChange -= freqOfMode;

                    // For all the possible sizes of the jth
                    // group that end at the ith element
                    // we pick the size that gives us the minimum
                    // cost for dp(i, j)
                    // elementsToChange is the cost of making
                    // all the elements in the jth group identical
                    // and we make use of dp(it - 1, j - 1) to
                    // find the overall minimal cost
                    dp[i][j] = min(dp[it - 1][j - 1]
                                       + elementsToChange,
                                   dp[i][j]);
                }
            }
        }
    }

    // Return the minimum cost for
    // partitioning array[0..n-1]
    // into k groups which is
    // stored at dp(n-1, k)
    return dp[n - 1][k];
}

// Driver code
int main()
{
    int k = 3;
    vector<int> ar = { 3, 1, 3, 3, 2, 1, 8, 5 };

    cout << getMinimumOps(ar, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

// Function to return the minimum number
// of operations needed to partition
// the array in k contiguous groups
// such that all elements of a
// given group are identical
static int getMinimumOps(int ar[], int k)
{
    // n is the size of the array
    int n = ar.length;

    // dp(i, j) represents the minimum cost for
    // partitioning the array[0..i] into j groups
    int dp[][] = new int[n][k + 1];

    // Base case, cost is 0 for parititoning the
    // array[0..0] into 1 group
    dp[0][1] = 0;

    // Fill dp(i, j) and the answer will
    // be stored at dp(n-1, k)
    for (int i = 1; i < n; i++)
    {

        // The maximum groups that the segment 0..i can
        // be divided in is represented by maxGroups
        int maxGroups = Math.min(k, i + 1);

        for (int j = 1; j <= maxGroups; j++)
        {

            // Initialize dp(i, j) to infinity
            dp[i][j] = Integer.MAX_VALUE;

            // Divide segment 0..i in 1 group
            if (j == 1)
            {

                // map and freqOfMode are together used to
                // keep track of the frequency of the most
                // occurring element in [0..i]
                int freq[] = new int[100000];
                int freqOfMode = 0;
                for (int it = 0; it <= i; it++)
                {
                    freq[ar[it]]++;
                    int newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;
                }

                // Change all the elements in the range
                // 0..i to the most frequent element
                // in this range
                dp[i][1] = (i + 1) - freqOfMode;
            }
            else
            {
                int freq[] = new int[100000];
                int freqOfMode = 0;

                // If the jth group is the segment from
                // it..i, we change all the elements in this
                // range to this range's most occurring element
                for (int it = i; it >= j - 1; it--)
                {
                    freq[ar[it]]++;
                    int newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;

                    // Number of elements we need to change
                    // in the jth group i.e. the range it..i
                    int elementsToChange = i - it + 1;
                    elementsToChange -= freqOfMode;

                    // For all the possible sizes of the jth
                    // group that end at the ith element
                    // we pick the size that gives us the minimum
                    // cost for dp(i, j)
                    // elementsToChange is the cost of making
                    // all the elements in the jth group identical
                    // and we make use of dp(it - 1, j - 1) to
                    // find the overall minimal cost
                    dp[i][j] = Math.min(dp[it - 1][j - 1] +
                                        elementsToChange, dp[i][j]);
                }
            }
        }
    }

    // Return the minimum cost for
    // partitioning array[0..n-1]
    // into k groups which is
    // stored at dp(n-1, k)
    return dp[n - 1][k];
}

// Driver code
public static void main(String args[])
{
    int k = 3;
    int ar[] = { 3, 1, 3, 3, 2, 1, 8, 5 };

    System.out.println(getMinimumOps(ar, k));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number
# of operations needed to partition
# the array in k contiguous groups
# such that all elements of a
# given group are identical
def getMinimumOps(ar, k):

    # n is the size of the array
    n = len(ar)

    # dp(i, j) represents the minimum cost for
    # partitioning the array[0..i] into j groups
    dp = [[ 0 for i in range(k + 1)]
              for i in range(n)]

    # Base case, cost is 0 for parititoning the
    # array[0..0] into 1 group
    dp[0][1] = 0

    # Fill dp(i, j) and the answer will
    # be stored at dp(n-1, k)
    for i in range(1, n):

        # The maximum groups that the segment 0..i can
        # be divided in is represented by maxGroups
        maxGroups = min(k, i + 1)

        for j in range(1, maxGroups + 1):

            # Initialize dp(i, j) to infinity
            dp[i][j] = 10**9

            # Divide segment 0..i in 1 group
            if (j == 1):

                # map and freqOfMode are together used to
                # keep track of the frequency of the most
                # occurring element in [0..i]
                freq1 = dict()
                freqOfMode = 0
                for it in range(0, i + 1):

                    freq1[ar[it]] = freq1.get(ar[it], 0) + 1
                    newElementFreq = freq1[ar[it]]
                    if (newElementFreq > freqOfMode):
                        freqOfMode = newElementFreq

                # Change all the elements in the range
                # 0..i to the most frequent element
                # in this range
                dp[i][1] = (i + 1) - freqOfMode

            else:
                freq = dict()
                freqOfMode = 0

                # If the jth group is the segment from
                # it..i, we change all the elements in this
                # range to this range's most occurring element
                for it in range(i, j - 2, -1):

                    #print(i,j,it)
                    freq[ar[it]] = freq.get(ar[it], 0) + 1
                    newElementFreq = freq[ar[it]]
                    if (newElementFreq > freqOfMode):
                        freqOfMode = newElementFreq

                    # Number of elements we need to change
                    # in the jth group i.e. the range it..i
                    elementsToChange = i - it + 1
                    elementsToChange -= freqOfMode

                    # For all the possible sizes of the jth
                    # group that end at the ith element
                    # we pick the size that gives us the minimum
                    # cost for dp(i, j)
                    # elementsToChange is the cost of making
                    # all the elements in the jth group identical
                    # and we make use of dp(it - 1, j - 1) to
                    # find the overall minimal cost
                    dp[i][j] = min(dp[it - 1][j - 1] + 
                                   elementsToChange, dp[i][j])

    # Return the minimum cost for
    # partitioning array[0..n-1]
    # into k groups which is
    # stored at dp(n-1, k)
    return dp[n - 1][k]

# Driver code
k = 3
ar =[3, 1, 3, 3, 2, 1, 8, 5]

print(getMinimumOps(ar, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to return the minimum number
// of operations needed to partition
// the array in k contiguous groups
// such that all elements of a
// given group are identical
static int getMinimumOps(int []ar, int k)
{
    // n is the size of the array
    int n = ar.Length;

    // dp(i, j) represents the minimum cost for
    // partitioning the array[0..i] into j groups
    int [,]dp = new int[n, k + 1];

    // Base case, cost is 0 for parititoning the
    // array[0..0] into 1 group
    dp[0, 1] = 0;

    // Fill dp(i, j) and the answer will
    // be stored at dp(n-1, k)
    for (int i = 1; i < n; i++)
    {

        // The maximum groups that the segment 0..i can
        // be divided in is represented by maxGroups
        int maxGroups = Math.Min(k, i + 1);

        for (int j = 1; j <= maxGroups; j++)
        {

            // Initialize dp(i, j) to infinity
            dp[i, j] = int.MaxValue;

            // Divide segment 0..i in 1 group
            if (j == 1)
            {

                // map and freqOfMode are together used to
                // keep track of the frequency of the most
                // occurring element in [0..i]
                int []freq = new int[100000];
                int freqOfMode = 0;
                for (int it = 0; it <= i; it++)
                {
                    freq[ar[it]]++;
                    int newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;
                }

                // Change all the elements in the range
                // 0..i to the most frequent element
                // in this range
                dp[i, 1] = (i + 1) - freqOfMode;
            }
            else
            {
                int []freq = new int[100000];
                int freqOfMode = 0;

                // If the jth group is the segment from
                // it..i, we change all the elements in this
                // range to this range's most occurring element
                for (int it = i; it >= j - 1; it--)
                {
                    freq[ar[it]]++;
                    int newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;

                    // Number of elements we need to change
                    // in the jth group i.e. the range it..i
                    int elementsToChange = i - it + 1;
                    elementsToChange -= freqOfMode;

                    // For all the possible sizes of the jth
                    // group that end at the ith element
                    // we pick the size that gives us the minimum
                    // cost for dp(i, j)
                    // elementsToChange is the cost of making
                    // all the elements in the jth group identical
                    // and we make use of dp(it - 1, j - 1) to
                    // find the overall minimal cost
                    dp[i, j] = Math.Min(dp[it - 1, j - 1] +
                                        elementsToChange, dp[i, j]);
                }
            }
        }
    }

    // Return the minimum cost for
    // partitioning array[0..n-1]
    // into k groups which is
    // stored at dp(n-1, k)
    return dp[n - 1, k];
}

// Driver code
public static void Main(String []args)
{
    int k = 3;
    int []ar = {3, 1, 3, 3, 2, 1, 8, 5};

    Console.WriteLine(getMinimumOps(ar, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to return the minimum number
// of operations needed to partition
// the array in k contiguous groups
// such that all elements of a
// given group are identical
function getMinimumOps(ar, k)
{

    // n is the size of the array
    let n = ar.length;

    // dp(i, j) represents the minimum cost for
    // partitioning the array[0..i] into j groups
    let dp = new Array(n);
    for(let i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(k+1);
        for(let j = 0; j < (k + 1); j++)
        {
            dp[i][j] = 0;
        }
    }

    // Base case, cost is 0 for parititoning the
    // array[0..0] into 1 group
    dp[0][1] = 0;

    // Fill dp(i, j) and the answer will
    // be stored at dp(n-1, k)
    for (let i = 1; i < n; i++)
    {

        // The maximum groups that the segment 0..i can
        // be divided in is represented by maxGroups
        let maxGroups = Math.min(k, i + 1);

        for (let j = 1; j <= maxGroups; j++)
        {

            // Initialize dp(i, j) to infinity
            dp[i][j] = Number.MAX_VALUE;

            // Divide segment 0..i in 1 group
            if (j == 1)
            {

                // map and freqOfMode are together used to
                // keep track of the frequency of the most
                // occurring element in [0..i]
                let freq = new Array(100000);
                for(let i=0;i<freq.length;i++)
                {
                    freq[i]=0;
                }
                let freqOfMode = 0;
                for (let it = 0; it <= i; it++)
                {
                    freq[ar[it]]++;
                    let newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;
                }

                // Change all the elements in the range
                // 0..i to the most frequent element
                // in this range
                dp[i][1] = (i + 1) - freqOfMode;
            }
            else
            {
                let freq = new Array(100000);
                for(let i = 0; i < freq.length; i++)
                {
                    freq[i] = 0;
                }
                let freqOfMode = 0;

                // If the jth group is the segment from
                // it..i, we change all the elements in this
                // range to this range's most occurring element
                for (let it = i; it >= j - 1; it--)
                {
                    freq[ar[it]]++;
                    let newElementFreq = freq[ar[it]];
                    if (newElementFreq > freqOfMode)
                        freqOfMode = newElementFreq;

                    // Number of elements we need to change
                    // in the jth group i.e. the range it..i
                    let elementsToChange = i - it + 1;
                    elementsToChange -= freqOfMode;

                    // For all the possible sizes of the jth
                    // group that end at the ith element
                    // we pick the size that gives us the minimum
                    // cost for dp(i, j)
                    // elementsToChange is the cost of making
                    // all the elements in the jth group identical
                    // and we make use of dp(it - 1, j - 1) to
                    // find the overall minimal cost
                    dp[i][j] = Math.min(dp[it - 1][j - 1] +
                                        elementsToChange, dp[i][j]);
                }
            }
        }
    }

    // Return the minimum cost for
    // partitioning array[0..n-1]
    // into k groups which is
    // stored at dp(n-1, k)
    return dp[n - 1][k];
}

// Driver code
let k = 3;
let ar=[3, 1, 3, 3, 2, 1, 8, 5 ];
document.write(getMinimumOps(ar, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N * N * K)，其中 N 为数组的大小，K 为数组应划分的组数。
**空间复杂度:** O(N * K)
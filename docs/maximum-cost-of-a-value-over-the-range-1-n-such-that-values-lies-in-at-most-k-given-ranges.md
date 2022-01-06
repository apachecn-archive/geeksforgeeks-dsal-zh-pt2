# 值在范围[1，N]内的最大成本，使得值最多位于 K 个给定范围内

> 原文:[https://www . geesforgeks . org/最大超范围价值成本-1-n-这样的价值位于最多 k 个给定范围内/](https://www.geeksforgeeks.org/maximum-cost-of-a-value-over-the-range-1-n-such-that-values-lies-in-at-most-k-given-ranges/)

给定正整数 **N** 和类型为 **{L，R，C}** 的大小为 **M** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，使得 **C** 是选择范围**【L，R】**中的元素的成本，而正整数 **K** 是寻找范围**【1，N】内的值的最大成本**

**示例:**

> **输入:** arr[] = {{2，8，800}，{6，9，1500}，{4，7，200}，{3，5，400}}，K = 2
> **输出:** 2300
> **解释:**
> 选择的项目是 6，选择的成本是第 0 和第 1 个指数，因此 6 属于 2 到 8 和 6 到 9 的范围。因此，成本 800 + 1500 的总和是 2300，这是最大值。
> 
> **输入:** arr[] = {{1，3，400}，{5，5，500}，{2，3，300}}，K = 3
> **输出:** 700

**方法:**给定的问题可以通过存储位于区间范围 L 到 R 内的每个项目 **i** 的所有成本，以及[以非递增顺序排序所选成本](https://www.geeksforgeeks.org/insertion-sort/)来解决。然后比较所有项目第一个 **K** 成本的[之和。可以遵循以下步骤:](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)

*   初始化一个变量，说**tomaxsum = 0**存储成本的最大和。
*   初始化一个变量，说 **sum = 0** 来存储**I<sup>th</sup>T5】项的成本总和。**
*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **currCost** 来存储**I<sup>th</sup>T7】项目的成本。**
*   使用变量 **i** 迭代**【1，N】**的范围，使用变量 **j** 嵌套[迭代**【0，M–1】**的范围，并执行以下步骤:](https://www.geeksforgeeks.org/range-based-loop-c/)
    *   如果 **i** 的值在**【arr[I][0]、arr[I][1]】**的范围内，则将 **arr[i][2]** 的值添加到向量 **currCost** 中。
    *   [按非递增顺序对向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **currCost** 进行排序。
    *   [迭代向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **currCost** 并将第一个 **K** 元素的值加到**和**上。
    *   通过**max(tomaxsum，sum)** 更新**tomaxsum**的值。
*   完成以上步骤后，打印**tomaxsum**的值作为最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the total cost
// by choosing an item which lies in
// the interval L to R
void maxTotalCost(vector<vector<int> >& arr,
                  int M, int N, int K)
{
    // Stores the total maximum sum
    int totMaxSum = 0;

    for (int i = 1; i <= N; ++i) {

        // Stores the cost for ith item
        vector<int> currCost;

        for (int j = 0; j < M; ++j) {

            // Check if the ith item
            // belongs in the interval
            if (arr[j][0] <= i
                && arr[j][1] >= i) {

                // Add the the jth cost
                currCost.push_back(arr[j][2]);
            }
        }

        // Sort the currCost[] in the
        // non increasing order
        sort(currCost.begin(),
             currCost.end(),
             greater<int>());

        // Stores the ith item sum
        int sum = 0;

        // Choose at most K costs
        for (int j = 0;
             j < K
             && j < currCost.size();
             ++j) {

            // Update the sum
            sum += currCost[j];
        }

        // Update the totMaxSum
        totMaxSum = max(totMaxSum, sum);
    }

    // Print the value of totMaxSum
    cout << totMaxSum << endl;
}

// Driver Code
int main()
{
    int N = 10;
    vector<vector<int> > arr = { { 2, 8, 800 },
                                 { 6, 9, 1500 },
                                 { 4, 7, 200 },
                                 { 3, 5, 400 } };
    int M = arr.size();
    int K = 2;

    maxTotalCost(arr, M, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to maximize the total cost
// by choosing an item which lies in
// the interval L to R
static void maxTotalCost(int[][] arr,
                  int M, int N, int K)
{

    // Stores the total maximum sum
    int totMaxSum = 0;

    for (int i = 1; i <= N; ++i) {

        // Stores the cost for ith item
        Vector<Integer> currCost = new Vector<Integer>();

        for (int j = 0; j < M; ++j) {

            // Check if the ith item
            // belongs in the interval
            if (arr[j][0] <= i
                && arr[j][1] >= i) {

                // Add the the jth cost
                currCost.add(arr[j][2]);
            }
        }

        // Sort the currCost[] in the
        // non increasing order
        Collections.sort(currCost,Collections.reverseOrder());

        // Stores the ith item sum
        int sum = 0;

        // Choose at most K costs
        for (int j = 0;
             j < K
             && j < currCost.size();
             ++j) {

            // Update the sum
            sum += currCost.get(j);
        }

        // Update the totMaxSum
        totMaxSum = Math.max(totMaxSum, sum);
    }

    // Print the value of totMaxSum
    System.out.print(totMaxSum +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;
    int[][]  arr = { { 2, 8, 800 },
                                 { 6, 9, 1500 },
                                 { 4, 7, 200 },
                                 { 3, 5, 400 } };
    int M = arr.length;
    int K = 2;

    maxTotalCost(arr, M, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach

# Function to maximize the total cost
# by choosing an item which lies in
# the interval L to R
def maxTotalCost(arr, M, N, K):

    # Stores the total maximum sum
    totMaxSum = 0

    for i in range(1, N + 1):

        # Stores the cost for ith item
        currCost = []

        for j in range(0, M):

            # Check if the ith item
            # belongs in the interval
            if (arr[j][0] <= i and arr[j][1] >= i):

                # Add the the jth cost
                currCost.append(arr[j][2])

                # Sort the currCost[] in the
                # non increasing order
        currCost.sort()

        # Stores the ith item sum
        sum = 0

        # Choose at most K costs
        for j in range(0, K):

                        # Update the sum
            if j >= len(currCost):
                break
            sum += currCost[j]

            # Update the totMaxSum
        totMaxSum = max(totMaxSum, sum)

        # Print the value of totMaxSum
    print(totMaxSum)

# Driver Code
if __name__ == "__main__":

    N = 10
    arr = [[2, 8, 800],
           [6, 9, 1500],
           [4, 7, 200],
           [3, 5, 400]
           ]
    M = len(arr)
    K = 2

    maxTotalCost(arr, M, N, K)

    # This code is contributed by rakeshsahni
```

## C#

```
// C++ program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to maximize the total cost
    // by choosing an item which lies in
    // the interval L to R
    static void maxTotalCost(int[, ] arr, int M, int N,
                             int K)
    {
        // Stores the total maximum sum
        int totMaxSum = 0;

        for (int i = 1; i <= N; ++i) {

            // Stores the cost for ith item
            List<int> currCost = new List<int>();

            for (int j = 0; j < M; ++j) {

                // Check if the ith item
                // belongs in the interval
                if (arr[j, 0] <= i && arr[j, 1] >= i) {

                    // Add the the jth cost
                    currCost.Add(arr[j, 2]);
                }
            }

            // Sort the currCost[] in the
            // non increasing order
            currCost.Sort();

            // Stores the ith item sum
            int sum = 0;

            // Choose at most K costs
            for (int j = 0; j < K && j < currCost.Count;
                 ++j) {

                // Update the sum
                sum += currCost[j];
            }

            // Update the totMaxSum
            totMaxSum = Math.Max(totMaxSum, sum);
        }

        // Print the value of totMaxSum
        Console.WriteLine(totMaxSum);
    }

    // Driver Code
    public static void Main()
    {
        int N = 10;
        int[, ] arr = { { 2, 8, 800 },
                        { 6, 9, 1500 },
                        { 4, 7, 200 },
                        { 3, 5, 400 } };
        int M = arr.GetLength(0);
        int K = 2;

        maxTotalCost(arr, M, N, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to maximize the total cost
        // by choosing an item which lies in
        // the interval L to R
        function maxTotalCost(arr,
            M, N, K)
        {

            // Stores the total maximum sum
            let totMaxSum = 0;

            for (let i = 1; i <= N; ++i) {

                // Stores the cost for ith item
                let currCost = [];

                for (let j = 0; j < M; ++j) {

                    // Check if the ith item
                    // belongs in the interval
                    if (arr[j][0] <= i
                        && arr[j][1] >= i) {

                        // Add the the jth cost
                        currCost.push(arr[j][2]);
                    }
                }

                // Sort the currCost[] in the
                // non increasing order
                currCost.sort(function (a, b) { return b - a })

                // Stores the ith item sum
                let sum = 0;

                // Choose at most K costs
                for (let j = 0;
                    j < K
                    && j < currCost.length;
                    ++j) {

                    // Update the sum
                    sum += currCost[j];
                }

                // Update the totMaxSum
                totMaxSum = Math.max(totMaxSum, sum);
            }

            // Print the value of totMaxSum
            document.write(totMaxSum + '<br>');
        }

        // Driver Code
        let N = 10;
        let arr = [[2, 8, 800],
        [6, 9, 1500],
        [4, 7, 200],
        [3, 5, 400]];
        let M = arr.length;
        let K = 2;

        maxTotalCost(arr, M, N, K);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2300
```

***时间复杂度:**O(N * M * log M)*
T5**辅助空间:** O(N*M)
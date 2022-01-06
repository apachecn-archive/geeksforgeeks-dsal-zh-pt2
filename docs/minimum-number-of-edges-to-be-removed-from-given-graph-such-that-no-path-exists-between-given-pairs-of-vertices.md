# 从给定图形中移除的最小边数，使得给定顶点对之间不存在路径

> 原文:[https://www . geeksforgeeks . org/给定图的最小移除边数-给定顶点对之间不存在路径/](https://www.geeksforgeeks.org/minimum-number-of-edges-to-be-removed-from-given-graph-such-that-no-path-exists-between-given-pairs-of-vertices/)

给定一个由在范围**【1，N】**上取值的 **N** 组成的无向图，使得顶点 **(i，i + 1)** 相连，以及一个由 **M** [对整数](https://www.geeksforgeeks.org/pair-in-cpp-stl/)组成的[数组**arr【】**，任务是找到应该从图中移除的最小边数，使得每对 **(u，v)不存在任何路径**](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> **输入:** arr[] = {{1，4}，{2，5}
> **输出:** 1
> **解释:**
> 对于 N = 5，给定的图可以表示为:
> 
> 1 2 3 4 5
> 
> 移除顶点 2 和 3 之间的边或顶点 3 和 4 之间的边后，图形将修改为:
> 
> 1 2 3 4 5
> 
> 现在，阵列中的每对节点之间不存在任何路径。因此，应该移除的最小边数为 1。
> 
> **输入:** arr[] = {{1，8}、{2，7}、{3，5}、{4，6}、{7，9}}
> **输出:** 2

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。其思想是[按照结束对的递增顺序对给定的对数组](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)**arr【】**进行排序，对于每个对，假设 **(u，v)** 移除与顶点 **v** 连接的最近边，以便包含顶点 **v** 的[连接组件](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)上的所有其他顶点都不可达。按照以下步骤解决给定的问题:

*   创建一个变量，比如说**将**设为 **0** ，存储移除的边的数量。
*   创建一个变量**可达**作为 **0** ，它跟踪从最后一个顶点可达的最小顶点，即 **N** 。
*   [按照配对的第二个值](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的递增顺序对给定的配对数组 **arr[]** 进行排序。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**对于**arr【】**中的每一对 **(u，v)** ，如果**可达> u** ，则表示 **u** 和 **v** 之间不存在路径，否则去除**(v–1)**和 **v** 之间的最后一条边是最理想的选择。因此，将 **minEdges** 的值增加 **1** ，则**可达**的值将等于 **v** 。
*   完成以上步骤后，打印**的值，结果为**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator function to sort the
// given array of pairs in increasing
// order of second value of the pairs
bool comp(pair<int, int> a, pair<int, int> b)
{
    if (a.second < b.second) {
        return true;
    }
    return false;
}

// Function to find minimum number of edges
// to be removed such that there exist no
// path between each pair in the array arr[]
int findMinEdges(vector<pair<int, int> > arr,
                 int N)
{
    // Stores the count of edges to be deleted
    int minEdges = 0;

    // Stores the smallest vertex rechable
    // from the current vertex
    int reachable = 0;

    // Sort the array arr[] in increasing
    // order of the second value of the pair
    sort(arr.begin(), arr.end(), comp);

    // Loop to iterate through array arr[]
    for (int i = 0; i < arr.size(); i++) {

        // If rechable > arr[i].first, there
        // exist no path between arr[i].first
        // and arr[i].second, hence continue
        if (reachable > arr[i].first)
            continue;

        else {
            // Update the rechable vertex
            reachable = arr[i].second;

            // Increment minEdges by 1
            minEdges++;
        }
    }

    // Return answer
    return minEdges;
}

// Driver Code
int main()
{
    vector<pair<int, int> > arr = {
        { 1, 8 }, { 2, 7 }, { 3, 5 }, { 4, 6 }, { 7, 9 }
    };
    int N = arr.size();
    cout << findMinEdges(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG
{

    // Comparator function to sort the
    // given array of pairs in increasing
    // order of second value of the pairs

    // Function to find minimum number of edges
    // to be removed such that there exist no
    // path between each pair in the array arr[]
    public static int findMinEdges(int[][] arr, int N)
    {

        // Stores the count of edges to be deleted
        int minEdges = 0;

        // Stores the smallest vertex rechable
        // from the current vertex
        int reachable = 0;

        // Sort the array arr[] in increasing
        // order of the second value of the pair
        Arrays.sort(arr, (a, b) -> (a[1] - b[1]));

        // Loop to iterate through array arr[]
        for (int i = 0; i < arr.length; i++) {

            // If rechable > arr[i][0], there
            // exist no path between arr[i][0]
            // and arr[i][1], hence continue
            if (reachable > arr[i][0])
                continue;

            else {
                // Update the rechable vertex
                reachable = arr[i][1];

                // Increment minEdges by 1
                minEdges++;
            }
        }

        // Return answer
        return minEdges;
    }

    // Driver Code
    public static void main(String args[]) {
        int[][] arr = { { 1, 8 }, { 2, 7 }, { 3, 5 }, { 4, 6 }, { 7, 9 } };
        int N = arr.length;
        System.out.println(findMinEdges(arr, N));
    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Comparator function to sort the
# given array of pairs in increasing
# order of second value of the pairs

# Function to find minimum number of edges
# to be removed such that there exist no
# path between each pair in the array arr[]
def findMinEdges(arr, N):
    # Stores the count of edges to be deleted
    minEdges = 0

    # Stores the smallest vertex rechable
    # from the current vertex
    reachable = 0

    # Sort the array arr[] in increasing
    # order of the second value of the pair
    arr.sort()

    # Loop to iterate through array arr[]
    for i in range(len(arr)):
        # If rechable > arr[i].first, there
        # exist no path between arr[i].first
        # and arr[i].second, hence continue
        if (reachable > arr[i][0]):
            continue

        else:
            # Update the rechable vertex
            reachable = arr[i][1]

            # Increment minEdges by 1
            minEdges += 1

    # Return answer
    return minEdges+1

# Driver Code
if __name__ == '__main__':
    arr = [[1, 8],[2, 7],[3, 5],[4, 6],[7, 9]]
    N = len(arr)
    print(findMinEdges(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find minimum number of edges
        // to be removed such that there exist no
        // path between each pair in the array arr[]
        function findMinEdges(arr,
            N)
        {

            // Stores the count of edges to be deleted
            let minEdges = 0;

            // Stores the smallest vertex rechable
            // from the current vertex
            let reachable = 0;

            // Sort the array arr[] in increasing
            // order of the second value of the pair
            arr.sort(function (a, b) { return a.second - b.second })

            // Loop to iterate through array arr[]
            for (let i = 0; i < arr.length; i++) {

                // If rechable > arr[i].first, there
                // exist no path between arr[i].first
                // and arr[i].second, hence continue
                if (reachable > arr[i].first)
                    continue;

                else {
                    // Update the rechable vertex
                    reachable = arr[i].second;

                    // Increment minEdges by 1
                    minEdges++;
                }
            }

            // Return answer
            return minEdges;
        }

        // Driver Code
        let arr = [{first: 1, second: 8},
              { first: 2, second: 7 },
            { first: 3, second: 5 },
            { first: 4, second: 6 },
            { first: 7, second: 9 }];
        let N = arr.length;
        document.write(findMinEdges(arr, N));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(M*log M)*
***辅助空间:** O(1)*
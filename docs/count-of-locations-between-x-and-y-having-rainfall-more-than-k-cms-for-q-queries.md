# Q 查询降雨大于 K 厘米的 X 和 Y 之间的位置计数

> 原文:[https://www . geeksforgeeks . org/x-和-y-之间的雨量超过 k-CMS-for-q-query/](https://www.geeksforgeeks.org/count-of-locations-between-x-and-y-having-rainfall-more-than-k-cms-for-q-queries/)

给定由 **N** 三元组(cms 中的开始、结束、降雨)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】【】**，定义降雨将从 cms 中给定降雨强度的开始位置到结束位置。也给定一个整数 **K** 和 **Q** 以数组的形式查询**查询[][]** (在每个查询中给出 **X** 和 **Y** )。对于每个查询，任务是查找降雨量超过 **K** cms 的 **X** 和 **Y** (含)之间的位置数量。

**示例:**

> **输入:** arr[][] = {{1，3，5}，{2，8，3}，{5，8，2}，{7，9，6}}，K = 5，查询[][] = {{1，5}，{5，9}，{2，9}，{1，9}}
> **输出:** 4，5，7，8
> **解释:**给定位置的聚合数组将为:
> 
> <figure class="table">
> 
> | five | eight | eight | three | five | five | Eleven | Eleven | six |
> | one | Two | three | four | five | six | seven | eight | nine |
> 
> 聚合数组显示每个位置的 ranifall 量。
> 
> 从位置 1 到 5，{ 1，2，3，5 }的降雨量> = 5 厘米，因此答案是 4。
> 从位置 5 到 9，{ 5，6，7，8，9 }有降雨> = 5 厘米，因此答案为 5。
> 从位置 2 到 9，{ 2，3，5，6，7，8，9 }有降雨> = 5 厘米，因此答案是 7。
> 从位置 1 到 9，{ 1，2，3，5，6，7，8，9 }有降雨> = 5 厘米，因此答案是 9。
> 
> **输入:** arr[][] = {{2，4，1 }，{3，9，3}}，K = 5，查询[][] = {{2，5}，{4，6 } }
> T3】输出: 3，3
> 
> </figure>

**天真的做法:** [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】【】**找到位置的最大值。创建一个大小等于找到的最大位置的数组。然后，对于每个降雨范围，更新数组以获得聚合数组。现在，对于每个查询，遍历形成的数组，计算降雨量大于 **K** cms 的位置数量。

下面是上述方法的代码。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of locatins
// with rainfall  more than K cms
vector<int> count(vector<int> arr,
                  vector<vector<int> > Q,
                  int q, int k)
{
    vector<int> ans;
    for (int i = 0; i < q; i++) {
        int temp = 0;
        for (int j = Q[i][0]; j <= Q[i][1]; j++) {
            if (arr[j] >= k)
                temp++;
        }
        ans.push_back(temp);
    }
    return ans;
}

// Function to find aggregate array
vector<int> aggregateArray(
    vector<vector<int> > arr, int n)
{
    // To store the maximum location
    int m = 0;

    for (int i = 0; i < n; i++)
        m = max(m, arr[i][1]);

    // Array to store the aggregate values
    vector<int> agg(m + 1);
    for (int i = 0; i < n; i++) {
        for (int j = arr[i][0]; j <= arr[i][1]; j++) {
            agg[j] += arr[i][2];
        }
    }
    return agg;
}

// Driver Code
int main()
{
    int N = 4;
    vector<vector<int> > arr = {
        { 1, 3, 5 }, { 2, 8, 3 },
        { 5, 8, 2 }, { 7, 9, 6 }
    };

    // Storing aggregate array
    vector<int> agg = aggregateArray(arr, N);

    int Q = 4;
    vector<vector<int> > queries
        = { { 1, 5 }, { 5, 9 },
            { 2, 9 }, { 1, 9 } };
    int K = 5;
    vector<int> ans = count(agg, queries, Q, K);

    // Printing answer to each query
    for (int i = 0; i < N; i++) {
        cout << ans[i] << endl;
    }
}
```

## 蟒蛇 3

```
# python program for above approach

# Function to find number of locatins
# with rainfall more than K cms
def count(arr, Q, q, k):

    ans = []
    for i in range(0, q):
        temp = 0
        for j in range(Q[i][0], Q[i][1] + 1):
            if (arr[j] >= k):
                temp += 1

        ans.append(temp)

    return ans

# Function to find aggregate array
def aggregateArray(arr, n):

    # To store the maximum location
    m = 0

    for i in range(0, n):
        m = max(m, arr[i][1])

    # Array to store the aggregate values
    agg = [0 for _ in range(m + 1)]
    for i in range(0, n):
        for j in range(arr[i][0], arr[i][1] + 1):
            agg[j] += arr[i][2]

    return agg

# Driver Code
if __name__ == "__main__":

    N = 4
    arr = [
        [1, 3, 5], [2, 8, 3],
        [5, 8, 2], [7, 9, 6]
    ]

    # Storing aggregate array
    agg = aggregateArray(arr, N)

    Q = 4
    queries = [[1, 5], [5, 9],
               [2, 9], [1, 9]]

    K = 5
    ans = count(agg, queries, Q, K)

    # Printing answer to each query
    for i in range(0, N):
        print(ans[i])

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find number of locatins
        // with rainfall  more than K cms
        function count(arr, Q, q, k) {
            let ans = [];
            for (let i = 0; i < q; i++) {
                let temp = 0;
                for (let j = Q[i][0]; j <= Q[i][1]; j++) {
                    if (arr[j] >= k)
                        temp++;
                }
                ans.push(temp);
            }
            return ans;
        }

        // Function to find aggregate array
        function aggregateArray(
            arr, n)
        {

            // To store the maximum location
            let m = 0;

            for (let i = 0; i < n; i++)
                m = Math.max(m, arr[i][1]);

            // Array to store the aggregate values
            let agg = new Array(m + 1).fill(0);
            for (let i = 0; i < n; i++) {
                for (let j = arr[i][0]; j <= arr[i][1]; j++) {
                    agg[j] += arr[i][2];
                }
            }
            return agg;
        }

        // Driver Code
        let N = 4;
        let arr = [
            [1, 3, 5], [2, 8, 3],
            [5, 8, 2], [7, 9, 6]
        ];

        // Storing aggregate array
        let agg = aggregateArray(arr, N);

        let Q = 4;
        let queries
            = [[1, 5], [5, 9],
            [2, 9], [1, 9]];
        let K = 5;
        let ans = count(agg, queries, Q, K);

        // Printing answer to each query
        for (let i = 0; i < N; i++) {
            document.write(ans[i] + "<br>");
        }

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
5
7
8
```

**时间复杂度:** O(最大值(O(N*M)，O(Q*M))。
**辅助空间** : O(M)。
其中 **N** 为输入数， **Q** 为查询数， **M** 为最大位置。

**高效方法:**给定的问题可以通过使用[加权作业调度](https://www.geeksforgeeks.org/weighted-job-scheduling-log-n-time/)方法并使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来解决。这个问题可以分为两部分来解决，形成聚合数组，然后应用前缀和来有效地回答查询。按照以下步骤解决给定的问题。

*   根据结束位置对 **arr[][]** 进行排序。
*   使用[地图数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储起始位置和重叠计数。
*   对于每个终点位置，通过降雨数据+重叠更新聚合数组。
*   在开始位置交叉后，使用散列表减少重叠。
*   对于每个三元组，用开始时间更新哈希表。
*   遍历和填充数组中的重叠部分，直到到达下一个三元组的结束位置。
*   找到聚合数组后，使用前缀 sum 查找每个查询的答案。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Comparator function to sort
// the array in specific order
static bool comp(vector<int> a, vector<int> b)
{
    return (a[1] > b[1]);
}

// Function to find number of locatins
// with rainfall  more than K cms
vector<int> count(vector<int> arr,
                  vector<vector<int> > Q,
                  int q, int k)
{

    // Prefix sum array,
    // of count of locations having
    // rainfall greater than k cms
    int n = arr.size();
    vector<int> arrPre(n);

    if (arr[0] >= k)
        arrPre[0] = 1;
    else
        arrPre[0] = 0;

    for (int i = 1; i < n; i++) {

        if (arr[i] >= k)
            arrPre[i] = arrPre[i - 1] + 1;

        else
            arrPre[i] = arrPre[i - 1];
    }

    // evaluating the queries
    vector<int> ans;
    for (int i = 0; i < q; i++) {
        ans.push_back(
            arrPre[Q[i][1]]
            - arrPre[Q[i][0] - 1]);
    }
    return ans;
}

// Function to find aggregate array
vector<int> aggregateArray(
    vector<vector<int> > N, int n)
{
    // To store the maximum location
    int m = 0;
    for (int i = 0; i < n; i++)
        m = max(m, N[i][1]);

    // Array to store rainfall
    // of m locations sorting
    // input array based on end time,
    // in descending order
    vector<int> arr(m + 1);
    sort(N.begin(), N.end(), comp);

    // To store start locn and
    // rainfall corresponding to it
    unordered_map<int, int> start;
    int overlap = 0;

    for (int i = 0; i < n; i++) {
        // If two inputs have same end time,
        // we need to reposition them
        if (m < N[i][1])
            m++;
        else
            // Fill m with overlap,
            // till we reach current end location,
            // and keep checking if we've crossed
            // start time of previously recorded data
            // and decreament overlap(map)
            while (m > 0 && m != N[i][1])
                overlap -= start[m],
                    arr[m--] = overlap;

        // To check if start time is crossed
        // of previously recorded data
        // and decreament overlap(map)
        overlap -= start[m];

        // Input data + previous recorded data
        arr[m] = overlap + N[i][2];

        // updating overlap with current data
        overlap += N[i][2];

        // storing start location with
        // corresponding rainfall data
        start[N[i][0] - 1] = N[i][2];

        // update m
        m--;
    }
    while (m >= N[n - 1][0])

        // fill out the left out indexes
        overlap -= start[m],
            arr[m--] = overlap;
    return arr;
}

// Driver Code
int main()
{
    int N = 4;
    vector<vector<int> > arr = {
        { 1, 3, 5 }, { 2, 8, 3 },
        { 5, 8, 2 }, { 7, 9, 6 }
    };
    vector<int> agg = aggregateArray(arr, N);

    int Q = 4;

    vector<vector<int> > queries
        = { { 1, 5 }, { 5, 9 },
            { 2, 9 }, { 1, 9 } };
    int K = 5;
    vector<int> ans = count(agg, queries, Q, K);

    // Printing answer to each query
    for (int i = 0; i < N; i++) {
        cout << ans[i] << endl;
    }
}
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to find number of locatins
// with rainfall  more than K cms
function count(arr, Q, q, k)
{

    // Prefix sum array,
    // of count of locations having
    // rainfall greater than k cms
    var n = arr.length;
    var arrPre = Array(n).fill(0);

    if (arr[0] >= k)
        arrPre[0] = 1;
    else
        arrPre[0] = 0;

    for (var i = 1; i < n; i++) {

        if (arr[i] >= k)
            arrPre[i] = arrPre[i - 1] + 1;

        else
            arrPre[i] = arrPre[i - 1];
    }

    // evaluating the queries
    var ans = [];
    for (var i = 0; i < q; i++) {
        ans.push(
            arrPre[Q[i][1]]
            - arrPre[Q[i][0] - 1]);
    }
    return ans;
}

// Function to find aggregate array
function aggregateArray(N, n)
{
    // To store the maximum location
    var m = 0;
    for (var i = 0; i < n; i++)
        m = Math.max(m, N[i][1]);

    // Array to store rainfall
    // of m locations sorting
    // input array based on end time,
    // in descending order
    var arr = Array(m + 1).fill(0);
    N.sort((a,b)=>b[1] - a[1]);

    // To store start locn and
    // rainfall corresponding to it
    var start = new Map();
    var overlap = 0;

    for (var i = 0; i < n; i++) {
        // If two inputs have same end time,
        // we need to reposition them
        if (m < N[i][1])
            m++;
        else
        {
            // Fill m with overlap,
            // till we reach current end location,
            // and keep checking if we've crossed
            // start time of previously recorded data
            // and decreament overlap(map)
            while (m > 0 && m != N[i][1])
            {
                overlap -= start.has(m)?start.get(m):0;
                arr[m--] = overlap;
            }
        }

        // To check if start time is crossed
        // of previously recorded data
        // and decreament overlap(map)
        overlap -= start.has(m)?start.get(m):0;

        // Input data + previous recorded data
        arr[m] = overlap + N[i][2];

        // updating overlap with current data
        overlap += N[i][2];

        // storing start location with
        // corresponding rainfall data
        start.set(N[i][0] - 1, N[i][2]);

        // update m
        m--;
    }
    while (m >= N[n - 1][0])
    {
        // fill out the left out indexes
        overlap -=  start.has(m)?start.get(m):0;
        arr[m--] = overlap;
    }

    return arr;
}

// Driver Code
var N = 4;
var arr = [
    [ 1, 3, 5 ], [ 2, 8, 3 ],
    [ 5, 8, 2 ], [ 7, 9, 6 ]
];
var agg = aggregateArray(arr, N);
var Q = 4;
var queries
    = [ [ 1, 5 ], [ 5, 9 ],
        [ 2, 9 ], [ 1, 9 ] ];
var K = 5;
var ans = count(agg, queries, Q, K);
// Printing answer to each query
for(var i = 0; i < N; i++) {
    document.write(ans[i] + "<br>");
}

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
4
5
7
8
```

**时间复杂度:** O(max(NlogN，M))。
**辅助空间:** O(M)。
其中 N 为输入数量，M 为最大位置。
# 尽量减少使用算术运算符将数字 N 转换为 M 所需的步骤

> 原文:[https://www . geeksforgeeks . org/使用算术运算符将数字 n 转换为 m 所需的最小化步骤/](https://www.geeksforgeeks.org/minimize-steps-required-to-convert-number-n-to-m-using-arithmetic-operators/)

给定两个整数 **N** 和 **M** ，任务是找到将数字 **N** 转换为 **M** 所需的最小操作数的顺序，使得在每个操作中 **N** 可以相加 **(N = N + N)** ，减去为**(N = N–N)**，乘以 **(N = N*N)** ，或者除以为【T11 如果无法将 **N** 转换为 **M** 则打印**-1”**。

**示例:**

> **输入:** N = 7，M = 392
> **输出:** 3
> +，*，+
> **说明:**
> 执行如下操作:
> 
> 1.  执行加法将 N 的值修改为7 + 7 = 14。
> 2.  执行乘法会将 N 的值修改为 14*14 = 196。
> 3.  执行加法会将 N 的值修改为 196 + 196 = 392。
> 
> 在上述移动顺序为“+*+”后，可以将 N 的值修改为 m
> 
> **输入:** N = 7，M = 9
> **输出:** -1
> **说明:**没有可能将 N 转换为 M 的操作顺序

**方法:**给定的问题可以使用以下观察结果来解决:

*   当 N = N–N = 0 时，减法运算总是得到 0。同样，除法运算总会得到 1，因为 N = N / N = 1。因此，这些案件很容易处理。
*   对于加法和乘法，可以使用[广度优先搜索遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)来解决该问题，方法是按照操作计数的递增顺序为每个操作序列创建一个状态。

解决给定问题的步骤如下:

*   维护一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)来存储 BFS 状态，其中每个状态包含当前可到达的整数**N’**和一个表示从 **N** 到达**N’**的操作序列的字符串。
*   最初，将表示 **N** 的状态 **{N，" }** 和操作序列作为空添加到队列中。
*   将除法运算的状态 **{1，"/}**也添加到队列中。
*   在[广度优先遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)期间，对于每个状态，添加两个状态，其中第一个状态将代表加法 **(N' + N')** ，第二个状态将代表乘法 **(N' * N')** 。
*   维护一个[无序地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)，以检查在 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)期间当前状态是否已经被访问。
*   如果当前状态的值等于 **M** ，则得到直到 **M** 的操作顺序为结果。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sequence of
// minimum number of operations needed
// to convert N into M using +, -, *, /
string changeNtoM(int N, int M)
{
    // Case where N and M are same
    if (N == M) {
        return " ";
    }

    // Case where M = 0
    if (M == 0) {
        return "-";
    }

    // Stores the BFS states in a queue
    queue<pair<int, string> > q;

    // Stores if current state is visited
    unordered_map<int, bool> visited;

    // Initial State
    q.push({ N, "" }), visited[N] = 1;

    // State where the first operation is /
    q.push({ 1, "/" }), visited[1] = 1;

    // Loop for the BFS traversal
    while (!q.empty()) {
        // Stores the current BFS state
        pair<int, string> cur = q.front();
        q.pop();

        // If the value of current state is
        // equal to M return the stored
        // sequence of operations
        if (cur.first == M) {
            // Return answer
            return cur.second;
        }

        // Adding 1st state representing the
        // addition operation(N' + N')
        if (!visited[cur.first + cur.first]
            && cur.first + cur.first <= M) {

            // Add state into queue and
            // mark the state visited
            q.push({ cur.first + cur.first,
                     cur.second + "+" });
            visited[cur.first + cur.first] = 1;
        }

        // Adding 2nd state representing the
        // multiplication operation(N' * N')
        if (!visited[cur.first * cur.first]
            && cur.first * cur.first <= M) {

            // Add state into queue and
            // mark the state visited
            q.push({ cur.first * cur.first,
                     cur.second + "*" });
            visited[cur.first * cur.first] = 1;
        }
    }

    // No valid sequence of operations exist
    return "-1";
}

// Driver Code
int main()
{
    int N = 7, M = 392;
    string result = changeNtoM(N, M);

    if (result == "-1")
        cout << result << endl;
    else
        cout << result.length() << endl
             << result;

    return 0;
}
```

**Output:** 

```
3
+*+
```

***时间复杂度:**O(min(2<sup>log</sup><sub><sup>2</sup></sub><sup>(M–N)</sup>、M–N))*
***辅助空间:**O((M-N)* log<sub>2</sub>(M–N))*
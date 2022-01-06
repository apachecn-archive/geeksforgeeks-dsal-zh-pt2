# 给定粉刷期限和日期限制时可连续粉刷的最大房屋数

> 原文:[https://www . geeksforgeeks . org/最大-可以连续喷漆的房屋-指定喷漆持续时间和日期限制/](https://www.geeksforgeeks.org/maximum-houses-that-can-be-painted-continuously-when-the-painting-duration-and-date-limit-is-given/)

给定一个由 **N** 对组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】【】】**，使得每对 **{L，R}** 代表在 **L** 日之前的 **R <sup>第</sup>** 日可以粉刷的第 i <sup>个</sup>个房屋，任务是找到可以连续粉刷的房屋的最大数量。
**示例:**

> **输入:** N = 4，paint[ ][ ] = [[1，19]，[2，2]，[4，17]，[1，1]]
> **输出:** 3
> **说明:**最多可以刷三间房子，顺序为{4，3，1}
> 
> **输入:** N = 4，paint[ ][ ] = [[100，210]，[200，1310]，[1000，1275]，[2500，3000]]
> **输出:** 3

**方法:**使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。想法是从当前最后一天所需的最低天数中进行选择。按照以下步骤进行操作。

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **V、**来存储所有可以取的对。
*   [使用比较器**对将向量**](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)T2【V】T3 排序。第二个小于**对。第一个**
*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) **pq** 并推送第一对[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **V.**
*   初始化一个变量，比如说 **t** ，来存储时间。
*   遍历[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)、 **V** ，将当前对放入[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) **pq** :
    *   如果 **t +天要求**小于或等于**最后一天**，则**继续**。
    *   否则，从[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)弹出，存储在**温度**变量中，并更新 **t** 等于**t–温度优先**
*   最后，返回[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)的**大小**。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

typedef vector<vector<int> > Matrix;

// Comparator for sorting
static bool cmp(pair<int, int> a, pair<int, int> b)
{
    return a.second < b.second;
}

// Function to count number of houses
// that can be painted
void countMaxPinted(int n, Matrix& paint)
{

    // Vector to store the pairs
    vector<pair<int, int> > V;
    for (int i = 0; i < n; i++) {

        // If house can be painted
        if (paint[i][0] <= paint[i][1]) {
            V.push_back(make_pair(paint[i][0], paint[i][1]));
        }
    }

    // Sort the vector
    sort(V.begin(), V.end(), cmp);

    // If vector is empty
    if (V.size() == 0) {
        cout << 0 << endl;
        return;
    }

    // Initialize t
    int t = V[0].first;

    // Initialize priority queue
    priority_queue<pair<int, int> > pq;
    pq.push(V[0]);

    // Traversing the vector
    for (int i = 1; i < V.size(); i++) {
        t += V[i].first;

        // Pushing in Vectors
        pq.push(V[i]);
        if (t <= V[i].second) {
            continue;
        }
        else {

            // Pop the top element
            auto temp = pq.top();
            pq.pop();
            t = t - temp.first;
        }
    }

    // Print the ans
    cout << pq.size() << endl;
}

// Driver Code
int main()
{

    // Given Input
    int n = 4;
    Matrix paint = { { 1, 19 }, { 2, 2 }, { 4, 17 }, { 1, 1 } };

    // Function Call
    countMaxPinted(n, paint);
}
```

**Output**

```
3
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*
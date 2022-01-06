# 最多选择 K 个项目所需的最大资金量

> 原文:[https://www . geeksforgeeks . org/最多选择 k 个项目所需的最大资本金额/](https://www.geeksforgeeks.org/maximum-amount-of-capital-required-for-selecting-at-most-k-projects/)

给定一个整数 **N** ，代表项目数，两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**P【】**和**C【】**，由 **N** 个整数组成，两个整数 **W** 和 **K** 其中， **W** 为初始资本金额，**P【I】**和**C【I】**为需要选择的利润和资本任务是计算最多选择**K 个项目**所需要的最大资金量，使得所选项目的利润加到 **W** 上，选择至少需要**C【I】**的任意项目。

**示例:**

> **输入:** N = 3，W = 0，K = 2，P[] = {1，2，3}，C[] = {0，1，1}
> **输出:** 4
> **说明:**
> **项目 1:** 在给定 W 为 0 的情况下，第 0<sup>项目可以 C[0]即 0 的成本进行选择，完成资本加 W 即 W 后
> **项目 2:** 在给定 W 为 1 的情况下，可以 C[2]即 1 的成本选择 2 <sup>nd</sup> 项目，完成加到 W 的资本后即 W 变成 W + P[2] = 1 + 3 = 4。</sup>
> 
> **输入:** N = 3，W = 1，K = 1，P[] = {10000，2000，3000}，C[] = {1，1，1 }
> T3】输出: 10001

**方法:**给定的问题可以使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)和[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)来解决。按照以下步骤解决问题:

*   初始化一个 [priority_queue](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) **PQ** 来存储所有项目的利润，其资金最多为**W**。
*   [使用变量 **i** 作为索引遍历数组 **C[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，并将对 **{C[i]，i}** 推送到对 **V** 的[向量中。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   [相对于第一个元素](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)以 [的升序排列向量 V。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   迭代直到 **K** 大于 **0** :
    *   推送优先队列 **PQ** 中所有尚未选定且资金最多为**W**的项目的利润。
    *   用**PQ**T5[最大元素增加 **W** ，即 **W += PQ.top()** 然后](https://www.geeksforgeeks.org/k-th-greatest-element-in-a-max-heap/)[弹出 **PQ**](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) 的顶元素。
    *   将 **K** 减 **1** 。
*   完成上述步骤后，打印 **W** 的值作为获得的最大资本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum capital
// obtained after choosing at most K
// projects whose capital is less than
// the given cost of projects
int maximizedCapital(int K, int W,
                     vector<int>& profits,
                     vector<int>& capital)
{
    // Stores all projects with
    // capital at most W
    priority_queue<int> pq;

    // Stores the pair of {C[i], i}
    vector<pair<int, int> > v;

    // Traverse the vector C[]
    for (int i = 0;
         i < capital.size(); i++) {
        v.push_back({ capital[i], i });
    }

    // Sort the vector v
    sort(v.begin(), v.end());

    int j = 0;

    while (K) {

        // If capital is at most W
        while (j < (int)capital.size()
               && v[j].first <= W) {

            // Push the profit into
            // priority queue
            pq.push(profits[v[j].second]);

            // Increment j by one
            j++;
        }

        // If pq is not empty
        if (!pq.empty()) {

            // Update the capital W
            W = W + pq.top();

            // Delete the top of pq
            pq.pop();
        }

        // Decrement K by one
        K--;
    }

    // Return the maximum capital
    return W;
}

// Driver Code
int main()
{
    int K = 2;
    int W = 0;
    vector<int> P = { 1, 2, 3 };
    vector<int> C = { 0, 1, 1 };
    cout << maximizedCapital(K, W, P, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to calculate maximum capital
    // obtained after choosing at most K
    // projects whose capital is less than
    // the given cost of projects
    static int maximizedCapital(int K, int W, int profits[],
                                int capital[])
    {
        // Stores all projects with
        // capital at most W
        PriorityQueue<Integer> pq = new PriorityQueue<>(
            Collections.reverseOrder());

        // Stores the pair of {C[i], i}
        ArrayList<int[]> v = new ArrayList<>();

        // Traverse the vector C[]
        for (int i = 0; i < capital.length; i++) {
            v.add(new int[] { capital[i], i });
        }

        // Sort the vector v
        Collections.sort(v, (a, b) -> {
            if (a[0] != b[0])
                return a[0] - b[0];
            return a[1] - b[1];
        });

        int j = 0;

        while (K != 0) {

            // If capital is at most W
            while (j < capital.length && v.get(j)[0] <= W) {

                // Add the profit into
                // priority queue
                pq.add(profits[v.get(j)[1]]);

                // Increment j by one
                j++;
            }

            // If pq is not empty
            if (!pq.isEmpty()) {

                // Update the capital W
                W = W + pq.peek();

                // Delete the top of pq
                pq.poll();
            }

            // Decrement K by one
            K--;
        }

        // Return the maximum capital
        return W;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int K = 2;
        int W = 0;
        int P[] = { 1, 2, 3 };
        int C[] = { 0, 1, 1 };

        System.out.println(maximizedCapital(K, W, P, C));
    }
}

// This code is contributed by Kingash.
```

**Output:** 

```
4
```

***时间复杂度:**O(N * K * log N)*
T5**辅助空间:** O(N)
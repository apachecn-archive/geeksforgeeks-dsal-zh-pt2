# 区间列表中最多两个不重叠区间的最大和|区间调度问题

> 原文:[https://www . geesforgeks . org/最多两个非重叠间隔列表中的间隔的最大和-间隔-调度-问题/](https://www.geeksforgeeks.org/maximum-sum-of-at-most-two-non-overlapping-intervals-in-a-list-of-intervals-interval-scheduling-problem/)

给定长度为 **N** 的数组**间隔**，其中每个元素代表三个值，即**{开始时间，结束时间，值}** 。任务是找出最多两个不重叠区间的最大值和。

**示例:**

> **输入:**间隔[] = [[1，3，2]，[4，5，2]，[2，4，3]]
> **输出:** 4
> **解释:**选择间隔 1 和 2(因为第三个间隔重叠)。因此，最大值为 2 + 2 = 4。
> 
> **输入:**间隔[] = [[1，3，2]，[4，5，2]，[1，5，5]]
> **输出:** 5
> **说明:**由于间隔 1 和 2 不重叠，但它们的值将为 2 + 2 = 4。因此，可以选择值为 5 的 3，而不是 1 和 2。

**进场:**这个问题可以借助一个[优先](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)队列解决。要解决此问题，请遵循以下步骤:

1.  排序给定的数组**间隔** w.r.t. **开始时间。**如果两个间隔的**开始时间**相同，则根据**结束时间**进行排序。
2.  将一对 **{endTime，value}** 存储在优先级队列中，并根据 **endTime** 进行排序。
3.  遍历给定数组，计算**结束时间**小于当前间隔的**开始时间**的所有事件的最大值，并将其存储在变量 **max 中。**
4.  现在，更新 ans，每次遍历后为**，ans= Math.max(ans，max +区间[i][2])** 。
5.  回答 ans 作为这个问题的最终答案。

下面是上述方法的实现

## C++

```
// C++ algorithm for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find
// maximum value of atmost two
// non-overlapping intervals
int maxTwoNonOverLapping(vector<vector<int> >& interval)
{

    // Sorting the given array
    // on the basis of startTime
    sort(interval.begin(), interval.end(),
         [](vector<int>& a, vector<int>& b) {
             return (a[0] == b[0]) ? a[1] < b[1]
                                   : a[0] < b[0];
         });

    // Initializing Priority Queue
    // which stores endTime
    // and value and sort
    // on the basis of endTime
    priority_queue<vector<int> > pq;

    // Initializing max
    // and ans variables
    int ma = 0;
    int ans = 0;

    // Traversing the given array
    for (auto e : interval) {
        while (!pq.empty()) {

            // If endTime from priority
            // queue is greater
            // than startTime of
            // traversing interval
            // then break the loop
            if (pq.top()[0] >= e[0])
                break;
            vector<int> qu = pq.top();
            pq.pop();

            // Updating max variable
            ma = max(ma, qu[1]);
        }

        // Updqating ans variable
        ans = max(ans, ma + e[2]);
        pq.push({ e[1], e[2] });
    }

    // Returning ans
    return ans;
}

// Driver Code
int main()
{
    vector<vector<int> > interval
        = { { 1, 3, 2 }, { 4, 5, 2 }, { 1, 5, 5 } };
    int maxValue = maxTwoNonOverLapping(interval);
    cout << maxValue;

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java algorithm for above approach

import java.util.*;

class GFG {

    // Driver Code
    public static void main(String[] args)
    {
        int[][] interval
            = { { 1, 3, 2 }, { 4, 5, 2 }, { 1, 5, 5 } };
        int maxValue = maxTwoNonOverLapping(interval);
        System.out.println(maxValue);
    }

    // Function to find
    // maximum value of atmost two
    // non-overlapping intervals
    public static int maxTwoNonOverLapping(int[][] interval)
    {
        // Sorting the given array
        // on the basis of startTime
        Arrays.sort(interval,
                    (a, b)
                        -> (a[0] == b[0]) ? a[1] - b[1]
                                          : a[0] - b[0]);

        // Initializing Priority Queue
        // which stores endTime
        // and value and sort
        // on the basis of endTime
        PriorityQueue<int[]> pq
            = new PriorityQueue<>((a, b) -> a[0] - b[0]);

        // Initializing max
        // and ans variables
        int max = 0;
        int ans = 0;

        // Traversing the given array
        for (int[] e : interval) {
            while (!pq.isEmpty()) {

                // If endTime from priority
                // queue is greater
                // than startTime of
                // traversing interval
                // then break the loop
                if (pq.peek()[0] >= e[0])
                    break;
                int[] qu = pq.remove();

                // Updating max variable
                max = Math.max(max, qu[1]);
            }

            // Updqating ans variable
            ans = Math.max(ans, max + e[2]);
            pq.add(new int[] { e[1], e[2] });
        }

        // Returning ans
        return ans;
    }
}
```

**Output**

```
5
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(N)
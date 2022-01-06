# 编码竞赛的最大可能评分

> 原文:[https://www . geeksforgeeks . org/编码竞赛的最大可能评分/](https://www.geeksforgeeks.org/maximum-possible-rating-of-a-coding-contest/)

给定两个大小为 **N** 的正整数**点[]** 、**上投票[]** 和一个值 **K** (1 < = K < = N)。任务是选择至少 K 个元素(问题)，使得编码竞赛的评分最大。

**竞赛评分:**竞赛评分定义为竞赛中所有问题的总积分乘以竞赛中所有问题的最小上票数

> 因此，**评分** =竞赛题的分数总和*竞赛题中的最小上票数。

**示例:**

> **输入:**点[] = {2，10，3，1，5，8}，上投票[] = {5，4，3，9，7，2}，K = 2
> **输出:** 60
> **说明:**
> 这里我们选择第 2 题和第 5 题来获得本次大赛的最高评分。
> 因此最大额定值为(10 + 5) *最小值(4，7) = 60
> 
> **输入:**点[] = {2，10，3，1，5，8}，上投票[] = {5，4，3，9，7，2}，K = 3
> **输出:** 68
> **说明:**
> 这里我们选择第 1、2、5 题，得到本次大赛的最高评分。
> 因此最大额定值为(2 + 10 + 5) *最小值(5，4，7) = 68
> 
> **输入:**点[] = {2，20，3，1，5，8}，上投票[] = {5，10，3，9，7，2}，K = 4
> **输出:** 200
> **说明:**
> 这里我们只选择第 2 题来获得本次大赛的最高评分。
> 进一步选择任何问题都会降低评级。
> 所以最大额定值为 20 * 10 = 200

**进场:**

*   尝试从最高到最低的每一个 upvote 的值，同时保持一个尽可能大的点数组，不断地在总点数上加点数，如果竞赛中的问题数超过 K，就裁掉最低点数的问题。这包括三个步骤。
    1.  按照问题的上升票值降序排列问题。
    2.  对于指数 i = 0，1，…，K-1，我们将点数推入 min_heap 并计算评级。我们只需要记录最高等级。我们使用 min_heap 来跟踪具有最小点的问题。
    3.  对于索引 i = K，K+1，…，N-1，如果当前问题的点大于 min_heap 的顶部，我们弹出现有的元素，并将当前元素推送到 min_heap 中，并更新最大评级。
        以这种方式，计算关于具有第 I 大向上票数的问题的最大评级，因为我们在 min_heap 中具有 K 个最大点的问题。

下面是上述方法的实现。

## C++

```
// C++ program to find the Maximum 
// Possible Rating of a Coding Contest
#include <bits/stdc++.h>
using namespace std;

// Function to sort all problems
// descending to upvotes
bool Comparator(pair<int, int> p1,
                pair<int, int> p2)
{
    return p1.second > p2.second;
}

// Function to return maximum
// rating
int FindMaxRating(int N, int Point[],
                  int Upvote[], int K)
{
    // Declaring vector of pairs
    vector<pair<int, int> > vec;

    // Each pair represents a problem
    // with its points and upvotes
    for (int i = 0; i < N; i++)
    {
        vec.push_back(make_pair(Point[i],
                                Upvote[i]));
    }

    // Step (1) - Sort problems by their 
    // upvotes value in decreasing order
    sort(vec.begin(), vec.end(), Comparator);

    // Declaring min_heap or priority queue 
    // to track of the problem with 
    // minimum points.
    priority_queue<int, vector<int>,
                  greater<int> > pq;

    int total_points = 0, max_rating = 0;

    // Step (2) - Loop for i = 0 to K - 1 and 
    // do accordingly
    for (int i = 0; i < K; i++)
    {
        total_points = total_points
                      + vec[i].first;
        max_rating = max(max_rating, 
                         total_points 
                         * vec[i].second);
        pq.push(vec[i].first);
    }

    // Step (3) - Loop for i = K to N - 1 
    // and do accordingly
    for (int i = K; i < N; i++)
    {
        if (pq.top() < vec[i].first)
        {
            total_points = total_points
                           - pq.top() 
                           + vec[i].first;
            max_rating = max(max_rating, 
                             total_points
                             * vec[i].second);

            pq.pop();

            pq.push(vec[i].first);
        }
    }

    return max_rating;
}

// Driver code
int main()
{
    int Point[] = { 2, 10, 3, 1, 5, 8 };
    int Upvote[] = { 5, 4, 3, 9, 7, 2 };

    int N = sizeof(Point) / sizeof(Point[0]);
    int K = 2;

    cout << "Maximum Rating of Coding Contest is: "
         << FindMaxRating(N, Point, Upvote, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find the Maximum 
# Possible Rating of a Coding Contest 
import heapq

# Function to sort all problems 
# descending to upvotes
def Comparator(p1):

    return p1[1]

# Function to return maximum 
# rating 
def FindMaxRating(N, Point, Upvote, K):

    # Declaring vector of pairs
    vec = []

    # Each pair represents a problem 
    # with its points and upvotes 
    for i in range(N):
        vec.append([Point[i], Upvote[i]])

    # Step (1) - Sort problems by their 
    # upvotes value in decreasing order 
    vec.sort(reverse = True, key = Comparator)

    # Declaring min_heap or priority queue 
    # to track of the problem with 
    # minimum points. 
    pq = []
    heapq.heapify(pq)

    total_points, max_rating = 0, 0

    # Step (2) - Loop for i = 0 to K - 1 and 
    # do accordingly 
    for i in range(K):
        total_points = (total_points + 
                        vec[i][0])

        max_rating = max(max_rating,
                         total_points * 
                         vec[i][1])

        heapq.heappush(pq, vec[i][0])

    # Step (3) - Loop for i = K to N - 1 
    # and do accordingly 
    for i in range(K, N):
        if pq[0] < vec[i][0]:
            total_points = (total_points - 
                                   pq[0] + 
                               vec[i][0])

            max_rating = max(max_rating, 
                             total_points * 
                             vec[i][1])

            heapq.heappop(pq)
            heapq.heappush(pq, vec[i][0])

    return max_rating

# Driver code
Point = [ 2, 10, 3, 1, 5, 8 ]
Upvote = [ 5, 4, 3, 9, 7, 2 ]

N = len(Point)
K = 2

print("Maximum Rating of Coding Contest is:",
       FindMaxRating(N, Point, Upvote, K))

# This code is contributed by stutipathak31jan
```

**Output:**

```
Maximum Rating of Coding Contest is: 60

```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(N)
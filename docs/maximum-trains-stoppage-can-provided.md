# 可提供停运的最大列车数

> 原文:[https://www . geesforgeks . org/maximum-trains-stop-can-provided/](https://www.geeksforgeeks.org/maximum-trains-stoppage-can-provided/)

我们有两个方向的 n 站台和两条主要的铁路轨道。需要在你的车站停车的列车必须占用一个站台停车，不需要在你的车站停车的列车将会不停车地通过任一主轨道逃跑。现在，每列火车都有三个值第一个到达时间、第二个离开时间和第三个所需站台号。我们接到通知说，在这种列车上，你必须告知你能在你的车站停车的最大列车数。

示例:

```
Input : n = 3, m = 6 
Train no.|  Arrival Time |Dept. Time | Platform No.
    1    |   10:00       |  10:30    |    1
    2    |   10:10       |  10:30    |    1
    3    |   10:00       |  10:20    |    2
    4    |   10:30       |  12:30    |    2
    5    |   12:00       |  12:30    |    3
    6    |   09:00       |  10:05    |    1
Output : Maximum Stopped Trains = 5
Explanation : If train no. 1 will left 
to go without stoppage then 2 and 6 can 
easily be accommodated on platform 1\. 
And 3 and 4 on platform 2 and 5 on platform 3.

Input : n = 1, m = 3
Train no.|Arrival Time|Dept. Time | Platform No.
    1    | 10:00      |  10:30    |    1
    2    | 11:10      |  11:30    |    1
    3    | 12:00      |  12:20    |    1

Output : Maximum Stopped Trains = 3
Explanation : All three trains can be easily
stopped at platform 1.

```

如果我们只从一个站台开始，那么我们只有一个站台和一些列车，它们的到达时间和离开时间，我们必须最大化该站台上的列车数量。这个任务类似于[活动选择问题。](https://en.wikipedia.org/wiki/Activity_selection_problem)因此，对于 n 个站台，我们将简单地制作 n 个向量，并根据站台号将相应的列车放入这些向量中。之后，通过应用贪婪方法，我们很容易解决这个问题。
注意:我们将采用 4 位整数的形式输入到达和离开时间，因为 1030 将代表 10:30，这样我们可以轻松处理数据类型。
同样，我们将选择二维数组作为 arr[m][3]输入，其中 arr[i][0]表示到达时间，arr[i][1]表示出发时间，arr[i][2]表示第七趟列车的站台。

```
// CPP to design platform for maximum stoppage
#include <bits/stdc++.h>
using namespace std;

// number of platforms and trains
#define n 2
#define m 5

// function to calculate maximum trains stoppage
int maxStop(int arr[][3])
{
    // declaring vector of pairs for platform
    vector<pair<int, int> > vect[n + 1];

    // Entering values in vector of pairs
    // as per platform number
    // make departure time first element 
    // of pair
    for (int i = 0; i < m; i++)
        vect[arr[i][2]].push_back(
             make_pair(arr[i][1], arr[i][0]));

    // sort trains for each platform as per
    // dept. time
    for (int i = 0; i <= n; i++)
        sort(vect[i].begin(), vect[i].end());

    // perform activity selection approach
    int count = 0;
    for (int i = 0; i <= n; i++) {
        if (vect[i].size() == 0)
            continue;

        // first train for each platform will
        // also be selected
        int x = 0;
        count++;
        for (int j = 1; j < vect[i].size(); j++) {
            if (vect[i][j].second >=
                             vect[i][x].first) {
                x = j;
                count++;
            }
        }
    }
    return count;
}

// driver function
int main()
{
    int arr[m][3] = { 1000, 1030, 1,
                      1010, 1020, 1,
                      1025, 1040, 1,
                      1130, 1145, 2,
                      1130, 1140, 2 };
    cout << "Maximum Stopped Trains = "
         << maxStop(arr);
    return 0;
}
```

输出:

```
Maximum Stopped Trains = 3

```
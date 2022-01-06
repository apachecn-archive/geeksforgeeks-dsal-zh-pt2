# 从给定的一组 N 个点中平行于坐标轴的方块数

> 原文:[https://www . geesforgeks . org/从给定的 n 点集合计算平行于坐标轴的方块数/](https://www.geeksforgeeks.org/count-of-squares-that-are-parallel-to-the-coordinate-axis-from-the-given-set-of-n-points/)

给定笛卡尔坐标系中的点阵列**点[]** ，任务是找出平行于坐标轴的正方形的数量。

**示例:**

> **输入:**点[] = {(0，0)、(0，2)、(2，0)、(2)、(1，1)}
> **输出:** 1
> **说明:**
> 由于点(0，0)、(0，2)、(2，0)、(2，2)形成平行于 X 轴和 Y 轴的正方形，因此这种正方形的计数为 1。
> 
> **输入:**点[] = {(2，0)，(0，2)，(2，2)，(0，0)，(-2，2)，(-2，0)}
> **输出:** 2
> **说明:**
> 由于点(0，0)，(0，2)，(2，0)，(2，2)形成一个正方形，而点(0，0)，(0，2)，(-2，0)，(-2，2)形成平行于 X 轴和 Y 轴的其他正方形

**逼近:**思路是从点的数组中选择两个点，使这两个点平行于坐标轴，然后借助点与点之间的距离找到正方形的其他两个点。如果这些点存在于数组中，那么就有一个这样的正方形。

下面是上述方法的实现:

## C++

```
// C++ implementation to find count of Squares
// that are parallel to the coordinate axis
// from the given set of N points

#include <bits/stdc++.h>
using namespace std;

#define sz(x) int(x.size())

// Function to get distance
// between two points
int get_dis(pair<int, int> p1,
            pair<int, int> p2)
{
    int a = abs(p1.first - p2.first);
    int b = abs(p1.second - p2.second);
    return ((a * a) + (b * b));
}

// Function to check that points
// forms a square and parallel to
// the co-ordinate axis
bool check(pair<int, int> p1,
           pair<int, int> p2,
           pair<int, int> p3,
           pair<int, int> p4)
{

    int d2 = get_dis(p1, p2);
    int d3 = get_dis(p1, p3);
    int d4 = get_dis(p1, p4);
    if (d2 == d3
        && 2 * d2 == d4
        && 2 * get_dis(p2, p4) == get_dis(p2, p3)) {
        return true;
    }
    if (d3 == d4
        && 2 * d3 == d2
        && 2 * get_dis(p3, p2) == get_dis(p3, p4)) {
        return true;
    }
    if (d2 == d4
        && 2 * d2 == d3
        && 2 * get_dis(p2, p3) == get_dis(p2, p4)) {
        return true;
    }
    return false;
}

// Function to find all the squares which is
// parallel to co-ordinate axis
int count(map<pair<int, int>, int> hash,
          vector<pair<int, int> > v, int n)
{
    int ans = 0;
    map<pair<int, int>, int> vis;

    // Loop to choose two points
    // from the array of points
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i == j)
                continue;
            pair<int, int> p1
                = make_pair(v[i].first,
                            v[j].second);
            pair<int, int> p2
                = make_pair(v[j].first,
                            v[i].second);
            set<pair<int, int> > s;
            s.insert(v[i]);
            s.insert(v[j]);
            s.insert(p1);
            s.insert(p2);
            if (sz(s) != 4)
                continue;

            // Condition to check if the
            // other points are present in the map
            if (hash.find(p1) != hash.end()
                && hash.find(p2) != hash.end()) {
                if ((!vis[v[i]] || !vis[v[j]]
                     || !vis[p1] || !vis[p2])
                    && (check(v[i], v[j], p1, p2))) {

                    vis[v[i]] = 1;
                    vis[v[j]] = 1;
                    vis[p1] = 1;
                    vis[p2] = 1;
                    ans++;
                }
            }
        }
    }
    cout << ans;
    return ans;
}

// Function to Count the number of squares
void countOfSquares(vector<pair<int, int> > v, int n)
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);

    map<pair<int, int>, int> hash;

    // Declaring iterator to a vector
    vector<pair<int, int> >::iterator ptr;

    // Adding the points to hash
    for (ptr = v.begin(); ptr < v.end(); ptr++)
        hash[*ptr] = 1;

    // Count the number of squares
    count(hash, v, n);
}

// Driver Code
int main()
{

    int n = 5;
    vector<pair<int, int> > v;
    v.push_back(make_pair(0, 0));
    v.push_back(make_pair(0, 2));
    v.push_back(make_pair(2, 0));
    v.push_back(make_pair(2, 2));
    v.push_back(make_pair(0, 1));

    // Function call
    countOfSquares(v, n);
    return 0;
}
```

**Output:**

```
1

```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，有两个循环需要 O(N <sup>2</sup> )时间，因此时间复杂度为 **O(N <sup>2</sup> )** 。
*   **辅助空间复杂度:**和上面的方法一样，使用了额外的空间，因此辅助空间复杂度为 **O(N)** 。
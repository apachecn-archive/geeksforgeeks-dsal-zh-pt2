# 从给定的数组中找出所有相交的对

> 原文:[https://www . geeksforgeeks . org/从给定数组中查找所有相交对/](https://www.geeksforgeeks.org/find-all-the-intersecting-pairs-from-a-given-array/)

给定 n 对(S[i]，F[i])，其中对于每个 I，S[i]< F[i]。当且仅当两个范围中的任何一个不完全位于另一个范围内时，即一对范围中只有一个点位于另一对范围的起点和终点之间，则称这两个范围相交。我们必须打印每对的所有相交范围。

***注:**F[I]的所有端点都是整数，也是唯一的。没有一对同时开始和结束。此外，没有一对的端点与另一对的起点相同。*

**示例:**

> **输入:**
> n = 6，v = {{9，12}，{2，11}，{1，3}，{6，10}，{5，7}，{4，8}}
> **输出:**
> {9，12}与:{6，10} {2，11}
> {2，11}与:{1，3} {9，12}
> {1，3}与:{ 2 }相交 8}与:{6，10}
> **相交解释:**
> 第一对(9，12)与第二对(2，11)和第四对(6，10)相交。
> 第二对(2，11)与第三对(1，3)和第一对(9，12)相交。
> 第三对(1，3)与第二对(2，11)相交。
> 第四对(6，10)与第五对(5，7)、第六对(4，8)和第一对(9，12)相交。
> 第五对(5，7)与第四对(6，10)相交。
> 第六对(4，8)与第四对(6，10)相交。
> 
> **输入:** n = 5，v = {1，3}、{2，4}、{5，9}、{6，8}、{7，10}}
> **输出:**
> {1，3}与:{2，4}
> {2，4}与:{1，3}
> {5，9}与:{7，10}
> {6，8}与:{7，10 }
> { 0 }相交
> 第二对(2，4)与第一对(1，3)相交。
> 第三对(5，9)与第五对(7，10)相交。
> 第四对(6，8)与第五对(7，10)相交。
> 第五对(7，10)与第三对(5，9)和第四对(6，8)相交。

**进场:**

上述问题可以通过使用排序来解决。首先，我们必须将该对中的第一个元素和第二个元素连同它们的位置一起插入一个向量中。然后根据第一个元素对所有元素进行排序。之后，使用**为该对中的第二个元素设置数据结构**。然后我们必须在向量中迭代，在向量中我们已经存储了第一个和第二个元素以及它们各自的位置，如果找到了第一个元素，那么计算与集合中的当前对相交的所有范围，如果遇到了对中的第二个元素，那么简单地从集合中删除第二个对。否则，添加当前对的第二个元素。

下面是上述方法的实现:

```
// CPP Program to Find all the
// intersecting pairs from a given array

#include <bits/stdc++.h>
using namespace std;

// Function that print intersecting pairs
// for each pair in the vector
void findIntersection(vector<pair<int, int> > v, int n)
{
    vector<pair<int, int> > data;

    vector<vector<int> > answer(n);

    // Store each pair with their positions
    for (int i = 0; i < n; i++) {
        data.push_back(make_pair(v[i].first, i));

        data.push_back(make_pair(v[i].second, i));
    }

    // Sort the vector with respect to
    // first element in the pair
    sort(data.begin(), data.end());

    int curr = 0;

    // set data structure for keeping
    // the second element of each pair
    set<pair<int, int> > s;

    // Iterating data vector
    for (auto it : data) {

        // check if all pairs are taken
        if (curr >= n)
            break;

        // check if current value is a second element
        // then remove it from the set
        if (s.count(it))

            s.erase(it);

        else {

            // index of the current pair
            int i = it.second;

            // Computing the second element of current pair
            int j = v[i].second;

            // Iterating in the set
            for (auto k : s) {

                // Check if the set element
                // has higher value than the current
                // element's second element
                if (k.first > j)
                    break;

                int index = k.second;

                answer[i].push_back(index);

                answer[index].push_back(i);

                curr++;

                // Check if curr is equal to
                // all available pairs or not
                if (curr >= n)
                    break;
            }

            // Insert second element
            // of current pair in the set
            s.insert(make_pair(j, i));
        }
    }

    // Printing the result
    for (int i = 0; i < n; i++) {

        cout << "{" << v[i].first << ", " << v[i].second << "}"
             << " is intersecting with: ";

        for (int j = 0; j < answer[i].size(); j++)

            cout << "{" << v[answer[i][j]].first << ", "
                 << v[answer[i][j]].second << "}"
                 << " ";

        cout << "\n";
    }
}

// Driver Code
int main()
{

    // initialise the size of vector
    int n = 6;

    // initialise the vector
    vector<pair<int, int> > v = { { 9, 12 },
                                  { 2, 11 },
                                  { 1, 3 },
                                  { 6, 10 },
                                  { 5, 7 },
                                  { 4, 8 } };

    findIntersection(v, n);

    return 0;
}
```

**Output:**

```
{9, 12} is intersecting with: {6, 10} {2, 11} 
{2, 11} is intersecting with: {1, 3} {9, 12} 
{1, 3} is intersecting with: {2, 11} 
{6, 10} is intersecting with: {5, 7} {4, 8} {9, 12} 
{5, 7} is intersecting with: {6, 10} 
{4, 8} is intersecting with: {6, 10}

```
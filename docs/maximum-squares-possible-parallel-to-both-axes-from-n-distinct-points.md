# 从 N 个不同点平行于两个轴的最大可能平方

> 原文:[https://www . geeksforgeeks . org/最大平方-可能-平行于两个轴-从-n-distinct-points/](https://www.geeksforgeeks.org/maximum-squares-possible-parallel-to-both-axes-from-n-distinct-points/)

给定二维平面中 **N** 个不同点的 **X <sub>i</sub>** 和 **Y <sub>i</sub>** 坐标，任务是计算从这些平行于 **X** 和 **Y** 轴的点可以形成的正方形数量。
**举例:**

> **输入:** X[] = { 0，2，0，2 }，Y[] = { 0，2，2，0 }
> **输出:** 1
> **解释:**使用这些点只能形成一个正方形–
> (0，2)(2，2)
> (0，0)(2，0)
> **输入:** X[] = { 3，2，0，6 }，Y[] = { 0，2，0，0

**天真方法:**迭代四个点的所有可能组合，检查是否可以形成平行于 X 轴和 Y 轴的正方形。这种方法的时间复杂度是 **O(N <sup>4</sup> )** 。
**有效方法:**我们可以观察到，对于任何四个点来制作所需的正方形，以下条件必须成立–

*   位于同一水平线的点必须具有相同的 **Y** 坐标。

*   位于同一垂直线上的点必须具有相同的 **X** 坐标。

*   这些点之间的距离应该相同。

这样任何正方形的四个点都可以写成顺时针方向的 **P1(X <sub>1</sub> 、Y <sub>1</sub> 、P2(X <sub>2</sub> 、Y <sub>1</sub> )、P3(X <sub>2</sub> 、Y <sub>2</sub> )** 、P4(X <sub>1</sub> 、Y <sub>2</sub> ) 。
从给定的点考虑同一水平或垂直线上的任意两点。计算它们之间的距离。在此基础上，形成另外两点。现在检查两个给定点是否都存在。如果是这样的话，它保证了一个正方形的存在。因此，增加计数并继续进行。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the count of
// squares parallel to both X and Y-axis
// from a given set of points
int countSquares(int* X, int* Y, int N)
{
    // Initialize result
    int count = 0;

    // Initialize a set to store points
    set<pair<int, int> > points;

    // Initialize a map to store the
    // points in the same vertical line
    map<int, vector<int> > vertical;

    // Store the points in a set
    for (int i = 0; i < N; i++) {
        points.insert({ X[i], Y[i] });
    }

    // Store the points in the same vertical line
    // i.e. with same X co-ordinates
    for (int i = 0; i < N; i++) {
        vertical[X[i]].push_back(Y[i]);
    }

    // Check for every two points
    // in the same vertical line
    for (auto line : vertical) {
        int X1 = line.first;
        vector<int> yList = line.second;

        for (int i = 0; i < yList.size(); i++) {
            int Y1 = yList[i];
            for (int j = i + 1; j < yList.size(); j++) {
                int Y2 = yList[j];
                int side = abs(Y1 - Y2);
                int X2 = X1 + side;

                // Check if other two point are present or not
                if (points.find({ X2, Y1 }) != points.end()
                and points.find({ X2, Y2 }) != points.end())
                    count++;
            }
        }
    }

    return count;
}

// Driver Code
int main()
{
    int X[] = { 0, 2, 0, 2 }, Y[] = { 0, 2, 2, 0 };

    int N = sizeof(X) / sizeof(X[0]);

    cout << countSquares(X, Y, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the count of
# squares parallel to both X and Y-axis
# from a given set of points
def countSquares(X,  Y, N) :

    # Initialize result
    count = 0;

    # Initialize a set to store points
    points = [];

    # Initialize a map to store the
    # points in the same vertical line
    vertical = dict.fromkeys(X, None);

    # Store the points in a set
    for i in range(N) :
        points.append((X[i], Y[i]));

    # Store the points in the same vertical line
    # i.e. with same X co-ordinates
    for i in range(N) :
        if vertical[X[i]] is None :
            vertical[X[i]] = [Y[i]];
        else :
            vertical[X[i]].append(Y[i]);

    # Check for every two points
    # in the same vertical line
    for line in vertical :
        X1 = line;
        yList = vertical[line];

        for i in range(len(yList)) :
            Y1 = yList[i];
            for j in range(i + 1, len(yList)) :
                Y2 = yList[j];
                side = abs(Y1 - Y2);
                X2 = X1 + side;

                # Check if other two point are present or not
                if ( X2, Y1 ) in points and ( X2, Y2 ) in points :
                    count += 1;

    return count;

# Driver Code
if __name__ == "__main__" :

    X = [ 0, 2, 0, 2 ]; Y = [ 0, 2, 2, 0 ];

    N = len(X);

    print(countSquares(X, Y, N));

# This code is contributed by AnkitRai01
```

**Output:** 

```
1
```

**时间复杂度:** O(N <sup>2</sup> )。

**辅助空间:** O(N)
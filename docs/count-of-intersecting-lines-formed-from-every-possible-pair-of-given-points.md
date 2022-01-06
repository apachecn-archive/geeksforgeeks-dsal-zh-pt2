# 由每对可能的给定点形成的相交线的数量

> 原文:[https://www . geeksforgeeks . org/由每对可能的给定点形成的交线计数/](https://www.geeksforgeeks.org/count-of-intersecting-lines-formed-from-every-possible-pair-of-given-points/)

给定两个整数数组，X 和 Y 代表 X-Y 平面上的点。计算由每对可能的坐标形成的相交线段对的数量。

> **示例:**
> 
> **输入:** X = [0，1，0，1]，Y = [0，1，3，2]
> 
> **输出:** 14
> 
> **说明:**
> 
> 为了简单起见，让我们表示 A = [0，0]，B = [1，1]，C = [1，2]，D = [0，3]。
> 
> 1.  **点(A，B)与点(A，C)** 之间的线段相交。
> 2.  **点(A，B)与点(A，D)** 之间的线段相交。
> 3.  **点(A，B)和点(B，D)** 之间的线段相交。
> 4.  **点(A，B)和点(C，D)** 之间的线段相交。
> 5.  **点(A，B)和点(B，C)** 之间的线段相交。
> 6.  **点(A，C)和点(C，D)** 之间的线段相交。
> 7.  **点(A，C)和点(B，D)** 之间的线段相交
> 8.  **点(A，C)与点(A，D)** 之间的线段相交。
> 9.  **点(A，C)和点(B，C)** 之间的线段相交..
> 10.  **点(A，D)与点(B，D)** 之间的线段相交。
> 11.  **点(A，D)与点(C，D)** 之间的线段相交。
> 12.  **点(B，C)和点(B，D)** 之间的线段相交。
> 13.  **点(B，C)和点(C，D)** 之间的线段相交。
> 14.  **点(B，D)与点(C，D)** 之间的线段相交。
> 
> **输入:** X = [0，0，0，2]，Y = [0，2，4，0]
> 
> **输出:** 6

**天真方法:**

1.  将所有坐标对存储在数据结构中。
2.  对于每对坐标，检查是否有平行。如果它们不平行，那么这条线一定相交。将答案增加 1。

**时间复杂度:** **O(N^4)**

**有效方法:**

1.  对于每对坐标，存储一条线的这些参数(斜率、x 轴或 y 轴上的截距)。
2.  对于平行于 X 轴的线:
    *   **斜率= 0，截距= Y[i]**
3.  对于平行于 Y 轴的直线:
    *   **斜率= INF，截距= X[i]**
4.  对于所有其他行:
    *   **斜率=(dy/dx =(y2–y1)/(x2–x1)**
    *   为了计算截距，我们知道直线的一般形式，即 y = (dy/dx)*x + c
        *   当直线本身通过(x1，y1)时，用 y1 代替 y，用 x1 代替 x。
        *   经过以上步骤，我们得到**截距=(y1 * dx–x1 * dy)/dx**
5.  对于每一行，我们有三种情况:
    *   一条线可以具有与其他线相同的斜率和截距。这些线不会相交，因为它们基本上是同一条线。
    *   一条线可以与另一条线具有相同的斜率和不同的截距。这些线也不会相交，因为它们是平行的。
    *   **一条线可以有不同于其他线的斜率。这些线肯定会相交，不管它们的截距如何**。
6.  存储相同斜率的线的频率根据上述条件绘制一张[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，并固定一种线段类型，计算与剩余线相交的线段数。

**注:**

在下面的实现中，我们避免了使用双精度来避免由于精度错误而导致的错误。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate total pairs
// of intersecting lines
int totalPairsOfIntersectineLines(
    int X[], int Y[], int N)
{
    // Set to check the occurences
    // of slope and intercept
    // It will store the slope dy/dx
    // as {dy, dx} and intercept as {c1, c2}
    set<pair<pair<int, int>, pair<int, int> > > st;

    // Map to keep track of count of slopes
    map<pair<int, int>, int> mp;
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N; j++) {

            // Numerator of the slope
            int dx = X[j] - X[i];

            // Denominator of the slope
            int dy = Y[j] - Y[i];

            // Making dx and dy coprime
            // so that we do not repeat
            int g = __gcd(dx, dy);
            dx /= g, dy /= g;

            // Checking for lines parallel to y axis
            if (dx == 0) {

                // Intercepts of the line
                int c1, c2;
                c1 = X[i];
                c2 = INT_MAX;

                // pair to check the previous occurence of
                // the line parameters
                pair<pair<int, int>, pair<int, int> > pr
                    = { { dx, dy }, { c1, c2 } };

                if (st.find(pr) != st.end()) {
                    // Do nothing as this line is same just
                    // an etenstion to some line with same
                    // slope and intercept
                }
                else {

                    // Insert this line to the set
                    st.insert(pr);

                    // increase the count of the slope of
                    // this line
                    mp[pr.first]++;
                }
            }

            // Checking for lines parallel to x- axis
            else if (dy == 0) {
                int c1, c2;
                c2 = Y[i];
                c1 = INT_MAX;
                pair<pair<int, int>, pair<int, int> > pr
                    = { { dx, dy }, { c1, c2 } };

                if (st.find(pr) != st.end()) {
                    // Do nothing as this line is same just
                    // an etenstion to some line with same
                    // slope and intercept
                }
                else {

                    // Insert this line to the set
                    st.insert(pr);

                    // increase the count of the slope of
                    // this line
                    mp[pr.first]++;
                }
            }
            else {
                int c1, c2;

                // c1 = y*dx - dy*dx
                // If one of them is negative, then
                // generalising that dx is negative and dy
                // is positive so that we don't repeat
                if (dx > 0 && dy < 0) {
                    dx *= -1, dy *= -1;
                }

                // Calculating the intercepts
                c1 = Y[i] * dx - dy * X[i];
                c2 = dx;

                // Normalising the intercepts
                int g2 = __gcd(c1, c2);
                c1 /= g2, c2 /= g2;
                pair<pair<int, int>, pair<int, int> > pr
                    = { { dx, dy }, { c1, c2 } };

                if (st.find(pr) != st.end()) {
                    // Do nothing as this line is same just
                    // an etenstion to some line with same
                    // slope and intercept
                }
                else {

                    // Insert this line to the set
                    st.insert(pr);

                    // increase the count of the slope of
                    // this line
                    mp[pr.first]++;
                }
            }
        }
    }

    // vector for storing all the counts
    // of the lines with different parameters
    vector<int> v;
    for (auto count : mp) {
        v.push_back(count.second);
    }
    // Counting all different line segments
    int cnt = accumulate(v.begin(), v.end(), 0);

    // Variable to store the count
    int ans = 0;
    for (int i = 0; i < v.size(); i++) {

        // Decreasing the count by current line segments
        // which will be parallel to each other
        cnt -= v[i];

        // Intersecting all other line
        // segments with this line segment
        ans += cnt * v[i];
    }
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int N = 4;
    int X[] = { 0, 1, 0, 1 };
    int Y[] = { 0, 1, 3, 2 };

    // Function call
    cout << totalPairsOfIntersectineLines(X, Y, N);
    return 0;
}
```

**Output**

```
14
```

**时间复杂度:O(N*N*logN)**

**空间复杂度:O(N)**
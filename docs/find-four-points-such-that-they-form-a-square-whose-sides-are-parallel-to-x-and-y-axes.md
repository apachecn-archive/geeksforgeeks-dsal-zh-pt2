# 找出四个点，使它们形成一个边平行于 x 轴和 y 轴的正方形

> 原文:[https://www . geeksforgeeks . org/find-四点，这样它们就形成了一个边平行于 x 轴和 y 轴的正方形/](https://www.geeksforgeeks.org/find-four-points-such-that-they-form-a-square-whose-sides-are-parallel-to-x-and-y-axes/)

给定 n 个点对，任务是找到四个点，使它们形成一个边平行于 x 轴和 y 轴的正方形，否则打印“没有这样的正方形”。
如果可能不止一个正方形，那么选择面积最大的正方形。

**示例:**

> **输入:** n = 6，点= (1，1)，(4，4)，(3，4)，(4，3)，(1，4)，(4，1)
> **输出:**
> 正方形的边是:3，正方形的点是 1，1 4，1 1，4 4，4
> **解释:**点 1，1 4，1 1，4 4，4 形成边 3 的正方形
> 
> **输入:** n= 6，点数= (1，1)，(4，5)，(3，4)，(4，3)，(7，4)，(3，1)
> **输出:**无此方块

**简单方法:**选择所有可能的具有四个嵌套循环的点对，然后看这些点是否形成平行于主轴的正方形。如果是，检查它是否是目前为止面积最大的正方形，并存储结果，然后在程序结束时显示结果。
**时间复杂度:** O(N^4)

**高效方法:**为正方形的右上角和左下角创建一个嵌套循环，用这两个点组成一个正方形，然后检查假设的其他两个点是否实际存在。要检查点是否存在，请创建地图并将点存储在地图中，以减少检查点是否存在的时间。此外，检查到目前为止面积最大的正方形，并在最后打印出来。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implemenataion of the above approach
#include <bits/stdc++.h>
using namespace std;

// find the largest square
void findLargestSquare(long long int points[][2], int n)
{
    // map to store which points exist
    map<pair<long long int, long long int>, int> m;

    // mark the available points
    for (int i = 0; i < n; i++) {
        m[make_pair(points[i][0], points[i][1])]++;
    }
    long long int side = -1, x = -1, y = -1;

    // a nested loop to choose the opposite corners of square
    for (int i = 0; i < n; i++) {

        // remove the chosen point
        m[make_pair(points[i][0], points[i][1])]--;
        for (int j = 0; j < n; j++) {

            // remove the chosen point
            m[make_pair(points[j][0], points[j][1])]--;

            // check if the other two points exist
            if (i != j 
                  && (points[i][0]-points[j][0]) == (points[i][1]-points[j][1])){
                if (m[make_pair(points[i][0], points[j][1])] > 0
                     && m[make_pair(points[j][0], points[i][1])] > 0) {

                    // if the square is largest then store it
                    if (side < abs(points[i][0] - points[j][0]) 
                         || (side == abs(points[i][0] - points[j][0]) 
                            && ((points[i][0] * points[i][0] 
                                   + points[i][1] * points[i][1]) 
                                      < (x * x + y * y)))) {
                        x = points[i][0];
                        y = points[i][1];
                        side = abs(points[i][0] - points[j][0]);
                    }
                }
            }

            // add the removed point
            m[make_pair(points[j][0], points[j][1])]++;
        }

        // add the removed point
        m[make_pair(points[i][0], points[i][1])]++;
    }

    // display the largest square
    if (side != -1)
        cout << "Side of the square is : " << side
             << ", \npoints of the square are " << x << ", " << y
             << " "
             << (x + side) << ", " << y
             << " "
             << (x) << ", " << (y + side)
             << " "
             << (x + side) << ", " << (y + side) << endl;
    else
        cout << "No such square" << endl;
}

//Driver code
int main()
{
    int n = 6;

    // given points
    long long int points[n][2]
      = { { 1, 1 }, { 4, 4 }, { 3, 4 }, { 4, 3 }, { 1, 4 }, { 4, 1 } };

    // find the largest square
    findLargestSquare(points, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implemenataion of the above approach

# find the largest square
def findLargestSquare(points,n):

    # map to store which points exist
    m = dict()

    # mark the available points
    for i in range(n):
        m[(points[i][0], points[i][1])] = \
        m.get((points[i][0], points[i][1]), 0) + 1

    side = -1
    x = -1
    y = -1

    # a nested loop to choose the opposite corners of square
    for i in range(n):

        # remove the chosen point
        m[(points[i][0], points[i][1])]-=1
        for j in range(n):

            # remove the chosen point
            m[(points[j][0], points[j][1])]-=1

            # check if the other two points exist
            if (i != j and (points[i][0]-points[j][0]) == \
                (points[i][1]-points[j][1])):
                if (m[(points[i][0], points[j][1])] > 0 and 
                    m[(points[j][0], points[i][1])] > 0):

                    # if the square is largest then store it
                    if (side < abs(points[i][0] - points[j][0])
                        or (side == abs(points[i][0] - points[j][0])
                            and ((points[i][0] * points[i][0]
                                + points[i][1] * points[i][1])
                                    < (x * x + y * y)))):
                        x = points[i][0]
                        y = points[i][1]
                        side = abs(points[i][0] - points[j][0])

            # add the removed point
            m[(points[j][0], points[j][1])] += 1

        # add the removed point
        m[(points[i][0], points[i][1])] += 1

    # display the largest square
    if (side != -1):
        print("Side of the square is : ",side
            ,", \npoints of the square are ",x,", ",y
            ," "
            ,(x + side),", ",y
            ," "
            ,(x),", ",(y + side)
            ," "
            ,(x + side),", ",(y + side))
    else:
        print("No such square")

# Driver code
n = 6

# given points
points=[[ 1, 1 ],[ 4, 4 ],[ 3, 4 ],[ 4, 3 ],[ 1, 4 ],[ 4, 1 ] ]

# find the largest square
findLargestSquare(points, n)

# This code is contributed by mohit kumar 29
```

**Output:**

```
Side of the square is : 3, 
points of the square are 1, 1 4, 1 1, 4 4, 4

```

**时间复杂度:** O(N^2)
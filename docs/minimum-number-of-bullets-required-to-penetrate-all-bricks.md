# 穿透所有砖块所需的最小子弹数

> 原文:[https://www . geesforgeks . org/穿透所有砖块所需的最小子弹数/](https://www.geeksforgeeks.org/minimum-number-of-bullets-required-to-penetrate-all-bricks/)

给定一个[矩阵](https://www.geeksforgeeks.org/matrix/) **砖块【】【】**表示二维空间中矩形砖块排列的砖块宽度的开始和结束坐标。子弹可以从 X 轴上的不同点垂直射出。坐标为 **X <sub>起点</sub>****X<sub>终点</sub>** 的砖块被从 **X** 位置射出的子弹穿透，如果 **X <sub>起点</sub> ≤ X ≤ X <sub>终点</sub>** 。可以射出的子弹数量没有限制，一颗子弹一旦射出就会沿着 Y 轴无限行进。任务是找到穿透所有砖块必须射出的最小子弹数。

**示例:**

> **输入:**砖块[][] = {{10，16}，{2，8}，{1，6}，{7，12}}
> **输出:** 2
> **说明:**
> 在 X = 6 处射出一发子弹，穿透{2，8}和{1，6}
> 处的砖块另一发子弹在 X = 11 处，穿透{7，12}和{10，16}处的砖块
> 
> **输入:**砖块[][] = {{5000，90000}，{150，499}，{1，100}}
> **输出:** 3

**进场:**思路是用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决此问题:

1.  用 0 初始化所需的项目符号数。
2.  [在 **X <sub>的基础上，将 **X <sub>开始</sub>T5、 **X <sub>结束</sub>T9】按升序排序。****</sub>**](https://www.geeksforgeeks.org/sort-c-stl/)
3.  遍历排序后的位置列表，检查当前砖块的 **X <sub>起点</sub>** 是否大于或等于前一块砖块的 **X <sub>终点</sub>** 。如果是这样，那么还需要一颗子弹。所以把计数增加 1。否则继续。
4.  在末尾返回计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Custom comparator function
bool compare(vector<int>& a,
             vector<int>& b)
{
    return a[1] < b[1];
}

// Function to find the minimum number of
// bullets required to penetrate all bricks
int findMinBulletShots(vector<vector<int> >& points)
{
    // Sort the points in ascending order
    sort(points.begin(), points.end(),
         compare);

    // Check if there are no points
    if (points.size() == 0)
        return 0;

    int cnt = 1;
    int curr = points[0][1];

    // Iterate through all the points
    for (int j = 1; j < points.size(); j++) {
        if (curr < points[j][0]) {

            // Increase the count
            cnt++;
            curr = points[j][1];
        }
    }

    // Return the count
    return cnt;
}

// Driver Code
int main()
{
    // Given coordinates of bricks
    vector<vector<int> > bricks{ { 5000, 900000 },
                                 { 1, 100 },
                                 { 150, 499 } };

    // Function call
    cout << findMinBulletShots(bricks);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Function to find the minimum number of 
// bullets required to penetrate all bricks 
static int findMinBulletShots(int[][] points) 
{ 

    // Sort the points in ascending order 
    Arrays.sort(points, (a, b) -> a[1] - b[1]);

    // Check if there are no points 
    if (points.length == 0) 
        return 0; 

    int cnt = 1; 
    int curr = points[0][1]; 

    // Iterate through all the points 
    for(int j = 1; j < points.length; j++) 
    { 
        if (curr < points[j][0])
        { 

            // Increase the count 
            cnt++; 
            curr = points[j][1]; 
        } 
    } 

    // Return the count 
    return cnt; 
} 

// Driver code
public static void main (String[] args)
{

    // Given coordinates of bricks 
    int[][] bricks = { { 5000, 900000 }, 
                       { 1, 100 }, 
                       { 150, 499 } }; 

    // Function call 
    System.out.print(findMinBulletShots(bricks)); 
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number of
# bullets required to penetrate all bricks
def findMinBulletShots(points):

    # Sort the points in ascending order
    for i in range(len(points)):
        points[i] = points[i][::-1]

    points = sorted(points)

    for i in range(len(points)):
        points[i] = points[i][::-1]

    # Check if there are no points
    if (len(points) == 0):
        return 0

    cnt = 1
    curr = points[0][1]

    # Iterate through all the points
    for j in range(1, len(points)):
        if (curr < points[j][0]):

            # Increase the count
            cnt += 1
            curr = points[j][1]

    # Return the count
    return cnt

# Driver Code
if __name__ == '__main__':

    # Given coordinates of bricks
    bricks = [ [ 5000, 900000 ],
               [ 1, 100 ],
               [ 150, 499 ] ]

    # Function call
    print(findMinBulletShots(bricks))

# This code is contributed by mohit kumar 29
```

**Output:** 

```
3

```

***时间复杂度:** O(N * log N)，其中 N 为砖块数。*
***辅助空间:** O(1)*
# 某点(X，Y)碰撞计数

> 原文:[https://www . geesforgeks . org/x-y 点碰撞计数/](https://www.geeksforgeeks.org/count-of-collisions-at-a-point-x-y/)

给定一个大小为 **N * 3** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**arr【】【】【】**使得每行由定义一个元素的 3 个属性组成，即 **(x 坐标、Y 坐标、速度)**，以及两个整数 **X** 和 **Y** ，任务是计算在点 **(X，Y)** 处可能的碰撞对的数量，如果给定数组中的每个元素都在直线移动
**示例:**

> **输入:** arr[] = [ [5，12，1]，[16，63，5]，[-10，24，2]，[7，24，2]，[-24，7，2] ]，X = 0，Y = 0
> **输出:** 4
> **解释:**
> 以下一对元素之间可能存在冲突:(arr[0]，arr[1])，(arr[0]，arr[2])，(arr[2]
> **输入:** arr[] = [ [1，42，9] ]，X = 1，Y = 1
> **输出:** 0
> **说明:**
> 由于存在单点，因此不会发生碰撞。
> 因此，总碰撞数为 0。

**方法:**想法是简单地找到每个点到达给定点(X，Y)的**时间**。如果两点同时到达原点，那么它们肯定会碰撞。现在，要计算每个点花费的时间，请执行以下操作:

> 对于给定的点(x，y)和速度 **S**
> 距离 **D** 由下式给出:
> D = =√((x2–x1)<sup>2</sup>+(y2–y1)<sup>2</sup>)=√((x)<sup>2</sup>+(y)<sup>2</sup>)
> 时间=距离/速度，两边求平方从距离中去根，
> **时间**

计算每个点的**时间 <sup>2</sup>** 后，只需检查它们中哪些是相同的，并计算碰撞的次数。
以下是步骤:

*   遍历数组 **arr[]** 。
*   创建一个新的数组 **Time[]** ，对于每个点，计算时间并追加到这个数组中并排序。
*   遍历**时间[]** 并统计同时到达给定点的元素数量，使用该计数计算当时的碰撞数量。
*   最后，返回冲突总数。

下面是上述方法的实现:

## C++14

```
// C++14 program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// possible pairs of collisions
int solve(vector<vector<int>> &D, int N,
                           int X, int Y)
{

    // Stores the time at which
    // points reach the origin
    vector<double> T;

    // Calculate time for each point
    for(int i = 0; i < N; i++)
    {
        int x = D[i][0];
        int y = D[i][1];

        double speed = D[i][2];

        double time = ((x * x - X * X) +
                       (y * y - Y * Y)) /
                       (speed * speed);

        T.push_back(time);
    }

    // Sort the times
    sort(T.begin(), T.end());

    int i = 0;
    int total = 0;

    // Counting total collisions
    while (i < T.size() - 1)
    {

        // Count of elements arriving at
        // a given point at the same time
        int count = 1;

        while (i < T.size() - 1 and
                T[i] == T[i + 1])
        {
            count += 1;
            i += 1;
        }

        total += (count * (count - 1)) / 2;
        i += 1;
    }
    return total;
}

// Driver Code
int main()
{
    int N = 5;

    // Given set of points with speed
    vector<vector<int>> D = { { 5, 12, 1 },
                              { 16, 63, 5 },
                              { -10, 24, 2 },
                              { 7, 24, 2 },
                              { -24, 7, 2 } };

    int X = 0, Y = 0;

    // Function call
    cout << (solve(D, N, X, Y));

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the count of
// possible pairs of collisions
static double solve(int[][] D, int N,
                        int X, int Y)
{

    // Stores the time at which
    // points reach the origin
    ArrayList<Double> T = new ArrayList<>();

    // Calculate time for each point
    for(int i = 0; i < N; i++)
    {
        int x = D[i][0];
        int y = D[i][1];

        double speed = D[i][2];

        double time = ((x * x - X * X) +
                       (y * y - Y * Y)) /
                       (speed * speed);

        T.add(time);
    }

    // Sort the times
    Collections.sort(T);

    int i = 0;
    int total = 0;

    // Counting total collisions
    while (i < (T.size() - 1))
    {

        // Count of elements arriving at
        // a given point at the same time
        int count = 1;

        while ((i < (T.size() - 1)) &&
               (Double.compare(T.get(i),
                               T.get(i + 1)) == 0))
        {
            count += 1;
            i += 1;
        }

        total += (count * (count - 1)) / 2;
        i += 1;

    }
    return total;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = 5;

    // Given set of points with speed
    int[][] D = { { 5, 12, 1 },
                  { 16, 63, 5 },
                  { -10, 24, 2 },
                  { 7, 24, 2 },
                  { -24, 7, 2 } };

    int X = 0, Y = 0;

    // Function call
    System.out.println(solve(D, N, X, Y));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find the count of
# possible pairs of collisions
def solve(D, N, X, Y):

    # Stores the time at which
    # points reach the origin
    T = []

    # Calculate time for each point
    for i in range(N):

        x = D[i][0]
        y = D[i][1]

        speed = D[i][2]

        time = ((x * x - X * X) +
                (y * y - Y * Y)) / (speed * speed)

        T.append(time)

    # Sort the times
    T.sort()

    i = 0
    total = 0

    # Counting total collisions
    while i<len(T)-1:

        # Count of elements arriving at
        # a given point at the same time
        count = 1

        while i<len(T)-1 and T[i] == T[i + 1]:
            count += 1
            i+= 1

        total+= (count*(count-1))/2
        i+= 1

    return total

# Driver Code

N = 5

# Given set of points with speed
D = [[5, 12, 1], [16, 63, 5], \
    [-10, 24, 2], [7, 24, 2], \
    [-24, 7, 2]]

X = 0
Y = 0

# Function Call
print(solve(D, N, X, Y))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;

class GFG{

// Function to find the count of
// possible pairs of collisions
static double solve(int[, ] D, int N,
                        int X, int Y)
{

    // Stores the time at which
    // points reach the origin
    ArrayList T = new ArrayList();

    // Calculate time for each point
    for(int i = 0; i < N; i++)
    {
        int x = D[i, 0];
        int y = D[i, 1];

        double speed = D[i, 2];

        double time = ((x * x - X * X) +
                       (y * y - Y * Y)) /
                       (speed * speed);

        T.Add(time);
    }

    // Sort the times
    T.Sort();

    int j = 0;
    int total = 0;

    // Counting total collisions
    while (j < (T.Count - 1))
    {

        // Count of elements arriving at
        // a given point at the same time
        int count = 1;

        while ((j < (T.Count - 1)) &&
              (Convert.ToDouble(T[j]).CompareTo(
               Convert.ToDouble(T[j + 1])) == 0))
        {
            count += 1;
            j += 1;
        }
        total += (count * (count - 1)) / 2;
        j += 1;
    }
    return total;
}

// Driver Code
public static void Main (String[] args)
{
    int N = 5;

    // Given set of points with speed
    int [,] D = new int [,] { { 5, 12, 1 },
                              { 16, 63, 5 },
                              { -10, 24, 2 },
                              { 7, 24, 2 },
                              { -24, 7, 2 } };

    int X = 0, Y = 0;

    // Function call
    Console.WriteLine(solve(D, N, X, Y));
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the count of
// possible pairs of collisions
function solve(D,N,X,Y)
{
    // Stores the time at which
    // points reach the origin
    let T = [];

    // Calculate time for each point
    for(let i = 0; i < N; i++)
    {
        let x = D[i][0];
        let y = D[i][1];

        let speed = D[i][2];

        let time = ((x * x - X * X) +
                       (y * y - Y * Y)) /
                       (speed * speed);

        T.push(time);
    }

    // Sort the times
    T.sort(function(a,b){return a-b;});

    let i = 0;
    let total = 0;

    // Counting total collisions
    while (i < (T.length - 1))
    {

        // Count of elements arriving at
        // a given point at the same time
        let count = 1;

        while ((i < (T.length - 1)) &&
               (T[i]==T[i+1]))
        {
            count += 1;
            i += 1;
        }

        total += (count * (count - 1)) / 2;
        i += 1;

    }
    return total;
}

// Driver Code
let arr=[1, 2, 3, 4, 5];
let N = 5;
 // Given set of points with speed
let D = [[5, 12, 1], [16, 63, 5],
    [-10, 24, 2], [7, 24, 2],
    [-24, 7, 2]];

let X = 0, Y = 0;
// Function call
document.write(solve(D, N, X, Y).toFixed(1));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4.0
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(1)*
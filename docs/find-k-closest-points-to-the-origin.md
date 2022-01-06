# 找到离原点最近的 K 个点

> 原文:[https://www . geesforgeks . org/find-k-最接近原点/](https://www.geeksforgeeks.org/find-k-closest-points-to-the-origin/)

给定二维平面上的一系列点和一个整数 K。任务是找到离原点最近的 K 个点并打印它们。
**注**:平面上两点之间的距离为[欧氏距离](https://en.wikipedia.org/wiki/Euclidean_distance)。

**示例:**

```
Input : point = [[3, 3], [5, -1], [-2, 4]], K = 2
Output : [[3, 3], [-2, 4]]
Square of Distance of origin from this point is 
(3, 3) = 18
(5, -1) = 26
(-2, 4) = 20
So the closest two points are [3, 3], [-2, 4].

Input : point = [[1, 3], [-2, 2]], K  = 1
Output : [[-2, 2]]
Square of Distance of origin from this point is
(1, 3) = 10
(-2, 2) = 8 
So the closest point to origin is (-2, 2)
```

**方法:**思路是计算每个给定点距原点的欧氏距离，并根据找到的欧氏距离对数组进行排序。打印列表中前 k 个最接近的点。

**算法:**
分别考虑坐标为(x1，y1)和(x2，y2)的两点。这两点之间的**欧几里得距离**将是:

```
√{(x2-x1)2 + (y2-y1)2}
```

1.  使用欧氏距离公式按距离对点进行排序。
2.  从列表中选择前 K 个点
3.  以任何顺序打印获得的分数。

**注:**

*   在 multimap 中，我们可以直接存储{(x2-x1)<sup>2</sup>+(y2-y1)<sup>2</sup>}的值，而不是它的平方根，因为以下属性:如果 sqrt(x)<sqrt(y)x<y
*   正因为如此，我们降低了时间复杂度(整数平方根的时间复杂度为 O(√ n))

下面是上述方法的实现:

## C++

```
// C++ program for implementation of 
// above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print required answer
void pClosest(vector<vector<int>> pts, int k)
{

    // In multimap values gets
    // automatically sorted based on
    // their keys which is distance here
    multimap<int, int> mp;
    for(int i = 0; i < pts.size(); i++)
    {
        int x = pts[i][0], y = pts[i][1];
        mp.insert({(x * x) + (y * y) , i});
    }

    for(auto it = mp.begin();
             it != mp.end() && k > 0;
             it++, k--)
        cout << "[" << pts[it->second][0] << ", "
             << pts[it->second][1] << "]" << "\n";
}

// Driver code
int main()
{
    vector<vector<int>> points = { { 3, 3 },
                                   { 5, -1 },
                                   { -2, 4 } };

    int K = 2;

    pClosest(points, K);
    return 0;
}

// This code is contributed by sarthak_eddy.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of 
// above approach
import java.util.*;

class GFG{

// Function to print required answer
static void pClosest(int [][]pts, int k)
{
    int n = pts.length;
    int[] distance = new int[n];
    for(int i = 0; i < n; i++)
    {
        int x = pts[i][0], y = pts[i][1];
        distance[i] = (x * x) + (y * y);
    }

    Arrays.sort(distance);

    // Find the k-th distance
    int distk = distance[k - 1];

    // Print all distances which are
    // smaller than k-th distance
    for(int i = 0; i < n; i++)
    {
        int x = pts[i][0], y = pts[i][1];
        int dist = (x * x) + (y * y);

        if (dist <= distk)
            System.out.println("[" + x + ", " + y + "]");
    }
}

// Driver code
public static void main (String[] args)
{
    int points[][] = { { 3, 3 },
                       { 5, -1 },
                       { -2, 4 } };

    int K = 2;

    pClosest(points, K);
}
}

// This code is contributed by sarthak_eddy.
```

## 蟒蛇 3

```
# Python3 program for implementation of
# above approach

# Function to return required answer
def pClosest(points, K):

    points.sort(key = lambda K: K[0]**2 + K[1]**2)

    return points[:K]

# Driver program
points = [[3, 3], [5, -1], [-2, 4]]

K = 2

print(pClosest(points, K))
```

## C#

```
// C# program for implementation
// of above approach
using System;
class GFG{

// Function to print
// required answer
static void pClosest(int [,]pts,
                     int k)
{
  int n = pts.GetLength(0);

  int[] distance = new int[n];

  for(int i = 0; i < n; i++)
  {
    int x = pts[i, 0],
        y = pts[i, 1];
    distance[i] = (x * x) +
                  (y * y);
  }

  Array.Sort(distance);

  // Find the k-th distance
  int distk = distance[k - 1];

  // Print all distances which are
  // smaller than k-th distance
  for(int i = 0; i < n; i++)
  {
    int x = pts[i, 0],
        y = pts[i, 1];
    int dist = (x * x) +
               (y * y);

    if (dist <= distk)
      Console.WriteLine("[" + x +
                        ", " + y + "]");
  }
}

// Driver code
public static void Main (string[] args)
{
  int [,]points = {{3, 3},
                   {5, -1},
                   {-2, 4}};
  int K = 2;
  pClosest(points, K);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript program for implementation of
// above approach

// Function to print required answer
function pClosest(pts,k)
{
    let n = pts.length;
    let distance = new Array(n);
    for(let i = 0; i < n; i++)
    {
        let x = pts[i][0], y = pts[i][1];
        distance[i] = (x * x) + (y * y);
    }

    distance.sort(function(a,b){return a-b;});

    // Find the k-th distance
    let distk = distance[k - 1];

    // Print all distances which are
    // smaller than k-th distance
    for(let i = 0; i < n; i++)
    {
        let x = pts[i][0], y = pts[i][1];
        let dist = (x * x) + (y * y);

        if (dist <= distk)
            document.write("[" + x + ", " + y + "]<br>");
    }
}

// Driver code
let points = [[3, 3], [5, -1], [-2, 4]];
let K = 2;
pClosest(points, K);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
[[3, 3], [-2, 4]]
```

**复杂度分析:**

*   **时间复杂度:** O(n log n)。
    求每个点距原点的距离的时间复杂度为 O(n)，对数组进行排序的时间复杂度为 O(n log n)
*   **空间复杂度:** O(n)。
    当我们制作一个数组来存储每个点离原点的距离时。
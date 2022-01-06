# 计算 K 维空间中距离等于整数值的点对

> 原文:[https://www . geeksforgeeks . org/count-对间有距离的点-等于 k 维空间中的整数值/](https://www.geeksforgeeks.org/count-pairs-of-points-having-distance-between-them-equal-to-integral-values-in-a-k-dimensional-space/)

给定一个在一个 **K** 维空间中代表 **N** 点的[数组](https://www.geeksforgeeks.org/array-data-structure/) **点[]** ，任务是找出空间中成对点的计数，使得每对点之间的距离是一个整数值。

**示例:**

> **输入:**点[] = { {1，2}，{5，5}，{2，8} }，K = 2
> **输出:** 1
> **说明:**
> 成对点之间的距离(点[0]，点[1]) = 5
> 成对点之间的距离(点[1]，点[2]) = sqrt(58)
> 成对点之间的距离(点[0]，点[2]) = 3 *
> 
> **输入:**分[]= {-3，7，8，2}，{-12，1，10，2}，{-2，8，9，3} }，K = 4
> T3】输出: 2。

**逼近:**思路是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)所有可能的对，找出每对点之间的距离，检查是否为整数值。如果发现为真，则增加计数。最后，打印获得的总计数。按照以下步骤解决问题:

*   成对点之间的距离({ a <sub>1</sub> 、a <sub>2</sub> 、…、a <sub>K</sub> }、{ b <sub>1</sub> 、b <sub>2</sub> 、…、b <sub>K</sub> })可使用以下公式计算:

> 距离(a，b)= sqrt((a<sub>1</sub>–b<sub>1</sub>)<sup>2</sup>+(a<sub>2</sub>–b<sub>2</sub>)<sup>2</sup>+…。+(a<sub>K</sub>–b<sub>K</sub>)<sup>2</sup>)

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，生成给定数组所有可能的对。
*   对于每对点，检查这对点之间的距离是否为整数。如果发现为真，则增加计数。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to  find pairs whose distance between
// the points of is an integer value.
void cntPairs(vector<vector<int> > points, int n, int K)
{

    // Stores count of pairs whose distance
    // between points is an integer
    int ans = 0;

    // Traverse the array, points[]
    for (int i = 0; i < n; i++) {

        for (int j = i + 1; j < n; j++) {

            // Stores distance between
            // points(i, j)
            int dist = 0;

            // Traverse all the points of
            // current pair
            for (int k = 0; k < K; k++) {

                // Update temp
                int temp = (points[i][k]
                            - points[j][k]);

                // Update dist
                dist += temp * temp;
            }

            // If dist is a perfect square
            if (sqrt(dist) * sqrt(dist) == dist) {

                // Update ans
                ans += 1;
            }
        }
    }

    cout << ans << endl;
}

// Driver Code
int main()
{

    // Given value of K
    int K = 2;

    // Given points
    vector<vector<int> > points
        = { { 1, 2 }, { 5, 5 }, { -2, 8 } };

    // Given value of N
    int n = points.size();

    // Function Call
    cntPairs(points, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

  // Function to  find pairs whose distance between
  // the points of is an integer value.
  static void cntPairs(int [][]points, int n, int K)
  {

    // Stores count of pairs whose distance
    // between points is an integer
    int ans = 0;

    // Traverse the array, points[]
    for (int i = 0; i < n; i++)
    {
      for (int j = i + 1; j < n; j++)
      {

        // Stores distance between
        // points(i, j)
        int dist = 0;

        // Traverse all the points of
        // current pair
        for (int k = 0; k < K; k++)
        {

          // Update temp
          int temp = (points[i][k]
                      - points[j][k]);

          // Update dist
          dist += temp * temp;
        }

        // If dist is a perfect square
        if (Math.sqrt(dist) * Math.sqrt(dist) == dist)
        {

          // Update ans
          ans += 1;
        }
      }
    }
    System.out.print(ans +"\n");
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given value of K
    int K = 2;

    // Given points
    int [][]points
      = { { 1, 2 }, { 5, 5 }, { -2, 8 } };

    // Given value of N
    int n = points.length;

    // Function Call
    cntPairs(points, n, K);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to  find pairs whose distance between
# the points of is an integer value.
def cntPairs(points, n, K):

    # Stores count of pairs whose distance
    # between points is an integer
    ans = 0

    # Traverse the array, points[]
    for i in range(0, n):

        for j in range(i + 1, n):

            # Stores distance between
            # points(i, j)
            dist = 0

            # Traverse all the points of
            # current pair
            for k in range(K):

                # Update temp
                temp = (points[i][k] - points[j][k])

                # Update dist
                dist += temp * temp

            # If dist is a perfect square
            if (((dist)**(1/2)) * ((dist)**(1/2)) == dist):

                # Update ans
                ans += 1
    print(ans)

# Driver Code
# Given value of K
K = 2

# Given points
points = [ [ 1, 2 ], [ 5, 5 ], [ -2, 8 ]]

# Given value of N
n = len(points)

# Function Call
cntPairs(points, n, K)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to  find pairs whose distance between
  // the points of is an integer value.
  static void cntPairs(int[, ] points, int n, int K)
  {

    // Stores count of pairs whose distance
    // between points is an integer
    int ans = 0;

    // Traverse the array, points[]
    for (int i = 0; i < n; i++) {

      for (int j = i + 1; j < n; j++) {

        // Stores distance between
        // points(i, j)
        int dist = 0;

        // Traverse all the points of
        // current pair
        for (int k = 0; k < K; k++) {

          // Update temp
          int temp
            = (points[i, k] - points[j, k]);

          // Update dist
          dist += temp * temp;
        }

        // If dist is a perfect square
        if (Math.Sqrt(dist) * Math.Sqrt(dist)
            == dist) {

          // Update ans
          ans += 1;
        }
      }
    }

    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main()
  {

    // Given value of K
    int K = 2;

    // Given points
    int[, ] points = { { 1, 2 }, { 5, 5 }, { -2, 8 } };

    // Given value of N
    int n = points.GetLength(0);

    // Function Call
    cntPairs(points, n, K);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// javascript program for the above approach   
// Function to find pairs whose distance between
    // the points of is an integer value.
    function cntPairs(points , n , K) {

        // Stores count of pairs whose distance
        // between points is an integer
        var ans = 0;

        // Traverse the array, points
        for (i = 0; i < n; i++) {
            for (j = i + 1; j < n; j++) {

                // Stores distance between
                // points(i, j)
                var dist = 0;

                // Traverse all the points of
                // current pair
                for (k = 0; k < K; k++) {

                    // Update temp
                    var temp = (points[i][k] -
                    points[j][k]);

                    // Update dist
                    dist += temp * temp;
                }

                // If dist is a perfect square
                if (Math.sqrt(dist) *
                Math.sqrt(dist) == dist)
                {

                    // Update ans
                    ans += 1;
                }
            }
        }
        document.write(ans + "\n");
    }

    // Driver Code

        // Given value of K
        var K = 2;

        // Given points
        var points = [ [ 1, 2 ], [ 5, 5 ],
        [ -2, 8 ] ];

        // Given value of N
        var n = points.length;

        // Function Call
        cntPairs(points, n, K);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>* K)*
***辅助空间:** O(1)*
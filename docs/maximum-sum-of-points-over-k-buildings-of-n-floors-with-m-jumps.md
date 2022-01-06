# 有 M 跳的 N 层 K 栋建筑上的最大点数和

> 原文:[https://www . geeksforgeeks . org/m-jumps-n 层最大 k 楼点数总和/](https://www.geeksforgeeks.org/maximum-sum-of-points-over-k-buildings-of-n-floors-with-m-jumps/)

给定 **K** 栋 **N** 层，一个站在地上最多能做出 **M** 跳的人。这个人必须爬上顶峰并获得最高分。如果这个人可以爬上楼梯到同一栋楼的下一层，或者他可以跳到任何相邻建筑的下一层，找到可以收集的最大点数。

**示例:**

> **输入** : N = 5，M = 2，K = 3，
> 点数= [ [4，5，1，2，10]，
> [9，7，3，20，16]，
> [ 6，12，13，9，8] ]
> **输出:** 70
> **说明:**从 2 号楼开始。一楼收 9 分。
> 跳到 3 号楼。从二楼收集 12 分，从三楼收集 13 分。(跳 1)
> 跳回 2 号楼。四楼收 20 分，五楼收 16 分。(跳 2)
> 跳数= 2
> 积分数= 9+12+13+20+16 = 70 分
> 
> **输入** : N = 4，M = 1，K = 3，
> 点= [ [7，5，4，10]，
> [8，9，20，16]，
> [ 12，13，3，8] ]
> **输出:** 61

**方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决；

*   首先我们定义 dp 的状态
    *   dp(i，j，k)状态–如果此人在第 **i** 层最多跳了 **j** 次并最终到达第 **k** 号楼，则可以收集的最大点数
*   然后我们将定义基本案例
    *   如果只有一层，那么这个人不能跳，把点数放在那个位置。
    *   如果允许有 0 次跳跃，那么可以选择三个建筑中的一个，并在同一建筑上继续向上攀爬。
    *   所以，人只能从同一栋楼的上一层取点并添加当前点
*   然后我们将定义状态之间的转换
*   如果我们在第一栋楼，那么我们可以:
    *   从第一栋楼下来，往下一层，不准跳
    *   从下一栋楼来，往下一层，一跃而下
*   为这两种情况添加存储在 1 号楼第 1 层的点
*   如果我们在中间建筑上，那么我们可以:
    *   从上一栋楼下来，往下一层，一跃而下
    *   从现在的大楼往下一层，不准跳
    *   可以从下一栋楼来，一层楼下来，一跃而下
*   将为所有 3 种情况添加存储在第 1 层中间建筑中的点数
*   如果我们在最后一栋楼，那么我们可以:
    *   来自上一栋楼，往下一层，再往下一跳
    *   从最后一栋楼下来，往下一层，没有跳跃补充
*   将为这两种情况添加存储在第一层最后一栋建筑物中的点数
*   对于最终答案，在允许的跳跃次数后，返回所有建筑物顶层收集的最大点数。

下面是上述方法的实现:

## C++14

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

int solve(vector<vector<int> >& a, int floors,
          int jumps, int buildings)
{
    /*
     dp(i, j, k) represents state of the maximum
     number of points that can be collected if
     the person is at ith floor having made at
     most j jumps and ended up at kth building.
    */
    int dp[floors + 1][jumps + 1][buildings + 1];

    // Initializing dp with 0
    memset(dp, 0, sizeof(dp));
    for (int i = 1; i <= floors; i++) {
        for (int j = 0; j <= jumps; j++) {
            for (int k = 0; k < buildings; k++) {

                // Base case: first floor
                if (i == 1) {
                    // Cannot jump on ground floor
                    // from any other building
                    dp[i][j][k] = a[k][i - 1];
                }

                // Base case: no jumps allowed
                else if (j == 0) {

                    /* can choose one of the buildings
                    and keep climbing up on the
                    same building so can only take
                    points from prev floor of same
                    building and add current points
                 */
                    dp[i][j][k] = dp[i - 1][j][k]
                                  + a[k][i - 1];
                }

                // transition
                else {

                    // first building
                    if (k == 0) {

                        /*
                        1)can come from building 1,
                        one floor down, no jumps.
                        2)can come from building 2,
                        one floor down, one jump added.
                        add points stored in building 1
                        at the ith floor for both cases.
                        */
                        dp[i][j][k] = max(dp[i - 1][j][k],
                                          dp[i - 1][j - 1][k + 1])
                                      + a[k][i - 1];
                    }

                    // Last Building
                    else if (k == buildings - 1) {

                        /*
                       1)Can come from building k-1 from
                         one floor below, one jump added.
                       2)Can come from building k from
                        one floor below, no jump added.
                        add points stored in building k
                        at the ith floor for both cases.
                            */
                        dp[i][j][k]
                            = max(
                                  dp[i - 1][j - 1][k - 1],
                                  dp[i - 1][j][k])
                              + a[k][i - 1];
                    }

                    // intermediate buildings
                    else {

                        /*
                        1)Can come from the building k-1,
                        one floor down, one jump added
                        2)Can come from the building k,
                        one floor down, no jump
                        3)Can come from the building k+1,
                        one floor down, one jump added.
                        add points stored in building k
                        at the ith floor for all 3 cases
                        */
                        dp[i][j][k]
                            = max(
                                  { dp[i - 1][j - 1][k - 1],
                                    dp[i - 1][j][k],
                                    dp[i - 1][j - 1][k + 1] })
                              + a[k][i - 1];
                    }
                }
            }
        }
    }

    // Return the maximum of points collected
    // over the top floor of all building after
    // engaging in permissible number of jumps
    int ans = 0;
    for (int building = 0; building < buildings; building++)
        ans = max(ans, dp[floors][jumps][building]);

    return ans;
}

// Driver code
int main()
{
    // Number of floors
    // and number of jumps allowed.
    int N = 5, M = 2, K = 3;

    // Number of points
    // at each floor of the buildings.
    vector<vector<int> > a = {
        { 4, 5, 1, 2, 10 },
        { 9, 7, 3, 20, 16 },
        { 6, 12, 13, 9, 8 }
    };

    // Function call
    cout << solve(a, N, M, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG
{

  static int solve(int[][] a, int floors,
                   int jumps, int buildings)
  {
    /*
     dp(i, j, k) represents state of the maximum
     number of points that can be collected if
     the person is at ith floor having made at
     most j jumps and ended up at kth building.
    */
    int [][][]dp = new int[floors + 1][jumps + 1][buildings + 1];

    for (int i = 1; i <= floors; i++) {
      for (int j = 0; j <= jumps; j++) {
        for (int k = 0; k < buildings; k++) {

          // Base case: first floor
          if (i == 1) {
            // Cannot jump on ground floor
            // from any other building
            dp[i][j][k] = a[k][i - 1];
          }

          // Base case: no jumps allowed
          else if (j == 0) {

            /* can choose one of the buildings
                    and keep climbing up on the
                    same building so can only take
                    points from prev floor of same
                    building and add current points
                 */
            dp[i][j][k] = dp[i - 1][j][k]
              + a[k][i - 1];
          }

          // transition
          else {

            // first building
            if (k == 0) {

              /*
                        1)can come from building 1,
                        one floor down, no jumps.
                        2)can come from building 2,
                        one floor down, one jump added.
                        add points stored in building 1
                        at the ith floor for both cases.
                        */
              dp[i][j][k] = Math.max(dp[i - 1][j][k],
                                     dp[i - 1][j - 1][k + 1])
                + a[k][i - 1];
            }

            // Last Building
            else if (k == buildings - 1) {

              /*
                       1)Can come from building k-1 from
                         one floor below, one jump added.
                       2)Can come from building k from
                        one floor below, no jump added.
                        add points stored in building k
                        at the ith floor for both cases.
                            */
              dp[i][j][k]
                = Math.max(
                dp[i - 1][j - 1][k - 1],
                dp[i - 1][j][k])
                + a[k][i - 1];
            }

            // intermediate buildings
            else {

              /*
                        1)Can come from the building k-1,
                        one floor down, one jump added
                        2)Can come from the building k,
                        one floor down, no jump
                        3)Can come from the building k+1,
                        one floor down, one jump added.
                        add points stored in building k
                        at the ith floor for all 3 cases
                        */
              dp[i][j][k]
                = Math.max(
                Math.max( dp[i - 1][j - 1][k - 1],
                         dp[i - 1][j][k]),
                dp[i - 1][j - 1][k + 1] )
                + a[k][i - 1];
            }
          }
        }
      }
    }

    // Return the maximum of points collected
    // over the top floor of all building after
    // engaging in permissible number of jumps
    int ans = 0;
    for (int building = 0; building < buildings; building++)
      ans = Math.max(ans, dp[floors][jumps][building]);

    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {

    // Number of floors
    // and number of jumps allowed.
    int N = 5, M = 2, K = 3;

    // Number of points
    // at each floor of the buildings.
    int[][] a = {
      { 4, 5, 1, 2, 10 },
      { 9, 7, 3, 20, 16 },
      { 6, 12, 13, 9, 8 }
    };

    // Function call
    System.out.print(solve(a, N, M, K) +"\n");

  }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

def solve(a, floors, jumps, buildings):

    #dp(i, j, k) represents state of the maximum
    #number of points that can be collected if
    #the person is at ith floor having made at
    #most j jumps and ended up at kth building.
    dp = [[[0 for i in range(buildings + 1)] for j in range(jumps + 1)] for k in range(floors + 1)]

    for i in range(1, floors + 1, 1):
        for j in range(0, jumps + 1, 1):
            for k in range(buildings):

                # Base case: first floor
                if (i == 1):

                    # Cannot jump on ground floor
                    # from any other building
                    dp[i][j][k] = a[k][i - 1]

                # Base case: no jumps allowed
                elif(j == 0):

                    # can choose one of the buildings
                    # and keep climbing up on the
                    # same building so can only take
                    # points from prev floor of same
                    # building and add current points
                    dp[i][j][k] = dp[i - 1][j][k] + a[k][i - 1]

                # transition
                else:

                    # first building
                    if (k == 0):
                        # 1)can come from building 1,
                        # one floor down, no jumps.
                        # 2)can come from building 2,
                        # one floor down, one jump added.
                        # add points stored in building 1
                        # at the ith floor for both cases.
                        dp[i][j][k] = max(dp[i - 1][j][k], dp[i - 1][j - 1][k + 1]) + a[k][i - 1]

                    # Last Building
                    elif(k == buildings - 1):
                        # 1)Can come from building k-1 from
                        # one floor below, one jump added.
                        # 2)Can come from building k from
                        # one floor below, no jump added.
                        # add points stored in building k
                        # at the ith floor for both cases.
                        dp[i][j][k] = max(dp[i - 1][j - 1][k - 1],dp[i - 1][j][k]) + a[k][i - 1]

                    # intermediate buildings
                    else:
                        # 1)Can come from the building k-1,
                        # one floor down, one jump added
                        # 2)Can come from the building k,
                        # one floor down, no jump
                        # 3)Can come from the building k+1,
                        # one floor down, one jump added.
                        # add points stored in building k
                        # at the ith floor for all 3 cases
                        dp[i][j][k] = max([dp[i - 1][j - 1][k - 1],dp[i - 1][j][k],dp[i - 1][j - 1][k + 1]])+ a[k][i - 1]

    # Return the maximum of points collected
    # over the top floor of all building after
    # engaging in permissible number of jumps
    ans = 0
    for temp in range(buildings):
        ans = max(ans, dp[floors][jumps][temp])

    return ans

# Driver code
if __name__ == '__main__':

    # Number of floors
    # and number of jumps allowed.
    N = 5
    M = 2
    K = 3

    # Number of points
    # at each floor of the buildings.
    a = [[4, 5, 1, 2, 10],
         [9, 7, 3, 20, 16],
         [6, 12, 13, 9, 8]]

    # Function call
    print(solve(a, N, M, K))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# implementation for the above approach
using System;

class GFG
{

  static int solve(int[,] a, int floors,
                   int jumps, int buildings)
  {
    /*
     dp(i, j, k) represents state of the maximum
     number of points that can be collected if
     the person is at ith floor having made at
     most j jumps and ended up at kth building.
    */
    int [,,]dp = new int[floors + 1,jumps + 1,buildings + 1];

    for (int i = 1; i <= floors; i++) {
      for (int j = 0; j <= jumps; j++) {
        for (int k = 0; k < buildings; k++) {

          // Base case: first floor
          if (i == 1)
          {

            // Cannot jump on ground floor
            // from any other building
            dp[i, j, k] = a[k, i - 1];
          }

          // Base case: no jumps allowed
          else if (j == 0) {

            /* can choose one of the buildings
                    and keep climbing up on the
                    same building so can only take
                    points from prev floor of same
                    building and add current points
                 */
            dp[i, j, k] = dp[i - 1, j, k]
              + a[k, i - 1];
          }

          // transition
          else {

            // first building
            if (k == 0) {

              /*
                        1)can come from building 1,
                        one floor down, no jumps.
                        2)can come from building 2,
                        one floor down, one jump added.
                        add points stored in building 1
                        at the ith floor for both cases.
                        */
              dp[i, j, k] = Math.Max(dp[i - 1, j, k],
                                     dp[i - 1, j - 1, k + 1])
                + a[k,i - 1];
            }

            // Last Building
            else if (k == buildings - 1) {

              /*
                       1)Can come from building k-1 from
                         one floor below, one jump added.
                       2)Can come from building k from
                        one floor below, no jump added.
                        add points stored in building k
                        at the ith floor for both cases.
                            */
              dp[i, j, k]
                = Math.Max(
                dp[i - 1,j - 1,k - 1],
                dp[i - 1,j,k])
                + a[k,i - 1];
            }

            // intermediate buildings
            else {

              /*
                        1)Can come from the building k-1,
                        one floor down, one jump added
                        2)Can come from the building k,
                        one floor down, no jump
                        3)Can come from the building k+1,
                        one floor down, one jump added.
                        add points stored in building k
                        at the ith floor for all 3 cases
                        */
              dp[i, j, k]
                = Math.Max(
                Math.Max( dp[i - 1, j - 1, k - 1],
                         dp[i - 1, j, k]),
                dp[i - 1, j - 1, k + 1] )
                + a[k, i - 1];
            }
          }
        }
      }
    }

    // Return the maximum of points collected
    // over the top floor of all building after
    // engaging in permissible number of jumps
    int ans = 0;
    for (int building = 0; building < buildings; building++)
      ans = Math.Max(ans, dp[floors,jumps,building]);

    return ans;
  }

  // Driver code
  public static void Main(string[] args)
  {

    // Number of floors
    // and number of jumps allowed.
    int N = 5, M = 2, K = 3;

    // Number of points
    // at each floor of the buildings.
    int[,] a = {
      { 4, 5, 1, 2, 10 },
      { 9, 7, 3, 20, 16 },
      { 6, 12, 13, 9, 8 }
    };

    // Function call
    Console.WriteLine(solve(a, N, M, K));

  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        function solve(a, floors, jumps, buildings)
        {

            /*
             dp(i, j, k) represents state of the maximum
             number of points that can be collected if
             the person is at ith floor having made at
             most j jumps and ended up at kth building.
            */
            var dp = new Array(floors + 1);

            // create 2D
            for (let i = 0; i < dp.length; i++)
            {
                dp[i] = new Array(jumps + 1).fill(0);
            }

            // create 3D
            for (let i = 0; i < dp.length; i++)
            {
                for (let j = 0; j < dp[0].length; j++)
                {
                    dp[i][j] = new Array(buildings + 1).fill(0);
                }
            }

            // Initializing dp with 0
            for (let i = 1; i <= floors; i++) {
                for (let j = 0; j <= jumps; j++) {
                    for (let k = 0; k < buildings; k++) {

                        // Base case: first floor
                        if (i == 1)
                        {

                            // Cannot jump on ground floor
                            // from any other building
                            dp[i][j][k] = a[k][i - 1];
                        }

                        // Base case: no jumps allowed
                        else if (j == 0) {

                            /* can choose one of the buildings
                            and keep climbing up on the
                            same building so can only take
                            points from prev floor of same
                            building and add current points
                         */
                            dp[i][j][k] = dp[i - 1][j][k]
                                + a[k][i - 1];
                        }

                        // transition
                        else {

                            // first building
                            if (k == 0) {

                                /*
                                1)can come from building 1,
                                one floor down, no jumps.
                                2)can come from building 2,
                                one floor down, one jump added.
                                add points stored in building 1
                                at the ith floor for both cases.
                                */
                                dp[i][j][k] = Math.max(dp[i - 1][j][k],
                                    dp[i - 1][j - 1][k + 1])
                                    + a[k][i - 1];
                            }

                            // Last Building
                            else if (k == buildings - 1) {

                                /*
                               1)Can come from building k-1 from
                                 one floor below, one jump added.
                               2)Can come from building k from
                                one floor below, no jump added.
                                add points stored in building k
                                at the ith floor for both cases.
                                    */
                                dp[i][j][k]
                                    = Math.max(
                                        dp[i - 1][j - 1][k - 1],
                                        dp[i - 1][j][k])
                                    + a[k][i - 1];
                            }

                            // intermediate buildings
                            else {

                                /*
                                1)Can come from the building k-1,
                                one floor down, one jump added
                                2)Can come from the building k,
                                one floor down, no jump
                                3)Can come from the building k+1,
                                one floor down, one jump added.
                                add points stored in building k
                                at the ith floor for all 3 cases
                                */
                                dp[i][j][k]
                                    = Math.max(
                                        dp[i - 1][j - 1][k - 1],
                                        dp[i - 1][j][k],
                                        dp[i - 1][j - 1][k + 1])
                                    + a[k][i - 1];
                            }
                        }
                    }
                }
            }

            // Return the maximum of points collected
            // over the top floor of all building after
            // engaging in permissible number of jumps
            let ans = 0;
            for (let building = 0; building < buildings; building++)
                ans = Math.max(ans, dp[floors][jumps][building]);

            return ans;
        }

        // Driver code

        // Number of floors
        // and number of jumps allowed.
        let N = 5, M = 2, K = 3;

        // Number of points
        // at each floor of the buildings.
        let a = [
            [4, 5, 1, 2, 10],
            [9, 7, 3, 20, 16],
            [6, 12, 13, 9, 8]
        ];

        // Function call
        document.write(solve(a, N, M, K));

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
70
```

**时间复杂度:** O(N*M*K)表示 O(楼层*跳跃*建筑)
T3】辅助空间: O(N*M*K)表示 O(楼层*跳跃*建筑)
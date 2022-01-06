# 矩阵中的最小奇数成本路径

> 原文:[https://www . geeksforgeeks . org/矩阵中最小奇数成本路径/](https://www.geeksforgeeks.org/minimum-odd-cost-path-in-a-matrix/)

给定一个矩阵，任务是找到到达矩阵底部的奇数的最小路径的成本。如果不存在这样的路径，请打印-1。
**注意:**只允许右下、左下、直下移动。

**示例:**

```
Input: mat[] = 
{{ 1, 2, 3, 4, 6},
{ 1, 2, 3, 4, 5 },
{ 1, 2, 3, 4, 5 },
{ 1, 2, 3, 4, 5 },
{ 100, 2, 3, 4, 5 }

Output: 11

Input: mat[][] = 
{{1, 5, 2},
{7, 2, 2},
{2, 8, 1}}

Output: 5
```

**方法:**这个问题可以用动态规划来解决:

> 对于第一行(基本情况)，成本是
> floor[0][j]=给定的[0][j] (floor 是我们的成本数组，给定的是我们的给定矩阵)

> //对于最左边的元素
> if(j = = 0)
> floor[I][j]=给定的[i][j]+min(floor[i-1][j]，floor[I-1][j+1])；

> //对于最右边的元素
> else if(j = = N-1)
> floor[I][j]=给定的[i][j] + min(floor[i-1][j]，floor[i-1][j-1])

*   因为除了最左边和最右边的元素之外，任何元素都可以通过上面或左上或右上行的块直接到达。所以，

> 否则
> 楼层[i][j] = a[i][j] + min(楼层[i-1][j-1] +楼层[i-1][j] +楼层[i-1][j+1])

最后，返回最后一行的最小奇数。如果它不存在，返回-1。

**以下是上述方法的实现:**

## C++

```
// C++ program to find Minimum
// odd cost path in a matrix
#include <bits/stdc++.h>
#define M 100 // number of rows
#define N 100 // number of columns
using namespace std;

// Function to find the minimum cost
int find_min_odd_cost(int given[M][N], int m, int n)
{
    int floor[M][N] = { { 0 }, { 0 } };
    int min_odd_cost = 0;
    int i, j, temp;

    for (j = 0; j < n; j++)
        floor[0][j] = given[0][j];

    for (i = 1; i < m; i++)
        for (j = 0; j < n; j++) {

            // leftmost element
            if (j == 0) {
                floor[i][j] = given[i][j];
                floor[i][j] += min(floor[i - 1][j], floor[i - 1][j + 1]);
            }

            // rightmost element
            else if (j == n - 1) {
                floor[i][j] = given[i][j];
                floor[i][j] += min(floor[i - 1][j], floor[i - 1][j - 1]);
            }

            // Any element except leftmost and rightmost element of a row
            // is reachable from direct upper or left upper or right upper
            // row's block
            else {

                // Counting the minimum cost
                temp = min(floor[i - 1][j], floor[i - 1][j - 1]);
                temp = min(temp, floor[i - 1][j + 1]);
                floor[i][j] = given[i][j] + temp;
            }
        }

    min_odd_cost = INT_MAX;

    // Find the minimum cost
    for (j = 0; j < n; j++) {
        if (floor[n - 1][j] % 2 == 1) {
            if (min_odd_cost > floor[n - 1][j])
                min_odd_cost = floor[n - 1][j];
        }
    }

    if (min_odd_cost == INT_MIN)
        return -1;

    return min_odd_cost;
}

// Driver code
int main()
{
    int m = 5, n = 5;
    int given[M][N] = { { 1, 2, 3, 4, 6 },
                        { 1, 2, 3, 4, 5 },
                        { 1, 2, 3, 4, 5 },
                        { 1, 2, 3, 4, 5 },
                        { 100, 2, 3, 4, 5 } };

    cout << "Minimum odd cost is "
         << find_min_odd_cost(given, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum odd
// cost path in a matrix
public class GFG {

    public static final int M = 100 ;
    public static final int N = 100 ;

    // Function to find the minimum cost
    static int find_min_odd_cost(int given[][], int m, int n)
    {
        int floor[][] = new int [M][N];
        int min_odd_cost = 0;
        int i, j, temp;

        for (j = 0; j < n; j++)
            floor[0][j] = given[0][j];

        for (i = 1; i < m; i++)
            for (j = 0; j < n; j++) {

                // leftmost element
                if (j == 0) {
                    floor[i][j] = given[i][j];
                    floor[i][j] += Math.min(floor[i - 1][j], floor[i - 1][j + 1]);
                }

                // rightmost element
                else if (j == n - 1) {
                    floor[i][j] = given[i][j];
                    floor[i][j] += Math.min(floor[i - 1][j], floor[i - 1][j - 1]);
                }

                // Any element except leftmost and rightmost element of a row
                // is reachable from direct upper or left upper or right upper
                // row's block
                else {

                    // Counting the minimum cost
                    temp = Math.min(floor[i - 1][j], floor[i - 1][j - 1]);
                    temp = Math.min(temp, floor[i - 1][j + 1]);
                    floor[i][j] = given[i][j] + temp;
                }
            }

        min_odd_cost = Integer.MAX_VALUE;

        // Find the minimum cost
        for (j = 0; j < n; j++) {
            if (floor[n - 1][j] % 2 == 1) {
                if (min_odd_cost > floor[n - 1][j])
                    min_odd_cost = floor[n - 1][j];
            }
        }

        if (min_odd_cost == Integer.MIN_VALUE)
            return -1;

        return min_odd_cost;
    }
    // Driver code
    public static void main(String args[])
    {
         int m = 5, n = 5;
            int given[][] = { { 1, 2, 3, 4, 6 },
                                { 1, 2, 3, 4, 5 },
                                { 1, 2, 3, 4, 5 },
                                { 1, 2, 3, 4, 5 },
                                { 100, 2, 3, 4, 5 } };

            System.out.println( "Minimum odd cost is " + find_min_odd_cost(given, m, n));
    }
    // This Code is contributed by ANKITRAI1
}

```

## 蟒蛇 3

```
# Python3 program to find Minimum
# odd cost path in a matrix
M = 100 # number of rows
N = 100 # number of columns

# Function to find the minimum cost
def find_min_odd_cost(given, m, n):

    floor = [[0 for i in range(M)]
                for i in range(N)]
    min_odd_cost = 0
    i, j, temp = 0, 0, 0

    for j in range(n):
        floor[0][j] = given[0][j]

    for i in range(1, m):
        for j in range(n):

            # leftmost element
            if (j == 0):
                floor[i][j] = given[i][j];
                floor[i][j] += min(floor[i - 1][j],
                                   floor[i - 1][j + 1])
            # rightmost element
            elif (j == n - 1):
                floor[i][j] = given[i][j];
                floor[i][j] += min(floor[i - 1][j],
                                   floor[i - 1][j - 1])

            # Any element except leftmost and rightmost
            # element of a row is reachable from direct
            # upper or left upper or right upper row's block
            else:

                # Counting the minimum cost
                temp = min(floor[i - 1][j],
                           floor[i - 1][j - 1])
                temp = min(temp, floor[i - 1][j + 1])
                floor[i][j] = given[i][j] + temp

    min_odd_cost = 10**9

    # Find the minimum cost
    for j in range(n):
        if (floor[n - 1][j] % 2 == 1):
            if (min_odd_cost > floor[n - 1][j]):
                min_odd_cost = floor[n - 1][j]

    if (min_odd_cost == -10**9):
        return -1;

    return min_odd_cost

# Driver code
m, n = 5, 5
given = [[ 1, 2, 3, 4, 6 ],
         [ 1, 2, 3, 4, 5 ],
         [ 1, 2, 3, 4, 5 ],
         [ 1, 2, 3, 4, 5 ],
         [ 100, 2, 3, 4, 5 ]]

print("Minimum odd cost is",
       find_min_odd_cost(given, m, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find minimum odd
// cost path in a matrix

using System;
public class GFG {

    public static int M = 100 ;
    public static int N = 100 ;

    // Function to find the minimum cost
    static int find_min_odd_cost(int[,] given, int m, int n)
    {
        int[,] floor = new int [M,N];
        int min_odd_cost = 0;
        int i, j, temp;

        for (j = 0; j < n; j++)
            floor[0,j] = given[0,j];

        for (i = 1; i < m; i++)
            for (j = 0; j < n; j++) {

                // leftmost element
                if (j == 0) {
                    floor[i,j] = given[i,j];
                    floor[i,j] += Math.Min(floor[i - 1,j], floor[i - 1,j + 1]);
                }

                // rightmost element
                else if (j == n - 1) {
                    floor[i,j] = given[i,j];
                    floor[i,j] += Math.Min(floor[i - 1,j], floor[i - 1,j - 1]);
                }

                // Any element except leftmost and rightmost element of a row
                // is reachable from direct upper or left upper or right upper
                // row's block
                else {

                    // Counting the minimum cost
                    temp = Math.Min(floor[i - 1,j], floor[i - 1,j - 1]);
                    temp = Math.Min(temp, floor[i - 1,j + 1]);
                    floor[i,j] = given[i,j] + temp;
                }
            }

        min_odd_cost = int.MaxValue;

        // Find the minimum cost
        for (j = 0; j < n; j++) {
            if (floor[n - 1,j] % 2 == 1) {
                if (min_odd_cost > floor[n - 1,j])
                    min_odd_cost = floor[n - 1,j];
            }
        }

        if (min_odd_cost == int.MinValue)
            return -1;

        return min_odd_cost;
    }
    // Driver code
    public static void Main()
    {
         int m = 5, n = 5;
            int[,] given = { { 1, 2, 3, 4, 6 },
                                { 1, 2, 3, 4, 5 },
                                { 1, 2, 3, 4, 5 },
                                { 1, 2, 3, 4, 5 },
                                { 100, 2, 3, 4, 5 } };

            Console.Write( "Minimum odd cost is " +
                          find_min_odd_cost(given, m, n));
    }

}

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Minimum
// odd cost path in a matrix
$M = 100; $N = 100;

// Function to find the minimum cost
function find_min_odd_cost($given, $m, $n)
{
    global $M, $N;

    $floor1[$M][$N] = array(array(0),
                            array(0));
    $min_odd_cost = 0;

    for ($j = 0; $j < $n; $j++)
        $floor1[0][$j] = $given[0][$j];

    for ($i = 1; $i < $m; $i++)
        for ($j = 0; $j < $n; $j++)
        {

            // leftmost element
            if ($j == 0)
            {
                $floor1[$i][$j] = $given[$i][$j];
                $floor1[$i][$j] += min($floor1[$i - 1][$j],
                                       $floor1[$i - 1][$j + 1]);
            }

            // rightmost element
            else if ($j == $n - 1)
            {
                $floor1[$i][$j] = $given[$i][$j];
                $floor1[$i][$j] += min($floor1[$i - 1][$j],
                                        $floor1[$i - 1][$j - 1]);
            }

            // Any element except leftmost and rightmost
            // element of a row is reachable from direct
            // upper or left upper or right upper row's block
            else
            {

                // Counting the minimum cost
                $temp = min($floor1[$i - 1][$j],
                            $floor1[$i - 1][$j - 1]);
                $temp = min($temp, $floor1[$i - 1][$j + 1]);
                $floor1[$i][$j] = $given[$i][$j] + $temp;
            }
        }

    $min_odd_cost = PHP_INT_MAX;

    // Find the minimum cost
    for ($j = 0; $j < $n; $j++)
    {
        if ($floor1[$n - 1][$j] % 2 == 1)
        {
            if ($min_odd_cost > $floor1[$n - 1][$j])
                $min_odd_cost = $floor1[$n - 1][$j];
        }
    }

    if ($min_odd_cost == PHP_INT_MIN)
        return -1;

    return $min_odd_cost;
}

// Driver code
$m = 5; $n = 5;
$given = array(array(1, 2, 3, 4, 6),
               array(1, 2, 3, 4, 5),
               array(1, 2, 3, 4, 5),
               array(1, 2, 3, 4, 5),
               array(100, 2, 3, 4, 5));

echo "Minimum odd cost is " .
      find_min_odd_cost($given, $m, $n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to find minimum odd
// cost path in a matrix

    let M = 100 ;
    let N = 100 ;

    // Function to find the minimum cost
    function find_min_odd_cost(given,m,n)
    {
        let floor = new Array(M);
        for(let i=0;i<M;i++)
        {
            floor[i]=new Array(N);
            for(let j=0;j<N;j++)
            {
                floor[i][j]=0;
            }
        }
        let min_odd_cost = 0;
        let i, j, temp;

        for (j = 0; j < n; j++)
            floor[0][j] = given[0][j];

        for (i = 1; i < m; i++)
            for (j = 0; j < n; j++) {

                // leftmost element
                if (j == 0) {
                    floor[i][j] = given[i][j];
                    floor[i][j] += Math.min(floor[i - 1][j],
                                            floor[i - 1][j + 1]);
                }

                // rightmost element
                else if (j == n - 1) {
                    floor[i][j] = given[i][j];
                    floor[i][j] += Math.min(floor[i - 1][j],
                                            floor[i - 1][j - 1]);
                }

                // Any element except leftmost and rightmost element of a row
                // is reachable from direct upper or left upper or right upper
                // row's block
                else {

                    // Counting the minimum cost
                    temp = Math.min(floor[i - 1][j],
                                    floor[i - 1][j - 1]);
                    temp = Math.min(temp, floor[i - 1][j + 1]);
                    floor[i][j] = given[i][j] + temp;
                }
            }

        min_odd_cost = Number.MAX_VALUE;

        // Find the minimum cost
        for (j = 0; j < n; j++) {
            if (floor[n - 1][j] % 2 == 1) {
                if (min_odd_cost > floor[n - 1][j])
                    min_odd_cost = floor[n - 1][j];
            }
        }

        if (min_odd_cost == Number.MIN_VALUE)
            return -1;

        return min_odd_cost;
    }

    // Driver code
    let m = 5, n = 5;
    let given = [[ 1, 2, 3, 4, 6 ],
         [ 1, 2, 3, 4, 5 ],
         [ 1, 2, 3, 4, 5 ],
         [ 1, 2, 3, 4, 5 ],
         [ 100, 2, 3, 4, 5 ]];

    document.write( "Minimum odd cost is " + find_min_odd_cost(given, m, n));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Minimum odd cost is 11
```
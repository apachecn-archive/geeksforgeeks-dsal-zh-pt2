# 给定矩阵的任何子矩阵的最大可能轨迹

> 原文:[https://www . geeksforgeeks . org/给定矩阵的任何子矩阵的最大可能跟踪数/](https://www.geeksforgeeks.org/maximum-trace-possible-for-any-sub-matrix-of-the-given-matrix/)

给定一个 **N x N** 矩阵 **mat[][]** ，任务是为给定矩阵的任何子矩阵找到最大可能的迹。
**例:**

> **输入:** mat[][] = {
> {10，2，5}，
> {6，10，4}，
> {2，7，-10}}
> **输出:** 20
> {{10，2}，
> {6，10}}
> 为最大迹子矩阵。
> **输入:** mat[][] = {
> {1，2，5}，
> {6，3，4}，
> {2，7，1}}
> **输出:** 13

**方法:**一种有效的方法是从矩阵的每个元素中取沿对角线的和，并更新最大和，因为任何正方形矩阵的迹都是其主对角线上元素的和。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 3

// Function to return the maximum trace possible
// for a sub-matrix of the given matrix
int MaxTraceSub(int mat[][N])
{
    int max_trace = 0;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            int r = i, s = j, trace = 0;

            // Calculate the trace for each of
            // the sub-matrix with top left corner
            // at cell (r, s)
            while (r < N && s < N) {
                trace += mat[r][s];
                r++;
                s++;

                // Update the maximum trace
                max_trace = max(trace, max_trace);
            }
        }
    }

    // Return the maximum trace
    return max_trace;
}

// Driver code
int main()
{
    int mat[N][N] = { { 10, 2, 5 },
                      { 6, 10, 4 },
                      { 2, 7, -10 } };
    cout << MaxTraceSub(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

static int N = 3;

// Function to return the maximum trace possible
// for a sub-matrix of the given matrix
static int MaxTraceSub(int mat[][])
{
    int max_trace = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            int r = i, s = j, trace = 0;

            // Calculate the trace for each of
            // the sub-matrix with top left corner
            // at cell (r, s)
            while (r < N && s < N)
            {
                trace += mat[r][s];
                r++;
                s++;

                // Update the maximum trace
                max_trace = Math.max(trace, max_trace);
            }
        }
    }

    // Return the maximum trace
    return max_trace;
}

// Driver code
public static void main(String[] args)
{
        int mat[][] = { { 10, 2, 5 },
                    { 6, 10, 4 },
                    { 2, 7, -10 } };
    System.out.println(MaxTraceSub(mat));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
N = 3

# Function to return the maximum trace possible
# for a sub-matrix of the given matrix
def MaxTraceSub(mat):
    max_trace = 0
    for i in range(N):
        for j in range(N):
            r = i
            s = j
            trace = 0

            # Calculate the trace for each of
            # the sub-matrix with top left corner
            # at cell (r, s)
            while (r < N and s < N):
                trace += mat[r]
                r += 1
                s += 1

                # Update the maximum trace
                max_trace = max(trace, max_trace)

    # Return the maximum trace
    return max_trace

# Driver code
if __name__ == '__main__':
    mat = [[10, 2, 5],[6, 10, 4],[2, 7, -10]]
    print(MaxTraceSub(mat))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

static int N = 3;

// Function to return the maximum trace possible
// for a sub-matrix of the given matrix
static int MaxTraceSub(int [][]mat)
{
    int max_trace = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            int r = i, s = j, trace = 0;

            // Calculate the trace for each of
            // the sub-matrix with top left corner
            // at cell (r, s)
            while (r < N && s < N)
            {
                trace += mat[r][s];
                r++;
                s++;

                // Update the maximum trace
                max_trace = Math.Max(trace, max_trace);
            }
        }
    }

    // Return the maximum trace
    return max_trace;
}

// Driver code
public static void Main()
{
    int[][] mat = new int[][]{new int[]{ 10, 2, 5 },
                new int[]{ 6, 10, 4 },
                new int[]{ 2, 7, -10 } };
    Console.WriteLine(MaxTraceSub(mat));
}
}

// This code has been contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$N = 3;

// Function to return the maximum
// trace possible for a sub-matrix
// of the given matrix
function MaxTraceSub($mat)
{
    global $N;
    $max_trace = 0;
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $N; $j++)
        {
            $r = $i;
            $s = $j;
            $trace = 0;

            // Calculate the trace for
            // each of the sub-matrix
            // with top left corner at
            // cell (r, s)
            while ($r < $N && $s < $N)
            {
                $trace += $mat[$r][$s];
                $r++;
                $s++;

                // Update the maximum trace
                $max_trace = max($trace,
                                 $max_trace);
            }
        }
    }

    // Return the maximum trace
    return $max_trace;
}

// Driver code
$mat = array(array( 10, 2, 5 ),
             array( 6, 10, 4 ),
             array( 2, 7, -10 ));
print(MaxTraceSub($mat));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for the above approach   
var N = 3;

    // Function to return the maximum trace possible
    // for a sub-matrix of the given matrix
    function MaxTraceSub(mat)
    {
        var max_trace = 0;
        for (i = 0; i < N; i++) {
            for (j = 0; j < N; j++) {
                var r = i, s = j, trace = 0;

                // Calculate the trace for each of
                // the sub-matrix with top left corner
                // at cell (r, s)
                while (r < N && s < N) {
                    trace += mat[r][s];
                    r++;
                    s++;

                    // Update the maximum trace
                    max_trace = Math.max(trace, max_trace);
                }
            }
        }

        // Return the maximum trace
        return max_trace;
    }

    // Driver code

        var mat = [
        [ 10, 2, 5 ],
        [ 6, 10, 4 ],
        [ 2, 7, -10 ] ];
        document.write(MaxTraceSub(mat));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
20
```
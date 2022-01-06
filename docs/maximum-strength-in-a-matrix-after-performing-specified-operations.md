# 执行指定操作后矩阵中的最大强度

> 原文:[https://www . geeksforgeeks . org/执行指定操作后矩阵中的最大强度/](https://www.geeksforgeeks.org/maximum-strength-in-a-matrix-after-performing-specified-operations/)

给定包含{ **0** 、 **1** 、 **#** }的 **N * M** 矩阵。任务是根据以下规则找到强度的最大值:

1.  初始强度为**零**。
2.  如果遇到 **0** ，强度降低 2。
3.  如果遇到 **1** ，强度增加 5。
4.  如果你遇到一个 **#** ，跳到新一排的开始，不要失去任何力量。

**注意:**需要从左到右自上而下遍历矩阵的每一行。
**例:**

```
Input:
      {{1, 0, 1, 0},
       {0, #, 0, 0},
       {1, 1, 0, 0},
       {0, #, 1, 0}}

Output: 14
Explanation:
Here you starts with strength S = 0.

For the first row {1, 0, 1, 0}:
After {1} -> S = S + 5 = 5
After {0} -> S = S - 2 = 3
After {1} -> S = S + 5 = 8
After {0} -> S = S - 2 = 6

For the Second row {0, #, 0, 0}:
After {0} -> S = S - 2 = 4
After {#} -> Jump to next row.

For the Third row {1, 1, 0, 0}:
After {1} -> S = S + 5 = 9
After {1} -> S = S + 5 = 14
After {0} -> S = S - 2 = 12
After {0} -> S = S - 2 = 10

For the Fourth row {0, #, 1, 0}:
After {0} -> S = S - 2 = 8
After {#} -> Jump to next row.

So, The maximum value of S is 14 
```

**进场:**

1.  [从 i = [0，N]，j = [0，M]遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/) mat[][]，并检查:

```
If mat[i][j] = 0 then, S = S - 2.
If mat[i][j] = 1 then, S = S + 5.
If mat[i][j] = # then, jump to the next row.
```

2.  每一步都存储到现在的最大力量值，并在最后打印力量值。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function return the Maximum
// value of the strength
void MaxStrength(char mat[100][100],
                 int n, int m)
{
    int S = 0;
    int ans = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            char Curr = mat[i][j];

            // If current element
            // is 1
            if (Curr == '1') {
                S += 5;
            }
            // If current element
            // is 0
            if (Curr == '0') {
                S -= 2;
            }
            // If current element
            // is '#'
            if (Curr == '#') {
                break;
            }

            // Store the value of
            // maximum strength
            // till now
            ans = max(ans, S);
        }
    }

    cout << ans;

    return;
}

// Driver code
int main()
{
    int N = 4;
    int M = 4;
    char Mat[100][100]{ { '1', '0', '1', '0' },
                        { '0', '#', '0', '0' },
                        { '1', '1', '0', '0' },
                        { '0', '#', '1', '0' } };

    MaxStrength(Mat, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function return the maximum
// value of the strength
static void MaxStrength(char[][] mat,
                        int n, int m)
{
    int S = 0;
    int ans = 0;

    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j < m; j++)
       {
          char Curr = mat[i][j];

          // If current element
          // is 1
          if (Curr == '1')
          {
              S += 5;
          }

          // If current element
          // is 0
          if (Curr == '0')
          {
              S -= 2;
          }

          // If current element
          // is '#'
          if (Curr == '#')
          {
              break;
          }

          // Store the value of
          // maximum strength
          // till now
          ans = Math.max(ans, S);
       }
    }
    System.out.println(ans);
    return;
}

// Driver code
public static void main (String[] args)
{
    int N = 4;
    int M = 4;
    char[][] Mat = { { '1', '0', '1', '0' },
                     { '0', '#', '0', '0' },
                     { '1', '1', '0', '0' },
                     { '0', '#', '1', '0' } };

    MaxStrength(Mat, N, M);
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# python3 program for the above approach

# Function return the Maximum
# value of the strength
def MaxStrength(mat, n, m):
    S = 0
    ans = 0

    for i in range(n):
        for j in range(m):
            Curr = mat[i][j]

            # If current element
            # is 1
            if (Curr == '1'):
                S += 5

            # If current element
            # is 0
            if (Curr == '0'):
                S -= 2

            # If current element
            # is '#'
            if (Curr == '#'):
                break

            # Store the value of
            # maximum strength
            # till now
            ans = max(ans, S)

    print(ans)
    return

# Driver code
if __name__ == '__main__':

    N = 4;
    M = 4;
    Mat = [ ['1', '0', '1', '0'],
            ['0', '#', '0', '0'],
            ['1', '1', '0', '0'],
            ['0', '#', '1', '0'] ]

    MaxStrength(Mat, N, M)

# This code is contributed by Samarth
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function return the maximum
// value of the strength
static void MaxStrength(char[,] mat,
                        int n, int m)
{
    int S = 0;
    int ans = 0;

    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j < m; j++)
       {
          char Curr = mat[i, j];

          // If current element
          // is 1
          if (Curr == '1')
          {
              S += 5;
          }

          // If current element
          // is 0
          if (Curr == '0')
          {
              S -= 2;
          }

          // If current element
          // is '#'
          if (Curr == '#')
          {
              break;
          }

          // Store the value of
          // maximum strength
          // till now
          ans = Math.Max(ans, S);
       }
    }
    Console.WriteLine(ans);
    return;
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;
    int M = 4;
    char[,] Mat = { { '1', '0', '1', '0' },
                    { '0', '#', '0', '0' },
                    { '1', '1', '0', '0' },
                    { '0', '#', '1', '0' } };

    MaxStrength(Mat, N, M);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function return the Maximum
// value of the strength
function MaxStrength(mat, n, m)
{
    var S = 0;
    var ans = 0;

    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {

            var Curr = mat[i][j];

            // If current element
            // is 1
            if (Curr == '1') {
                S += 5;
            }
            // If current element
            // is 0
            if (Curr == '0') {
                S -= 2;
            }
            // If current element
            // is '#'
            if (Curr == '#') {
                break;
            }

            // Store the value of
            // maximum strength
            // till now
            ans = Math.max(ans, S);
        }
    }

    document.write( ans);

    return;
}

// Driver code
var N = 4;
var M = 4;
var Mat = [ [ '1', '0', '1', '0' ],
                    [ '0', '#', '0', '0' ],
                    [ '1', '1', '0', '0' ],
                    [ '0', '#', '1', '0' ] ];
MaxStrength(Mat, N, M);

// This code is contributed by noob2000.

</script>
```

**Output:** 

```
14
```
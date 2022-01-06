# 矩阵中的最大和路径

> 原文:[https://www.geeksforgeeks.org/maximum-sum-path-in-a-matrix/](https://www.geeksforgeeks.org/maximum-sum-path-in-a-matrix/)

给定一个 **n*m** 矩阵，任务是找出从单元格(0，0)到单元格(n-1，m-1)的单元格元素的最大和。
然而，允许的移动是向右、向下或对角向右，即从位置(I，j)下一个移动可以是 **(i+1，j)** ，或者， **(i，j+1)** ，或者 **(i+1，j+1)** 。找出满足允许移动的元素的最大和。
**示例:**

```
Input:
mat[][] = {{100, -350, -200},
           {-100, -300, 700}}
Output: 500
Explanation: 
Path followed is 100 -> -300 -> 700

Input:
mat[][] = {{500, 100, 230},
           {1000, 300, 100},
           {200, 1000, 200}}
Output: 3000
Explanation:
Path followed is 500 -> 1000 -> 300 -> 1000 -> 200
```

**方法:**采用动态规划递归求解上述问题。

1.  在矩阵的开头(0，0)分配一个位置。
2.  从当前位置检查每个下一个允许的位置，并选择具有最大和的路径。
3.  注意矩阵的边界，也就是说，如果位置到达最后一行或最后一列，那么唯一可能的选择就是向右或向下。
4.  使用[地图](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储所有访问位置的轨迹，在访问任何(I，j)之前，检查该位置之前是否被访问过。
5.  更新每次递归调用返回的所有可能路径的最大值。
6.  一直走到位置到达目的单元格，即(n-1.m-1)。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define N 100

// No of rows and columns
int n, m;

// Declaring the matrix of maximum
// 100 rows and 100 columns
int a[N][N];

// Variable visited is used to keep
// track of all the visited positions
// Variable dp is used to store
// maximum sum till current position
vector<vector<int> > dp(N, vector<int>(N)),
    visited(N, vector<int>(N));

// For storing current sum
int current_sum = 0;

// For continuous update of
// maximum sum required
int total_sum = 0;

// Function to Input the matrix of size n*m
void inputMatrix()
{
    n = 3;
    m = 3;
    a[0][0] = 500;
    a[0][1] = 100;
    a[0][2] = 230;
    a[1][0] = 1000;
    a[1][1] = 300;
    a[1][2] = 100;
    a[2][0] = 200;
    a[2][1] = 1000;
    a[2][2] = 200;
}

// Function to calculate maximum sum of path
int maximum_sum_path(int i, int j)
{
    // Checking boundary condition
    if (i == n - 1 && j == m - 1)
        return a[i][j];

    // Checking whether or not (i, j) is visited
    if (visited[i][j])
        return dp[i][j];

    // Marking (i, j) is visited
    visited[i][j] = 1;

    // Updating the maximum sum till
    // the current position in the dp
    int& total_sum = dp[i][j];

    // Checking whether the position hasn't
    // visited the last row or the last column.
    // Making recursive call for all the possible
    // moves from the current cell and then adding the
    // maximum returned by the calls and updating it.
    if (i < n - 1 & j < m - 1) {
        int current_sum = max(maximum_sum_path(i, j + 1),
                              max(
                                  maximum_sum_path(i + 1, j + 1),
                                  maximum_sum_path(i + 1, j)));
        total_sum = a[i][j] + current_sum;
    }

    // Checking whether
    // position has reached last row
    else if (i == n - 1)
        total_sum = a[i][j]
                    + maximum_sum_path(i, j + 1);

    // If the position is in the last column
    else
        total_sum = a[i][j]
                    + maximum_sum_path(i + 1, j);

    // Returning the updated maximum value
    return dp[i][j] = total_sum;
}

// Driver Code
int main()
{
    inputMatrix();

    // Calling the implemented function
    int maximum_sum = maximum_sum_path(0, 0);

    cout << maximum_sum;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

static final int N = 100;

// No of rows and columns
static int n, m;

// Declaring the matrix of maximum
// 100 rows and 100 columns
static int a[][] = new int[N][N];

// Variable visited is used to keep
// track of all the visited positions
// Variable dp is used to store
// maximum sum till current position
static int dp[][] = new int[N][N];
static int visited[][] = new int[N][N];

// For storing current sum
static int current_sum = 0;

// For continuous update of
// maximum sum required
static int total_sum = 0;

// Function to Input the matrix
// of size n*m
static void inputMatrix()
{
    n = 3;
    m = 3;
    a[0][0] = 500;
    a[0][1] = 100;
    a[0][2] = 230;
    a[1][0] = 1000;
    a[1][1] = 300;
    a[1][2] = 100;
    a[2][0] = 200;
    a[2][1] = 1000;
    a[2][2] = 200;
}

// Function to calculate maximum sum of path
static int maximum_sum_path(int i, int j)
{

    // Checking boundary condition
    if (i == n - 1 && j == m - 1)
        return a[i][j];

    // Checking whether or not
    // (i, j) is visited
    if (visited[i][j] != 0)
        return dp[i][j];

    // Marking (i, j) is visited
    visited[i][j] = 1;

    int total_sum = 0;

    // Checking whether the position hasn't
    // visited the last row or the last column.
    // Making recursive call for all the possible
    // moves from the current cell and then adding the
    // maximum returned by the calls and updating it.
    if (i < n - 1 & j < m - 1)
    {
        int current_sum = Math.max(
                          maximum_sum_path(i, j + 1),
                          Math.max(
                          maximum_sum_path(i + 1, j + 1),
                          maximum_sum_path(i + 1, j)));
        total_sum = a[i][j] + current_sum;
    }

    // Checking whether position
    // has reached last row
    else if (i == n - 1)
        total_sum = a[i][j] +
                    maximum_sum_path(i, j + 1);

    // If the position is in the last column
    else
        total_sum = a[i][j] +
                    maximum_sum_path(i + 1, j);

    // Updating the maximum sum till
    // the current position in the dp
    dp[i][j] = total_sum;

    // Returning the updated maximum value
    return total_sum;
}

// Driver Code
public static void main(String[] args)
{
    inputMatrix();

    // Calling the implemented function
    int maximum_sum = maximum_sum_path(0, 0);

    System.out.println(maximum_sum);
}
}

// This code is contributed by jrishabh99
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

static readonly int N = 100;

// No of rows and columns
static int n, m;

// Declaring the matrix of maximum
// 100 rows and 100 columns
static int[,]a = new int[N, N];

// Variable visited is used to keep
// track of all the visited positions
// Variable dp is used to store
// maximum sum till current position
static int [,]dp = new int[N, N];
static int [,]visited = new int[N, N];

// For storing current sum
static int current_sum = 0;

// For continuous update of
// maximum sum required
static int total_sum = 0;

// Function to Input the matrix
// of size n*m
static void inputMatrix()
{
  n = 3;
  m = 3;
  a[0, 0] = 500;
  a[0, 1] = 100;
  a[0, 2] = 230;
  a[1, 0] = 1000;
  a[1, 1] = 300;
  a[1, 2] = 100;
  a[2, 0] = 200;
  a[2, 1] = 1000;
  a[2, 2] = 200;
}

// Function to calculate maximum
// sum of path
static int maximum_sum_path(int i,
                            int j)
{
  // Checking boundary condition
  if (i == n - 1 && j == m - 1)
    return a[i, j];

  // Checking whether or not
  // (i, j) is visited
  if (visited[i, j] != 0)
    return dp[i, j];

  // Marking (i, j) is visited
  visited[i, j] = 1;

  int total_sum = 0;

  // Checking whether the position
  // hasn't visited the last row
  // or the last column.
  // Making recursive call for all
  // the possible moves from the
  // current cell and then adding the
  // maximum returned by the calls
  // and updating it.
  if (i < n - 1 & j < m - 1)
  {
    int current_sum = Math.Max(maximum_sum_path(i, j + 1),
                      Math.Max(maximum_sum_path(i + 1,
                                                j + 1),
                               maximum_sum_path(i + 1, j)));
    total_sum = a[i, j] + current_sum;
  }

  // Checking whether position
  // has reached last row
  else if (i == n - 1)
    total_sum = a[i, j] +
                maximum_sum_path(i, j + 1);

  // If the position is
  // in the last column
  else
    total_sum = a[i, j] +
                maximum_sum_path(i + 1, j);

  // Updating the maximum
  // sum till the current
  // position in the dp
  dp[i, j] = total_sum;

  // Returning the updated
  // maximum value
  return total_sum;
}

// Driver Code
public static void Main(String[] args)
{
  inputMatrix();

  // Calling the implemented function
  int maximum_sum = maximum_sum_path(0, 0);

  Console.WriteLine(maximum_sum);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    let N = 100;

    // No of rows and columns
    let n, m;

    // Declaring the matrix of maximum
    // 100 rows and 100 columns
    let a = new Array(N);

    // Variable visited is used to keep
    // track of all the visited positions
    // Variable dp is used to store
    // maximum sum till current position
    let dp = new Array(N);
    let visited = new Array(N);
    for(let i = 0; i < N; i++)
    {
        a[i] = new Array(N);
        dp[i] = new Array(N);
        visited[i] = new Array(N);
        for(let j = 0; j < N; j++)
        {
            a[i][j] = 0;
            dp[i][j] = 0;
            visited[i][j] = 0;
        }
    }

    // For storing current sum
    let current_sum = 0;

    // For continuous update of
    // maximum sum required
    let total_sum = 0;

    // Function to Input the matrix
    // of size n*m
    function inputMatrix()
    {
        n = 3;
        m = 3;
        a[0][0] = 500;
        a[0][1] = 100;
        a[0][2] = 230;
        a[1][0] = 1000;
        a[1][1] = 300;
        a[1][2] = 100;
        a[2][0] = 200;
        a[2][1] = 1000;
        a[2][2] = 200;
    }

    // Function to calculate maximum sum of path
    function maximum_sum_path(i, j)
    {

        // Checking boundary condition
        if (i == n - 1 && j == m - 1)
            return a[i][j];

        // Checking whether or not
        // (i, j) is visited
        if (visited[i][j] != 0)
            return dp[i][j];

        // Marking (i, j) is visited
        visited[i][j] = 1;

        let total_sum = 0;

        // Checking whether the position hasn't
        // visited the last row or the last column.
        // Making recursive call for all the possible
        // moves from the current cell and then adding the
        // maximum returned by the calls and updating it.
        if (i < n - 1 & j < m - 1)
        {
            let current_sum = Math.max(
                              maximum_sum_path(i, j + 1),
                              Math.max(
                              maximum_sum_path(i + 1, j + 1),
                              maximum_sum_path(i + 1, j)));
            total_sum = a[i][j] + current_sum;
        }

        // Checking whether position
        // has reached last row
        else if (i == n - 1)
            total_sum = a[i][j] + maximum_sum_path(i, j + 1);

        // If the position is in the last column
        else
            total_sum = a[i][j] + maximum_sum_path(i + 1, j);

        // Updating the maximum sum till
        // the current position in the dp
        dp[i][j] = total_sum;

        // Returning the updated maximum value
        return total_sum;
    }

    inputMatrix();

    // Calling the implemented function
    let maximum_sum = maximum_sum_path(0, 0);

    document.write(maximum_sum);

// This code is contributed by suresh07.
</script>
```

## 蟒蛇 3

```
N=100

# No of rows and columns
n, m=-1,-1

# Declaring the matrix of maximum
# 100 rows and 100 columns
a=[[-1]*N for _ in range(N)]

# Variable visited is used to keep
# track of all the visited positions
# Variable dp is used to store
# maximum sum till current position
dp,visited=[[-1]*N for _ in range(N)],[[False]*N for _ in range(N)]

# For storing current sum
current_sum = 0

# For continuous update of
# maximum sum required
total_sum = 0

# Function to Input the matrix of size n*m
def inputMatrix():
    global n, m
    n = 3
    m = 3
    a[0][0] = 500
    a[0][1] = 100
    a[0][2] = 230
    a[1][0] = 1000
    a[1][1] = 300
    a[1][2] = 100
    a[2][0] = 200
    a[2][1] = 1000
    a[2][2] = 200

# Function to calculate maximum sum of path
def maximum_sum_path(i, j):
    global total_sum
    # Checking boundary condition
    if (i == n - 1 and j == m - 1):
        return a[i][j]

    # Checking whether or not (i, j) is visited
    if (visited[i][j]):
        return dp[i][j]

    # Marking (i, j) is visited
    visited[i][j] = True

    # Updating the maximum sum till
    # the current position in the dp
    total_sum = dp[i][j]

    # Checking whether the position hasn't
    # visited the last row or the last column.
    # Making recursive call for all the possible
    # moves from the current cell and then adding the
    # maximum returned by the calls and updating it.
    if (i < n - 1 and j < m - 1) :
        current_sum = max(maximum_sum_path(i, j + 1),
                              max(
                                  maximum_sum_path(i + 1, j + 1),
                                  maximum_sum_path(i + 1, j)))
        total_sum = a[i][j] + current_sum

    # Checking whether
    # position has reached last row
    elif (i == n - 1):
        total_sum = a[i][j] + maximum_sum_path(i, j + 1)

    # If the position is in the last column
    else:
        total_sum = a[i][j] + maximum_sum_path(i + 1, j)

    # Returning the updated maximum value
    dp[i][j] = total_sum
    return total_sum

# Driver Code
if __name__ == '__main__':
    inputMatrix()

    # Calling the implemented function
    maximum_sum = maximum_sum_path(0, 0)

    print(maximum_sum)
```

**Output**

```
3000
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N*M)
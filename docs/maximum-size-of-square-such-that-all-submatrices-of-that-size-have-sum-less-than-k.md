# 正方形的最大尺寸，使得该尺寸的所有子矩阵的和小于 K

> 原文:[https://www . geeksforgeeks . org/最大平方尺寸，以至于该尺寸的所有子矩阵的总和都小于 k/](https://www.geeksforgeeks.org/maximum-size-of-square-such-that-all-submatrices-of-that-size-have-sum-less-than-k/)

给定一个整数**N×M**矩阵和一个整数 **K** ，任务是找到最大正方形子矩阵**(S×S)**的大小，使得该大小的给定矩阵的所有正方形子矩阵**的和小于 **K** 。**

**例:**

```
Input: K = 30 
mat[N][M] = {{1, 2, 3, 4, 6}, 
             {5, 3, 8, 1, 2}, 
             {4, 6, 7, 5, 5}, 
             {2, 4, 8, 9, 4} }; 
Output: 2
Explanation:
All Sub-matrices of size 2 x 2 
have sum less than 30

Input : K = 100 
mat[N][M] = { { 1, 2, 3, 4 },
              { 5, 6, 7, 8 }, 
              { 9, 10, 11, 12 }, 
              { 13, 14, 15, 16 } };
Output: 3
Explanation:
All Sub-matrices of size 3 x 3 
have sum less than 100
```

**朴素方法**基本解决方案是选择子矩阵的大小 **S** ，找到该大小的所有子矩阵，并检查所有子矩阵的和是否小于给定的和，而这可以通过使用[这种](https://www.geeksforgeeks.org/submatrix-sum-queries/)方法计算矩阵的和来改进。因此，任务将是选择可能的最大尺寸以及每个可能的子矩阵的开始和结束位置。因此总的时间复杂度为 0(N<sup>3</sup>)。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum size square submatrix
// such that their sum is less than K

#include <bits/stdc++.h>

using namespace std;

// Size of matrix
#define N 4
#define M 5

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
void preProcess(int mat[N][M],
                int aux[N][M])
{
    // Loop to copy the first row
    // of the matrix into the aux matrix
    for (int i = 0; i < M; i++)
        aux[0][i] = mat[0][i];

    // Computing the sum column-wise
    for (int i = 1; i < N; i++)
        for (int j = 0; j < M; j++)
            aux[i][j] = mat[i][j] +
                      aux[i - 1][j];

    // Computing row wise sum
    for (int i = 0; i < N; i++)
        for (int j = 1; j < M; j++)
            aux[i][j] += aux[i][j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
int sumQuery(int aux[N][M], int tli,
          int tlj, int rbi, int rbj)
{
    // Overall sum from the top to
    // right corner of matrix
    int res = aux[rbi][rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1][rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi][tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res +
           aux[tli - 1][tlj - 1];

    return res;
}

// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
int maximumSquareSize(int mat[N][M], int K)
{
    int aux[N][M];
    preProcess(mat, aux);

    // Loop to choose the size of matrix
    for (int i = min(N, M); i >= 1; i--) {

        bool satisfies = true;

        // Loop to find the sum of the
        // matrix of every possible submatrix
        for (int x = 0; x < N; x++) {
            for (int y = 0; y < M; y++) {
                if (x + i - 1 <= N - 1 &&
                     y + i - 1 <= M - 1) {
                    if (sumQuery(aux, x, y,
                   x + i - 1, y + i - 1) > K)
                        satisfies = false;
                }
            }
        }
        if (satisfies == true)
            return (i);
    }
    return 0;
}

// Driver Code
int main()
{
    int K = 30;
    int mat[N][M] = { { 1, 2, 3, 4, 6 },
                    { 5, 3, 8, 1, 2 },
                    { 4, 6, 7, 5, 5 },
                    { 2, 4, 8, 9, 4 } };

    cout << maximumSquareSize(mat, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum size square submatrix
// such that their sum is less than K
class GFG{

// Size of matrix
static final int N = 4;
static final int M = 5;

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
static void preProcess(int [][]mat,
                int [][]aux)
{
    // Loop to copy the first row
    // of the matrix into the aux matrix
    for (int i = 0; i < M; i++)
        aux[0][i] = mat[0][i];

    // Computing the sum column-wise
    for (int i = 1; i < N; i++)
        for (int j = 0; j < M; j++)
            aux[i][j] = mat[i][j] +
                      aux[i - 1][j];

    // Computing row wise sum
    for (int i = 0; i < N; i++)
        for (int j = 1; j < M; j++)
            aux[i][j] += aux[i][j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
static int sumQuery(int [][]aux, int tli,
          int tlj, int rbi, int rbj)
{
    // Overall sum from the top to
    // right corner of matrix
    int res = aux[rbi][rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1][rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi][tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res +
           aux[tli - 1][tlj - 1];

    return res;
}

// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
static int maximumSquareSize(int [][]mat, int K)
{
    int [][]aux = new int[N][M];
    preProcess(mat, aux);

    // Loop to choose the size of matrix
    for (int i = Math.min(N, M); i >= 1; i--) {

        boolean satisfies = true;

        // Loop to find the sum of the
        // matrix of every possible submatrix
        for (int x = 0; x < N; x++) {
            for (int y = 0; y < M; y++) {
                if (x + i - 1 <= N - 1 &&
                     y + i - 1 <= M - 1) {
                    if (sumQuery(aux, x, y,
                   x + i - 1, y + i - 1) > K)
                        satisfies = false;
                }
            }
        }
        if (satisfies == true)
            return (i);
    }
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int K = 30;
    int mat[][] = { { 1, 2, 3, 4, 6 },
                    { 5, 3, 8, 1, 2 },
                    { 4, 6, 7, 5, 5 },
                    { 2, 4, 8, 9, 4 } };

    System.out.print(maximumSquareSize(mat, K));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum size square submatrix
# such that their sum is less than K

# Size of matrix
N = 4
M = 5

# Function to preprocess the matrix
# for computing the sum of every
# possible matrix of the given size
def preProcess(mat, aux):

    # Loop to copy the first row
    # of the matrix into the aux matrix
    for i in range (M):
        aux[0][i] = mat[0][i]

    # Computing the sum column-wise
    for i in range (1, N):
        for j in range (M):
            aux[i][j] = (mat[i][j] +
                         aux[i - 1][j])

    # Computing row wise sum
    for i in range (N):
        for j in range (1, M):
            aux[i][j] += aux[i][j - 1]

# Function to find the sum of a
# submatrix with the given indices
def sumQuery(aux, tli, tlj, rbi, rbj):

    # Overall sum from the top to
    # right corner of matrix
    res = aux[rbi][rbj]

    # Removing the sum from the top
    # corer of the matrix
    if (tli > 0):
        res = res - aux[tli - 1][rbj]

    # Remove the overlapping sum
    if (tlj > 0):
        res = res - aux[rbi][tlj - 1]

    # Add the sum of top corner
    # which is subtracted twice
    if (tli > 0 and tlj > 0):
        res = (res +
        aux[tli - 1][tlj - 1])

    return res

# Function to find the maximum
# square size possible with the
# such that every submatrix have
# sum less than the given sum
def maximumSquareSize(mat, K):

    aux = [[0 for x in range (M)]
              for y in range (N)]
    preProcess(mat, aux)

    # Loop to choose the size of matrix
    for i in range (min(N, M), 0, -1):

        satisfies = True

        # Loop to find the sum of the
        # matrix of every possible submatrix
        for x in range (N):
            for y in range (M) :
                if (x + i - 1 <= N - 1 and
                    y + i - 1 <= M - 1):
                    if (sumQuery(aux, x, y,
                                 x + i - 1,
                                 y + i - 1) > K):
                        satisfies = False

        if (satisfies == True):
            return (i)
    return 0

# Driver Code
if __name__ == "__main__":

    K = 30
    mat = [[1, 2, 3, 4, 6],
            [5, 3, 8, 1, 2],
           [4, 6, 7, 5, 5],
           [2, 4, 8, 9, 4]]

    print( maximumSquareSize(mat, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation to find the
// maximum size square submatrix
// such that their sum is less than K
using System;

public class GFG{

// Size of matrix
static readonly int N = 4;
static readonly int M = 5;

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
static void preProcess(int [,]mat,
                int [,]aux)
{
    // Loop to copy the first row
    // of the matrix into the aux matrix
    for (int i = 0; i < M; i++)
        aux[0,i] = mat[0,i];

    // Computing the sum column-wise
    for (int i = 1; i < N; i++)
        for (int j = 0; j < M; j++)
            aux[i,j] = mat[i,j] +
                      aux[i - 1,j];

    // Computing row wise sum
    for (int i = 0; i < N; i++)
        for (int j = 1; j < M; j++)
            aux[i,j] += aux[i,j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
static int sumQuery(int [,]aux, int tli,
          int tlj, int rbi, int rbj)
{
    // Overall sum from the top to
    // right corner of matrix
    int res = aux[rbi,rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1,rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi,tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res +
           aux[tli - 1,tlj - 1];

    return res;
}

// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
static int maximumSquareSize(int [,]mat, int K)
{
    int [,]aux = new int[N,M];
    preProcess(mat, aux);

    // Loop to choose the size of matrix
    for (int i = Math.Min(N, M); i >= 1; i--) {

        bool satisfies = true;

        // Loop to find the sum of the
        // matrix of every possible submatrix
        for (int x = 0; x < N; x++) {
            for (int y = 0; y < M; y++) {
                if (x + i - 1 <= N - 1 &&
                     y + i - 1 <= M - 1) {
                    if (sumQuery(aux, x, y,
                   x + i - 1, y + i - 1) > K)
                        satisfies = false;
                }
            }
        }
        if (satisfies == true)
            return (i);
    }
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int K = 30;
    int [,]mat = { { 1, 2, 3, 4, 6 },
                    { 5, 3, 8, 1, 2 },
                    { 4, 6, 7, 5, 5 },
                    { 2, 4, 8, 9, 4 } };

    Console.Write(maximumSquareSize(mat, K));
}
}

// This code contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// maximum size square submatrix
// such that their sum is less than K

// Size of matrix
let N = 4;
let M = 5;

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
function preProcess(mat,aux)
{
    // Loop to copy the first row
    // of the matrix into the aux matrix
    for (let i = 0; i < M; i++)
        aux[0][i] = mat[0][i];

    // Computing the sum column-wise
    for (let i = 1; i < N; i++)
        for (let j = 0; j < M; j++)
            aux[i][j] = mat[i][j] +
                      aux[i - 1][j];

    // Computing row wise sum
    for (let i = 0; i < N; i++)
        for (let j = 1; j < M; j++)
            aux[i][j] += aux[i][j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
function sumQuery(aux,tli,tlj,rbi,rbj)
{
    // Overall sum from the top to
    // right corner of matrix
    let res = aux[rbi][rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1][rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi][tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res +
           aux[tli - 1][tlj - 1];

    return res;
}

// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
function maximumSquareSize(mat,k)
{
    let aux = new Array(N);
    for(let i=0;i<N;i++)
    {
        aux[i]=new Array(M);
    }

    preProcess(mat, aux);

    // Loop to choose the size of matrix
    for (let i = Math.min(N, M); i >= 1; i--) {

        let satisfies = true;

        // Loop to find the sum of the
        // matrix of every possible submatrix
        for (let x = 0; x < N; x++) {
            for (let y = 0; y < M; y++) {
                if (x + i - 1 <= N - 1 &&
                     y + i - 1 <= M - 1) {
                    if (sumQuery(aux, x, y,
                   x + i - 1, y + i - 1) > K)
                        satisfies = false;
                }
            }
        }
        if (satisfies == true)
            return (i);
    }
    return 0;
}

// Driver Code
let mat = [[1, 2, 3, 4, 6],
            [5, 3, 8, 1, 2],
           [4, 6, 7, 5, 5],
           [2, 4, 8, 9, 4]];

let K = 30;
document.write(maximumSquareSize(mat, K));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```

*   **时间复杂度:** O(N <sup>3</sup> )
*   **辅助空间:** O(N <sup>2</sup> )

**有效方法:**关键观察是，如果边 s 的平方是满足条件的最大尺寸，那么所有小于它的尺寸都将满足条件。利用这一点，我们可以将每一步的搜索空间减少一半，这正是[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的想法。下面是方法步骤的图解:

*   **Search space:** The search space for this question will start from [1, min(N, M)]. In other words, the search space of method of bisection is defined as-

```
low = 1
high = min(N, M)
```

*   **Next search space:** Find the middle of of the search space in each iteration, and finally check whether the sum of all subarrays of this size is less than **k** . If the sum of all subarrays of this size is less than k, then the next possible search space will be in the middle right. Otherwise, the next possible search space will be on the left in the middle. That's not in the middle.
    *   **Case 1:** The sum of the sizes ***of all subarrays*** is less than **k** . And then-

```
if checkSubmatrix(mat, mid, K):
    low = mid + 1
```

*   **Case 2:** Condition When the sum of the sizes of all subarrays is greater than **k** . And then-

```
if not checkSubmatrix(mat, mid, K):
    high = mid - 1
```

下面是上述方法的实现:

## c++

```
// C++ implementation to find the
// maximum size square submatrix
// such that their sum is less than K

#include <bits/stdc++.h>

using namespace std;

// Size of matrix
#define N 4
#define M 5

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
void preProcess(int mat[N][M],
                     int aux[N][M])
{
    // Loop to copy the first row
    // of the matrix into the aux matrix
    for (int i = 0; i < M; i++)
        aux[0][i] = mat[0][i];

    // Computing the sum column-wise
    for (int i = 1; i < N; i++)
        for (int j = 0; j < M; j++)
            aux[i][j] = mat[i][j] +
                       aux[i - 1][j];

    // Computing row wise sum
    for (int i = 0; i < N; i++)
        for (int j = 1; j < M; j++)
            aux[i][j] += aux[i][j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
int sumQuery(int aux[N][M], int tli,
          int tlj, int rbi, int rbj)
{
    // Overall sum from the top to
    // right corner of matrix
    int res = aux[rbi][rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1][rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi][tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res + aux[tli - 1][tlj - 1];

    return res;
}

// Function to check whether square
// sub matrices of size mid satisfy
// the condition or not
bool check(int mid, int aux[N][M],
                           int K)
{

    bool satisfies = true;

    // Iterating throught all possible
    // submatrices of given size
    for (int x = 0; x < N; x++) {
        for (int y = 0; y < M; y++) {
            if (x + mid - 1 <= N - 1 &&
                  y + mid - 1 <= M - 1) {
                if (sumQuery(aux, x, y,
          x + mid - 1, y + mid - 1) > K)
                    satisfies = false;
            }
        }
    }
    return (satisfies == true);
}
// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
int maximumSquareSize(int mat[N][M],
                              int K)
{
    int aux[N][M];

    preProcess(mat, aux);

    // Search space
    int low = 1, high = min(N, M);
    int mid;

    // Binary search for size
    while (high - low > 1) {
        mid = (low + high) / 2;

        // Check if the mid satisfies
        // the given condition
        if (check(mid, aux, K)) {
            low = mid;
        }
        else
            high = mid;
    }
    if (check(high, aux, K))
        return high;
    return low;
}

// Driver Code
int main()
{
    int K = 30;
    int mat[N][M] = { { 1, 2, 3, 4, 6 },
                    { 5, 3, 8, 1, 2 },
                    { 4, 6, 7, 5, 5 },
                    { 2, 4, 8, 9, 4 } };

    cout << maximumSquareSize(mat, K);
    return 0;
}
```

## Java

```
// Java implementation to find the
// maximum size square submatrix
// such that their sum is less than K
class GFG{

// Size of matrix
static final int N = 4;
static final int M = 5;

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
static void preProcess(int [][]mat,
                       int [][]aux)
{

    // Loop to copy the first row of
    // the matrix into the aux matrix
    for(int i = 0; i < M; i++)
       aux[0][i] = mat[0][i];

    // Computing the sum column-wise
    for(int i = 1; i < N; i++)
       for(int j = 0; j < M; j++)
          aux[i][j] = mat[i][j] +
                      aux[i - 1][j];

    // Computing row wise sum
    for(int i = 0; i < N; i++)
       for(int j = 1; j < M; j++)
          aux[i][j] += aux[i][j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
static int sumQuery(int [][]aux, int tli,
                    int tlj, int rbi, int rbj)
{

    // Overall sum from the top to
    // right corner of matrix
    int res = aux[rbi][rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1][rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi][tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res + aux[tli - 1][tlj - 1];

    return res;
}

// Function to check whether square
// sub matrices of size mid satisfy
// the condition or not
static boolean check(int mid, int [][]aux,
                     int K)
{

    boolean satisfies = true;

    // Iterating throught all possible
    // submatrices of given size
    for(int x = 0; x < N; x++)
    {
       for(int y = 0; y < M; y++)
       {
          if (x + mid - 1 <= N - 1 &&
              y + mid - 1 <= M - 1)
          {
              if (sumQuery(aux, x, y,
                           x + mid - 1,
                           y + mid - 1) > K)
                  satisfies = false;
          }
       }
    }
    return (satisfies == true);
}

// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
static int maximumSquareSize(int [][]mat,
                             int K)
{
    int [][]aux = new int[N][M];

    preProcess(mat, aux);

    // Search space
    int low = 1, high = Math.min(N, M);
    int mid;

    // Binary search for size
    while (high - low > 1)
    {
        mid = (low + high) / 2;

        // Check if the mid satisfies
        // the given condition
        if (check(mid, aux, K))
        {
            low = mid;
        }
        else
            high = mid;
    }
    if (check(high, aux, K))
        return high;
    return low;
}

// Driver Code
public static void main(String[] args)
{
    int K = 30;
    int [][]mat = { { 1, 2, 3, 4, 6 },
                    { 5, 3, 8, 1, 2 },
                    { 4, 6, 7, 5, 5 },
                    { 2, 4, 8, 9, 4 } };

    System.out.print(maximumSquareSize(mat, K));
}
}

// This code is contributed by Rajput-Ji
```

## python 3

```
# Python3 implementation to find the
# maximum size square submatrix
# such that their sum is less than K

# Function to preprocess the matrix
# for computing the sum of every
# possible matrix of the given size
def preProcess(mat, aux):

    # Loop to copy the first row
    # of the matrix into the aux matrix
    for i in range(5):
        aux[0][i] = mat[0][i]

    # Computing the sum column-wise
    for i in range(1, 4):
        for j in range(5):
            aux[i][j] = (mat[i][j] +
                         aux[i - 1][j])

    # Computing row wise sum
    for i in range(4):
        for j in range(1, 5):
            aux[i][j] += aux[i][j - 1]

    return aux

# Function to find the sum of a
# submatrix with the given indices
def sumQuery(aux, tli, tlj, rbi, rbj):

    # Overall sum from the top to
    # right corner of matrix
    res = aux[rbi][rbj]

    # Removing the sum from the top
    # corer of the matrix
    if (tli > 0):
        res = res - aux[tli - 1][rbj]

    # Remove the overlapping sum
    if (tlj > 0):
        res = res - aux[rbi][tlj - 1]

    # Add the sum of top corner
    # which is subtracted twice
    if (tli > 0 and tlj > 0):
        res = res + aux[tli - 1][tlj - 1]

    return res

# Function to check whether square
# sub matrices of size mid satisfy
# the condition or not
def check(mid, aux, K):

    satisfies = True

    # Iterating throught all possible
    # submatrices of given size
    for x in range(4):
        for y in range(5):
            if (x + mid - 1 <= 4 - 1 and
                y + mid - 1 <= 5 - 1):
                if (sumQuery(aux, x, y,
                             x + mid - 1,
                             y + mid - 1) > K):
                    satisfies = False

    return True if satisfies == True else False

# Function to find the maximum
# square size possible with the
# such that every submatrix have
# sum less than the given sum
def maximumSquareSize(mat, K):

    aux = [[0 for i in range(5)]
              for i in range(4)]

    aux = preProcess(mat, aux)

    # Search space
    low , high = 1, min(4, 5)
    mid = 0

    # Binary search for size
    while (high - low > 1):
        mid = (low + high) // 2

        # Check if the mid satisfies
        # the given condition
        if (check(mid, aux, K)):
            low = mid
        else:
            high = mid

    if (check(high, aux, K)):
        return high

    return low

# Driver Code
if __name__ == '__main__':

    K = 30

    mat = [ [ 1, 2, 3, 4, 6 ],
            [ 5, 3, 8, 1, 2 ],
            [ 4, 6, 7, 5, 5 ],
            [ 2, 4, 8, 9, 4 ] ]

    print(maximumSquareSize(mat, K))

# This code is contributed by mohit kumar 29
```

## c#

```
// C# implementation to find the
// maximum size square submatrix
// such that their sum is less than K
using System;

class GFG{

// Size of matrix
static readonly int N = 4;
static readonly int M = 5;

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
static void preProcess(int [,]mat,
                       int [,]aux)
{

    // Loop to copy the first row of
    // the matrix into the aux matrix
    for(int i = 0; i < M; i++)
       aux[0, i] = mat[0, i];

    // Computing the sum column-wise
    for(int i = 1; i < N; i++)
       for(int j = 0; j < M; j++)
          aux[i, j] = mat[i, j] +
                      aux[i - 1, j];

    // Computing row wise sum
    for(int i = 0; i < N; i++)
       for(int j = 1; j < M; j++)
          aux[i, j] += aux[i, j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
static int sumQuery(int [,]aux, int tli,
                    int tlj, int rbi, int rbj)
{

    // Overall sum from the top to
    // right corner of matrix
    int res = aux[rbi, rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1, rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi, tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res + aux[tli - 1, tlj - 1];

    return res;
}

// Function to check whether square
// sub matrices of size mid satisfy
// the condition or not
static bool check(int mid, int [,]aux,
                  int K)
{

    bool satisfies = true;

    // Iterating throught all possible
    // submatrices of given size
    for(int x = 0; x < N; x++)
    {
       for(int y = 0; y < M; y++)
       {
          if (x + mid - 1 <= N - 1 &&
              y + mid - 1 <= M - 1)
          {
              if (sumQuery(aux, x, y,
                           x + mid - 1,
                           y + mid - 1) > K)
                  satisfies = false;
          }
       }
    }
    return (satisfies == true);
}

// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
static int maximumSquareSize(int [,]mat,
                             int K)
{
    int [,]aux = new int[N, M];

    preProcess(mat, aux);

    // Search space
    int low = 1, high = Math.Min(N, M);
    int mid;

    // Binary search for size
    while (high - low > 1)
    {
        mid = (low + high) / 2;

        // Check if the mid satisfies
        // the given condition
        if (check(mid, aux, K))
        {
            low = mid;
        }
        else
            high = mid;
    }
    if (check(high, aux, K))
        return high;
    return low;
}

// Driver Code
public static void Main(String[] args)
{
    int K = 30;
    int [,]mat = { { 1, 2, 3, 4, 6 },
                   { 5, 3, 8, 1, 2 },
                   { 4, 6, 7, 5, 5 },
                   { 2, 4, 8, 9, 4 } };

    Console.Write(maximumSquareSize(mat, K));
}
}

// This code is contributed by Rajput-Ji
```

## Javascript

```
<script>
// Javascript implementation to find the
// maximum size square submatrix
// such that their sum is less than K

// Size of matrix
let N = 4;
let M = 5;

// Function to preprocess the matrix
// for computing the sum of every
// possible matrix of the given size
function preProcess(mat,aux)
{
    // Loop to copy the first row of
    // the matrix into the aux matrix
    for(let i = 0; i < M; i++)
       aux[0][i] = mat[0][i];

    // Computing the sum column-wise
    for(let i = 1; i < N; i++)
       for(let j = 0; j < M; j++)
          aux[i][j] = mat[i][j] +
                      aux[i - 1][j];

    // Computing row wise sum
    for(let i = 0; i < N; i++)
       for(let j = 1; j < M; j++)
          aux[i][j] += aux[i][j - 1];
}

// Function to find the sum of a
// submatrix with the given indices
function sumQuery(aux,tli,tlj,rbi,rbj)
{
    // Overall sum from the top to
    // right corner of matrix
    let res = aux[rbi][rbj];

    // Removing the sum from the top
    // corer of the matrix
    if (tli > 0)
        res = res - aux[tli - 1][rbj];

    // Remove the overlapping sum
    if (tlj > 0)
        res = res - aux[rbi][tlj - 1];

    // Add the sum of top corner
    // which is subtracted twice
    if (tli > 0 && tlj > 0)
        res = res + aux[tli - 1][tlj - 1];

    return res;
}

// Function to check whether square
// sub matrices of size mid satisfy
// the condition or not
function check(mid,aux,K)
{
    let satisfies = true;

    // Iterating throught all possible
    // submatrices of given size
    for(let x = 0; x < N; x++)
    {
       for(let y = 0; y < M; y++)
       {
          if (x + mid - 1 <= N - 1 &&
              y + mid - 1 <= M - 1)
          {
              if (sumQuery(aux, x, y,
                           x + mid - 1,
                           y + mid - 1) > K)
                  satisfies = false;
          }
       }
    }
    return (satisfies == true);
}

// Function to find the maximum
// square size possible with the
// such that every submatrix have
// sum less than the given sum
function maximumSquareSize(mat,K)
{
    let aux = new Array(N);
    for(let i=0;i<N;i++)
    {
        aux[i]=new Array(M);
    }

    preProcess(mat, aux);

    // Search space
    let low = 1, high = Math.min(N, M);
    let mid;

    // Binary search for size
    while (high - low > 1)
    {
        mid = Math.floor((low + high) / 2);

        // Check if the mid satisfies
        // the given condition
        if (check(mid, aux, K))
        {
            low = mid;
        }
        else
            high = mid;
    }
    if (check(high, aux, K))
        return high;
    return low;
}

// Driver Code
let K = 30;
let mat = [[1, 2, 3, 4, 6 ],
                    [ 5, 3, 8, 1, 2 ],
                    [ 4, 6, 7, 5, 5 ],
                    [ 2, 4, 8, 9, 4 ] ];
document.write(maximumSquareSize(mat, K));

// This code is contributed by rag2127
</script>
```

**输出:**

```
2
```

**性能分析:**

*   **Time complexity:** o (n <sup>2</sup> * log (n))
*   **auxiliary space:** o (n <sup>2</sup> )
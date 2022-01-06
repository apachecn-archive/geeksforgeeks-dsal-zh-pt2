# 给定数组中最多 K 次跳跃的最大路径和

> 原文:[https://www . geeksforgeeks . org/给定数组中最大路径和最多 k 跳数/](https://www.geeksforgeeks.org/maximum-path-sum-in-the-given-arrays-with-at-most-k-jumps/)

给定三个数组 **A、B** 和 **C** ，每个数组都有 **N** 个元素，任务是找到沿着任意**有效路径**最多有 **K** 个跳跃可以获得的最大和。
如果路径遵循以下属性，则该路径为**有效**:

1.  它从数组的第 0 个索引开始。
2.  它在数组的第(N-1)个索引处结束。
3.  对于索引 I 处路径中的任何元素，下一个元素应该只在当前或相邻数组的索引 i+1 上。
4.  如果路径涉及从相邻数组中选择下一个(i + 1)元素，而不是当前元素，则称之为 **1 跳转**

**示例:**

> **输入:** A[] = {4，5，1，2，10}，B[] = {9，7，3，20，16}，C[] = {6，12，13，9，8}， K = 2
> **输出:** 70
> **说明:**
> 从数组 B 开始选择元素如下:
> 选择 B[0]: 9 = > sum = 9
> 跳转到 C[1]: 12 = > sum = 21
> 选择 C[2]: 13 = > sum = 34
> 跳转到 B[3]: 20 = > sum = 54
> 选择 B[3
> **输入:** A[] = {10，4，1，8}，B[] = {9，0，2，5}，C[] = {6，2，7，3}，K = 2
> **输出:** 24

**直觉贪婪方法(不正确):**解决这个问题的一个可能的想法是在当前索引处选择最大元素，并从当前数组或相邻数组(如果还有跳转)移动到下一个具有最大值的索引。
例如:

```
Given,
A[] = {4, 5, 1, 2, 10},
B[] = {9, 7, 3, 20, 16},
C[] = {6, 12, 13, 9, 8},
K = 2
```

使用贪婪方法找到解决方案:

```
Current maximum: 9, K = 2, sum = 9
Next maximum: 12, K = 1, sum = 12
Next maximum: 13, K = 1, sum = 25
Next maximum: 20, K = 0, sum = 45
Adding rest of elements: 16, K = 0, sum = 61

Clearly, this is not the maximum sum.
```

因此，这种方法是不正确的。
**动态编程方法**:动态编程可以分两步使用——递归和记忆。

*   **递归:**可以使用以下递归关系分解问题:
    *   在数组 A 上，索引 I 带有 K 个跳转

> pathSum(A，I，k) = A[i] + max(pathSum(A，i+1，k)，pathSum(B，i+1，k-1))；

*   同样，在阵列 B 上，

> pathSum(B，I，k) = B[i] + max(pathSum(B，i+1，k)、max(pathSum(A，i+1，k-1)、pathSum(C，i+1，k-1))；

*   同样，在数组 C 上，

> pathSum(C，I，k) = C[i] + max(pathSum(C，i+1，k)，pathSum(B，i+1，k-1))；

*   因此，最大总和可以计算为:

> maxSum = max(pathSum(A，I，k)，max(pathSum(B，I，k)，pathSum(C，I，k))；

*   **记忆:**上述递归解的复杂度可以借助记忆来降低。
    *   将计算后的结果存储在大小为[3][N][K]的三维数组中。
    *   dp 数组的任何元素的值都存储数组中 x 个跳转左边的第 I 个索引的最大和

以下是该方法的实施情况:

## C++

```
// C++ program to maximum path sum in
// the given arrays with at most K jumps

#include <iostream>
using namespace std;

#define M 3
#define N 5
#define K 2

int dp[M][N][K];

void initializeDp()
{
    for (int i = 0; i < M; i++)
        for (int j = 0; j < N; j++)
            for (int k = 0; k < K; k++)
                dp[i][j][k] = -1;
}

// Function to calculate maximum path sum
int pathSum(int* a, int* b, int* c,
            int i, int n,
            int k, int on)
{
    // Base Case
    if (i == n)
        return 0;

    if (dp[on][i][k] != -1)
        return dp[on][i][k];

    int current, sum;
    switch (on) {
    case 0:
        current = a[i];
        break;
    case 1:
        current = b[i];
        break;
    case 2:
        current = c[i];
        break;
    }

    // No jumps available.
    // Hence pathSum can be
    // from current array only
    if (k == 0) {
        return dp[on][i][k]
               = current
                 + pathSum(a, b, c, i + 1,
                           n, k, on);
    }

    // Since jumps are available
    // pathSum can be from current
    // or adjacent array
    switch (on) {
    case 0:
        sum = current
              + max(pathSum(a, b, c, i + 1,
                            n, k - 1, 1),
                    pathSum(a, b, c, i + 1,
                            n, k, 0));
        break;
    case 1:
        sum = current
              + max(pathSum(a, b, c, i + 1,
                            n, k - 1, 0),
                    max(pathSum(a, b, c, i + 1,
                                n, k, 1),
                        pathSum(a, b, c, i + 1,
                                n, k - 1, 2)));
        break;
    case 2:
        sum = current
              + max(pathSum(a, b, c, i + 1,
                            n, k - 1, 1),
                    pathSum(a, b, c, i + 1,
                            n, k, 2));
        break;
    }

    return dp[on][i][k] = sum;
}

void findMaxSum(int* a, int* b,
                int* c, int n, int k)
{
    int sum = 0;

    // Creating the DP array for memorisation
    initializeDp();

    // Find the pathSum using recursive approach
    for (int i = 0; i < 3; i++) {

        // Maximise the sum
        sum = max(sum,
                  pathSum(a, b, c, 0,
                          n, k, i));
    }

    cout << sum;
}

// Driver Code
int main()
{
    int n = 5, k = 1;
    int A[n] = { 4, 5, 1, 2, 10 };
    int B[n] = { 9, 7, 3, 20, 16 };
    int C[n] = { 6, 12, 13, 9, 8 };

    findMaxSum(A, B, C, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximum path sum in
// the given arrays with at most K jumps
import java.util.*;
class GFG
{
    static int M = 3;
    static int N = 5;
    static int K = 2;

    static int dp[][][] = new int[M][N][K];

    static void initializeDp()
    {
        for (int i = 0; i < M; i++)
            for (int j = 0; j < N; j++)
                for (int k = 0; k < K; k++)
                    dp[i][j][k] = -1;
    }

    // Function to calculate maximum path sum
    static int pathSum(int a[], int b[], int c[],
                int i, int n,
                int k, int on)
    {
        // Base Case
        if (i == n)
            return 0;

        if (dp[on][i][k] != -1)
            return dp[on][i][k];

        int current = 0, sum = 0;

        switch (on) {
        case 0:
            current = a[i];
            break;
        case 1:
            current = b[i];
            break;
        case 2:
            current = c[i];
            break;
        }

        // No jumps available.
        // Hence pathSum can be
        // from current array only
        if (k == 0) {
            return dp[on][i][k]
                = current
                    + pathSum(a, b, c, i + 1,
                            n, k, on);
        }

        // Since jumps are available
        // pathSum can be from current
        // or adjacent array
        switch (on) {
        case 0:
            sum = current
                + Math.max(pathSum(a, b, c, i + 1,
                                n, k - 1, 1),
                        pathSum(a, b, c, i + 1,
                                n, k, 0));
            break;
        case 1:
            sum = current
                + Math.max(pathSum(a, b, c, i + 1,
                                n, k - 1, 0),
                        Math.max(pathSum(a, b, c, i + 1,
                                    n, k, 1),
                            pathSum(a, b, c, i + 1,
                                    n, k - 1, 2)));
            break;
        case 2:
            sum = current
                + Math.max(pathSum(a, b, c, i + 1,
                                n, k - 1, 1),
                        pathSum(a, b, c, i + 1,
                                n, k, 2));
            break;
        }

        return dp[on][i][k] = sum;
    }

    static void findMaxSum(int a[], int b[],
                    int c[], int n, int k)
    {
        int sum = 0;

        // Creating the DP array for memorisation
        initializeDp();

        // Find the pathSum using recursive approach
        for (int i = 0; i < 3; i++) {

            // Maximise the sum
            sum = Math.max(sum,
                    pathSum(a, b, c, 0,
                            n, k, i));
        }

        System.out.print(sum);
    }

    // Driver Code
    public static void main(String []args)
    {
        int n = 5, k = 1;
        int A[] = { 4, 5, 1, 2, 10 };
        int B[] = { 9, 7, 3, 20, 16 };
        int C[] = { 6, 12, 13, 9, 8 };

        findMaxSum(A, B, C, n, k);
    }
}

// This code is contributed by chitranayal
```

## 计算机编程语言

```
#Python3 program to maximum path sum in
#the given arrays with at most K jumps
M = 3
N = 5
K = 2
dp=[[[-1 for i in range(K)]
      for i in range(N)]
      for i in range(M)]
def initializeDp():
    for i in range(M):
        for j in range(N):
            for k in range(K):
                dp[i][j][k] = -1

#Function to calculate maximum path sum
def pathSum(a, b, c, i, n, k, on):

    #Base Case
    if (i == n):
        return 0

    if (dp[on][i][k] != -1):
        return dp[on][i][k]
    current, sum = 0, 0
    if on == 0:
        current = a[i]
        #break
    if on == 1:
        current = b[i]
        #break
    if on == 2:
        current = c[i]
        #break

    #No jumps available.
    #Hence pathSum can be
    #from current array only
    if (k == 0):
        dp[on][i][k] = current +
                       pathSum(a, b, c,
                               i + 1, n, k, on)
        return dp[on][i][k]

    #Since jumps are available
    #pathSum can be from current
    #or adjacent array
    if on == 0:
        sum = current + max(pathSum(a, b, c, i + 1,
                                    n, k - 1, 1),
                            pathSum(a, b, c,
                                    i + 1, n, k, 0))

    #break
    if on == 1:
        sum = current + max(pathSum(a, b, c, i + 1,
                                    n, k - 1, 0),
                        max(pathSum(a, b, c, i + 1,
                                    n, k, 1),
                            pathSum(a, b, c, i + 1,
                                    n, k - 1, 2)))

    #break
    if on == 2:
        sum = current + max(pathSum(a, b, c, i + 1,
                                    n, k - 1, 1),
                            pathSum(a, b, c, i + 1,
                                    n, k, 2))

    #break
    dp[on][i][k] = sum

    return sum

def findMaxSum(a, b, c, n, k):
    sum = 0

    #Creating the DP array for memorisation
    initializeDp()

    #Find the pathSum using recursive approach
    for i in range(3):

        #Maximise the sum
        sum = max(sum, pathSum(a, b, c, 0, n, k, i))

    print(sum)

#Driver Code
if __name__ == '__main__':
    n = 5
    k = 1
    A = [4, 5, 1, 2, 10]
    B = [9, 7, 3, 20, 16]
    C = [6, 12, 13, 9, 8]
    findMaxSum(A, B, C, n, k)

#This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to maximum path sum in
// the given arrays with at most K jumps
using System;

class GFG{

static int M = 3;
static int N = 5;
static int K = 2;

static int [,,]dp = new int[M, N, K];

static void initializeDp()
{
    for(int i = 0; i < M; i++)
       for(int j = 0; j < N; j++)
          for(int k = 0; k < K; k++)
             dp[i, j, k] = -1;
}

// Function to calculate maximum path sum
static int pathSum(int []a, int []b, int []c,
                   int i, int n,
                   int k, int on)
{

    // Base Case
    if (i == n)
        return 0;

    if (dp[on, i, k] != -1)
        return dp[on, i, k];

    int current = 0, sum = 0;

    switch (on)
    {
    case 0:
        current = a[i];
        break;
    case 1:
        current = b[i];
        break;
    case 2:
        current = c[i];
        break;
    }

    // No jumps available.
    // Hence pathSum can be
    // from current array only
    if (k == 0)
    {
        return dp[on, i, k] = current +
                              pathSum(a, b, c, i + 1,
                                      n, k, on);
    }

    // Since jumps are available
    // pathSum can be from current
    // or adjacent array
    switch (on)
    {
    case 0:
        sum = current + Math.Max(pathSum(a, b, c, i + 1,
                                         n, k - 1, 1),
                                 pathSum(a, b, c, i + 1,
                                         n, k, 0));
        break;
    case 1:
        sum = current + Math.Max(pathSum(a, b, c, i + 1,
                                         n, k - 1, 0),
                        Math.Max(pathSum(a, b, c, i + 1,
                                          n, k, 1),
                                 pathSum(a, b, c, i + 1,
                                         n, k - 1, 2)));
        break;
    case 2:
        sum = current + Math.Max(pathSum(a, b, c, i + 1,
                                         n, k - 1, 1),
                                 pathSum(a, b, c, i + 1,
                                         n, k, 2));
        break;
    }

    return dp[on, i, k] = sum;
}

static void findMaxSum(int []a, int []b,
                       int []c, int n, int k)
{
    int sum = 0;

    // Creating the DP array for memorisation
    initializeDp();

    // Find the pathSum using recursive approach
    for(int i = 0; i < 3; i++)
    {

       // Maximise the sum
       sum = Math.Max(sum, pathSum(a, b, c, 0,
                                   n, k, i));
    }
    Console.Write(sum);
}

// Driver Code
public static void Main(String []args)
{
    int n = 5, k = 1;
    int []A = { 4, 5, 1, 2, 10 };
    int []B = { 9, 7, 3, 20, 16 };
    int []C = { 6, 12, 13, 9, 8 };

    findMaxSum(A, B, C, n, k);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to maximum path sum in
// the given arrays with at most K jumps

    let  M = 3;
    let N = 5;
    let K = 2;

    let dp=new Array(M);

    function initializeDp()
    {
        for (let i = 0; i < M; i++)
        {   
            dp[i]=new Array(N);
            for (let j = 0; j < N; j++)
            {
                dp[i][j]=new Array(K);
                for (let k = 0; k < K; k++)
                    dp[i][j][k] = -1;
            }
         }
     }

     // Function to calculate maximum path sum
     function pathSum(a,b,c,i,n,k,on)
     {
         // Base Case
        if (i == n)
            return 0;

        if (dp[on][i][k] != -1)
            return dp[on][i][k];

        let current = 0, sum = 0;

        switch (on) {
        case 0:
            current = a[i];
            break;
        case 1:
            current = b[i];
            break;
        case 2:
            current = c[i];
            break;

        }

        // No jumps available.
        // Hence pathSum can be
        // from current array only
        if (k == 0) {
            return dp[on][i][k]
                = current
                    + pathSum(a, b, c, i + 1,
                            n, k, on);
        }

        // Since jumps are available
        // pathSum can be from current
        // or adjacent array
        switch (on) {
        case 0:
            sum = current
                + Math.max(pathSum(a, b, c, i + 1,
                                n, k - 1, 1),
                        pathSum(a, b, c, i + 1,
                                n, k, 0));
            break;
        case 1:
            sum = current
                + Math.max(pathSum(a, b, c, i + 1,
                                n, k - 1, 0),
                        Math.max(pathSum(a, b, c, i + 1,
                                    n, k, 1),
                            pathSum(a, b, c, i + 1,
                                    n, k - 1, 2)));
            break;
        case 2:
            sum = current
                + Math.max(pathSum(a, b, c, i + 1,
                                n, k - 1, 1),
                        pathSum(a, b, c, i + 1,
                                n, k, 2));
            break;

        }

        return dp[on][i][k] = sum;
     }

     function findMaxSum(a,b,c,n,k)
     {
         let sum = 0;

        // Creating the DP array for memorisation
        initializeDp();

        // Find the pathSum using recursive approach
        for (let i = 0; i < 3; i++) {

            // Maximise the sum
            sum = Math.max(sum,
                    pathSum(a, b, c, 0,
                            n, k, i));
        }

        document.write(sum);
     }

     // Driver Code
     let n = 5, k = 1;
     let A=[4, 5, 1, 2, 10];
     let B=[9, 7, 3, 20, 16];
     let C=[6, 12, 13, 9, 8 ];

    findMaxSum(A, B, C, n, k);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
67
```

***时间复杂度:**O(N * K)*
T5**辅助空间:** O(N * K)
# 允许两人见面一次的最高积分

> 原文:[https://www . geeksforgeeks . org/最多两人积分-允许见面一次/](https://www.geeksforgeeks.org/maximum-points-collected-by-two-persons-allowed-to-meet-once/)

给定一个二维矩阵 A[N][M]，其中 A[i][j]表示这个单元上可用的点。两个人，P1 和 P2，从这个矩阵的两个角开始。P1 从左上角开始，需要到达右下角。另一方面，P2 从左下开始，需要到达右上。P1 可以上下移动。P2 完全可以胜任。当他们参观一个牢房时，A[i][j]点被加到他们的总数中。任务是最大化他们两个收集的总点数的总和，条件是他们只能见面一次，并且该单元的成本不应包含在他们的总点数中。

**示例:**

```
Input : A[][] = { {100, 100, 100},
                   {100, 1, 100},
                   {100, 100, 100}};
Output : 800
P1 needs to go from (0,0) to (2,2)
P2 needs to go from (2,0) to (0,2)
Explanation: P1 goes through A[0][0]->A[0][1]->A[1][1]->
                             A[2][1]->A[2][2]. 
             P2 goes through A[2][0]->A[1][0]->A[1][1]->
                             A[1][2]->A[0][2].
They meet at A[1][1]. So total points collected: 
A[0][0] + A[0][1] + A[2][1] + A[2][2] + 
A[2][0] + A[1][0] + A[1][2] + A[0][2] = 800

Input : A[][] = {{100, 100, 100, 100},
                 {100, 100, 100, 100},
                 {100, 0, 100, 100},
                 {100, 100, 100, 100}};
Output : 1200
```

P1 需要从左上角(0，0)移动到右下角(n-1，m-1)。P1 可以向右下移动，即从 A[i][j]移动到 A[i][j+1]或 A[i+1][j]
P2 需要从左下角(n-1，0)移动到右上角(0，m-1)。P2 可以向右上方移动，即从 A[i][j]移动到 A[i][j+1]或 A[i-1][j]。

这个想法是把每个点都看作一个交汇点，找到所有交汇点的最大值。当我们将点 A[i][j]视为交汇点时，我们需要有以下四个值来找到当点 A[i][j]为交汇点时收集的最大总点数。
1)P1 从(0，0)到(I，j)收集的点数。
2)P1 从(I，j)到(n-1，m-1)收集的点。
3)P2 从(n-1，0)到(I，j)收集的点。
4)P2 从(I，j)到(0，m-1)收集的点。
我们可以使用动态规划来计算以上四个值。一旦我们对每个点有了以上四个值，我们就可以在每个交汇点找到最大点。

对于每个交汇点，有两个可能的值可以到达它和离开它，因为我们只能有一个交汇点。
1) P1 通过右移到达它，p2 通过上移到达它，它们也以同样的方式离开。
2) P1 通过向下移动到达它，p2 通过向右移动到达它，它们也以相同的方式离开。
我们取上述两个值中的最大值，在这个交汇点找到最佳点。

最后，我们返回所有会议点的最大值。

## C++

```
// C++ program to find maximum points that can
// be collected by two persons in a matrix.
#include<bits/stdc++.h>
#define M 3
#define N 3
using namespace std;

int findMaxPoints(int A[][M])
{
    // To store points collected by Person P1
    // when he/she begins journey from start and
    // from end.
    int P1S[M+1][N+1], P1E[M+1][N+1];
    memset(P1S, 0, sizeof(P1S));
    memset(P1E, 0, sizeof(P1E));

    // To store points collected by Person P2
    // when he/she begins journey from start and
    // from end.
    int P2S[M+1][N+1], P2E[M+1][N+1];
    memset(P2S, 0, sizeof(P2S));
    memset(P2E, 0, sizeof(P2E));

    // Table for P1's journey from
    // start to meeting cell
    for (int i=1; i<=N; i++)
        for (int j=1; j<=M; j++)
            P1S[i][j] = max(P1S[i-1][j],
                  P1S[i][j-1]) + A[i-1][j-1];

    // Table for P1's journey from
    // end to meet cell
    for (int i=N; i>=1; i--)
        for (int j=M; j>=1; j--)
            P1E[i][j] = max(P1E[i+1][j],
                  P1E[i][j+1]) + A[i-1][j-1];

    // Table for P2's journey from start to meeting cell
    for (int i=N; i>=1; i--)
        for(int j=1; j<=M; j++)
            P2S[i][j] = max(P2S[i+1][j],
                  P2S[i][j-1]) + A[i-1][j-1];

    // Table for P2's journey from end to meeting cell
    for (int i=1; i<=N; i++)
        for (int j=M; j>=1; j--)
            P2E[i][j] = max(P2E[i-1][j],
                  P2E[i][j+1]) + A[i-1][j-1];

    // Now iterate over all meeting positions (i,j)
    int ans = 0;
    for (int i=2; i<N; i++)
    {
        for (int j=2; j<M; j++)
        {
            int op1 = P1S[i][j-1] + P1E[i][j+1] +
                      P2S[i+1][j] + P2E[i-1][j];
            int op2 = P1S[i-1][j] + P1E[i+1][j] +
                      P2S[i][j-1] + P2E[i][j+1];
            ans = max(ans, max(op1, op2));
        }
    }
    return ans;
}

// Driver code
int main()
{
    //input the calories burnt matrix
    int A[][M] = {{100, 100, 100},
                  {100, 1, 100},
                  {100, 100, 100}};
    cout << "Max Points : " << findMaxPoints(A);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum points that can
// be collected by two persons in a matrix.

class GFG
{
    static final int M = 3;
    static final int N = 3 ;
static int findMaxPoints(int A[][])
{
    // To store points collected by Person P1
    // when he/she begins journey from start and
    // from end.
    int [][]P1S = new int[M + 2][N + 2];
    int [][]P1E = new int[M + 2][N + 2];

    // To store points collected by Person P2
    // when he/she begins journey from start and
    // from end.
    int [][]P2S = new int[M + 2][N + 2];
    int [][]P2E = new int[M + 2][N + 2];

    // Table for P1's journey from
    // start to meeting cell
    for (int i = 1; i <= N; i++)
        for (int j = 1; j <= M; j++)
            P1S[i][j] = Math.max(P1S[i - 1][j],
                P1S[i][j - 1]) + A[i - 1][j - 1];

    // Table for P1's journey from
    // end to meet cell
    for (int i = N; i >= 1; i--)
        for (int j = M; j >= 1; j--)
            P1E[i][j] = Math.max(P1E[i + 1][j],
                P1E[i][j + 1]) + A[i - 1][j - 1];

    // Table for P2's journey from start to meeting cell
    for (int i = N; i >= 1; i--)
        for(int j = 1; j <= M; j++)
            P2S[i][j] = Math.max(P2S[i + 1][j],
                P2S[i][j - 1]) + A[i - 1][j - 1];

    // Table for P2's journey from end to meeting cell
    for (int i = 1; i <= N; i++)
        for (int j = M; j >= 1; j--)
            P2E[i][j] = Math.max(P2E[i - 1][j],
                P2E[i][j + 1]) + A[i - 1][j - 1];

    // Now iterate over all meeting positions (i, j)
    int ans = 0;
    for (int i = 2; i < N; i++)
    {
        for (int j = 2; j < M; j++)
        {
            int op1 = P1S[i][j - 1] + P1E[i][j + 1] +
                    P2S[i + 1][j] + P2E[i - 1][j];
            int op2 = P1S[i - 1][j] + P1E[i + 1][j] +
                    P2S[i][j - 1] + P2E[i][j + 1];
            ans = Math.max(ans, Math.max(op1, op2));
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    // input the calories burnt matrix
    int A[][] = {{100, 100, 100},
                {100, 1, 100},
                {100, 100, 100}};
    System.out.print("Max Points : " + findMaxPoints(A));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find maximum points that can
# be collected by two persons in a matrix.
M = 3
N = 3
def findMaxPoints(A):

    # To store points collected by Person P1
    # when he/she begins journey from start and
    # from end.
    P1S = [[0 for i in range(N + 2)] for j in range(M + 2)]
    P1E = [[0 for i in range(N + 2)] for j in range(M + 2)]

    # To store points collected by Person P2
    # when he/she begins journey from start and
    # from end.
    P2S = [[0 for i in range(N + 2)] for j in range(M + 2)]
    P2E = [[0 for i in range(N + 2)] for j in range(M + 2)]

    # Table for P1's journey from
    # start to meeting cell
    for i in range(1, N + 1):
        for j in range(1,M + 1):
            P1S[i][j] = max(P1S[i - 1][j],
                        P1S[i][j - 1]) + A[i - 1][j - 1]

    # Table for P1's journey from
    # end to meet cell
    for i in range(N, 0, -1):
        for j in range(M, 0, -1):
            P1E[i][j] = max(P1E[i + 1][j],
                        P1E[i][j + 1]) + A[i - 1][j - 1]

    # Table for P2's journey from start to meeting cell
    for i in range(N, 0, -1):
        for j in range(1, M + 1):
            P2S[i][j] = max(P2S[i + 1][j],
                        P2S[i][j - 1]) + A[i - 1][j - 1]

    # Table for P2's journey from end to meeting cell
    for i in range(1, N + 1):
        for j in range(M, 0, -1):
            P2E[i][j] = max(P2E[i - 1][j],
                        P2E[i][j + 1]) + A[i - 1][j - 1]

    # Now iterate over all meeting positions (i,j)
    ans = 0
    for i in range(2, N):
        for j in range(2, M):
            op1 = P1S[i][j - 1] + P1E[i][j + 1] + \
                  P2S[i + 1][j] + P2E[i - 1][j]
            op2 = P1S[i - 1][j] + P1E[i + 1][j] + \
                  P2S[i][j - 1] + P2E[i][j + 1]
            ans = max(ans, max(op1, op2))

    return ans

# Driver code
# input the calories burnt matrix
A= [[100, 100, 100], [100, 1, 100], [100, 100, 100]]
print("Max Points : ", findMaxPoints(A))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to find maximum points that can
// be collected by two persons in a matrix.
using System;

class GFG
{
    static readonly int M = 3;
    static readonly int N = 3 ;
    static int findMaxPoints(int [,]A)
    {
        // To store points collected by Person P1
        // when he/she begins journey from start and
        // from end.
        int [,]P1S = new int[M + 2, N + 2];
        int [,]P1E = new int[M + 2, N + 2];

        // To store points collected by Person P2
        // when he/she begins journey from start and
        // from end.
        int [,]P2S = new int[M + 2, N + 2];
        int [,]P2E = new int[M + 2, N + 2];

        // Table for P1's journey from
        // start to meeting cell
        for (int i = 1; i <= N; i++)
            for (int j = 1; j <= M; j++)
                P1S[i, j] = Math.Max(P1S[i - 1, j],
                    P1S[i, j - 1]) + A[i - 1, j - 1];

        // Table for P1's journey from
        // end to meet cell
        for (int i = N; i >= 1; i--)
            for (int j = M; j >= 1; j--)
                P1E[i, j] = Math.Max(P1E[i + 1, j],
                    P1E[i, j + 1]) + A[i - 1, j - 1];

        // Table for P2's journey from start to meeting cell
        for (int i = N; i >= 1; i--)
            for(int j = 1; j <= M; j++)
                P2S[i, j] = Math.Max(P2S[i + 1, j],
                    P2S[i, j - 1]) + A[i - 1, j - 1];

        // Table for P2's journey from end to meeting cell
        for (int i = 1; i <= N; i++)
            for (int j = M; j >= 1; j--)
                P2E[i, j] = Math.Max(P2E[i - 1, j],
                    P2E[i, j + 1]) + A[i - 1, j - 1];

        // Now iterate over all meeting positions (i, j)
        int ans = 0;
        for (int i = 2; i < N; i++)
        {
            for (int j = 2; j < M; j++)
            {
                int op1 = P1S[i, j - 1] + P1E[i, j + 1] +
                        P2S[i + 1, j] + P2E[i - 1, j];
                int op2 = P1S[i - 1, j] + P1E[i + 1, j] +
                        P2S[i, j - 1] + P2E[i, j + 1];
                ans = Math.Max(ans, Math.Max(op1, op2));
            }
        }
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // input the calories burnt matrix
        int [,]A = {{100, 100, 100},
                    {100, 1, 100},
                    {100, 100, 100}};
        Console.Write("Max Points : " + findMaxPoints(A));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find
// maximum points that can be
// collected by two persons in a matrix.
let M = 3;
let N = 3;

function findMaxPoints(A)
{

    // To store points collected by Person P1
    // when he/she begins journey from start and
    // from end.
    let P1S = new Array(M + 2);
    let P1E = new Array(M + 2);

    // To store points collected by Person P2
    // when he/she begins journey from start and
    // from end.
    let P2S = new Array(M + 2);
    let P2E = new Array(M + 2);

    for(let i = 0; i< M + 2; i++)
    {
        P1S[i] = new Array(N + 2);
        P1E[i] = new Array(N + 2);
        P2S[i] = new Array(N + 2);
        P2E[i] = new Array(N + 2);
        for(let j = 0; j < N + 2; j++)
        {
            P1S[i][j] = 0;
            P1E[i][j] = 0;
            P2S[i][j] = 0;
            P2E[i][j] = 0;
        }
    }

    // Table for P1's journey from
    // start to meeting cell
    for(let i = 1; i <= N; i++)
        for(let j = 1; j <= M; j++)
            P1S[i][j] = Math.max(P1S[i - 1][j],
                  P1S[i][j - 1]) + A[i - 1][j - 1];

    // Table for P1's journey from
    // end to meet cell
    for(let i = N; i >= 1; i--)
        for(let j = M; j >= 1; j--)
            P1E[i][j] = Math.max(P1E[i + 1][j],
                  P1E[i][j + 1]) + A[i - 1][j - 1];

    // Table for P2's journey from start to
    // meeting cell
    for(let i = N; i >= 1; i--)
        for(let j = 1; j <= M; j++)
            P2S[i][j] = Math.max(P2S[i + 1][j],
                  P2S[i][j - 1]) + A[i - 1][j - 1];

    // Table for P2's journey from
    // end to meeting cell
    for(let i = 1; i <= N; i++)
        for(let j = M; j >= 1; j--)
            P2E[i][j] = Math.max(P2E[i - 1][j],
                  P2E[i][j + 1]) + A[i - 1][j - 1];

    // Now iterate over all meeting positions (i, j)
    let ans = 0;
    for(let i = 2; i < N; i++)
    {
        for(let j = 2; j < M; j++)
        {
            let op1 = P1S[i][j - 1] + P1E[i][j + 1] +
                         P2S[i + 1][j] + P2E[i - 1][j];
            let op2 = P1S[i - 1][j] + P1E[i + 1][j] +
                   P2S[i][j - 1] + P2E[i][j + 1];
            ans = Math.max(ans, Math.max(op1, op2));
        }
    }
    return ans;
}

// Driver code
let A = [ [ 100, 100, 100 ],
          [ 100, 1, 100 ],
          [ 100, 100, 100 ] ];
document.write("Max Points : " +
               findMaxPoints(A));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Max Points : 800
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N * M)

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
# 通过从三个给定数组中选择 X 个不同索引的元素来最大化总和

> 原文:[https://www . geesforgeks . org/通过从三个给定数组中选择 x 个不同的索引元素来最大化总和/](https://www.geeksforgeeks.org/maximize-sum-by-selecting-x-different-indexed-elements-from-three-given-arrays/)

给定大小为 **N** 的三个[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**、**B【】**和**C【】**以及三个正整数 **X** 、 **Y** 和 **Z** ，任务是通过最多选择 **N** 个数组元素来找到最大可能和，使得最多 **X** 个元素来自数组 **最多 **Y** 元素来自数组 **B[]** ，最多 **Z** 元素来自数组 **C[]** ，所有元素来自不同的索引。**

**示例:**

> **输入:** A[] = {10，0，5}，B[] = {5，10，0}，C[] = {0，5，10}，X = 1，Y = 1，Z = 1
> **输出:** 30
> **解释:**
> 选择 A[0]，B[1]，C[2]使和= A[0] + B[1] + C[2] = 30，这是满足给定条件后的最大可能和
> 因此，所需输出为 30。
> 
> **输入:** A[] = {0}，B[] = {0}，C[] = {0}，X = 1，Y = 1，Z = 1
> T3】输出: 0

**天真的做法:**按照以下步骤解决问题:

*   [遍历所有数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并生成所有可能的组合，从满足给定条件的三个不同数组中最多选择 **N** 个元素:
*   对于每一个**I**元素，可以执行以下四个操作:
    *   从阵中选择**I<sup>th</sup>T3【元素， **A[]** 。**
    *   从阵中选择**I<sup>th</sup>T3【元素， **A[]** 。**
    *   从阵中选择**I<sup>th</sup>T3【元素， **A[]** 。**
    *   从任意阵列中选择第**I**元素。
*   因此，解决问题的递推关系如下:

> FindMaxS(X，Y，Z，I)= max(A[I]+FindMaxS(X–1，Y，Z，I–1)，B[i] + FindMaxS(X，Y–1，Z，I–1)，C[i] + FindMaxS(X，Y，Z–1，I–1)，find maxs(X，Y，Z，I–1))

*   利用上述递推关系，根据给定条件，打印选择 **N** 数组元素的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum of at most N with
// different index array elements such that at most X
// are from A[], Y are from B[] and Z are from C[]
int FindMaxS(int X, int Y, int Z, int n, vector<int>& A,
             vector<int>& B, vector<int>& C)
{

    // Base Cases
    if (X < 0 or Y < 0 or Z < 0)
        return INT_MIN;
    if (n < 0)
        return 0;

    // Selecting i-th element from A[]
    int ch = A[n] + FindMaxS(X - 1, Y, Z,
                             n - 1, A, B, C);

    // Selecting i-th element from B[]
    int ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1,
                             A, B, C);

    // Selecting i-th element from C[]
    int co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,
                             A, B, C);

    // i-th elements not selected from
    // any of the arrays
    int no = FindMaxS(X, Y, Z, n - 1, A, B, C);

    // Select the maximum sum from all
    // the possible calls
    int maximum = max(ch, max(ca, max(co, no)));

    return maximum;
}

// Driver Code
int main()
{

    // Given X, Y and Z

    int X = 1;
    int Y = 1;
    int Z = 1;

    // Given A[]
    vector<int> A = { 10, 0, 5 };

    // Given B[]
    vector<int> B = { 5, 10, 0 };

    // Given C[]
    vector<int> C = { 0, 5, 10 };

    // Given Size
    int n = B.size();

    // Function Call
    cout << FindMaxS(X, Y, Z, n - 1, A, B, C);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find maximum sum of at most N with
// different index array elements such that at most X
// are from A[], Y are from B[] and Z are from C[]
static int FindMaxS(int X, int Y, int Z, int n,
                    int A[], int B[], int C[])
{

    // Base Cases
    if (X < 0 || Y < 0 || Z < 0)
        return Integer.MIN_VALUE;
    if (n < 0)
        return 0;

    // Selecting i-th element from A[]
    int ch = A[n] + FindMaxS(X - 1, Y, Z,
                             n - 1, A, B, C);

    // Selecting i-th element from B[]
    int ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1,
                             A, B, C);

    // Selecting i-th element from C[]
    int co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,
                             A, B, C);

    // i-th elements not selected from
    // any of the arrays
    int no = FindMaxS(X, Y, Z, n - 1, A, B, C);

    // Select the maximum sum from all
    // the possible calls
    int maximum = Math.max(ch, Math.max(
        ca, Math.max(co, no)));

    return maximum;
}

// Driver Code
public static void main (String[] args)
{

    // Given X, Y and Z
    int X = 1;
    int Y = 1;
    int Z = 1;

    // Given A[]
    int A[] = { 10, 0, 5 };

    // Given B[]
    int B[] = { 5, 10, 0 };

    // Given C[]
    int C[] = { 0, 5, 10 };

    // Given Size
    int n = B.length;

    // Function Call
    System.out.println(FindMaxS(X, Y, Z, n - 1, A, B, C));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find maximum sum of at most N with
# different index array elements such that at most X
# are from A[], Y are from B[] and Z are from C[]
def FindMaxS(X, Y, Z, n):

    global A, B, C
    if (X < 0 or Y < 0 or Z < 0):
        return -10**9
    if (n < 0):
        return 0

    # Selecting i-th element from A[]
    ch = A[n] + FindMaxS(X - 1, Y, Z,n - 1)

    # Selecting i-th element from B[]
    ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1)

    # Selecting i-th element from C[]
    co = C[n] + FindMaxS(X, Y, Z - 1, n - 1)

    # i-th elements not selected from
    # any of the arrays
    no = FindMaxS(X, Y, Z, n - 1)

    # Select the maximum sum from all
    # the possible calls
    maximum = max(ch, max(ca, max(co, no)))
    return maximum

# Driver Code
if __name__ == '__main__':

    # Given X, Y and Z
    X = 1
    Y = 1
    Z = 1

    # Given A[]
    A = [10, 0, 5]

    # Given B[]
    B = [5, 10, 0]

    # Given C[]
    C = [0, 5, 10]

    # Given Size
    n = len(B)

    # Function Call
    print (FindMaxS(X, Y, Z, n - 1))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find maximum sum of at most N with
// different index array elements such that at most X
// are from []A, Y are from []B and Z are from C[]
static int FindMaxS(int X, int Y, int Z, int n,
                    int []A, int []B, int []C)
{

    // Base Cases
    if (X < 0 || Y < 0 || Z < 0)
        return int.MinValue;
    if (n < 0)
        return 0;

    // Selecting i-th element from []A
    int ch = A[n] + FindMaxS(X - 1, Y, Z,
                             n - 1, A, B, C);

    // Selecting i-th element from []B
    int ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1,
                             A, B, C);

    // Selecting i-th element from C[]
    int co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,
                             A, B, C);

    // i-th elements not selected from
    // any of the arrays
    int no = FindMaxS(X, Y, Z, n - 1, A, B, C);

    // Select the maximum sum from all
    // the possible calls
    int maximum = Math.Max(ch, Math.Max(
        ca, Math.Max(co, no)));
    return maximum;
}

// Driver Code
public static void Main(String[] args)
{

    // Given X, Y and Z
    int X = 1;
    int Y = 1;
    int Z = 1;

    // Given []A
    int []A = { 10, 0, 5 };

    // Given []B
    int []B = { 5, 10, 0 };

    // Given C[]
    int []C = { 0, 5, 10 };

    // Given Size
    int n = B.Length;

    // Function Call
    Console.WriteLine(FindMaxS(X, Y, Z, n - 1, A, B, C));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find maximum sum of at most N with
// different index array elements such that at most X
// are from A[], Y are from B[] and Z are from C[]
function FindMaxS(X, Y, Z, n, A, B, C)
{

    // Base Cases
    if (X < 0 || Y < 0 || Z < 0)
        return -1000000000;
    if (n < 0)
        return 0;

    // Selecting i-th element from A[]
    var ch = A[n] + FindMaxS(X - 1, Y, Z,
                             n - 1, A, B, C);

    // Selecting i-th element from B[]
    var ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1,
                             A, B, C);

    // Selecting i-th element from C[]
    var co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,
                             A, B, C);

    // i-th elements not selected from
    // any of the arrays
    var no = FindMaxS(X, Y, Z, n - 1, A, B, C);

    // Select the maximum sum from all
    // the possible calls
    var maximum = Math.max(ch, Math.max(ca, Math.max(co, no)));

    return maximum;
}

// Driver Code
// Given X, Y and Z
var X = 1;
var Y = 1;
var Z = 1;
// Given A[]
var A = [10, 0, 5];
// Given B[]
var B = [5, 10, 0];
// Given C[]
var C = [0, 5, 10];
// Given Size
var n = B.length;
// Function Call
document.write( FindMaxS(X, Y, Z, n - 1, A, B, C));

</script>
```

**Output:** 

```
30
```

***时间复杂度:**O(4<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)进行优化。按照以下步骤解决问题:

*   初始化一个 4D 数组，比如 **dp[N][X][Y][Z]** ，存储上述递归关系的重叠子问题。
*   使用上述递归关系，使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)打印 **dp[N][X][Y][Z]** 的值。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Store overlapping subproblems
// of the recurrence relation
int dp[50][50][50][50];

// Function to find maximum sum of at most N with
// different index array elements such that at most X
// are from A[], Y are from B[] and Z are from C[]
int FindMaxS(int X, int Y, int Z, int n, vector<int>& A,
            vector<int>& B, vector<int>& C)
{

    // Base Cases
    if (X < 0 or Y < 0 or Z < 0)
        return INT_MIN;
    if (n < 0)
        return 0;

    // If the subproblem already computed
    if (dp[n][X][Y][Z] != -1) {

        return dp[n][X][Y][Z];
    }

    // Selecting i-th element from A[]
    int ch = A[n] + FindMaxS(X - 1, Y, Z,
                             n - 1, A, B, C);

    // Selecting i-th element from B[]
    int ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1,
                             A, B, C);

    // Selecting i-th element from C[]
    int co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,
                             A, B, C);

    // i-th elements not selected from
    // any of the arrays
    int no = FindMaxS(X, Y, Z, n - 1, A, B, C);

    // Select the maximum sum from all
    // the possible calls
    int maximum = max(ch, max(ca, max(co, no)));
    return dp[n][X][Y][Z] = maximum;
}

// Driver Code
int main()
{

    // Given X, Y and Z
    int X = 1;
    int Y = 1;
    int Z = 1;

    // Given A[]
    vector<int> A = { 10, 0, 5 };

    // Given B[]
    vector<int> B = { 5, 10, 0 };

    // Given C[]
    vector<int> C = { 0, 5, 10 };

    // Given Size
    int n = B.size();
    memset(dp, -1, sizeof(dp));

    // Function Call
    cout << FindMaxS(X, Y, Z, n - 1, A, B, C);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Store overlapping subproblems
// of the recurrence relation
static int [][][][]dp = new int[50][50][50][50];

// Function to find maximum sum of at most N with
// different index array elements such that at most X
// are from A[], Y are from B[] and Z are from C[]
static int FindMaxS(int X, int Y, int Z, int n,
                    int []A, int []B, int []C)
{

    // Base Cases
    if (X < 0 || Y < 0 || Z < 0)
        return Integer.MIN_VALUE;
    if (n < 0)
        return 0;

    // If the subproblem already computed
    if (dp[n][X][Y][Z] != -1)
    {
        return dp[n][X][Y][Z];
    }

    // Selecting i-th element from A[]
    int ch = A[n] + FindMaxS(X - 1, Y, Z,
                             n - 1, A, B, C);

    // Selecting i-th element from B[]
    int ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1,
                             A, B, C);

    // Selecting i-th element from C[]
    int co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,
                             A, B, C);

    // i-th elements not selected from
    // any of the arrays
    int no = FindMaxS(X, Y, Z, n - 1, A, B, C);

    // Select the maximum sum from all
    // the possible calls
    int maximum = Math.max(
        ch, Math.max(ca, Math.max(co, no)));
    return dp[n][X][Y][Z] = maximum;
}

// Driver Code
public static void main(String[] args)
{

    // Given X, Y and Z
    int X = 1;
    int Y = 1;
    int Z = 1;

    // Given A[]
    int []A = { 10, 0, 5 };

    // Given B[]
    int []B = { 5, 10, 0 };

    // Given C[]
    int []C = { 0, 5, 10 };

    // Given Size
    int n = B.length;
    for(int i = 0; i < 50; i++)
         for(int j = 0; j < 50; j++)
             for(int k = 0; k < 50; k++)
                 for(int l = 0; l < 50; l++)
                     dp[i][j][k][l] = -1;

    // Function Call
    System.out.print(FindMaxS(X, Y, Z, n - 1,
                              A, B, C));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Store overlapping subproblems
# of the recurrence relation
dp =  [[[[-1 for i in range(50)] for j in range(50)] for k in range(50)] for l in range(50)]

# Function to find maximum sum of at most N with
# different index array elements such that at most X
# are from A[], Y are from B[] and Z are from C[]
def FindMaxS(X, Y, Z, n, A, B, C):

    # Base Cases
    if (X < 0 or Y < 0 or Z < 0):
        return -sys.maxsize - 1
    if (n < 0):
        return 0

    # If the subproblem already computed
    if (dp[n][X][Y][Z] != -1):
        return dp[n][X][Y][Z]

    # Selecting i-th element from A[]
    ch = A[n] + FindMaxS(X - 1, Y, Z, n - 1, A, B, C)

    # Selecting i-th element from B[]
    ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1, A, B, C)

    # Selecting i-th element from C[]
    co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,A, B, C)

    # i-th elements not selected from
    # any of the arrays
    no = FindMaxS(X, Y, Z, n - 1, A, B, C)

    # Select the maximum sum from all
    # the possible calls
    maximum = max(ch, max(ca, max(co, no)))
    dp[n][X][Y][Z] = maximum
    return dp[n][X][Y][Z]

# Driver Code
if __name__ == '__main__':

    # Given X, Y and Z
    X = 1
    Y = 1
    Z = 1

    # Given A[]
    A =  [10, 0, 5]

    # Given B[]
    B =  [5, 10, 0]

    # Given C[]
    C =  [0, 5, 10]

    # Given Size
    n = len(B)

    # Function Call
    print(FindMaxS(X, Y, Z, n - 1, A, B, C))

   # This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Store overlapping subproblems
// of the recurrence relation
static int[,,,] dp = new int[50, 50, 50, 50];

// Function to find maximum sum of at most N with
// different index array elements such that at most X
// are from A[], Y are from B[] and Z are from C[]
static int FindMaxS(int X, int Y, int Z, int n,
                    int[] A, int[] B, int[] C)
{

    // Base Cases
    if (X < 0 || Y < 0 || Z < 0)
        return Int32.MinValue;
    if (n < 0)
        return 0;

    // If the subproblem already computed
    if (dp[n, X, Y, Z] != -1)
    {
        return dp[n, X, Y, Z];
    }

    // Selecting i-th element from A[]
    int ch = A[n] + FindMaxS(X - 1, Y, Z,
                             n - 1, A, B, C);

    // Selecting i-th element from B[]
    int ca = B[n] + FindMaxS(X, Y - 1, Z,
                                n - 1, A, B, C);

    // Selecting i-th element from C[]
    int co = C[n] + FindMaxS(X, Y, Z - 1, n - 1,
                             A, B, C);

    // i-th elements not selected from
    // any of the arrays
    int no = FindMaxS(X, Y, Z, n - 1, A, B, C);

    // Select the maximum sum from all
    // the possible calls
    int maximum = Math.Max(
        ch, Math.Max(ca, Math.Max(co, no)));
    return dp[n, X, Y, Z] = maximum;
}

// Driver Code
public static void Main(string[] args)
{

    // Given X, Y and Z
    int X = 1;
    int Y = 1;
    int Z = 1;

    // Given A[]
    int[] A = { 10, 0, 5 };

    // Given B[]
    int[] B = { 5, 10, 0 };

    // Given C[]
    int[] C = { 0, 5, 10 };

    // Given Size
    int n = B.Length;
    for(int i = 0; i < 50; i++)
        for(int j = 0; j < 50; j++)
            for(int k = 0; k < 50; k++)
                for(int l = 0; l < 50; l++)
                    dp[i, j, k, l] = -1;

    // Function Call
    Console.Write(FindMaxS(X, Y, Z, n - 1, A, B, C));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Store overlapping subproblems
    // of the recurrence relation
    let dp = new Array(50);

    // Function to find maximum sum of at most N with
    // different index array elements such that at most X
    // are from A[], Y are from B[] and Z are from C[]
    function FindMaxS(X, Y, Z, n, A, B, C)
    {

        // Base Cases
        if (X < 0 || Y < 0 || Z < 0)
            return Number.MIN_VALUE;
        if (n < 0)
            return 0;

        // If the subproblem already computed
        if (dp[n][X][Y][Z] != -1)
        {
            return dp[n][X][Y][Z];
        }

        // Selecting i-th element from A[]
        let ch = A[n] + FindMaxS(X - 1, Y, Z, n - 1, A, B, C);

        // Selecting i-th element from B[]
        let ca = B[n] + FindMaxS(X, Y - 1, Z, n - 1, A, B, C);

        // Selecting i-th element from C[]
        let co = C[n] + FindMaxS(X, Y, Z - 1, n - 1, A, B, C);

        // i-th elements not selected from
        // any of the arrays
        let no = FindMaxS(X, Y, Z, n - 1, A, B, C);

        // Select the maximum sum from all
        // the possible calls
        let maximum = Math.max(ch, Math.max(ca, Math.max(co, no)));
        dp[n][X][Y][Z] = maximum;
        return dp[n][X][Y][Z];
    }

    // Given X, Y and Z
    let X = 1;
    let Y = 1;
    let Z = 1;

    // Given A[]
    let A = [ 10, 0, 5 ];

    // Given B[]
    let B = [ 5, 10, 0 ];

    // Given C[]
    let C = [ 0, 5, 10 ];

    // Given Size
    let n = B.length;
    for(let i = 0; i < 50; i++)
    {
         dp[i] = new Array(50);
         for(let j = 0; j < 50; j++)
         {
             dp[i][j] = new Array(50);
             for(let k = 0; k < 50; k++)
             {
                  dp[i][j][k] = new Array(50);
                 for(let l = 0; l < 50; l++)
                 {
                     dp[i][j][k][l] = -1;
                 }
             }
         }
    }

    // Function Call
    document.write(FindMaxS(X, Y, Z, n - 1, A, B, C));

</script>
```

**输出:**

```
30
```

***时间复杂度*** : O(N * X * Y * Z)

***空间复杂度:*** O(N * X * Y * Z)
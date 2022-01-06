# 将巧克力棒分割成块，最小化无效块的面积

> 原文:[https://www . geeksforgeeks . org/将巧克力棒分成碎片-最小化无效碎片的面积/](https://www.geeksforgeeks.org/divide-chocolate-bar-into-pieces-minimizing-the-area-of-invalid-pieces/)

给定一个 [2d 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **arr[][]** 和一块尺寸为 **N × M** 的巧克力块，任务是通过将巧克力块分成一个或多个块来找到无效块面积的最小可能和，如果该块的尺寸与任何给定的对不匹配，则该块被称为无效。

**注意:**一块巧克力可以垂直或水平(垂直于它的边)切割，这样它被分成两块，并且给定向量中的维度是**非有序的**，即对于给定向量中的一对(x，y)，维度(x，y)和(y，x)都被认为是有效的。

**示例:**

> **输入** : N = 10，M =10，arr[][] = {{1，2}}
> **输出** : 0
> **解释** :
> 将给定的尺寸为(10，10)的巧克力棒分成 50 块尺寸为(1，2)或(2，1)的巧克力棒，不留下任何剩余块，因此输出为零。
> 
> **输入** : N = 10，M =10，arr[][] = {{3，5}}
> 输出 : 10

**天真的方法:**天真的想法是使用[递归](https://www.geeksforgeeks.org/recursion/)通过进行每个可能的垂直或水平切割，在每个可能的维度上分割巧克力。请按照以下步骤解决此问题:

*   将巧克力棒分成[所有可能的方式](https://www.geeksforgeeks.org/print-all-possible-ways-to-write-n-as-sum-of-two-or-more-positive-integers/)，也就是说，将每一个可能的垂直&水平切割一个接一个，并为每种情况递归地找到最终碎片的解决方案[。](https://www.geeksforgeeks.org/recursion/)
*   对于基本情况，只需检查当前划分是否有效:
    *   如果有效，则返回零。
    *   否则，尝试使用上述方法将其分成有效的部分，如果不能进一步分成有效的部分，则返回该部分的面积。

***时间复杂度:**O(N+M)<sup>(N+M)</sup>*
***辅助空间:** O(1)*

**有效方法:**优化上述方法的思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，因为上述方法有[重叠的子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，需要计算一次以上，并使用 [<u>t</u> 运算或记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)减少该计算。可制作的不同巧克力块总数仅为 **N × M** ，因此上述算法有 N × M 个状态。

按照以下步骤解决问题:

*   初始化数组 **dp[][]** 以在 **dp[l][b]存储**minivalidareautil(l，b)** ，确定[][]** 以在 **ok[i][j] = 1** 和 **ok[j][i] = 1 中存储有效尺寸巧克力(I，j)。**
*   对于每个状态，从查找表**中确定当前片 **(l，b)** 是否在恒定时间内有效[][]**
    *   如果当前件 **(l，b)** 有效，即**ok【l】【b】= = 1**。因此，返回 **dp[l][b] = 0**
    *   否则，通过一个接一个地进行所有可能的垂直和水平切割来计算它，并为每种情况找到最终碎片的解决方案。因此，更新 **dp[l][b]。**
*   将最终答案打印为**minivalidareautil(l，b)。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

const int sz = 1001;

// Store valid dimensions
bool ok[sz][sz] = {};

// Stores memoization
int dp[sz][sz];

// Utility function to calculate minimum invalid area for
// Chocolate piece having dimension (l, r)
int minInvalidAreaUtil(int l, int b)
{
    if (dp[l][b] == -1) {

        // Check whether current piece is valid or not
        // If it is, then return zero
        // for current dimension
        if (ok[l][b]) {
            return dp[l][b] = 0;
        }

        int ans = l * b;

        // Making all possible horizontal cuts, one by
        // one and calculating the sum of minimum invalid
        // area for both the resulting pieces
        for (int i = 1; i < b; i++) {
            ans = min(ans,
                      minInvalidAreaUtil(l, i)
                          + minInvalidAreaUtil(l, b - i));
        }

        // Making all possible vertical cuts, one by one
        // and calculating the sum of minimum invalid area
        // for both the resulting pieces
        for (int i = 1; i < l; i++) {
            ans = min(ans,
                      minInvalidAreaUtil(i, b)
                          + minInvalidAreaUtil(l - i, b));
        }

        // Store the computed result
        dp[l][b] = ans;
    }

    return dp[l][b];
}

// Function to calculate minimum invalid area for
// Chocolate piece having dimension (l, r)
void minInvalidArea(int N, int M,
                     vector<pair<int, int> >& dimensions)
{
    // Total number of valid dimensions
    int K = dimensions.size();

    // Storing valid dimensions as for every (x, y)
    // both (x, y) and (y, x) are valid
    for (int i = 0; i < K; i++) {
        ok[dimensions[i].first][dimensions[i].second] = 1;
        ok[dimensions[i].second][dimensions[i].first] = 1;
    }

    // Fill dp[][] table with -1, indicating that
    // results are not computed yet
    for (int i = 0; i < sz; i++) {
        for (int j = 0; j < sz; j++) {
            dp[i][j] = -1;
        }
    }

    // Stores minimum area
    int minArea = minInvalidAreaUtil(N, M);

    // Print minArea as the output
    cout << minArea << endl;
}

// Driver Code
int main()
{
    // Given N & M
    int N = 10, M = 10;

    // Given valid dimensions
    vector<pair<int, int> > dimensions = { { 3, 5 } };

    // Function Call
    minInvalidArea(N, M, dimensions);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

static final int sz = 1001;

// Store valid dimensions
static boolean ok[][] = new boolean[sz][sz];

// Stores memoization
static int dp[][] = new int[sz][sz];

static class pair
{
    int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }  
}

// Utility function to calculate minimum invalid
// area for Chocolate piece having dimension (l, r)
static int minInvalidAreaUtil(int l, int b)
{
    if (dp[l][b] == -1)
    {

        // Check whether current piece is valid
        // or not. If it is, then return zero
        // for current dimension
        if (ok[l][b])
        {
            return dp[l][b] = 0;
        }

        int ans = l * b;

        // Making all possible horizontal cuts, one by
        // one and calculating the sum of minimum invalid
        // area for both the resulting pieces
        for(int i = 1; i < b; i++)
        {
            ans = Math.min(ans,
                           minInvalidAreaUtil(l, i) +
                           minInvalidAreaUtil(l, b - i));
        }

        // Making all possible vertical cuts, one by one
        // and calculating the sum of minimum invalid area
        // for both the resulting pieces
        for(int i = 1; i < l; i++)
        {
            ans = Math.min(ans,
                           minInvalidAreaUtil(i, b) +
                           minInvalidAreaUtil(l - i, b));
        }

        // Store the computed result
        dp[l][b] = ans;
    }
    return dp[l][b];
}

// Function to calculate minimum invalid area for
// Chocolate piece having dimension (l, r)
static void minInvalidArea(int N, int M,
                           Vector<pair> dimensions)
{

    // Total number of valid dimensions
    int K = dimensions.size();

    // Storing valid dimensions as for every (x, y)
    // both (x, y) and (y, x) are valid
    for(int i = 0; i < K; i++)
    {
        ok[dimensions.elementAt(i).first][dimensions.elementAt(i).second] = true;
        ok[dimensions.elementAt(i).second][dimensions.elementAt(i).first] = true;
    }

    // Fill dp[][] table with -1, indicating that
    // results are not computed yet
    for(int i = 0; i < sz; i++)
    {
        for(int j = 0; j < sz; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Stores minimum area
    int minArea = minInvalidAreaUtil(N, M);

    // Print minArea as the output
    System.out.println(minArea);
}

// Driver Code
public static void main(String[] args)
{

    // Given N & M
    int N = 10, M = 10;

    // Given valid dimensions
    Vector<pair > dimensions = new Vector<>();
      dimensions.add(new pair(3, 5));

    // Function Call
    minInvalidArea(N, M, dimensions);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach
sz = 1001

# Store valid dimensions
ok = [[0 for i in range(sz)]
         for i in range(sz)]

# Stores memoization
dp = [[0 for i in range(sz)]
         for i in range(sz)]

# Utility function to calculate minimum
# invalid area for Chocolate piece having
# dimension (l, r)
def minInvalidAreaUtil(l, b):

    global dp, ok

    if (dp[l][b] == -1):

        # Check whether current piece is valid
        # or not If it is, then return zero
        # for current dimension
        if (ok[l][b]):
            dp[l][b] = 0
            return dp[l][b]

        ans = l * b

        # Making all possible horizontal cuts, one by
        # one and calculating the sum of minimum invalid
        # area for both the resulting pieces
        for i in range(1, b):
            ans = min(ans, minInvalidAreaUtil(l, i) +
                           minInvalidAreaUtil(l, b - i))

        # Making all possible vertical cuts, one by one
        # and calculating the sum of minimum invalid area
        # for both the resulting pieces
        for i in range(1, l):
            ans = min(ans, minInvalidAreaUtil(i, b) +
                           minInvalidAreaUtil(l - i, b))

        # Store the computed result
        dp[l][b] = ans

    return dp[l][b]

# Function to calculate minimum invalid area for
# Chocolate piece having dimension (l, r)
def minInvalidArea(N, M, dimensions):

    global dp, ok

    # Total number of valid dimensions
    K = len(dimensions)

    # Storing valid dimensions as for every (x, y)
    # both (x, y) and (y, x) are valid
    for i in range(K):
        ok[dimensions[i][0]][dimensions[i][1]] = 1
        ok[dimensions[i][1]][dimensions[i][0]] = 1

    # Fill dp[][] table with -1, indicating that
    # results are not computed yet
    for i in range(sz):
        for j in range(sz):
            dp[i][j] = -1

    # Stores minimum area
    minArea = minInvalidAreaUtil(N, M)

    # PrminArea as the output
    print(minArea)

#Driver Code
if __name__ == '__main__':

    # Given N & M
    N, M = 10, 10

    # Given valid dimensions
    dimensions = [ [ 3, 5 ] ]

    # Function Call
    minInvalidArea(N, M, dimensions)

# This code is contributed by mohit kumar 29
```

**Output**

```
10
```

***时间复杂度:** O(N * M * (N + M))*
***辅助空间:** O(N * M)*
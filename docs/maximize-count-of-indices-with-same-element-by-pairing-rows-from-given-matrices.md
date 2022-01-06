# 通过配对给定矩阵中的行，最大化具有相同元素的索引数

> 原文:[https://www . geeksforgeeks . org/通过对给定矩阵中的行进行配对来最大化具有相同元素的索引数/](https://www.geeksforgeeks.org/maximize-count-of-indices-with-same-element-by-pairing-rows-from-given-matrices/)

给定两个大小均为 **M*N** 的 [2D 二进制数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **a[][]** 和 **b[][]** ，任务是将数组 **a[][]** 中的每一行与数组**b[][]****中的任意一行进行配对，从而使总分最大化，并将每一对的分数计算为两行值相同的总索引。**

****注:**阵中每排 **b[][]** 只能与单排*T5T7**a[][]**配对。***

****示例:****

> ****输入:** a[][] = {{1，1，0}，{1，0，1}，{0，0，1}}，b[][] = {{1，0，0}，{0，0，1}，{1，1，0}}
> **输出:** 8
> **解释:**
> 按照以下顺序考虑行的配对，以最大化获得的总分:**
> 
>  ***   **a[][]** 的 R *ow 0 与 **b[][]*** 的*排 2 配对，得分为 3。*
> *   *第 1 行 **a[][]*** 与第 0 行 **b[][]** 配对，得分为 2。
> *   ***a[][]***第 2 排与 **b[][]** 第 1 排配对，得分为 3。
> 
> 所以得到的分数总和是 3 + 2 + 3 = 8。
> 
> **输入:** a[][] = {{0，0}，{0，0}，{0，0}}，b[][] = {{1，1}，{1，1}，{1，1}}
> **输出:** 0**

****天真法:**解决给定问题最简单的方法是[生成数组 **a[][]** 行的所有可能排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，对于数组的每个[排列 **a[][]** ，求每个对应对的得分之和，如果大于当前的**答案**，则将**答案**更新为当前得分之和的值。检查所有配对后，打印获得的最高分数。](https://www.geeksforgeeks.org/permute-the-elements-of-an-array-following-given-order/)**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum score
void maxScoreSum(vector<vector<int> >& a,
                 vector<vector<int> >& b)
{
    // Stores the maximum sum of scores
    int maxSum = 0;

    vector<int> pos;
    for (int i = 0; i < a.size(); i++) {
        pos.push_back(i);
    }

    // For each permutation of pos vector
    // calculate the score
    do {
        int curSum = 0;
        for (int i = 0; i < a.size(); i++) {

            for (int j = 0;
                 j < a[pos[i]].size(); j++) {

                // If values at current indexes
                // are same then increment the
                // current score
                curSum += (a[pos[i]][j] == b[i][j]);
                maxSum = max(maxSum, curSum);
            }
        }
    } while (next_permutation(pos.begin(), pos.end()));

    // Print the maximum score
    cout << maxSum;
}

// Driver Code
int main()
{
    int N = 3, M = 3;
    vector<vector<int> > a
        = { { 1, 1, 0 }, { 1, 0, 1 }, { 0, 0, 1 } };
    vector<vector<int> > b
        = { { 1, 0, 0 }, { 0, 0, 1 }, { 1, 1, 0 } };

    maxScoreSum(a, b);

    return 0;
}
```

## **java 描述语言**

```
<script>
        // JavaScript Program to implement
        // the above approach
        function next_permutation(array) {
            var i = array.length - 1;
            while (i > 0 && array[i - 1] >= array[i]) {
                i--;
            }

            if (i <= 0) {
                return false;
            }

            var j = array.length - 1;

            while (array[j] <= array[i - 1]) {
                j--;
            }

            var temp = array[i - 1];
            array[i - 1] = array[j];
            array[j] = temp;

            j = array.length - 1;

            while (i < j) {
                temp = array[i];
                array[i] = array[j];
                array[j] = temp;
                i++;
                j--;
            }

            return array;
        }
        // Function to find the maximum score
        function maxScoreSum(a, b) {
            // Stores the maximum sum of scores
            let maxSum = 0;

            let pos = [];
            for (let i = 0; i < a.length; i++) {
                pos.push(i);
            }

            // For each permutation of pos vector
            // calculate the score
            do {
                let curSum = 0;
                for (let i = 0; i < a.length; i++) {

                    for (let j = 0;
                        j < a[pos[i]].length; j++) {

                        // If values at current indexes
                        // are same then increment the
                        // current score
                        curSum += (a[pos[i]][j] == b[i][j]);
                        maxSum = Math.max(maxSum, curSum);
                    }
                }
            } while (next_permutation(pos));

            // Print the maximum score
            document.write(maxSum);
        }

        // Driver Code

        let N = 3, M = 3;
        let a
            = [[1, 1, 0], [1, 0, 1], [0, 0, 1]];
        let b
            = [[1, 0, 0], [0, 0, 1], [1, 1, 0]];

        maxScoreSum(a, b);

     // This code is contributed by Potta Lokesh

    </script>
```

****Output:** 

```
8
```** 

*****时间复杂度:** O(N*M*M！)，哪里 M！是排列数和 N*M，用于计算*每对的*分数。*
***辅助空间:** O(M)***

****高效方法:**上述方法也可以使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)的概念进行优化，思路是针对向量 **a[][]** 中的每一行，尝试向量 **b[][]** 中之前没有选择过的所有行。使用[位掩码](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)来表示已经选择的向量行 **b[][]** 。为了避免重新计算同一个子问题，[记住每个](https://www.geeksforgeeks.org/tabulation-vs-memoization/)[位掩码](https://www.geeksforgeeks.org/bitmasking-dynamic-programming-set-2-tsp/)的结果。按照以下步骤解决问题:**

*   **将变量**行**初始化为 **0，将**屏蔽为**(2<sup>M</sup>–1)**。**
*   **[用值 **-1** 初始化大小为**遮罩+ 1** 的向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **dp[]** 。**
*   **如果**行**大于等于 **a.size()** 则返回 **0** ，如果 **dp【掩码】**不等于 **-1** 则返回 **dp【掩码】**。**
*   **将变量**和**初始化为 **0** 来存储答案。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，a.size())** ，并执行以下任务:

    *   如果**掩码**和 **2 <sup>i</sup>** 的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为**真**，则将变量 **newMask** 初始化为**mask^(1<t19】I)**和 **curSum** 为 **0** 。
    *   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)T2【0，a【I】。size()) 使用变量 **j** ，如果 **a【行】【j】**等于**b【I】【j】**，则将 **curSum** 的值增加 **1** 。
    *   将 **ans** 的值设置为 **ans** 或**curSum+maxscorcsum(a，b，row+1，newmask，dp)** [递归](https://www.geeksforgeeks.org/recursion/)的最大值。** 
*   **执行上述步骤后，将 **dp【掩码】**的值设置为 **ans** ，并返回 **ans** 的值作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum defined
// score
int maxScoreSum(vector<vector<int> >& a,
                vector<vector<int> >& b,
                int row, int mask,
                vector<int>& dp)
{
    // If all students are assigned
    if (row >= a.size()) {
        return 0;
    }
    if (dp[mask] != -1) {
        return dp[mask];
    }

    int ans = 0;

    for (int i = 0; i < a.size(); i++) {

        // Check if row is not paired yet
        if (mask & (1 << i)) {
            int newMask = mask ^ (1 << i);
            int curSum = 0;

            // Check for all indexes
            for (int j = 0; j < a[i].size(); j++) {

                // If values at current indexes
                // are same increase curSum
                if (a[row][j] == b[i][j]) {
                    curSum++;
                }
            }

            // Further recursive call
            ans = max(
                ans, curSum
                         + maxScoreSum(
                               a, b, row + 1,
                               newMask, dp));
        }
    }

    // Store the ans for current
    // mask and return
    return dp[mask] = ans;
}

// Utility function to find the maximum
// defined score
int maxScoreSumUtil(vector<vector<int> >& a,
                    vector<vector<int> >& b,
                    int N, int M)
{
    int row = 0;

    // Create a mask with all set bits
    // 1 -> row is not paired yet
    // 0 -> row is already paired
    int mask = pow(2, M) - 1;

    // Initialise dp array with -1
    vector<int> dp(mask + 1, -1);

    return maxScoreSum(a, b, row, mask, dp);
}

// Driver Code
int main()
{
    int N = 3, M = 3;
    vector<vector<int> > a
        = { { 1, 1, 0 }, { 1, 0, 1 }, { 0, 0, 1 } };
    vector<vector<int> > b
        = { { 1, 0, 0 }, { 0, 0, 1 }, { 1, 1, 0 } };

    cout << maxScoreSumUtil(a, b, N, M);

    return 0;
}
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Function to find the maximum defined
# score
def maxScoreSum(a, b, row, mask, dp):

    # If all students are assigned
    if (row >= len(a)):
        return 0

    if (dp[mask] != -1):
        return dp[mask]

    ans = 0

    for i in range(len(a)):

        # Check if row is not paired yet
        if (mask & (1 << i)):
            newMask = mask ^ (1 << i)
            curSum = 0

            # Check for all indexes
            for j in range(len(a[i])):

                # If values at current indexes
                # are same increase curSum
                if (a[row][j] == b[i][j]):
                    curSum += 1

            # Further recursive call
            ans = max(
                ans, curSum
                + maxScoreSum(
                    a, b, row + 1,
                    newMask, dp))

    # Store the ans for current
    # mask and return
    dp[mask] = ans
    return dp[mask]

# Utility function to find the maximum
# defined score
def maxScoreSumUtil(a,
                    b,
                    N, M):

    row = 0

    # Create a mask with all set bits
    # 1 -> row is not paired yet
    # 0 -> row is already paired
    mask = pow(2, M) - 1

    # Initialise dp array with -1
    dp = [-1]*(mask + 1)

    return maxScoreSum(a, b, row, mask, dp)

# Driver Code
if __name__ == "__main__":

    N = 3
    M = 3
    a = [[1, 1, 0], [1, 0, 1], [0, 0, 1]]
    b = [[1, 0, 0], [0, 0, 1], [1, 1, 0]]

    print(maxScoreSumUtil(a, b, N, M))

    # This code is contributed by ukasp.
```

****Output:** 

```
8
```** 

*****时间复杂度:**O(2<sup>M</sup>* M * N)*
***辅助空间:** O(2 <sup>M</sup> )***
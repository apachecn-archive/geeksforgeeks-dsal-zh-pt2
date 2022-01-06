# 阵列中最小的删除，使相邻元素的差异不减少

> 原文:[https://www . geeksforgeeks . org/数组中最小删除数对相邻元素的差值-非递减/](https://www.geeksforgeeks.org/minimum-deletions-in-array-to-make-difference-of-adjacent-elements-non-decreasing/)

给定一个非负整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A****N**，任务是计算要删除的元素的最小数量，以便满足以下条件:

*   元素按非递减顺序排列。(形式上，对于每个 i (1 ≤ i ≤ N-1)，条件**A<sub>I+1</sub>>= A<sub>I</sub>**应该成立。)
*   相邻元素之间的差异应该是不递减的。(形式上，对于每个 i (2 ≤ i ≤ N-1)，条件**A<sub>I</sub>-A<sub>I-1</sub>≤A<sub>I+1</sub>-A<sub>I</sub>T9】应成立。)**

**示例:**

> **输入** : A = {1，4，5，7，20，21}
> **输出** :
> 2
> **说明**:删除 5 和 21，得到数组{1，4，7，20}。这里，元素按非递减顺序排列，相邻元素之间的差为 3、3、13，它们按非递减顺序排列。
> 
> **输入** : A = {3，2}
> 输出 :
> 1
> **说明**:原阵不满足第一个条件。因此，任何一个元素都可以被删除，得到一个只有一个元素的数组。

**朴素方法:**朴素方法是[生成给定数组的所有子集](https://www.geeksforgeeks.org/find-distinct-subsets-given-set/)，并检查是否有任何子集满足条件。如果有，检查有多少元素被删除，以获得该子集，然后取最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function for finding minimum deletions so that the array
// becomes non decreasing and the difference between adjacent
// elements also becomes non decreasing
int minimumDeletions(int A[], int N)
{
    // initialize answer to a large value
    int ans = INT_MAX;

    // generating all subsets
    for (int i = 1; i < (1 << N); i++) {
        vector<int> temp;
        for (int j = 0; j < N; j++) {
            if ((i & (1 << j)) != 0) {
                temp.push_back(A[j]);
            }
        }
        int flag = 0;

        // checking the first condition
        for (int j = 1; j < temp.size(); j++)
            if (temp[j] < temp[j - 1])
                flag = 1;

        // checking the second condition
        for (int j = 1; j < temp.size() - 1; j++)
            if (temp[j] - temp[j - 1]
                > temp[j + 1] - temp[j])
                flag = 1;

        // if both conditions are satisfied consider the
        // answer for minimum
        if (flag == 0) {
            ans = min(ans, N - (int)temp.size());
        }
    }
    return ans;
}
// Driver code
int main()
{
    // Input
    int A[] = { 1, 4, 5, 7, 20, 21 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << minimumDeletions(A, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.ArrayList;

class GFG{

// Function for finding minimum deletions so that the array
// becomes non decreasing and the difference between adjacent
// elements also becomes non decreasing
public static int minimumDeletions(int A[], int N)
{
    // initialize answer to a large value
    int ans = Integer.MAX_VALUE;

    // generating all subsets
    for (int i = 1; i < (1 << N); i++) {
        ArrayList<Integer> temp = new ArrayList<Integer>();
        for (int j = 0; j < N; j++) {
            if ((i & (1 << j)) != 0) {
                temp.add(A[j]);
            }
        }
        int flag = 0;

        // checking the first condition
        for (int j = 1; j < temp.size(); j++)
            if (temp.get(j) < temp.get(j - 1))
                flag = 1;

        // checking the second condition
        for (int j = 1; j < temp.size() - 1; j++)
            if (temp.get(j) - temp.get(j - 1)
                > temp.get(j + 1) - temp.get(j))
                flag = 1;

        // if both conditions are satisfied consider the
        // answer for minimum
        if (flag == 0) {
            ans = Math.min(ans, N - (int)temp.size());
        }
    }
    return ans;
}
// Driver code
public static void main(String args[])
{
    // Input
    int A[] = { 1, 4, 5, 7, 20, 21 };
    int N = A.length;

    // Function call
    System.out.println(minimumDeletions(A, N));
}
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function for finding minimum deletions so that the array
# becomes non decreasing and the difference between adjacent
# elements also becomes non decreasing
def minimumDeletions(A, N):
    # initialize answer to a large value
    ans = 10**8

    # generating all subsets
    for i in range(1,(1<<N)):
        temp = []
        for j in range(N):
            if ((i & (1 << j)) != 0):
                temp.append(A[j])
        flag = 0

        # checking the first condition
        for j in range(1,len(temp)):
            if (temp[j] < temp[j - 1]):
                flag = 1

        # checking the second condition
        for j in range(1,len(temp)-1):
            if (temp[j] - temp[j - 1]> temp[j + 1] - temp[j]):
                flag = 1

        # if both conditions are satisfied consider the
        # answer for minimum
        if (flag == 0):
            ans = min(ans, N - len(temp))
    return ans

# Driver code
if __name__ == '__main__':
    # Input
    A= [1, 4, 5, 7, 20, 21]
    N = len(A)

    # Function call
    print (minimumDeletions(A, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function for finding minimum deletions so that the array
// becomes non decreasing and the difference between adjacent
// elements also becomes non decreasing
static int minimumDeletions(int []A, int N)
{
    // initialize answer to a large value
    int ans = Int32.MaxValue;

    // generating all subsets
    for (int i = 1; i < (1 << N); i++) {
        List<int> temp = new List<int>();
        for (int j = 0; j < N; j++) {
            if ((i & (1 << j)) != 0) {
                temp.Add(A[j]);
            }
        }
        int flag = 0;

        // checking the first condition
        for (int j = 1; j < temp.Count; j++)
            if (temp[j] < temp[j - 1])
                flag = 1;

        // checking the second condition
        for (int j = 1; j < temp.Count - 1; j++)
            if (temp[j] - temp[j - 1]
                > temp[j + 1] - temp[j])
                flag = 1;

        // if both conditions are satisfied consider the
        // answer for minimum
        if (flag == 0) {
            ans = Math.Min(ans, N - temp.Count);
        }
    }
    return ans;
}

// Driver code
public static void Main()
{
    // Input
    int []A = { 1, 4, 5, 7, 20, 21 };
    int N = A.Length;

    // Function call
    Console.Write(minimumDeletions(A, N));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function for finding minimum deletions so that the array
// becomes non decreasing and the difference between adjacent
// elements also becomes non decreasing
function minimumDeletions(A, N) {
    // initialize answer to a large value
    let ans = Number.MAX_SAFE_INTEGER;

    // generating all subsets
    for (let i = 1; i < (1 << N); i++) {
        let temp = [];
        for (let j = 0; j < N; j++) {
            if ((i & (1 << j)) != 0) {
                temp.push(A[j]);
            }
        }
        let flag = 0;

        // checking the first condition
        for (let j = 1; j < temp.length; j++)
            if (temp[j] < temp[j - 1])
                flag = 1;

        // checking the second condition
        for (let j = 1; j < temp.length - 1; j++)
            if (temp[j] - temp[j - 1]
                > temp[j + 1] - temp[j])
                flag = 1;

        // if both conditions are satisfied consider the
        // answer for minimum
        if (flag == 0) {
            ans = Math.min(ans, N - temp.length);
        }
    }
    return ans;
}

// Driver code

// Input
let A = [1, 4, 5, 7, 20, 21];
let N = A.length;

// Function call

document.write(minimumDeletions(A, N) + "<br>");

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**使用动态规划的有效方法:**可以通过找到条件成立的子集的最大大小来解决问题，而不是找到删除的最小数量。按照以下步骤解决问题:

1.  创建一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **dp** ，其中**DP【I】【j】**存储要从索引 **1 到 i** 中删除的满足以下条件的最小元素数:
    1.  **A[i]-A[i-1]=A[j]**
2.  使用 **i** 从 **0 迭代到 N-1** ，并执行以下操作:
    1.  将 **1** 存放在 **dp[i][0]** 中，大小为 **1** 。
    2.  使用 **j** 从 **i-1 迭代到 0** ，并执行以下操作:
        1.  检查 **A[i]** 是否大于 **A[j]。**如果更大，请执行以下操作:
            1.  将 **A[i]-A[j]** 存储在一个变量中，比如 **diff。**
            2.  使用 **k** 从 **0 迭代到不同的**，并执行以下操作:
                1.  在 **dp[i]** 中存储 **dp[i]** 和 **dp[j][k]+1** 之间的最大值。
                2.  因此，过渡是:
                    1.  **dp[i]=max(dp[i]，DP[j][k]+1]**
3.  使用 **i** 从 **0 迭代到 MAX** ，并将**DP【N-1】【I】**的最大值存储在一个变量中，比如 **maxSetSize。**
4.  答案是 **N-maxSetSize** 。

下面是实现该方法的代码

## C++

```
#include <bits/stdc++.h>
using namespace std;

// the maximum value of A[i]
#define MAX 100001

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
int minimumDeletions(int A[], int N)
{
    // initializing the dp table
    // and setting all values to 0
    int dp[N][MAX];
    for (int i = 0; i < N; i++)
        for (int j = 0; j < MAX; j++)
            dp[i][j] = 0;

    // Find the maximum size valid set
    // that can be taken and then subtract
    // its size from N to get
    // minimum number of deletions

    for (int i = 0; i < N; i++) {
        // when selecting only current element
        // and deleting all elements
        // from 0 to i-1 inclusive
        dp[i][0] = 1;

        for (int j = i - 1; j >= 0; j--) {
            // if this is true moving from
            // index j to i is possible
            if (A[i] >= A[j]) {
                int diff = A[i] - A[j];
                // iterate over all elements from 0
                // to diff and find the max
                for (int k = 0; k <= diff; k++) {
                    dp[i]
                        = max(dp[i], dp[j][k] + 1);
                }
            }
        }
    }

    // take the max set size
    // from dp[N-1][0] to dp[N-1][MAX]
    int maxSetSize = -1;
    for (int i = 0; i < MAX; i++)
        maxSetSize = max(maxSetSize, dp[N - 1][i]);

    return N - maxSetSize;
}

// Driver code
int main()
{
    // Input
    int A[] = { 1, 4, 5, 7, 20, 21 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << minimumDeletions(A, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// the maximum value of A[i]
static int MAX = 100001;

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
static int minimumDeletions(int A[], int N)
{
    // initializing the dp table
    // and setting all values to 0
    int[][] dp = new int[N][MAX];
    for (int i = 0; i < N; i++)
        for (int j = 0; j < MAX; j++)
            dp[i][j] = 0;

    // Find the maximum size valid set
    // that can be taken and then subtract
    // its size from N to get
    // minimum number of deletions

    for (int i = 0; i < N; i++) {
        // when selecting only current element
        // and deleting all elements
        // from 0 to i-1 inclusive
        dp[i][0] = 1;

        for (int j = i - 1; j >= 0; j--) {
            // if this is true moving from
            // index j to i is possible
            if (A[i] >= A[j]) {
                int diff = A[i] - A[j];
                // iterate over all elements from 0
                // to diff and find the max
                for (int k = 0; k <= diff; k++) {
                    dp[i]
                        = Math.max(dp[i], dp[j][k] + 1);
                }
            }
        }
    }

    // take the max set size
    // from dp[N-1][0] to dp[N-1][MAX]
    int maxSetSize = -1;
    for (int i = 0; i < MAX; i++)
        maxSetSize = Math.max(maxSetSize, dp[N - 1][i]);

    return N - maxSetSize;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 4, 5, 7, 20, 21 };
    int N = A.length;

    // Function call
    System.out.println(minimumDeletions(A, N));
}
}

// This code is contributed by code_hunt.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// The maximum value of A[i]
static int MAX = 100001;

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
static int minimumDeletions(int[] A, int N)
{

    // Initializing the dp table
    // and setting all values to 0
    int[,] dp = new int[N, MAX];
    for(int i = 0; i < N; i++)
        for(int j = 0; j < MAX; j++)
            dp[i, j] = 0;

    // Find the maximum size valid set
    // that can be taken and then subtract
    // its size from N to get
    // minimum number of deletions
    for(int i = 0; i < N; i++)
    {

        // When selecting only current element
        // and deleting all elements
        // from 0 to i-1 inclusive
        dp[i, 0] = 1;

        for(int j = i - 1; j >= 0; j--)
        {

            // If this is true moving from
            // index j to i is possible
            if (A[i] >= A[j])
            {
                int diff = A[i] - A[j];

                // Iterate over all elements from 0
                // to diff and find the max
                for(int k = 0; k <= diff; k++)
                {
                    dp[i, diff] = Math.Max(dp[i, diff],
                                           dp[j, k] + 1);
                }
            }
        }
    }

    // Take the max set size
    // from dp[N-1][0] to dp[N-1][MAX]
    int maxSetSize = -1;
    for(int i = 0; i < MAX; i++)
        maxSetSize = Math.Max(maxSetSize, dp[N - 1, i]);

    return N - maxSetSize;
}

// Driver Code
public static void Main()
{
    int[] A = { 1, 4, 5, 7, 20, 21 };
    int N = A.Length;

    // Function call
    Console.Write(minimumDeletions(A, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// The maximum value of A[i]
let MAX = 100001

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
function minimumDeletions(A, N)
{

    // Initializing the dp table
    // and setting all values to 0
    let dp = new Array(N).fill(0).map(
       () => new Array(MAX));

    for(let i = 0; i < N; i++)
        for(let j = 0; j < MAX; j++)
            dp[i][j] = 0;

    // Find the maximum size valid set
    // that can be taken and then subtract
    // its size from N to get
    // minimum number of deletions
    for(let i = 0; i < N; i++)
    {

        // When selecting only current element
        // and deleting all elements
        // from 0 to i-1 inclusive
        dp[i][0] = 1;

        for(let j = i - 1; j >= 0; j--)
        {

            // If this is true moving from
            // index j to i is possible
            if (A[i] >= A[j])
            {
                let diff = A[i] - A[j];

                // Iterate over all elements from 0
                // to diff and find the max
                for(let k = 0; k <= diff; k++)
                {
                    dp[i] = Math.max(dp[i],
                                           dp[j][k] + 1);
                }
            }
        }
    }

    // Take the max set size
    // from dp[N-1][0] to dp[N-1][MAX]
    let maxSetSize = -1;
    for(let i = 0; i < MAX; i++)
        maxSetSize = Math.max(maxSetSize,
                              dp[N - 1][i]);

    return N - maxSetSize;
}

// Driver code

// Input
let A = [ 1, 4, 5, 7, 20, 21 ];
let N = A.length;

// Function call
document.write(minimumDeletions(A, N) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output**

```
2
```

***时间复杂度:** O(N <sup>2</sup> *M)，其中 M 为 A 中最大元素，*
***辅助空间:** O(N*M)*

**使用优化动态规划的有效方法:**在上述方法中，重复计算每个 **k** 从 **0** 到 **diff** 的最小值。为了避免这种情况，可以保持 [2D 前缀最大数组](https://www.geeksforgeeks.org/prefix-sum-2d-array/) **pref** ，其中**pref【I】【j】**存储子集大小的最大值，使得从 **1 到 i** 满足以下条件:

1.  **A[i]-A[i-1]=A[j]**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// the maximum value of A[i]
#define MAX 100001

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
int minimumDeletions(int A[], int N)
{
    // initialize the dp table
    // and set all values to 0
    // pref[i][j] will contain min(dp[i][0],
    // dp[i][1], ...dp[i][j])
    int dp[N][MAX];
    int pref[N][MAX];
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < MAX; j++) {
            dp[i][j] = 0;
            pref[i][j] = 0;
        }
    }

    // find the maximum sized valid set
    // possible and then subtract its
    // size from N to get
    // minimum number of deletions
    for (int i = 0; i < N; i++) {

        // when selecting only the current element and
        // deleting all elements from 0 to i-1 inclusive
        dp[i][0] = 1;

        for (int j = i - 1; j >= 0; j--) {
            // if this is true,
            // moving from index j to i is possible
            if (A[i] >= A[j]) {
                int diff = A[i] - A[j];
                // we can get min(dp[j][0], .. dp[j])
                // from pref array;
                dp[i]
                    = max(dp[i], pref[j] + 1);
            }
        }

        // construct the prefix array for this element
        pref[i][0] = dp[i][0];
        for (int j = 1; j < MAX; j++)
            pref[i][j] = max(dp[i][j], pref[i][j - 1]);
    }

    // take the max set size from dp[N-1][0] to dp[N-1][MAX]
    int maxSetSize = -1;
    for (int i = 0; i < MAX; i++)
        maxSetSize = max(maxSetSize, dp[N - 1][i]);

    return N - maxSetSize;
}

// Driver code
int main()
{
    int A[] = { 1, 4, 5, 7, 20, 21 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << minimumDeletions(A, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// the maximum value of A[i]
static int MAX = 100001;

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
static int minimumDeletions(int A[], int N)
{
    // initialize the dp table
    // and set all values to 0
    // pref[i][j] will contain min(dp[i][0],
    // dp[i][1], ...dp[i][j])
    int[][] dp = new int[N][MAX];
    int[][] pref = new int[N][MAX];

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < MAX; j++) {
            dp[i][j] = 0;
            pref[i][j] = 0;
        }
    }

    // find the maximum sized valid set
    // possible and then subtract its
    // size from N to get
    // minimum number of deletions
    for (int i = 0; i < N; i++) {

        // when selecting only the current element and
        // deleting all elements from 0 to i-1 inclusive
        dp[i][0] = 1;

        for (int j = i - 1; j >= 0; j--)
        {

            // if this is true,
            // moving from index j to i is possible
            if (A[i] >= A[j])
            {
                int diff = A[i] - A[j];

                // we can get min(dp[j][0], .. dp[j])
                // from pref array;
                dp[i]
                    = Math.max(dp[i], pref[j] + 1);
            }
        }

        // construct the prefix array for this element
        pref[i][0] = dp[i][0];
        for (int j = 1; j < MAX; j++)
            pref[i][j] = Math.max(dp[i][j], pref[i][j - 1]);
    }

    // take the max set size from dp[N-1][0] to dp[N-1][MAX]
    int maxSetSize = -1;
    for (int i = 0; i < MAX; i++)
        maxSetSize = Math.max(maxSetSize, dp[N - 1][i]);

    return N - maxSetSize;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 4, 5, 7, 20, 21 };
    int N = A.length;

    // Function call
    System.out.println(minimumDeletions(A, N));
}
}

// This code is contributed by target_2.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

// the maximum value of A[i]
static int MAX = 100001;

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
static int minimumDeletions(int []A, int N)
{

    // initialize the dp table
    // and set all values to 0
    // pref[i][j] will contain min(dp[i][0],
    // dp[i][1], ...dp[i][j])
    int[,] dp = new int[N,MAX];
    int[,] pref = new int[N,MAX];

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < MAX; j++) {
            dp[i,j] = 0;
            pref[i,j] = 0;
        }
    }

    // find the maximum sized valid set
    // possible and then subtract its
    // size from N to get
    // minimum number of deletions
    for (int i = 0; i < N; i++) {

        // when selecting only the current element and
        // deleting all elements from 0 to i-1 inclusive
        dp[i,0] = 1;

        for (int j = i - 1; j >= 0; j--)
        {

            // if this is true,
            // moving from index j to i is possible
            if (A[i] >= A[j])
            {
                int diff = A[i] - A[j];

                // we can get min(dp[j][0], .. dp[j])
                // from pref array;
                dp[i,diff]
                    = Math.Max(dp[i,diff], pref[j,diff] + 1);
            }
        }

        // construct the prefix array for this element
        pref[i,0] = dp[i,0];
        for (int j = 1; j < MAX; j++)
            pref[i,j] = Math.Max(dp[i,j], pref[i,j - 1]);
    }

    // take the max set size from dp[N-1][0] to dp[N-1][MAX]
    int maxSetSize = -1;
    for (int i = 0; i < MAX; i++)
        maxSetSize = Math.Max(maxSetSize, dp[N - 1,i]);

    return N - maxSetSize;
}

// Driver Code
  public static void Main(String[] args)
{
    int []A = { 1, 4, 5, 7, 20, 21 };
    int N = A.Length;

    // Function call
    Console.Write(minimumDeletions(A, N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// the maximum value of A[i]
var MAX = 100001;

// Function for finding minimum deletions
// so that the array becomes non-decreasing
// and the difference between adjacent
// elements is also non-decreasing
function minimumDeletions(A, N)
{

    // initialize the dp table
    // and set all values to 0
    // pref[i][j] will contain min(dp[i][0],
    // dp[i][1], ...dp[i][j])
    var dp = new Array(N,MAX);
    var pref = new Array(N,MAX);

    for (var i = 0; i < N; i++) {
        for (var j = 0; j < MAX; j++) {
            dp[i,j] = 0;
            pref[i,j] = 0;
        }
    }

    // find the maximum sized valid set
    // possible and then subtract its
    // size from N to get
    // minimum number of deletions
    for (var i = 0; i < N; i++) {

        // when selecting only the current element and
        // deleting all elements from 0 to i-1 inclusive
        dp[i,0] = 1;

        for (var j = i - 1; j >= 0; j--)
        {

            // if this is true,
            // moving from index j to i is possible
            if (A[i] >= A[j])
            {
                var diff = A[i] - A[j];

                // we can get min(dp[j][0], .. dp[j])
                // from pref array;
                dp[i]
                    = Math.max(dp[i,diff], pref[j,diff] + 1);
            }
        }

        // construct the prefix array for this element
        pref[i,0] = dp[i,0];
        for (var j = 1; j < MAX; j++)
            pref[i,j] = Math.max(dp[i,j], pref[i,j - 1]);
    }

    // take the max set size from dp[N-1][0] to dp[N-1][MAX]
    var maxSetSize = -1;
    for (var i = 0; i < MAX; i++)
        maxSetSize = Math.max(maxSetSize, dp[N - 1,i]);

    return N - maxSetSize;
}

// Driver Code
    var A = [ 1, 4, 5, 7, 20, 21 ];
    var N = A.length;

    // Function call
    document.write(minimumDeletions(A, N));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
2
```

***时间复杂度:** O(N*M+N <sup>2</sup> ，其中 M 为 A 中最大元素，*
***辅助空间:** O(N*M)*
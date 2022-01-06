# 最大化从两个给定阵列中选择的相同索引子阵列的分数

> 原文:[https://www . geeksforgeeks . org/最大化相同索引子数组的分数-从两个给定数组中选择/](https://www.geeksforgeeks.org/maximize-score-of-same-indexed-subarrays-selected-from-two-given-arrays/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，两者都由 **N** 正整数组成，任务是在两个[数组](https://www.geeksforgeeks.org/array-data-structure/)中所有可能的相同索引的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中找到最大得分，使得任何[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)在范围**【L， R]** 按值**(A<sub>L</sub>* B<sub>L</sub>+A<sub>L+1</sub>* B<sub>L+1</sub>+…+A<sub>R</sub>* B<sub>R</sub>)+(A<sub>R</sub>* B<sub>L</sub>+A<sub>R–1</sub>的最大值计算**

**示例:**

> **输入:** A[] = {13，4，5}，B[] = {10，22，2}
> **输出:** 326
> **解释:**
> 考虑子阵 **{A[0]，A[1]}** 和 **{B[0]，B[1]}** 。这些子阵列的得分可以计算为以下两个表达式的最大值:
> 
> 1.  表达式**的值(A<sub>0</sub>* B<sub>0</sub>+A<sub>1</sub>* B<sub>1</sub>)**= 13 * 1+4 * 22 = 218。
> 2.  表达式**的值(A<sub>0</sub>* B<sub>1</sub>+A<sub>1</sub>* B<sub>0</sub>)**= 13 * 1+4 * 22 = 326。
> 
> 因此，上述两个表达式的最大值是 326，这是所有可能的子阵列中的最大得分。
> 
> **输入:** A[] = {9，8，7，6，1}，B[]={6，7，8，9，1 }
> T3】输出: 230

**天真方法:**解决给定问题最简单的方法是[生成所有可能对应的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并存储使用给定标准生成的所有子阵列的所有分数。存储所有分数后，打印生成的所有分数中的最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the score
// of same-indexed subarrays selected
// from the arrays a[] and b[]
int currSubArrayScore(int* a, int* b,
                      int l, int r)
{
    int straightScore = 0;
    int reverseScore = 0;

    // Traverse the current subarray
    for (int i = l; i <= r; i++) {

        // Finding the score without
        // reversing the subarray
        straightScore += a[i] * b[i];

        // Calculating the score of
        // the reversed subarray
        reverseScore += a[r - (i - l)]
                        * b[i];
    }

    // Return the score of subarray
    return max(straightScore,
               reverseScore);
}

// Function to find the subarray with
// the maximum score
void maxScoreSubArray(int* a, int* b,
                      int n)
{
    // Stores the maximum score and the
    // starting and the ending point
    // of subarray with maximum score
    int res = 0, start = 0, end = 0;

    // Traverse all the subarrays
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            // Store the score of the
            // current subarray
            int currScore
                = currSubArrayScore(
                    a, b, i, j);

            // Update the maximum score
            if (currScore > res) {
                res = currScore;
                start = i;
                end = j;
            }
        }
    }

    // Print the maximum score
    cout << res;
}

// Driver Code
int main()
{
    int A[] = { 13, 4, 5 };
    int B[] = { 10, 22, 2 };
    int N = sizeof(A) / sizeof(A[0]);
    maxScoreSubArray(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate the score
// of same-indexed subarrays selected
// from the arrays a[] and b[]
static int currSubArrayScore(int[] a, int[] b,
                             int l, int r)
{
    int straightScore = 0;
    int reverseScore = 0;

    // Traverse the current subarray
    for(int i = l; i <= r; i++)
    {

        // Finding the score without
        // reversing the subarray
        straightScore += a[i] * b[i];

        // Calculating the score of
        // the reversed subarray
        reverseScore += a[r - (i - l)] * b[i];
    }

    // Return the score of subarray
    return Math.max(straightScore, reverseScore);
}

// Function to find the subarray with
// the maximum score
static void maxScoreSubArray(int[] a, int[] b, int n)
{

    // Stores the maximum score and the
    // starting and the ending point
    // of subarray with maximum score
    int res = 0, start = 0, end = 0;

    // Traverse all the subarrays
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {

            // Store the score of the
            // current subarray
            int currScore = currSubArrayScore(a, b, i, j);

            // Update the maximum score
            if (currScore > res)
            {
                res = currScore;
                start = i;
                end = j;
            }
        }
    }

    // Print the maximum score
    System.out.print(res);
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 13, 4, 5 };
    int B[] = { 10, 22, 2 };
    int N = A.length;

    maxScoreSubArray(A, B, N);
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate the score
# of same-indexed subarrays selected
# from the arrays a[] and b[]
def currSubArrayScore(a, b,
                      l, r):

    straightScore = 0
    reverseScore = 0

    # Traverse the current subarray
    for i in range(l, r+1) :

        # Finding the score without
        # reversing the subarray
        straightScore += a[i] * b[i]

        # Calculating the score of
        # the reversed subarray
        reverseScore += a[r - (i - l)] * b[i]

    # Return the score of subarray
    return max(straightScore,
               reverseScore)

# Function to find the subarray with
# the maximum score
def maxScoreSubArray(a, b,
                      n) :

    # Stores the maximum score and the
    # starting and the ending point
    # of subarray with maximum score
    res = 0
    start = 0
    end = 0

    # Traverse all the subarrays
    for i in range(n) :
        for j in range(i, n) :

            # Store the score of the
            # current subarray
            currScore = currSubArrayScore(a, b, i, j)

            # Update the maximum score
            if (currScore > res) :
                res = currScore
                start = i
                end = j

    # Print the maximum score
    print(res)

# Driver Code
A = [ 13, 4, 5 ]
B = [ 10, 22, 2 ]
N = len(A)
maxScoreSubArray(A, B, N)

# This code is contributed by target_2.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate the score
// of same-indexed subarrays selected
// from the arrays a[] and b[]
static int currSubArrayScore(int[] a, int[] b,
                             int l, int r)
{
    int straightScore = 0;
    int reverseScore = 0;

    // Traverse the current subarray
    for(int i = l; i <= r; i++)
    {

        // Finding the score without
        // reversing the subarray
        straightScore += a[i] * b[i];

        // Calculating the score of
        // the reversed subarray
        reverseScore += a[r - (i - l)] * b[i];
    }

    // Return the score of subarray
    return Math.Max(straightScore, reverseScore);
}

// Function to find the subarray with
// the maximum score
static void maxScoreSubArray(int[] a, int[] b, int n)
{

    // Stores the maximum score and the
    // starting and the ending point
    // of subarray with maximum score
    int res = 0;

    // Traverse all the subarrays
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {

            // Store the score of the
            // current subarray
            int currScore = currSubArrayScore(
                a, b, i, j);

            // Update the maximum score
            if (currScore > res)
            {
                res = currScore;
            }
        }
    }

    // Print the maximum score
    Console.Write(res);
}

// Driver Code
static public void Main()
{
    int[] A = { 13, 4, 5 };
    int[] B = { 10, 22, 2 };
    int N = A.Length;

    maxScoreSubArray(A, B, N);
}
}

// This code is contributed by unknown2108
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the score
// of same-indexed subarrays selected
// from the arrays a[] and b[]
function currSubArrayScore(a, b, l, r)
{
    let straightScore = 0;
    let reverseScore = 0;

    // Traverse the current subarray
    for (let i = l; i <= r; i++) {

        // Finding the score without
        // reversing the subarray
        straightScore += a[i] * b[i];

        // Calculating the score of
        // the reversed subarray
        reverseScore += a[r - (i - l)]
            * b[i];
    }

    // Return the score of subarray
    return Math.max(straightScore,
        reverseScore);
}

// Function to find the subarray with
// the maximum score
function maxScoreSubArray(a, b, n) {
    // Stores the maximum score and the
    // starting and the ending point
    // of subarray with maximum score
    let res = 0, start = 0, end = 0;

    // Traverse all the subarrays
    for (let i = 0; i < n; i++) {
        for (let j = i; j < n; j++) {

            // Store the score of the
            // current subarray
            let currScore
                = currSubArrayScore(
                    a, b, i, j);

            // Update the maximum score
            if (currScore > res) {
                res = currScore;
                start = i;
                end = j;
            }
        }
    }

    // Print the maximum score
    document.write(res);
}

// Driver Code

let A = [13, 4, 5];
let B = [10, 22, 2];
let N = A.length;
maxScoreSubArray(A, B, N);

// This code is contributed by gfgking.

</script>
```

**Output:** 

```
326
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过将每个元素视为每个可能的[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的中点，然后在两个方向上扩展[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，同时更新每个值的最大得分来优化。按照以下步骤解决问题:

*   初始化一个变量，说 **res** 来存储结果最大值。
*   [使用变量**中的**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–1】**，并执行以下步骤:
    *   初始化两个变量，对于奇数长度的子阵列，将**评分 1** 和**评分 2** 设为 **A【中】*B【中】**。
    *   初始化两个变量，将 **prev** 设为**(中间–1)**，将 **next** 设为**(中间+ 1)** ，展开当前子阵列。
    *   [迭代一个循环，直到](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **prev** 为正且 **next** 的值小于 **N** ，并执行以下步骤:
        *   将**(a[prev]* b[prev]+a[next]* b[next])的值**添加到变量**分数 1** 中。
        *   将**(a[上一个]* b[下一个]+a[下一个]* b[上一个])** 的值添加到变量**分数 2** 中。
        *   将 **res** 的值更新为**评分 1** 、**评分 2** 和 **res** 的最大值。
        *   将**的值减去 **1** 的值，然后将**的值增加**的值减去 **1** 。**
    *   将**评分 1** 、**评分 2** 的值更新为 **0** ，将 **prev** 的值设置为**(mid–1)**、 **next** 设置为 **mid** 考虑偶长度子阵的情况。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the score
// of same-indexed subarrays selected
// from the arrays a[] and b[]
void maxScoreSubArray(int* a, int* b,
                      int n)
{
    // Store the required result
    int res = 0;

    // Iterate in the range [0, N-1]
    for (int mid = 0; mid < n; mid++) {

        // Consider the case of odd
        // length subarray
        int straightScore = a[mid] * b[mid],
            reverseScore = a[mid] * a[mid];
        int prev = mid - 1, next = mid + 1;

        // Update the maximum score
        res = max(res, max(straightScore,
                           reverseScore));

        // Expanding the subarray in both
        // directions with equal length
        // so that mid point remains same
        while (prev >= 0 && next < n) {

            // Update both the scores
            straightScore
                += (a[prev] * b[prev]
                    + a[next] * b[next]);
            reverseScore
                += (a[prev] * b[next]
                    + a[next] * b[prev]);

            res = max(res,
                      max(straightScore,
                          reverseScore));

            prev--;
            next++;
        }

        // Consider the case of
        // even length subarray
        straightScore = 0;
        reverseScore = 0;

        prev = mid - 1, next = mid;
        while (prev >= 0 && next < n) {

            // Update both the scores
            straightScore
                += (a[prev] * b[prev]
                    + a[next] * b[next]);
            reverseScore
                += (a[prev] * b[next]
                    + a[next] * b[prev]);

            res = max(res,
                      max(straightScore,
                          reverseScore));

            prev--;
            next++;
        }
    }

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    int A[] = { 13, 4, 5 };
    int B[] = { 10, 22, 2 };
    int N = sizeof(A) / sizeof(A[0]);
    maxScoreSubArray(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG {
    // Function to calculate the score
    // of same-indexed subarrays selected
    // from the arrays a[] and b[]
    static void maxScoreSubArray(int[] a, int[] b, int n)
    {
        // Store the required result
        int res = 0;

        // Iterate in the range [0, N-1]
        for (int mid = 0; mid < n; mid++) {

            // Consider the case of odd
            // length subarray
            int straightScore = a[mid] * b[mid],
                reverseScore = a[mid] * a[mid];
            int prev = mid - 1, next = mid + 1;

            // Update the maximum score
            res = Math.max(
                res, Math.max(straightScore, reverseScore));

            // Expanding the subarray in both
            // directions with equal length
            // so that mid point remains same
            while (prev >= 0 && next < n) {

                // Update both the scores
                straightScore += (a[prev] * b[prev]
                                  + a[next] * b[next]);
                reverseScore += (a[prev] * b[next]
                                 + a[next] * b[prev]);

                res = Math.max(res, Math.max(straightScore,
                                             reverseScore));

                prev--;
                next++;
            }

            // Consider the case of
            // even length subarray
            straightScore = 0;
            reverseScore = 0;

            prev = mid - 1;
            next = mid;
            while (prev >= 0 && next < n) {

                // Update both the scores
                straightScore += (a[prev] * b[prev]
                                  + a[next] * b[next]);
                reverseScore += (a[prev] * b[next]
                                 + a[next] * b[prev]);

                res = Math.max(res, Math.max(straightScore,
                                             reverseScore));

                prev--;
                next++;
            }
        }

        // Print the result
        System.out.println(res);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 13, 4, 5 };
        int B[] = { 10, 22, 2 };
        int N = A.length;
        maxScoreSubArray(A, B, N);
    }
}

        // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the score
# of same-indexed subarrays selected
# from the arrays a[] and b[]
def maxScoreSubArray(a, b, n):

    # Store the required result
    res = 0

    # Iterate in the range [0, N-1]
    for mid in range(n):

        # Consider the case of odd
        # length subarray
        straightScore = a[mid] * b[mid]
        reverseScore = a[mid] * a[mid]
        prev = mid - 1
        next = mid + 1

        # Update the maximum score
        res = max(res, max(straightScore,
                           reverseScore))

        # Expanding the subarray in both
        # directions with equal length
        # so that mid poremains same
        while (prev >= 0 and next < n):

            # Update both the scores
            straightScore += (a[prev] * b[prev] +
                              a[next] * b[next])
            reverseScore += (a[prev] * b[next] +
                             a[next] * b[prev])

            res = max(res, max(straightScore,
                               reverseScore))

            prev -= 1
            next += 1

        # Consider the case of
        # even length subarray
        straightScore = 0
        reverseScore = 0

        prev = mid - 1
        next = mid

        while (prev >= 0 and next < n):

            # Update both the scores
            straightScore += (a[prev] * b[prev] +
                              a[next] * b[next])
            reverseScore += (a[prev] * b[next] +
                             a[next] * b[prev])

            res = max(res, max(straightScore,
                               reverseScore))

            prev -= 1
            next += 1

    # Print the result
    print(res)

# Driver Code
if __name__ == '__main__':

    A = [ 13, 4, 5 ]
    B = [ 10, 22, 2 ]
    N = len(A)

    maxScoreSubArray(A, B, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program for the above approach
using System;

public class GFG{

    // Function to calculate the score
    // of same-indexed subarrays selected
    // from the arrays a[] and b[]
    static void maxScoreSubArray(int[] a, int[] b, int n)
    {

        // Store the required result
        int res = 0;

        // Iterate in the range [0, N-1]
        for (int mid = 0; mid < n; mid++) {

            // Consider the case of odd
            // length subarray
            int straightScore = a[mid] * b[mid],
                reverseScore = a[mid] * a[mid];
            int prev = mid - 1, next = mid + 1;

            // Update the maximum score
            res = Math.Max(
                res, Math.Max(straightScore, reverseScore));

            // Expanding the subarray in both
            // directions with equal length
            // so that mid point remains same
            while (prev >= 0 && next < n) {

                // Update both the scores
                straightScore += (a[prev] * b[prev]
                                  + a[next] * b[next]);
                reverseScore += (a[prev] * b[next]
                                 + a[next] * b[prev]);

                res = Math.Max(res, Math.Max(straightScore,
                                             reverseScore));

                prev--;
                next++;
            }

            // Consider the case of
            // even length subarray
            straightScore = 0;
            reverseScore = 0;

            prev = mid - 1;
            next = mid;
            while (prev >= 0 && next < n) {

                // Update both the scores
                straightScore += (a[prev] * b[prev]
                                  + a[next] * b[next]);
                reverseScore += (a[prev] * b[next]
                                 + a[next] * b[prev]);

                res = Math.Max(res, Math.Max(straightScore,
                                             reverseScore));

                prev--;
                next++;
            }
        }

        // Print the result
        Console.WriteLine(res);
    }

    // Driver Code  
    static public void Main (){

        int[] A = { 13, 4, 5 };
        int[] B = { 10, 22, 2 };
        int N = A.Length;
        maxScoreSubArray(A, B, N);

    }
}

// This code is contributed by patel2127.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the score
// of same-indexed subarrays selected
// from the arrays a[] and b[]
function maxScoreSubArray(a, b, n) {
    // Store the required result
    let res = 0;

    // Iterate in the range [0, N-1]
    for (let mid = 0; mid < n; mid++) {

        // Consider the case of odd
        // length subarray
        let straightScore = a[mid] * b[mid],
            reverseScore = a[mid] * a[mid];
        let prev = mid - 1, next = mid + 1;

        // Update the maximum score
        res = Math.max(res, Math.max(straightScore,
            reverseScore));

        // Expanding the subarray in both
        // directions with equal length
        // so that mid point remains same
        while (prev >= 0 && next < n) {

            // Update both the scores
            straightScore
                += (a[prev] * b[prev]
                    + a[next] * b[next]);
            reverseScore
                += (a[prev] * b[next]
                    + a[next] * b[prev]);

            res = Math.max(res,
                Math.max(straightScore,
                    reverseScore));

            prev--;
            next++;
        }

        // Consider the case of
        // even length subarray
        straightScore = 0;
        reverseScore = 0;

        prev = mid - 1, next = mid;
        while (prev >= 0 && next < n) {

            // Update both the scores
            straightScore
                += (a[prev] * b[prev]
                    + a[next] * b[next]);
            reverseScore
                += (a[prev] * b[next]
                    + a[next] * b[prev]);

            res = Math.max(res,
                Math.max(straightScore,
                    reverseScore));

            prev--;
            next++;
        }
    }

    // Print the result
    document.write(res);
}

// Driver Code

let A = [13, 4, 5];
let B = [10, 22, 2];
let N = A.length
maxScoreSubArray(A, B, N);

</script>
```

**Output:** 

```
326
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
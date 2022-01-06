# K 次查询重排数组后的最大和

> 原文:[https://www . geeksforgeeks . org/k 查询重排数组后的最大和/](https://www.geeksforgeeks.org/maximum-sum-after-rearranging-the-array-for-k-queries/)

给定包含 **N** 整数的两个数组 **arr[]** 和包含 **K** 查询的 **Q[][]** ，其中每个查询代表一个范围**【L，R】**。任务是重新排列数组并找到所有子数组的最大可能和，其中每个子数组由每个查询给出的范围**【L，R】**中的数组元素定义。
**注意:**在 **Q[][]** 数组中使用基于 1 的索引来表示范围。
**举例:**

> **输入:** arr[] = { 2，6，10，1，5，6}，Q[][2] = {{1，3}，{4，6 }，{3，4}}
> **输出:** 46
> **解释:**
> 一种可能的方法是将数组重新排列为 arr[] = { 2，6，10，6，5，1}。
> 在此排列中:
> 范围[1，3] = 2 + 6 + 10 = 18 的子阵列之和。
> 范围[4，6] = 6 + 5 + 1 = 12 的子阵之和。
> 范围[3，4] = 10 + 6 = 16 的子阵列之和。
> 所有子阵列的总和= 46，这是最大可能值。
> **输入:** arr[] = { 1，2，3，4，5，6，7，8}，Q[][2] = {{1，4}，{5，5}，{7，8}，{8，8}}
> **输出:** 43
> **解释:**
> 一种可能的方法是将数组重新排列为 arr[] = {2，3，4，5，6，1，7，8 }。
> 在这种排列中:
> 子阵列在[1，4] = 2 + 3 + 4 + 5 = 14 范围内的和。
> 范围[5，5] = 6 = 6 的子阵之和。
> 范围[7，8] = 7 + 8 = 15 的子阵之和。
> 范围[8，8] = 8 = 8 的子阵之和。
> 所有子阵列的总和= 43，这是最大可能值。

**方法:**在观察清楚的情况下，可以得出一个结论:当最大元素包含在尽可能多的子阵中时，我们得到最大和。为此，我们需要通过迭代所有查询来找到每个索引被包含的次数。
**例如:**让数组为 **arr[] = {2，6，10，6，5，1}** ，查询为 **Q[][] = {{1，3}，{4，6}，{3，4}}** 。

1.  **第一步:**创建一个 n 大小的计数数组 **C[]** 所以，最初，计数数组 **C[] = {0，0，0，0，0，0}** 。
2.  **步骤 2:** 对于查询**【1，3】**，索引【1，3】处的元素增加 1。该查询后的计数数组变为 **{1，1，1，0，0，0}** 。
3.  **第三步:**同样，对于下一个查询，计数数组变为{1，1，1，1，1，1}，最后，在第三个查询之后，计数数组变为 **{1，1，2，2，1，1}** 。
4.  **第四步:**获取计数数组后，思路是用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)得到最大和。
5.  **第五步:**排序后，数组 **C[] = {1，1，1，1，2，2}** 和 **arr[] = {1，2，5，6，6，10}** 。**最大可能和是两个数组**的加权和，即:

> 总和=((1 * 1)+(1 * 2)+(1 * 5)+(1 * 6)+(2 * 6)+(2 * 10))= 46

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum sum
// after rearranging the array for K queries

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum after
// rearranging array elements
int maxSumArrangement(int A[], int R[][2],
                      int N, int M)
{

    // Auxiliary array to find the
    // count of each selected elements
    int count[N];

    // Initialize with 0
    memset(count, 0, sizeof count);

    // Finding count of every element
    // to be selected
    for (int i = 0; i < M; ++i) {

        int l = R[i][0], r = R[i][1] + 1;

        // Making it to 0-indexing
        l--;
        r--;

        // Prefix sum array concept is used
        // to obtain the count array
        count[l]++;

        if (r < N)
            count[r]--;
    }

    // Iterating over the count array
    // to get the final array
    for (int i = 1; i < N; ++i) {
        count[i] += count[i - 1];
    }
for (int i = 0; i < N; ++i) {
cout<<count[i];
}
    // Variable to store the maximum sum
    int ans = 0;

    // Sorting both the arrays
    sort(count, count + N);
    sort(A, A + N);

  for (int i = 0; i < N; ++i) {
cout<<endl<<A[i];
}
    // Loop to find the maximum sum
    for (int i = N - 1; i >= 0; --i) {
        ans += A[i] * count[i];
    }

    return ans;
}

// Driver code
int main()
{
    int A[] = { 2, 6, 10, 1, 5, 6 };
    int R[][2]
        = { { 1, 3 }, { 4, 6 }, { 3, 4 } };

    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(R) / sizeof(R[0]);

    cout << maxSumArrangement(A, R, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum sum
// after rearranging the array for K queries
import java.util.*;

class GFG
{

    // Function to find maximum sum after
    // rearranging array elements
    static int maxSumArrangement(int A[], int R[][],
                          int N, int M)
    {

        // Auxiliary array to find the
        // count of each selected elements
        int count[] = new int[N];
        int i;

        // Finding count of every element
        // to be selected
        for ( i = 0; i < M; ++i) {

            int l = R[i][0], r = R[i][1] + 1;

            // Making it to 0-indexing
            l--;
            r--;

            // Prefix sum array concept is used
            // to obtain the count array
            count[l]++;

            if (r < N)
                count[r]--;
        }

        // Iterating over the count array
        // to get the final array
        for (i = 1; i < N; ++i) {
            count[i] += count[i - 1];
        }

        // Variable to store the maximum sum
        int ans = 0;

        // Sorting both the arrays
        Arrays.sort( count);
        Arrays.sort(A);

        // Loop to find the maximum sum
        for (i = N - 1; i >= 0; --i) {
            ans += A[i] * count[i];
        }

        return ans;
    }

    // Driver code
    public static void main(String []args)
    {
        int A[] = { 2, 6, 10, 1, 5, 6 };
        int R[][]
            = { { 1, 3 }, { 4, 6 }, { 3, 4 } };

        int N = A.length;
        int M = R.length;

        System.out.print(maxSumArrangement(A, R, N, M));

    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to find the maximum sum
# after rearranging the array for K queries

# Function to find maximum sum after
# rearranging array elements
def maxSumArrangement( A,  R,  N,  M):

    # Auxiliary array to find the
    # count of each selected elements
    # Initialize with 0
    count = [0 for i in range(N)]

    # Finding count of every element
    # to be selected
    for i in range(M):

        l = R[i][0]
        r = R[i][1] + 1

        # Making it to 0-indexing
        l = l - 1
        r = r - 1

        # Prefix sum array concept is used
        # to obtain the count array
        count[l] = count[l] + 1

        if (r < N):
            count[r] = count[r] - 1

    # Iterating over the count array
    # to get the final array
    for i in range(1, N):
        count[i] = count[i] + count[i - 1]

    # Variable to store the maximum sum
    ans = 0

    # Sorting both the arrays
    count.sort()
    A.sort()

    # Loop to find the maximum sum
    for i in range(N - 1, -1, -1):
        ans = ans + A[i] * count[i]

    return ans

# Driver code
A = [ 2, 6, 10, 1, 5, 6 ]
R = [ [ 1, 3 ], [ 4, 6 ], [ 3, 4 ] ]

N = len(A)
M = len(R)

print(maxSumArrangement(A, R, N, M))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find the maximum sum
// after rearranging the array for K queries
using System;

class GFG
{

    // Function to find maximum sum after
    // rearranging array elements
    static int maxSumArrangement(int []A, int [,]R,
                          int N, int M)
    {

        // Auxiliary array to find the
        // count of each selected elements
        int []count = new int[N];
        int i;

        // Finding count of every element
        // to be selected
        for ( i = 0; i < M; ++i) {

            int l = R[i, 0], r = R[i, 1] + 1;

            // Making it to 0-indexing
            l--;
            r--;

            // Prefix sum array concept is used
            // to obtain the count array
            count[l]++;

            if (r < N)
                count[r]--;
        }

        // Iterating over the count array
        // to get the readonly array
        for (i = 1; i < N; ++i) {
            count[i] += count[i - 1];
        }

        // Variable to store the maximum sum
        int ans = 0;

        // Sorting both the arrays
        Array.Sort( count);
        Array.Sort(A);

        // Loop to find the maximum sum
        for (i = N - 1; i >= 0; --i) {
            ans += A[i] * count[i];
        }

        return ans;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []A = { 2, 6, 10, 1, 5, 6 };
        int [,]R
            = { { 1, 3 }, { 4, 6 }, { 3, 4 } };

        int N = A.Length;
        int M = R.GetLength(0);

        Console.Write(maxSumArrangement(A, R, N, M));     
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
//Javascript program to find the maximum sum
// after rearranging the array for K queries

//function to sort a array
function arrSort(a, n) {
   var i, j, min, temp;
   for (i = 0; i < n - 1; i++) {
      min = i;
      for (j = i + 1; j < n; j++)
      if (a[j] < a[min])
      min = j;
      temp = a[i];
      a[i] = a[min];
      a[min] = temp;
   }
}

// Function to find maximum sum after
// rearranging array elements
function maxSumArrangement(A, R, N, M)
{

    // Auxiliary array to find the
    // count of each selected elements
    var count = new Array(N);

    // Initialize with 0
    count.fill(0);

    // Finding count of every element
    // to be selected
    for (var i = 0; i < M; i++) {

        var l = R[i][0], r = R[i][1] + 1;

        // Making it to 0-indexing
        l--;
        r--;

        // Prefix sum array concept is used
        // to obtain the count array
        count[l]++;

        if (r < N)
            count[r]--;
    }

    // Iterating over the count array
    // to get the final array
    for (var i = 1; i < N; ++i) {
        count[i] += count[i - 1];
    }

    // Variable to store the maximum sum
    var ans = 0;

    // Sorting both the arrays
    count.sort();
    arrSort(A,N);

    // Loop to find the maximum sum
    for (var i = N - 1; i >= 0; --i) {
        ans += A[i] * count[i];
    }

    return ans;
}

var A = [ 2, 6, 10, 1, 5, 6 ];
var R = [ [ 1, 3 ], [ 4, 6 ], [ 3, 4 ] ];
var N = A.length;
var M = R.length;
document.write( maxSumArrangement(A, R, N, M));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
46
```

***时间复杂度:** O(N* log(N))*
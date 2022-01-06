# 总和在[L，R]范围内且最大和最小元素之差至少为 X 的子序列的计数

> 原文:[https://www . geesforgeks . org/带范围内和的子序列计数-l-r-和-最大和最小元素差-至少-x/](https://www.geeksforgeeks.org/count-of-subsequences-with-a-sum-in-range-l-r-and-difference-between-max-and-min-element-at-least-x/)

给定由 **N** 正整数和 **3** 整数**L****R**和 **X** 组成的[数组**arr【】**，任务是找出大小至少为 2 的](https://www.geeksforgeeks.org/array-data-structure/)[子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的数量，其和在**【L，R】**的范围内，最大和最小元素之间的差至少为 **X**

**示例:**

> **输入:** arr[] = {1 2 3}，L = 5，R = 6，X = 1
> **输出:** 2
> **解释:**
> 有两个可能的子序列，即{2，3}和{1，2，3}。
> 
> **输入:** arr[] = {10，20，30，25}，L = 40，R = 50，X = 10
> **输出:** 2

**方法:**由于 **N** 较小，这个问题可以使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)解决。共有 **2 <sup>n</sup>** [个子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)种可能。因此，每个子序列可以用一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) 来表示，即**掩码**，其中如果第**和**位被**设置为**，即 **1** ，则该元素在[子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)中被考虑，否则不被考虑。按照以下步骤解决问题:

*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，2<sup>n</sup>–1】**中迭代，并执行以下步骤:
    *   初始化一个变量，比如说 **cnt** 为 **0** 和 **sum** 为 **0** 来存储所选元素的总和。
    *   初始化一个变量，比如说 **minVal** 为 **INT_MAX** 和 **maxVal** 为 **INT_MIN** 来存储子序列中的最小值和最大值。
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
        *   如果带掩码的**的 **jth** 位打开，那么将 **cnt** 增加 **1，**将**arr【j】**加到**和**上，并将 **maxVal** 更新为 **maxVal** 和**a【j】**的最大值，将 **minVal** 更新为 **minVal 的最小值****
    *   如果 **cnt > = 2** 和**之和**在**【L，R】**的范围内，且 **maxVal** 和 **minVal** 之差大于等于 **X** ，则 **ans** 增加 **1。**
*   完成以上步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of subsequences
// of the given array with a sum in range [L, R]
// and the difference between the maximum and
// minimum element is at least X
int numberofSubsequences(int a[], int L,
                         int R, int X, int n)
{
    // Initialize answer as 0
    int ans = 0;

    // Creating mask from [0, 2^n-1]
    for (int i = 0; i < (1 << n); i++) {

        // Stores the count and sum of
        // selected elements respectively
        int cnt = 0, sum = 0;

        // Variables to store the value of
        // Minimum and maximum element
        int minVal = INT_MAX, maxVal = INT_MIN;

        // Traverse the array
        for (int j = 0; j < n; j++) {
            // If the jth bit of the ith
            // mask is on
            if ((i & (1 << j))) {

                cnt += 1;

                // Add the selected element
                sum += a[j];

                // Update maxVal and minVal value
                maxVal = max(maxVal, a[j]);
                minVal = min(minVal, a[j]);
            }
        }

        // Check if the given conditions are
        // true, increment ans by 1.
        if (cnt >= 2 && sum >= L && sum <= R
            && (maxVal - minVal >= X)) {
            ans += 1;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int a[] = { 10, 20, 30, 25 };
    int L = 40, R = 50, X = 10;
    int N = sizeof(a) / sizeof(a[0]);

    // Function Call
    cout << numberofSubsequences(a, L, R, X, N)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to find the number of subsequences
    // of the given array with a sum in range [L, R]
    // and the difference between the maximum and
    // minimum element is at least X
    static int numberofSubsequences(int a[], int L, int R,
                                    int X, int n)
    {
        // Initialize answer as 0
        int ans = 0;

        // Creating mask from [0, 2^n-1]
        for (int i = 0; i < (1 << n); i++) {

            // Stores the count and sum of
            // selected elements respectively
            int cnt = 0, sum = 0;

            // Variables to store the value of
            // Minimum and maximum element
            int minVal = Integer.MAX_VALUE,
                maxVal = Integer.MIN_VALUE;

            // Traverse the array
            for (int j = 0; j < n; j++) {
                // If the jth bit of the ith
                // mask is on
                if ((i & (1 << j)) == 0) {

                    cnt += 1;

                    // Add the selected element
                    sum += a[j];

                    // Update maxVal and minVal value
                    maxVal = Math.max(maxVal, a[j]);
                    minVal = Math.min(minVal, a[j]);
                }
            }

            // Check if the given conditions are
            // true, increment ans by 1.
            if (cnt >= 2 && sum >= L && sum <= R
                && (maxVal - minVal >= X)) {
                ans += 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 10, 20, 30, 25 };
        int L = 40, R = 50, X = 10;
        int N = a.length;

        // Function Call
        System.out.println(
            numberofSubsequences(a, L, R, X, N));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the number of subsequences
# of the given array with a sum in range [L, R]
# and the difference between the maximum and
# minimum element is at least X
def numberofSubsequences(a, L, R, X, n):

    # Initialize answer as 0
    ans = 0

    # Creating mask from [0, 2^n-1]
    for i in range(0, (1 << n), 1):

        # Stores the count and sum of
        # selected elements respectively
        cnt = 0
        sum = 0

        # Variables to store the value of
        # Minimum and maximum element
        minVal = sys.maxsize
        maxVal = -sys.maxsize - 1

        # Traverse the array
        for j in range(n):

            # If the jth bit of the ith
            # mask is on
            if ((i & (1 << j))):
                cnt += 1

                # Add the selected element
                sum += a[j]

                # Update maxVal and minVal value
                maxVal = max(maxVal, a[j])
                minVal = min(minVal, a[j])

        # Check if the given conditions are
        # true, increment ans by 1.
        if (cnt >= 2 and sum >= L and
            sum <= R and (maxVal - minVal >= X)):
            ans += 1

    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    a = [ 10, 20, 30, 25 ]
    L = 40
    R = 50
    X = 10
    N = len(a)

    # Function Call
    print(numberofSubsequences(a, L, R, X, N))

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number of subsequences
// of the given array with a sum in range [L, R]
// and the difference between the maximum and
// minimum element is at least X
static int numberofSubsequences(int[] a, int L, int R,
                                int X, int n)
{

    // Initialize answer as 0
    int ans = 0;

    // Creating mask from [0, 2^n-1]
    for(int i = 0; i < (1 << n); i++)
    {

        // Stores the count and sum of
        // selected elements respectively
        int cnt = 0, sum = 0;

        // Variables to store the value of
        // Minimum and maximum element
        int minVal = Int32.MaxValue,
            maxVal = Int32.MinValue;

        // Traverse the array
        for(int j = 0; j < n; j++)
        {

            // If the jth bit of the ith
            // mask is on
            if ((i & (1 << j)) == 0)
            {
                cnt += 1;

                // Add the selected element
                sum += a[j];

                // Update maxVal and minVal value
                maxVal = Math.Max(maxVal, a[j]);
                minVal = Math.Min(minVal, a[j]);
            }
        }

        // Check if the given conditions are
        // true, increment ans by 1.
        if (cnt >= 2 && sum >= L && sum <= R &&
           (maxVal - minVal >= X))
        {
            ans += 1;
        }
    }
    return ans;
}

// Driver Code
static public void Main()
{
    // Given input
    int[] a = { 10, 20, 30, 25 };
    int L = 40, R = 50, X = 10;
    int N = a.Length;

    // Function Call
    Console.Write(numberofSubsequences(a, L, R, X, N));
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of subsequences
// of the given array with a sum in range [L, R]
// and the difference between the maximum and
// minimum element is at least X
function numberofSubsequences(a, L, R, X, n)
{

    // Initialize answer as 0
    let ans = 0;

    // Creating mask from [0, 2^n-1]
    for (let i = 0; i < (1 << n); i++) {

        // Stores the count and sum of
        // selected elements respectively
        let cnt = 0, sum = 0;

        // Variables to store the value of
        // Minimum and maximum element
        let minVal = Number.MAX_SAFE_INTEGER, maxVal = Number.MIN_SAFE_INTEGER;

        // Traverse the array
        for (let j = 0; j < n; j++)
        {

            // If the jth bit of the ith
            // mask is on
            if ((i & (1 << j)))
            {

                cnt += 1;

                // Add the selected element
                sum += a[j];

                // Update maxVal and minVal value
                maxVal = Math.max(maxVal, a[j]);
                minVal = Math.min(minVal, a[j]);
            }
        }

        // Check if the given conditions are
        // true, increment ans by 1.
        if (cnt >= 2 && sum >= L && sum <= R
            && (maxVal - minVal >= X)) {
            ans += 1;
        }
    }
    return ans;
}

// Driver Code

// Given Input
let a = [10, 20, 30, 25];
let L = 40, R = 50, X = 10;
let N = a.length;

// Function Call
document.write(numberofSubsequences(a, L, R, X, N) + "<br>");

// This code is contributed by gfgking.
</script>
```

**Output**

```
2
```

***时间复杂度:**O(N×2<sup>N</sup>)*
***辅助空间:** O(1)*
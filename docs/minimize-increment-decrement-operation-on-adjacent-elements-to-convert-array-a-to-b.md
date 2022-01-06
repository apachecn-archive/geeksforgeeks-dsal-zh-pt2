# 最小化相邻元素的递增-递减操作，将数组 A 转换为数组 B

> 原文:[https://www . geesforgeks . org/minimum-increment-减量-operation-on-neighbor-elements-convert-array-a-b/](https://www.geeksforgeeks.org/minimize-increment-decrement-operation-on-adjacent-elements-to-convert-array-a-to-b/)

给定两个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是找到将数组**A【】**转换为数组**B【】**所需的数组相邻元素的最小增量和减量数。如果不可能，则打印【T12 "-1 "。

**示例:**

> **输入:** A[] = {1，2}，B[] = {2，1}
> **输出:** 1
> **解释:**
> 对数组 A[]:执行以下操作:
> 
> 1.  考虑相邻对 **(arr[0]，arr[1])** ，在递增和递减对之后，将数组 A[]修改为{2，1}。
> 
> 上述运算后，数组 A[] = {2，1}等于 B，所需的最小运算次数为 1。
> 
> **输入:** A[] = {1，0，0}，B[] = {2，3，1}
> **输出:** -1

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

*   可以观察到，如果数组 **A[]** 和 **B[]** 的和不相等，则不存在有效的操作序列。在这种情况下，答案将是 **-1** 。
*   否则，[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** ，根据以下情况执行以下步骤:
    1.  **A[i] > B[i]:** 的情况
        *   在这种情况下，跟踪额外的值(即**A[I]–B[I]**)使用来自**【I–1，0】**的指针 **j** 进行迭代，并将额外的值不断添加到索引中，直到 **A[j] < B[j]** 直到额外的值耗尽**(A[I]–B[I]**变为 **0** )或者数组结束同样，向右遍历**【I+1，N–1】**，继续添加额外的值。
        *   记录变量中的移动次数，并将 **1** 从索引 **i** 转移到索引 **j** ，所需的最小操作次数为**| I–j |**。
    2.  **A[i] < = B[i]** 的情况。在这种情况下，迭代到 **i** 的下一个值，因为在上述情况下迭代时会考虑这些索引。

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of operations to convert
// array A to array B by incrementing
// and decrementing adjacent elements
int minimumMoves(int A[], int B[], int N)
{
    // Stores the final count
    int ans = 0;

    // Stores the sum of array A
    // and B respectivelly
    int sum_A = 0, sum_B = 0;
    for (int i = 0; i < N; i++) {
        sum_A += A[i];
    }
    for (int i = 0; i < N; i++) {
        sum_B += B[i];
    }

    // Check of the sums are unequal
    if (sum_A != sum_B) {
        return -1;
    }

    // Pointer to iterate through array
    int i = 0;

    while (i < N) {

        // Case 1 where A[i] > B[i]
        if (A[i] > B[i]) {

            // Stores the extra values
            // for the current index
            int temp = A[i] - B[i];
            int j = i - 1;

            // Iterate the array from [i-1, 0]
            while (j >= 0 && temp > 0) {
                if (B[j] > A[j]) {

                    // Stores the count of
                    // values being transferred
                    // from A[i] to A[j]
                    int cnt = min(temp, (B[j] - A[j]));
                    A[j] += cnt;
                    temp -= cnt;

                    // Add operation count
                    ans += (cnt * abs(j - i));
                }
                j--;
            }

            // Iterate the array in right
            // direction id A[i]-B[i] > 0
            if (temp > 0) {
                int j = i + 1;

                // Iterate the array from [i+1, n-1]
                while (j < N && temp > 0) {
                    if (B[j] > A[j]) {

                        // Stores the count of
                        // values being transferred
                        // from A[i] to A[j]
                        int cnt = min(temp, (B[j] - A[j]));
                        A[j] += cnt;
                        temp -= cnt;

                        // Add operation count
                        ans += (cnt * abs(j - i));
                    }
                    j++;
                }
            }
        }
        i++;
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int A[] = { 1, 5, 7 };
    int B[] = { 13, 0, 0 };
    int N = sizeof(A) / sizeof(int);

    // Function Call
    cout << minimumMoves(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to calculate the minimum
    // number of operations to convert
    // array A to array B by incrementing
    // and decrementing adjacent elements
    static int minimumMoves(int A[], int B[], int N)
    {

        // Stores the final count
        int ans = 0;

        // Stores the sum of array A
        // and B respectivelly
        int sum_A = 0, sum_B = 0;
        for (int i = 0; i < N; i++) {
            sum_A += A[i];
        }
        for (int i = 0; i < N; i++) {
            sum_B += B[i];
        }

        // Check of the sums are unequal
        if (sum_A != sum_B) {
            return -1;
        }

        // Pointer to iterate through array
        int i = 0;

        while (i < N) {

            // Case 1 where A[i] > B[i]
            if (A[i] > B[i]) {

                // Stores the extra values
                // for the current index
                int temp = A[i] - B[i];
                int j = i - 1;

                // Iterate the array from [i-1, 0]
                while (j >= 0 && temp > 0) {
                    if (B[j] > A[j]) {

                        // Stores the count of
                        // values being transferred
                        // from A[i] to A[j]
                        int cnt
                            = Math.min(temp, (B[j] - A[j]));
                        A[j] += cnt;
                        temp -= cnt;

                        // Add operation count
                        ans += (cnt * Math.abs(j - i));
                    }
                    j--;
                }

                // Iterate the array in right
                // direction id A[i]-B[i] > 0
                if (temp > 0) {
                     j = i + 1;

                    // Iterate the array from [i+1, n-1]
                    while (j < N && temp > 0) {
                        if (B[j] > A[j]) {

                            // Stores the count of
                            // values being transferred
                            // from A[i] to A[j]
                            int cnt = Math.min(
                                temp, (B[j] - A[j]));
                            A[j] += cnt;
                            temp -= cnt;

                            // Add operation count
                            ans += (cnt * Math.abs(j - i));
                        }
                        j++;
                    }
                }
            }
            i++;
        }

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 1, 5, 7 };
        int B[] = { 13, 0, 0 };
        int N = A.length;

        // Function Call
        System.out.println(minimumMoves(A, B, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 Program of the above approach

# Function to calculate the minimum
# number of operations to convert
# array A to array B by incrementing
# and decrementing adjacent elements
def minimumMoves(A, B, N):

    # Stores the final count
    ans = 0

    # Stores the sum of array A
    # and B respectivelly
    sum_A = 0
    sum_B = 0
    for i in range(N):
        sum_A += A[i]
    for i in range(N):
        sum_B += B[i]

    # Check of the sums are unequal
    if (sum_A != sum_B):
        return -1

    # Pointer to iterate through array
    i = 0

    while (i < N):
        # Case 1 where A[i] > B[i]
        if (A[i] > B[i]):
            # Stores the extra values
            # for the current index
            temp = A[i] - B[i]
            j = i - 1

            # Iterate the array from [i-1, 0]
            while (j >= 0 and temp > 0):
                if (B[j] > A[j]):

                    # Stores the count of
                    # values being transferred
                    # from A[i] to A[j]
                    cnt = min(temp, (B[j] - A[j]))
                    A[j] += cnt
                    temp -= cnt

                    # Add operation count
                    ans += (cnt * abs(j - i))
                j -= 1

            # Iterate the array in right
            # direction id A[i]-B[i] > 0
            if (temp > 0):
                j = i + 1

                # Iterate the array from [i+1, n-1]
                while (j < N and temp > 0):
                    if (B[j] > A[j]):

                        # Stores the count of
                        # values being transferred
                        # from A[i] to A[j]
                        cnt = min(temp, (B[j] - A[j]))
                        A[j] += cnt
                        temp -= cnt

                        # Add operation count
                        ans += (cnt * abs(j - i))
                    j += 1
        i += 1

    # Return Answer
    return ans

# Driver Code
if __name__ == '__main__':
    A = [1, 5, 7]
    B = [13, 0, 0]
    N = len(A)

    # Function Call
    print(minimumMoves(A, B, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach

using System;

public class GFG
{

    // Function to calculate the minimum
    // number of operations to convert
    // array A to array B by incrementing
    // and decrementing adjacent elements
    static int minimumMoves(int []A, int []B, int N)
    {

        // Stores the final count
        int ans = 0;

        // Stores the sum of array A
        // and B respectivelly
        int sum_A = 0, sum_B = 0;
        for (int i = 0; i < N; i++) {
            sum_A += A[i];
        }
        for (int i = 0; i < N; i++) {
            sum_B += B[i];
        }

        // Check of the sums are unequal
        if (sum_A != sum_B) {
            return -1;
        }

        // Pointer to iterate through array
        int k = 0;

        while (k < N) {

            // Case 1 where A[i] > B[i]
            if (A[k] > B[k]) {

                // Stores the extra values
                // for the current index
                int temp = A[k] - B[k];
                int j = k - 1;

                // Iterate the array from [i-1, 0]
                while (j >= 0 && temp > 0) {
                    if (B[j] > A[j]) {

                        // Stores the count of
                        // values being transferred
                        // from A[i] to A[j]
                        int cnt
                            = Math.Min(temp, (B[j] - A[j]));
                        A[j] += cnt;
                        temp -= cnt;

                        // Add operation count
                        ans += (cnt * Math.Abs(j - k));
                    }
                    j--;
                }

                // Iterate the array in right
                // direction id A[i]-B[i] > 0
                if (temp > 0) {
                     j = k + 1;

                    // Iterate the array from [i+1, n-1]
                    while (j < N && temp > 0) {
                        if (B[j] > A[j]) {

                            // Stores the count of
                            // values being transferred
                            // from A[i] to A[j]
                            int cnt = Math.Min(
                                temp, (B[j] - A[j]));
                            A[j] += cnt;
                            temp -= cnt;

                            // Add operation count
                            ans += (cnt * Math.Abs(j - k));
                        }
                        j++;
                    }
                }
            }
            k++;
        }

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int []A = { 1, 5, 7 };
        int []B = { 13, 0, 0 };
        int N = A.Length;

        // Function Call
        Console.WriteLine(minimumMoves(A, B, N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript Program of the above approach

// Function to calculate the minimum
// number of operations to convert
// array A to array B by incrementing
// and decrementing adjacent elements
function minimumMoves(A, B, N)
{
    // Stores the final count
    var ans = 0;
    var i;

    // Stores the sum of array A
    // and B respectivelly
    var sum_A = 0, sum_B = 0;
    for (i = 0; i < N; i++) {
        sum_A += A[i];
    }
    for (i = 0; i < N; i++) {
        sum_B += B[i];
    }

    // Check of the sums are unequal
    if (sum_A != sum_B) {
        return -1;
    }

    // Pointer to iterate through array
    var i = 0;

    while (i < N) {

        // Case 1 where A[i] > B[i]
        if (A[i] > B[i]) {

            // Stores the extra values
            // for the current index
            var temp = A[i] - B[i];
            var j = i - 1;

            // Iterate the array from [i-1, 0]
            while (j >= 0 && temp > 0) {
                if (B[j] > A[j]) {

                    // Stores the count of
                    // values being transferred
                    // from A[i] to A[j]
                    var cnt = Math.min(temp, (B[j] - A[j]));
                    A[j] += cnt;
                    temp -= cnt;

                    // Add operation count
                    ans += (cnt * Math.abs(j - i));
                }
                j--;
            }

            // Iterate the array in right
            // direction id A[i]-B[i] > 0
            if (temp > 0) {
                var j = i + 1;

                // Iterate the array from [i+1, n-1]
                while (j < N && temp > 0) {
                    if (B[j] > A[j]) {

                        // Stores the count of
                        // values being transferred
                        // from A[i] to A[j]
                        var cnt = Math.min(temp, (B[j] - A[j]));
                        A[j] += cnt;
                        temp -= cnt;

                        // Add operation count
                        ans += (cnt * Math.abs(j - i));
                    }
                    j++;
                }
            }
        }
        i++;
    }

    // Return Answer
    return ans;
}

// Driver Code
    var A = [1, 5, 7];
    var B = [13, 0, 0];
    var N = A.length;

    // Function Call
    document.write(minimumMoves(A, B, N));

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

**Output:** 

```
19
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
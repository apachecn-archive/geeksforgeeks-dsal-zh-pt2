# 最大化位于给定范围内的长度子序列的平均值之和

> 原文:[https://www . geeksforgeeks . org/最大化给定范围内长度子序列的平均值之和/](https://www.geeksforgeeks.org/maximize-sum-of-averages-of-subsequences-of-lengths-lying-in-a-given-range/)

给定一个由 **N** 个整数和两个整数 **X** 和 **Y** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是找出通过将数组拆分成长度在**【X，Y】**范围内的子序列而获得的每个子序列平均值的最大和。

**注:**的 **X** 和 **Y** 的值是这样的，总是可以组成这样的组。

**示例:**

> **输入:** A[] = {4，10，6，5}，X = 2，Y = 3
> **输出:** 12.50
> **解释:**
> 将给定的数组分成{4，10}，{6，5}两组，使它们的大小在范围[2，3]内。
> 第一组平均值= (4 + 10) / 2 = 7。
> 第二组平均值= (6 + 5) / 2 = 5.5。
> 因此，平均值之和= 7 + 5.5 = 12.5，这在所有可能的组中是最小的。
> 
> **输入:** A[] = {3，3，1 }
> T3】输出: 3.00

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。想法是[按照升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组进行排序，选择大小为 **X** 的组，因为平均值与元素数量成反比。最后，将剩余的元素添加到最后一组中。按照以下步骤解决问题:

*   [按升序排列给定数组 **arr[]**](https://www.geeksforgeeks.org/sorting-algorithms/) 。
*   初始化变量，说**和，res，**和**计数**为 **0** ，存储数组元素的[和，结果，以及当前组中元素](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的[计数。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   将**arr【I】**的值加到变量 **sum** 上，并将 **count** 的值增加 **1** 。
    *   如果 **count** 的值等于 **X** ，并且剩余的数组元素不能组成一个组，那么将它们添加到当前组，并在变量 **res** 中添加平均值。
    *   否则，在变量 **res** 中加上到目前为止形成的组的平均值。
*   完成以上步骤后，打印 **res** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
// of average of groups
void maxAverage(int A[], int N, int X,
                int Y)
{
    // Sort the given array
    sort(A, A + N);

    int sum = 0;

    // Stores the sum of averages
    double res = 0;

    // Stores count of array element
    int count = 0;

    for (int i = 0; i < N; i++) {

        // Add the current value to
        // the variable sum
        sum += A[i];

        // Increment the count by 1
        count++;

        // If the current size is X
        if (count == X) {

            // If the remaining elements
            // can't become a group
            if (N - i - 1 < X) {
                i++;
                int cnt = 0;

                // Iterate until i is
                // less than N
                while (i < N) {
                    cnt++;
                    sum += A[i];
                    i++;
                }

                // Update the value of X
                X = X + cnt;

                // Update the average
                res += (double)sum / double(X);
                break;
            }

            // Find the average
            res += (double)sum / double(X);

            // Reset the sum and count
            sum = 0;
            count = 0;
        }
    }

    // Print maximum sum of averages
    cout << fixed << setprecision(2)
         << res << "\n";
}

// Driver Code
int main()
{
    int A[] = { 4, 10, 6, 5 };
    int N = sizeof(A) / sizeof(A[0]);
    int X = 2, Y = 3;

    maxAverage(A, N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum sum
// of average of groups
static void maxAverage(int A[], int N, int X,
                       int Y)
{

    // Sort the given array
    Arrays.sort(A);

    int sum = 0;

    // Stores the sum of averages
    double res = 0;

    // Stores count of array element
    int count = 0;

    for(int i = 0; i < N; i++)
    {

        // Add the current value to
        // the variable sum
        sum += A[i];

        // Increment the count by 1
        count++;

        // If the current size is X
        if (count == X)
        {

            // If the remaining elements
            // can't become a group
            if (N - i - 1 < X)
            {
                i++;
                int cnt = 0;

                // Iterate until i is
                // less than N
                while (i < N)
                {
                    cnt++;
                    sum += A[i];
                    i++;
                }

                // Update the value of X
                X = X + cnt;

                // Update the average
                res += (double)sum / (double)(X);
                break;
            }

            // Find the average
            res += (double)sum / (double)(X);

            // Reset the sum and count
            sum = 0;
            count = 0;
        }
    }

    // Print maximum sum of averages
    System.out.println(res);
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 4, 10, 6, 5 };
    int N = A.length;
    int X = 2, Y = 3;

    maxAverage(A, N, X, Y);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum sum
# of average of groups
def maxAverage(A,N,X,Y):
    # Sort the given array
    A.sort()

    sum = 0

    # Stores the sum of averages
    res = 0

    # Stores count of array element
    count = 0

    for i in range(N):
        # Add the current value to
        # the variable sum
        sum += A[i]

        # Increment the count by 1
        count += 1

        # If the current size is X
        if (count == X):

            # If the remaining elements
            # can't become a group
            if (N - i - 1 < X):
                i += 1
                cnt = 0

                # Iterate until i is
                # less than N
                while (i < N):
                    cnt += 1
                    sum += A[i]
                    i += 1

                # Update the value of X
                X = X + cnt

                # Update the average
                res += sum / X
                break

            # Find the average
            res += sum / X

            # Reset the sum and count
            sum = 0
            count = 0

    # Print maximum sum of averages
    print(res)

# Driver Code
if __name__ == '__main__':
    A = [4, 10, 6, 5]
    N = len(A)
    X = 2
    Y = 3

    maxAverage(A, N, X, Y)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to find the maximum sum
// of average of groups
static void maxAverage(int []A, int N, int X,
                       int Y)
{

    // Sort the given array
    Array.Sort(A);

    int sum = 0;

    // Stores the sum of averages
    double res = 0;

    // Stores count of array element
    int count = 0;

    for(int i = 0; i < N; i++)
    {

        // Add the current value to
        // the variable sum
        sum += A[i];

        // Increment the count by 1
        count++;

        // If the current size is X
        if (count == X)
        {

            // If the remaining elements
            // can't become a group
            if (N - i - 1 < X)
            {
                i++;
                int cnt = 0;

                // Iterate until i is
                // less than N
                while (i < N)
                {
                    cnt++;
                    sum += A[i];
                    i++;
                }

                // Update the value of X
                X = X + cnt;

                // Update the average
                res += (double)sum / (double)(X);
                break;
            }

            // Find the average
            res += (double)sum / (double)(X);

            // Reset the sum and count
            sum = 0;
            count = 0;
        }
    }

    // Print maximum sum of averages
    Console.WriteLine(res);
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 4, 10, 6, 5 };
    int N = A.Length;
    int X = 2, Y = 3;

    maxAverage(A, N, X, Y);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the maximum sum
        // of average of groups
        function maxAverage(A, N, X, Y) {
            // Sort the given array
            A.sort(function (a, b) { return a - b; })

            let sum = 0;

            // Stores the sum of averages
            let res = 0;

            // Stores count of array element
            let count = 0;

            for (let i = 0; i < N; i++) {

                // Add the current value to
                // the variable sum
                sum += A[i];

                // Increment the count by 1
                count++;

                // If the current size is X
                if (count == X) {

                    // If the remaining elements
                    // can't become a group
                    if (N - i - 1 < X) {
                        i++;
                        let cnt = 0;

                        // Iterate until i is
                        // less than N
                        while (i < N) {
                            cnt++;
                            sum += A[i];
                            i++;
                        }

                        // Update the value of X
                        X = X + cnt;

                        // Update the average
                        res += sum / X;
                        break;
                    }

                    // Find the average
                    res += sum / X;

                    // Reset the sum and count
                    sum = 0;
                    count = 0;
                }
            }

            // Print maximum sum of averages
            document.write(res.toPrecision(3))

        }

        // Driver Code

        let A = [4, 10, 6, 5];
        let N = A.length;
        let X = 2, Y = 3;

        maxAverage(A, N, X, Y);

    // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
12.50
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*
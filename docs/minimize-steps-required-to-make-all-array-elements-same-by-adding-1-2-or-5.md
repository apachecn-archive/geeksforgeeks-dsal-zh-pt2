# 通过添加 1、2 或 5

来最小化使所有数组元素相同所需的步骤

> 原文:[https://www . geesforgeks . org/minimum-steps-要求通过添加-1-2-或-5 使所有数组元素相同/](https://www.geeksforgeeks.org/minimize-steps-required-to-make-all-array-elements-same-by-adding-1-2-or-5/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过在每一步将 **1、2、**或 **5** 精确地添加到数组的**(N–1)**元素来计算使所有数组元素相同所需的最小步数。

**示例:**

> **输入:** N = 4，arr[] = {2，2，3，7}
> **输出:** 2
> **解释:**
> 步骤 1: {2，2，3，7} - > {3，3，3，8}
> 步骤 2: {3，3，3，8} - > {8，8，8，8}
> 
> **输入:** N = 3，arr[] = {10，7，12 }
> T3】输出: 3

**天真方法:**最简单的方法是尝试所有可能的组合[递归地](https://www.geeksforgeeks.org/recursion/)相加数字 **1、2 和 5** 使得所有的元素变得相同，并计算所有这样的组合所需的步数。最后，打印其中最少的一个作为所需答案。

***时间复杂度:** O(M <sup>M</sup> ，其中 M 是数组中存在的最大元素。*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过以下观察进行优化:

*   将数字 **K** 添加到除一个指数之外的所有指数(比如指数 **X** )与从指数 **X** 处的值中移除 **K** 相同。
*   这将搜索最终数组元素的界限降低到小于或等于给定数组中的最小值。
*   设最小值为 **A** ，那么优化运算后的最终值可以是 **A** 、**A–1**或**A–2**。
*   计算中未考虑**A–3**等原因是因为 **A + 1** 需要 2 步才能到达那里(-1，-2)**A+2**需要一步才能到达**A–3**(-5)但可以轻松到达 **A** 需要一步( **A+1** 需要 1 步(-1)才能到达**A****A+2**
*   **此外， **A + 3** 需要 2 步(-5，-1)才能到达**A–3**和 **2** 步才能再次到达**A**(-1，-2)。**
*   **因此，不需要考虑**A–3**或任何较低的碱基。**

**因此，想法是通过减去 **1、2 和 5** ，找到将所有数组元素减少到其最小元素(比如 **minE** )、**MiNE–1**和**MiNE–2**所需的操作数。打印以上三个操作中的最小值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of steps
int calculate_steps(int arr[], int n,
                    int minimum)
{
    // count stores number of operations
    // required to make all elements
    // equal to minimum value
    int count = 0;

    // Remark, the array should remain
    // unchanged for further calculations
    // with different minimum
    for (int i = 0; i < n; i++) {

        // Storing the current value of
        // arr[i] in val
        int val = arr[i];

        if (arr[i] > minimum) {

            // Finds how much extra amount
            // is to be removed
            arr[i] = arr[i] - minimum;

            // Subtract the maximum number
            // of 5 and stores remaining
            count += arr[i] / 5;

            arr[i] = arr[i] % 5;

            // Subtract the maximum number
            // of 2 and stores remaining
            count += arr[i] / 2;

            arr[i] = arr[i] % 2;

            if (arr[i]) {
                count++;
            }
        }

        // Restores the actual value
        // of arr[i]
        arr[i] = val;
    }

    // Return the count
    return count;
}

// Function to find the minimum number
// of steps to make array elements same
int solve(int arr[], int n)
{

    // Sort the array in descending order
    sort(arr, arr + n, greater<int>());

    // Stores the minimum array element
    int minimum = arr[n - 1];

    int count1 = 0, count2 = 0, count3 = 0;

    // Stores the operations required
    // to make array elements equal to minimum
    count1 = calculate_steps(arr, n, minimum);

    // Stores the operations required
    // to make array elements equal to minimum - 1
    count2 = calculate_steps(arr, n, minimum - 1);

    // Stores the operations required
    // to make array elements equal to minimum - 2
    count3 = calculate_steps(arr, n, minimum - 2);

    // Return minimum of the three counts
    return min(count1, min(count2, count3));
}

// Driver Code
int main()
{
    int arr[] = { 3, 6, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);
    cout << solve(arr, N);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to calculate the minimum
// number of steps
static int calculate_steps(Integer arr[],
                           int n, int minimum)
{
    // count stores number of operations
    // required to make all elements
    // equal to minimum value
    int count = 0;

    // Remark, the array should remain
    // unchanged for further calculations
    // with different minimum
    for (int i = 0; i < n; i++)
    {
        // Storing the current value of
        // arr[i] in val
        int val = arr[i];

        if (arr[i] > minimum)
        {
            // Finds how much extra amount
            // is to be removed
            arr[i] = arr[i] - minimum;

            // Subtract the maximum number
            // of 5 and stores remaining
            count += arr[i] / 5;

            arr[i] = arr[i] % 5;

            // Subtract the maximum number
            // of 2 and stores remaining
            count += arr[i] / 2;

            arr[i] = arr[i] % 2;

            if (arr[i] > 0)
            {
                count++;
            }
        }

        // Restores the actual value
        // of arr[i]
        arr[i] = val;
    }

    // Return the count
    return count;
}

// Function to find the minimum number
// of steps to make array elements same
static int solve(Integer arr[], int n)
{

    // Sort the array in descending order
     Arrays.sort(arr, Collections.reverseOrder());

    // Stores the minimum array element
    int minimum = arr[n - 1];

    int count1 = 0, count2 = 0, count3 = 0;

    // Stores the operations required
    // to make array elements equal
    // to minimum
    count1 = calculate_steps(arr, n,
                             minimum);

    // Stores the operations required
    // to make array elements equal to
    // minimum - 1
    count2 = calculate_steps(arr, n,
                             minimum - 1);

    // Stores the operations required
    // to make array elements equal to
    // minimum - 2
    count3 = calculate_steps(arr, n,
                             minimum - 2);

    // Return minimum of the three counts
    return Math.min(count1, Math.min(count2,
                                     count3));
}

// Driver Code
public static void main(String[] args)
{
    Integer arr[] = {3, 6, 6};
    int N = arr.length;
    System.out.print(solve(arr, N));
}
}
// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to calculate the minimum
# number of steps
def calculate_steps(arr, n, minimum):

    # count stores number of operations
    # required to make all elements
    # equal to minimum value
    count = 0

    # Remark, the array should remain
    # unchanged for further calculations
    # with different minimum
    for i in range(n):

        # Storing the current value of
        # arr[i] in val
        val = arr[i]

        if (arr[i] > minimum):

            # Finds how much extra amount
            # is to be removed
            arr[i] = arr[i] - minimum

            # Subtract the maximum number
            # of 5 and stores remaining
            count += arr[i] // 5

            arr[i] = arr[i] % 5

            # Subtract the maximum number
            # of 2 and stores remaining
            count += arr[i] // 2

            arr[i] = arr[i] % 2

            if (arr[i]):
                count += 1

        # Restores the actual value
        # of arr[i]
        arr[i] = val

    # Return the count
    return count

# Function to find the minimum number
# of steps to make array elements same
def solve(arr, n):

    # Sort the array in descending order
    arr = sorted(arr)
    arr = arr[::-1]

    # Stores the minimum array element
    minimum = arr[n - 1]

    count1 = 0
    count2 = 0
    count3 = 0

    # Stores the operations required
    # to make array elements equal to minimum
    count1 = calculate_steps(arr, n, minimum)

    # Stores the operations required
    # to make array elements equal to minimum - 1
    count2 = calculate_steps(arr, n, minimum - 1)

    # Stores the operations required
    # to make array elements equal to minimum - 2
    count3 = calculate_steps(arr, n, minimum - 2)

    # Return minimum of the three counts
    return min(count1, min(count2, count3))

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 6, 6 ]
    N = len(arr)

    print(solve(arr, N))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach

using System;

public class GFG{

// Function to calculate the minimum
// number of steps
static int calculate_steps(int []arr, int n,
                    int minimum)
{
    // count stores number of operations
    // required to make all elements
    // equal to minimum value
    int count = 0;

    // Remark, the array should remain
    // unchanged for further calculations
    // with different minimum
    for (int i = 0; i < n; i++) {

        // Storing the current value of
        // arr[i] in val
        int val = arr[i];

        if (arr[i] > minimum) {

            // Finds how much extra amount
            // is to be removed
            arr[i] = arr[i] - minimum;

            // Subtract the maximum number
            // of 5 and stores remaining
            count += arr[i] / 5;

            arr[i] = arr[i] % 5;

            // Subtract the maximum number
            // of 2 and stores remaining
            count += arr[i] / 2;

            arr[i] = arr[i] % 2;

            if (arr[i]>0) {
                count++;
            }
        }

        // Restores the actual value
        // of arr[i]
        arr[i] = val;
    }

    // Return the count
    return count;
}

// Function to find the minimum number
// of steps to make array elements same
static int solve(int []arr, int n)
{

    // Sort the array in descending order
    Array.Sort(arr);
    Array.Reverse(arr);
    // Stores the minimum array element
    int minimum = arr[n - 1];

    int count1 = 0, count2 = 0, count3 = 0;

    // Stores the operations required
    // to make array elements equal to minimum
    count1 = calculate_steps(arr, n, minimum);

    // Stores the operations required
    // to make array elements equal to minimum - 1
    count2 = calculate_steps(arr, n, minimum - 1);

    // Stores the operations required
    // to make array elements equal to minimum - 2
    count3 = calculate_steps(arr, n, minimum - 2);

    // Return minimum of the three counts
    return Math.Min(count1, Math.Min(count2, count3));
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 6, 6 };

    int N = arr.Length;
    Console.Write(solve(arr, N));
}
}

// This code contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>
      // JavaScript program for the above approach
      // Function to calculate the minimum
      // number of steps
      function calculate_steps(arr, n, minimum) {
        // count stores number of operations
        // required to make all elements
        // equal to minimum value
        var count = 0;

        // Remark, the array should remain
        // unchanged for further calculations
        // with different minimum
        for (var i = 0; i < n; i++) {
          // Storing the current value of
          // arr[i] in val
          var val = arr[i];

          if (arr[i] > minimum) {
            // Finds how much extra amount
            // is to be removed
            arr[i] = arr[i] - minimum;

            // Subtract the maximum number
            // of 5 and stores remaining
            count += parseInt(arr[i] / 5);

            arr[i] = arr[i] % 5;

            // Subtract the maximum number
            // of 2 and stores remaining
            count += parseInt(arr[i] / 2);

            arr[i] = arr[i] % 2;

            if (arr[i]) {
              count++;
            }
          }

          // Restores the actual value
          // of arr[i]
          arr[i] = val;
        }

        // Return the count
        return count;
      }

      // Function to find the minimum number
      // of steps to make array elements same
      function solve(arr, n) {
        // Sort the array in descending order
        arr.sort((a, b) => b - a);

        // Stores the minimum array element
        var minimum = arr[n - 1];

        var count1 = 0,
          count2 = 0,
          count3 = 0;

        // Stores the operations required
        // to make array elements equal to minimum
        count1 = calculate_steps(arr, n, minimum);

        // Stores the operations required
        // to make array elements equal to minimum - 1
        count2 = calculate_steps(arr, n, minimum - 1);

        // Stores the operations required
        // to make array elements equal to minimum - 2
        count3 = calculate_steps(arr, n, minimum - 2);

        // Return minimum of the three counts
        return Math.min(count1, Math.min(count2, count3));
      }

      // Driver Code
      var arr = [3, 6, 6];
      var N = arr.length;
      document.write(solve(arr, N));
    </script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(N)，其中 N 是给定数组的大小。*
***辅助空间:** O(1)***
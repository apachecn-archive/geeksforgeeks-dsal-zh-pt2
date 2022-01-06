# 最小化总重量为 W 的背包数量，以存储包含大于 W/3 的元素的数组

> 原文:[https://www . geeksforgeeks . org/最小化总重量为 w 的背包数量-需要存储包含大于 w 的元素的数组-3/](https://www.geeksforgeeks.org/minimize-number-of-knapsacks-with-total-weigh-w-required-to-store-array-containing-elements-greater-than-w-3/)

给定一个[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]**和权重 **W** 。任务是最小化存储数组所有元素所需的背包数量。单个背包最多可以存放 **W** 的总重量。
**注:**数组的每个整数都大于(W/3)。

**示例:**

> **输入:** arr[] = {150，150，150，150}，W = 300
> **输出:** 3
> **说明:**至少需要 3 个背包来存储所有元素
> 背包 1 –{ 150，150}、背包 2 –{ 150，150}、背包 3 –{ 150 }。每个背包的重量为< = W。
> 
> **输入:** arr[] = {130，140，150，160}，W = 300
> **输出:** 2
> **说明:**背包可以填充为{130，150}、{140，160}。

方法:这个问题可以通过[两点法](https://www.geeksforgeeks.org/two-pointers-technique/)和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)来解决。按照以下步骤解决给定的问题。

*   [**<u>按非递减顺序排列数组。</u>**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   由于数组包含的元素值大于 **W/3** ，因此任何背包都不能包含两个以上的元素。
*   维护 [**<u>两个指针</u>**](https://www.geeksforgeeks.org/two-pointers-technique/) **L** 和 **R** 。最初 **L = 0** ， **R = N-1** 。
*   保持一段时间值循环 **L < = R** 。
*   对于每个 **L** 和 **R** 检查值**arr【L】+A【R】<= W**。如果这是真的，那么就有可能把这些积木放在同一个背包里。将 **L** 增加 **1** ，将 **R** 减少 **1** 。
*   否则，背包将有一个单一的值元素**arr【I】**。用 **1** 减少 **R** 。
*   为每个有效步骤增加答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// minimum knapsacks required to
int minimumKnapsacks(int A[], int N, int W)
{
    // Variable to store
    // the knapsacks required
    int ans = 0;

    // Maintain two pointers L and R
    int L = 0, R = N - 1;

    // Sort the array in
    // non-decreasing order
    sort(A, A + N);

    // Maintain a while loop
    while (L <= R) {

        // Check if there two elements
        // can be stored in a
        // single knapsack
        if (A[L] + A[R] <= W) {

            // Increment the answer
            ans++;

            // Decrease the right pointer
            R--;

            // Increase the left pointer
            L++;
        }
        else {
            // A single knapsack will be requried
            // to store the Right element
            R--;
            ans++;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int W = 300;
    int arr[] = { 130, 140, 150, 160 };

    // To store the size of arr[]
    int N = sizeof(arr) / sizeof(arr[0]);

    // Print the answer
    cout << minimumKnapsacks(arr, N, W);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to calculate
// minimum knapsacks required to
static int minimumKnapsacks(int A[], int N, int W)
{

    // Variable to store
    // the knapsacks required
    int ans = 0;

    // Maintain two pointers L and R
    int L = 0, R = N - 1;

    // Sort the array in
    // non-decreasing order
    Arrays.sort(A);

    // Maintain a while loop
    while (L <= R) {

        // Check if there two elements
        // can be stored in a
        // single knapsack
        if (A[L] + A[R] <= W) {

            // Increment the answer
            ans++;

            // Decrease the right pointer
            R--;

            // Increase the left pointer
            L++;
        }
        else {
            // A single knapsack will be requried
            // to store the Right element
            R--;
            ans++;
        }
    }
    return ans;
}

// Driver code
public static void main (String args[])
{

    int W = 300;
    int arr[] = { 130, 140, 150, 160 };

    // To store the size of arr[]
    int N = arr.length;

    // Print the answer
    System.out.println(minimumKnapsacks(arr, N, W));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to calculate
# minimum knapsacks required to
def minimumKnapsacks(A, N, W):
    # Variable to store
    # the knapsacks required
    ans = 0;

    # Maintain two pointers L and R
    L = 0
    R = N - 1;

    # Sort the array in
    # non-decreasing order
    A.sort();

    # Maintain a while loop
    while (L <= R):

        # Check if there two elements
        # can be stored in a
        # single knapsack
        if (A[L] + A[R] <= W):

            # Increment the answer
            ans += 1

            # Decrease the right pointer
            R -= 1

            # Increase the left pointer
            L += 1
        else:
            # A single knapsack will be requried
            # to store the Right element
            R -= 1
            ans += 1
    return ans;

# Driver Code

W = 300;
arr = [ 130, 140, 150, 160 ]

# To store the size of arr[]
N = len(arr);

# Print the answer
print(minimumKnapsacks(arr, N, W))

# This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to calculate
// minimum knapsacks required to
static int minimumKnapsacks(int []A, int N, int W)
{

    // Variable to store
    // the knapsacks required
    int ans = 0;

    // Maintain two pointers L and R
    int L = 0, R = N - 1;

    // Sort the array in
    // non-decreasing order
    Array.Sort(A);

    // Maintain a while loop
    while (L <= R) {

        // Check if there two elements
        // can be stored in a
        // single knapsack
        if (A[L] + A[R] <= W) {

            // Increment the answer
            ans++;

            // Decrease the right pointer
            R--;

            // Increase the left pointer
            L++;
        }
        else {
            // A single knapsack will be requried
            // to store the Right element
            R--;
            ans++;
        }
    }
    return ans;
}

// Driver code
public static void Main ()
{

    int W = 300;
    int []arr = { 130, 140, 150, 160 };

    // To store the size of arr[]
    int N = arr.Length;

    // Print the answer
    Console.Write(minimumKnapsacks(arr, N, W));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript implementation for the above approach

    // Function to calculate
    // minimum knapsacks required to
    const minimumKnapsacks = (A, N, W) => {

        // Variable to store
        // the knapsacks required
        let ans = 0;

        // Maintain two pointers L and R
        let L = 0, R = N - 1;

        // Sort the array in
        // non-decreasing order
        A.sort();

        // Maintain a while loop
        while (L <= R) {

            // Check if there two elements
            // can be stored in a
            // single knapsack
            if (A[L] + A[R] <= W) {

                // Increment the answer
                ans++;

                // Decrease the right pointer
                R--;

                // Increase the left pointer
                L++;
            }
            else
            {

                // A single knapsack will be requried
                // to store the Right element
                R--;
                ans++;
            }
        }
        return ans;
    }

    // Driver Code
    let W = 300;
    let arr = [130, 140, 150, 160];

    // To store the size of arr[]
    let N = arr.length;

    // Print the answer
    document.write(minimumKnapsacks(arr, N, W));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
2
```

**时间复杂度:** O(N*log(N))
**辅助空间:** O(1)
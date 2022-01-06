# 范围[0，N–1]

内所有可能的 K 值的最小绝对值(K–arr[I])

> 原文:[https://www . geeksforgeeks . org/k-arri 的最小绝对值范围内的所有可能 k 值-0-n-1/](https://www.geeksforgeeks.org/minimum-absolute-value-of-k-arri-for-all-possible-values-of-k-over-the-range-0-n-1/)

给定一个正整数 **N** 和一个由 **M** 个整数组成的排序数组**arr【】**，任务是为范围**【0，N-1】**内 **K** 的所有可能值找到**(K–arr[I])**的最小绝对值。

**示例:**

> **输入:** N = 5，arr[] = {0，4}
> **输出:** 0 1 2 1 0
> **说明:**
> 以下是 K 在[0，N–1]范围内所有可能值的可能最小值:
> 
> *   **K = 0:** 通过将 arr[i]视为 0，得到**ABS(K–arr[I])**的最小值。因此，该值为 ABS(0–0)= 0。
> *   **K = 1:** 通过将 arr[i]视为 0，得到**ABS(K–arr[I])**的最小值。因此，该值为 ABS(1–0)= 1。
> *   **K = 2:** 通过将 arr[i]视为 0，得到**ABS(K–arr[I])**的最小值。因此，该值为 ABS(2–0)= 2。
> *   **K = 3:** 通过考虑 arr[i]为 4 得到**ABS(K–arr[I])**的最小值。因此，该值为 ABS(3–4)= 1。
> *   **K = 4:** 通过将 arr[i]视为 4，得到**ABS(K–arr[I])**的最小值。因此，该值为 ABS(4–4)= 0。
> 
> **输入:** N = 6，arr[] = {0，1，4，5 }
> T3】输出:0 0 1 0 0 0

**方法:**给定的问题可以通过从数组中选择大于或小于 **K** 当前值的值来解决。按照以下步骤解决问题:

*   初始化一个变量，说 **ind** 为 **0** ，初始化一个变量，说 **prev** 到**arr【0】**存储之前分配的值。
*   [使用变量 **K** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   初始化一个变量，说**距离**存储**(K–arr[I])**的最小绝对值。
    *   如果 **i** 的值小于**arr【0】**，则更新**距离**到**的值(arr【0】–I)**。
    *   否则，如果 **i** 的值至少为**prev**， **(ind + 1)** 的值小于 **M** ， **i** 的值最多为**arr【ind+1】**，则执行以下步骤:
        *   将**距离**的值更新为**(I–prev)**和**(arr[ind+1]–I)**的最小值。
        *   如果 **i** 的值等于**arr【ind+1】**，则将**距离**的值更新为 **0** 、 **prev** 至**arr【ind+1】**，并将 **ind** 的值增加 **1** 。
    *   如果 **i** 的值大于 **prev** ，则将**距离**的值更新为**(I–prev)**。
    *   完成上述步骤后，将**距离**的值打印为 **K** 当前值的**(K–arr[I])**的最小绝对值。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum absolute
// value of (K - arr[i]) for each possible
// value of K over the range [0, N - 1]|
void minimumDistance(vector<int> arr,
                     int N)
{
    int ind = 0;
    int prev = arr[ind];
    int s = arr.size();

    // Traverse the given array arr[]
    for (int i = 0; i < N; i++) {

        // Stores the mininimum distance
        // to any array element arr[i]
        int distance = INT_MAX;

        // Check if there is no safe
        // position smaller than i
        if (i < arr[0]) {
            distance = arr[0] - i;
        }

        // Check if the current position
        // is between two safe positions
        else if (i >= prev && ind + 1 < s
                 && i <= arr[ind + 1]) {

            // Take the minimum of two
            // distances
            distance = min(i - prev,
                           arr[ind + 1] - i);

            // Check if the current index
            // is a safe position
            if (i == arr[ind + 1]) {
                distance = 0;
                prev = arr[ind + 1];
                ind++;
            }
        }

        // Check if there is no safe
        // position greater than i
        else {
            distance = i - prev;
        }

        // Print the minimum distance
        cout << distance << " ";
    }
}

// Driver Code
int main()
{
    int N = 5;
    vector<int> arr = { 0, 4 };
    minimumDistance(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Functinion to find the minimum absolute
    // value of (K - arr[i]) for each possible
    // value of K over the range [0, N - 1]|
    public static void minimumDistance(int arr[],
                         int N)
    {
        int ind = 0;
        int prev = arr[ind];
        int s = arr.length;

        // Traverse the given array arr[]
        for (int i = 0; i < N; i++) {

            // Stores the mininimum distance
            // to any array element arr[i]
            int distance = Integer.MAX_VALUE;

            // Check if there is no safe
            // position smaller than i
            if (i < arr[0]) {
                distance = arr[0] - i;
            }

            // Check if the current position
            // is between two safe positions
            else if (i >= prev && ind + 1 < s
                     && i <= arr[ind + 1]) {

                // Take the minimum of two
                // distances
                distance = Math.min(i - prev,
                               arr[ind + 1] - i);

                // Check if the current index
                // is a safe position
                if (i == arr[ind + 1]) {
                    distance = 0;
                    prev = arr[ind + 1];
                    ind++;
                }
            }

            // Check if there is no safe
            // position greater than i
            else {
                distance = i - prev;
            }

            // Print the minimum distance
            System.out.print(distance+" ");
        }
    }

    // driver code
    public static void main (String[] args) {
        int N = 5;
        int arr[] = { 0, 4 };
        minimumDistance(arr, N);
    }
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum absolute
# value of (K - arr[i]) for each possible
# value of K over the range [0, N - 1]|
def minimumDistance(arr, N):
    ind = 0;
    prev = arr[ind];
    s = len(arr);

    # Traverse the given array arr[]
    for i in range(N):

        # Stores the mininimum distance
        # to any array element arr[i]
        distance = 10**9;

        # Check if there is no safe
        # position smaller than i
        if (i < arr[0]):
            distance = arr[0] - i;

        # Check if the current position
        # is between two safe positions
        elif (i >= prev and ind + 1 < s
            and i <= arr[ind + 1]):

            # Take the minimum of two
            # distances
            distance = min(i - prev, arr[ind + 1] - i);

            # Check if the current index
            # is a safe position
            if (i == arr[ind + 1]):
                distance = 0;
                prev = arr[ind + 1];
                ind += 1;

        # Check if there is no safe
        # position greater than i
        else:
            distance = i - prev;

        # Print the minimum distance
        print(distance, end=" ");

# Driver Code

N = 5;
arr = [0, 4];
minimumDistance(arr, N);

# This code is contributed by _saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Functinion to find the minimum absolute
    // value of (K - arr[i]) for each possible
    // value of K over the range [0, N - 1]|
    public static void minimumDistance(int []arr,
                         int N)
    {
        int ind = 0;
        int prev = arr[ind];
        int s = arr.Length;

        // Traverse the given array arr[]
        for (int i = 0; i < N; i++) {

            // Stores the mininimum distance
            // to any array element arr[i]
            int distance = Int32.MaxValue;

            // Check if there is no safe
            // position smaller than i
            if (i < arr[0]) {
                distance = arr[0] - i;
            }

            // Check if the current position
            // is between two safe positions
            else if (i >= prev && ind + 1 < s
                     && i <= arr[ind + 1]) {

                // Take the minimum of two
                // distances
                distance = Math.Min(i - prev,
                               arr[ind + 1] - i);

                // Check if the current index
                // is a safe position
                if (i == arr[ind + 1]) {
                    distance = 0;
                    prev = arr[ind + 1];
                    ind++;
                }
            }

            // Check if there is no safe
            // position greater than i
            else {
                distance = i - prev;
            }

            // Print the minimum distance
            Console.Write(distance+" ");
        }
    }

    // driver code
    public static void Main (string[] args) {
        int N = 5;
        int []arr = { 0, 4 };
        minimumDistance(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum absolute
// value of (K - arr[i]) for each possible
// value of K over the range [0, N - 1]|
function minimumDistance(arr, N) {
    let ind = 0;
    let prev = arr[ind];
    let s = arr.length;

    // Traverse the given array arr[]
    for (let i = 0; i < N; i++) {

        // Stores the mininimum distance
        // to any array element arr[i]
        let distance = Number.MAX_SAFE_INTEGER;

        // Check if there is no safe
        // position smaller than i
        if (i < arr[0]) {
            distance = arr[0] - i;
        }

        // Check if the current position
        // is between two safe positions
        else if (i >= prev && ind + 1 < s
            && i <= arr[ind + 1]) {

            // Take the minimum of two
            // distances
            distance = Math.min(i - prev,
                arr[ind + 1] - i);

            // Check if the current index
            // is a safe position
            if (i == arr[ind + 1]) {
                distance = 0;
                prev = arr[ind + 1];
                ind++;
            }
        }

        // Check if there is no safe
        // position greater than i
        else {
            distance = i - prev;
        }

        // Print the minimum distance
        document.write(distance + " ");
    }
}

// Driver Code

let N = 5;
let arr = [0, 4];
minimumDistance(arr, N);

</script>
```

**Output:** 

```
0 1 2 1 0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
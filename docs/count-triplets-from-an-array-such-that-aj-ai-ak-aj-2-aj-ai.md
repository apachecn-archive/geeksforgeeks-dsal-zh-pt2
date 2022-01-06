# 对数组中的三元组进行计数，使 a[j]–a[I]≤a[k]–a[j]≤2 *(a[j]–a[I])

> 原文:[https://www . geeksforgeeks . org/count-triples-from-a-so-aj-ai-AK-aj-2-aj-ai/](https://www.geeksforgeeks.org/count-triplets-from-an-array-such-that-aj-ai-ak-aj-2-aj-ai/)

给定一个由不同元素组成的大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算三元组的数量，使得**(arr[j]–arr[I])≤(arr[k]–arr[j])≤2 *(arr[j]–arr[I])**和**arr[I]<arr[j]<arr[k]**(***1≤I***

**示例:**

> **输入:** arr[] = {5，3，12，9，6}
> **输出:** 4
> **解释:**所有满足条件的三元组为{3，5，9}、{3，6，9}、{3，6，12}、{6，9，12}
> 
> **输入:** arr[] = {1，2，3 }
> T3】输出: 1

**天真方法:**最简单的方法是生成所有可能的三元组，并针对每一个三元组，检查其是否满足给定条件。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效途径:**以上途径可以通过[二分搜索法](https://www.geeksforgeeks.org/binary-search/)进行优化。按照以下步骤解决问题:

*   [排序数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/) **arr[]** 。
*   初始化一个变量，说 **ans** 为 **0，**存储三胞胎的数量。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N】**中迭代，并执行以下步骤:
        *   将 **X** 初始化为**arr[j]–arr[I]**。
        *   使用[下界](https://www.geeksforgeeks.org/lower_bound-in-cpp/)找到**arr【j】+X**的下界，并将其索引存储在变量 **l** 中。
        *   同样，使用默认函数[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)找到 **arr[j] + 2×X** 的上限，并将其索引存储在变量 **r** 中。
        *   将 **r-l** 添加到变量 **ans** 中。
*   执行上述步骤后，打印**和**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
int countTriplets(int arr[], int N)
{
    // Sort the array
    sort(arr, arr + N);

    // Stores count of triplets
    int l, r, i, j, ans = 0;

    // Iterate over the range [1, N]
    for (i = 0; i < N; i++) {
        // Iterate over the range [i+1, N]
        for (j = i + 1; j < N; j++) {
            // Required difference
            int x = arr[j] - arr[i];

            // Find lower bound of arr[j] + x
            // and upper bound of arr[j] + 2*x
            l = lower_bound(arr, arr + N, arr[j] + x) - arr;
            r = upper_bound(arr, arr + N, arr[j] + 2 * x)
                - arr;

            // Adjust the indexing of arr[j]+2*r
            if (r == N || arr[r] != arr[j] + 2 * x)
                r -= 1;

            // From l to r, count number of
            // triplets by using arr[i] and arr[j]
            ans += r - l + 1;
        }
    }
    // return main ans
    return ans;
}
// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int ans = countTriplets(arr, N);
    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

public static int countTriplets(int arr[], int N)
{

    // Sort the array
    Arrays.sort(arr);

    // Stores count of triplets
    int l, r, i, j, ans = 0;

    // Iterate over the range [1, N]
    for(i = 0; i < N; i++)
    {

        // Iterate over the range [i+1, N]
        for(j = i + 1; j < N; j++)
        {

            // Required difference
            int x = arr[j] - arr[i];

            // Find lower bound of arr[j] + x
            // and upper bound of arr[j] + 2*x
            l = lower_bound(arr, 0, arr.length - 1,
                                        arr[j] + x);
            r = upper_bound(arr, 0, arr.length - 1,
                                    arr[j] + 2 * x);

            // Adjust the indexing of arr[j]+2*r
            if (r == N || arr[r] != arr[j] + 2 * x)
                r -= 1;

            // From l to r, count number of
            // triplets by using arr[i] and arr[j]
            ans += r - l + 1;
        }
    }

    // Return main ans
    return ans;
}

public static int upper_bound(int[] arr, int low,
                              int high, int X)
{

    // Base Case
    if (low > high)
        return low;

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is less than
    // or equal to X search in
    // right subarray
    if (arr[mid] <= X)
    {
        return upper_bound(arr, mid + 1, high, X);
    }

    // If arr[mid] is greater than X
    // then search in left subarray
    return upper_bound(arr, low, mid - 1, X);
}

public static int lower_bound(int[] arr, int low,
                              int high, int X)
{

    // Base Case
    if (low > high)
    {
        return low;
    }

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is greater than
    // or equal to X then search
    // in left subarray
    if (arr[mid] >= X)
    {
        return lower_bound(arr, low, mid - 1, X);
    }

    // If arr[mid] is less than X
    // then search in right subarray
    return lower_bound(arr, mid + 1, high, X);
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3 };
    int N = arr.length;
    int ans = countTriplets(arr, N);

    System.out.println(ans);
}
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Import library to apply
# binary search and find bound
from bisect import bisect_left

# Function to count triplets
# from an array that satisfies
# the given conditions
def countTriplets(arr, N):

    # Sort the array
    arr.sort()

    # Stores count of triplets
    ans = 0

    # Iterate over the range [1, N]
    for i in range(N):

        # Iterate over the range [i+1, N]
        for j in range(i+1, N):

            # Required difference
            x = arr[j]-arr[i]

            # Find lower bound of arr[j] + x
            # and upper bound of arr[j] + 2*x
            l = bisect_left(arr, arr[j] + x)
            r = bisect_left(arr, arr[j] + 2*x)

            # Adjust the indexing of arr[j]+2*r
            if r == N or arr[r] != arr[j]+2*x:
                r -= 1

            # From l to r, count number of
            # triplets by using arr[i] and arr[j]
            ans += r-l+1

    # return main ans
    return ans

# Driver Code
if __name__ == "__main__":

    # Given Input
    arr = [1, 2, 3]
    N = len(arr)

    # Function Call
    ans = countTriplets(arr, N)
    print(ans)
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static int countTriplets(int[] arr, int N)
    {

        // Sort the array
        Array.Sort(arr);

        // Stores count of triplets
        int l, r, i, j, ans = 0;

        // Iterate over the range [1, N]
        for(i = 0; i < N; i++)
        {

            // Iterate over the range [i+1, N]
            for(j = i + 1; j < N; j++)
            {

                // Required difference
                int x = arr[j] - arr[i];

                // Find lower bound of arr[j] + x
                // and upper bound of arr[j] + 2*x
                l = lower_bound(arr, 0, arr.Length - 1,
                                            arr[j] + x);
                r = upper_bound(arr, 0, arr.Length - 1,
                                        arr[j] + 2 * x);

                // Adjust the indexing of arr[j]+2*r
                if (r == N || arr[r] != arr[j] + 2 * x)
                    r -= 1;

                // From l to r, count number of
                // triplets by using arr[i] and arr[j]
                ans += r - l + 1;
            }
        }

        // Return main ans
        return ans;
    }

    static int upper_bound(int[] arr, int low,
                                  int high, int X)
    {

        // Base Case
        if (low > high)
            return low;

        // Find the middle index
        int mid = low + (high - low) / 2;

        // If arr[mid] is less than
        // or equal to X search in
        // right subarray
        if (arr[mid] <= X)
        {
            return upper_bound(arr, mid + 1, high, X);
        }

        // If arr[mid] is greater than X
        // then search in left subarray
        return upper_bound(arr, low, mid - 1, X);
    }

    static int lower_bound(int[] arr, int low,
                                  int high, int X)
    {

        // Base Case
        if (low > high)
        {
            return low;
        }

        // Find the middle index
        int mid = low + (high - low) / 2;

        // If arr[mid] is greater than
        // or equal to X then search
        // in left subarray
        if (arr[mid] >= X)
        {
            return lower_bound(arr, low, mid - 1, X);
        }

        // If arr[mid] is less than X
        // then search in right subarray
        return lower_bound(arr, mid + 1, high, X);
    }

  static void Main() {
    int[] arr = { 1, 2, 3 };
    int N = arr.Length;
    int ans = countTriplets(arr, N);

    Console.WriteLine(ans);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

function countTriplets(arr, N) {
    // Sort the array
    arr.sort((a, b) => a - b);

    // Stores count of triplets
    let l, r, i, j, ans = 0;

    // Iterate over the range [1, N]
    for (i = 0; i < N; i++) {
        // Iterate over the range [i+1, N]
        for (j = i + 1; j < N; j++) {
            // Required difference
            let x = arr[j] - arr[i];

            // Find lower bound of arr[j] + x
            // and upper bound of arr[j] + 2*x
            l = lower_bound(arr, 0, arr.length - 1, arr[j] + x);
            //console.log(l)

            console.log(arr, arr[j] + 2 * x)
            r = upper_bound(arr, 0, arr.length - 1, arr[j] + 2 * x);
            console.log(r)

            // Adjust the indexing of arr[j]+2*r
            if (r == N || arr[r] != arr[j] + 2 * x)
                r -= 1;

            // From l to r, count number of
            // triplets by using arr[i] and arr[j]
            ans += r - l + 1;
        }
    }
    // return main ans
    return ans;
}

function upper_bound(arr, low, high, X) {
    // Base Case
    if (low > high)
        return low;

    // Find the middle index
    let mid = Math.floor(low + (high - low) / 2);

    // If arr[mid] is less than
    // or equal to X search in
    // right subarray
    if (arr[mid] <= X) {
        return upper_bound(arr, mid + 1, high, X);
    }

    // If arr[mid] is greater than X
    // then search in left subarray
    return upper_bound(arr, low, mid - 1, X);

}

function lower_bound(arr, low, high, X) {
    // Base Case
    if (low > high) {
        return low;
    }

    // Find the middle index
    let mid = Math.floor(low + (high - low) / 2);

    // If arr[mid] is greater than
    // or equal to X then search
    // in left subarray
    if (arr[mid] >= X) {
        return lower_bound(arr, low, mid - 1, X);
    }

    // If arr[mid] is less than X
    // then search in right subarray
    return lower_bound(arr, mid + 1, high, X);
}

// Driver code

let arr = [1, 2, 3];
let N = arr.length;
let ans = countTriplets(arr, N);
document.write(ans);

</script>
```

**Output**

```
1
```

***时间复杂度:**T3】O(N<sup>2</sup>* log(N))
*T8】辅助空间:T10】O(1)**
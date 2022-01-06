# 通过从给定数组中选择 K 个元素来最大化任意元素对之间的最小差异

> 原文:[https://www . geeksforgeeks . org/通过从给定数组中选择 k 个元素来最大化任意元素对之间的最小差异/](https://www.geeksforgeeks.org/maximize-the-minimum-difference-between-any-element-pair-by-selecting-k-elements-from-given-array/)

给定一个由 **N** 个整数组成的数组，任务是从这些 **N** 个元素中选择 **K** 个元素，使得 K 个数字之间的最小差值最大。选择任意 **K** 元素后返回最大最小差。

**示例:**

> **输入:** N = 4，K = 3，arr = [2，6，2，5]
> **输出:** 1
> **说明:**4 个元素中选择 3 个元素，差异尽可能小。选择 2、2、5 将导致最小差值为 0。选择 2、5、6 将导致最小差值为 6-5=1
> 
> **输入:** N = 7，K = 4，arr = [1，4，9，0，2，13，3]
> **输出:** 4
> **说明:**选择 0，4，9，13 将产生最小差 4，这是可能的最大最小差

**天真方法:** [生成大小为 K 的所有子集](https://www.geeksforgeeks.org/print-subsets-given-size-set/)，并找到所有子集的最小差异。然后返回差异中的最大值。

**有效方法:**给定的问题可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的答题技巧来有效解决。可以遵循以下步骤来解决问题:

*   [按升序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)
*   将最小答案**和**初始化为 1
*   二分搜索法用于数组中从 1 到最大元素的范围 **arr**
*   变量 **dif** 用于存储每次迭代的最大最小差
*   辅助函数用于检查是否可以选择 **K** 元素，最小差值大于上一次迭代中计算的 **dif** 。如果可能，则返回 true，否则返回 false。
*   如果上述函数返回:
    *   真则更新 **ans** 为 **dif** ，左为 **dif** + 1
    *   如果为假，则将权限更新为**dif**–1

以下是上述二分搜索法方法的实施情况

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// To check if selection of K elements
// is possible such that difference
// between them is greater than dif
bool isPossibleToSelect(int arr[], int N,
                        int dif, int K)
{
    // Selecting first element in the
    // sorted array
    int count = 1;

    // prev is the previously selected
    // element initially at index 0 as
    // first element is already selected
    int prev = arr[0];

    // Check if selection of K-1 elements
    // from array with a minimum
    // difference of dif is possible
    for (int i = 1; i < N; i++) {

        // If the current element is
        // atleast dif difference apart
        // from the  previously selected
        // element then select the current
        // element and increase the count
        if (arr[i] >= (prev + dif)) {
            count++;

            // If selection of K elements
            // with a min difference of dif
            // is possible then return true
            if (count == K)
                return true;

            // Prev will become current
            // element for the next iteration
            prev = arr[i];
        }
    }
    // If selection of K elements with minimum
    // difference of dif is not possible
    // then return false
    return false;
}

int binarySearch(int arr[], int left,
                 int right, int K, int N)
{
    // Minimum largest difference
    // possible is 1
    int ans = 1;
    while (left <= right) {
        int dif = left + (right - left) / 2;

        // Check if selection of K elements
        // is possible with a minimum
        // difference of dif
        if (isPossibleToSelect(arr, N,
                               dif, K)) {

            // If dif is greater than
            // previous ans we update ans
            ans = max(ans, dif);

            // Continue to search for better
            // answer. Try finding greater dif
            left = dif + 1;
        }

        // K elements cannot be selected
        else
            right = dif - 1;
    }
    return ans;
}

// Driver code
int main()
{
    int N, K;
    N = 7, K = 4;
    int arr[] = { 1, 4, 9, 0, 2, 13, 3 };

    // arr should be in a sorted order
    sort(arr, arr + N);

    cout << binarySearch(arr, 0, arr[N - 1], K, N)
         << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

  // To check if selection of K elements
  // is possible such that difference
  // between them is greater than dif
  static boolean isPossibleToSelect(int []arr, int N,
                                    int dif, int K)
  {

    // Selecting first element in the
    // sorted array
    int count = 1;

    // prev is the previously selected
    // element initially at index 0 as
    // first element is already selected
    int prev = arr[0];

    // Check if selection of K-1 elements
    // from array with a minimum
    // difference of dif is possible
    for (int i = 1; i < N; i++) {

      // If the current element is
      // atleast dif difference apart
      // from the  previously selected
      // element then select the current
      // element and increase the count
      if (arr[i] >= (prev + dif)) {
        count++;

        // If selection of K elements
        // with a min difference of dif
        // is possible then return true
        if (count == K)
          return true;

        // Prev will become current
        // element for the next iteration
        prev = arr[i];
      }
    }
    // If selection of K elements with minimum
    // difference of dif is not possible
    // then return false
    return false;
  }

  static int binarySearch(int []arr, int left,
                          int right, int K, int N)
  {
    // Minimum largest difference
    // possible is 1
    int ans = 1;
    while (left <= right) {
      int dif = left + (right - left) / 2;

      // Check if selection of K elements
      // is possible with a minimum
      // difference of dif
      if (isPossibleToSelect(arr, N,
                             dif, K)) {

        // If dif is greater than
        // previous ans we update ans
        ans = Math.max(ans, dif);

        // Continue to search for better
        // answer. Try finding greater dif
        left = dif + 1;
      }

      // K elements cannot be selected
      else
        right = dif - 1;
    }
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    int N, K;
    N = 7;
    K = 4;
    int []arr = { 1, 4, 9, 0, 2, 13, 3 };

    // arr should be in a sorted order
    Arrays.sort(arr);

    System.out.println(binarySearch(arr, 0, arr[N - 1], K, N));
  }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# To check if selection of K elements
# is possible such that difference
# between them is greater than dif
def isPossibleToSelect(arr, N,
                       dif, K):

    # Selecting first element in the
    # sorted array
    count = 1

    # prev is the previously selected
    # element initially at index 0 as
    # first element is already selected
    prev = arr[0]

    # Check if selection of K-1 elements
    # from array with a minimum
    # difference of dif is possible
    for i in range(1, N):

        # If the current element is
        # atleast dif difference apart
        # from the  previously selected
        # element then select the current
        # element and increase the count
        if (arr[i] >= (prev + dif)):
            count += 1

            # If selection of K elements
            # with a min difference of dif
            # is possible then return true
            if (count == K):
                return True

            # Prev will become current
            # element for the next iteration
            prev = arr[i]
    # If selection of K elements with minimum
    # difference of dif is not possible
    # then return false
    return False

def binarySearch(arr, left,
                 right, K,  N):
    # Minimum largest difference
    # possible is 1
    ans = 1
    while (left <= right):
        dif = left + (right - left) // 2

        # Check if selection of K elements
        # is possible with a minimum
        # difference of dif
        if (isPossibleToSelect(arr, N, dif, K)):

            # If dif is greater than
            # previous ans we update ans
            ans = max(ans, dif)

            # Continue to search for better
            # answer. Try finding greater dif
            left = dif + 1

        # K elements cannot be selected
        else:
            right = dif - 1

    return ans

# Driver code
if __name__ == "__main__":

    N = 7
    K = 4
    arr = [1, 4, 9, 0, 2, 13, 3]

    # arr should be in a sorted order
    arr.sort()

    print(binarySearch(arr, 0, arr[N - 1], K, N)
          )

    # This code is contributed by ukasp.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{

// To check if selection of K elements
// is possible such that difference
// between them is greater than dif
static bool isPossibleToSelect(int []arr, int N,
                        int dif, int K)
{
    // Selecting first element in the
    // sorted array
    int count = 1;

    // prev is the previously selected
    // element initially at index 0 as
    // first element is already selected
    int prev = arr[0];

    // Check if selection of K-1 elements
    // from array with a minimum
    // difference of dif is possible
    for (int i = 1; i < N; i++) {

        // If the current element is
        // atleast dif difference apart
        // from the  previously selected
        // element then select the current
        // element and increase the count
        if (arr[i] >= (prev + dif)) {
            count++;

            // If selection of K elements
            // with a min difference of dif
            // is possible then return true
            if (count == K)
                return true;

            // Prev will become current
            // element for the next iteration
            prev = arr[i];
        }
    }
    // If selection of K elements with minimum
    // difference of dif is not possible
    // then return false
    return false;
}

static int binarySearch(int []arr, int left,
                 int right, int K, int N)
{
    // Minimum largest difference
    // possible is 1
    int ans = 1;
    while (left <= right) {
        int dif = left + (right - left) / 2;

        // Check if selection of K elements
        // is possible with a minimum
        // difference of dif
        if (isPossibleToSelect(arr, N,
                               dif, K)) {

            // If dif is greater than
            // previous ans we update ans
            ans = Math.Max(ans, dif);

            // Continue to search for better
            // answer. Try finding greater dif
            left = dif + 1;
        }

        // K elements cannot be selected
        else
            right = dif - 1;
    }
    return ans;
}

// Driver code
public static void Main()
{
    int N, K;
    N = 7;
     K = 4;
    int []arr = { 1, 4, 9, 0, 2, 13, 3 };

    // arr should be in a sorted order
    Array.Sort(arr);

    Console.Write(binarySearch(arr, 0, arr[N - 1], K, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // To check if selection of K elements
        // is possible such that difference
        // between them is greater than dif
        function isPossibleToSelect(arr, N,
            dif, K)
        {

            // Selecting first element in the
            // sorted array
            let count = 1;

            // prev is the previously selected
            // element initially at index 0 as
            // first element is already selected
            let prev = arr[0];

            // Check if selection of K-1 elements
            // from array with a minimum
            // difference of dif is possible
            for (let i = 1; i < N; i++) {

                // If the current element is
                // atleast dif difference apart
                // from the  previously selected
                // element then select the current
                // element and increase the count
                if (arr[i] >= (prev + dif)) {
                    count++;

                    // If selection of K elements
                    // with a min difference of dif
                    // is possible then return true
                    if (count == K)
                        return true;

                    // Prev will become current
                    // element for the next iteration
                    prev = arr[i];
                }
            }
            // If selection of K elements with minimum
            // difference of dif is not possible
            // then return false
            return false;
        }

        function binarySearch(arr, left,
            right, K, N) {
            // Minimum largest difference
            // possible is 1
            let ans = 1;
            while (left <= right) {
                let dif = left + Math.floor((right - left) / 2);

                // Check if selection of K elements
                // is possible with a minimum
                // difference of dif
                if (isPossibleToSelect(arr, N,
                    dif, K)) {

                    // If dif is greater than
                    // previous ans we update ans
                    ans = Math.max(ans, dif);

                    // Continue to search for better
                    // answer. Try finding greater dif
                    left = dif + 1;
                }

                // K elements cannot be selected
                else
                    right = dif - 1;
            }
            return ans;
        }

        // Driver code

        let N, K;
        N = 7, K = 4;
        let arr = [1, 4, 9, 0, 2, 13, 3];

        // arr should be in a sorted order
        arr.sort(function (a, b) { return a - b })

        document.write(binarySearch(arr, 0, arr[N - 1], K, N)
            + '<br>');

     // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
4
```

**时间复杂度:**O(N * log N)
T3】空间复杂度: O(1)
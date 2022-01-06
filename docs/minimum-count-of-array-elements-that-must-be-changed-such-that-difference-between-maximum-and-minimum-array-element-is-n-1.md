# 必须改变的最小数组元素数，使得最大和最小数组元素之差为 N–1

> 原文:[https://www . geesforgeks . org/数组元素的最小计数必须更改，以使数组元素的最大值和最小值之差为-n-1/](https://www.geeksforgeeks.org/minimum-count-of-array-elements-that-must-be-changed-such-that-difference-between-maximum-and-minimum-array-element-is-n-1/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出必须更改为任意整数的最小数组元素数，使得最大数组元素和最小数组元素之差为**(N–1)**，[所有数组元素必须不同](https://www.geeksforgeeks.org/check-if-all-array-elements-are-distinct/)。

**示例:**

> **输入:** arr[] = {1，2，3，5，6}
> **输出:** 1
> **解释:**
> 变化 6- > 4，最终数组将为{1，2，3，5，4}，差值等于 5–1 = 4。
> 
> **输入:** arr[] = {1，10，100，1000 }
> T3】输出: 3

**方法:**使用[排序](https://www.geeksforgeeks.org/merge-sort/)和[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)可以解决给定的问题。按照以下步骤解决问题:

*   [按非递减顺序排列数组](https://www.geeksforgeeks.org/merge-sort/)。
*   维护一个变量**和**，并用值 **N** 初始化它，它将存储最小可能的答案。
*   [从给定数组中移除所有重复元素 **arr[]** 。](https://www.geeksforgeeks.org/remove-duplicates-sorted-array/)
*   [在使用变量 **i** 移除重复项后，迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M)** ，其中 **M** 是数组的新[大小，并执行以下任务:](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)
    *   循环遍历一段时间，直到 **j** 小于 **M** 且**A【j】**小于等于**A【I】+N–1**并将 **j** 的值增加 **1** 。
    *   将 **ans** 的值更新为 **ans** 和**(N–j+I)**的最小值。
*   执行上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum changes
// needed to make difference of maximum
// and minimum element as (N - 1)
int minOperations(vector<int>& A)
{
    int N = A.size();

    // Stores the resultant count
    int ans = N;

    // Maintain a pointer j that will
    // denote the rightmost position of
    // the valid array
    int j = 0;

    // Sort the array
    sort(begin(A), end(A));

    // Only keep unique elements
    A.erase(unique(begin(A), end(A)),
            end(A));

    // Store the new size of the array
    // after removing duplicates
    int M = A.size();

    // IterM;ate over the range
    for (int i = 0; i < M; ++i) {
        while (j < M && A[j] <= A[i] + N - 1) {
            ++j;
        }

        // Check minimum over this
        // starting point
        ans = min(ans, N - j + i);

        // The length of this subarray
        // is `j - i`. Replace `N - j + i`
        // elements to make it good
    }

    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 10, 100, 1000 };
    cout << minOperations(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
import java.util.*;

class GFG {

    // Function to find the minimum changes
    // needed to make difference of maximum
    // and minimum element as (N - 1)
    public static int minOperations(int[] A) {
        int N = A.length;

        // Stores the resultant count
        int ans = N;

        // Maintain a pointer j that will
        // denote the rightmost position of
        // the valid array
        int j = 0;

        // Sort the array
        Arrays.sort(A);

        // Only keep unique elements
        removeDups(A);

        // Store the new size of the array
        // after removing duplicates
        int M = A.length;

        // IterM;ate over the range
        for (int i = 0; i < M; ++i) {
            while (j < M && A[j] <= A[i] + N - 1) {
                ++j;
            }

            // Check minimum over this
            // starting point
            ans = Math.min(ans, N - j + i);

            // The length of this subarray
            // is `j - i`. Replace `N - j + i`
            // elements to make it good
        }

        return ans;
    }

    public static void removeDups(int[] a) {

        LinkedHashSet<Integer> set = new LinkedHashSet<Integer>();

        // adding elements to LinkedHashSet
        for (int i = 0; i < a.length; i++)
            set.add(a[i]);

    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 1, 10, 100, 1000 };
        System.out.println(minOperations(arr));

    }

}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum changes
# needed to make difference of maximum
# and minimum element as (N - 1)
def minOperations(A):
    N = len(A)

    # Stores the resultant count
    ans = N

    # Maintain a pointer j that will
    # denote the rightmost position of
    # the valid array
    j = 0

    # Sort the array
    A.sort()

    # Only keep unique elements
    A = list(set(A))

    # Store the new size of the array
    # after removing duplicates
    A.sort()
    M = len(A)

    # IterM;ate over the range
    for i in range(M):
        while (j < M and A[j] <= A[i] + N - 1):
            j += 1

        # Check minimum over this
        # starting point
        ans = min(ans, N - j + i)

        # The length of this subarray
        # is `j - i`. Replace `N - j + i`
        # elements to make it good

    return ans

# Driver Code
if __name__ == '__main__':
    arr = [1, 10, 100, 1000]
    print(minOperations(arr))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the minimum changes
    // needed to make difference of maximum
    // and minimum element as (N - 1)
    public static int minOperations(int[] A) {
        int N = A.Length;

        // Stores the resultant count
        int ans = N;

        // Maintain a pointer j that will
        // denote the rightmost position of
        // the valid array
        int j = 0;

        // Sort the array
        Array.Sort(A);

        // Only keep unique elements
        removeDups(A);

        // Store the new size of the array
        // after removing duplicates
        int M = A.Length;

        // IterM;ate over the range
        for (int i = 0; i < M; ++i) {
            while (j < M && A[j] <= A[i] + N - 1) {
                ++j;
            }

            // Check minimum over this
            // starting point
            ans = Math.Min(ans, N - j + i);

            // The length of this subarray
            // is `j - i`. Replace `N - j + i`
            // elements to make it good
        }

        return ans;
    }

    public static void removeDups(int[] a) {

        HashSet<int> set = new HashSet<int>();

        // adding elements to LinkedHashSet
        for (int i = 0; i < a.Length; i++)
            set.Add(a[i]);

    }

    // Driver Code
    public static void Main() {
        int[] arr = { 1, 10, 100, 1000 };
        Console.Write(minOperations(arr));
    }

}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the minimum changes
       // needed to make difference of maximum
       // and minimum element as (N - 1)
       function minOperations(A)
       {
           let N = A.length;

           // Stores the resultant count
           let ans = N;

           // Maintain a pointer j that will
           // denote the rightmost position of
           // the valid array
           let j = 0;

           // Sort the array
           A.sort(function (a, b) { return a - b });

           // Only keep unique elements
           let unique_A = [];
           for (let i = 0; i < A.length - 1; i++) {
               if (A[i] != A[i + 1]) {
                   unique_A.push(A[i])
               }
           }
           A = unique_A;
           // Store the new size of the array
           // after removing duplicates
           let M = A.length;

           // Iterate over the range
           for (let i = 0; i < M; ++i) {
               while (j < M && A[j] <= A[i] + N - 1) {
                   ++j;
               }

               // Check minimum over this
               // starting point
               ans = Math.min(ans, N - j + i);

               // The length of this subarray
               // is `j - i`. Replace `N - j + i`
               // elements to make it good
           }

           return ans;
       }

       // Driver Code

       let arr = [1, 10, 100, 1000];
       document.write(minOperations(arr));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*
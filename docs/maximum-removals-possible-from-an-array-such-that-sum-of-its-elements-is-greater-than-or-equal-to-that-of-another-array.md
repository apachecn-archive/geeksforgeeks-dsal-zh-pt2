# 从一个数组中可能的最大移除量，使得其元素之和大于或等于另一个数组的元素之和

> 原文:[https://www . geeksforgeeks . org/从一个数组中最大可能移除的元素之和大于或等于另一个数组的元素之和/](https://www.geeksforgeeks.org/maximum-removals-possible-from-an-array-such-that-sum-of-its-elements-is-greater-than-or-equal-to-that-of-another-array/)

给定两个大小分别为 **N** 和 **M** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和 **brr[]** ，任务是计算可以从数组 **arr[]** 中移除的元素的最大数量，使得 **arr[]** 中的元素之和大于或等于 **brr[]** 中的元素之和。

**示例:**

> **输入:** arr[] = { 1，2，4，6 }，brr[] = { 7 }
> **输出:** 2
> **解释:**
> 移除 arr[2]将 arr[]修改为{ 1，2，6 }并且和等于 9 ( > 7)
> 移除 arr[1]将 arr[]修改为{ 1，6 }并且和等于 7(&gr；7)
> 移除 arr[0]会将 arr[]修改为{ 6 }并且总和等于 6 ( < 7)
> 因此，所需的输出为 2。
> 
> **输入:** arr[] = { 10，20 }，brr[] = { 5 }
> **输出:** 1
> **解释:**
> 移除 arr[1]将 arr[]修改为{ 10 }且和等于 10 ( > 5)
> 移除 arr[0]将 arr[]修改为{ }且和等于 0 ( < 5)
> 因此，所需的输出为 1。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   [对数组进行排序，按升序排列](https://www.geeksforgeeks.org/sort-c-stl/)。
*   从数组 **arr[]** 中移除最小元素，检查 **arr[]** 的元素之和是否大于或等于数组元素之和 **brr[]** 。如果发现为真，则增加计数。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the count of elements
// required to be removed from arr[] such that
// the sum of arr[] is greater than or equal
// to sum of the array brr[]
int maxCntRemovedfromArray(int arr[], int N,
                           int brr[], int M)
{

    // Sort the array arr[]
    sort(arr, arr + N);

    // Stores index of smallest
    // element of arr[]
    int i = 0;

    // Stores sum of elements
    // of the array arr[]
    int sumArr = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update sumArr
        sumArr += arr[i];
    }

    // Stores sum of elements
    // of the array brr[]
    int sumBrr = 0;

    // Traverse the array brr[]
    for (int i = 0; i < M; i++) {

        // Update sumArr
        sumBrr += brr[i];
    }

    // Stores count of
    // removed elements
    int cntRemElem = 0;

    // Repeatedly remove the smallest
    // element of arr[]
    while (i < N and sumArr >= sumBrr) {

        // Update sumArr
        sumArr -= arr[i];

        // Remove the smallest element
        i += 1;

        // If the sum of remaining elements
        // in arr[] >= sum of brr[]
        if (sumArr >= sumBrr) {

            // Update cntRemElem
            cntRemElem += 1;
        }
    }

    return cntRemElem;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 4, 6 };

    int brr[] = { 7 };

    int N = sizeof(arr) / sizeof(arr[0]);

    int M = sizeof(brr) / sizeof(brr[0]);

    cout << maxCntRemovedfromArray(arr, N, brr, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG
{

    // Function to maximize the count of elements
    // required to be removed from arr[] such that
    // the sum of arr[] is greater than or equal
    // to sum of the array brr[]
    static int maxCntRemovedfromArray(int[] arr, int N,
                                      int[] brr, int M)
    {

        // Sort the array arr[]
        Arrays.sort(arr);

        // Stores index of smallest
        // element of arr[]
        int i = 0;

        // Stores sum of elements
        // of the array arr[]
        int sumArr = 0;

        // Traverse the array arr[]
        for (i = 0; i < N; i++)       
        {

            // Update sumArr
            sumArr += arr[i];
        }

        // Stores sum of elements
        // of the array brr[]
        int sumBrr = 0;

        // Traverse the array brr[]
        for (i = 0; i < M; i++)
        {

            // Update sumArr
            sumBrr += brr[i];
        }

        // Stores count of
        // removed elements
        int cntRemElem = 0;

        // Repeatedly remove the smallest
        // element of arr[]
        while (i < N && sumArr >= sumBrr) {

            // Update sumArr
            sumArr -= arr[i];

            // Remove the smallest element
            i += 1;

            // If the sum of remaining elements
            // in arr[] >= sum of brr[]
            if (sumArr >= sumBrr) {

                // Update cntRemElem
                cntRemElem += 1;
            }
        }
        return cntRemElem;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = new int[] { 1, 2, 4, 6 };
        int[] brr = new int[] { 7 };
        int N = arr.length;
        int M = brr.length;
        System.out.println(
            maxCntRemovedfromArray(arr, N, brr, M));
    }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to maximize the count of elements
# required to be removed from arr[] such that
# the sum of arr[] is greater than or equal
# to sum of the array brr[]
def maxCntRemovedfromArray(arr, N, brr, M):

    # Sort the array arr[]
    arr.sort(reverse = False)

    # Stores index of smallest
    # element of arr[]
    i = 0

    # Stores sum of elements
    # of the array arr[]
    sumArr = 0

    # Traverse the array arr[]
    for i in range(N):

        # Update sumArr
        sumArr += arr[i]

    # Stores sum of elements
    # of the array brr[]
    sumBrr = 0

    # Traverse the array brr[]
    for i in range(M):

        # Update sumArr
        sumBrr += brr[i]

    # Stores count of
    # removed elements
    cntRemElem = 0

    # Repeatedly remove the smallest
    # element of arr[]
    while (i < N and sumArr >= sumBrr):

        # Update sumArr
        sumArr -= arr[i]

        # Remove the smallest element
        i += 1

        # If the sum of remaining elements
        # in arr[] >= sum of brr[]
        if (sumArr >= sumBrr):

            # Update cntRemElem
            cntRemElem += 1

    return cntRemElem

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 4, 6 ]

    brr = [7]

    N = len(arr)

    M = len(brr)

    print(maxCntRemovedfromArray(arr, N, brr, M))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to maximize the count of elements
    // required to be removed from arr[] such that
    // the sum of arr[] is greater than or equal
    // to sum of the array brr[]
    static int maxCntRemovedfromArray(int[] arr, int N,
                                      int[] brr, int M)
    {

        // Sort the array arr[]
        Array.Sort(arr);

        // Stores index of smallest
        // element of arr[]
        int i = 0;

        // Stores sum of elements
        // of the array arr[]
        int sumArr = 0;

        // Traverse the array arr[]
        for (i = 0; i < N; i++)
        {

            // Update sumArr
            sumArr += arr[i];
        }

        // Stores sum of elements
        // of the array brr[]
        int sumBrr = 0;

        // Traverse the array brr[]
        for (i = 0; i < M; i++)
        {

            // Update sumArr
            sumBrr += brr[i];
        }

        // Stores count of
        // removed elements
        int cntRemElem = 0;

        // Repeatedly remove the smallest
        // element of arr[]
        while (i < N && sumArr >= sumBrr)
        {

            // Update sumArr
            sumArr -= arr[i];

            // Remove the smallest element
            i += 1;

            // If the sum of remaining elements
            // in arr[] >= sum of brr[]
            if (sumArr >= sumBrr)
            {

                // Update cntRemElem
                cntRemElem += 1;
            }
        }
        return cntRemElem;
    }

    // Driver Code
    static public void Main()
    {
        int[] arr = new int[] { 1, 2, 4, 6 };
        int[] brr = new int[] { 7 };
        int N = arr.Length;
        int M = brr.Length;
        Console.WriteLine(
            maxCntRemovedfromArray(arr, N, brr, M));
    }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program of the above approach

    // Function to maximize the count of elements
    // required to be removed from arr[] such that
    // the sum of arr[] is greater than or equal
    // to sum of the array brr[]
    function maxCntRemovedfromArray(arr, N, brr, M)
    {

        // Sort the array arr[]
        arr.sort();

        // Stores index of smallest
        // element of arr[]
        let i = 0;

        // Stores sum of elements
        // of the array arr[]
        let sumArr = 0;

        // Traverse the array arr[]
        for (i = 0; i < N; i++)      
        {

            // Update sumArr
            sumArr += arr[i];
        }

        // Stores sum of elements
        // of the array brr[]
        let sumBrr = 0;

        // Traverse the array brr[]
        for (i = 0; i < M; i++)
        {

            // Update sumArr
            sumBrr += brr[i];
        }

        // Stores count of
        // removed elements
        let cntRemElem = 0;

        // Repeatedly remove the smallest
        // element of arr[]
        while (i < N && sumArr >= sumBrr) {

            // Update sumArr
            sumArr -= arr[i];

            // Remove the smallest element
            i += 1;

            // If the sum of remaining elements
            // in arr[] >= sum of brr[]
            if (sumArr >= sumBrr) {

                // Update cntRemElem
                cntRemElem += 1;
            }
        }
        return cntRemElem;
    }

    // Driver Code

          let arr = [ 1, 2, 4, 6 ];
        let brr = [ 7 ];
        let N = arr.length;
        let M = brr.length;
        document.write(
        maxCntRemovedfromArray(arr, N, brr, M)
        );

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*
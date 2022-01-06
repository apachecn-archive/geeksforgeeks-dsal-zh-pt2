# 排序数组的最少插入次数

> 原文:[https://www . geesforgeks . org/minimum-insertions-sort-array/](https://www.geeksforgeeks.org/minimum-insertions-sort-array/)

给定一个整数数组，我们需要以最少的步骤对这个数组进行排序，在一个步骤中，我们可以将任何数组元素从它的位置插入到任何其他位置。
**例:**

```
Input  : arr[] = [2, 3, 5, 1, 4, 7, 6]
Output : 3
We can sort above array in 3 insertion 
steps as shown below,
1 before array value 2
4 before array value 5
6 before array value 7

Input : arr[] = {4, 6, 5, 1}
Output : 2
```

我们可以用动态规划来解决这个问题。要观察的主要事情是，移动一个元素不会改变除了正在移动的元素之外的元素的相对顺序。现在考虑[最长的递增子序列(LIS)](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/) ，其中相等的元素也被作为递增序列的一部分，现在如果保持这个递增序列的元素不变并移动所有其他元素，那么它将采取最少的步骤，因为我们已经采取了最长的不需要移动的子序列。最后，答案将是数组的大小减去最长递增子序列的大小。
由于 [LIS 问题](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)可以在 O(N^2 用 O(N)个额外空间使用动态规划来解决。
以下是以上思路的实现。

## C++

```
// C++ program to get minimum number of insertion
// steps to sort an array
#include <bits/stdc++.h>
using namespace std;

//  method returns min steps of insertion we need
// to perform to sort array 'arr'
int minInsertionStepToSortArray(int arr[], int N)
{
    // lis[i] is going to store length of lis
    // that ends with i.
    int lis[N];

    /* Initialize lis values for all indexes */
    for (int i = 0; i < N; i++)
        lis[i] = 1;

    /* Compute optimized lis values in bottom up manner */
    for (int i = 1; i < N; i++)
        for (int j = 0; j < i; j++)
            if (arr[i] >= arr[j] && lis[i] < lis[j] + 1)
                lis[i] = lis[j] + 1;

    /* The overall LIS must end with of the array
       elements. Pick maximum of all lis values */
    int max = 0;
    for (int i = 0; i < N; i++)
        if (max < lis[i])
            max = lis[i];

    // return size of array minus length of LIS
    // as final result
    return (N - max);
}

// Driver code to test above methods
int main()
{
    int arr[] = {2, 3, 5, 1, 4, 7, 6};
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minInsertionStepToSortArray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get minimum number of insertion
// steps to sort an array
class Main
{

    //  method returns min steps of insertion we need
    // to perform to sort array 'arr'
    static int minInsertionStepToSortArray(int arr[], int N)
    {
        // lis[i] is going to store length of lis
        // that ends with i.
        int[] lis = new int[N];

        /* Initialize lis values for all indexes */
        for (int i = 0; i < N; i++)
            lis[i] = 1;

        /* Compute optimized lis values in bottom up manner */
        for (int i = 1; i < N; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] >= arr[j] && lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;

        /* The overall LIS must end with of the array
           elements. Pick maximum of all lis values */
        int max = 0;
        for (int i = 0; i < N; i++)
            if (max < lis[i])
                max = lis[i];

        // return size of array minus length of LIS
        // as final result
        return (N - max);
    }

    // Driver code to test above methods
    public static void main (String[] args)
    {
        int arr[] = {2, 3, 5, 1, 4, 7, 6};
        int N = arr.length;
        System.out.println(minInsertionStepToSortArray(arr, N));
    }
}

/* This code is contributed by Harsh Agarwal */
```

## 蟒蛇 3

```
# Python3 program to get minimum number
# of insertion steps to sort an array

# method returns min steps of insertion
# we need to perform to sort array 'arr'
def minInsertionStepToSortArray(arr, N):

    # lis[i] is going to store length
    # of lis that ends with i.
    lis = [0] * N

    # Initialize lis values for all indexes
    for i in range(N):
        lis[i] = 1

    # Compute optimized lis values in
    # bottom up manner
    for i in range(1, N):
        for j in range(i):
            if (arr[i] >= arr[j] and
                lis[i] < lis[j] + 1):
                lis[i] = lis[j] + 1

    # The overall LIS must end with of the array
    # elements. Pick maximum of all lis values
    max = 0
    for i in range(N):
        if (max < lis[i]):
            max = lis[i]

    # return size of array minus length
    # of LIS as final result
    return (N - max)

# Driver Code
if __name__ == "__main__":
    arr = [2, 3, 5, 1, 4, 7, 6]
    N = len(arr)
    print (minInsertionStepToSortArray(arr, N))

# This code is contributed by ita_c
```

## C#

```
// C# program to get minimum number of
// insertion steps to sort an array
using System;

class GfG {

    // method returns min steps of insertion
    // we need to perform to sort array 'arr'
    static int minInsertionStepToSortArray(
                             int []arr, int N)
    {

        // lis[i] is going to store length
        // of lis that ends with i.
        int[] lis = new int[N];

        /* Initialize lis values for all
        indexes */
        for (int i = 0; i < N; i++)
            lis[i] = 1;

        /* Compute optimized lis values in
        bottom up manner */
        for (int i = 1; i < N; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] >= arr[j] &&
                        lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;

        /* The overall LIS must end with of
        the array elements. Pick maximum
        of all lis values */
        int max = 0;

        for (int i = 0; i < N; i++)
            if (max < lis[i])
                max = lis[i];

        // return size of array minus length
        // of LIS as final result
        return (N - max);
    }

    // Driver code to test above methods
    public static void Main (String[] args)
    {
        int []arr = {2, 3, 5, 1, 4, 7, 6};
        int N = arr.Length;

        Console.Write(
          minInsertionStepToSortArray(arr, N));
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get minimum
// number of insertion steps
// to sort an array

// method returns min steps of
// insertion we need to perform
// to sort array 'arr'
function minInsertionStepToSortArray($arr, $N)
{
    // lis[i] is going to store
    // length of lis that ends with i.
    $lis[$N] = 0;

    /* Initialize lis values
    for all indexes */
    for ($i = 0; $i < $N; $i++)
        $lis[$i] = 1;

    /* Compute optimized lis values
       in bottom up manner */
    for ($i = 1; $i < $N; $i++)
        for ($j = 0; $j < $i; $j++)
            if ($arr[$i] >= $arr[$j] &&
                $lis[$i] < $lis[$j] + 1)

                $lis[$i] = $lis[$j] + 1;

    /* The overall LIS must end with
    of the array elements. Pick
    maximum of all lis values */
    $max = 0;
    for ($i = 0; $i < $N; $i++)
        if ($max < $lis[$i])
            $max = $lis[$i];

    // return size of array minus
    // length of LIS as final result
    return ($N - $max);
}

// Driver code
$arr = array(2, 3, 5, 1, 4, 7, 6);
$N = sizeof($arr) / sizeof($arr[0]);
echo minInsertionStepToSortArray($arr, $N);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Javascript program to get minimum number of insertion
// steps to sort an array

    //  method returns min steps of insertion we need
    // to perform to sort array 'arr'
    function minInsertionStepToSortArray(arr,N)
    {

        // lis[i] is going to store length of lis
        // that ends with i.
        let lis = new Array(N);

        /* Initialize lis values for all indexes */
        for (let i = 0; i < N; i++)
        {
            lis[i] = 1;
        }

        /* Compute optimized lis values in bottom up manner */
        for (let i = 1; i < N; i++)
        {
            for (let j = 0; j < i; j++)
            {
                if (arr[i] >= arr[j] && lis[i] < lis[j] + 1)
                {
                    lis[i] = lis[j] + 1;
                }
            }
        }

        /* The overall LIS must end with of the array
           elements. Pick maximum of all lis values */
        let max = 0;
        for (let i = 0; i < N; i++)
        {
            if (max < lis[i])
            {
                max = lis[i];
            }
        }

        // return size of array minus length of LIS
        // as final result
        return (N - max);
    }

    // Driver code to test above methods
    let arr = new Array(2, 3, 5, 1, 4, 7, 6);
    let N = arr.length;
    document.write(minInsertionStepToSortArray(arr, N));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
3
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
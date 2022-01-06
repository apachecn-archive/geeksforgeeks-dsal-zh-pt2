# O(n ^ log n)中最长的双子序列

> 原文:[https://www . geesforgeks . org/long-bitonic-subserial-onlogn/](https://www.geeksforgeeks.org/longest-bitonic-subsequence-onlogn/)

给定一个包含 n 个正整数的数组 arr[0 … n-1]，如果 arr[]的子序列先递增后递减，则称之为 Bitonic。编写一个函数，以数组为参数，返回最长的双音素子序列的长度。
按递增顺序排序的序列被视为双音素序列，递减部分为空。类似地，递减顺序被认为是 Bitonic，递增部分为空。
预期时间复杂度:0(n log n)

**示例:**

```
Input arr[] = {1, 11, 2, 10, 4, 5, 2, 1};
Output: 6 
Explanation : A Longest Bitonic Subsequence 
            of length 6 is 1, 2, 10, 4, 2, 1

Input arr[] = {12, 11, 40, 5, 3, 1}
Output: 5 
Explanation : A Longest Bitonic Subsequence 
            of length 5 is 12, 11, 5, 3, 1)

Input arr[] = {80, 60, 30, 40, 20, 10}
Output: 5 
Explanation : A Longest Bitonic Subsequence
         of length 5 is 80, 60, 30, 20, 10)
```

我们在[动态规划|集合 15(最长双调和子序列)](https://www.geeksforgeeks.org/dynamic-programming-set-15-longest-bitonic-subsequence/)
中讨论了 O(n <sup>2</sup> )解，思路是按照[最长递增子序列大小(n log n)](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/) 来看最长递增子序列(LIS)的计算方式长度。

**算法:**

```
Step 1: Define 4 Auxiliary arrays of size n:
        increasing[n] to calculate LIS of the 
        array  tail1[n] to store the values for 
        LIS for increasing[n]
        decreasing[n] to calculate LIS of the 
        array  tail2[n] to store the values for
        LIS for decreasing[n]
Step 2: Find LIS for increasing array
Step 3: Reverse array and store it in decreasing
Step 4: Find LIS for decreasing array
Step 5: Longest Bitonicc SubSequence length now 
        will be max of tail1[i] + tail2[i] + 1
```

## C++

```
// C++ program to find length of longest
// Bitonic subsequence in O (n Log n( time,
#include <bits/stdc++.h>
using namespace std;

// Binary Search
int ceilIndex(int arr[], int l, int r, int x)
{
    if (l > r)
        return -1;

    int mid = l + (r - l) / 2;
    if (arr[mid] == x)
        return mid;

    if (x < arr[mid])
        return ceilIndex(arr, l, mid - 1, x);

    return ceilIndex(arr, mid + 1, r, x);

}

// function to reverse an array
void revereseArr(int arr[], int n)
{
    int i = 0;
    int j = n - 1;
    while (i < j)
       swap(arr[i++], arr[j--]);
}

// Returns length of longest Bitonic
// subsequence in O(n Log n) time.
int getLBSLengthLogn(int arr[], int n)
{
    // Base Case:
    if (n == 0)
        return 0;

    // Aux array storing the input array
    // in same order to calculate LIS:
    int increasing[n];
    int tail1[n];  // To store lengths of IS

    // Aux array storing the input array
    // in reverse order to calculate LIS:
    // This will calculate Longest Decreasing
    // Subsequence which is required for
    // Longest Bitonic Subsequence
    int decreasing[n];
    int tail2[n]; // To store lengths of DS

    // initializing first index same as
    // original array:
    increasing[0] = arr[0];

    // index in initialized as 1 from where
    // the remaining computations will be done
    int in = 1;

    // tail1 stores Longest Increasing subsequence
    // length values till index in
    tail1[0] = 0;

    // remaining computations to get the
    // LIS length for increasing
    for (int i = 1; i < n; i++)
    {
        if (arr[i] < increasing[0])
        {
            increasing[0] = arr[i];
            tail1[i] = 0;
        }
        else if (arr[i] > increasing[in - 1])
        {
            increasing[in++] = arr[i];
            tail1[i] = in - 1;
        }
        else
        {
            increasing[ceilIndex(increasing, -1,
                        in - 1, arr[i])] = arr[i];
            tail1[i] = ceilIndex(increasing, -1,
                                   in - 1, arr[i]);
        }
    }

    // reiitializing the index to 1
    in = 1;

    // reversing the array to get the Longest
    // Decreasing Subsequence Length:
    revereseArr(arr, n);
    decreasing[0] = arr[0];
    tail2[0] = 0;

    for (int i = 1; i < n; i++)
    {
        if (arr[i] < decreasing[0])
        {
            decreasing[0] = arr[i];
            tail2[i] = 0;
        }
        else if (arr[i] > decreasing[in - 1])
        {
            decreasing[in++] = arr[i];
            tail2[i] = in - 1;
        }
        else
        {
            decreasing[ceilIndex(decreasing, -1,
                      in - 1, arr[i])] = arr[i];
            tail2[i] = ceilIndex(decreasing, -1,
                                 in - 1, arr[i]);
        }
    }

    revereseArr(arr, n);
    revereseArr(tail2, n);

    // Longest Bitonic Subsequence length is
    // maximum of tail1[i] + tail2[i] + 1:
    int ans = 0;
    for (int i = 0; i < n; i++)
        if (ans < (tail1[i] + tail2[i] + 1))
            ans = (tail1[i] + tail2[i] + 1);

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 0, 8, 4, 12, 2, 10, 6, 14,
                  1, 9, 5, 13, 3, 11, 7, 15
                };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << getLBSLengthLogn(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of longest
// Bitonic subsequence in O (n Log n) time,
import java.util.Arrays;
public class GFG
{
    // function to reverse an array
    static void revereseArr(int arr[])
    {
        int i = 0;
        int j = arr.length - 1;
        while (i < j)
        {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;j--;
        }
    }

    // Returns length of longest Bitonic
    // subsequence in O(n Log n) time.
    static int getLBSLengthLogn(int arr[])
    {
        int n = arr.length;

        // Base Case:
        if(n==0)
            return 0;

        /*Aux array storing the input array
        in same order to calculate LIS:*/
        int increasing[] = new int[n];

        //to store lengths of IS
        int tail1[] = new int[n];

        /*Aux array storing the input array
          in reverse order to calculate LIS:
          This will calculate Longest Decreasing
          Subsequence which is required for
          Longest Bitonic Subsequence*/
        int decreasing[] = new int[n];

        // To store lengths of DS
        int tail2[] = new int[n];

        // initializing first index same as
        // original array:
        increasing[0] = arr[0];

        // index in initialized as 1 from where
        // the remaining computations will be done
        int in = 1;

        // tail1 stores Longest Increasing
        // subsequence length values till index in
        tail1[0] = 0;

        // remaining computations to get the
        // LIS length for increasing
        for(int i = 1; i < n; i++)
        {
            if(arr[i] < increasing[0])
            {
                increasing[0] = arr[i];
                tail1[i] = 0;
            }
            else if(arr[i] > increasing[in - 1])
            {
                increasing[in++] = arr[i];
                tail1[i] = in - 1;
            }
            else
            {
                int getIndex1 = Arrays.binarySearch(increasing,
                                                0, in, arr[i]);
                if(getIndex1 <= -1)
                    continue;

                increasing[getIndex1] = arr[i];
                tail1[i] = getIndex1;
            }
        }

        // reinitializing the index to 1
        in = 1;

        // reversing the array to get the Longest
        // Decreasing Subsequence Length:
        revereseArr(arr);
        decreasing[0] = arr[0];
        tail2[0] = 0;

        for(int i = 0; i < n; i++)
        {
            if(arr[i] < decreasing[0])
            {
                decreasing[0] = arr[i];
                tail2[i] = 0;
            }
            else if(arr[i] > decreasing[in - 1])
            {
                decreasing[in++] = arr[i];
                tail2[i] = in - 1;
            }
            else
            {
                int getIndex2 =  Arrays.binarySearch(decreasing,
                                                0, in , arr[i]);
                if(getIndex2 <= -1)
                    continue;

                decreasing[getIndex2] = arr[i];
                tail2[i] = getIndex2;

            }
        }

        revereseArr(arr);
        revereseArr(tail2);

        // Longest Bitonic Subsequence length is
        // maximum of tail1[i] + tail2[i] + 1:
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            if (ans < (tail1[i] + tail2[i] + 1))
                ans = (tail1[i] + tail2[i] + 1);
        }
        return ans;
    }

    // Driver code to test above methods
    public static void main(String[] args)
    {
        int arr[] = { 0, 8, 4, 12, 2, 10, 6, 14,
                      1, 9, 5, 13, 3, 11, 7, 15 };
        System.out.println(getLBSLengthLogn(arr));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python3 program to find length of longest
# Bitonic subsequence in O (n Log n) time

# Binary Search
def ceilIndex(arr, l, r, x):
    if (l > r):
        return -1

    mid = l + (r - l) / 2
    if (arr[mid] == x):
        return mid

    if (x < arr[mid]):
        return ceilIndex(arr, l, mid - 1, x)

    return ceilIndex(arr, mid + 1, r, x)

# Function to reverse an array
def revereseArr(arr, n):
    i = 0
    j = n - 1
    while (i < j):
        t = arr[i]
        arr[i] = arr[j]
        arr[j] = t
        i += 1
        j -= 1

# Returns length of longest Bitonic
# subsequence in O(n Log n) time.
def getLBSLengthLogn(arr, n):

    # Base Case:
    if (n == 0):
        return 0

    # Aux array storing the input array
    # in same order to calculate LIS:
    increasing = [0 for i in range(n)]
    tail1 = [0 for i in range(n)]  # To store lengths of LIS

    # Aux array storing the input array
    # in reverse order to calculate LIS:
    # This will calculate Longest Decreasing
    # Subsequence which is required for
    # Longest Bitonic Subsequence
    decreasing = [0 for i in range(n)]
    tail2 = [0 for i in range(n)]   # To store lengths of DS

    # initializing first index same as
    # original array:
    increasing [0] = arr [0]

    # index in initialized as 1 from where
    # the remaining computations will be done
    ind = 1

    # tail1 stores Longest Increasing subsequence
    # length values till index in
    tail1[0] = 0

    # remaining computations to get the
    # LIS length for increasing
    for i in range(1, n):
        if (arr[i] < increasing[0]):
            increasing[0] = arr[i]
            tail1[i] = 0
        elif (arr[i] > increasing[ind - 1]):
            increasing[ind] = arr[i]
            ind += 1
            tail1[i] = ind - 1
        else:
            increasing[ceilIndex(increasing, -1,
                        ind - 1, arr[i])] = arr[i]
            tail1[i] = ceilIndex(increasing, -1,
                                   ind- 1, arr[i])

    # reinitializing the index to 1
    ind = 1

    # reversing the array to get the Longest
    # Decreasing Subsequence Length:
    revereseArr(arr, n)
    decreasing[0] = arr[0]
    tail2[0] = 0
    for i in range(1, n):
        if (arr[i] < decreasing[0]):
            decreasing[0] = arr[i]
            tail2[i] = 0
        elif (arr[i] > decreasing[ind - 1]):
            decreasing[ind] = arr[i]
            ind += 1
            tail2[i] = ind - 1
        else:
            decreasing[ceilIndex(decreasing, -1,
                      ind - 1, arr[i])] = arr[i]
            tail2[i] = ceilIndex(decreasing, -1,
                                 ind - 1, arr[i])
    revereseArr(arr, n)
    revereseArr(tail2, n)
    # Longest Bitonic Subsequence length is
    # maximum of tail1[i] + tail2[i] + 1:
    ans = 0
    for i in range(n):
        if (ans < (tail1[i] + tail2[i] + 1)):
            ans = (tail1[i] + tail2[i] + 1)

    return ans

# Driver code
arr = [ 0, 8, 4, 12, 2, 10, 6, 14,
                  1, 9, 5, 13, 3, 11, 7, 15]
n = len(arr)
print getLBSLengthLogn(arr, n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find length of longest
// Bitonic subsequence in O (n Log n) time,
using System;

public class GFG {

    // function to reverse an array
    static void revereseArr(int []arr)
    {
        int i = 0;
        int j = arr.Length - 1;
        while (i < j)
        {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }
    }

    // Returns length of longest Bitonic
    // subsequence in O(n Log n) time.
    static int getLBSLengthLogn(int []arr)
    {
        int n = arr.Length;

        // Base Case:
        if(n == 0)
            return 0;

        /*Aux array storing the input array
        in same order to calculate LIS:*/
        int []increasing = new int[n];

        //to store lengths of IS
        int []tail1 = new int[n];

        /*Aux array storing the input array
        in reverse order to calculate LIS:
        This will calculate Longest Decreasing
        Subsequence which is required for
        Longest Bitonic Subsequence*/
        int []decreasing = new int[n];

        // To store lengths of DS
        int []tail2 = new int[n];

        // initializing first index same as
        // original array:
        increasing[0] = arr[0];

        // index in initialized as 1 from where
        // the remaining computations will be done
        int inn = 1;

        // tail1 stores Longest Increasing
        // subsequence length values till index in
        tail1[0] = 0;

        // remaining computations to get the
        // LIS length for increasing
        for(int i = 1; i < n; i++)
        {
            if(arr[i] < increasing[0])
            {
                increasing[0] = arr[i];
                tail1[i] = 0;
            }
            else if(arr[i] > increasing[inn - 1])
            {
                increasing[inn++] = arr[i];
                tail1[i] = inn - 1;
            }
            else
            {
                int getIndex1 = Array.BinarySearch(increasing,
                                                0, inn, arr[i]);
                if(getIndex1 <= -1)
                    continue;

                increasing[getIndex1] = arr[i];
                tail1[i] = getIndex1;
            }
        }

        // reinitializing the index to 1
        inn = 1;

        // reversing the array to get the Longest
        // Decreasing Subsequence Length:
        revereseArr(arr);
        decreasing[0] = arr[0];
        tail2[0] = 0;

        for(int i = 0; i < n; i++)
        {
            if(arr[i] < decreasing[0])
            {
                decreasing[0] = arr[i];
                tail2[i] = 0;
            }
            else if(arr[i] > decreasing[inn - 1])
            {
                decreasing[inn++] = arr[i];
                tail2[i] = inn - 1;
            }
            else
            {
                int getIndex2 = Array.BinarySearch(decreasing,
                                             0, inn , arr[i]);
                if(getIndex2 <= -1)
                    continue;

                decreasing[getIndex2] = arr[i];
                tail2[i] = getIndex2;

            }
        }

        revereseArr(arr);
        revereseArr(tail2);

        // Longest Bitonic Subsequence length is
        // maximum of tail1[i] + tail2[i] + 1:
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            if (ans < (tail1[i] + tail2[i] + 1))
                ans = (tail1[i] + tail2[i] + 1);
        }
        return ans;
    }

    // Driver code to test above methods
    public static void Main()
    {
        int []arr = { 0, 8, 4, 12, 2, 10, 6, 14,
                     1, 9, 5, 13, 3, 11, 7, 15 };
        Console.Write(getLBSLengthLogn(arr));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of longest
// Bitonic subsequence in O (n Log n( time,

// Binary Search
function ceilIndex(&$arr, $l, $r, $x)
{
    if ($l > $r)
        return -1;

    $mid = intval($l + ($r - $l) / 2);
    if ($arr[$mid] == $x)
        return $mid;

    if ($x < $arr[$mid])
        return ceilIndex($arr, $l,
                         $mid - 1, $x);

    return ceilIndex($arr, $mid + 1, $r, $x);
}

// function to reverse an array
function revereseArr(&$arr, $n)
{
    $i = 0;
    $j = $n - 1;
    while ($i < $j)
    {
        $temp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $temp;
        $i++;
        $j--;
    }
}

// Returns length of longest Bitonic
// subsequence in O(n Log n) time.
function getLBSLengthLogn(&$arr, $n)
{
    // Base Case:
    if ($n == 0)
        return 0;

    // Aux array storing the input array
    // in same order to calculate LIS:
    $increasing = array_fill(0, $n, NULL);
    $tail1 = array_fill(0, $n, NULL); // To store lengths of IS

    // Aux array storing the input array
    // in reverse order to calculate LIS:
    // This will calculate Longest Decreasing
    // Subsequence which is required for
    // Longest Bitonic Subsequence
    $decreasing = array_fill(0, $n, NULL);
    $tail2 = array_fill(0, $n, NULL); // To store lengths of DS

    // initializing first index same as
    // original array:
    $increasing[0] = $arr[0];

    // index in initialized as 1 from where
    // the remaining computations will be done
    $in = 1;

    // tail1 stores Longest Increasing
    // subsequence length values till index in
    $tail1[0] = 0;

    // remaining computations to get the
    // LIS length for increasing
    for ($i = 1; $i < $n; $i++)
    {
        if ($arr[$i] < $increasing[0])
        {
            $increasing[0] = $arr[$i];
            $tail1[$i] = 0;
        }
        else if ($arr[$i] > $increasing[$in - 1])
        {
            $increasing[$in++] = $arr[$i];
            $tail1[$i] = $in - 1;
        }
        else
        {
            $increasing[ceilIndex($increasing, -1,
                        $in - 1, $arr[$i])] = $arr[$i];
            $tail1[$i] = ceilIndex($increasing, -1,
                                   $in - 1, $arr[$i]);
        }
    }

    // reiitializing the index to 1
    $in = 1;

    // reversing the array to get the Longest
    // Decreasing Subsequence Length:
    revereseArr($arr, $n);
    $decreasing[0] = $arr[0];
    $tail2[0] = 0;

    for ($i = 1; $i < $n; $i++)
    {
        if ($arr[$i] < $decreasing[0])
        {
            $decreasing[0] = $arr[$i];
            $tail2[$i] = 0;
        }
        else if ($arr[$i] > $decreasing[$in - 1])
        {
            $decreasing[$in++] = $arr[$i];
            $tail2[$i] = $in - 1;
        }
        else
        {
            $decreasing[ceilIndex($decreasing, -1,
                    $in - 1, $arr[$i])] = $arr[$i];
            $tail2[$i] = ceilIndex($decreasing, -1,
                                $in - 1, $arr[$i]);
        }
    }

    revereseArr($arr, $n);
    revereseArr($tail2, $n);

    // Longest Bitonic Subsequence length is
    // maximum of tail1[i] + tail2[i] + 1:
    $ans = 0;
    for ($i = 0; $i < $n; $i++)
        if ($ans < ($tail1[$i] + $tail2[$i] + 1))
            $ans = ($tail1[$i] + $tail2[$i] + 1);

    return $ans;
}

// Driver code
$arr = array(0, 8, 4, 12, 2, 10, 6, 14,
             1, 9, 5, 13, 3, 11, 7, 15);
$n = sizeof($arr);
echo getLBSLengthLogn($arr, $n) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to find length of longest
// Bitonic subsequence in O (n Log n) time,

    function binarySearch(arr, x, start, end) {

    // Base Condition
    if (start > end) return false;

    // FInd the middle Index
    let mid=Math.floor((start + end)/2);

    // Compare mid with given key x
    if (arr[mid]===x) return true;

    // If element at mid is greater than x,
    // search In the left half of mid
    if(arr[mid] > x)
        return binarySearch(arr, x, start, mid-1);
    else

        // If element at mid is smaller than x,
        // search In the right half of mid
        return binarySearch(arr, x, mid+1, end);
    }

    // function to reverse an array
    function revereseArr(arr)
    {
        let i = 0;
        let j = arr.length - 1;
        while (i < j)
        {
            let temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;j--;
        }
    }

    // Returns length of longest Bitonic
    // subsequence in O(n Log n) time.
    function getLBSLengthLogn(arr)
    {
        let n = arr.length;

        // Base Case:
        if(n==0)
            return 0;

        /*Aux array storIng the Input array
        In same order to calculate LIS:*/
        let IncreasIng = new Array(n);

        //to store lengths of IS
        let tail1 = new Array(n);

        /*Aux array storIng the Input array
          In reverse order to calculate LIS:
          This will calculate Longest DecreasIng
          Subsequence which is required for
          Longest Bitonic Subsequence*/
        let decreasIng = new Array(n);

        // To store lengths of DS
        let tail2 = new Array(n);

        // InitializIng first Index same as
        // origInal array:
        IncreasIng[0] = arr[0];

        // Index In Initialized as 1 from where
        // the remaInIng computations will be done
        let In = 1;

        // tail1 stores Longest IncreasIng
        // subsequence length values till Index In
        tail1[0] = 0;

        // remaInIng computations to get the
        // LIS length for IncreasIng
        for(let i = 1; i < n; i++)
        {
            if(arr[i] < IncreasIng[0])
            {
                IncreasIng[0] = arr[i];
                tail1[i] = 0;
            }
            else if(arr[i] > IncreasIng[In - 1])
            {
                IncreasIng[In++] = arr[i];
                tail1[i] = In - 1;
            }
            else
            {
                let getIndex1 = binarySearch(IncreasIng,
                                                0, In, arr[i]);
                if(getIndex1 <= -1)
                    contInue;

                IncreasIng[getIndex1] = arr[i];
                tail1[i] = getIndex1;
            }
        }

        // reInitializIng the Index to 1
        In = 1;

        // reversIng the array to get the Longest
        // DecreasIng Subsequence Length:
        revereseArr(arr);
        decreasIng[0] = arr[0];
        tail2[0] = 0;

        for(let i = 0; i < n; i++)
        {
            if(arr[i] < decreasIng[0])
            {
                decreasIng[0] = arr[i];
                tail2[i] = 0;
            }
            else if(arr[i] > decreasIng[In - 1])
            {
                decreasIng[In++] = arr[i];
                tail2[i] = In - 1;
            }
            else
            {
                let getIndex2 =  binarySearch(decreasIng,
                                                0, In , arr[i]);
                if(getIndex2 <= -1)
                    contInue;

                decreasIng[getIndex2] = arr[i];
                tail2[i] = getIndex2;

            }
        }

        revereseArr(arr);
        revereseArr(tail2);

        // Longest Bitonic Subsequence length is
        // maximum of tail1[i] + tail2[i] + 1:
        let ans = 0;
        for (let i = 0; i < n; i++)
        {
            if (ans < (tail1[i] + tail2[i] + 1))
                ans = (tail1[i] + tail2[i] + 1);
        }
        return ans;
    }

    // Driver code to test above methods
    let arr=[ 0, 8, 4, 12, 2, 10, 6, 14,
                      1, 9, 5, 13, 3, 11, 7, 15];
    document.write(getLBSLengthLogn(arr));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
7
```

**时间复杂度:**O(nLogn)
T3】辅助空间: O(n)
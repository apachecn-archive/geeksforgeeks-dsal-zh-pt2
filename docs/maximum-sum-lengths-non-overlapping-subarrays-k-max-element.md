# 以 k 为最大元素的非重叠子阵长度的最大和。

> 原文:[https://www . geesforgeks . org/maximum-sum-length-non-重叠-子数组-k-max-element/](https://www.geeksforgeeks.org/maximum-sum-lengths-non-overlapping-subarrays-k-max-element/)

求以 k 为最大元素的非重叠子阵(邻接元素)长度的最大和。
**例:**

```
Input : arr[] = {2, 1, 4, 9, 2, 3, 8, 3, 4} 
        k = 4
Output : 5
{2, 1, 4} => Length = 3
{3, 4} => Length = 2
So, 3 + 2 = 5 is the answer

Input : arr[] = {1, 2, 3, 2, 3, 4, 1} 
        k = 4
Output : 7
{1, 2, 3, 2, 3, 4, 1} => Length = 7

Input : arr = {4, 5, 7, 1, 2, 9, 8, 4, 3, 1}
        k = 4
Ans = 4
{4} => Length = 1
{4, 3, 1} => Length = 3
So, 1 + 3 = 4 is the answer
```

**问题来源:**[https://www . geeksforgeeks . org/Amazon-面试-体验-设置-376-校园-实习/](https://www.geeksforgeeks.org/amazon-interview-experience-set-376-campus-internship/)

**算法:**

```
Traverse the array starting from first element
   Take a loop and keep on incrementing count 
   If element is less than equal to k
       if array element is equal to k, then mark
       a flag

   If flag is marked, add this count to answer

   Take another loop and traverse the array 
   till element is greater than k
return ans
```

## C++

```
// CPP program to calculate max sum lengths of
// non overlapping contiguous subarrays with k as
// max element
#include <bits/stdc++.h>
using namespace std;

// Returns max sum of lengths with maximum element
// as k
int calculateMaxSumLength(int arr[], int n, int k)
{
    int ans = 0; // final sum of lengths

    // number of elements in current subarray
    int count = 0;

    // variable for checking if k appeared in subarray
    int flag = 0;

    for (int i = 0; i < n;) {
        count = 0;
        flag = 0;

        // count the number of elements which are
        // less than equal to k
        while (arr[i] <= k && i < n) {
            count++;
            if (arr[i] == k)
                flag = 1;
            i++;
        }

        // if current element appeared in current
        // subarray add count to sumLength
        if (flag == 1)
            ans += count;   

        // skip the array elements which are
        // greater than k
        while (arr[i] > k && i < n)
            i++;    
    }
    return ans;
}

// driver program
int main()
{
    int arr[] = { 4, 5, 7, 1, 2, 9, 8, 4, 3, 1 };
    int size = sizeof(arr) / sizeof(arr[0]);
    int k = 4;
    int ans = calculateMaxSumLength(arr, size, k);
    cout << "Max Length :: " << ans << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to calculate max sum lengths of
// non overlapping contiguous subarrays with k as
// max element
public class GFG
{
    // Returns max sum of lengths with maximum element
    // as k
    static int calculateMaxSumLength(int arr[], int n, int k) {
        int ans = 0; // final sum of lengths

        // number of elements in current subarray
        int count = 0;

        // variable for checking if k appeared in subarray
        int flag = 0;

        for (int i = 0; i < n;) {
            count = 0;
            flag = 0;

            // count the number of elements which are
            // less than equal to k
            while (i < n && arr[i] <= k) {
                count++;
                if (arr[i] == k)
                    flag = 1;
                i++;
            }

            // if current element appeared in current
            // subarray add count to sumLength
            if (flag == 1)
                ans += count;

            // skip the array elements which are
            // greater than k
            while (i < n && arr[i] > k)
                i++;
        }
        return ans;
    }

    // driver program to test above method
    public static void main(String[] args) {

        int arr[] = { 4, 5, 7, 1, 2, 9, 8, 4, 3, 1 };
        int size = arr.length;
        int k = 4;
        int ans = calculateMaxSumLength(arr, size, k);
        System.out.println("Max Length :: " + ans);
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to calculate max sum lengths of non
# overlapping contiguous subarrays with k as max element

# Returns max sum of lengths with max elements as k
def calculateMaxSumLength(arr, n, k):
    ans = 0 # final sum of lengths
    i=0
    while i < n :

        # number of elements in current sub array
        count = 0

        # Variable for checking if k appeared in the sub array
        flag = 0

        # Count the number of elements which are
        # less than or equal to k
        while i < n and arr[i] <= k :
            count = count + 1
            if arr[i] == k:
                flag = 1
            i = i + 1

        # if current element appeared in current
        # subarray and count to sumLength
        if flag == 1:
            ans = ans + count

        # skip the array elements which are greater than k
        while i < n and arr[i] > k :
            i = i + 1

    return ans

# Driver Program
arr = [4, 5, 7, 1, 2, 9, 8, 4, 3, 1]
size = len(arr)
k = 4
ans = calculateMaxSumLength(arr, size, k)
print "Max Length ::",ans

# Contributed by Rohit
```

## C#

```
// A C# program to calculate max
// sum lengths of non overlapping
// contiguous subarrays with k as
// max element
using System;
class GFG {

    // Returns max sum of lengths
    // with maximum element as k
    static int calculateMaxSumLength(int []arr,
                                     int n,
                                     int k)
    {

        // final sum of lengths
        int ans = 0;

        // number of elements in
        // current subarray
        int count = 0;

        // variable for checking if
        // k appeared in subarray
        int flag = 0;

        for(int i = 0; i < n;)
        {
            count = 0;
            flag = 0;

            // count the number of
            // elements which are
            // less than equal to k
            while (i < n && arr[i] <= k)
            {
                count++;
                if (arr[i] == k)
                    flag = 1;
                i++;
            }

            // if current element
            // appeared in current
            // subarray add count
            // to sumLength
            if (flag == 1)
                ans += count;

            // skip the array
            // elements which are
            // greater than k
            while (i < n && arr[i] > k)
                i++;
        }
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {4, 5, 7, 1, 2, 9, 8, 4, 3, 1};
        int size = arr.Length;
        int k = 4;
        int ans = calculateMaxSumLength(arr, size, k);
        Console.WriteLine("Max Length :: " + ans);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate max sum lengths
// of non overlapping contiguous subarrays
// with k as max element

// Returns max sum of lengths with maximum
// element as k
function calculateMaxSumLength(&$arr, $n, $k)
{
    $ans = 0; // final sum of lengths

    // number of elements in current subarray
    $count = 0;

    // variable for checking if k
    // appeared in subarray
    $flag = 0;

    for ($i = 0; $i < $n😉
    {
        $count = 0;
        $flag = 0;

        // count the number of elements which
        // are less than equal to k
        while ($arr[$i] <= $k && $i < $n)
        {
            $count++;
            if ($arr[$i] == $k)
                $flag = 1;
            $i++;
        }

        // if current element appeared in current
        // subarray add count to sumLength
        if ($flag == 1)
            $ans += $count;

        // skip the array elements which are
        // greater than k
        while ($arr[$i] > $k && $i < $n)
            $i++;    
    }
    return $ans;
}

// Driver Code
$arr = array( 4, 5, 7, 1, 2,   
              9, 8, 4, 3, 1 );
$size = sizeof($arr);
$k = 4;
$ans = calculateMaxSumLength($arr, $size, $k);
echo "Max Length :: " . $ans . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// A Javascript program to calculate max sum lengths of
// non overlapping contiguous subarrays with k as
// max element

    // Returns max sum of lengths with maximum element
    // as k
    function calculateMaxSumLength(arr,n,k)
    {
        let ans = 0; // final sum of lengths

        // number of elements in current subarray
        let count = 0;

        // variable for checking if k appeared in subarray
        let flag = 0;

        for (let i = 0; i < n;) {
            count = 0;
            flag = 0;

            // count the number of elements which are
            // less than equal to k
            while (i < n && arr[i] <= k) {
                count++;
                if (arr[i] == k)
                    flag = 1;
                i++;
            }

            // if current element appeared in current
            // subarray add count to sumLength
            if (flag == 1)
                ans += count;

            // skip the array elements which are
            // greater than k
            while (i < n && arr[i] > k)
                i++;
        }
        return ans;
    }

    // driver program to test above method
    let arr=[4, 5, 7, 1, 2, 9, 8, 4, 3, 1];
    let size = arr.length;
    let k = 4;
    let ans = calculateMaxSumLength(arr, size, k);
    document.write("Max Length :: " + ans);

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Max Length :: 4
```

**时间复杂度:** O(n)
可能看起来像 O(n2)，但仔细看的话，数组只遍历一次
本文由[T5】曼德普辛格 T7】供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用](https://github.com/msdeep14)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
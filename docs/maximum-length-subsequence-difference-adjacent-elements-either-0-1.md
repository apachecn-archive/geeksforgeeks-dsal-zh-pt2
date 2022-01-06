# 相邻元素之间差异为 0 或 1 的最大长度子序列

> 原文:[https://www . geesforgeks . org/最大长度-子序列-差异-相邻元素-任一-0-1/](https://www.geeksforgeeks.org/maximum-length-subsequence-difference-adjacent-elements-either-0-1/)

给定一组 **n 个**整数。问题是找到相邻元素之间的差为 0 或 1 的子序列的最大长度。
示例:

```
Input : arr[] = {2, 5, 6, 3, 7, 6, 5, 8}
Output : 5
The subsequence is {5, 6, 7, 6, 5}.

Input : arr[] = {-2, -1, 5, -1, 4, 0, 3}
Output : 4
The subsequence is {-2, -1, -1, 0}.
```

**来源:**T2【Expedia 采访体验|第 12 集 T4】

这个问题的解决方案非常类似于[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence/)问题。唯一的区别是，这里我们必须检查子序列相邻元素之间的绝对差是 0 还是 1。

## C++

```
// C++ implementation to find maximum length
// subsequence with difference between adjacent
// elements as either 0 or 1
#include <bits/stdc++.h>
using namespace std;

// function to find maximum length subsequence
// with difference between adjacent elements as
// either 0 or 1
int maxLenSub(int arr[], int n)
{
    int mls[n], max = 0;

    // Initialize mls[] values for all indexes
    for (int i=0; i<n; i++)
        mls[i] = 1;

    // Compute optimized maximum length subsequence
    // values in bottom up manner
    for (int i=1; i<n; i++)
        for (int j=0; j<i; j++)
            if (abs(arr[i] - arr[j]) <= 1 &&
                    mls[i] < mls[j] + 1)
                mls[i] = mls[j] + 1;

    // Store maximum of all 'mls' values in 'max'   
    for (int i=0; i<n; i++)
        if (max < mls[i])
            max = mls[i];

    // required maximum length subsequence
    return max;       
}

// Driver program to test above
int main()
{
    int arr[] = {2, 5, 6, 3, 7, 6, 5, 8};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum length subsequence = "
         << maxLenSub(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Maximum length subsequence
// with difference between adjacent elements
// as either 0 or 1
import java.util.*;

class GFG {

    // function to find maximum length subsequence
    // with difference between adjacent elements as
    // either 0 or 1
     public static int maxLenSub(int arr[], int n)
    {
        int mls[] = new int[n], max = 0;

        // Initialize mls[] values for all indexes
        for (int i = 0; i < n; i++)
            mls[i] = 1;

        // Compute optimized maximum length
        // subsequence values in bottom up manner
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (Math.abs(arr[i] - arr[j]) <= 1
                      && mls[i] < mls[j] + 1)
                    mls[i] = mls[j] + 1;

        // Store maximum of all 'mls' values in 'max'   
        for (int i = 0; i < n; i++)
            if (max < mls[i])
                max = mls[i];

        // required maximum length subsequence
        return max;       
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {2, 5, 6, 3, 7, 6, 5, 8};
        int n = arr.length;
        System.out.println("Maximum length subsequence = "+
                               maxLenSub(arr, n));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python implementation to find maximum length
# subsequence with difference between adjacent
# elements as either 0 or 1

# function to find maximum length subsequence
# with difference between adjacent elements as
# either 0 or 1
def maxLenSub( arr, n):
    mls=[]
    max = 0

    #Initialize mls[] values for all indexes
    for i in range(n):
        mls.append(1)

    #Compute optimized maximum length subsequence
    # values in bottom up manner
    for i in range(n):
        for j in range(i):
            if (abs(arr[i] - arr[j]) <= 1 and mls[i] < mls[j] + 1):
                mls[i] = mls[j] + 1

    # Store maximum of all 'mls' values in 'max'
    for i in range(n):
        if (max < mls[i]):
            max = mls[i]

    #required maximum length subsequence
    return max

#Driver program to test above
arr = [2, 5, 6, 3, 7, 6, 5, 8]
n = len(arr)
print("Maximum length subsequence = ",maxLenSub(arr, n))

#This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# Code for Maximum length subsequence
// with difference between adjacent elements
// as either 0 or 1
using System;

class GFG {

    // function to find maximum length subsequence
    // with difference between adjacent elements as
    // either 0 or 1
    public static int maxLenSub(int[] arr, int n)
    {
        int[] mls = new int[n];
        int max = 0;

        // Initialize mls[] values for all indexes
        for (int i = 0; i < n; i++)
            mls[i] = 1;

        // Compute optimized maximum length
        // subsequence values in bottom up manner
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (Math.Abs(arr[i] - arr[j]) <= 1
                    && mls[i] < mls[j] + 1)
                    mls[i] = mls[j] + 1;

        // Store maximum of all 'mls' values in 'max'
        for (int i = 0; i < n; i++)
            if (max < mls[i])
                max = mls[i];

        // required maximum length subsequence
        return max;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 2, 5, 6, 3, 7, 6, 5, 8 };
        int n = arr.Length;
        Console.Write("Maximum length subsequence = " +
                                    maxLenSub(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find maximum length
// subsequence with difference between adjacent
// elements as either 0 or 1

// function to find maximum length subsequence
// with difference between adjacent elements as
// either 0 or 1
function maxLenSub($arr, $n)
{
    $mls = array(); $max = 0;

    // Initialize mls[] values
    // for all indexes
    for($i = 0; $i < $n; $i++)
        $mls[$i] = 1;

    // Compute optimized maximum
    // length subsequence
    // values in bottom up manner
    for ($i = 1; $i < $n; $i++)
        for ( $j = 0; $j < $i; $j++)
            if (abs($arr[$i] - $arr[$j]) <= 1 and
                         $mls[$i] < $mls[$j] + 1)
                $mls[$i] = $mls[$j] + 1;

    // Store maximum of all
    // 'mls' values in 'max'
    for($i = 0; $i < $n; $i++)
        if ($max < $mls[$i])
            $max = $mls[$i];

    // required maximum
    // length subsequence
    return $max;    
}

    // Driver Code
    $arr = array(2, 5, 6, 3, 7, 6, 5, 8);
    $n = count($arr);
    echo "Maximum length subsequence = "
        , maxLenSub($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript Code for
// Maximum length subsequence
// with difference between
// adjacent elements
// as either 0 or 1

    // function to find maximum
    // length subsequence
    // with difference between
    // adjacent elements as
    // either 0 or 1
     function  maxLenSub(arr, n)
    {
        let mls = new Array(n).fill(1), max = 0;

        // Initialize mls[] values for all indexes
        for (let i = 0; i < n; i++)
            mls[i] = 1;

        // Compute optimized maximum length
        // subsequence values in bottom up manner
        for (let i = 1; i < n; i++)
            for (let j = 0; j < i; j++)
                if (Math.abs(arr[i] - arr[j]) <= 1
                      && mls[i] < mls[j] + 1)
                    mls[i] = mls[j] + 1;

        // Store maximum of all 'mls' values in 'max'   
        for (let i = 0; i < n; i++)
            if (max < mls[i])
                max = mls[i];

        // required maximum length subsequence
        return max;       
    }

// driver program

        let arr = [2, 5, 6, 3, 7, 6, 5, 8];
        let n = arr.length;
        document.write("Maximum length subsequence = "+
                               maxLenSub(arr, n));

</script>
```

**输出:**

```
Maximum length subsequence = 5
```

时间复杂度:O(n)<sup>2</sup>)
辅助空间:O(n)
[相邻元素之差为 0 或 1 的最大长度子序列|集合 2](https://www.geeksforgeeks.org/maximum-length-subsequence-difference-adjacent-elements-either-0-1-set-2/)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
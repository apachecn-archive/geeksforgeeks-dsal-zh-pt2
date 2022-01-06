# 最长的分割子序列

> 原文:[https://www.geeksforgeeks.org/longest-dividing-subsequence/](https://www.geeksforgeeks.org/longest-dividing-subsequence/)

给你一个大小为 n 的数组 A，你的任务是找出最大分割子序列的长度。一个划分序列是一个序列 a1，a2，…，aN 其中 ai 每当 i < j. For example, 3, 15, 60, 720 is a dividing sequence. 
**输入-**
时划分 aj 每个测试用例的第一行是 N，其中 N 是数组的大小。
每个测试用例的第二行包含 N 个空格分隔的整数，这是数组的输入。
**输出-**
最大分割子序列的长度
示例:

> 输入:arr[]= { 2 11 16 12 36 60 71 17 29 144 288 129 432 993 }
> 输出:5
> 2 12 36 144 288 正在划分最大尺寸的子序列
> 输入:1 2 4 8 16
> 输出:5
> 整个序列正在划分

这个问题只是[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence/)的一个变种。我们可以使用动态编程来解决这个问题。其思想是找到以每个元素结束的最长的分割子序列，并最终返回最大值。

## C++

```
/* Dynamic Programming C++ implementation of lds problem */
#include<bits/stdc++.h>
using namespace std;

/* lds() returns the length of the longest dividing
  subsequence in arr[] of size n */
int lds( int arr[], int n )
{
    int lds[n];

    lds[0] = 1;  

    /* Compute optimized lds values in bottom up manner */
    for (int i = 1; i < n; i++ )
    {
        lds[i] = 1;
        for (int j = 0; j < i; j++ ) 
            if (lds[j] != 0 && arr[i] % arr[j] == 0)
                lds[i] = max(lds[i], lds[j] + 1);
    }

    // Return maximum value in lds[]
    return *max_element(lds, lds+n);
}

/* Driver program to test above function */
int main()
{
    int arr[] = { 2, 11, 16, 12, 36, 60, 71, 17,
                     29, 144, 288, 129, 432, 993};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Length of lds is %d\n", lds( arr, n ) );
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Dynamic Programming Java implementation of lds problem */

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{
/* lds() returns the length of the longest dividing
  subsequence in arr[] of size n */
static int lds( Integer arr[], int n )
{
    Integer lds[]=new Integer[n];

    lds[0] = 1;  

    /* Compute optimized lds values in bottom up manner */
    for (int i = 1; i < n; i++ )
    {
        lds[i] = 1;
        for (int j = 0; j < i; j++ ) 
            if (lds[j] != 0 && arr[i] % arr[j] == 0)
                lds[i] = Math.max(lds[i], lds[j] + 1);
    }

    // Return maximum value in lds[]
    int max=(int)Collections.max(Arrays.asList(lds));
    return max;
}

/* Driver program to test above function */
public static void main(String args[])
{
    Integer arr[] = { 2, 11, 16, 12, 36, 60, 71, 17,
                     29, 144, 288, 129, 432, 993};
    int n =arr.length ;
    System.out.println("Length of lds is "+lds( arr, n ) );
}
}
```

## 蟒蛇 3

```
# Dynamic Programming Python3
# implementation of lds problem

# lds() returns the length of the longest
# dividing subsequence in arr[] of size n
def lds(arr, n):

    lds = [0 for i in range(n)]

    lds[0] = 1

    # Compute optimized lds values
    # in bottom up manner
    for i in range(n):
        lds[i] = 1
        for j in range(i):
            if (lds[j] != 0 and
                arr[i] % arr[j] == 0):
                lds[i] = max(lds[i], lds[j] + 1)

    return max(lds)

# Driver Code
arr = [2, 11, 16, 12, 36, 60, 71, 17,
         29, 144, 288, 129, 432, 993]

print("Length of lds is",
       lds(arr, len(arr)))

# This code is contributed
# by Mohit Kumar
```

## C#

```
/* Dynamic Programming C# implementation of lds problem */
using System;
using System.Linq;
public class GFG{
    /* lds() returns the length of the longest dividing
      subsequence in arr[] of size n */
    static int lds( int []arr, int n )
    {
        int []lds=new int[n];

        lds[0] = 1;  

        /* Compute optimized lds values in bottom up manner */
        for (int i = 1; i < n; i++ )
        {
            lds[i] = 1;
            for (int j = 0; j < i; j++ ) 
                if (lds[j] != 0 && arr[i] % arr[j] == 0)
                    lds[i] = Math.Max(lds[i], lds[j] + 1);
        }

        // Return maximum value in lds[]
        int max=lds.Max();
        return max;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int []arr = { 2, 11, 16, 12, 36, 60, 71, 17,
                         29, 144, 288, 129, 432, 993};
        int n =arr.Length ;
        Console.Write("Length of lds is "+lds( arr, n ) );
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
/* Dynamic Programming Javascript implementation of lds problem */

/* lds() returns the length of the longest dividing
  subsequence in arr[] of size n */
function lds(arr,n)
{
    let lds = new Array(n);
    lds[0] = 1; 

    /* Compute optimized lds values in bottom up manner */
    for (let i = 1; i < n; i++ )
    {
        lds[i] = 1;
        for (let j = 0; j < i; j++ )
            if (lds[j] != 0 && arr[i] % arr[j] == 0)
                lds[i] = Math.max(lds[i], lds[j] + 1);
    }

    // Return maximum value in lds[]
    let max=Math.max(...lds);
    return max;
}

/* Driver program to test above function */
let arr=[2, 11, 16, 12, 36, 60, 71, 17,
                     29, 144, 288, 129, 432, 993];

let n =arr.length ;
document.write("Length of lds is "+lds( arr, n ) );

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Length of lds is 5
```

**时间复杂度:** O(N*N)

**辅助空间:** O(N)
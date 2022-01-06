# 根据元素在 0 到 n-1 范围内的频率填充数组

> 原文:[https://www . geesforgeks . org/fill-基于数组-频率-元素-范围-0-n-1/](https://www.geeksforgeeks.org/fill-array-based-frequency-elements-range-0-n-1/)

给定允许重复的正整数数组。数组包含从 0 到 n-1 的元素。任务是填充数组，使得 arr[i]包含 i.
的频率

**示例:**

```
Input  : arr[] = {1, 4, 3, 4, 1, 1, 4, 4, 4, 7}
Output : arr[] = {0, 3, 0, 1, 5, 0, 0, 1, 0, 0}
Here 0 appears 0 times, so arr[0] is 0
     1 appears 3 times 
     2 appears 0 times 
     3 appears 0 times 
     4 appears 5 times 
     ..........

Input  : arr[] = {1, 2, 3, 4, 1, 1, 4, 5, 6, 7}
Output : arr[] = {0, 3, 1, 1, 2, 1, 1, 1, 0, 0} 
```

这个问题的一个**简单解决方案**是运行两个循环。外部循环逐个挑选元素。内部循环计算拾取元素的频率，并将频率存储在最终数组中。

一个**有效的解决方案**是使用一个大小为 n 的辅助数组。

```
1) Create an array temp[0..n-1] and 
   initialize it as 0.
2) Traverse given array and do following
   for every element arr[i].
     temp[arr[i]]++
3) Copy temp[] to arr[].
```

下面是以上步骤的实现。

## C++

```
// C++ program to fill an array with frequencies.
#include<bits/stdc++.h>
using namespace std;

// Fills arr[] with frequencies of elements
void fillWithFreq(int arr[], int n)
{
    int temp[n];
    memset(temp, 0, sizeof(temp));

    // Fill temp with frequencies
    for (int i=0; i<n; i++)
        temp[arr[i]] += 1;

    // Copy temp to array
    for (int i=0; i<n; i++)
        arr[i] = temp[i];
}

// Driver code
int main()
{
    int arr[] = {5, 2, 3, 4, 5, 5, 4, 5, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);
    fillWithFreq(arr, n);
    for (int i=0; i<n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to fill an array with frequencies.
import java.util.Arrays;

class GFG {

    // Fills arr[] with frequencies of elements
    static void fillWithFreq(int arr[], int n)
    {

        int temp[]=new int[n];
        Arrays.fill(temp, 0);

        // Fill temp with frequencies
        for (int i = 0; i < n; i++)
            temp[arr[i]] += 1;

        // Copy temp to array
        for (int i = 0; i < n; i++)
            arr[i] = temp[i];
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = {5, 2, 3, 4, 5, 5, 4, 5, 6, 7};
        int n = arr.length;

        fillWithFreq(arr, n);

        for (int i=0; i<n; i++)
            System.out.print(arr[i] + " ");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to fill an
# array with frequencies.

# Fills arr[] with frequencies of elements
def fillWithFreq(arr, n):

    temp = [0 for i in range(n)]

    # Fill temp with frequencies
    for i in range(n):
        temp[arr[i]] += 1

    # Copy temp to array
    for i in range(n):
        arr[i] = temp[i]

# Driver Code
arr = [5, 2, 3, 4, 5, 5, 4, 5, 6, 7]
n = len(arr)
fillWithFreq(arr, n)
for i in range(n):
    print(arr[i], end = " ")

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to fill an
// array with frequencies.
using System;

class GFG {

    // Fills arr[] with frequencies of elements
    static void fillWithFreq(int []arr, int n)
    {
        int []temp = new int[n];
        for(int i = 0; i < n; i++)
         temp[i] = 0;

        // Fill temp with frequencies
        for (int i = 0; i < n; i++)
            temp[arr[i]] += 1;

        // Copy temp to array
        for (int i = 0; i < n; i++)
            arr[i] = temp[i];
    }

    // Driver method
    public static void Main()
    {
        int []arr = {5, 2, 3, 4, 5,
                     5, 4, 5, 6, 7};
        int n = arr.Length;

        // Function calling
        fillWithFreq(arr, n);

        for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to fill an
// array with frequencies.

// Fills arr[] with frequencies
// of elements
function fillWithFreq($arr, $n)
{
    $temp = array();
    for($i = 0; $i < $n; $i++)
    $temp[$i] = 0;

    // Fill temp with frequencies
    for ($i = 0; $i < $n; $i++)
        $temp[$arr[$i]] += 1;

    // Copy temp to array
    for ($i = 0; $i < $n; $i++)
        $arr[$i] = $temp[$i];

    // print array
    for ($i = 0; $i < $n; $i++)
    echo $arr[$i] . " ";
}

// Driver method
$arr = array(5, 2, 3, 4, 5,
             5, 4, 5, 6, 7);
$n = count($arr);

// Function calling
fillWithFreq($arr, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to fill an
    // array with frequencies.

    // Fills arr[] with frequencies of elements
    function fillWithFreq(arr, n)
    {
        let temp = new Array(n);
        for(let i = 0; i < n; i++)
         temp[i] = 0;

        // Fill temp with frequencies
        for (let i = 0; i < n; i++)
            temp[arr[i]] += 1;

        // Copy temp to array
        for (let i = 0; i < n; i++)
            arr[i] = temp[i];
    }

    let arr = [5, 2, 3, 4, 5, 5, 4, 5, 6, 7];
    let n = arr.length;

    // Function calling
    fillWithFreq(arr, n);

    for (let i = 0; i < n; i++)
      document.write(arr[i] + " ");

</script>
```

**输出:**

```
0 0 1 1 2 4 1 1 0 0 
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 一个数组中可以形成的最小连续序列数

> 原文:[https://www . geeksforgeeks . org/数组中可形成的最小连续序列数/](https://www.geeksforgeeks.org/minimum-number-of-consecutive-sequences-that-can-be-formed-in-an-array/)

给定一个整数数组。任务是找到可以使用数组元素形成的最小数量的连续序列。
**例:**

```
Input: arr[] = { -3, -2, -1, 0, 2 }
Output: 2
Consecutive sequences are (-3, -2, -1, 0), (2).

Input: arr[] = { 3, 4, 0, 2, 6, 5, 10 }
Output: 3
Consecutive sequences are (0), {2, 3, 4, 5, 6} and {10}
```

**进场:**

*   对数组排序。
*   迭代数组，检查当前元素是否只比下一个元素小 1。

*   如果是，则将计数增加 1。
*   返回连续序列的最终计数。

**以下是上述方法的实施:**

## C++

```
// C++ program find the minimum number of consecutive
// sequences in an array
#include <bits/stdc++.h>
using namespace std;

int countSequences(int arr[], int n)
{
    int count = 1;

    sort(arr, arr + n);

    for (int i = 0; i < n - 1; i++)
        if (arr[i] + 1 != arr[i + 1])
            count++;

    return count;
}

// Driver program
int main()
{
    int arr[] = { 1, 7, 3, 5, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // function call to print required answer
    cout << countSequences(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program find the minimum number of consecutive
// sequences in an array

import java.util.Arrays;
import java.io.*;

class GFG {

static int countSequences(int arr[], int n)
{
    int count = 1;

    Arrays.sort(arr);

    for (int i = 0; i < n - 1; i++)
        if (arr[i] + 1 != arr[i + 1])
            count++;

    return count;
}

// Driver program
    public static void main (String[] args) {

    int arr[] = { 1, 7, 3, 5, 10 };
    int n = arr.length;
    // function call to print required answer
    System.out.println( countSequences(arr, n));

    }
//This code is contributed by ajit.   
}
```

## 蟒蛇 3

```
# Python3 program find the minimum number of consecutive
# sequences in an array

def countSequences(arr, n) :
    count = 1

    arr.sort()

    for i in range( n -1) :
        if (arr[i] + 1 != arr[i + 1]) :
            count += 1

    return count

# Driver program
if __name__ == "__main__" :

    arr = [ 1, 7, 3, 5, 10 ]
    n = len(arr)

    # function call to print required answer
    print(countSequences(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program find the minimum number of consecutive
// sequences in an array
 using System;
class GFG {

static int countSequences(int []arr, int n)
{
    int count = 1;

    Array.Sort(arr);

    for (int i = 0; i < n - 1; i++)
        if (arr[i] + 1 != arr[i + 1])
            count++;

    return count;
}

// Driver program
    static public void Main (String []args) {

    int []arr = { 1, 7, 3, 5, 10 };
    int n = arr.Length;
    // function call to print required answer
    Console.WriteLine( countSequences(arr, n));

    }
}
//This code is contributed by Arnab Kundu  
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program find the minimum number
// of consecutive sequences in an array

function countSequences($arr, $n)
{
    $count = 1;

    sort($arr);

    for ($i = 0; $i < $n - 1; $i++)
        if ($arr[$i] + 1 != $arr[$i + 1])
            $count++;

    return $count;
}

// Driver Code
$arr = array( 1, 7, 3, 5, 10 );
$n = count($arr);

// function call to print required answer
echo countSequences($arr, $n);

// This code is contributed by inder_verma
?>
```

## java 描述语言

```
<script>

    // Javascript program find the
    // minimum number of consecutive
    // sequences in an array

    function countSequences(arr, n)
    {
        let count = 1;

        arr.sort(function(a, b){return a - b});

        for (let i = 0; i < n - 1; i++)
            if (arr[i] + 1 != arr[i + 1])
                count++;

        return count;
    }

    let arr = [ 1, 7, 3, 5, 10 ];
    let n = arr.length;

    // function call to print required answer
    document.write(countSequences(arr, n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(n log n)，其中 n 为数组的大小。
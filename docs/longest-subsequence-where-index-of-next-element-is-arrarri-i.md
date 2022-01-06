# 最长子序列，其中下一个元素的索引是 arr[arr[i] + i]

> 原文:[https://www . geesforgeks . org/最长子序列-下一个元素的索引是-arrari-I/](https://www.geeksforgeeks.org/longest-subsequence-where-index-of-next-element-is-arrarri-i/)

给定一个数组 **arr[]** ，任务是从满足以下条件的数组中找到最大长度的子序列:
任何元素都可以被选为子序列的第一个元素，但是下一个元素的索引将由**arr【arr[I]+I】**确定，其中 **i** 是序列中前一个元素的索引。
**示例:**

> **输入:** arr[] = {1，2，3，4，5 }
> T3】输出: 1 2 4
> arr[0] = 1，arr[1 + 0] = arr[1] = 2，arr[2 + 1] = arr[3] = 4
> 其他可能的子序列有{2，4}、{3}、{4}和{5}
> **输入:** arr[] = {1，6，3，1，1 2，1

**进场:**

*   利用两个数组**温度**和**打印**。
*   **temp** 数组将存储当前正在考虑的数组元素， **print** 数组将存储要打印的数组元素作为最终输出。
*   从 **0** 迭代到**n–1**，并将当前元素视为序列的第一个元素。
*   将当前序列的所有元素存储到 **temp** 数组中。
*   如果 **temp** 数组的大小大于 **print** 数组，则将 **temp** 数组的所有内容复制到 **print** 数组。
*   当考虑了所有的序列后，打印**打印**数组的内容。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum length sub-sequence
void maxLengthSubSeq(int a[], int n)
{
    // Arrays to store the values to be printed
    int temp[n], print[n];
    int y = 0;

    for (int i = 0; i < n; i++) {
        int j = 0;
        int x = 0;

        // Store the first value into the temp array
        temp[j++] = a[x];

        // Index of the next element
        x = a[x] + x;

        // Iterate till index is in range of the array
        while (x < n) {
            temp[j++] = a[x];
            x = a[x] + x;
        }

        // If the length (temp) > the length (print) then
        // copy the contents of the temp array into
        // the print array
        if (y < j) {
            for (int k = 0; k < j; k++) {
                print[k] = temp[k];
                y = j;
            }
        }
    }

    // Print the contents of the array
    for (int i = 0; i < y; i++)
        cout << print[i] << " ";
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(a) / sizeof(a[0]);
    maxLengthSubSeq(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java  implementation of the approach/

import java.io.*;

class GFG {

// Function to print the maximum length sub-sequence
static void maxLengthSubSeq(int a[], int n)
{
    // Arrays to store the values to be printed
    int temp[]=new int[n];
    int print[]=new int[n];
    int y = 0;

    for (int i = 0; i < n; i++) {
        int j = 0;
        int x = 0;

        // Store the first value into the temp array
        temp[j++] = a[x];

        // Index of the next element
        x = a[x] + x;

        // Iterate till index is in range of the array
        while (x < n) {
            temp[j++] = a[x];
            x = a[x] + x;
        }

        // If the length (temp) > the length (print) then
        // copy the contents of the temp array into
        // the print array
        if (y < j) {
            for (int k = 0; k < j; k++) {
                print[k] = temp[k];
                y = j;
            }
        }
    }

    // Print the contents of the array
    for (int i = 0; i < y; i++)
            System.out.print(print[i] + " ");
}

// Driver code
    public static void main (String[] args) {

    int a[] = { 1, 2, 3, 4, 5 };
    int n = a.length;
    maxLengthSubSeq(a, n);
    }
//This code is contributed by @Tushil.   
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to print the maximum length
# sub-sequence
def maxLengthSubSeq(a, n):

    # Arrays to store the values to be printed
    temp = [0 for i in range(n)]
    print1 = [0 for i in range(n)]
    y = 0

    for i in range(0, n, 1):
        j = 0
        x = 0

        # Store the first value into
        # the temp array
        temp[j] = a[x]
        j += 1

        # Index of the next element
        x = a[x] + x

        # Iterate till index is in range
        # of the array
        while (x < n):
            temp[j] = a[x]
            j += 1
            x = a[x] + x

        # If the length (temp) > the length
        # (print) then copy the contents of
        # the temp array into the print array
        if (y < j):
            for k in range(0, j, 1):
                print1[k] = temp[k]
                y = j

    # Print the contents of the array
    for i in range(0, y, 1):
        print(print1[i], end = " ")

# Driver code
if __name__ == '__main__':
    a = [1, 2, 3, 4, 5]
    n = len(a)
    maxLengthSubSeq(a, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
//C# implementation of the approach/

using System;

public class GFG{

// Function to print the maximum length sub-sequence
static void maxLengthSubSeq(int []a, int n)
{
    // Arrays to store the values to be printed
    int []temp=new int[n];
    int []print=new int[n];
    int y = 0;

    for (int i = 0; i < n; i++) {
        int j = 0;
        int x = 0;

        // Store the first value into the temp array
        temp[j++] = a[x];

        // Index of the next element
        x = a[x] + x;

        // Iterate till index is in range of the array
        while (x < n) {
            temp[j++] = a[x];
            x = a[x] + x;
        }

        // If the length (temp) > the length (print) then
        // copy the contents of the temp array into
        // the print array
        if (y < j) {
            for (int k = 0; k < j; k++) {
                print[k] = temp[k];
                y = j;
            }
        }
    }

    // Print the contents of the array
    for (int i = 0; i < y; i++)
            Console.Write(print[i] + " ");
}

// Driver code
    static public void Main (){

    int []a = { 1, 2, 3, 4, 5 };
    int n = a.Length;
    maxLengthSubSeq(a, n);
    }
//This code is contributed by ajit.
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the maximum
// length sub-sequence
function maxLengthSubSeq($a, $n)
{
    $y = 0;

    for ($i = 0; $i < $n; $i++)
    {
        $j = 0;
        $x = 0;

        // Store the first value into
        // the temp array
        $temp[$j++] = $a[$x];

        // Index of the next element
        $x = $a[$x] + $x;

        // Iterate till index is in
        // range of the array
        while ($x < $n)
        {
            $temp[$j++] = $a[$x];
            $x = $a[$x] + $x;
        }

        // If the length (temp) > the length
        // (print) then copy the contents of
        // the temp array into the print array
        if ($y < $j)
        {
            for ($k = 0; $k < $j; $k++)
            {
                $print[$k] = $temp[$k];
                $y = $j;
            }
        }
    }

    // Print the contents of the array
    for ($i = 0; $i < $y; $i++)
        echo $print[$i] . " ";
}

// Driver code
$a = array(1, 2, 3, 4, 5);
$n = sizeof($a);
maxLengthSubSeq($a, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to print the maximum length sub-sequence
    function maxLengthSubSeq(a, n)
    {
        // Arrays to store the values to be printed
        let temp=new Array(n);
        temp.fill(0);
        let print=new Array(n);
        print.fill(0);
        let y = 0;

        for (let i = 0; i < n; i++) {
            let j = 0;
            let x = 0;

            // Store the first value into the temp array
            temp[j++] = a[x];

            // Index of the next element
            x = a[x] + x;

            // Iterate till index is in range of the array
            while (x < n) {
                temp[j++] = a[x];
                x = a[x] + x;
            }

            // If the length (temp) > the length (print) then
            // copy the contents of the temp array into
            // the print array
            if (y < j) {
                for (let k = 0; k < j; k++) {
                    print[k] = temp[k];
                    y = j;
                }
            }
        }

        // Print the contents of the array
        for (let i = 0; i < y; i++)
                document.write(print[i] + " ");
    }

    let a = [ 1, 2, 3, 4, 5 ];
    let n = a.length;
    maxLengthSubSeq(a, n);

</script>
```

**Output:** 

```
1 2 4
```
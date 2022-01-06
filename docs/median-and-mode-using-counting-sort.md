# 使用计数排序的中值和模式

> 原文:[https://www . geesforgeks . org/median-and-mode-using-counting-sort/](https://www.geeksforgeeks.org/median-and-mode-using-counting-sort/)

给定一个 **n** 大小的未排序数组，使用**计数排序**技术找到中值和模式。当数组元素在有限的范围内时，Thia 会很有用。

**示例:**

```
Input : array a[] = {1, 1, 1, 2, 7, 1}
Output : Mode = 1
         Median = 1
Note : Median is average of middle two numbers (1 and 1)

Input : array a[] = {9, 9, 9, 9, 9}
Output : Mode = 9
         Median = 9

```

**先决条件:** [计数排序](https://www.geeksforgeeks.org/counting-sort/)[数组中值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)，模式([数组中最频繁的元素](https://www.geeksforgeeks.org/find-the-maximum-repeating-number-in-ok-time/)

输入= [1，4，1，2，7，1，2，5，3，6]

1.辅助(计数)数组在对其之前的计数求和之前，c[]:
索引:0 1 2 3 4 5 6 7 8 9 10
计数:0 3 1 1 1 0 0 0 0

2.Mode =具有最大计数值的索引。
模式= 1(上例)

3.计数数组的修改与执行计数排序时的修改类似。
指数:0 1 2 3 4 5 6 7 8 9 10
计数:0 3 5 6 7 8 9 10 10 10

4.输出数组通常按照计数排序计算，b[]:
输出数组 b[] = {1，1，1，2，2，3，4，5，6，7}

5.如果数组 b[]的大小为奇数，则中位数= b[n/2]
否则中位数= (b[(n-1)/2] + b[n/2])/2

6.对于上面的例子，b[]的大小是偶数，因此中位数= (b[4] + b[5])/2。
中位数= (2 + 3)/2 = 2.5

要遵循的基本方法:
假设输入数组的大小为 **n** :
**步骤 1:** 在将计数数组的前一个计数相加到下一个索引之前取计数数组。
**步骤 2:** 其中存储最大值的索引是给定数据的模式。
**步骤 3:** 如果有多个最大值的索引，都是模式的结果，所以我们可以取任意一个。
**步骤 4:** 将该索引处的值存储在一个名为 mode 的单独变量中。
**步骤 5:** 继续计数排序的正常处理。
**步骤 6:** 在结果(排序)数组中，如果 n 是奇数，则中位数= T21 排序数组的最中间元素，如果 n 是偶数，则中位数=排序数组的两个最中间元素的平均值。
**步骤 7:** 将结果存储在一个名为中值的单独变量中。

下面是上面讨论的问题的实现:

## C++

```
// C++ Program for Mode and
// Median using Counting
// Sort technique
#include <bits/stdc++.h>
using namespace std;

// function that sort input array a[] and 
// calculate mode and median using counting
// sort.
void printModeMedian(int a[], int n)
{
    // The output array b[] will
    // have sorted array
    int b[n];

    // variable to store max of
    // input array which will 
    // to have size of count array
    int max = *max_element(a, a+n);

    // auxiliary(count) array to 
    // store count. Initialize
    // count array as 0\. Size
    // of count array will be
    // equal to (max + 1).
    int t = max + 1;
    int count[t];
    for (int i = 0; i < t; i++)
        count[i] = 0;    

    // Store count of each element
    // of input array
    for (int i = 0; i < n; i++)
        count[a[i]]++;    

    // mode is the index with maximum count
    int mode = 0;
    int k = count[0];
    for (int i = 1; i < t; i++)
    {
        if (count[i] > k)
        {
            k = count[i];
            mode = i;
        }
    }    

    // Update count[] array with sum
    for (int i = 1; i < t; i++)
        count[i] = count[i] + count[i-1];

    // Sorted output array b[]
    // to calculate median
    for (int i = 0; i < n; i++)
    {
        b[count[a[i]]-1] = a[i];
        count[a[i]]--;
    }

    // Median according to odd and even 
    // array size respectively.
    float median;
    if (n % 2 != 0)
        median = b[n/2];
    else
        median = (b[(n-1)/2] + 
                  b[(n/2)])/2.0;

    // Output the result 
    cout << "median = " << median << endl;
    cout << "mode = " << mode;
}

// Driver program
int main()
{
    int a[] = { 1, 4, 1, 2, 7, 1, 2,  5, 3, 6 };
    int n = sizeof(a)/sizeof(a[0]);
    printModeMedian(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java Program for Mode and 
// Median using Counting 
// Sort technique 
class GFG 
{
// function that sort input array a[] and 
// calculate mode and median using counting 
// sort. 

    static void printModeMedian(int a[], int n) 
    {
        // The output array b[] will 
        // have sorted array 
        int[] b = new int[n];

        // variable to store max of 
        // input array which will 
        // to have size of count array 
        int max = Arrays.stream(a).max().getAsInt();

        // auxiliary(count) array to 
        // store count. Initialize 
        // count array as 0\. Size 
        // of count array will be 
        // equal to (max + 1). 
        int t = max + 1;
        int count[] = new int[t];
        for (int i = 0; i < t; i++)
        {
            count[i] = 0;
        }

        // Store count of each element 
        // of input array 
        for (int i = 0; i < n; i++)
        {
            count[a[i]]++;
        }

        // mode is the index with maximum count 
        int mode = 0;
        int k = count[0];
        for (int i = 1; i < t; i++) 
        {
            if (count[i] > k)
            {
                k = count[i];
                mode = i;
            }
        }

        // Update count[] array with sum 
        for (int i = 1; i < t; i++)
        {
            count[i] = count[i] + count[i - 1];
        }

        // Sorted output array b[] 
        // to calculate median 
        for (int i = 0; i < n; i++) 
        {
            b[count[a[i]] - 1] = a[i];
            count[a[i]]--;
        }

        // Median according to odd and even 
        // array size respectively. 
        float median;
        if (n % 2 != 0) 
        {
            median = b[n / 2];
        }
        else
        {
            median = (float) ((b[(n - 1) / 2]
                    + b[(n / 2)]) / 2.0);
        }

        // Output the result 
        System.out.println("median = " + median);
        System.out.println("mode = " + mode);
    }

// Driver program 
public static void main(String[] args)
{
    int a[] = {1, 4, 1, 2, 7, 1, 2, 5, 3, 6};
    int n = a.length;
    printModeMedian(a, n);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for Mode and Median 
# using Counting Sort technique 

# Function that sort input array a[] and 
# calculate mode and median using counting sort 
def printModeMedian(a, n):

    # The output array b[] will 
    # have sorted array
    b = [0] * n 

    # Variable to store max of input array
    # which will to have size of count array 
    Max = max(a)

    # Auxiliary(count) array to store count.
    # Initialize count array as 0\. Size of
    # count array will be equal to (max + 1).
    t = Max + 1
    count = [0] * t

    # Store count of each element 
    # of input array 
    for i in range(n):
        count[a[i]] += 1

    # Mode is the index with maximum count 
    mode = 0
    k = count[0]

    for i in range(1, t):
        if (count[i] > k):
            k = count[i]
            mode = i 

    # Update count[] array with sum
    for i in range(1, t):
        count[i] = count[i] + count[i - 1]

    # Sorted output array b[] 
    # to calculate median 
    for i in range(n):
        b[count[a[i]] - 1] = a[i]
        count[a[i]] -= 1

    # Median according to odd and even 
    # array size respectively.
    median = 0.0
    if (n % 2 != 0):
        median = b[n // 2]
    else:
        median = ((b[(n - 1) // 2] + 
                   b[n // 2]) / 2.0)

    # Output the result
    print("median =", median)
    print("mode =", mode)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 4, 1, 2, 7, 1, 2, 5, 3, 6]
    n = len(arr)

    printModeMedian(arr, n)

# This code is contributed by himanshu77
```

## C#

```
// C# Program for Mode and 
// Median using Counting 
// Sort technique 
using System;
using System.Linq;

class GFG 
{
    // function that sort input array a[] and 
    // calculate mode and median using counting 
    // sort. 
    static void printModeMedian(int []a, int n) 
    {
        // The output array b[] will 
        // have sorted array 
        int[] b = new int[n];

        // variable to store max of 
        // input array which will 
        // to have size of count array 
        int max = a.Max();

        // auxiliary(count) array to 
        // store count. Initialize 
        // count array as 0\. Size 
        // of count array will be 
        // equal to (max + 1). 
        int t = max + 1;
        int []count = new int[t];
        for (int i = 0; i < t; i++)
        {
            count[i] = 0;
        }

        // Store count of each element 
        // of input array 
        for (int i = 0; i < n; i++)
        {
            count[a[i]]++;
        }

        // mode is the index with maximum count 
        int mode = 0;
        int k = count[0];
        for (int i = 1; i < t; i++) 
        {
            if (count[i] > k)
            {
                k = count[i];
                mode = i;
            }
        }

        // Update count[] array with sum 
        for (int i = 1; i < t; i++)
        {
            count[i] = count[i] + count[i - 1];
        }

        // Sorted output array b[] 
        // to calculate median 
        for (int i = 0; i < n; i++) 
        {
            b[count[a[i]] - 1] = a[i];
            count[a[i]]--;
        }

        // Median according to odd and even 
        // array size respectively. 
        float median;
        if (n % 2 != 0) 
        {
            median = b[n / 2];
        }
        else
        {
            median = (float) ((b[(n - 1) / 2] + 
                               b[(n / 2)]) / 2.0);
        }

        // Output the result 
        Console.WriteLine("median = " + median);
        Console.WriteLine("mode = " + mode);
    }

// Driver Code
public static void Main(String[] args)
{
    int []a = {1, 4, 1, 2, 7, 1, 2, 5, 3, 6};
    int n = a.Length;
    printModeMedian(a, n);
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program for Mode and Median using 
// Counting Sort technique

// Function that sort input array a[] and 
// calculate mode and median using counting
// sort.
function printModeMedian($a, $n)
{
    // The output array b[] will
    // have sorted array
    $b[$n] = array();

    // variable to store max of input 
    // array which will to have size 
    // of count array
    $max = max($a);

    // auxiliary(count) array to store 
    // count. Initialize count array as 
    // 0\. Size of count array will be
    // equal to (max + 1).
    $t = $max + 1;
    $count[$t] = array();
    for ($i = 0; $i < $t; $i++)
        $count[$i] = 0; 

    // Store count of each element
    // of input array
    for ($i = 0; $i < $n; $i++)
        $count[$a[$i]]++; 

    // mode is the index with maximum count
    $mode = 0;
    $k = $count[0];
    for ($i = 1; $i < $t; $i++)
    {
        if ($count[$i] > $k)
        {
            $k = $count[$i];
            $mode = $i;
        }
    } 

    // Update count[] array with sum
    for ($i = 1; $i < $t; $i++)
        $count[$i] = $count[$i] + $count[$i - 1];

    // Sorted output array b[]
    // to calculate median
    for ($i = 0; $i < $n; $i++)
    {
        $b[$count[$a[$i]] - 1] = $a[$i];
        $count[$a[$i]]--;
    }

    // Median according to odd and even 
    // array size respectively.
    $median;
    if ($n % 2 != 0)
        $median = $b[$n / 2];
    else
        $median = ($b[($n - 1) / 2] + 
                   $b[($n / 2)]) / 2.0;

    // Output the result 
    echo "median = ", $median, "\n" ;
    echo "mode = " , $mode;
}

// Driver Code
$a = array( 1, 4, 1, 2, 7, 
            1, 2, 5, 3, 6 );
$n = sizeof($a);
printModeMedian($a, $n);

// This code is contributed by jit_t
?>
```

**Output:**

```
median = 2.5
mode = 1

```

**时间复杂度** = O(N + P)，其中 N 为输入数组的时间，P 为计数数组的时间。
**空间复杂度** = O(P)，其中 P 为辅助阵的大小。
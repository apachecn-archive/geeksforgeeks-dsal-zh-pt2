# 下插入点

> 原文:[https://www.geeksforgeeks.org/lower-insertion-point/](https://www.geeksforgeeks.org/lower-insertion-point/)

给定一个由 **n** 排序的整数元素组成的数组 **arr[]** 和一个整数 **X** ，任务是找到数组中 **X** 的下插入点。下插入点是第一个元素的索引 **≥ X** 。如果 **X** 大于 **arr** 的所有元素，则打印 **n** ，如果 **X** 小于**arr【】**的所有元素，则返回 **0** 。
**举例:**

> **输入:** arr[] = {2，3，4，4，5，6，7，9}，X = 4
> **输出:** 2
> **输入:** arr[] = {0，5，8，15}，X = 16
> **输出:** 4

**进场:**

*   如果 **X < arr[0]** 打印 **0** 或**X>arr[n–1]**打印 **n** 。
*   初始化 **lowertPnt = 0** 并开始从 **1** 到**n–1**遍历数组。
    *   如果**arr【I】<X**则更新**lowerpoint = I**和 **i = i * 2** 。
    *   **i** 的第一个值，其中**X≥arr【I】**或当 **i ≥ n** 时，断开回路。
    *   现在检查从**下限**到**n–1**的其余元素，同时 **arr【下限】< X** 更新**下限=下限+ 1。**
    *   最终打印**下限**..

以下是上述方法的实现:

## C++

```
// C++ program to find the lower insertion point
// of an element in a sorted array
#include <iostream>
using namespace std;

// Function to return the lower insertion point
// of an element in a sorted array
int LowerInsertionPoint(int arr[], int n, int X)
{

    // Base cases
    if (X < arr[0])
        return 0;
    else if (X > arr[n - 1])
        return n;

    int lowerPnt = 0;
    int i = 1;

    while (i < n && arr[i] < X) {
        lowerPnt = i;
        i = i * 2;
    }

    // Final check for the remaining elements which are < X
    while (lowerPnt < n && arr[lowerPnt] < X)
        lowerPnt++;

    return lowerPnt;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 4, 5, 6, 7, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int X = 4;
    cout << LowerInsertionPoint(arr, n, X);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find the lower insertion point
//of an element in a sorted array
public class AQES {

    //Function to return the lower insertion point
    //of an element in a sorted array
    static int LowerInsertionPoint(int arr[], int n, int X)
    {

     // Base cases
     if (X < arr[0])
         return 0;
     else if (X > arr[n - 1])
         return n;

     int lowerPnt = 0;
     int i = 1;

     while (i < n && arr[i] < X) {
         lowerPnt = i;
         i = i * 2;
     }

     // Final check for the remaining elements which are < X
     while (lowerPnt < n && arr[lowerPnt] < X)
         lowerPnt++;

     return lowerPnt;
    }

    //Driver code
    public static void main(String[] args) {

         int arr[] = { 2, 3, 4, 4, 5, 6, 7, 9 };
         int n = arr.length;
         int X = 4;
         System.out.println(LowerInsertionPoint(arr, n, X));

    }
}
```

## 蟒蛇 3

```
# Python3 program to find the lower insertion
# point of an element in a sorted array

# Function to return the lower insertion
# point of an element in a sorted array
def LowerInsertionPoint(arr, n, X) :

    # Base cases
    if (X < arr[0]) :
        return 0;
    elif (X > arr[n - 1]) :
        return n

    lowerPnt = 0
    i = 1

    while (i < n and arr[i] < X) :
        lowerPnt = i
        i = i * 2

    # Final check for the remaining elements
    # which are < X
    while (lowerPnt < n and arr[lowerPnt] < X) :
        lowerPnt += 1

    return lowerPnt

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 3, 4, 4, 5, 6, 7, 9 ]
    n = len(arr)
    X = 4
    print(LowerInsertionPoint(arr, n, X))

# This code is contributed by Ryuga
```

## C#

```
// C#  program to find the lower insertion point
//of an element in a sorted array
using System;

public class GFG{
    //Function to return the lower insertion point
    //of an element in a sorted array
    static int LowerInsertionPoint(int []arr, int n, int X)
    {

    // Base cases
    if (X < arr[0])
        return 0;
    else if (X > arr[n - 1])
        return n;

    int lowerPnt = 0;
    int i = 1;

    while (i < n && arr[i] < X) {
        lowerPnt = i;
        i = i * 2;
    }

    // Final check for the remaining elements which are < X
    while (lowerPnt < n && arr[lowerPnt] < X)
        lowerPnt++;

    return lowerPnt;
    }

    //Driver code
    static public void Main (){
        int []arr = { 2, 3, 4, 4, 5, 6, 7, 9 };
        int n = arr.Length;
        int X = 4;
        Console.WriteLine(LowerInsertionPoint(arr, n, X));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the lower insertion
// point of an element in a sorted array

// Function to return the lower insertion
// point of an element in a sorted array
function LowerInsertionPoint($arr, $n, $X)
{

    // Base cases
    if ($X < $arr[0])
        return 0;
    else if ($X > $arr[$n - 1])
        return $n;

    $lowerPnt = 0;
    $i = 1;

    while ($i < $n && $arr[$i] < $X)
    {
        $lowerPnt = $i;
        $i = $i * 2;
    }

    // Final check for the remaining
    // elements which are < X
    while ($lowerPnt < $n && $arr[$lowerPnt] < $X)
        $lowerPnt++;

    return $lowerPnt;
}

// Driver code
$arr = array( 2, 3, 4, 4, 5, 6, 7, 9 );
$n = sizeof($arr);
$X = 4;
echo LowerInsertionPoint($arr, $n, $X);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the lower insertion point
    // of an element in a sorted array

    // Function to return the lower insertion point
    // of an element in a sorted array
    function LowerInsertionPoint(arr, n, X)
    {

        // Base cases
        if (X < arr[0])
            return 0;
        else if (X > arr[n - 1])
            return n;

        let lowerPnt = 0;
        let i = 1;

        while (i < n && arr[i] < X) {
            lowerPnt = i;
            i = i * 2;
        }

        // Final check for the remaining elements which are < X
        while (lowerPnt < n && arr[lowerPnt] < X)
            lowerPnt++;

        return lowerPnt;
    } 

    let arr = [ 2, 3, 4, 4, 5, 6, 7, 9 ];
    let n = arr.length;
    let X = 4;
    document.write(LowerInsertionPoint(arr, n, X));

</script>
```

**Output:** 

```
2
```

**进一步优化:**上述解的时间复杂度在最坏的情况下会变成 O(n)。我们可以使用二分搜索法优化解决方案，使其在 O(Log n)时间内工作。详情请参考[无界二分搜索法](https://www.geeksforgeeks.org/find-position-element-sorted-array-infinite-numbers/)。
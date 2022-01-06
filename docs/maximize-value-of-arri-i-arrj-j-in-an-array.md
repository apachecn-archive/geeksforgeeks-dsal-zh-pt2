# 最大化数组中(arr[I]–I)–(arr[j]–j)的值

> 原文:[https://www . geeksforgeeks . org/arri-I-arrj-j 阵列中的最大价值/](https://www.geeksforgeeks.org/maximize-value-of-arri-i-arrj-j-in-an-array/)

给定一个数组，arr[]求(arr[I]–I)–(arr[j]–j)的最大值，其中 I 不等于 j，I 和 j 从 0 到 n-1 不等，n 是输入数组 arr[]的大小。
**例:**

```
Input : arr[] = {9, 15, 4, 12, 13}
Output : 12
We get the maximum value for i = 1 and j = 2
(15 - 1) - (4 - 2) = 12

Input : arr[] = {-1, -2, -3, 4, 10}
Output : 6
We get the maximum value for i = 4 and j = 2
(10 - 4) - (-3 - 2) = 11
```

一个重要的观察是,( arr[I]–I)–(arr[j]–j)的值永远不能为负。我们总是可以交换 I 和 j，将负值转换为正值。所以条件 I 不等于 j 是假的，不需要明确的检查。
**方法 1(Naive:O(n)<sup>2</sup>)**
思路是运行两个循环来考虑所有可能的对，并跟踪表达式的最大值(arr[i]-i)-(arr[j]-j)。下面是这个想法的实现。

## C++

```
// C++ program to find maximum value (arr[i]-i)
// - (arr[j]-j) in an array.
#include<bits/stdc++.h>
using namespace std;

// Returns maximum value of (arr[i]-i) - (arr[j]-j)
int findMaxDiff(int arr[], int n)
{
    if (n < 2)
    {
        cout << "Invalid ";
        return 0;
    }

    // Use two nested loops to find the result
    int res = INT_MIN;
    for (int i=0; i<n; i++)
       for (int j=0; j<n; j++)
          if ( res < (arr[i]-arr[j]-i+j) )
            res = (arr[i]-arr[j]-i+j);

    return res;
}

// Driver program
int main()
{
   int arr[] = {9, 15, 4, 12, 13};
   int n = sizeof(arr)/sizeof(arr[0]);
   cout << findMaxDiff(arr, n);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum value (arr[i]-i)
// - (arr[j]-j) in an array.
import java.util.*;

class GFG {

// Returns maximum value of
// (arr[i]-i) - (arr[j]-j)
static int findMaxDiff(int arr[], int n)
{
    if (n < 2) {
    System.out.print("Invalid ");
    return 0;
    }

    // Use two nested loops to find the result
    int res = Integer.MIN_VALUE;
    for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
        if (res < (arr[i] - arr[j] - i + j))
        res = (arr[i] - arr[j] - i + j);

    return res;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {9, 15, 4, 12, 13};
    int n = arr.length;
    System.out.print(findMaxDiff(arr, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# maximum value (arr[i]-i)
# - (arr[j]-j) in an array.

# Returns maximum value of
# (arr[i]-i) - (arr[j]-j)
def findMaxDiff(arr,n):

    if (n < 2):

        print("Invalid ")
        return 0

    # Use two nested loops
    # to find the result
    res = -2147483648
    for i in range(n):
        for j in range(n):
            if ( res < (arr[i]-arr[j]-i+j) ):
                res = (arr[i]-arr[j]-i+j)

    return res

# Driver code

arr= [9, 15, 4, 12, 13]
n = len(arr)

print(findMaxDiff(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find maximum
// value (arr[i]-i)- (arr[j]-j)
// in an array.
using System;
class GFG {

// Returns maximum value of
// (arr[i]-i) - (arr[j]-j)
static int findMaxDiff(int []arr, int n)
{
    if (n < 2) {
    Console.WriteLine("Invalid ");
    return 0;
    }

    // Use two nested loops to
    // find the result
    int res = int.MinValue;
    for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
        if (res < (arr[i] - arr[j] - i + j))
            res = (arr[i] - arr[j] - i + j);

    return res;
}

// Driver code
public static void Main()
{
    int []arr = {9, 15, 4, 12, 13};
    int n = arr.Length;
    Console.WriteLine(findMaxDiff(arr, n));
}
}

// This code is contributed by anjuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum value
// (arr[i]-i) - (arr[j]-j) in an array.

// Returns maximum value of
// (arr[i]-i) - (arr[j]-j)
function findMaxDiff( $arr, $n)
{
    if ($n < 2)
    {
        echo "Invalid ";
        return 0;
    }

    // Use two nested loops to
    // find the result
    $res = PHP_INT_MIN;
    for($i = 0; $i < $n; $i++)
    for($j = 0; $j < $n; $j++)
        if($res < ($arr[$i] - $arr[$j] - $i + $j))
            $res = ($arr[$i] - $arr[$j] - $i + $j);

    return $res;
}

// Driver Code
$arr = array(9, 15, 4, 12, 13);
$n = count($arr);
echo findMaxDiff($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find maximum
    // value (arr[i]-i)- (arr[j]-j)
    // in an array.

    // Returns maximum value of
    // (arr[i]-i) - (arr[j]-j)
    function findMaxDiff(arr, n)
    {
        if (n < 2) {
            document.write("Invalid ");
            return 0;
        }

        // Use two nested loops to
        // find the result
        let res = Number.MIN_VALUE;
        for (let i = 0; i < n; i++)
            for (let j = 0; j < n; j++)
                if (res < (arr[i] - arr[j] - i + j))
                    res = (arr[i] - arr[j] - i + j);

        return res;
    }

    let arr = [9, 15, 4, 12, 13];
    let n = arr.length;
    document.write(findMaxDiff(arr, n));

</script>
```

**输出:**

```
12
```

**方法 2(棘手:O(n))**
1)求 arr[I]–I 在整个数组中的最大值。
2)求整数组中 arr[I]–I 的最小值。
3)返回上述两个值的差值。

## C++

```
// C++ program to find maximum value (arr[i]-i)
// - (arr[j]-j) in an array.
#include<bits/stdc++.h>
using namespace std;

// Returns maximum value of (arr[i]-i) - (arr[j]-j)
int findMaxDiff(int a[], int n)
{
    if (n < 2)
    {
        cout << "Invalid ";
        return 0;
    }

    // Find maximum of value of arr[i] - i for all
    // possible values of i. Let this value be max_val.
    // Find minimum of value of arr[i] - i for all
    // possible values of i. Let this value be min_val.
    // The difference max_val - min_v
    int min_val = INT_MAX, max_val =
                           INT_MIN;
    for (int i=0; i<n; i++)
    {
        if ((a[i]-i) > max_val)
            max_val = a[i] - i;
        if ((a[i]-i) < min_val)
            min_val = a[i]-i;
    }

    return (max_val - min_val);
}

// Driver program
int main()
{
    int arr[] = {9, 15, 4, 12, 13};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << findMaxDiff(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum value (arr[i]-i)
// - (arr[j]-j) in an array.
import java.io.*;

class GFG {

    // Returns maximum value of (arr[i]-i) -
    // (arr[j]-j)
    static int findMaxDiff(int arr[], int n)   
    {
        if (n < 2)
        {
            System.out.println("Invalid ");
            return 0;
        }

        // Find maximum of value of arr[i] - i
        // for all possible values of i. Let
        // this value be max_val. Find minimum
        // of value of arr[i] - i for all
        // possible values of i. Let this value
        // be min_val. The difference max_val -
        // min_v
        int min_val = Integer.MAX_VALUE,
            max_val = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++)
        {
            if ((arr[i]-i) > max_val)
                max_val = arr[i] - i;

            if ((arr[i]-i) < min_val)
                min_val = arr[i]-i;
        }

        return (max_val - min_val);
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = {9, 15, 4, 12, 13};
        int n = arr.length;
        System.out.println(findMaxDiff(arr, n));
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program to find maximum value
# (arr[i]-i) - (arr[j]-j) in an array.
import sys

# Returns maximum value of
# (arr[i]-i) - (arr[j]-j)
def findMaxDiff(a, n):
    if (n < 2):
        print("Invalid ")
        return 0

    # Find maximum of value of arr[i] - i
    # for all possible values of i. Let
    # this value be max_val. Find minimum
    # of value of arr[i] - i for all possible
    # values of i. Let this value be min_val.
    # The difference max_val - min_v
    min_val = sys.maxsize
    max_val = -sys.maxsize - 1
    for i in range(n):
        if ((a[i] - i) > max_val):
            max_val = a[i] - i
        if ((a[i] - i) < min_val):
            min_val = a[i] - i

    return (max_val - min_val)

# Driver Code
if __name__ == '__main__':
    arr = [9, 15, 4, 12, 13]
    n = len(arr)
    print(findMaxDiff(arr, n))

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find maximum value (arr[i]-i)
// - (arr[j]-j) in an array.
using System;

class GFG {

    // Returns maximum value of (arr[i]-i) -
    // (arr[j]-j)
    static int findMaxDiff(int []arr, int n)   
    {
        if (n < 2)
        {
            Console.Write("Invalid ");
            return 0;
        }

        // Find maximum of value of arr[i] - i
        // for all possible values of i. Let
        // this value be max_val. Find minimum
        // of value of arr[i] - i for all
        // possible values of i. Let this value
        // be min_val. The difference max_val -
        // min_v
        int min_val = int.MaxValue,
            max_val = int.MinValue;

        for (int i = 0; i < n; i++)
        {
            if ((arr[i] - i) > max_val)
                max_val = arr[i] - i;

            if ((arr[i] - i) < min_val)
                min_val = arr[i] - i;
        }

        return (max_val - min_val);
    }

    // Driver program
    public static void Main()
    {
        int []arr = {9, 15, 4, 12, 13};
        int n = arr.Length;
        Console.Write(findMaxDiff(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum value
// (arr[i]-i) - (arr[j]-j) in an array.

// Returns maximum value of
// (arr[i]-i) - (arr[j]-j)
function findMaxDiff($a, $n)
{
    if ($n < 2)
    {
        echo "Invalid ";
        return 0;
    }

    // Find maximum of value of arr[i] - i
    // for all possible values of i. Let
    // this value be max_val. Find minimum
    // of value of arr[i] - i for all
    // possible values of i. Let this value
    // be min_val. The difference max_val - min_v
    $min_val = PHP_INT_MAX;
    $max_val = PHP_INT_MIN;
    for ($i = 0; $i < $n; $i++)
    {
        if (($a[$i] - $i) > $max_val)
            $max_val = $a[$i] - $i;
        if (($a[$i] - $i) < $min_val)
            $min_val = $a[$i] - $i;
    }

    return ($max_val - $min_val);
}

// Driver Code
$arr = array(9, 15, 4, 12, 13);
$n = sizeof($arr);
echo findMaxDiff($arr, $n);

// This code is contributed by Sachin.
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // maximum value (arr[i]-i)
    // - (arr[j]-j) in an array.

    // Returns maximum value of (arr[i]-i) -
    // (arr[j]-j)
    function findMaxDiff(arr, n)  
    {
        if (n < 2)
        {
            document.write("Invalid ");
            return 0;
        }

        // Find maximum of value of arr[i] - i
        // for all possible values of i. Let
        // this value be max_val. Find minimum
        // of value of arr[i] - i for all
        // possible values of i. Let this value
        // be min_val. The difference max_val -
        // min_v
        let min_val =
        Number.MAX_VALUE, max_val = Number.MIN_VALUE;

        for (let i = 0; i < n; i++)
        {
            if ((arr[i] - i) > max_val)
                max_val = arr[i] - i;

            if ((arr[i] - i) < min_val)
                min_val = arr[i] - i;
        }

        return (max_val - min_val);
    }

    let arr = [9, 15, 4, 12, 13];
    let n = arr.length;
    document.write(findMaxDiff(arr, n));

</script>
```

**输出:**

```
12
```

本文由 **Shivam Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
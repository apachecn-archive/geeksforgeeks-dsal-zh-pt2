# 最大值| arr[I]–arr[j]|+| I–j |

> 哎哎哎:# t0]https://www . geeksforgeeks . org/maximum-value-arri-arr j/

给定一组 **N** 正整数。任务是找到| arr[i]–arr[j]|+| I–j |，其中 0 < = i，j<= N–1 和 arr[I]，arr[j]属于数组。

**示例:**

> **输入:** N = 4，arr[] = { 1，2，3，1 }
> **输出:** 4
> **说明:**
> 选择 i = 0，j = 2。这将导致|1-3|+|0-2| = 4，这是最大可能值。
> 
> **输入:** N = 3，arr[] = { 1，1，1 }
> T3】输出: 2

**方法 1:** 想法是使用蛮力，即循环迭代两次。

下面是该方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define MAX 10

// Return maximum value of |arr[i] - arr[j]| + |i - j|
int findValue(int arr[], int n)
{
    int ans = 0;

    // Iterating two for loop, one for
    // i and another for j.
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)

            // Evaluating |arr[i] - arr[j]| + |i - j|
            // and compare with previous maximum.
            ans = max(ans,
                      abs(arr[i] - arr[j]) + abs(i - j));

    return ans;
}

// Driven Program
int main()
{
    int arr[] = { 1, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findValue(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find maximum value of
// |arr[i] - arr[j]| + |i - j|
class GFG {
    static final int MAX = 10;

    // Return maximum value of
    // |arr[i] - arr[j]| + |i - j|
    static int findValue(int arr[], int n)
    {
        int ans = 0;

        // Iterating two for loop,
        // one for i and another for j.
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)

                // Evaluating |arr[i] - arr[j]|
                // + |i - j| and compare with
                // previous maximum.
                ans = Math.max(ans,
                               Math.abs(arr[i] - arr[j])
                               + Math.abs(i - j));

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 1 };
        int n = arr.length;

        System.out.println(findValue(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# maximum value of
# |arr[i] - arr[j]| + |i - j|

# Return maximum value of
# |arr[i] - arr[j]| + |i - j|
def findValue(arr, n):
    ans = 0;

    # Iterating two for loop,
    # one for i and another for j.
    for i in range(n):
        for j in range(n):

            # Evaluating |arr[i] -
            # arr[j]| + |i - j|
            # and compare with
            # previous maximum.
            ans = ans if ans>(abs(arr[i] - arr[j]) +
                              abs(i - j)) else (abs(arr[i] -
                                      arr[j]) + abs(i - j)) ;
    return ans;

# Driver Code
arr = [1, 2, 3, 1];
n = len(arr);
print(findValue(arr, n));

# This code is contributed by mits.
```

## C#

```
// C# program to find maximum value of
// |arr[i] - arr[j]| + |i - j|
using System;

class GFG {

    // Return maximum value of
    // |arr[i] - arr[j]| + |i - j|
    static int findValue(int []arr, int n)
    {
        int ans = 0;

        // Iterating two for loop,
        // one for i and another for j.
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)

                // Evaluating |arr[i] - arr[j]|
                // + |i - j| and compare with
                // previous maximum.
                ans = Math.Max(ans,
                    Math.Abs(arr[i] - arr[j])
                            + Math.Abs(i - j));

        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 2, 3, 1 };
        int n =arr.Length;

        Console.Write(findValue(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum value of
// |arr[i] - arr[j]| + |i - j|
$MAX = 10;

// Return maximum value of
// |arr[i] - arr[j]| + |i - j|
function findValue($arr, $n)
{
    $ans = 0;

    // Iterating two for loop,
    // one for i and another for j.
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n; $j++)

            // Evaluating |arr[i] -
            // arr[j]| + |i - j|
            // and compare with
            // previous maximum.
            $ans = max($ans, abs($arr[$i] -
                   $arr[$j]) + abs($i - $j));

    return $ans;
}

    // Driver Code
    $arr = array(1, 2, 3, 1);
    $n = count($arr);

    echo findValue($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum value of
// |arr[i] - arr[j]| + |i - j|
var MAX = 10;

// Return maximum value of
// |arr[i] - arr[j]| + |i - j|
function findValue(arr , n)
{
    var ans = 0;

    // Iterating two for loop,
    // one for i and another for j.
    for(var i = 0; i < n; i++)
        for(var j = 0; j < n; j++)

            // Evaluating |arr[i] - arr[j]|
            // + |i - j| and compare with
            // previous maximum.
            ans = Math.max(ans,
                           Math.abs(arr[i] - arr[j]) +
                           Math.abs(i - j));

    return ans;
}

// Driver code
var arr = [ 1, 2, 3, 1 ];
var n = arr.length;

document.write(findValue(arr, n));

// This code is contributed by shikhasingrajput

</script>
```

**Output**

```
4
```

**方法 2(棘手):**

首先，让我们通过去掉绝对值符号(“|”)来建立四个方程。将形成以下 4 个方程，我们需要找到这些方程的最大值，这就是我们的答案。

1.  arr[I]–arr[j]+I–j =(arr[I]+I)–(arr[j]+j)
2.  arr[I]–arr[j]–I+j =(arr[I]–I)–(arr[j]–j)
3.  -arr[I]+arr[j]+I–j =-(arr[I]–I)+(arr[j]–j)
4.  -arr[I]+arr[j]–I+j =-(arr[I]+I)+(arr[j]+j)

观察等式(1)和(4)是否相同。类似地，等式(2)和(3)是相同的。
现在的任务是找到这些方程的最大值。所以方法是形成两个数组，first_array[]，它将存储 arr[i] + i，0 < = i < n，second_array[]，它将存储 arr[I]–I，0 < = i < n.
现在我们的任务很简单，我们只需要找到这两个数组的两个值之间的最大差。
为此，我们在 first_array 中找到最大值和最小值并存储它们的差值:
ans1 =(first _ array 中的最大值–first _ array 中的最小值)
同样，我们需要在 second_array 中找到最大值和最小值并存储它们的差值:
ans2 =(second _ array 中的最大值–second _ array 中的最小值)
我们的答案将是 ans1 和 ans2 的最大值。

下面是上述方法的实现:

## C++

```
// Efficient CPP program to find maximum value
// of |arr[i] - arr[j]| + |i - j|
#include <bits/stdc++.h>
using namespace std;

// Return maximum |arr[i] - arr[j]| + |i - j|
int findValue(int arr[], int n)
{
    int a[n], b[n], tmp;

    // Calculating first_array and second_array
    for (int i = 0; i < n; i++)
    {
        a[i] = (arr[i] + i);
        b[i] = (arr[i] - i);
    }

    int x = a[0], y = a[0];

    // Finding maximum and minimum value in
    // first_array
    for (int i = 0; i < n; i++)
    {
        if (a[i] > x)
            x = a[i];

        if (a[i] < y)
            y = a[i];
    }

    // Storing the difference between maximum and
    // minimum value in first_array
    int ans1 = (x - y);

    x = b[0];
    y = b[0];

    // Finding maximum and minimum value in
    // second_array
    for (int i = 0; i < n; i++)
    {
        if (b[i] > x)
            x = b[i];

        if (b[i] < y)
            y = b[i];
    }

    // Storing the difference between maximum and
    // minimum value in second_array
    int ans2 = (x - y);

    return max(ans1, ans2);
}

// Driven Code
int main()
{
    int arr[] = { 1, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findValue(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find maximum
// value of |arr[i] - arr[j]| + |i - j|
import java.io.*;
class GFG {

    // Return maximum |arr[i] -
    // arr[j]| + |i - j|
    static int findValue(int arr[], int n)
    {
        int a[] = new int[n];
        int b[] = new int[n];
        int tmp;

        // Calculating first_array
        // and second_array
        for (int i = 0; i < n; i++)
        {
            a[i] = (arr[i] + i);
            b[i] = (arr[i] - i);
        }

        int x = a[0], y = a[0];

        // Finding maximum and
        // minimum value in
        // first_array
        for (int i = 0; i < n; i++)
        {
            if (a[i] > x)
                x = a[i];

            if (a[i] < y)
                y = a[i];
        }

        // Storing the difference
        // between maximum and
        // minimum value in first_array
        int ans1 = (x - y);

        x = b[0];
        y = b[0];

        // Finding maximum and
        // minimum value in
        // second_array
        for (int i = 0; i < n; i++)
        {
            if (b[i] > x)
                x = b[i];

            if (b[i] < y)
                y = b[i];
        }

        // Storing the difference
        // between maximum and
        // minimum value in second_array
        int ans2 = (x - y);

        return Math.max(ans1, ans2);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 1 };
        int n = arr.length;
        System.out.println(findValue(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Efficient Python3 program
# to find maximum value
# of |arr[i] - arr[j]| + |i - j|

# Return maximum |arr[i] -
# arr[j]| + |i - j|

def findValue(arr, n):
    a = []
    b = []

    # Calculating first_array
    # and second_array
    for i in range(n):
        a.append(arr[i] + i)
        b.append(arr[i] - i)

    x = a[0]
    y = a[0]

    # Finding maximum and
    # minimum value in
    # first_array
    for i in range(n):
        if (a[i] > x):
            x = a[i]

        if (a[i] < y):
            y = a[i]

    # Storing the difference
    # between maximum and
    # minimum value in first_array
    ans1 = (x - y)

    x = b[0]
    y = b[0]

    # Finding maximum and
    # minimum value in
    # second_array
    for i in range(n):
        if (b[i] > x):
            x = b[i]

        if (b[i] < y):
            y = b[i]

    # Storing the difference
    # between maximum and
    # minimum value in
    # second_array
    ans2 = (x - y)

    return max(ans1, ans2)

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 1]
    n = len(arr)

    print(findValue(arr, n))

# This code is contributed by mits
```

## C#

```
// Efficient Java program to find maximum
// value of |arr[i] - arr[j]| + |i - j|
using System;
class GFG {

    // Return maximum |arr[i] -
    // arr[j]| + |i - j|
    static int findValue(int[] arr, int n)
    {
        int[] a = new int[n];
        int[] b = new int[n];
        // int tmp;

        // Calculating first_array
        // and second_array
        for (int i = 0; i < n; i++)
        {
            a[i] = (arr[i] + i);
            b[i] = (arr[i] - i);
        }

        int x = a[0], y = a[0];

        // Finding maximum and
        // minimum value in
        // first_array
        for (int i = 0; i < n; i++)
        {
            if (a[i] > x)
                x = a[i];

            if (a[i] < y)
                y = a[i];
        }

        // Storing the difference
        // between maximum and
        // minimum value in first_array
        int ans1 = (x - y);

        x = b[0];
        y = b[0];

        // Finding maximum and
        // minimum value in
        // second_array
        for (int i = 0; i < n; i++)
        {
            if (b[i] > x)
                x = b[i];

            if (b[i] < y)
                y = b[i];
        }

        // Storing the difference
        // between maximum and
        // minimum value in second_array
        int ans2 = (x - y);

        return Math.Max(ans1, ans2);
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 1 };
        int n = arr.Length;
        Console.WriteLine(findValue(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient CPP program
// to find maximum value
// of |arr[i] - arr[j]| + |i - j|

// Return maximum |arr[i] -
// arr[j]| + |i - j|
function findValue($arr, $n)
{
    $a[] =array(); $b=array();$tmp;

    // Calculating first_array
    // and second_array
    for ($i = 0; $i < $n; $i++)
    {
        $a[$i] = ($arr[$i] + $i);
        $b[$i] = ($arr[$i] - $i);
    }

    $x = $a[0]; $y = $a[0];

    // Finding maximum and
    // minimum value in
    // first_array
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] > $x)
        $x = $a[$i];

        if ($a[$i] < $y)
            $y = $a[$i];
    }

    // Storing the difference
    // between maximum and
    // minimum value in first_array
    $ans1 = ($x - $y);

    $x = $b[0];
    $y = $b[0];

    // Finding maximum and
    // minimum value in
    // second_array
    for ($i = 0; $i < $n; $i++)
    {
        if ($b[$i] > $x)
            $x = $b[$i];

        if ($b[$i] < $y)
            $y = $b[$i];
    }

    // Storing the difference
    // between maximum and
    // minimum value in
    // second_array
    $ans2 = ($x -$y);

    return max($ans1, $ans2);
}

    // Driver Code
    $arr = array(1, 2, 3, 1);
    $n = count($arr);

    echo findValue($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Efficient Javascript program to find maximum
    // value of |arr[i] - arr[j]| + |i - j|

    // Return maximum |arr[i] -
    // arr[j]| + |i - j|
    function findValue(arr, n)
    {
        let a = new Array(n);
        let b = new Array(n);
        // int tmp;

        // Calculating first_array
        // and second_array
        for (let i = 0; i < n; i++)
        {
            a[i] = (arr[i] + i);
            b[i] = (arr[i] - i);
        }

        let x = a[0], y = a[0];

        // Finding maximum and
        // minimum value in
        // first_array
        for (let i = 0; i < n; i++)
        {
            if (a[i] > x)
                x = a[i];

            if (a[i] < y)
                y = a[i];
        }

        // Storing the difference
        // between maximum and
        // minimum value in first_array
        let ans1 = (x - y);

        x = b[0];
        y = b[0];

        // Finding maximum and
        // minimum value in
        // second_array
        for (let i = 0; i < n; i++)
        {
            if (b[i] > x)
                x = b[i];

            if (b[i] < y)
                y = b[i];
        }

        // Storing the difference
        // between maximum and
        // minimum value in second_array
        let ans2 = (x - y);

        return Math.max(ans1, ans2);
    }

    let arr = [ 1, 2, 3, 1 ];
    let n = arr.length;
    document.write(findValue(arr, n));

</script>
```

**Output**

```
4
```

**方法–3**

```
This solution is space optimization on above mentioned (method2) solution.
In Method 2 solution we had used two matrix of size n which laid to O(n) space complexity 
but here we only use O(1) space instead of that two n size array
```

## C++

```
// Optimized CPP program to find maximum value of
// |arr[i] - arr[j]| + |i - j|
#include <bits/stdc++.h>
using namespace std;

// Return maximum |arr[i] - arr[j]| + |i - j|
int findValue(int arr[], int n)
{
    int temp1, temp2;
    int max1 = INT_MIN, max2 = INT_MIN;
    int min1 = INT_MAX, min2 = INT_MAX;

    // Calculating max1 , min1 and max2, min2
    for (int i = 0; i < n; i++) {
        temp1 = arr[i] + i;
        temp2 = arr[i] - i;
        max1 = max(max1, temp1);
        min1 = min(min1, temp1);
        max2 = max(max2, temp2);
        min2 = min(min2, temp2);
    }

    // required maximum ans is max of (max1-min1) and
    // (max2-min2)
    return max((max1 - min1), (max2 - min2));
}

// Driven Code
int main()
{
    int arr[] = { 1, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findValue(arr, n) << endl;

    return 0;
}

// code by AJAY MAKVANA
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Optimized JAVA program to find maximum value of
// |arr[i] - arr[j]| + |i - j|
import java.util.*;
class GFG
{

// Return maximum |arr[i] - arr[j]| + |i - j|
static int findValue(int arr[], int n)
{
    int temp1, temp2;
    int max1 = Integer.MIN_VALUE, max2 = Integer.MIN_VALUE;
    int min1 = Integer.MAX_VALUE, min2 = Integer.MAX_VALUE;

    // Calculating max1 , min1 and max2, min2
    for (int i = 0; i < n; i++) {
        temp1 = arr[i] + i;
        temp2 = arr[i] - i;
        max1 = Math.max(max1, temp1);
        min1 = Math.min(min1, temp1);
        max2 = Math.max(max2, temp2);
        min2 = Math.min(min2, temp2);
    }

    // required maximum ans is max of (max1-min1) and
    // (max2-min2)
    return Math.max((max1 - min1), (max2 - min2));
}

// Driven Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 1 };
    int n = arr.length;

    System.out.print(findValue(arr, n) +"\n");
}
}

// This code is contributed by gauravrajput1.
```

## 蟒蛇 3

```
# Optimized Python program to find maximum value of
# |arr[i] - arr[j]| + |i - j|
import sys

# Return maximum |arr[i] - arr[j]| + |i - j|
def findValue(arr, n):
    temp1=0;
    temp2=0;
    max1 = -sys.maxsize;
    max2 = -sys.maxsize;
    min1 = sys.maxsize;
    min2 = sys.maxsize;

    # Calculating max1 , min1 and max2, min2
    for i in range(n):
        temp1 = arr[i] + i;
        temp2 = arr[i] - i;
        max1 = max(max1, temp1);
        min1 = min(min1, temp1);
        max2 = max(max2, temp2);
        min2 = min(min2, temp2);

    # required maximum ans is max of (max1-min1) and
    # (max2-min2)
    return max((max1 - min1), (max2 - min2));

# Driven Code
if __name__ == '__main__':
    arr = [ 1, 2, 3, 1 ];
    n = len(arr);

    print(findValue(arr, n));

# This code is contributed by umadevi9616
```

## C#

```
// Optimized JAVA program to find maximum value of
// |arr[i] - arr[j]| + |i - j|
using System;

public class GFG {

    // Return maximum |arr[i] - arr[j]| + |i - j|
    static int findValue(int[] arr, int n)
    {
        int temp1, temp2;
        int max1 = int.MinValue, max2 = int.MinValue;
        int min1 = int.MaxValue, min2 = int.MaxValue;

        // Calculating max1 , min1 and max2, min2
        for (int i = 0; i < n; i++) {
            temp1 = arr[i] + i;
            temp2 = arr[i] - i;
            max1 = Math.Max(max1, temp1);
            min1 = Math.Min(min1, temp1);
            max2 = Math.Max(max2, temp2);
            min2 = Math.Min(min2, temp2);
        }

        // required maximum ans is max of (max1-min1) and
        // (max2-min2)
        return Math.Max((max1 - min1), (max2 - min2));
    }

    // Driven Code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 2, 3, 1 };
        int n = arr.Length;

        Console.Write(findValue(arr, n) + "\n");
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Optimized javascript program to find maximum value of
// |arr[i] - arr[j]| + |i - j|

    // Return maximum |arr[i] - arr[j]| + |i - j|
    function findValue(arr , n) {
        var temp1, temp2;
        var max1 = Number.MIN_VALUE, max2 = Number.MIN_VALUE;
        var min1 = Number.MAX_VALUE, min2 = Number.MAX_VALUE;

        // Calculating max1 , min1 and max2, min2
        for (i = 0; i < n; i++) {
            temp1 = arr[i] + i;
            temp2 = arr[i] - i;
            max1 = Math.max(max1, temp1);
            min1 = Math.min(min1, temp1);
            max2 = Math.max(max2, temp2);
            min2 = Math.min(min2, temp2);
        }

        // required maximum ans is max of (max1-min1) and
        // (max2-min2)
        return Math.max((max1 - min1), (max2 - min2));
    }

    // Driven Code
        var arr = [ 1, 2, 3, 1 ];
        var n = arr.length;

        document.write(findValue(arr, n) + "\n");

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
4
```

**时间复杂度:** O(N)

**辅助空间:**O(1)**T3】**

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
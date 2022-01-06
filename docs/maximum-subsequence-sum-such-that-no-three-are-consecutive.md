# 最大子序列和，使得没有三个是连续的

> 原文:[https://www . geeksforgeeks . org/maximum-subsequence-sum-so-no-3 是连续的/](https://www.geeksforgeeks.org/maximum-subsequence-sum-such-that-no-three-are-consecutive/)

给定一个正数序列，求不存在三个连续元素的最大和。
**例:**

```
Input: arr[] = {1, 2, 3}
Output: 5
We can't take three of them, so answer is
2 + 3 = 5

Input: arr[] = {3000, 2000, 1000, 3, 10}
Output: 5013 
3000 + 2000 + 3 + 10 = 5013

Input: arr[] = {100, 1000, 100, 1000, 1}
Output: 2101
100 + 1000 + 1000 + 1 = 2101

Input: arr[] = {1, 1, 1, 1, 1}
Output: 4

Input: arr[] = {1, 2, 3, 4, 5, 6, 7, 8}
Output: 27
```

这个问题主要是下面问题的延伸。
[最大和使得没有两个元素相邻](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/)
我们维护一个辅助数组和[](与输入数组大小相同)来寻找结果。

```
sum[i] : Stores result for subarray arr[0..i], i.e.,
         maximum possible sum in subarray arr[0..i]
         such that no three elements are consecutive.

sum[0] = arr[0]

// Note : All elements are positive
sum[1] = arr[0] + arr[1]

// We have three cases
// 1) Exclude arr[2], i.e., sum[2] = sum[1]
// 2) Exclude arr[1], i.e., sum[2] = sum[0] + arr[2]
// 3) Exclude arr[0], i.e., sum[2] = arr[1] + arr[2] 
sum[2] = max(sum[1], arr[0] + arr[2], arr[1] + arr[2])

In general,
// We have three cases
// 1) Exclude arr[i],  i.e.,  sum[i] = sum[i-1]
// 2) Exclude arr[i-1], i.e., sum[i] = sum[i-2] + arr[i]
// 3) Exclude arr[i-2], i.e., sum[i-3] + arr[i] + arr[i-1] 
sum[i] = max(sum[i-1], sum[i-2] + arr[i],
             sum[i-3] + arr[i] + arr[i-1])
```

下面是上述想法的实现。

## C++14

```
// C++ program to find the maximum sum such that
// no three are consecutive
#include <bits/stdc++.h>
using namespace std;

// Returns maximum subsequence sum such that no three
// elements are consecutive
int maxSumWO3Consec(int arr[], int n)
{
    // Stores result for subarray arr[0..i], i.e.,
    // maximum possible sum in subarray arr[0..i]
    // such that no three elements are consecutive.
    int sum[n];

    // Base cases (process first three elements)
    if (n >= 1)
        sum[0] = arr[0];

    if (n >= 2)
        sum[1] = arr[0] + arr[1];

    if (n > 2)
        sum[2] = max(sum[1], max(arr[1] +
                               arr[2], arr[0] + arr[2]));

    // Process rest of the elements
    // We have three cases
    // 1) Exclude arr[i], i.e., sum[i] = sum[i-1]
    // 2) Exclude arr[i-1], i.e., sum[i] = sum[i-2] + arr[i]
    // 3) Exclude arr[i-2], i.e., sum[i-3] + arr[i] + arr[i-1]
    for (int i = 3; i < n; i++)
        sum[i] = max(max(sum[i - 1], sum[i - 2] + arr[i]),
                     arr[i] + arr[i - 1] + sum[i - 3]);

    return sum[n - 1];
}

// Driver code
int main()
{
    int arr[] = { 100, 1000 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxSumWO3Consec(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find the maximum sum
// such that no three are consecutive
import java.io.*;

class GFG {

    // Returns maximum subsequence sum such that no three
    // elements are consecutive
    static int maxSumWO3Consec(int arr[], int n)
    {
        // Stores result for subarray arr[0..i], i.e.,
        // maximum possible sum in subarray arr[0..i]
        // such that no three elements are consecutive.
        int sum[] = new int[n];

        // Base cases (process first three elements)
        if (n >= 1)
            sum[0] = arr[0];

        if (n >= 2)
            sum[1] = arr[0] + arr[1];

        if (n > 2)
            sum[2] = Math.max(sum[1], Math.max(arr[1] + arr[2], arr[0] + arr[2]));

        // Process rest of the elements
        // We have three cases
        // 1) Exclude arr[i], i.e., sum[i] = sum[i-1]
        // 2) Exclude arr[i-1], i.e., sum[i] = sum[i-2] + arr[i]
        // 3) Exclude arr[i-2], i.e., sum[i-3] + arr[i] + arr[i-1]
        for (int i = 3; i < n; i++)
            sum[i] = Math.max(Math.max(sum[i - 1], sum[i - 2] + arr[i]),
                              arr[i] + arr[i - 1] + sum[i - 3]);

        return sum[n - 1];
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 100, 1000, 100, 1000, 1 };
        int n = arr.length;
        System.out.println(maxSumWO3Consec(arr, n));
    }
}

// This code is contributed by vt_m
```

## 计算机编程语言

```
# Python program to find the maximum sum such that
# no three are consecutive

# Returns maximum subsequence sum such that no three
# elements are consecutive
def maxSumWO3Consec(arr, n):
    # Stores result for subarray arr[0..i], i.e.,
    # maximum possible sum in subarray arr[0..i]
    # such that no three elements are consecutive.
    sum = [0 for k in range(n)]

    # Base cases (process first three elements)

    if n >= 1 :
        sum[0] = arr[0]

    if n >= 2 :
        sum[1] = arr[0] + arr[1]

    if n > 2 :
        sum[2] = max(sum[1], max(arr[1] + arr[2], arr[0] + arr[2]))

    # Process rest of the elements
    # We have three cases
    # 1) Exclude arr[i], i.e., sum[i] = sum[i-1]
    # 2) Exclude arr[i-1], i.e., sum[i] = sum[i-2] + arr[i]
    # 3) Exclude arr[i-2], i.e., sum[i-3] + arr[i] + arr[i-1]
    for i in range(3, n):
        sum[i] = max(max(sum[i-1], sum[i-2] + arr[i]), arr[i] + arr[i-1] + sum[i-3])

    return sum[n-1]

# Driver code
arr = [100, 1000, 100, 1000, 1]
n = len(arr)
print maxSumWO3Consec(arr, n)

# This code is contributed by Afzal Ansari
```

## C#

```
// C# program to find the maximum sum
// such that no three are consecutive
using System;
class GFG {

    // Returns maximum subsequence
    // sum such that no three
    // elements are consecutive
    static int maxSumWO3Consec(int[] arr,
                               int n)
    {
        // Stores result for subarray
        // arr[0..i], i.e., maximum
        // possible sum in subarray
        // arr[0..i] such that no
        // three elements are consecutive.
        int[] sum = new int[n];

        // Base cases (process
        // first three elements)
        if (n >= 1)
            sum[0] = arr[0];

        if (n >= 2)
            sum[1] = arr[0] + arr[1];

        if (n > 2)
            sum[2] = Math.Max(sum[1], Math.Max(arr[1] + arr[2], arr[0] + arr[2]));

        // Process rest of the elements
        // We have three cases
        // 1) Exclude arr[i], i.e.,
        // sum[i] = sum[i-1]
        // 2) Exclude arr[i-1], i.e.,
        // sum[i] = sum[i-2] + arr[i]
        // 3) Exclude arr[i-2], i.e.,
        // sum[i-3] + arr[i] + arr[i-1]
        for (int i = 3; i < n; i++)
            sum[i] = Math.Max(Math.Max(sum[i - 1],
                                       sum[i - 2] + arr[i]),
                              arr[i] + arr[i - 1] + sum[i - 3]);

        return sum[n - 1];
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 100, 1000, 100, 1000, 1 };
        int n = arr.Length;
        Console.Write(maxSumWO3Consec(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// sum such that no three are consecutive

// Returns maximum subsequence
// sum such that no three
// elements are consecutive
function maxSumWO3Consec($arr, $n)
{
    // Stores result for subarray
    // arr[0..i], i.e., maximum
    // possible sum in subarray
    // arr[0..i] such that no three
    // elements are consecutive$.
    $sum = array();

    // Base cases (process
    // first three elements)
    if ( $n >= 1)
    $sum[0] = $arr[0];

    if ($n >= 2)
    $sum[1] = $arr[0] + $arr[1];

    if ( $n > 2)
    $sum[2] = max($sum[1], max($arr[1] + $arr[2],
                            $arr[0] + $arr[2]));

    // Process rest of the elements
    // We have three cases
    // 1) Exclude arr[i], i.e.,
    // sum[i] = sum[i-1]
    // 2) Exclude arr[i-1], i.e.,
    // sum[i] = sum[i-2] + arr[i]
    // 3) Exclude arr[i-2], i.e.,
    // sum[i-3] + arr[i] + arr[i-1]
    for ($i = 3; $i < $n; $i++)
        $sum[$i] = max(max($sum[$i - 1],
                        $sum[$i - 2] + $arr[$i]),
                        $arr[$i] + $arr[$i - 1] +
                                    $sum[$i - 3]);

    return $sum[$n-1];
}

// Driver code
$arr = array(100, 1000, 100, 1000, 1);
$n =count($arr);
echo maxSumWO3Consec($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum sum
// such that no three are consecutive

    // Returns maximum subsequence sum such that no three
    // elements are consecutive
    function maxSumWO3Consec(arr, n)
    {
        // Stores result for subarray arr[0..i], i.e.,
        // maximum possible sum in subarray arr[0..i]
        // such that no three elements are consecutive.
        let sum = [];

        // Base cases (process first three elements)
        if (n >= 1)
            sum[0] = arr[0];

        if (n >= 2)
            sum[1] = arr[0] + arr[1];

        if (n > 2)
            sum[2] = Math.max(sum[1], Math.max(arr[1] + arr[2], arr[0] + arr[2]));

        // Process rest of the elements
        // We have three cases
        // 1) Exclude arr[i], i.e., sum[i] = sum[i-1]
        // 2) Exclude arr[i-1], i.e., sum[i] = sum[i-2] + arr[i]
        // 3) Exclude arr[i-2], i.e., sum[i-3] + arr[i] + arr[i-1]
        for (let i = 3; i < n; i++)
            sum[i] = Math.max(Math.max(sum[i - 1], sum[i - 2] + arr[i]),
                              arr[i] + arr[i - 1] + sum[i - 3]);

        return sum[n - 1];
    }

// Driver Code
        let arr = [ 100, 1000, 100, 1000, 1 ];
        let n = arr.length;
        document.write(maxSumWO3Consec(arr, n));

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
2101
```

**时间复杂度:**O(n)
T3】辅助空间:O(n)
T6】另一种方法:(使用递归)

## C++

```
// C++ program to find the maximum sum such that
// no three are consecutive using recursion.
#include<bits/stdc++.h>
using namespace std;

int arr[] = {100, 1000, 100, 1000, 1};
int sum[10000];

// Returns maximum subsequence sum such that no three
// elements are consecutive
int maxSumWO3Consec(int n)
{
    if(sum[n]!=-1)
    return sum[n];

    //Base cases (process first three elements)

    if(n==0)
    return sum[n] = 0;

    if(n==1)
    return sum[n] = arr[0];

    if(n==2)
    return sum[n] = arr[1]+arr[0];

    // Process rest of the elements
    // We have three cases
    return sum[n] = max(max(maxSumWO3Consec(n-1),
                    maxSumWO3Consec(n-2) + arr[n]),
                    arr[n] + arr[n-1] + maxSumWO3Consec(n-3));

}

// Driver code
int main()
{

    int n = sizeof(arr) / sizeof(arr[0]);
    memset(sum,-1,sizeof(sum));
    cout << maxSumWO3Consec(n);

// this code is contributed by Kushdeep Mittal
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// sum such that no three are
// consecutive using recursion.
import java.util.Arrays;

class GFG
{

static int arr[] = {100, 1000, 100, 1000, 1};
static int sum[] = new int[10000];

// Returns maximum subsequence
// sum such that no three
// elements are consecutive
static int maxSumWO3Consec(int n)
{
    if(sum[n] != -1)
        return sum[n];

    //Base cases (process first three elements)

    if(n == 0)
        return sum[n] = 0;

    if(n == 1)
        return sum[n] = arr[0];

    if(n == 2)
        return sum[n] = arr[1] + arr[0];

    // Process rest of the elements
    // We have three cases
    return sum[n] = Math.max(Math.max(maxSumWO3Consec(n - 1),
                    maxSumWO3Consec(n - 2) + arr[n]),
                    arr[n] + arr[n - 1] + maxSumWO3Consec(n - 3));

}

// Driver code
public static void main(String[] args)
{
    int n = arr.length;
        Arrays.fill(sum, -1);
    System.out.println(maxSumWO3Consec(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# sum such that no three are consecutive
# using recursion.
arr = [100, 1000, 100, 1000, 1]
sum = [-1] * 10000

# Returns maximum subsequence sum such
# that no three elements are consecutive
def maxSumWO3Consec(n) :

    if(sum[n] != -1):
        return sum[n]

    # 3 Base cases (process first
    # three elements)
    if(n == 0) :
        sum[n] = 0
        return sum[n]

    if(n == 1) :
        sum[n] = arr[0]
        return sum[n]

    if(n == 2) :
        sum[n] = arr[1] + arr[0]
        return sum[n]

    # Process rest of the elements
    # We have three cases
    sum[n] = max(max(maxSumWO3Consec(n - 1),
                     maxSumWO3Consec(n - 2) + arr[n]),
                     arr[n] + arr[n - 1] +
                     maxSumWO3Consec(n - 3))

    return sum[n]

# Driver code
if __name__ == "__main__" :

    n = len(arr)

    print(maxSumWO3Consec(n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the maximum
// sum such that no three are
// consecutive using recursion.
using System;

class GFG
{

    static int []arr = {100, 1000,
                        100, 1000, 1};
    static int []sum = new int[10000];

    // Returns maximum subsequence
    // sum such that no three
    // elements are consecutive
    static int maxSumWO3Consec(int n)
    {
        if(sum[n] != -1)
            return sum[n];

        //Base cases (process first
        // three elements)
        if(n == 0)
            return sum[n] = 0;

        if(n == 1)
            return sum[n] = arr[0];

        if(n == 2)
            return sum[n] = arr[1] + arr[0];

        // Process rest of the elements
        // We have three cases
        return sum[n] = Math.Max(Math.Max(maxSumWO3Consec(n - 1),
                        maxSumWO3Consec(n - 2) + arr[n]),
                        arr[n] + arr[n - 1] + maxSumWO3Consec(n - 3));

    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = arr.Length;
        for(int i = 0; i < sum.Length; i++)
            sum[i] = -1;
        Console.WriteLine(maxSumWO3Consec(n));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum sum such that
// no three are consecutive using recursion.
$arr = array(100, 1000, 100, 1000, 1);
$sum = array_fill(0, count($arr) + 1, -1);

// Returns maximum subsequence sum such that
// no three elements are consecutive
function maxSumWO3Consec($n)
{
    global $sum,$arr;
    if($sum[$n] != -1)
        return $sum[$n];

    // Base cases (process first three elements)
    if($n == 0)
        return $sum[$n] = 0;

    if($n == 1)
        return $sum[$n] = $arr[0];

    if($n == 2)
        return $sum[$n] = $arr[1] + $arr[0];

    // Process rest of the elements
    // We have three cases
    return $sum[$n] = max(max(maxSumWO3Consec($n - 1),
                              maxSumWO3Consec($n - 2) + $arr[$n]),
                                              $arr[$n] + $arr[$n - 1] +
                              maxSumWO3Consec($n - 3));
}

// Driver code
$n = count($arr);
echo maxSumWO3Consec($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find the maximum
    // sum such that no three are
    // consecutive using recursion.

    let arr = [100, 1000, 100, 1000, 1];
    let sum = new Array(10000);
    for(let i = 0; i < 10000; i++)
    {
        sum[i] = -1;
    }

    // Returns maximum subsequence
    // sum such that no three
    // elements are consecutive
    function maxSumWO3Consec(n)
    {
        if(sum[n] != -1)
        {
            return sum[n];   
        }

        //Base cases (process first three elements)

        if(n == 0)
        {
            return sum[n] = 0;
        }

        if(n == 1)
        {
            return sum[n] = arr[0];
        }

        if(n == 2)
        {
            return sum[n] = arr[1] + arr[0];
        }

        // Process rest of the elements
        // We have three cases        
          return sum[n] =
        500+Math.max(Math.max(maxSumWO3Consec(n - 1),
        maxSumWO3Consec(n - 2) + arr[n]),
        arr[n] + arr[n - 1] + maxSumWO3Consec(n - 3));
    }

    let n = arr.length - 1;
    document.write(maxSumWO3Consec(n) + 1);

</script>
```

**输出:**

```
2101
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
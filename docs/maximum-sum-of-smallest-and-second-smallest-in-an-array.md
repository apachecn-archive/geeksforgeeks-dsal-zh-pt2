# 数组中最小和第二小的最大和

> 原文:[https://www . geeksforgeeks . org/阵列中最小和第二最小的最大和/](https://www.geeksforgeeks.org/maximum-sum-of-smallest-and-second-smallest-in-an-array/)

#### 给定一个数组，从所有可能的子数组中找出最小和第二小元素的最大和。更正式地说，如果我们写出大小> =2 的数组的所有(nC2)子阵，并求出最小和第二小的和，那么我们的答案将是其中的最大和。
示例:

```
Input : arr[] = [4, 3, 1, 5, 6]
Output : 11
Subarrays with smallest and second smallest are,
[4, 3]        smallest = 3    second smallest = 4
[4, 3, 1]    smallest = 1    second smallest = 3
[4, 3, 1, 5]    smallest = 1    second smallest = 3
[4, 3, 1, 5, 6]    smallest = 1    second smallest = 3
[3, 1]         smallest = 1    second smallest = 3
[3, 1, 5]     smallest = 1    second smallest = 3
[3, 1, 5, 6]    smallest = 1    second smallest = 3
[1, 5]        smallest = 1    second smallest = 5
[1, 5, 6]    smallest = 1    second smallest = 5
[5, 6]         smallest = 5    second smallest = 6
Maximum sum among all above choices is, 5 + 6 = 11

Input : arr[] =  {5, 4, 3, 1, 6}
Output : 9
```

一个**简单的解决方法**就是生成所有的子阵，求每个子阵的最小和第二小的和。最后返回所有和的最大值。
一个**有效的解决方案**是基于这样的观察:这个问题简化为寻找数组中两个连续元素的最大和。

如果(x，y)是对，那么(x+y)就是答案，那么 x 和 y 必须是数组中连续的元素。

#### 证据:

对于具有 2 个元素的子阵列，第一个和第二个最小元素是这 2 个元素。

现在 x 和 y 出现在一些子阵列中，所以它们是端点。

现在，x，y 一定是那个子阵的最小的 2 个元素。如果还有其他元素 Z <sub>1</sub> ，Z <sub>2</sub> ，……。，Z <sub>K</sub> 在 x 和 y 之间，它们大于或等于 x 和 y，

#### 案例 1:

如果在 x 和 y 之间有一个元素 z，那么包含元素 max(x，y)和 z 的较小子阵列应该是答案，因为 max(x，y) + z >= x + y

#### 案例 2:

如果 x 和 y 之间有多个元素，那么 x 和 y 内的子阵列将有所有连续的元素(Z<sub>I</sub>+Z<sub>I+1</sub>)>=(x+y)，所以(x，y)对不可能是答案。

所以，通过矛盾，x 和 y 必须是数组中连续的元素。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to get max sum with smallest
// and second smallest element from any subarray
#include <bits/stdc++.h>
using namespace std;

/*  Method returns maximum obtainable sum value
    of smallest and the second smallest value
    taken over all possible subarrays */
int pairWithMaxSum(int arr[], int N)
{
   if (N < 2)
     return -1;

   // Find two consecutive elements with maximum
   // sum.
   int res = arr[0] + arr[1];
   for (int i=1; i<N-1; i++)
      res = max(res, arr[i] + arr[i+1]);

   return res;
}

//  Driver code to test above methods
int main()
{
    int arr[] = {4, 3, 1, 5, 6};
    int N = sizeof(arr) / sizeof(int);

    cout << pairWithMaxSum(arr, N) << endl;
    return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to get max sum with smallest
// and second smallest element from any subarray
import java.lang.*;
class num{

// Method returns maximum obtainable sum value
// of smallest and the second smallest value
// taken over all possible subarrays */
static int pairWithMaxSum(int[] arr, int N)
{
if (N < 2)
    return -1;

// Find two consecutive elements with maximum
// sum.
int res = arr[0] + arr[1];
for (int i=1; i<N-1; i++)
    res = Math.max(res, arr[i] + arr[i+1]);

return res;
}

// Driver program
public static void main(String[] args)
{
    int arr[] = {4, 3, 1, 5, 6};
    int N = arr.length;
    System.out.println(pairWithMaxSum(arr, N));
}
}
//This code is contributed by
//Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to get max
# sum with smallest and second
# smallest element from any
# subarray

# Method returns maximum obtainable
# sum value of smallest and the
# second smallest value taken
# over all possible subarrays
def pairWithMaxSum(arr, N):

    if (N < 2):
        return -1

    # Find two consecutive elements with
    # maximum sum.
    res = arr[0] + arr[1]

    for i in range(1, N-1):
        res = max(res, arr[i] + arr[i + 1])

    return res

# Driver code
arr = [4, 3, 1, 5, 6]
N = len(arr)

print(pairWithMaxSum(arr, N))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to get max sum with smallest
// and second smallest element from any subarray
using System;

class GFG {

// Method returns maximum obtainable sum value
// of smallest and the second smallest value
// taken over all possible subarrays
static int pairWithMaxSum(int []arr, int N)
{

if (N < 2)
    return -1;

// Find two consecutive elements
// with maximum sum.
int res = arr[0] + arr[1];
for (int i = 1; i < N - 1; i++)
    res = Math.Max(res, arr[i] + arr[i + 1]);

return res;
}

// Driver code
public static void Main()
{
    int []arr = {4, 3, 1, 5, 6};
    int N = arr.Length;
    Console.Write(pairWithMaxSum(arr, N));
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get max sum with smallest
// and second smallest element from any subarray

/* Method returns maximum
   obtainable sum value
   of smallest and the
   second smallest value
   taken over all possible
   subarrays */
function pairWithMaxSum( $arr, $N)
{
    if ($N < 2)
        return -1;

    // Find two consecutive
    // elements with maximum
    // sum.
    $res = $arr[0] + $arr[1];
    for($i = 1; $i < $N - 1; $i++)
        $res = max($res, $arr[$i] +
                    $arr[$i + 1]);

    return $res;
}

    // Driver Code
    $arr = array(4, 3, 1, 5, 6);
    $N = count($arr);

    echo pairWithMaxSum($arr, $N);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
// javascript program to get max sum with smallest
// and second smallest element from any subarray

// Method returns maximum obtainable sum value
// of smallest and the second smallest value
// taken over all possible subarrays

function pairWithMaxSum(arr,  N)
{

if (N < 2)
    return -1;

// Find two consecutive elements
// with maximum sum.

var res = arr[0] + arr[1];
for (var i = 1; i < N - 1; i++)
    res = Math.max(res, arr[i] + arr[i + 1]);

return res;
}

// Driver code

    var arr = [4, 3, 1, 5, 6]
    var N = arr.length;
    document.write(pairWithMaxSum(arr, N));

// This code is contributed by bunnyram19.
```

输出:

```
11
```

时间复杂度:O(n)
感谢 Md Mishfaq Ahmed 提出这个方法。
本文由 [**【乌塔什·特里维迪】**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
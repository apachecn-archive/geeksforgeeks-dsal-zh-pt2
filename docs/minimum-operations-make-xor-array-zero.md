# 使数组异或为零的最小运算

> 原文:[https://www . geesforgeks . org/minimum-operations-make-xor-array-zero/](https://www.geeksforgeeks.org/minimum-operations-make-xor-array-zero/)

给我们一个由 n 个元素组成的数组。任务是对整个数组 0 进行异或运算。我们可以通过以下方式来实现这一点。

1.  我们可以选择任何一个元素。
2.  选择一个元素后，我们可以增加或减少 1。

我们需要找到所选元素所需的最小递增/递减操作数，以使整个数组的异或和为零。

**示例:**

```
Input : arr[] = {2, 4, 8}
Output : Element = 8, 
         Operation required = 2
Explanation : Select 8 as element and perform 2 
              time decrement on it. So that it
              became 6, Now our array is {2, 4, 6} 
              whose XOR sum is 0.

Input : arr[] = {1, 1, 1, 1}
Output : Element = 1, 
         Operation required = 0
Explanation : Select any of 1 and you have already
              your XOR sum = 0\. So, no operation 
              required.
```

**天真方法:**选择一个元素，然后求数组其余部分的异或。如果那个元素变成等于异或，那么我们整个数组的异或应该变成零。现在，我们的成本将是所选元素和所获得的异或之间的绝对差异。这一寻找成本的过程将针对每个元素进行，因此导致时间复杂度为(n^2).
**高效进场:**求全阵异或。现在，假设我们选择了 arr[i]元素，那么该元素所需成本将是 absolute(arr[i]-(XORsum^arr[i])).计算每个元素的这些绝对值的最小值将是我们的最小所需操作，与最小所需操作相对应的元素也将是我们选择的元素。

## C++

```
// CPP to find min cost to make
// XOR of whole array zero
#include <bits/stdc++.h>
using namespace std;

// function to find min cost
void minCost(int arr[], int n)
{
    int cost = INT_MAX;
    int element;

    // calculate XOR sum of array
    int XOR = 0;
    for (int i = 0; i < n; i++)
        XOR ^= arr[i];

    // find the min cost and element corresponding
    for (int i = 0; i < n; i++) {
        if (cost > abs((XOR ^ arr[i]) - arr[i])) {
            cost = abs((XOR ^ arr[i]) - arr[i]);
            element = arr[i];
        }
    }

    cout << "Element = " << element << endl;
    cout << "Operation required = " << abs(cost);
}

// driver program
int main()
{
    int arr[] = { 2, 8, 4, 16 };
    int n = sizeof(arr) / sizeof(arr[0]);
    minCost(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find min cost to make
// XOR of whole array zero
import java.lang.*;

class GFG
{
    // function to find min cost
    static void minCost(int[] arr, int n)
    {
        int cost = Integer.MAX_VALUE;
        int element=0;

        // calculate XOR sum of array
        int XOR = 0;
        for (int i = 0; i < n; i++)
            XOR ^= arr[i];

        // find the min cost and element
        // corresponding
        for (int i = 0; i < n; i++) {
            if (cost > Math.abs((XOR ^ arr[i])
                                - arr[i])) {
                cost = Math.abs((XOR ^ arr[i]) -
                                       arr[i]);
                element = arr[i];
            }
        }

    System.out.println("Element = " + element);
    System.out.println("Operation required = "+
                             Math.abs(cost));
    }

    // driver program
    public static void main (String[] args)
    {
        int[] arr = { 2, 8, 4, 16 };
        int n = arr.length;
        minCost(arr, n);
    }
}
/* This code is contributed by Kriti Shukla */
```

## 蟒蛇 3

```
# python to find min cost to make
# XOR of whole array zero

# function to find min cost
def minCost(arr,n):

    cost = 999999;

    # calculate XOR sum of array
    XOR = 0;
    for i in range(0, n):
        XOR ^= arr[i];

    # find the min cost and element
    # corresponding
    for i in range(0,n):
        if (cost > abs((XOR ^ arr[i]) - arr[i])):
            cost = abs((XOR ^ arr[i]) - arr[i])
            element = arr[i]

    print("Element = ", element)
    print("Operation required = ", abs(cost))

# driver program
arr = [ 2, 8, 4, 16 ]
n = len(arr)
minCost(arr, n)

# This code is contributed by Sam007
```

## C#

```
// C# program to find min cost to
// make XOR of whole array zero
using System;

class GFG
{
    // function to find min cost
    static void minCost(int []arr, int n)
    {
        int cost = int.MaxValue;
        int element=0;

        // calculate XOR sum of array
        int XOR = 0;
        for (int i = 0; i < n; i++)
            XOR ^= arr[i];

        // find the min cost and
        // element corresponding
        for (int i = 0; i < n; i++)
        {
            if (cost > Math.Abs((XOR ^ arr[i]) - arr[i]))
            {
                cost = Math.Abs((XOR ^ arr[i]) - arr[i]);
                element = arr[i];
            }
        }

    Console.WriteLine("Element = " + element);
    Console.Write("Operation required = "+
                          Math.Abs(cost));
    }

    // Driver program
    public static void Main ()
    {
        int []arr = {2, 8, 4, 16};
        int n = arr.Length;
        minCost(arr, n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to find min cost to make
// XOR of whole array zero

// function to find min cost
function minCost($arr, $n)
{
    $cost = PHP_INT_MAX;
    $element;

    // calculate XOR sum of array
    $XOR = 0;
    for ($i = 0; $i < $n; $i++)
        $XOR ^= $arr[$i];

    // find the min cost and
    // element corresponding
    for ($i = 0; $i < $n; $i++)
    {
        if ($cost > abs(($XOR ^ $arr[$i]) -
                                 $arr[$i]))
        {
            $cost = abs(($XOR ^ $arr[$i]) -
                                 $arr[$i]);
            $element = $arr[$i];
        }
    }

    echo "Element = " , $element ,"\n";
    echo "Operation required = " , abs($cost);
}

// Driver Code
$arr = array(2, 8, 4, 16) ;
$n = count($arr);
minCost($arr, $n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// javascript to find min cost to make
// XOR of whole array zero

// function to find min cost
function minCost(arr, n)
{
    var cost = 1000000000;
    var element;

    // calculate XOR sum of array
    var XOR = 0;
    for (var i = 0; i < n; i++)
        XOR ^= arr[i];

    // find the min cost and element corresponding
    for (var i = 0; i < n; i++) {
        var x= Math.abs((XOR ^ arr[i]) - arr[i])
        if (cost > x) {
            cost = x;
            element = arr[i];
        }
    }

    document.write( "Element = " + element + "<br>");
    document.write( "Operation required = " + Math.abs(cost));
}

// driver program
var arr = [ 2, 8, 4, 16 ];
var n = arr.length;
minCost(arr, n);

</script>
```

**输出:**

```
Element = 16
Operation required = 2
```

时间复杂度:O(n)
本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
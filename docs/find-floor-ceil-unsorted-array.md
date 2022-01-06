# 在未排序的数组中查找楼层和天花板

> 原文:[https://www . geesforgeks . org/find-floor-ceil-unsorted-array/](https://www.geeksforgeeks.org/find-floor-ceil-unsorted-array/)

给定一个未排序的数组 arr[]和一个元素 x，求 arr[0]中 x 的下限和上限..n-1]。
**x 的 Floor** 是小于或等于 x 的最大元素，如果 x 小于 arr[]的最小元素，则不存在 x 的 Floor。
**x 的 Cell**是大于或等于 x 的最小元素，如果 x 大于 arr[]的 greates 元素，则 x 的 Cell 不存在。
**举例:**

```
Input : arr[] = {5, 6, 8, 9, 6, 5, 5, 6}      
        x = 7
Output : Floor = 6
         Ceiling = 8

Input : arr[] = {5, 6, 8, 9, 6, 5, 5, 6}      
        x = 6
Output : Floor = 6
         Ceiling = 6

Input : arr[] = {5, 6, 8, 9, 6, 5, 5, 6}      
        x = 10
Output : Floor = 9
         Ceiling doesn't exist.
```

**方法 1(使用排序)**
1)排序输入数组。
2)使用二分搜索法查找 x 的地板和天花板，参照[本](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)和[本](https://www.geeksforgeeks.org/search-floor-and-ceil-in-a-sorted-array/)实现地板和天花板的排序排列。
时间复杂度:O(n log n)
辅助空间:O(1)
如果在一个静态数组上有多个楼层和天花板的查询，这个解决方案是很好用的。我们可以对数组进行一次排序，并在 O(Log n)时间内回答查询。
**方法 2(使用线性搜索**
思路是遍历数组并保持两个距离相对于 x 的轨迹。
1)元素的最小距离大于或等于 x。
2)元素的最小距离小于或等于 x。
最后打印最小距离的元素。

## C++

```
// C++ program to find floor and ceiling in an
// unsorted array.
#include<bits/stdc++.h>
using namespace std;

// Function to floor and ceiling of x in arr[]
void floorAndCeil(int arr[], int n, int x)
{
    // Indexes of floor and ceiling
    int fInd, cInd;

    // Distances of current floor and ceiling
    int fDist = INT_MAX, cDist = INT_MAX;

    for (int i=0; i<n; i++)
    {
        // If current element is closer than
        // previous ceiling.
        if (arr[i] >= x && cDist > (arr[i] - x))
        {
        cInd = i;
        cDist = arr[i] - x;
        }

        // If current element is closer than
        // previous floor.
        if (arr[i] <= x && fDist > (x - arr[i]))
        {
        fInd = i;
        fDist = x - arr[i];
        }
    }

    if (fDist == INT_MAX)
    cout << "Floor doesn't exist " << endl;
    else
    cout << "Floor is " << arr[fInd] << endl;

    if (cDist == INT_MAX)
    cout << "Ceil doesn't exist " << endl;
    else
    cout << "Ceil is " << arr[cInd] << endl;
}

// Driver code
int main()
{
    int arr[] = {5, 6, 8, 9, 6, 5, 5, 6};
    int n = sizeof(arr)/sizeof(int);
    int x = 7;
    floorAndCeil(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find floor and ceiling in an
// unsorted array.
import java.io.*;

class GFG
{
     // Function to floor and ceiling of x in arr[]
    public static void floorAndCeil(int arr[], int x)
    {
        int n = arr.length;

        // Indexes of floor and ceiling
        int fInd = -1, cInd = -1;

        // Distances of current floor and ceiling
        int fDist = Integer.MAX_VALUE, cDist = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++)
        {
            // If current element is closer than
            // previous ceiling.
            if (arr[i] >= x && cDist > (arr[i] - x))
            {
                cInd = i;
                cDist = arr[i] - x;
            }

            // If current element is closer than
            // previous floor.
            if (arr[i] <= x && fDist > (x - arr[i]))
            {
                fInd = i;
                fDist = x - arr[i];
            }
        }

        if(fDist == Integer.MAX_VALUE)
            System.out.println("Floor doesn't exist " );
        else
            System.out.println("Floor is " +  arr[fInd]);

        if(cDist == Integer.MAX_VALUE)
            System.out.println("Ceil doesn't exist ");
        else
            System.out.println("Ceil is  " + arr[cInd]);
    }

    public static void main (String[] args)
    {
        int arr[] = {5, 6, 8, 9, 6, 5, 5, 6};
        int x = 7;
        floorAndCeil(arr, x);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# floor and ceiling in an
# unsorted array.

import sys

# Function to floor and
# ceiling of x in arr[]
def floorAndCeil(arr, n, x):

    # Distances of current
    # floor and ceiling
    fDist = sys.maxsize
    cDist = sys.maxsize

    for i in range(n):

        # If current element is closer
        # than previous ceiling.
        if (arr[i] >= x and
            cDist > (arr[i] - x)):

            cInd = i
            cDist = arr[i] - x

        # If current element is closer
        # than previous floor.
        if (arr[i] <= x and fDist > (x - arr[i])):

            fInd = i
            fDist = x - arr[i]

    if (fDist == sys.maxsize):
        print("Floor doesn't exist ")
    else:
        print("Floor is " + str(arr[fInd]))

    if (cDist == sys.maxsize):
        print( "Ceil doesn't exist ")
    else:
        print("Ceil is " + str(arr[cInd]))

# Driver code
if __name__ == "__main__":
    arr = [5, 6, 8, 9, 6, 5, 5, 6]
    n = len(arr)
    x = 7
    floorAndCeil(arr, n, x)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find floor and ceiling in an
// unsorted array.
using System;

class GFG {

    // Function to floor and ceiling of x in arr[]
    public static void floorAndCeil(int []arr, int x)
    {
        int n = arr.Length;

        // Indexes of floor and ceiling
        int fInd = -1, cInd = -1;

        // Distances of current floor and ceiling
        int fDist = int.MaxValue,
            cDist =int.MaxValue;

        for (int i = 0; i < n; i++)
        {

            // If current element is closer than
            // previous ceiling.
            if (arr[i] >= x && cDist > (arr[i] - x))
            {
                cInd = i;
                cDist = arr[i] - x;
            }

            // If current element is closer than
            // previous floor.
            if (arr[i] <= x && fDist > (x - arr[i]))
            {
                fInd = i;
                fDist = x - arr[i];
            }
        }

        if(fDist == int.MaxValue)
            Console.Write("Floor doesn't exist " );
        else
            Console.WriteLine("Floor is " + arr[fInd]);

        if(cDist == int.MaxValue)
        Console.Write("Ceil doesn't exist ");
        else
            Console.Write("Ceil is " + arr[cInd]);
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {5, 6, 8, 9, 6, 5, 5, 6};
        int x = 7;

        floorAndCeil(arr, x);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// floor and ceiling in
// an unsorted array.

// Function to floor and
// ceiling of x in arr[]
function floorAndCeil($arr,
                      $n, $x)
{
    // Indexes of floor
    // and ceiling
    $fInd = 0;
    $cInd = 0;

    // Distances of current
    // floor and ceiling
    $fDist = 999999;
    $cDist = 999999;

    for ($i = 0; $i < $n; $i++)
    {
        // If current element
        // is closer than
        // previous ceiling.
        if ($arr[$i] >= $x &&
            $cDist > ($arr[$i] - $x))
        {
            $cInd = $i;
            $cDist = $arr[$i] - $x;
        }

        // If current element
        // is closer than
        // previous floor.
        if ($arr[$i] <= $x &&
            $fDist > ($x - $arr[$i]))
        {
            $fInd = $i;
            $fDist = $x - $arr[$i];
        }
    }

    if ($fDist == 999999)
        echo "Floor doesn't ".
             "exist " . "\n" ;
    else
        echo "Floor is " .
              $arr[$fInd] . "\n";

    if ($cDist == 999999)
        echo "Ceil doesn't " .
             "exist " . "\n";
    else
        echo "Ceil is " .
             $arr[$cInd] . "\n";
}

// Driver code
$arr = array(5, 6, 8, 9,
             6, 5, 5, 6);
$n = count($arr);
$x = 7;
floorAndCeil($arr, $n, $x);

// This code is contributed
// by Sam007
?>
```

## java 描述语言

```
<script>
// Javascript program to find floor and ceiling in an
// unsorted array.

    // Function to floor and ceiling of x in arr[]
    function floorAndCeil(arr,x)
    {
        let n = arr.length;

        // Indexes of floor and ceiling
        let fInd = -1, cInd = -1;

        // Distances of current floor and ceiling
        let fDist = Number.MAX_VALUE, cDist = Number.MAX_VALUE;

        for (let i = 0; i < n; i++)
        {
            // If current element is closer than
            // previous ceiling.
            if (arr[i] >= x && cDist > (arr[i] - x))
            {
                cInd = i;
                cDist = arr[i] - x;
            }

            // If current element is closer than
            // previous floor.
            if (arr[i] <= x && fDist > (x - arr[i]))
            {
                fInd = i;
                fDist = x - arr[i];
            }
        }

        if(fDist == Number.MAX_VALUE)
            document.write("Floor doesn't exist <br>" );
        else
            document.write("Floor is " +  arr[fInd]+"<br>");

        if(cDist == Number.MAX_VALUE)
            document.write("Ceil doesn't exist <br>");
        else
            document.write("Ceil is  " + arr[cInd]+"<br>");
    }

    let arr=[5, 6, 8, 9, 6, 5, 5, 6];
    let x = 7;
    floorAndCeil(arr, x);

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Floor is 6
Ceil is 8
```

**时间复杂度:** O(n)
**辅助空间:** O(1)
**相关文章:**
[排序数组中的天花板](https://www.geeksforgeeks.org/search-floor-and-ceil-in-a-sorted-array/)
[排序数组中的地板](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)
本文由**丹麦语 _RAZA** 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
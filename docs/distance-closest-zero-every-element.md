# 距离每个元素最近的零点的距离

> 原文:[https://www . geesforgeks . org/distance-close-zero-ever-element/](https://www.geeksforgeeks.org/distance-closest-zero-every-element/)

给定一个 n 个整数的数组，对于每个元素，打印最接近零的距离。数组中至少有 1 个零。
**例:**

```
Input: 5 6 0 1 -2 3 4
Output: 2 1 0 1 2 3 4 
Explanation : The nearest 0(indexed 2) to 
5(indexed 0) is at a distance of 2, so we 
print 2\. Same is done for the rest of elements.
```

**天真的方法:**天真的方法是，对于每个元素，向左滑动并找出最近的 0，然后再次向右滑动以找出最近的 0(如果有的话)，并打印两个距离的最小值。这将是空间高效的，但是时间复杂度将会很高，因为我们必须迭代每个元素，直到我们找到 0，在最坏的情况下，我们可能在一个方向上找不到。
*时间复杂度* : O(n^2)
*辅助空间:* O(1)

**高效的方法:**一种高效的方法是使用[滑动窗口手法](https://www.geeksforgeeks.org/window-sliding-technique/)两次。一种是从右向左穿越，另一种是从左向右穿越。
用最大值初始化 ans[0]。从左到右迭代数组。如果当前位置的值为 0，则将距离设置为 0，否则将距离增加 1。在每一步中，将距离值写入答案数组。
做同样的事情，但是从右向左。这会发现最接近右边的零。现在我们应该存储当前距离值和答案数组中已经存在的值的最小值。
以下是上述办法的实施情况。

## C++

```
// CPP program to find closest 0 for every element
#include <bits/stdc++.h>
using namespace std;

// Print the distance with zeroes of every element
void print_distance(int arr[], int n)
{
    // initializes an array of size n with 0
    int ans[n];
    memset(arr, 0, sizeof(arr));

    // if first element is 0 then the distance
    // will be 0
    if (arr[0] == 0)
        ans[0] = 0;
    else
        ans[0] = INT_MAX; // if not 0 then initialize
                          // with a maximum value

    // traverse in loop from 1 to n and store
    // the distance from left
    for (int i = 1; i < n; ++i) {

        // add 1 to the distance from previous one
        ans[i] = ans[i - 1] + 1;

        // if the present element is 0 then distance
        // will be 0
        if (arr[i] == 0)
            ans[i] = 0;       
    }

    // if last element is zero then it will be 0 else
    // let the answer be what was found when traveled
    // form left to right
    if (arr[n - 1] == 0)
        ans[n - 1] = 0;

    // traverse from right to left and store the minimum
    // of distance if found from right to left or left
    // to right
    for (int i = n - 2; i >= 0; --i) {

        // store the minimum of distance from left to
        // right or right to left
        ans[i] = min(ans[i], ans[i + 1] + 1);

        // if it is 0 then minimum will always be 0
        if (arr[i] == 0)
            ans[i] = 0;
    }

    // print the answer array
    for (int i = 0; i < n; ++i)
        cout << ans[i] << " ";   
}

// driver program to test the above function
int main()
{
    int a[] = { 2, 1, 0, 3, 0, 0, 3, 2, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    printDistances(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find closest
// 0 for every element
import java.util.Arrays;

class GFG
{
    // Print the distance with zeroes of every element
    static void print_distance(int arr[], int n)
    {
        // initializes an array of size n with 0
        int ans[]=new int[n];
        Arrays.fill(ans,0);

        // if first element is 0 then the distance
        // will be 0
        if (arr[0] == 0)
            ans[0] = 0;

        // if not 0 then initialize
        // with a maximum value   
        else
            ans[0] = +2147483647;

        // traverse in loop from 1 to n and store
        // the distance from left
        for (int i = 1; i < n; ++i)
        {

            // add 1 to the distance
            // from previous one
            ans[i] = ans[i - 1] + 1;

            // if the present element is
            // 0 then distance will be 0
            if (arr[i] == 0)
                ans[i] = 0;    
        }

        // if last element is zero
        // then it will be 0 else
        // let the answer be what was
        // found when traveled
        // form left to right
        if (arr[n - 1] == 0)
            ans[n - 1] = 0;

        // traverse from right to
        // left and store the minimum
        // of distance if found from
        // right to left or left
        // to right
        for (int i = n - 2; i >= 0; --i)
        {

            // store the minimum of distance
            // from left to right or right to left
            ans[i] = Math.min(ans[i], ans[i + 1] + 1);

            // if it is 0 then minimum
            // will always be 0
            if (arr[i] == 0)
                ans[i] = 0;
        }

        // print the answer array
        for (int i = 0; i < n; ++i)
            System.out.print(ans[i] + " ");
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 2, 1, 0, 3, 0, 0, 3, 2, 4 };
        int n = a.length;
        print_distance(a, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find closest 0
# for every element

# Print the distance with zeroes of
# every element
def print_distance(arr, n):

    # initializes an array of size n with 0
    ans = [0 for i in range(n)]

    # if first element is 0 then the
    # distance will be 0
    if (arr[0] == 0):
        ans[0] = 0
    else:
        ans[0] = 10**9  # if not 0 then initialize
                        # with a maximum value

    # traverse in loop from 1 to n and
    # store the distance from left
    for i in range(1, n):

        # add 1 to the distance from
        # previous one
        ans[i] = ans[i - 1] + 1

        # if the present element is 0 then
        # distance will be 0
        if (arr[i] == 0):
            ans[i] = 0

    # if last element is zero then it will be 0
    # else let the answer be what was found when
    # traveled form left to right
    if (arr[n - 1] == 0):
        ans[n - 1] = 0

    # traverse from right to left and store
    # the minimum of distance if found from
    # right to left or left to right
    for i in range(n - 2, -1, -1):

        # store the minimum of distance from
        # left to right or right to left
        ans[i] = min(ans[i], ans[i + 1] + 1)

        # if it is 0 then minimum will
        # always be 0
        if (arr[i] == 0):
            ans[i] = 0

    # print the answer array
    for i in ans:
        print(i, end = " ")

# Driver Code
a = [2, 1, 0, 3, 0, 0, 3, 2, 4]
n = len(a)
print_distance(a, n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find closest
// 0 for every element
using System;
class GFG
{
    // Print the distance with zeroes of every element
    static void print_distance(int []arr, int n)
    {
        // initializes an array of size n with 0
        int []ans=new int[n];
        for(int i = 0; i < n; i++)
            ans[i] = 0;

        // if first element is 0 then the distance
        // will be 0
        if (arr[0] == 0)
            ans[0] = 0;

        // if not 0 then initialize
        // with a maximum value
        else
            ans[0] = +2147483646;

        // traverse in loop from 1 to n and store
        // the distance from left
        for (int i = 1; i < n; ++i)
        {

            // add 1 to the distance
            // from previous one
            ans[i] = ans[i - 1] + 1;

            // if the present element is
            // 0 then distance will be 0
            if (arr[i] == 0)
                ans[i] = 0;    
        }

        // if last element is zero
        // then it will be 0 else
        // let the answer be what was
        // found when traveled
        // form left to right
        if (arr[n - 1] == 0)
            ans[n - 1] = 0;

        // traverse from right to
        // left and store the minimum
        // of distance if found from
        // right to left or left
        // to right
        for (int i = n - 2; i >= 0; --i)
        {

            // store the minimum of distance
            // from left to right or right to left
            ans[i] = Math.Min(ans[i], ans[i + 1] + 1);

            // if it is 0 then minimum
            // will always be 0
            if (arr[i] == 0)
                ans[i] = 0;
        }

        // print the answer array
        for (int i = 0; i < n; ++i)
            Console.Write(ans[i] + " ");
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []a = { 2, 1, 0, 3, 0, 0, 3, 2, 4 };
        int n = a.Length;
        print_distance(a, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find closest 0
// for every element

// Print the distance with zeroes
// of every element
function print_distance($arr, $n)
{
    // initializes an array of size n with 0
    $ans[$n] = array();

    $ans = array_fill(0, $n, true);

    // if first element is 0 then the
    // distance will be 0
    if ($arr[0] == 0)
        $ans[0] = 0;
    else
        $ans[0] = PHP_INT_MAX; // if not 0 then initialize
                               // with a maximum value

    // traverse in loop from 1 to n and
    // store the distance from left
    for ( $i = 1; $i < $n; ++$i)
    {

        // add 1 to the distance from
        // previous one
        $ans[$i] = $ans[$i - 1] + 1;

        // if the present element is 0
        // then distance will be 0
        if ($arr[$i] == 0)
            $ans[$i] = 0;    
    }

    // if last element is zero then it will
    // be 0 else let the answer be what was
    // found when traveled form left to right
    if ($arr[$n - 1] == 0)
        $ans[$n - 1] = 0;

    // traverse from right to left and store
    // the minimum of distance if found from
    // right to left or left to right
    for ($i = $n - 2; $i >= 0; --$i)
    {

        // store the minimum of distance from
        // left to right or right to left
        $ans[$i] = min($ans[$i], $ans[$i + 1] + 1);

        // if it is 0 then minimum will
        // always be 0
        if ($arr[$i] == 0)
            $ans[$i] = 0;
    }

    // print the answer array
    for ($i = 0; $i < $n; ++$i)
        echo $ans[$i] , " ";
}

// Driver Code
$a = array( 2, 1, 0, 3, 0, 0, 3, 2, 4 );
$n = sizeof($a);
print_distance($a, $n);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>
// javascript program to find closest
// 0 for every element
// Print the distance with zeroes of every element
    function print_distance(arr , n)
    {

        // initializes an array of size n with 0
        var ans = Array(n).fill(0);

        // if first element is 0 then the distance
        // will be 0
        if (arr[0] == 0)
            ans[0] = 0;

        // if not 0 then initialize
        // with a maximum value
        else
            ans[0] = +2147483647;

        // traverse in loop from 1 to n and store
        // the distance from left
        for (i = 1; i < n; ++i) {

            // add 1 to the distance
            // from previous one
            ans[i] = ans[i - 1] + 1;

            // if the present element is
            // 0 then distance will be 0
            if (arr[i] == 0)
                ans[i] = 0;
        }

        // if last element is zero
        // then it will be 0 else
        // let the answer be what was
        // found when traveled
        // form left to right
        if (arr[n - 1] == 0)
            ans[n - 1] = 0;

        // traverse from right to
        // left and store the minimum
        // of distance if found from
        // right to left or left
        // to right
        for (i = n - 2; i >= 0; --i) {

            // store the minimum of distance
            // from left to right or right to left
            ans[i] = Math.min(ans[i], ans[i + 1] + 1);

            // if it is 0 then minimum
            // will always be 0
            if (arr[i] == 0)
                ans[i] = 0;
        }

        // print the answer array
        for (i = 0; i < n; ++i)
            document.write(ans[i] + " ");
    }

    // Driver code
        var a = [ 2, 1, 0, 3, 0, 0, 3, 2, 4 ];
        var n = a.length;
        print_distance(a, n);

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
2 1 0 1 0 0 1 2 3 
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由[**Raja vikramatitya**](https://www.facebook.com/raja.vikramaditya.7)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
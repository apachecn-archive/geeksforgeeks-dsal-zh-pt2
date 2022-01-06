# 最大化数组中连续元素子集的大小

> 原文:[https://www . geesforgeks . org/maximum-size-continuous-element-subset-array/](https://www.geeksforgeeks.org/maximise-size-consecutive-element-subsets-array/)

给定一个整数数组和一个整数 k。数组元素表示一维数字线上的点的位置，求点子集的最大大小，该子集可以具有连续的点值，这些点值可以通过在数字线上放置另 k 个点来形成。请注意，所有坐标都应该是不同的，并且数组的元素是按升序排列的。

**示例:**

```
Input : arr[] = {1, 2, 3, 4, 10, 11, 14, 15},
            k = 4 
Output : 8
For maximum size subset, it is optimal to
choose the points on number line at 
coordinates 12, 13, 16 and 17, so that the
size of the consecutive valued subset will
become 8 which will be maximum .

Input : arr[] = {7, 8, 12, 13, 15, 18}
        k = 5
Output : 10
For maximum size subset, it is optimal to choose
the points on number line at coordinates 9, 10, 
11, 14 and 16, so that the size of the consecutive 
valued subset will become 10 which will be maximum .
```

**蛮力方法(时间复杂度–O(N<sup>2</sup>):**

蛮力包括检查条件((arr[r]-arr[l])-(r-l)) ≤ k 的所有可能的(l，r)对。为了找出一对(l，r)是否有效，我们应该检查需要放置在这两个初始对之间的点数是否不大于 k。由于 arr[i]是输入数组(arr)中第 I 个点的坐标，因此我们需要检查(arr[r]–arr[l])–(r–l)≤k。

这个解决方案的复杂度为 O(N <sup>2</sup> )。

## C++

```
/* C++ program to find the maximum size of subset of
   points that can have consecutive values using
   brute force */
#include <bits/stdc++.h>
using namespace std;

int maximiseSubset(int arr[], int n, int k)
{
    // Since we can always enforce the solution
    // to contain all the K added points
    int ans = k;

    for (int l = 0; l < n - 1; l++)
        for (int r = l; r < n; r++)

            // check if the number of points that
            // need to be placed between these two
            // initial ones is not greater than k
            if ((arr[r] - arr[l]) - (r - l) <= k)
                ans = max(ans, r - l + k + 1);

    return (ans);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 10, 11, 14, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;
    printf("%dn", maximiseSubset(arr, n, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find the maximum size of subset of
points that can have consecutive values using
brute force */
import java.util.*;

class GFG
{

    static int maximiseSubset(int[] arr, int n, int k)
    {
        // Since we can always enforce the solution
        // to contain all the K added points
        int ans = k;

        for (int l = 0; l < n - 1; l++)
            for (int r = l; r < n; r++)

                // check if the number of points that
                // need to be placed between these two
                // initial ones is not greater than k
                if ((arr[r] - arr[l]) - (r - l) <= k)
                    ans = Math.max(ans, r - l + k + 1);

        return (ans);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4, 10, 11, 14, 15 };
        int n = arr.length;
        int k = 4;
        System.out.println(maximiseSubset(arr, n, k)); 
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python3 program to find the maximum size
# of subset of points that can have consecutive
# values using brute force

def maximiseSubset(arr , n, k):

    # Since we can always enforce the solution
    # to contain all the K added points
    ans = k

    for l in range(n - 1):
        for r in range(l, n):

            # check if the number of points that
            # need to be placed between these two
            # initial ones is not greater than k
            if ((arr[r] - arr[l]) - (r - l) <= k) :
                ans = max(ans, r - l + k + 1)

    return (ans)

# Driver code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 10, 11, 14, 15 ]
    n = len(arr)
    k = 4
    print(maximiseSubset(arr, n, k))

# This code is contributed by ita_c
```

## C#

```
/* C# program to find the
maximum size of subset of
points that can have
consecutive values using
brute force */
using System;

class GFG
{

    static int maximiseSubset(int[] arr,
                              int n, int k)
    {
        // Since we can always enforce
        // the solution to contain all
        // the K added points
        int ans = k;

        for (int l = 0; l < n - 1; l++)
            for (int r = l; r < n; r++)

                // check if the number of
                // points that need to be
                // placed between these
                // two initial ones is not
                // greater than k
                if ((arr[r] - arr[l]) -
                              (r - l) <= k)
                    ans = Math.Max(ans, r - l +
                                        k + 1);

        return (ans);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = {1, 2, 3, 4,
                    10, 11, 14, 15};
        int n = arr.Length;
        int k = 4;
        Console.WriteLine(maximiseSubset(arr, n, k));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum size
// of subset of points that can have 
// consecutive values using brute force
function maximiseSubset($arr, $n, $k)
{
    // Since we can always enforce
    // the solution to contain all
    // the K added points
    $ans = $k;

    for ($l = 0; $l < $n - 1; $l++)
        for ($r = $l; $r < $n; $r++)

            // check if the number of points that
            // need to be placed between these two
            // initial ones is not greater than k
            if (($arr[$r] - $arr[$l]) -
                ($r - $l) <= $k)
                $ans = max($ans, $r - $l + $k + 1);

    return ($ans);
}

// Driver code
$arr = array(1, 2, 3, 4, 10, 11, 14, 15 );
$n = sizeof($arr);
$k = 4;
echo (maximiseSubset($arr, $n, $k));

// This code is contributed
// by Sach_Code   
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// maximum size of subset of points
// that can have consecutive values using
// brute force
function maximiseSubset(arr, n, k)
{

    // Since we can always enforce the
    // solution to contain all the K
    // added points
    let ans = k;

    for(let l = 0; l < n - 1; l++)
        for(let r = l; r < n; r++)

            // Check if the number of points that
            // need to be placed between these two
            // initial ones is not greater than k
            if ((arr[r] - arr[l]) - (r - l) <= k)
                ans = Math.max(ans, r - l + k + 1);

    return (ans);
}

// Driver code
let arr = [ 1, 2, 3, 4, 10, 11, 14, 15 ];
let n = arr.length;
let k = 4;

document.write(maximiseSubset(arr, n, k)); 

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
8
```

**高效方法(时间复杂度–O(N))**

为了优化蛮力，请注意，如果 r 增加，那么 l 也会增加(或者至少保持不变)。我们可以维护两个索引。将 l 和 r 都初始化为 0。然后我们开始增加 r，这样做的时候，在每一步我们增加 l，直到蛮力方法中使用的条件变为真。当 r 到达最后一个索引时，我们停止。

## C++

```
/* C++ program to find the maximum size of subset
   of points that can have consecutive values
   using efficient approach */
#include <bits/stdc++.h>
using namespace std;

int maximiseSubset(int arr[], int n, int k)
{
    // Since we can always enforce the
    // solution to contain all the K added
    // points
    int ans = k;

    int l = 0, r = 0;
    while (r < n) {

        // increment l until the number of points
        // that need to be placed between index l
        // and index r is not greater than k
        while ((arr[r] - arr[l]) - (r - l) > k)
            l++;

        // update the solution as below
        ans = max(ans, r - l + k + 1);

        r++;
    }

    return (ans);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 10, 11, 14, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;
    printf("%d", maximiseSubset(arr, n, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find the maximum size of subset
of points that can have consecutive values
using efficient approach */
import java.util.*;

class GFG
{
    static int maximiseSubset(int[] arr, int n, int k)
    {
        // Since we can always enforce the
        // solution to contain all the K added
        // points
        int ans = k;

        int l = 0, r = 0;
        while (r < n) {

            // increment l until the number of points
            // that need to be placed between index l
            // and index r is not greater than k
            while ((arr[r] - arr[l]) - (r - l) > k)
                l++;

            // update the solution as below
            ans = Math.max(ans, r - l + k + 1);

            r++;
        }

        return (ans);
    }

    // Driver code 
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 4, 10, 11, 14, 15 };
        int n = arr.length;
        int k = 4;
        System.out.println(maximiseSubset(arr, n, k));
    }
}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python 3 program to find the maximum size
# of subset of points that can have consecutive
# values using efficient approach
def maximiseSubset(arr, n, k):

    # Since we can always enforce the solution
    # to contain all the K added points
    ans = k;

    l = 0; r = 0;
    while (r < n):

        # increment l until the number of points
        # that need to be placed between index l
        # and index r is not greater than k
        while ((arr[r] - arr[l]) - (r - l) > k):
            l = l + 1;

        # update the solution as below
        ans = max(ans, r - l + k + 1);

        r = r + 1;

    return (ans);

# Driver code
arr = [ 1, 2, 3, 4, 10, 11, 14, 15 ];
n = len(arr);
k = 4;
print(maximiseSubset(arr, n, k));

# This code is contributed
# by Akanksha Rai
```

## C#

```
/* C# program to find the
maximum size of subset
of points that can have
consecutive values using
efficient approach */
using System;

class GFG
{
    static int maximiseSubset(int[] arr,
                              int n, int k)
    {
        // Since we can always enforce
        // the solution to contain all
        // the K added points
        int ans = k;

        int l = 0, r = 0;
        while (r < n)
        {

            // increment l until the
            // number of points that
            // need to be placed
            // between index l and
            // index r is not greater
            // than k
            while ((arr[r] - arr[l]) -
                        (r - l) > k)
                l++;

            // update the
            // solution as below
            ans = Math.Max(ans, r - l +
                                k + 1);

            r++;
        }

        return (ans);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = {1, 2, 3, 4,
                    10, 11, 14, 15};
        int n = arr.Length;
        int k = 4;
        Console.WriteLine(maximiseSubset(arr, n, k));
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum size
// of subset of points that can have
// consecutive values using efficient approach
function maximiseSubset($arr, $n, $k)
{
    // Since we can always enforce the
    // solution to contain all the K
    // added points
    $ans = $k;

    $l = 0; $r = 0;
    while ($r < $n)
    {

        // increment l until the number of points
        // that need to be placed between index l
        // and index r is not greater than k
        while (($arr[$r] - $arr[$l]) -
               ($r - $l) > $k)
            $l++;

        // update the solution as below
        $ans = max($ans, $r - $l + $k + 1);

        $r++;
    }

    return ($ans);
}

// Driver code
$arr = array(1, 2, 3, 4, 10, 11, 14, 15 );
$n = sizeof($arr);
$k = 4;
echo(maximiseSubset($arr, $n, $k));

// This code is contributed by Mukul Singh
?>
```

## java 描述语言

```
<script>
/* Javascript program to find the maximum size of subset
of points that can have consecutive values
using efficient approach */

    function maximiseSubset(arr,n,k)
    {
        // Since we can always enforce the
        // solution to contain all the K added
        // points
        let ans = k;

        let l = 0, r = 0;
        while (r < n) {

            // increment l until the number of points
            // that need to be placed between index l
            // and index r is not greater than k
            while ((arr[r] - arr[l]) - (r - l) > k)
                l++;

            // update the solution as below
            ans = Math.max(ans, r - l + k + 1);

            r++;
        }

        return (ans);
    }

    // Driver code
    let arr=[1, 2, 3, 4, 10, 11, 14, 15 ];
    let n = arr.length;
    let k = 4;
    document.write(maximiseSubset(arr, n, k));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
8
```

**时间复杂度:** O(N)

本文由 [**Divyanshu_Gupta**](https://auth.geeksforgeeks.org/profile.php?user=Divyanshu_Gupta) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
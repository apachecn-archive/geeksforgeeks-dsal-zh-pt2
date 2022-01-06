# 所有 K 大小子集的最大值和最小值之间的最小差值

> 原文:[https://www . geesforgeks . org/mini-difference-max-min-k-size-subset/](https://www.geeksforgeeks.org/minimum-difference-max-min-k-size-subsets/)

给定一个整数值数组，我们需要找到所有可能的 K 长度子集的最大值和最小值之间的最小差。

**示例:**

```
Input : arr[] = [3, 5, 100, 101, 102]
        K = 3
Output : 2

Explanation : Possible subsets of K-length with
their differences are,
[3 5 100]  max min diff is (100 - 3) = 97
[3 5 101]  max min diff is (101 - 3) = 98
[3 5 102]  max min diff is (102 - 3) = 99
[3 100 101]  max min diff is (101 - 3) = 98
[3 100 102]  max min diff is (102 - 3) = 99
[3 101 102]  max min diff is (102 - 3) = 98
[5 100 101]  max min diff is (101 - 5) = 96
[5 100 102]  max min diff is (102 - 5) = 97
[5 101 102]  max min diff is (102 - 5) = 97
[100 101 102] max min diff is (102 - 100) = 2
As the minimum difference is 2, it should 
be the answer for given array.

Input : arr[] = {5, 1, 10, 6}
        k = 2
Output : 1

We get the above result considering subset
{5, 6}
```

一旦我们对给定的数组进行排序，我们就可以通过观察结果子集总是连续的这一事实来解决这个问题，而无需迭代所有可能的子集。原因是排序将价值方面的紧密元素聚集在一起。
我们可以如下证明上述事实——假设我们选择了 a1、a2、a3 … aK 这些按递增顺序排列但不连续的数，那么我们的差将是(aK–a1)，但是如果我们包括之前没有取的数(让 aR)，那么我们的 K 长度子集将是 a2、a3、… aR、…。aK。在这种情况下，我们的差异将(Ak–a2)小于(Ak–a1)，因为 a2 > a1。所以我们可以说包含我们答案的子集在排序数组中总是连续的。
从上面的事实开始，为了解决这个问题，我们首先对数组进行排序，然后我们将迭代第一个(N–K)元素，每次我们将取相距 K 的元素之间的差，我们的最终答案将是它们中的最小值。

## C++

```
// C++ program to find minimum difference
// between max and min of all subset of K size
#include <bits/stdc++.h>

using namespace std;

// returns min difference between max
// and min of any K-size subset
int minDifferenceAmongMaxMin(int arr[], int N, int K)
{
    // sort the array so that close
    // elements come together.
    sort(arr, arr + N);

    // initialize result by a big integer number
    int res = INT_MAX;

    // loop over first (N - K) elements
    // of the array only
    for (int i = 0; i <= (N - K); i++)
    {
        // get difference between max and
        // min of current K-sized segment
        int curSeqDiff = arr[i + K - 1] - arr[i];
        res = min(res, curSeqDiff);
    }

    return res;
}

// Driver code
int main()
    {
        int arr[] = {10, 20, 30, 100, 101, 102};
        int N = sizeof(arr) / sizeof(arr[0]);

        int K = 3;
         cout << minDifferenceAmongMaxMin(arr, N, K);
        return 0;
    }
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum difference
// between max and min of all subset of
// K size
import java.util.Arrays;

class GFG
{

    // returns min difference between max
    // and min of any K-size subset
    static int minDifferenceAmongMaxMin(int arr[],
                                    int N, int K)
    {

        // sort the array so that close
        // elements come together.
        Arrays.sort(arr);

        // initialize result by
        // a big integer number
        int res = 2147483647;

        // loop over first (N - K) elements
        // of the array only
        for (int i = 0; i <= (N - K); i++)
        {

            // get difference between max and
            // min of current K-sized segment
            int curSeqDiff = arr[i + K - 1] - arr[i];
            res = Math.min(res, curSeqDiff);
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {10, 20, 30, 100, 101, 102};
        int N = arr.length;

        int K = 3;
        System.out.print(
            minDifferenceAmongMaxMin(arr, N, K));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find minimum
# difference between max and min
# of all subset of K size

# Returns min difference between max
# and min of any K-size subset
def minDifferenceAmongMaxMin(arr, N, K):

    # sort the array so that close
    # elements come together.
    arr.sort()

    # initialize result by a
    # big integer number
    res = 2147483647

    # loop over first (N - K) elements
    # of the array only
    for i in range((N - K) + 1):

        # get difference between max and min
        # of current K-sized segment
        curSeqDiff = arr[i + K - 1] - arr[i]
        res = min(res, curSeqDiff)

    return res

# Driver Code
arr = [10, 20, 30, 100, 101, 102]
N = len(arr)
K = 3
print(minDifferenceAmongMaxMin(arr, N, K))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find minimum difference
// between max and min of all subset of
// K size
using System;

class GFG
{

    // returns min difference between max
    // and min of any K-size subset
    static int minDifferenceAmongMaxMin(int []arr,
                                    int N, int K)
    {

        // sort the array so that close
        // elements come together.
        Array.Sort(arr);

        // initialize result by
        // a big integer number
        int res = 2147483647;

        // loop over first (N - K) elements
        // of the array only
        for (int i = 0; i <= (N - K); i++)
        {

            // get difference between max and
            // min of current K-sized segment
            int curSeqDiff = arr[i + K - 1] - arr[i];
            res = Math.Min(res, curSeqDiff);
        }

        return res;
    }

    // Driver code
    public static void Main()
    {
        int []arr= {10, 20, 30, 100, 101, 102};
        int N = arr.Length;

        int K = 3;
    Console.Write(
            minDifferenceAmongMaxMin(arr, N, K));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum difference
// between max and min of all subset
// of K size

// returns min difference between max
// and min of any K-size subset
function minDifferenceAmongMaxMin($arr, $N,
                                        $K)
{
    $INT_MAX = 2;

    // sort the array so that close
    // elements come together.
    sort($arr); sort($arr , $N);

    // initialize result by a
    // big integer number
    $res = $INT_MAX;

    // loop over first (N - K) elements
    // of the array only
    for ($i = 0; $i <= ($N - $K); $i++)
    {

        // get difference between max and
        // min of current K-sized segment
        $curSeqDiff = $arr[$i + $K - 1] -
                               $arr[$i];
        $res = min($res, $curSeqDiff);
    }

    return $res;
}

    // Driver Code
    $arr = array(10, 20, 30, 100, 101, 102);
    $N = sizeof($arr);

    $K = 3;
    echo minDifferenceAmongMaxMin($arr, $N, $K);

// This code is contributed by Nitin Mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum difference
// between max and min of all subset of
// K size

    // returns min difference between max
    // and min of any K-size subset
    function minDifferenceAmongMaxMin(arr, N, K)
    {

        // sort the array so that close
        // elements come together.
        arr.sort((a, b) => a - b);

        // initialize result by
        // a big integer number
        let res = 2147483647;

        // loop over first (N - K) elements
        // of the array only
        for (let i = 0; i <= (N - K); i++)
        {

            // get difference between max and
            // min of current K-sized segment
            let curSeqDiff = arr[i + K - 1] - arr[i];
            res = Math.min(res, curSeqDiff);
        }

        return res;
    }

// Driver Code

     let arr = [10, 20, 30, 100, 101, 102];
        let N = arr.length;

        let K = 3;
        document.write(
            minDifferenceAmongMaxMin(arr, N, K));

</script>
```

**输出:**

```
2
```

时间复杂度:0(对数 n)

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
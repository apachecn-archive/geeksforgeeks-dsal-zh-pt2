# 特定差异对的最大和

> 原文:[https://www . geesforgeks . org/maximum-sum-pairs-specific-difference/](https://www.geeksforgeeks.org/maximum-sum-pairs-specific-difference/)

给定一个整数数组和一个数 k，如果数组中的两个数之间的差严格小于 k，我们可以对它们进行配对，任务是找到不相交对的最大可能和。P 对的和是所有对的 2P 数的和。

**示例:**

> **输入:** arr[] = {3，5，10，15，17，12，9}，K = 4
> **输出:** 62
> **解释:**
> 那么差小于 K 的不相交对是，(3，5)，(10，12)，(15，17)
> 所以我们能得到的最大和是 3 + 5 + 12 + 10 + 15 + 17 = 62
> 注意一种交替的形成方式
> 
> **输入:** arr[] = {5，15，10，300}，k = 12
> T3】输出: 25

**方法:**
首先，我们按照递增的顺序对给定的数组进行排序。一旦数组被排序，我们遍历数组。对于每个元素，我们首先尝试将其与其前一个元素配对。为什么我们更喜欢前面的元素？Let arr[i]可以与 arr[i-1]和 arr[i-2]配对(即 arr[I]–arr[I-1]<K 和 arr[i]-arr[i-2] < K)。由于数组是排序的，arr[i-1]的值将大于 arr[i-2]。另外，我们需要用小于 k 的差配对，这意味着如果 arr[i-2]可以配对，那么 arr[i-1]也可以在排序数组中配对。
现在观察上述事实，我们可以将我们的动态规划解公式化如下，
让 dp[i]表示我们使用数组的前 I 个元素可以实现的最大不相交对和。假设现在，我们在第一个位置，那么我们有两种可能。

```
  Pair up i with (i-1)th element, i.e. 
      dp[i] = dp[i-2] + arr[i] + arr[i-1]
  Don't pair up, i.e. 
      dp[i] = dp[i-1] 
```

上述迭代需要 O(N)个时间，数组排序需要 O(N log N)个时间，因此解决方案的总时间复杂度为 O(N log N)

## C++

```
// C++ program to find maximum pair sum whose
// difference is less than K
#include <bits/stdc++.h>
using namespace std;

// method to return maximum sum we can get by
// finding less than K difference pair
int maxSumPairWithDifferenceLessThanK(int arr[], int N, int K)
{
    // Sort input array in ascending order.
    sort(arr, arr+N);

    // dp[i] denotes the maximum disjoint pair sum
    // we can achieve using first i elements
    int dp[N];

    //  if no element then dp value will be 0
    dp[0] = 0;

    for (int i = 1; i < N; i++)
    {
        // first give previous value to dp[i] i.e.
        // no pairing with (i-1)th element
        dp[i] = dp[i-1];

        // if current and previous element can form a pair
        if (arr[i] - arr[i-1] < K)
        {
            // update dp[i] by choosing maximum between
            // pairing and not pairing
            if (i >= 2)
                dp[i] = max(dp[i], dp[i-2] + arr[i] + arr[i-1]);
            else
                dp[i] = max(dp[i], arr[i] + arr[i-1]);
        }
    }

    //  last index will have the result
    return dp[N - 1];
}

//  Driver code to test above methods
int main()
{
    int arr[] = {3, 5, 10, 15, 17, 12, 9};
    int N = sizeof(arr)/sizeof(int);

    int K = 4;
    cout << maxSumPairWithDifferenceLessThanK(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum pair sum whose
// difference is less than K

import java.io.*;
import java.util.*;

class GFG {

    // method to return maximum sum we can get by
    // finding less than K difference pair
    static int maxSumPairWithDifferenceLessThanK(int arr[],
                                               int N, int K)
    {

        // Sort input array in ascending order.
        Arrays.sort(arr);

        // dp[i] denotes the maximum disjoint pair sum
        // we can achieve using first i elements
        int dp[] = new int[N];

        // if no element then dp value will be 0
        dp[0] = 0;

        for (int i = 1; i < N; i++)
        {
            // first give previous value to dp[i] i.e.
            // no pairing with (i-1)th element
            dp[i] = dp[i-1];

            // if current and previous element can form a pair
            if (arr[i] - arr[i-1] < K)
            {

                // update dp[i] by choosing maximum between
                // pairing and not pairing
                if (i >= 2)
                    dp[i] = Math.max(dp[i], dp[i-2] + arr[i] +
                                                    arr[i-1]);
                else
                    dp[i] = Math.max(dp[i], arr[i] + arr[i-1]);
            }
        }

        // last index will have the result
        return dp[N - 1];
    }

    // Driver code to test above methods
    public static void main (String[] args) {

        int arr[] = {3, 5, 10, 15, 17, 12, 9};
        int N = arr.length;
        int K = 4;

        System.out.println ( maxSumPairWithDifferenceLessThanK(
                                                    arr, N, K));

    }
}

//This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find maximum pair
# sum whose difference is less than K

# method to return maximum sum we can
# get by get by finding less than K
# difference pair
def maxSumPairWithDifferenceLessThanK(arr, N, K):

    # Sort input array in ascending order.
    arr.sort()

    # dp[i] denotes the maximum disjoint
    # pair sum we can achieve using first
    # i elements
    dp = [0] * N

    # if no element then dp value will be 0
    dp[0] = 0

    for i in range(1, N):

        # first give previous value to
        # dp[i] i.e. no pairing with
        # (i-1)th element
        dp[i] = dp[i-1]

        # if current and previous element
        # can form a pair
        if (arr[i] - arr[i-1] < K):

            # update dp[i] by choosing
            # maximum between pairing
            # and not pairing
            if (i >= 2):
                dp[i] = max(dp[i], dp[i-2] + arr[i] + arr[i-1]);
            else:
                dp[i] = max(dp[i], arr[i] + arr[i-1]);

    # last index will have the result
    return dp[N - 1]

# Driver code to test above methods
arr = [3, 5, 10, 15, 17, 12, 9]
N = len(arr)
K = 4
print(maxSumPairWithDifferenceLessThanK(arr, N, K))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find maximum pair sum whose
// difference is less than K
using System;

class GFG {

    // method to return maximum sum we can get by
    // finding less than K difference pair
    static int maxSumPairWithDifferenceLessThanK(int []arr,
                                              int N, int K)
    {

        // Sort input array in ascending order.
        Array.Sort(arr);

        // dp[i] denotes the maximum disjoint pair sum
        // we can achieve using first i elements
        int []dp = new int[N];

        // if no element then dp value will be 0
        dp[0] = 0;

        for (int i = 1; i < N; i++)
        {
            // first give previous value to dp[i] i.e.
            // no pairing with (i-1)th element
            dp[i] = dp[i-1];

            // if current and previous element can form
            // a pair
            if (arr[i] - arr[i-1] < K)
            {

                // update dp[i] by choosing maximum
                // between pairing and not pairing
                if (i >= 2)
                    dp[i] = Math.Max(dp[i], dp[i-2]
                                + arr[i] + arr[i-1]);
                else
                    dp[i] = Math.Max(dp[i], arr[i]
                                        + arr[i-1]);
            }
        }

        // last index will have the result
        return dp[N - 1];
    }

    // Driver code to test above methods
    public static void Main () {

        int []arr = {3, 5, 10, 15, 17, 12, 9};
        int N = arr.Length;
        int K = 4;

        Console.WriteLine(
          maxSumPairWithDifferenceLessThanK(arr, N, K));

    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to find maximum pair sum whose
// difference is less than K

// method to return maximum sum we can get by
// finding less than K difference pair
function maxSumPairWithDifferenceLessThanK($arr, $N, $K)
{
    // Sort input array in ascending order.
    sort($arr) ;

    // dp[i] denotes the maximum disjoint pair sum
    // we can achieve using first i elements
    $dp = array() ;

    // if no element then dp value will be 0
    $dp[0] = 0;

    for ($i = 1; $i < $N; $i++)
    {
        // first give previous value to dp[i] i.e.
        // no pairing with (i-1)th element
        $dp[$i] = $dp[$i-1];

        // if current and previous element can form a pair
        if ($arr[$i] - $arr[$i-1] < $K)
        {
            // update dp[i] by choosing maximum between
            // pairing and not pairing
            if ($i >= 2)
                $dp[$i] = max($dp[$i], $dp[$i-2] + $arr[$i] + $arr[$i-1]);
            else
                $dp[$i] = max($dp[$i], $arr[$i] + $arr[$i-1]);
        }
    }

    // last index will have the result
    return $dp[$N - 1];
}

    // Driver code

    $arr = array(3, 5, 10, 15, 17, 12, 9);
    $N = sizeof($arr) ;

    $K = 4;
    echo maxSumPairWithDifferenceLessThanK($arr, $N, $K);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum pair sum whose
// difference is less than K

    // method to return maximum sum we can get by
    // finding less than K difference pair
    function maxSumPairWithDifferenceLessThanK(arr,
                                               N, K)
    {

        // Sort input array in ascending order.
        arr.sort();

        // dp[i] denotes the maximum disjoint pair sum
        // we can achieve using first i elements
        let dp = [];

        // if no element then dp value will be 0
        dp[0] = 0;

        for (let i = 1; i < N; i++)
        {
            // first give previous value to dp[i] i.e.
            // no pairing with (i-1)th element
            dp[i] = dp[i-1];

            // if current and previous element can form a pair
            if (arr[i] - arr[i-1] < K)
            {

                // update dp[i] by choosing maximum between
                // pairing and not pairing
                if (i >= 2)
                    dp[i] = Math.max(dp[i], dp[i-2] + arr[i] +
                                                    arr[i-1]);
                else
                    dp[i] = Math.max(dp[i], arr[i] + arr[i-1]);
            }
        }

        // last index will have the result
        return dp[N - 1];
    }

// Driver code to test above methods

        let arr = [3, 5, 10, 15, 17, 12, 9];
        let N = arr.length;
        let K = 4;

        document.write( maxSumPairWithDifferenceLessThanK(
                                                    arr, N, K));
// This code is contributed by avijitmondal1998.
</script>
```

**Output**

```
62
```

***时间复杂度:** O(N Log N)*
***辅助空间:** O(N)*

Amit Sane 提供的优化解决方案如下所示:

## C++

```
// C++ program to find maximum pair sum whose
// difference is less than K
#include <bits/stdc++.h>
using namespace std;

// Method to return maximum sum we can get by
// finding less than K difference pairs
int maxSumPair(int arr[], int N, int k)
{
    int maxSum = 0;

    // Sort elements to ensure every i and i-1 is closest
    // possible pair
    sort(arr, arr + N);

    // To get maximum possible sum,
    // iterate from largest to
    // smallest, giving larger
    // numbers priority over smaller
    // numbers.
    for (int i = N - 1; i > 0; --i)
    {
        // Case I: Diff of arr[i] and arr[i-1]
        //  is less then K,add to maxSum      
        // Case II: Diff between arr[i] and arr[i-1] is not
        // less then K, move to next i since with
        // sorting we know, arr[i]-arr[i-1] <
        // rr[i]-arr[i-2] and so on.
        if (arr[i] - arr[i - 1] < k)
        {
            // Assuming only positive numbers.
            maxSum += arr[i];
            maxSum += arr[i - 1];

            // When a match is found skip this pair
            --i;
        }
    }

    return maxSum;
}

// Driver code
int main()
{
    int arr[] = { 3, 5, 10, 15, 17, 12, 9 };
    int N = sizeof(arr) / sizeof(int);

    int K = 4;
    cout << maxSumPair(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum pair sum whose
// difference is less than K

import java.io.*;
import java.util.*;

class GFG {

    // Method to return maximum sum we can get by
    // finding less than K difference pairs
    static int maxSumPairWithDifferenceLessThanK(int arr[],
                                                 int N,
                                                 int k)
    {
        int maxSum = 0;

        // Sort elements to ensure every i and i-1 is
        // closest possible pair
        Arrays.sort(arr);

        // To get maximum possible sum,
        // iterate from largest
        // to smallest, giving larger
        // numbers priority over
        // smaller numbers.
        for (int i = N - 1; i > 0; --i)
        {
            // Case I: Diff of arr[i] and arr[i-1] is less
            // then K, add to maxSum
            // Case II: Diff between arr[i] and arr[i-1] is
            // not less then K, move to next i
            // since with sorting we know, arr[i]-arr[i-1] <
            // arr[i]-arr[i-2] and so on.
            if (arr[i] - arr[i - 1] < k)
            {
                // Assuming only positive numbers.
                maxSum += arr[i];
                maxSum += arr[i - 1];

                // When a match is found skip this pair
                --i;
            }
        }

        return maxSum;
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 3, 5, 10, 15, 17, 12, 9 };
        int N = arr.length;
        int K = 4;

        System.out.println(
            maxSumPairWithDifferenceLessThanK(arr, N, K));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find maximum pair sum
# whose difference is less than K

# Method to return maximum sum we can
# get by finding less than K difference
# pairs

def maxSumPairWithDifferenceLessThanK(arr, N, k):

    maxSum = 0

    # Sort elements to ensure every i and
    # i-1 is closest possible pair
    arr.sort()

    # To get maximum possible sum, iterate
    # from largest to smallest, giving larger
    # numbers priority over smaller numbers.
    i = N - 1
    while (i > 0):

        # Case I: Diff of arr[i] and arr[i-1]
        #     is less then K, add to maxSum
        # Case II: Diff between arr[i] and
        #     arr[i-1] is not less then K,
        #     move to next i since with sorting
        #     we know, arr[i]-arr[i-1] < arr[i]-arr[i-2]
        #     and so on.
        if (arr[i] - arr[i - 1] < k):

            # Assuming only positive numbers.
            maxSum += arr[i]
            maxSum += arr[i - 1]

            # When a match is found skip this pair
            i -= 1
        i -= 1

    return maxSum

# Driver Code
arr = [3, 5, 10, 15, 17, 12, 9]
N = len(arr)

K = 4
print(maxSumPairWithDifferenceLessThanK(arr, N, K))

# This code is contributed by mits
```

## C#

```
// C# program to find maximum pair sum whose
// difference is less than K
using System;
class GFG {

    // Method to return maximum sum we can get by
    // finding less than K difference pairs
    static int maxSumPairWithDifferenceLessThanK(int []arr,
                                               int N, int k)
    {
        int maxSum = 0;

        // Sort elements to ensure
        // every i and i-1 is closest
        // possible pair
        Array.Sort(arr);

        // To get maximum possible sum,
        // iterate from largest
        // to smallest, giving larger
        // numbers priority over
        // smaller numbers.
        for (int i = N-1; i > 0; --i)
        {

            /* Case I: Diff of arr[i] and
                       arr[i-1] is less then K,
                       add to maxSum
               Case II: Diff between arr[i] and
                        arr[i-1] is not less
                        then K, move to next i
                        since with sorting we
                        know, arr[i]-arr[i-1] <
                        arr[i]-arr[i-2] and
                        so on.*/
            if (arr[i] - arr[i-1] < k)
            {

                // Assuming only positive numbers.
                maxSum += arr[i];
                maxSum += arr[i - 1];

                // When a match is found
                // skip this pair
                --i;
            }
        }

        return maxSum;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {3, 5, 10, 15, 17, 12, 9};
        int N = arr.Length;
        int K = 4;

        Console.Write( maxSumPairWithDifferenceLessThanK(arr,
                                                         N, K));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum pair sum 
// whose difference is less than K

// Method to return maximum sum we can 
// get by finding less than K difference
// pairs
function maxSumPairWithDifferenceLessThanK($arr, $N, $k)
{
    $maxSum = 0;

    // Sort elements to ensure every i and
    // i-1 is closest possible pair
    sort($arr);

    // To get maximum possible sum, iterate
    // from largest to smallest, giving larger
    // numbers priority over smaller numbers.
    for ($i = $N - 1; $i > 0; --$i)
    {
        // Case I: Diff of arr[i] and arr[i-1]
        //           is less then K, add to maxSum
        // Case II: Diff between arr[i] and
        //            arr[i-1] is not less then K,
        //          move to next i since with sorting
        //          we know, arr[i]-arr[i-1] < arr[i]-arr[i-2]
        //            and so on.
        if ($arr[$i] - $arr[$i - 1] < $k)
        {
            // Assuming only positive numbers.
            $maxSum += $arr[$i];
            $maxSum += $arr[$i - 1];

            // When a match is found skip this pair
            --$i;
        }
    }

    return $maxSum;
}

// Driver Code
$arr = array(3, 5, 10, 15, 17, 12, 9);
$N = sizeof($arr);

$K = 4;
echo maxSumPairWithDifferenceLessThanK($arr, $N, $K);

// This code is contributed
// by Sach_Code   
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// maximum pair sum whose
// difference is less than K
// Method to return maximum sum we can get by
// finding less than K difference pairs
function maxSumPairWithDifferenceLessThanK(arr, N, k)
{
    var maxSum = 0;

    // Sort elements to ensure every i and i-1 is
    // closest possible pair
    arr.sort((a,b)=>a-b);

    // To get maximum possible sum,
    // iterate from largest
    // to smallest, giving larger
    // numbers priority over
    // smaller numbers.
    for (i = N - 1; i > 0; --i)
    {
        // Case I: Diff of arr[i] and arr[i-1] is less
        // then K, add to maxSum
        // Case II: Diff between arr[i] and arr[i-1] is
        // not less then K, move to next i
        // since with sorting we know, arr[i]-arr[i-1] <
        // arr[i]-arr[i-2] and so on.
        if (arr[i] - arr[i - 1] < k)
        {
            // Assuming only positive numbers.
            maxSum += arr[i];
            maxSum += arr[i - 1];

            // When a match is found skip this pair
            --i;
        }
    }

    return maxSum;
}

// Driver code
var arr = [ 3, 5, 10, 15, 17, 12, 9 ];
var N = arr.length;
var K = 4;

document.write(maxSumPairWithDifferenceLessThanK(arr, N, K));

// This code is contributed by 29AjayKumar

</script>
```

**Output**

```
62
```

***时间复杂度:** O(N Log N)*
***辅助空间:** O(1)*

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
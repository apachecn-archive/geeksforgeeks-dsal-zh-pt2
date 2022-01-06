# k 次更新可以相等的最大元素数

> 原文:[https://www . geesforgeks . org/max-elements-can-make-equal-k-updates/](https://www.geeksforgeeks.org/maximum-elements-can-made-equal-k-updates/)

给定一个数组和值 k。我们必须找到该数组可能的最大相等元素数，这样我们就可以通过增加最多 k 的总数来增加数组的元素数。
**示例:**

> **输入:**数组= { 2，4，9 }，k = 3
> **输出:** 2
> 我们最多可以做三个增量。我们可以用 2 乘以 2 得到两个元素 4。请注意，我们不能将两个元素设为 9，因为将 4 转换为 9 需要 5 个增量。
> **输入:**数组= { 5，5，3，1 }，k = 5
> **输出:** 3
> **说明:**这里第 1 个和第 2 个元素相等。然后我们可以将第三个元素 3 增加到 5。然后 k 变成(k-2) = 3。现在我们不能增加 1 到 5，因为 k 值是 3，上升需要 4。因此相等的元素可能是 3。这里我们也可以增加 1 到 5。然后我们还有 3，因为我们不能更新 3 到 5。
> **输入:**数组= { 5，5，3，1 }，k = 6
> **输出:** 4

**天真方法:**在天真方法中，我们在 **O(n^2)** 时间中有一个算法，在该算法中，我们检查每个元素有多少其他元素可以增加，以便它们将变得与它们相等。
**高效方法:**在这种方法中，首先我们将对数组进行排序。然后我们维护两个数组。首先是前缀和数组，它存储数组的前缀和，另一个是 maxx[]数组，它存储直到每一点找到的最大元素，即 max[i]表示从 1 到 I 的最大元素。在前缀[]数组和 maxx[]数组中存储这些值后，我们进行从 1 到 n(数组的元素数)的二分搜索法运算，以计算可以增加多少个元素使它们相等。在二分搜索法中，我们使用一个函数，在这个函数中，我们确定*元素的数量可以增加多少，使它们等于一个值*。

## C++

```
// C++ program to find maximum elements that can
// be made equal with k updates
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the maximum number of
// equal elements possible with atmost K increment
// of values .Here we have done sliding window
// to determine that whether there are x number of
// elements present which on increment will become
// equal. The loop here will run in fashion like
// 0...x-1, 1...x, 2...x+1, ...., n-x-1...n-1
bool ElementsCalculationFunc(int pre[], int maxx[],
                               int x, int k, int n)
{
    for (int i = 0, j = x; j <= n; j++, i++) {

        // It can be explained with the reasoning
        // that if for some x number of elements
        // we can update the values then the
        // increment to the segment (i to j having
        // length -> x) so that all will be equal is
        // (x*maxx[j]) this is the total sum of
        // segment and (pre[j]-pre[i]) is present sum
        // So difference of them should be less than k
        // if yes, then that segment length(x) can be
        // possible return true
        if (x * maxx[j] - (pre[j] - pre[i]) <= k)
            return true;
    }
    return false;
}

void MaxNumberOfElements(int a[], int n, int k)
{
    // sort the array in ascending order
    sort(a, a + n);
    int pre[n + 1]; // prefix sum array
    int maxx[n + 1]; // maximum value array

    // Initializing the prefix array
    // and maximum array
    for (int i = 0; i <= n; ++i) {
        pre[i] = 0;
        maxx[i] = 0;
    }

    for (int i = 1; i <= n; i++) {

        // Calculating prefix sum of the array
        pre[i] = pre[i - 1] + a[i - 1];

        // Calculating max value upto that position
        // in the array
        maxx[i] = max(maxx[i - 1], a[i - 1]);
    }

    // Binary search applied for
    // computation here
    int l = 1, r = n, ans;
    while (l < r) {
        int mid = (l + r) / 2;

        if (ElementsCalculationFunc(pre, maxx,
                              mid - 1, k, n)) {
            ans = mid;
            l = mid + 1;
        }
        else
            r = mid - 1;
    }

    // printing result
    cout << ans << "\n";
}

int main()
{
    int arr[] = { 2, 4, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    MaxNumberOfElements(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find maximum elements that can
// be made equal with k updates

import java.util.Arrays;
public class GFG {

    // Function to calculate the maximum number of
    // equal elements possible with atmost K increment
    // of values .Here we have done sliding window
    // to determine that whether there are x number of
    // elements present which on increment will become
    // equal. The loop here will run in fashion like
    // 0...x-1, 1...x, 2...x+1, ...., n-x-1...n-1
    static boolean ElementsCalculationFunc(int pre[],
                      int maxx[], int x, int k, int n)
    {
        for (int i = 0, j = x; j <= n; j++, i++) {

            // It can be explained with the reasoning
            // that if for some x number of elements
            // we can update the values then the
            // increment to the segment (i to j having
            // length -> x) so that all will be equal is
            // (x*maxx[j]) this is the total sum of
            // segment and (pre[j]-pre[i]) is present sum
            // So difference of them should be less than k
            // if yes, then that segment length(x) can be
            // possible return true
            if (x * maxx[j] - (pre[j] - pre[i]) <= k)
                return true;
        }
        return false;
    }

    static void MaxNumberOfElements(int a[], int n, int k)
    {
        // sort the array in ascending order
        Arrays.sort(a);
        int []pre = new int[n + 1]; // prefix sum array
        int []maxx = new int[n + 1]; // maximum value array

        // Initializing the prefix array
        // and maximum array
        for (int i = 0; i <= n; ++i) {
            pre[i] = 0;
            maxx[i] = 0;
        }

        for (int i = 1; i <= n; i++) {

            // Calculating prefix sum of the array
            pre[i] = pre[i - 1] + a[i - 1];

            // Calculating max value upto that position
            // in the array
            maxx[i] = Math.max(maxx[i - 1], a[i - 1]);
        }

        // Binary search applied for
        // computation here
        int l = 1, r = n, ans=0;
        while (l < r) {

            int mid = (l + r) / 2;

            if (ElementsCalculationFunc(pre, maxx,
                                   mid - 1, k, n))
            {
                ans = mid;
                l = mid + 1;
            }
            else
                r = mid - 1;
        }

        // printing result
        System.out.print((int)ans + "\n");
    }

    public static void main(String args[]) {

        int arr[] = { 2, 4, 9 };
        int n = arr.length;
        int k = 3;

        MaxNumberOfElements(arr, n, k);

    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to find maximum elements
# that can be made equal with k updates

# Function to calculate the maximum number of
# equal elements possible with atmost K increment
# of values .Here we have done sliding window
# to determine that whether there are x number of
# elements present which on increment will become
# equal. The loop here will run in fashion like
# 0...x-1, 1...x, 2...x+1, ...., n-x-1...n-1
def ElementsCalculationFunc(pre, maxx,
                            x, k, n):

    i = 0
    j = x
    while j <= n:

        # It can be explained with the reasoning
        # that if for some x number of elements
        # we can update the values then the
        # increment to the segment (i to j having
        # length -> x) so that all will be equal is
        # (x*maxx[j]) this is the total sum of
        # segment and (pre[j]-pre[i]) is present sum
        # So difference of them should be less than k
        # if yes, then that segment length(x) can be
        # possible return true
        if (x * maxx[j] - (pre[j] - pre[i]) <= k):
            return True

        i += 1
        j += 1

    return False

def MaxNumberOfElements( a, n, k):

    # sort the array in ascending order
    a.sort()
    pre = [0] * (n + 1) # prefix sum array
    maxx = [0] * (n + 1) # maximum value array

    # Initializing the prefix array
    # and maximum array
    for i in range (n + 1):
        pre[i] = 0
        maxx[i] = 0

    for i in range(1, n+1):

        # Calculating prefix sum of the array
        pre[i] = pre[i - 1] + a[i - 1]

        # Calculating max value upto that
        # position in the array
        maxx[i] = max(maxx[i - 1], a[i - 1])

    # Binary search applied for
    # computation here
    l = 1
    r = n
    while (l < r) :
        mid = (l + r) // 2

        if (ElementsCalculationFunc(pre, maxx,
                                    mid - 1, k, n)):
            ans = mid
            l = mid + 1

        else:
            r = mid - 1

    # printing result
    print (ans)

# Driver Code
if __name__ == "__main__":

    arr = [2, 4, 9 ]
    n = len(arr)
    k = 3
    MaxNumberOfElements(arr, n, k)

# This code is contributed by Ita_c
```

## C#

```
// C# program to find maximum elements that can
// be made equal with k updates
using System;

class GFG {

    // Function to calculate the maximum number of
    // equal elements possible with atmost K increment
    // of values .Here we have done sliding window
    // to determine that whether there are x number of
    // elements present which on increment will become
    // equal. The loop here will run in fashion like
    // 0...x-1, 1...x, 2...x+1, ...., n-x-1...n-1
    static bool ElementsCalculationFunc(int []pre,
                      int []maxx, int x, int k, int n)
    {
        for (int i = 0, j = x; j <= n; j++, i++) {

            // It can be explained with the reasoning
            // that if for some x number of elements
            // we can update the values then the
            // increment to the segment (i to j having
            // length -> x) so that all will be equal is
            // (x*maxx[j]) this is the total sum of
            // segment and (pre[j]-pre[i]) is present sum
            // So difference of them should be less than k
            // if yes, then that segment length(x) can be
            // possible return true
            if (x * maxx[j] - (pre[j] - pre[i]) <= k)
                return true;
        }
        return false;
    }

    static void MaxNumberOfElements(int []a, int n, int k)
    {
        // sort the array in ascending order
        Array.Sort(a);
        int []pre = new int[n + 1]; // prefix sum array
        int []maxx = new int[n + 1]; // maximum value array

        // Initializing the prefix array
        // and maximum array
        for (int i = 0; i <= n; ++i) {
            pre[i] = 0;
            maxx[i] = 0;
        }

        for (int i = 1; i <= n; i++) {

            // Calculating prefix sum of the array
            pre[i] = pre[i - 1] + a[i - 1];

            // Calculating max value upto that position
            // in the array
            maxx[i] = Math.Max(maxx[i - 1], a[i - 1]);
        }

        // Binary search applied for
        // computation here
        int l = 1, r = n, ans=0;
        while (l < r) {

            int mid = (l + r) / 2;

            if (ElementsCalculationFunc(pre, maxx,
                                   mid - 1, k, n))
            {
                ans = mid;
                l = mid + 1;
            }
            else
                r = mid - 1;
        }

        // printing result
        Console.Write ((int)ans + "\n");
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 4, 9 };
        int n = arr.Length;
        int k = 3;

        MaxNumberOfElements(arr, n, k);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find maximum elements that can
// be made equal with k updates
// Function to calculate the maximum number of
// equal elements possible with atmost K increment
// of values .Here we have done sliding window
// to determine that whether there are x number of
// elements present which on increment will become
// equal. The loop here will run in fashion like
// 0...x-1, 1...x, 2...x+1, ...., n-x-1...n-1
function  ElementsCalculationFunc($pre, $maxx,$x,  $k, $n)
{
    for ( $i = 0, $j = $x; $j <= $n; $j++, $i++) {

        // It can be explained with the reasoning
        // that if for some x number of elements
        // we can update the values then the
        // increment to the segment (i to j having
        // length -> x) so that all will be equal is
        // (x*maxx[j]) this is the total sum of
        // segment and (pre[j]-pre[i]) is present sum
        // So difference of them should be less than k
        // if yes, then that segment length(x) can be
        // possible return true
        if ($x * $maxx[$j] - ($pre[$j] - $pre[$i]) <= $k)
            return true;
    }
    return false;
}

function  MaxNumberOfElements($a, $n, $k)
{
    // sort the array in ascending order
    sort($a);
    $pre[$n + 1]=array(); // prefix sum array
    $maxx[$n + 1]=array(); // maximum value array

    // Initializing the prefix array
    // and maximum array
    for ($i = 0; $i <= $n; ++$i) {
        $pre[$i] = 0;
        $maxx[$i] = 0;
    }

    for ($i = 1; $i <= $n; $i++) {

        // Calculating prefix sum of the array
        $pre[$i] = $pre[$i - 1] + $a[$i - 1];

        // Calculating max value upto that position
        // in the array
        $maxx[$i] = max($maxx[$i - 1], $a[$i - 1]);
    }

    // Binary search applied for
    // computation here
    $l = 1;
    $r = $n;
    $ans;
    while ($l < $r) {
        $mid = ($l + $r) / 2;

        if (ElementsCalculationFunc($pre, $maxx,
                            $mid - 1, $k, $n)) {
            $ans = $mid;
            $l = $mid + 1;
        }
        else
            $r = $mid - 1;
    }

    // printing result
    echo  $ans , "\n";
}
//Code driven
    $arr = array(2, 4, 9 );
    $n = sizeof($arr) / sizeof($arr[0]);
    $k = 3;
    MaxNumberOfElements($arr, $n, $k);

#This code is contributed by akt_mit.
?>
```

## java 描述语言

```
<script>
// javascript program to find maximum elements that can
// be made equal with k updates

    // Function to calculate the maximum number of
    // equal elements possible with atmost K increment
    // of values .Here we have done sliding window
    // to determine that whether there are x number of
    // elements present which on increment will become
    // equal. The loop here will run in fashion like
    // 0...x-1, 1...x, 2...x+1, ...., n-x-1...n-1
    function ElementsCalculationFunc(pre, maxx, x, k, n)
    {
        for (let i = 0, j = x; j <= n; j++, i++)
        {

            // It can be explained with the reasoning
            // that if for some x number of elements
            // we can update the values then the
            // increment to the segment (i to j having
            // length -> x) so that all will be equal is
            // (x*maxx[j]) this is the total sum of
            // segment and (pre[j]-pre[i]) is present sum
            // So difference of them should be less than k
            // if yes, then that segment length(x) can be
            // possible return true
            if (x * maxx[j] - (pre[j] - pre[i]) <= k)
                return true;
        }
        return false;
    }

    function MaxNumberOfElements(a, n, k)
    {

        // sort the array in ascending order
        a.sort(function(a,b){return a-b;});
        let pre = new Array(n + 1); // prefix sum array
        let maxx = new Array(n + 1); // maximum value array

        // Initializing the prefix array
        // and maximum array
        for (let i = 0; i <= n; ++i)
        {
            pre[i] = 0;
            maxx[i] = 0;
        }

        for (let i = 1; i <= n; i++)
        {

            // Calculating prefix sum of the array
            pre[i] = pre[i - 1] + a[i - 1];

            // Calculating max value upto that position
            // in the array
            maxx[i] = Math.max(maxx[i - 1], a[i - 1]);
        }

        // Binary search applied for
        // computation here
        let l = 1, r = n, ans=0;
        while (l < r)
        {

            let mid = Math.floor((l + r) / 2);

            if (ElementsCalculationFunc(pre, maxx,
                                   mid - 1, k, n))
            {
                ans = mid;
                l = mid + 1;
            }
            else
                r = mid - 1;
        }

        // printing result
        document.write(ans + "\n");
    }

    let arr = [2, 4, 9 ];
    let n = arr.length;
    let k = 3;
    MaxNumberOfElements(arr, n, k);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(nlog(n))
T3】空间复杂度: O(n)
# 使数组 GCD 为 k 的倍数的最小运算

> 原文:[https://www . geesforgeks . org/minimum-operations-make-gcd-array-multi-k/](https://www.geeksforgeeks.org/minimum-operations-make-gcd-array-multiple-k/)

给定一个数组和 k，我们需要找到使数组的 GCD 等于或等于 k 的倍数所需的最小操作。这里，操作意味着将数组元素增加或减少 1。

**示例:**

> 输入:a = { 4，5，6 }，k = 5
> 输出:2
> 说明:我们可以将 4 加 1 使其变成 5，将 6 减 1 使其变成 5。因此最小操作将是 2。
> 输入:a = { 4，9，6 }，k = 5
> 输出:3
> 说明:就像前面的例子一样，我们可以把 4 和 6 加 1 减 1，把 9 加 1，这样就变成了 10。现在每个元素都有 GCD 5。因此最小操作将是 3。

这里我们必须使数组的 gcd 等于或等于 k 的倍数，这意味着会有一些元素接近 k 或接近它的倍数的情况。所以，为了解决这个问题，我们只需要使每个数组的值等于或等于 k 的倍数。通过这样做，我们将实现我们的解决方案，就好像每个元素都是 k 的倍数，那么它的 GCD 至少是 k。现在，我们的下一个目标是在最小操作中转换数组元素，即最小数量的增量和减量。这个增量或减量的最小值只能通过从 K 中取每个数的余数来知道，即*要么我们必须取余数值，要么取(K 余数)值，取其中的最小值。*

下面是这种方法的实现:

## C++

```
// CPP program to make GCD of array a multiple
// of k.
#include <bits/stdc++.h>
using namespace std;

int MinOperation(int a[], int n, int k)
{

    int result = 0;

    for (int i = 0; i < n; ++i) {

        // If array value is not 1
        // and it is greater than k
        // then we can increase the
        // or decrease the remainder
        // obtained by dividing k
        // from the ith value of array
        // so that we get the number
        // which is either closer to k
        // or its multiple
        if (a[i] != 1 && a[i] > k) {
            result = result + min(a[i] % k, k - a[i] % k);
        }
        else {

            // Else we only have one choice
            // which is to increment the value
            // to make equal to k
            result = result + k - a[i];
        }
    }

    return result;
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 5;
    cout << MinOperation(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make GCD
// of array a multiple of k.
import java.io.*;

class GFG
{
static int MinOperation(int a[],
                        int n, int k)
{

    int result = 0;

    for (int i = 0; i < n; ++i)
    {

        // If array value is not 1
        // and it is greater than k
        // then we can increase the
        // or decrease the remainder
        // obtained by dividing k
        // from the ith value of array
        // so that we get the number
        // which is either closer to k
        // or its multiple
        if (a[i] != 1 && a[i] > k)
        {
            result = result +
                     Math.min(a[i] % k,
                          k - a[i] % k);
        }
        else
        {

            // Else we only have one
            // choice which is to
            // increment the value
            // to make equal to k
            result = result + k - a[i];
        }
    }

    return result;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = {4, 5, 6};
    int n = arr.length;
    int k = 5;
    System.out.println(MinOperation(arr, n, k));
}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python 3 program to make GCD
# of array a multiple of k.
def MinOperation(a, n, k):

    result = 0

    for i in range(n) :

        ''' If array value is not 1 and it
        is greater than k then we can
        increase the or decrease the
        remainder obtained by dividing
        k from the ith value of array so
        that we get the number which is
        either closer to k or its multiple '''
        if (a[i] != 1 and a[i] > k) :
            result = (result + min(a[i] % k,
                               k - a[i] % k))

        else :

            # Else we only have one choice
            # which is to increment the value
            # to make equal to k
            result = result + k - a[i]

    return result

# Driver code
if __name__ == "__main__":

    arr = [ 4, 5, 6 ]
    n = len(arr)
    k = 5
    print(MinOperation(arr, n, k))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C#  program to make GCD
// of array a multiple of k.
using System;

public class GFG{

    static int MinOperation(int []a,
                        int n, int k)
{

    int result = 0;

    for (int i = 0; i < n; ++i)
    {

        // If array value is not 1
        // and it is greater than k
        // then we can increase the
        // or decrease the remainder
        // obtained by dividing k
        // from the ith value of array
        // so that we get the number
        // which is either closer to k
        // or its multiple
        if (a[i] != 1 && a[i] > k)
        {
            result = result +
                    Math.Min(a[i] % k,
                        k - a[i] % k);
        }
        else
        {

            // Else we only have one
            // choice which is to
            // increment the value
            // to make equal to k
            result = result + k - a[i];
        }
    }

    return result;
}

// Driver code

    static public void Main (){
        int []arr = {4, 5, 6};
        int n = arr.Length;
        int k = 5;
        Console.WriteLine(MinOperation(arr, n, k));
    }
}

// This code is contributed
// by Tushil
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to make
// GCD of array a multiple
// of k.

function MinOperation($a, $n, $k)
{
    $result = 0;

    for ($i = 0; $i < $n; ++$i)
    {

        // If array value is
        // not 1 and it is
        // greater than k then
        // we can increase the
        // or decrease the remainder
        // obtained by dividing
        // k from the ith value of
        // array so that we get the
        // number which is either
        // closer to k or its multiple
        if ($a[$i] != 1 && $a[$i] > $k)
        {
            $result = $result + min($a[$i] %
                                    $k, $k -
                                    $a[$i] % $k);
        }
        else
        {

            // Else we only have one
            // choice which is to
            // increment the value
            // to make equal to k
            $result = $result +
                      $k - $a[$i];
        }
    }

    return $result;
}

// Driver code
$arr = array(4, 5, 6);
$n = sizeof($arr) /
     sizeof($arr[0]);
$k = 5;
echo MinOperation($arr, $n, $k);

// This code is contributed
// by @ajit
?>
```

## java 描述语言

```
<script>

 // Javascript program to make
// GCD of array a multiple
// of k.

function MinOperation(a, n, k)
{
    let result = 0;

    for (let i = 0; i < n; ++i)
    {

        // If array value is
        // not 1 and it is
        // greater than k then
        // we can increase the
        // or decrease the remainder
        // obtained by dividing
        // k from the ith value of
        // array so that we get the
        // number which is either
        // closer to k or its multiple
        if (a[i] != 1 && a[i] > k)
        {
            result = result + Math.min(a[i] %
                                    k, k -
                                    a[i] % k);
        }
        else
        {

            // Else we only have one
            // choice which is to
            // increment the value
            // to make equal to k
            result = result +
                      k - a[i];
        }
    }

    return result;
}

// Driver code
let arr = [4, 5, 6];
let n = arr.length;
let k = 5;
document.write(MinOperation(arr, n, k));

// This code is contributed
// by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
```
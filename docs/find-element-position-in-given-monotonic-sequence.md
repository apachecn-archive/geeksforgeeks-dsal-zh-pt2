# 在给定的单调序列中找到元素位置

> 原文:[https://www . geesforgeks . org/find-element-position-in-给定-单调-sequence/](https://www.geeksforgeeks.org/find-element-position-in-given-monotonic-sequence/)

给定整数 **k** 和单调递增序列:
**f(n)= an+bn【log2(n)】+cn^3**其中( **a** = 1、2、3、…)、( **b** = 1、2、3、…)、( **c** = 0、1、2、3、…)
在这里，【log <sub>2</sub> (n)】表示将日志带到
如果 n = 2-3，则值为 1。
如果 n = 4-7，则值为 2。
如果 n = 8-15，则值为 3。
任务是找到值 **n** ，使得 **f(n) = k** ，如果 **k** 不属于该序列，则打印 **0** 。

**注:**取值可以用 64 位表示，a、b、c 三个整数不超过 100。

**示例:**

> **输入:** a = 2，b = 1，c = 1，k = 12168587437017
> T3】输出:23001
> f(23001)= 12168587437017
> 
> **输入:** a = 7，b = 3，c = 0，k = 119753085330
> T3】输出: 1234567890

**天真方法:**给定 a、b、c 的值，为 n 的每个值找到 f(n)的值，并进行比较。

**有效方法:**使用二分搜索法，选择 **n =(最小值+最大值)/ 2** ，其中 **min** 和 **max** 是 **n** 可能的最小值和最大值，

*   如果 **f(n) < k** 则增加 **n** 。
*   如果 **f(n) > k** 则递减 **n** 。
*   如果 **f(n) = k** ，那么 **n** 就是要求的答案。
*   重复上述步骤，直到找到所需的值，或者在序列中找不到。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <math.h>
#define SMALL_N 1000000
#define LARGE_N  1000000000000000
using namespace std;

// Function to return the value of f(n) for given values of a, b, c, n
long long func(long long a, long long b, long long c, long long n)
{
    long long res = a * n;
    long long logVlaue = floor(log2(n));
    res += b * n * logVlaue;
    res += c * (n * n * n);
    return res;
}

long long getPositionInSeries(long long a, long long b,
                             long long c, long long k)
{
    long long start = 1, end = SMALL_N;

    // if c is 0, then value of n can be in order of 10^15.
    // if c!=0, then n^3 value has to be in order of 10^18
    // so maximum value of n can be 10^6.
    if (c == 0) {
        end = LARGE_N;
    }
    long long ans = 0;

    // for efficient searching, use binary search.
    while (start <= end) {
        long long mid = (start + end) / 2;
        long long val = func(a, b, c, mid);
        if (val == k) {
            ans = mid;
            break;
        }
        else if (val > k) {
            end = mid - 1;
        }
        else {
            start = mid + 1;
        }
    }
    return ans;
}

// Driver code
int main()
{
    long long a = 2, b = 1, c = 1;
    long long k = 12168587437017;

    cout << getPositionInSeries(a, b, c, k);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import log2, floor
SMALL_N = 1000000
LARGE_N = 1000000000000000

# Function to return the value of f(n)
# for given values of a, b, c, n
def func(a, b, c, n) :

    res = a * n
    logVlaue = floor(log2(n))
    res += b * n * logVlaue
    res += c * (n * n * n)
    return res

def getPositionInSeries(a, b, c, k) :

    start = 1
    end = SMALL_N

    # if c is 0, then value of n
    # can be in order of 10^15.
    # if c!=0, then n^3 value has
    # to be in order of 10^18
    # so maximum value of n can be 10^6.
    if (c == 0) :
        end = LARGE_N

    ans = 0

    # for efficient searching,
    # use binary search.
    while (start <= end) :

        mid = (start + end) // 2
        val = func(a, b, c, mid)
        if (val == k) :
            ans = mid
            break

        elif (val > k) :
            end = mid - 1

        else :
            start = mid + 1

    return ans;

# Driver code
if __name__ == "__main__" :

    a = 2
    b = 1
    c = 1
    k = 12168587437017

    print(getPositionInSeries(a, b, c, k))

# This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// from math import log2, floor
$SMALL_N = 1000000;
$LARGE_N = 1000000000000000;

// Function to return the value of f(n)
// for given values of a, b, c, n
function func($a, $b, $c, $n)
{
    $res = $a * $n;
    $logVlaue = floor(log($n, 2));
    $res += $b * $n * $logVlaue;
    $res += $c * ($n * $n * $n);
    return $res;
}

function getPositionInSeries($a, $b, $c, $k)
{
    global $SMALL_N, $LARGE_N;
    $start = 1;
    $end = $SMALL_N;

    // if c is 0, then value of n
    // can be in order of 10^15.
    // if c!=0, then n^3 value has
    // to be in order of 10^18
    // so maximum value of n can be 10^6.
    if ($c == 0)
        $end = $LARGE_N;

    $ans = 0;

    // for efficient searching,
    // use binary search.
    while ($start <= $end)
    {
        $mid = (int)(($start + $end) / 2);
        $val = func($a, $b, $c, $mid) ;
        if ($val == $k)
        {
            $ans = $mid;
            break;
        }

        else if ($val > $k)
            $end = $mid - 1;

        else
            $start = $mid + 1;
    }
    return $ans;
}

// Driver code
$a = 2;
$b = 1;
$c = 1;
$k = 12168587437017;

print(getPositionInSeries($a, $b, $c, $k));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
const SMALL_N = 1000000;
const LARGE_N = 1000000000000000;

// Function to return the value of f(n)
// for given values of a, b, c, n
function func(a, b, c, n)
{
    let res = a * n;
    let logVlaue = Math.floor(Math.log(n) /
                              Math.log(2));
    res += b * n * logVlaue;
    res += c * (n * n * n);
    return res;
}

function getPositionInSeries(a, b, c, k)
{
    let start = 1, end = SMALL_N;

    // If c is 0, then value of n can be
    // in order of 10^15\. If c!=0, then
    // n^3 value has to be in order of 10^18
    // so maximum value of n can be 10^6.
    if (c == 0)
    {
        end = LARGE_N;
    }
    let ans = 0;

    // For efficient searching, use binary search.
    while (start <= end)
    {
        let mid = parseInt((start + end) / 2);
        let val = func(a, b, c, mid);
        if (val == k)
        {
            ans = mid;
            break;
        }
        else if (val > k)
        {
            end = mid - 1;
        }
        else
        {
            start = mid + 1;
        }
    }
    return ans;
}

// Driver code
let a = 2, b = 1, c = 1;
let k = 12168587437017;

document.write(getPositionInSeries(a, b, c, k));

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
23001
```
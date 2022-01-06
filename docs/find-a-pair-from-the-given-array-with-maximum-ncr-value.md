# 从给定数组中找出一对最大 nCr 值的数组

> 原文:[https://www . geeksforgeeks . org/从给定的最大 ncr 值数组中找到一对/](https://www.geeksforgeeks.org/find-a-pair-from-the-given-array-with-maximum-ncr-value/)

给定正整数的数组**arr[]****n**。任务是从数组中找到元素**arr【I】**和**arr【j】**，使得**<sup>arr【I】</sup>C<sub>arr【j】</sub>**成为最大可能。如果有效对超过 1 对，打印其中任何一对。
**举例:**

> **输入:** arr[] = {3，1，2}
> **输出:**3 2
> <sup>3</sup>C<sub>1</sub>= 3
> <sup>3</sup>C<sub>2</sub>= 3
> <sup>2</sup>C<sub>1</sub>= 2
> (3，1)和(3，2)是仅有的最大<sup>n
> 的对
> **输入:** arr[] = {9，2，4，11，6}
> **输出:** 11 6</sup>

**逼近:**T2<sup>n</sup>C<sub>r</sub>T7】是单调递增函数，即**T9】n+1C<sub>r</sub>T70<sup>n</sup>C<sub>r</sub>T17】。我们可以用这个事实来接近我们的答案，我们将在所有给定的整数中选择最大值 **n** 。这样我们就固定了 **n** 的值。
现在，我们要寻找 **r** 。既然我们知道**<sup>n</sup>C<sub>r</sub>=<sup>n</sup>C<sub>n–r</sub>**，就意味着**<sup>n</sup>C<sub>r</sub>**会先达到最大值再下降。
如果 **n** 为奇数，那么我们的最大值将出现在 **n / 2** 和 **n / 2 + 1** 处。
对于 **n = 11** ，我们将在**<sup>11</sup>C<sub>5</sub>**和**<sup>11</sup>C<sub>6</sub>**处得到最大值。
当 **n** 为偶数时，我们的最大值将出现在 **n / 2** 处。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the pair that gives maximum nCr
void printMaxValPair(vector<long long>& v, int n)
{
    sort(v.begin(), v.end());

    // This gives the value of N in nCr
    long long N = v[n - 1];

    // Case 1 : When N is odd
    if (N % 2 == 1) {
        long long first_maxima = N / 2;
        long long second_maxima = first_maxima + 1;
        long long ans1 = 3e18, ans2 = 3e18;
        long long from_left = -1, from_right = -1;
        long long from = -1;
        for (long long i = 0; i < n; ++i) {
            if (v[i] > first_maxima) {
                from = i;
                break;
            }
            else {
                long long diff = first_maxima - v[i];
                if (diff < ans1) {
                    ans1 = diff;
                    from_left = v[i];
                }
            }
        }
        from_right = v[from];
        long long diff1 = first_maxima - from_left;
        long long diff2 = from_right - second_maxima;

        if (diff1 < diff2)
            cout << N << " " << from_left;
        else
            cout << N << " " << from_right;
    }

    // Case 2 : When N is even
    else {
        long long maxima = N / 2;
        long long ans1 = 3e18;
        long long R = -1;
        for (long long i = 0; i < n - 1; ++i) {
            long long diff = abs(v[i] - maxima);
            if (diff < ans1) {
                ans1 = diff;
                R = v[i];
            }
        }
        cout << N << " " << R;
    }
}

// Driver code
int main()
{
    vector<long long> v = { 1, 1, 2, 3, 6, 1 };
    int n = v.size();
    printMaxValPair(v, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to print the pair that gives maximum nCr
static void printMaxValPair(Vector<Long> v, int n)
{
    Collections.sort(v);

    // This gives the value of N in nCr
    long N = v.get((int)n - 1);

    // Case 1 : When N is odd
    if (N % 2 == 1)
    {
        long first_maxima = N / 2;
        long second_maxima = first_maxima + 1;
        long ans1 =(long) 3e18, ans2 = (long)3e18;
        long from_left = -1, from_right = -1;
        long from = -1;
        for (long i = 0; i < n; ++i)
        {
            if (v.get((int)i) > first_maxima)
            {
                from = i;
                break;
            }
            else
            {
                long diff = first_maxima - v.get((int)i);
                if (diff < ans1)
                {
                    ans1 = diff;
                    from_left = v.get((int)i);
                }
            }
        }
        from_right = v.get((int)from);
        long diff1 = first_maxima - from_left;
        long diff2 = from_right - second_maxima;

        if (diff1 < diff2)
            System.out.println( N + " " + from_left);
        else
            System.out.println( N + " " + from_right);
    }

    // Case 2 : When N is even
    else
    {
        long maxima = N / 2;
        long ans1 =(int) 3e18;
        long R = -1;
        for (long i = 0; i < n - 1; ++i)
        {
            long diff = Math.abs(v.get((int)i) - maxima);

            if (diff < ans1)
            {
                ans1 = diff;
                R = v.get((int)i);
            }
        }
        System.out.println( N + " " + R);
    }
}

// Driver code
public static void main(String args[])
{
    long arr[] = { 1, 1, 2, 3, 6, 1};
    Vector<Long> v = new Vector<Long>( );

    for(int i = 0; i < arr.length; i++)
    v.add(arr[i]);

    int n = v.size();
    printMaxValPair(v, n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the pair that
# gives maximum nCr
def printMaxValPair(v, n):

    v.sort()

    # This gives the value of N in nCr
    N = v[n - 1]

    # Case 1 : When N is odd
    if N % 2 == 1:
        first_maxima = N // 2
        second_maxima = first_maxima + 1
        ans1, ans2 = 3 * (10 ** 18), 3 * (10 ** 18)
        from_left, from_right = -1, -1
        _from = -1
        for i in range(0, n):
            if v[i] > first_maxima:
                _from = i
                break

            else:
                diff = first_maxima - v[i]
                if diff < ans1:
                    ans1 = diff
                    from_left = v[i]

        from_right = v[_from]
        diff1 = first_maxima - from_left
        diff2 = from_right - second_maxima

        if diff1 < diff2:
            print(N, from_left)
        else:
            print(N, from_right)

    # Case 2 : When N is even
    else:
        maxima = N // 2
        ans1 = 3 * (10 ** 18)
        R = -1
        for i in range(0, n - 1):
            diff = abs(v[i] - maxima)
            if diff < ans1:
                ans1 = diff
                R = v[i]

        print(N, R)

# Driver code
if __name__ == "__main__":

    v = [1, 1, 2, 3, 6, 1]
    n = len(v)
    printMaxValPair(v, n)

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to print the pair that gives maximum nCr
static void printMaxValPair(List<long> v, int n)
{
    v.Sort();

    // This gives the value of N in nCr
    long N = v[(int)n - 1];

    // Case 1 : When N is odd
    if (N % 2 == 1)
    {
        long first_maxima = N / 2;
        long second_maxima = first_maxima + 1;
        long ans1 = (long) 3e18, ans2 = (long)3e18;
        long from_left = -1, from_right = -1;
        long from = -1;
        for (long i = 0; i < n; ++i)
        {
            if (v[(int)i] > first_maxima)
            {
                from = i;
                break;
            }
            else
            {
                long diff = first_maxima - v[(int)i];
                if (diff < ans1)
                {
                    ans1 = diff;
                    from_left = v[(int)i];
                }
            }
        }
        from_right = v[(int)from];
        long diff1 = first_maxima - from_left;
        long diff2 = from_right - second_maxima;

        if (diff1 < diff2)
            Console.WriteLine( N + " " + from_left);
        else
            Console.WriteLine( N + " " + from_right);
    }

    // Case 2 : When N is even
    else
    {
        long maxima = N / 2;
        long ans1 = (long)3e18;
        long R = -1;
        for (long i = 0; i < n - 1; ++i)
        {
            long diff = Math.Abs(v[(int)i] - maxima);

            if (diff < ans1)
            {
                ans1 = diff;
                R = v[(int)i];
            }
        }
        Console.WriteLine( N + " " + R);
    }
}

// Driver code
public static void Main(String []args)
{
    long []arr = { 1, 1, 2, 3, 6, 1};
    List<long> v = new List<long>( );

    for(int i = 0; i < arr.Length; i++)
    v.Add(arr[i]);

    int n = v.Count;
    printMaxValPair(v, n);
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the pair that
// gives maximum nCr
function printMaxValPair($v, $n)
{
    sort($v);

    // This gives the value of N in nCr
    $N = $v[$n - 1];

    // Case 1 : When N is odd
    if ($N % 2 == 1)
    {
        $first_maxima = $N / 2;
        $second_maxima = $first_maxima + 1;
        $ans1 = 3e18;
        $ans2 = 3e18;
        $from_left = -1;
        $from_right = -1;
        $from = -1;
        for ($i = 0; $i < $n; ++$i)
        {
            if ($v[$i] > $first_maxima)
            {
                $from = $i;
                break;
            }
            else
            {
                $diff = $first_maxima - $v[$i];
                if ($diff < $ans1)
                {
                    $ans1 = $diff;
                    $from_left = $v[$i];
                }
            }
        }
        $from_right = $v[$from];
        $diff1 = $first_maxima - $from_left;
        $diff2 = $from_right - $second_maxima;

        if ($diff1 < $diff2)
            echo $N . " " . $from_left;
        else
            echo $N . " " . $from_right;
    }

    // Case 2 : When N is even
    else
    {
        $maxima = $N / 2;
        $ans1 = 3e18;
        $R = -1;
        for ($i = 0; $i < $n - 1; ++$i)
        {
            $diff = abs($v[$i] - $maxima);
            if ($diff < $ans1)
            {
                $ans1 = $diff;
                $R = $v[$i];
            }
        }
        echo $N . " " . $R;
    }
}

// Driver code
$v = array( 1, 1, 2, 3, 6, 1 );
$n = count($v);
printMaxValPair($v, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the pair that gives maximum nCr
function printMaxValPair(v,  n)
{
    v.sort((a,b)=>a-b)

    // This gives the value of N in nCr
    var N = v[n - 1];

    // Case 1 : When N is odd
    if (N % 2 == 1) {
        var first_maxima = N / 2;
        var second_maxima = first_maxima + 1;
        var ans1 = 3000000000000000000, ans2 = 3000000000000000000;
        var from_left = -1, from_right = -1;
        var from = -1;
        for (var i = 0; i < n; ++i) {
            if (v[i] > first_maxima) {
                from = i;
                break;
            }
            else {
                var diff = first_maxima - v[i];
                if (diff < ans1) {
                    ans1 = diff;
                    from_left = v[i];
                }
            }
        }
        from_right = v[from];
        var diff1 = first_maxima - from_left;
        var diff2 = from_right - second_maxima;

        if (diff1 < diff2)
            document.write( N + " " + from_left);
        else
            document.write( N + " " + from_right);
    }

    // Case 2 : When N is even
    else {
        var maxima = parseInt(N / 2);
        var ans1 = 3000000000000000000;
        var R = -1;
        for (var i = 0; i < n - 1; ++i) {
            var diff = Math.abs(v[i] - maxima);
            if (diff < ans1) {
                ans1 = diff;
                R = v[i];
            }
        }
        document.write( N + " " + R);
    }
}

// Driver code
var v = [1, 1, 2, 3, 6, 1 ];
var n = v.length;
printMaxValPair(v, n);

// This code is contributed by famously.
</script>
```

**Output:** 

```
6 3
```
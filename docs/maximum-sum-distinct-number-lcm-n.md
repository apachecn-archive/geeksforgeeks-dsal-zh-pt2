# 不同数字的最大和，LCM 为 N

> 原文:[https://www . geesforgeks . org/maximum-sum-distinct-number-LCM-n/](https://www.geeksforgeeks.org/maximum-sum-distinct-number-lcm-n/)

给定一个数 N，任务是找出不同数的最大和，使得所有这些数的最小公倍数为 N。

```
Input  : N = 12
Output : 20
Maximum sum which we can achieve is,
1 + 2 + 3 + 4 + 6 + 12 = 28

Input  : N = 15
Output : 24 
```

我们可以通过观察一些情况来解决这个问题，因为 N 需要是所有数的 LCM，所以它们都将是 N 的除数，但是因为一个数在和中只能取一次，所以所有取的数应该是不同的。想法是**取 N 的每个除数求和一次**使结果最大化。
我们怎么能说我们得到的和是最大和呢？原因是，我们已经把 N 的所有除数都加到了和中，现在如果我们再把一个不是 N 除数的数加到和中，那么和会增加，但是 LCM 性质不会被所有这些整数所保持。所以除了 N 的所有除数之外，不可能在我们的和中再加一个数，所以我们的问题归结为，给定 N，求所有除数的和，它可以在 O(sqrt(N))时间内求解。
所以解的总时间复杂度将为 O(sqrt(N))加上 O(1)个额外空间。
以下给出了上述概念的代码。求一个数的所有除数请参考[这个](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)帖子。

## C++

```
// C/C++ program to get maximum sum of Numbers
// with condition that their LCM should be N
#include <bits/stdc++.h>
using namespace std;

// Method returns maximum sum f distinct
// number whose LCM is N
int getMaximumSumWithLCMN(int N)
{
    int sum = 0;
    int LIM = sqrt(N);

    // find all divisors which divides 'N'
    for (int i = 1; i <= LIM; i++) {
        // if 'i' is divisor of 'N'
        if (N % i == 0) {
            // if both divisors are same then add
            // it only once else add both
            if (i == (N / i))
                sum += i;
            else
                sum += (i + N / i);
        }
    }

    return sum;
}

// Driver code to test above methods
int main()
{
    int N = 12;
    cout << getMaximumSumWithLCMN(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get
// maximum sum of Numbers
// with condition that
// their LCM should be N

class GFG {
    // Method returns maximum
    // sum f distinct number
    // whose LCM is N
    static int getMaximumSumWithLCMN(int N)
    {
        int sum = 0;
        int LIM = (int)Math.sqrt(N);

        // find all divisors which divides 'N'
        for (int i = 1; i <= LIM; i++) {
            // if 'i' is divisor of 'N'
            if (N % i == 0) {
                // if both divisors are same then add
                // it only once else add both
                if (i == (N / i))
                    sum += i;
                else
                    sum += (i + N / i);
            }
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 12;
        System.out.println(getMaximumSumWithLCMN(N));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to get
# maximum sum of Numbers
# with condition that
# their LCM should be N

import math

# Method returns maximum sum f distinct
# number whose LCM is N
def getMaximumSumWithLCMN(N):

    sum = 0
    LIM = int(math.sqrt(N))

    # find all divisors which divides 'N'
    for i in range(1, LIM + 1):

        # if 'i' is divisor of 'N'
        if (N % i == 0):

            # if both divisors are same then add
            # it only once else add both
            if (i == (N // i)):
                sum = sum + i
            else:
                sum = sum + (i + N // i)

    return sum

# driver code

N = 12
print(getMaximumSumWithLCMN(N))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to get maximum sum
// of Numbers with condition that
// their LCM should be N
using System;

class GFG {

    // Method returns maximum sum f
    // distinct number whose LCM is N
    static int getMaximumSumWithLCMN(int N)
    {
        int sum = 0;
        int LIM = (int)Math.Sqrt(N);

        // Find all divisors which divides 'N'
        for (int i = 1; i <= LIM; i++) {

            // if 'i' is divisor of 'N'
            if (N % i == 0) {

                // if both divisors are same then
                // add it only once else add both
                if (i == (N / i))
                    sum += i;
                else
                    sum += (i + N / i);
            }
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {
        int N = 12;
        Console.Write(getMaximumSumWithLCMN(N));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//php program to find the max sum of
// numbers whose lcm is n

// Returns maximum sum of numbers with
// LCM as N
function maxSumLCM($n)
{
    $max_sum = 0; // Initialize result

    // Finding a divisor of n and adding
    // it to max_sum
    for ($i = 1; $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {
            $max_sum += $i;
            if ($n/$i != $i)
                $max_sum += ($n / $i);
        }
    }

    return $max_sum;
}

// Driver code
$n = 2;
echo MaxSumLCM($n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to get maximum sum of Numbers
// with condition that their LCM should be N

// Method returns maximum sum f distinct
// number whose LCM is N
function getMaximumSumWithLCMN(N)
{
    let sum = 0;
    let LIM = Math.sqrt(N);

    // find all divisors which divides 'N'
    for (let i = 1; i <= LIM; i++)
    {

        // if 'i' is divisor of 'N'
        if (N % i == 0)
        {

            // if both divisors are same then add
            // it only once else add both
            if (i == (N / i))
                sum += i;
            else
                sum += (i + N / i);
        }
    }
    return sum;
}

// Driver code to test above methods
    let N = 12;
    document.write(getMaximumSumWithLCMN(N) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

输出:

```
28
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
# 用连续数的和来表示一个数的计数方式

> 原文:[https://www . geesforgeks . org/count-way-express-number-sum-continuous-numbers/](https://www.geeksforgeeks.org/count-ways-express-number-sum-consecutive-numbers/)

给定一个整数 **N** ，任务是找到将这个数表示为 2 个或更多连续[自然数](https://www.geeksforgeeks.org/natural-numbers/)之和的方法数。

**例:**

> **输入:** N = 15
> **输出:** 3
> **说明:**
> 15 可以表示为:
> 
> 1.  1 + 2 + 3 + 4 + 5
> 2.  4 + 5 + 6
> 3.  7 + 8
> 
> **输入:**N = 10
> T3】输出: 1

**方法:**想法是将 N 表示为长度为 L+1 的序列，表示为:
N = a + (a+1) + (a+2) +..+(a+L)
=>N =(L+1)* a+(L *(L+1))/2
=>a =(N-L*(L+1)/2)/(L+1)
我们用 1 到 L *(L+1)/2 之间的值代替 L<N
如果我们得到一个自然数“a”，那么这个解应该被计数。

？列表= PLM 68 oyaq FM 7q-SV 3ga 5 xbzgvkoq 0 xdrw

## C++

```
// C++ program to count number of ways to express
// N as sum of consecutive numbers.
#include <bits/stdc++.h>
using namespace std;

long int countConsecutive(long int N)
{
    // constraint on values of L gives us the
    // time Complexity as O(N^0.5)
    long int count = 0;
    for (long int L = 1; L * (L + 1) < 2 * N; L++) {
        double a = (1.0 * N - (L * (L + 1)) / 2) / (L + 1);
        if (a - (int)a == 0.0)
            count++;
    }
    return count;
}

// Driver Code
int main()
{
    long int N = 15;
    cout << countConsecutive(N) << endl;
    N = 10;
    cout << countConsecutive(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to count number of ways
// to express N as sum of consecutive numbers.
public class SumConsecutiveNumber {
    // Utility method to compute number of ways
    // in which N can be represented as sum of
    // consecutive number
    static int countConsecutive(int N)
    {
        // constraint on values of L gives us the
        // time Complexity as O(N^0.5)
        int count = 0;
        for (int L = 1; L * (L + 1) < 2 * N; L++) {
            double a = (double)((1.0 * N - (L * (L + 1)) / 2) / (L + 1));
            if (a - (int)a == 0.0)
                count++;
        }
        return count;
    }

    // Driver code to test above function
    public static void main(String[] args)
    {
        int N = 15;
        System.out.println(countConsecutive(N));
        N = 10;
        System.out.println(countConsecutive(N));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to count number of ways to
# express N as sum of consecutive numbers.

def countConsecutive(N):

    # constraint on values of L gives us the
    # time Complexity as O(N ^ 0.5)
    count = 0
    L = 1
    while( L * (L + 1) < 2 * N):
        a = (1.0 * N - (L * (L + 1) ) / 2) / (L + 1)
        if (a - int(a) == 0.0):
            count += 1
        L += 1
    return count

# Driver code

N = 15
print countConsecutive(N)
N = 10
print countConsecutive(N)

# This code is contributed by Sachin Bisht
```

## C#

```
// A C# program to count number of
// ways to express N as sum of
// consecutive numbers.
using System;

public class GFG {

    // Utility method to compute
    // number of ways in which N
    // can be represented as sum
    // of consecutive number
    static int countConsecutive(int N)
    {

        // constraint on values of L
        // gives us the time
        // Complexity as O(N^0.5)
        int count = 0;
        for (int L = 1; L * (L + 1)
                        < 2 * N;
             L++) {
            double a = (double)((1.0
                                   * N
                               - (L * (L + 1))
                                     / 2)
                              / (L + 1));

            if (a - (int)a == 0.0)
                count++;
        }

        return count;
    }

    // Driver code to test above
    // function
    public static void Main()
    {
        int N = 15;
        Console.WriteLine(
            countConsecutive(N));

        N = 10;
        Console.Write(
            countConsecutive(N));
    }
}

// This code is contributed by
// nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of ways to express N as sum
// of consecutive numbers.

function countConsecutive($N)
{
    // constraint on values
    // of L gives us the
    // time Complexity as O(N^0.5)
    $count = 0;
    for ($L = 1;
         $L * ($L + 1) < 2 * $N; $L++)
    {
        $a = (int)(1.0 * $N - ($L *
             (int)($L + 1)) / 2) / ($L + 1);
        if ($a - (int)$a == 0.0)
            $count++;
    }
    return $count;
}

// Driver Code
$N = 15;
echo countConsecutive($N), "\n";
$N = 10;
echo countConsecutive($N), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // A Javascript program to count number of
    // ways to express N as sum of
    // consecutive numbers.

    // Utility method to compute
    // number of ways in which N
    // can be represented as sum
    // of consecutive number
    function countConsecutive(N)
    {

        // constraint on values of L
        // gives us the time
        // Complexity as O(N^0.5)
        let count = 0;
        for (let L = 1; L * (L + 1) < 2 * N; L++)
        {
            let a = ((1.0 * N-(L * (L + 1)) / 2) / (L + 1));

            if (a - parseInt(a, 10) == 0.0)
                count++;    
        }

        return count;
    }

    let N = 15;
    document.write(countConsecutive(N) + "</br>");

    N = 10;
    document.write(countConsecutive(N));

</script>
```

**Output:** 

```
3
1
```

**时间复杂度:** O(N^0.5)

本文由**普拉纳夫·马拉特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。
看看你在极客主页上的文章，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
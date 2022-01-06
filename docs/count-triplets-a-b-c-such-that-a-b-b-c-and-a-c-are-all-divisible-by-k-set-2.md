# 计算三元组(a，b，c)，使得 a + b，b + c 和 a + c 都可以被 K 整除|集合 2

> 原文:[https://www . geesforgeks . org/count-triples-a-B- c-so-a-B- B- c-和-a-c-都可以被 k-set-2 整除/](https://www.geeksforgeeks.org/count-triplets-a-b-c-such-that-a-b-b-c-and-a-c-are-all-divisible-by-k-set-2/)

给定两个正整数 **N** 和 **K** ，任务是统计三胞胎 **(a、b、c)** 的数量，使得 **0 < a、b、c < N** 和 **(a + b)** 、 **(b + c)** 和 **(c + a)** 都是 **K** 的倍数。

**示例:**

> ***输入:** N = 2，K = 2*
> ***输出:** 2*
> **解释:** *满足给定性质的所有可能三元组为(1，1，1)和(2，2，2)。*
> *因此，总计数为 2。*
> 
> ***输入:** N = 3，K = 2*
> T5**输出:** 9

**天真的做法:**参考[之前的帖子](https://www.geeksforgeeks.org/triplet-pair-a-b-c-such-that-ab-bc-and-ac-are-all-divisible-by-k/)解决这个问题最简单的做法。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   给定的条件由同余式表示:

> = > a+b≡b+c≡c+a≡0(mod K)
> =>a+b≡b+c(mod K)
> =>a≡c(mod K)

*   在不使用同余式的情况下，也可以观察到上述关系:
    *   由于 **(a + b)** 是 **K** 的倍数， **(c + b)** 是 **K** 的倍数。因此**(a+b)—(c+b)= a–c**也是 **K** 的倍数，即 **a ≡ b ≡ c (mod K)** 。
    *   因此，该表达式可以进一步评估为:

> = > a+b≡0(mod K)
> =>a+a≡0(mod K)(因为 a 与 b 全等)
> = > 2a ≡ 0 (mod K)

根据以上观察，可以计算以下两种情况的结果:

*   如果 **K 为奇数**，那么 **a ≡ b ≡ c ≡ 0(mod K)** 因为三者全等，三胞胎总数可以计算为 **(N / K) <sup>3</sup>** 。
*   如果 **K 为偶数**，则 **K** 可被 **2** 和 **a ≡ 0 (mod K)** 、 **b ≡ 0 (mod K)** 、 **c ≡ 0 (mod K)** 整除。因此，三胞胎总数可计算为**(N/K)<sup>3</sup>((N+(K/2))/K)<sup>3</sup>**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to count the number of
// triplets from the range [1, N - 1]
// having sum of all pairs divisible by K
int countTriplets(int N, int K)
{
    // If K is even
    if (K % 2 == 0) {
        long long int x = N / K;
        long long int y = (N + (K / 2)) / K;

        return x * x * x + y * y * y;
    }

    // Otherwise
    else {
        long long int x = N / K;
        return x * x * x;
    }
}

// Driver Code
int main()
{
    int N = 2, K = 2;
    cout << countTriplets(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count the number of
// triplets from the range [1, N - 1]
// having sum of all pairs divisible by K
static int countTriplets(int N, int K)
{

    // If K is even
    if (K % 2 == 0)
    {
        int x = N / K;
        int y = (N + (K / 2)) / K;

        return x * x * x + y * y * y;
    }

    // Otherwise
    else
    {
        int x = N / K;
        return x * x * x;
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, K = 2;

    System.out.print(countTriplets(N, K));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# triplets from the range [1, N - 1]
# having sum of all pairs divisible by K
def countTriplets(N, K):

    # If K is even
    if (K % 2 == 0):
        x = N // K
        y = (N + (K // 2)) // K

        return x * x * x + y * y * y

    # Otherwise
    else:
        x = N // K
        return x * x * x

# Driver Code
if __name__ == "__main__":

    N = 2
    K = 2

    print(countTriplets(N, K))

# This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach 

// Function to count the number of
// triplets from the range [1, N - 1]
// having sum of all pairs divisible by K
function countTriplets(N, K)
{

    // If K is even
    if (K % 2 == 0)
    {
        var x = parseInt(N / K);
        var y = parseInt((N + (K / 2)) / K);

        return x * x * x + y * y * y;
    }

    // Otherwise
    else
    {
        var x = parseInt(N / K);
        return x * x * x;
    }
}

// Driver Code
var N = 2, K = 2;

document.write(countTriplets(N, K));

// This code is contributed by Ankita saini

</script>
```

## C#

```
// C# program for the above approach

using System;

class GFG{

// Function to count the number of
// triplets from the range [1, N - 1]
// having sum of all pairs divisible by K
static int countTriplets(int N, int K)
{

    // If K is even
    if (K % 2 == 0)
    {
        int x = N / K;
        int y = (N + (K / 2)) / K;

        return x * x * x + y * y * y;
    }

    // Otherwise
    else
    {
        int x = N / K;
        return x * x * x;
    }
}

// Driver Code
    static void Main() {
       int N = 2, K = 2;

       Console.Write(countTriplets(N, K));
    }
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach
    // Function to count the number of
    // triplets from the range [1, N - 1]
    // having sum of all pairs divisible by K
    function countTriplets(N,K)
    {
        // If K is even
        if (K % 2 == 0) {
            let x = parseInt(N / K, 10);
            let y = parseInt((N + parseInt(K / 2, 10)) / K, 10);

            return x * x * x + y * y * y;
        }

        // Otherwise
        else {
            let x = parseInt(N / K, 10);
            return x * x * x;
        }
    }

    // Driver Code

    let N = 2, K = 2;
    document.write(countTriplets(N, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)
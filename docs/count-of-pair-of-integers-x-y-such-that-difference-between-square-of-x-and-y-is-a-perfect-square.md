# 对整数对(x，y)进行计数，使得 x 和 y 的平方之差为完美平方

> 原文:[https://www . geeksforgeeks . org/整数对计数-x-y-x 和-y 的平方差等于完美平方/](https://www.geeksforgeeks.org/count-of-pair-of-integers-x-y-such-that-difference-between-square-of-x-and-y-is-a-perfect-square/)

给定一个整数 N，任务是找出小于 N 且大于 1 的整数对(x，y)的个数，使得**x<sup>2</sup>–y**是一个平方数或 0。

**示例:**

> **输入:** N = 3
> **输出:** 2
> **解释:**
> 唯一可能的有效对是(1，1)，(2，3)。因此，这种对的计数是 2。
> 
> **输入:**N = 2
> T3】输出: 1

**天真法:**解决给定问题最简单的方法是[在范围**【1，N】**上生成所有可能的**对整数**](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(x，y)** ，然后检查**(x<sup>2</sup>–y)**的值是否为[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果发现是**真**，那就数这一对。检查所有可能的情况后，打印获得的总计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过以下观察进行优化:

> **x <sup>2</sup> -y** 是一个数的平方，比如说 **z** 的平方。
> x<sup>2</sup>–y = z<sup>2</sup>
> x<sup>2</sup>–z<sup>2</sup>= y
> (x+z)*(x–z)= y
> 
> 现在，让 **x + z = p** 和**x–z = q**T4】p * q = y

因此，问题简化为计算成对的 **p，q** 而不是 **x，y** 。
现在，由于 y 只能在 **1** 到 **N**
的范围内，所以， **p*q** 也将在 1 到 N 的范围内，而由于 **p > =q** (因为 **x+z > = x-z** )， **q** 将在 **1 到√N** 的范围内

> 同样 **p+q = 2*x** ，所以 **x = (p+q)/2。**
> 现在，由于 **x** 可以有最大值 **N** ，因此
> **(p+q)/2<= N**
> **p<= 2 * N-q**

所以 **p 的最大值= min(2 * N–q，N/q)。**
现在，在知道 **p** & **q、**的范围后，尝试 **p** & **q** 的所有可能值。并且在固定之后，所有可能的配对都是 **(l，q)** ，其中 **l** 在从 **q** 到最大值 **p.**
的范围内，所以形成的配对总数是**(p–q+1)**，比如 **cnt** 。

现在，我们知道 **p=x+z** 和 **q=x-z，**所以这两个 **p** & **q** 不是偶数就是奇数。基于这一结论，如果 **q** 为偶数，则有效对总数为 **cnt/2(去除所有对后，p 值为****)**，如果为奇数，则有效对总数为 **(cnt/2 + 1)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find number of pairs
// (x, y) such that x^2 - y is a
// square number
int countPairs(int N)
{
    // Stores the count of total pairs
    int res = 0;

    // Iterate q value 1 to sqrt(N)
    for (int q = 1; q * q <= N; q++) {

        // Maximum possible value of p is
        // min(2 * N - q, N / q)
        int maxP = min(2 * N - q, N / q);

        // P must be greater than or
        // equal to q
        if (maxP < q)
            continue;

        // Total number of pairs are
        int cnt = maxP - q + 1;

        // Adding all valid pairs to res
        res += (cnt / 2 + (cnt & 1));
    }

    // Return total no of pairs (x, y)
    return res;
}

// Driver Code
int main()
{
    int N = 3;
    cout << countPairs(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find number of pairs
// (x, y) such that x^2 - y is a
// square number
static int countPairs(int N)
{

    // Stores the count of total pairs
    int res = 0;

    // Iterate q value 1 to Math.sqrt(N)
    for (int q = 1; q * q <= N; q++) {

        // Maximum possible value of p is
        // Math.min(2 * N - q, N / q)
        int maxP = Math.min(2 * N - q, N / q);

        // P must be greater than or
        // equal to q
        if (maxP < q)
            continue;

        // Total number of pairs are
        int cnt = maxP - q + 1;

        // Adding all valid pairs to res
        res += (cnt / 2 + (cnt & 1));
    }

    // Return total no of pairs (x, y)
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    System.out.print(countPairs(N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function to find number of pairs
# (x, y) such that x^2 - y is a
# square number
def countPairs(N):

    # Stores the count of total pairs
    res = 0

    # Iterate q value 1 to sqrt(N)
    for q in range(1, int(math.sqrt(N)) + 1):

        # Maximum possible value of p is
        # min(2 * N - q, N / q)
        maxP = min(2 * N - q, N // q)

        # P must be greater than or
        # equal to q
        if (maxP < q):
            continue

        # Total number of pairs are
        cnt = maxP - q + 1

        # Adding all valid pairs to res
        res += (cnt // 2 + (cnt & 1))

    # Return total no of pairs (x, y)
    return res

# Driver Code
if __name__ == "__main__":

    N = 3
    print(countPairs(N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to find number of pairs
    // (x, y) such that x^2 - y is a
    // square number
    static int countPairs(int N)
    {

        // Stores the count of total pairs
        int res = 0;

        // Iterate q value 1 to sqrt(N)
        for (int q = 1; q * q <= N; q++) {

            // Maximum possible value of p is
            // min(2 * N - q, N / q)
            int maxP = Math.Min(2 * N - q, N / q);

            // P must be greater than or
            // equal to q
            if (maxP < q)
                continue;

            // Total number of pairs are
            int cnt = maxP - q + 1;

            // Adding all valid pairs to res
            res += (cnt / 2 + (cnt & 1));
        }

        // Return total no of pairs (x, y)
        return res;
    }

    // Driver Code
    public static void Main()
    {
        int N = 3;
        Console.WriteLine(countPairs(N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find number of pairs
        // (x, y) such that x^2 - y is a
        // square number
        function countPairs(N) {
            // Stores the count of total pairs
            let res = 0;

            // Iterate q value 1 to sqrt(N)
            for (let q = 1; q * q <= N; q++) {

                // Maximum possible value of p is
                // min(2 * N - q, N / q)
                let maxP = Math.min(2 * N - q, N / q);

                // P must be greater than or
                // equal to q
                if (maxP < q)
                    continue;

                // Total number of pairs are
                let cnt = maxP - q + 1;

                // Adding all valid pairs to res
                res += Math.floor(cnt / 2 + (cnt & 1));
            }

            // Return total no of pairs (x, y)
            return res;
        }

        // Driver Code

        let N = 3;
        document.write(countPairs(N));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N<sup>1/2</sup>)
T5】辅助空间: O(1)
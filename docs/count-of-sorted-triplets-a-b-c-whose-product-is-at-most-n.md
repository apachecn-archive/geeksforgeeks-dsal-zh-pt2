# 乘积最多为 N 的已排序三元组(a，b，c)的计数

> 原文:[https://www . geeksforgeeks . org/count-of-sorted-triples-a-B- c-谁的产品最多是-n/](https://www.geeksforgeeks.org/count-of-sorted-triplets-a-b-c-whose-product-is-at-most-n/)

给定一个整数 **N** ，任务是找到三元组(a，b，c)的计数，使得 a < = b < = c，a * b * c < = N。

**示例:**

> **输入:** N = 5
> **输出:** 6
> **说明:**符合要求条件的三元组是(1，1，1，(1，1，2)，(1，1，3)，(1，1，4)，(1，1，1，5)和(1，2，2)。因此，值三元组的计数是 6。
> 
> **输入:**N = 20
> T3】输出: 40

**方法:**给定的问题可以基于以下观察来解决:

*   由于 **a < = b < =c** ，可以观察到 **a** 的值必须在**【1，N<sup>1/3</sup>**的范围内。
*   同样，对于给定的**a****b**的值必须在范围**【a、(不适用)<sup>1/2</sup>**内。
*   同样，当 **a** 和 **b** 的值固定时， **c** 的值必须在**【b，N/(a * b)】**的范围内。因此 **c** 的可能值的数量是在**【b，N/(a * b)】**范围内的整数的计数。因此，对于每一个有效的 **a** 和 **b** ，则 **c** 的可能值个数为**N/(a * b)–b+ 1**。

因此，使用下面的上述观察是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to find the count of valid
// triplets (a, b, c) such that the value
// of a * b * c <= N and a <= b <= c
long long validTriplets(int N)
{
    // Stores count of triplets
    long long ans = 0;

    // Loop to iterate in the
    // range [1, N^(1/3)]
    for (long long a = 1; a * a * a <= N; a++) {

        // Loop to iterate in the
        // range [a, (N/a)^(1/2)]
        for (long long b = a; a * b * b <= N; b++) {

            // Add the count of valid
            // values of c for a fixed
            // value of a and b
            ans += N / a / b - b + 1;
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int N = 5;
    cout << validTriplets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to find the count of valid
// triplets (a, b, c) such that the value
// of a * b * c <= N and a <= b <= c
static long validTriplets(int N)
{

    // Stores count of triplets
    long ans = 0;

    // Loop to iterate in the
    // range [1, N^(1/3)]
    for (long a = 1; a * a * a <= N; a++) {

        // Loop to iterate in the
        // range [a, (N/a)^(1/2)]
        for (long b = a; a * b * b <= N; b++) {

            // Add the count of valid
            // values of c for a fixed
            // value of a and b
            ans += N / a / b - b + 1;
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    System.out.print(validTriplets(N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to find the count of valid
# triplets (a, b, c) such that the value
# of a * b * c <= N and a <= b <= c
def validTriplets(N):

    # Stores count of triplets
    ans = 0;

    # Loop to iterate in the
    # range [1, N^(1/3)]
    for a in range(1, int(N ** (1 / 3)) + 1):

        # Loop to iterate in the
        # range [a, (N/a)^(1/2)]
        b = a;
        while(a * b * b <= N):
            # Add the count of valid
            # values of c for a fixed
            # value of a and b
            ans += N / a / b - b + 1;
            b += 1

    # Return Answer
    return int(ans);

# Driver Code
N = 5;

print(validTriplets(N));

# This code is contributed by gfgking
```

## C#

```
// C# implementation of the above approach
using System;
class GFG {
    // Function to find the count of valid
    // triplets (a, b, c) such that the value
    // of a * b * c <= N and a <= b <= c
    static long validTriplets(int N)
    {
        // Stores count of triplets
        long ans = 0;

        // Loop to iterate in the
        // range [1, N^(1/3)]
        for (long a = 1; a * a * a <= N; a++) {

            // Loop to iterate in the
            // range [a, (N/a)^(1/2)]
            for (long b = a; a * b * b <= N; b++) {

                // Add the count of valid
                // values of c for a fixed
                // value of a and b
                ans += N / a / b - b + 1;
            }
        }

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        int N = 5;
        Console.WriteLine(validTriplets(N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to find the count of valid
// triplets (a, b, c) such that the value
// of a * b * c <= N and a <= b <= c
function validTriplets(N)
{

    // Stores count of triplets
    let ans = 0;

    // Loop to iterate in the
    // range [1, N^(1/3)]
    for(let a = 1; a * a * a <= N; a++)
    {

        // Loop to iterate in the
        // range [a, (N/a)^(1/2)]
        for(let b = a; a * b * b <= N; b++)
        {

            // Add the count of valid
            // values of c for a fixed
            // value of a and b
            ans += N / a / b - b + 1;
        }
    }

    // Return Answer
    return Math.floor(ans);
}

// Driver Code
let N = 5;

document.write(validTriplets(N));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
6
```

***时间复杂度:**O(N<sup>2/3</sup>)*
***辅助空间:** O(1)*
# 计算三胞胎，使两个数与第三个数的乘积为 N

> 原文:[https://www . geeksforgeeks . org/count-triples-这样两个数的乘积加第三个数为-n/](https://www.geeksforgeeks.org/count-triplets-such-that-product-of-two-numbers-added-with-third-number-is-n/)

给定一个正整数 **N** ，任务是找到三元组 **(A，B，C)** 的个数，其中 **A** 、 **B** 、 **C** 为正整数，使得两个数相加的乘积为 **N** ，即 **A * B + C = N** 。

**示例:**

> **输入:** N = 3
> **输出:** 3
> **解释:**
> 以下是满足给定标准的可能三元组:
> 
> 1.  (1，1，2):1 * 1+2 = 3 的值。
> 2.  (1，2，1):1 * 2+1 = 3 的值。
> 3.  (2，1，1):2 * 1+1 = 3 的值。
> 
> 因此，这样的三胞胎总数是 3。
> 
> **输入:**N = 5
> T3】输出: 8

**方法:**将方程 **A * B + C = N** 重新排列为**A * B = N–C**，即可求解给定问题。现在，唯一可能的值 **A** 和 **B** 必须满足上述等式的是**N–C**的除数。例如，如果**的值 N–C = 18**，有 6 个除数，即 1、2、3、6、9、18。因此，满足上述等式的 **A、B** 的值为: **(1，18)、(2，9)、(3，6)、(6，3)、(9，2)、(18，1)** 。因此，对于**N–C = 18**的值， **A** 、 **B** 的可能值为 **6** ，即**N–C(= 18)**的除数。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说**计数**为 **0** ，它存储可能的三元组的总数。
*   [使用变量 **i** 在范围【T11，N–1】](https://www.geeksforgeeks.org/range-based-loop-c/)内循环，对于每个值， **i** [找到**(N–I)**的除数总数](https://www.geeksforgeeks.org/total-number-divisors-given-number/)，并将其添加到变量**计数**中。
*   完成上述步骤后，打印**计数**的值作为三胞胎的合成数量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the divisors of
// the number (N - i)
int countDivisors(int n)
{
    // Stores the resultant count of
    // divisors of (N - i)
    int divisors = 0;
    int i;

    // Iterate over range [1, sqrt(N)]
    for (i = 1; i * i < n; i++) {
        if (n % i == 0) {
            divisors++;
        }
    }
    if (i - (n / i) == 1) {
        i--;
    }
    for (; i >= 1; i--) {
        if (n % i == 0) {
            divisors++;
        }
    }
    // Return the total divisors
    return divisors;
}

// Function to find the number of triplets
// such that A * B - C = N
int possibleTriplets(int N)
{
    int count = 0;

    // Loop to fix the value of C
    for (int i = 1; i < N; i++) {

        // Adding the number of
        // divisors in count
        count += countDivisors(N - i);
    }

    // Return count of triplets
    return count;
}

// Driver Code
int main()
{
    int N = 10;
    cout << possibleTriplets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

      // Function to find the divisors of
    // the number (N - i)
    static int countDivisors(int n)
    {

        // Stores the resultant count of
        // divisors of (N - i)
        int divisors = 0;
        int i;

        // Iterate over range [1, sqrt(N)]
        for (i = 1; i * i < n; i++) {
            if (n % i == 0) {
                divisors++;
            }
        }
        if (i - (n / i) == 1) {
            i--;
        }
        for (; i >= 1; i--) {
            if (n % i == 0) {
                divisors++;
            }
        }

        // Return the total divisors
        return divisors;
    }

    // Function to find the number of triplets
    // such that A * B - C = N
    static int possibleTriplets(int N)
    {
        int count = 0;

        // Loop to fix the value of C
        for (int i = 1; i < N; i++) {

            // Adding the number of
            // divisors in count
            count += countDivisors(N - i);
        }

        // Return count of triplets
        return count;
    }

    // Driver Code
    public static void main (String[] args) {

        int N = 10;
        System.out.println(possibleTriplets(N));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# function to find the divisors of
# the number (N - i)
def countDivisors(n):

    # Stores the resultant count of
    # divisors of (N - i)
    divisors = 0

    # Iterate over range [1, sqrt(N)]
    for i in range(1, math.ceil(math.sqrt(n))+1):
        if n % i == 0:
            divisors = divisors+1

        if (i - (n / i) == 1):
            i = i-1

    for i in range(math.ceil(math.sqrt(n))+1, 1, -1):
        if (n % i == 0):
            divisors = divisors+1

     # Return the total divisors
    return divisors

    # def to find the number of triplets
    # such that A * B - C = N

def possibleTriplets(N):
    count = 0

    # Loop to fix the value of C
    for i in range(1, N):

        # Adding the number of
        # divisors in count
        count = count + countDivisors(N - i)

        # Return count of triplets
    return count

    # Driver Code
# Driver Code
if __name__ == "__main__":
    N = 10
    print(possibleTriplets(N))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the divisors of
// the number (N - i)
static int countDivisors(int n)
{
    // Stores the resultant count of
    // divisors of (N - i)
    int divisors = 0;
    int i;

    // Iterate over range [1, sqrt(N)]
    for (i = 1; i * i < n; i++) {
        if (n % i == 0) {
            divisors++;
        }
    }
    if (i - (n / i) == 1) {
        i--;
    }
    for (; i >= 1; i--) {
        if (n % i == 0) {
            divisors++;
        }
    }
    // Return the total divisors
    return divisors;
}

// Function to find the number of triplets
// such that A * B - C = N
static int possibleTriplets(int N)
{
    int count = 0;

    // Loop to fix the value of C
    for (int i = 1; i < N; i++) {

        // Adding the number of
        // divisors in count
        count += countDivisors(N - i);
    }

    // Return count of triplets
    return count;
}

// Driver Code
public static void Main()
{
    int N = 10;
    Console.Write(possibleTriplets(N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// javascript program for the above approach
      // Function to find the divisors of
    // the number (N - i)
    function countDivisors(n)
    {

        // Stores the resultant count of
        // divisors of (N - i)
        var divisors = 0;
        var i;

        // Iterate over range [1, sqrt(N)]
        for (i = 1; i * i < n; i++) {
            if (n % i == 0) {
                divisors++;
            }
        }
        if (i - (n / i) == 1) {
            i--;
        }
        for (; i >= 1; i--) {
            if (n % i == 0) {
                divisors++;
            }
        }

        // Return the total divisors
        return divisors;
    }

    // Function to find the number of triplets
    // such that A * B - C = N
    function possibleTriplets(N)
    {
        var count = 0;

        // Loop to fix the value of C
        for (var i = 1; i < N; i++) {

            // Adding the number of
            // divisors in count
            count += countDivisors(N - i);
        }

        // Return count of triplets
        return count;
    }

    // Driver Code
    var N = 10;
    document.write(possibleTriplets(N));

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
23
```

***时间复杂度:** O(N*sqrt(N))*
***辅助空间:** O(1)*
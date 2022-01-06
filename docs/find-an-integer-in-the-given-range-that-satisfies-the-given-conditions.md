# 求给定范围内满足给定条件的整数

> 原文:[https://www . geesforgeks . org/find-满足给定条件的给定范围内的整数/](https://www.geeksforgeeks.org/find-an-integer-in-the-given-range-that-satisfies-the-given-conditions/)

给定两个整数 **L** 和 **R** ，其中 **L ≤ R** ，任务是找到一个整数 **K** ，这样:

1.  **L ≤ K ≤ R** 。
2.  **K** 的所有数字都是不同的。
3.  表达式**(L–K)*(K–R)**的值最大。

如果存在多个答案，则选择 **K** 的较大值。
**例:**

> **输入:** L = 5，R = 10
> **输出:** 8
> **输入:** L = 50，R = 60
> **输出:** 56

**方法:**从 **L** 迭代到 **R** ，对于 **K** 的每个值，检查是否包含所有不同的数字，**(L–K)*(K–R)**最大。如果两个或多个值为表达式给出相同的最大值，则选择 **K** 的较大值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 10;

// Function that returns true if x
// contains all distinct digits
bool distinctDigits(int x)
{
    bool present[MAX] = { false };

    while (x > 0) {

        // Last digit of x
        int digit = x % 10;

        // If current digit has
        // appeared before
        if (present[digit])
            return false;

        // Mark the current digit
        // to present
        present[digit] = true;

        // Remove the last digit
        x /= 10;
    }

    return true;
}

// Function to return the
// required value of k
int findK(int l, int r)
{

    // To store the maximum value
    // for the given expression
    int maxExp = INT_MIN;
    int k = -1;
    for (int i = l; i <= r; i++) {

        // If i contains all distinct digits
        if (distinctDigits(i)) {
            int exp = (l - i) * (i - r);

            // If the value of the expression
            // is also maximum then update k
            // and the expression
            if (exp >= maxExp) {
                k = i;
                maxExp = exp;
            }
        }
    }

    return k;
}

// Driver code
int main()
{
    int l = 50, r = 60;

    cout << findK(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAX = 10;

// Function that returns true if x
// contains all distinct digits
static boolean distinctDigits(int x)
{
    boolean []present = new boolean[MAX];

    while (x > 0)
    {

        // Last digit of x
        int digit = x % 10;

        // If current digit has
        // appeared before
        if (present[digit])
            return false;

        // Mark the current digit
        // to present
        present[digit] = true;

        // Remove the last digit
        x /= 10;
    }

    return true;
}

// Function to return the
// required value of k
static int findK(int l, int r)
{

    // To store the maximum value
    // for the given expression
    int maxExp = Integer.MIN_VALUE;
    int k = -1;
    for (int i = l; i <= r; i++)
    {

        // If i contains all distinct digits
        if (distinctDigits(i))
        {
            int exp = (l - i) * (i - r);

            // If the value of the expression
            // is also maximum then update k
            // and the expression
            if (exp >= maxExp)
            {
                k = i;
                maxExp = exp;
            }
        }
    }

    return k;
}

// Driver code
public static void main(String[] args)
{
    int l = 50, r = 60;

    System.out.print(findK(l, r));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys
MAX = 10

# Function that returns true if x
# contains all distinct digits
def distinctDigits(x):
    present = [False for i in range(MAX)]

    while (x > 0):

        # Last digit of x
        digit = x % 10

        # If current digit has
        # appeared before
        if (present[digit]):
            return False

        # Mark the current digit
        # to present
        present[digit] = True

        # Remove the last digit
        x = x // 10

    return True

# Function to return the
# required value of k
def findK(l, r):

    # To store the maximum value
    # for the given expression
    maxExp = -sys.maxsize - 1
    k = -1
    for i in range(l, r + 1, 1):

        # If i contains all distinct digits
        if (distinctDigits(i)):
            exp = (l - i) * (i - r)

            # If the value of the expression
            # is also maximum then update k
            # and the expression
            if (exp >= maxExp):
                k = i;
                maxExp = exp
    return k

# Driver code
if __name__ == '__main__':
    l = 50
    r = 60

    print(findK(l, r))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 10;

// Function that returns true if x
// contains all distinct digits
static bool distinctDigits(int x)
{
    bool []present = new bool[MAX];

    while (x > 0)
    {

        // Last digit of x
        int digit = x % 10;

        // If current digit has
        // appeared before
        if (present[digit])
            return false;

        // Mark the current digit
        // to present
        present[digit] = true;

        // Remove the last digit
        x /= 10;
    }
    return true;
}

// Function to return the
// required value of k
static int findK(int l, int r)
{

    // To store the maximum value
    // for the given expression
    int maxExp = int.MinValue;
    int k = -1;
    for (int i = l; i <= r; i++)
    {

        // If i contains all distinct digits
        if (distinctDigits(i))
        {
            int exp = (l - i) * (i - r);

            // If the value of the expression
            // is also maximum then update k
            // and the expression
            if (exp >= maxExp)
            {
                k = i;
                maxExp = exp;
            }
        }
    }
    return k;
}

// Driver code
public static void Main(String[] args)
{
    int l = 50, r = 60;

    Console.Write(findK(l, r));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
var MAX = 10;

    // Function that returns true if x
    // contains all distinct digits
    function distinctDigits(x)
    {
        var present = new Array(MAX).fill(false);

        while (x > 0) {

            // Last digit of x
            var digit = x % 10;

            // If current digit has
            // appeared before
            if (present[digit])
                return false;

            // Mark the current digit
            // to present
            present[digit] = true;

            // Remove the last digit
            x = parseInt(x/10);
        }

        return true;
    }

    // Function to return the
    // required value of k
    function findK(l , r) {

        // To store the maximum value
        // for the given expression
        var maxExp = Number.MIN_VALUE;
        var k = -1;
        for (var i = l; i <= r; i++) {

            // If i contains all distinct digits
            if (distinctDigits(i)) {
                var exp = (l - i) * (i - r);

                // If the value of the expression
                // is also maximum then update k
                // and the expression
                if (exp >= maxExp) {
                    k = i;
                    maxExp = exp;
                }
            }
        }

        return k;
    }

    // Driver code
        var l = 50, r = 60;
        document.write(findK(l, r));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
56
```
# 包含至少一个除 K 的数字的[L，R]范围内的数字计数

> 原文:[https://www . geeksforgeeks . org/从范围-l-r-中计数数字，其中包含至少一个数字来除-k/](https://www.geeksforgeeks.org/count-of-numbers-from-the-range-l-r-which-contains-at-least-one-digit-that-divides-k/)

给定三个正整数 **L** 、 **R** 和 **K** 。任务是从包含至少一个数字的范围**【L，R】**中找到所有数字的计数，该数字除以数字 **K** 。

**示例:**

> **输入:** L = 5，R = 11，K = 10
> **输出:** 3
> 5，10，11 只是这样的数字。
> 
> **输入:** L = 32，R = 38，K = 13
> T3】输出: 0

**方法:**初始化**计数= 0** 并且对于范围**【L，R】**中的每个元素，检查它是否包含至少一个除 **K** 的数字。如果是，则增加计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if num
// contains at least one digit
// that divides k
bool digitDividesK(int num, int k)
{
    while (num) {

        // Get the last digit
        int d = num % 10;

        // If the digit is non-zero
        // and it divides k
        if (d != 0 and k % d == 0)
            return true;

        // Remove the last digit
        num = num / 10;
    }

    // There is no digit in num
    // that divides k
    return false;
}

// Function to return the required
// count of elements from the given
// range which contain at least one
// digit that divides k
int findCount(int l, int r, int k)
{

    // To store the result
    int count = 0;

    // For every number from the range
    for (int i = l; i <= r; i++) {

        // If any digit of the current
        // number divides k
        if (digitDividesK(i, k))
            count++;
    }
    return count;
}

// Driver code
int main()
{
    int l = 20, r = 35;
    int k = 45;

    cout << findCount(l, r, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
    // Function that returns true if num
    // contains at least one digit
    // that divides k
    static boolean digitDividesK(int num, int k)
    {
        while (num != 0)
        {

            // Get the last digit
            int d = num % 10;

            // If the digit is non-zero
            // and it divides k
            if (d != 0 && k % d == 0)
                return true;

            // Remove the last digit
            num = num / 10;
        }

        // There is no digit in num
        // that divides k
        return false;
    }

    // Function to return the required
    // count of elements from the given
    // range which contain at least one
    // digit that divides k
    static int findCount(int l, int r, int k)
    {

        // To store the result
        int count = 0;

        // For every number from the range
        for (int i = l; i <= r; i++)
        {

            // If any digit of the current
            // number divides k
            if (digitDividesK(i, k))
                count++;
        }
        return count;
    }

    // Driver code
    public static void main(String []args)
    {
        int l = 20, r = 35;
        int k = 45;

        System.out.println(findCount(l, r, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if num
# contains at least one digit
# that divides k
def digitDividesK(num, k):
    while (num):

        # Get the last digit
        d = num % 10

        # If the digit is non-zero
        # and it divides k
        if (d != 0 and k % d == 0):
            return True

        # Remove the last digit
        num = num // 10

    # There is no digit in num
    # that divides k
    return False

# Function to return the required
# count of elements from the given
# range which contain at least one
# digit that divides k
def findCount(l, r, k):

    # To store the result
    count = 0

    # For every number from the range
    for i in range(l, r + 1):

        # If any digit of the current
        # number divides k
        if (digitDividesK(i, k)):
            count += 1

    return count

# Driver code
l = 20
r = 35
k = 45

print(findCount(l, r, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function that returns true if num
    // contains at least one digit
    // that divides k
    static bool digitDividesK(int num, int k)
    {
        while (num != 0)
        {

            // Get the last digit
            int d = num % 10;

            // If the digit is non-zero
            // and it divides k
            if (d != 0 && k % d == 0)
                return true;

            // Remove the last digit
            num = num / 10;
        }

        // There is no digit in num
        // that divides k
        return false;
    }

    // Function to return the required
    // count of elements from the given
    // range which contain at least one
    // digit that divides k
    static int findCount(int l, int r, int k)
    {

        // To store the result
        int count = 0;

        // For every number from the range
        for (int i = l; i <= r; i++)
        {

            // If any digit of the current
            // number divides k
            if (digitDividesK(i, k))
                count++;
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int l = 20, r = 35;
        int k = 45;

        Console.WriteLine(findCount(l, r, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if num
// contains at least one digit
// that divides k
function digitDividesK(num, k)
{
    while (num)
    {

        // Get the last digit
        let d = num % 10;

        // If the digit is non-zero
        // and it divides k
        if (d != 0 && k % d == 0)
            return true;

        // Remove the last digit
        num = parseInt(num / 10);
    }

    // There is no digit in num
    // that divides k
    return false;
}

// Function to return the required
// count of elements from the given
// range which contain at least one
// digit that divides k
function findCount(l, r, k)
{

    // To store the result
    let count = 0;

    // For every number from the range
    for(let i = l; i <= r; i++)
    {

        // If any digit of the current
        // number divides k
        if (digitDividesK(i, k))
            count++;
    }
    return count;
}

// Driver code
let l = 20, r = 35;
let k = 45;

document.write(findCount(l, r, k));

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
10
```
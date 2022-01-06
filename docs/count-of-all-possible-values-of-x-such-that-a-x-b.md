# 计算 X 的所有可能值，使得 A % X = B

> 原文:[https://www . geesforgeks . org/count-of-x-so-a-x-b/](https://www.geeksforgeeks.org/count-of-all-possible-values-of-x-such-that-a-x-b/)

给定两个整数 **A** 和 **B** 。任务是找到所有可能值的计数 **X** 这样 **A % X = B** 。如果有无限多个可能值，则打印 **-1** 。
**举例:**

> **输入:** A = 21，B = 5
> **输出:** 2
> 8 和 16 是 X 的唯一有效值。
> **输入:** A = 5，B = 5
> **输出:** -1
> X 可以有任意值> 5

**方法:**有三种可能的情况:

1.  如果 **A < B** 那么 **X** 的值都不能满足给定的条件。
2.  如果 **A = B** 那么无限解是可能的。因此，将 **-1** 打印为 **X** 可以是大于 **A** 的任何值。
3.  如果 **A > B** 那么**(A–B)**大于 **B** 的[除数](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)就是需要的计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of all possible values for x
// such that (A % x) = B
int countX(int a, int b)
{
    // Case 1
    if (b > a)
        return 0;

    // Case 2
    else if (a == b)
        return -1;

    // Case 3
    else {
        int x = a - b, ans = 0;

        // Find the number of divisors of x
        // which are greater than b
        for (int i = 1; i * i <= x; i++) {
            if (x % i == 0) {
                int d1 = i, d2 = b - 1;
                if (i * i != x)
                    d2 = x / i;
                if (d1 > b)
                    ans++;
                if (d2 > b)
                    ans++;
            }
        }
        return ans;
    }
}

// Driver code
int main()
{
    int a = 21, b = 5;

    cout << countX(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count
    // of all possible values for x
    // such that (A % x) = B
    static int countX(int a, int b)
    {
        // Case 1
        if (b > a)
            return 0;

        // Case 2
        else if (a == b)
            return -1;

        // Case 3
        else
        {
            int x = a - b, ans = 0;

            // Find the number of divisors of x
            // which are greater than b
            for (int i = 1; i * i <= x; i++)
            {
                if (x % i == 0)
                {
                    int d1 = i, d2 = b - 1;
                    if (i * i != x)
                        d2 = x / i;
                    if (d1 > b)
                        ans++;
                    if (d2 > b)
                        ans++;
                }
            }
            return ans;
        }
    }

    // Driver code
    static public void main (String args[])
    {
        int a = 21, b = 5;

        System.out.println(countX(a, b));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of all possible values for x
# such that (A % x) = B
def countX( a, b):
    # Case 1
    if (b > a):
        return 0

    # Case 2
    elif (a == b):
        return -1

    # Case 3
    else:
        x = a - b
        ans = 0

        # Find the number of divisors of x
        # which are greater than b
        i = 1
        while i * i <= x:
            if (x % i == 0):
                d1 = i
                d2 = b - 1
                if (i * i != x):
                    d2 = x // i
                if (d1 > b):
                    ans+=1
                if (d2 > b):
                    ans+=1
            i+=1
        return ans

# Driver code
if __name__ == "__main__":
    a = 21
    b = 5

    print(countX(a, b))

    # This code is contributed by ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of all possible values for x
    // such that (A % x) = B
    static int countX(int a, int b)
    {
        // Case 1
        if (b > a)
            return 0;

        // Case 2
        else if (a == b)
            return -1;

        // Case 3
        else
        {
            int x = a - b, ans = 0;

            // Find the number of divisors of x
            // which are greater than b
            for (int i = 1; i * i <= x; i++)
            {
                if (x % i == 0)
                {
                    int d1 = i, d2 = b - 1;
                    if (i * i != x)
                        d2 = x / i;
                    if (d1 > b)
                        ans++;
                    if (d2 > b)
                        ans++;
                }
            }
            return ans;
        }
    }

    // Driver code
    static public void Main ()
    {
        int a = 21, b = 5;

        Console.WriteLine(countX(a, b));

    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of all possible values for x
// such that (A % x) = B
function countX(a, b)
{
    // Case 1
    if (b > a)
        return 0;

    // Case 2
    else if (a == b)
        return -1;

    // Case 3
    else {
        let x = a - b, ans = 0;

        // Find the number of divisors of x
        // which are greater than b
        for (let i = 1; i * i <= x; i++) {
            if (x % i == 0) {
                let d1 = i, d2 = b - 1;
                if (i * i != x)
                    d2 = parseInt(x / i);
                if (d1 > b)
                    ans++;
                if (d2 > b)
                    ans++;
            }
        }
        return ans;
    }
}

// Driver code
    let a = 21, b = 5;

    document.write(countX(a, b));

</script>
```

**Output:** 

```
2
```
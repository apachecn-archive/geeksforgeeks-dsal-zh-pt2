# 找到一个 N 位数，这样它就不能被它的任何一个数字整除

> 原文:[https://www . geesforgeks . org/find-a-n-digit-number-so-它不能被它的任何数字-2 除尽/](https://www.geeksforgeeks.org/find-a-n-digit-number-such-that-it-is-not-divisible-by-any-of-its-digits-2/)

给定一个整数 N，任务是找到一个 N 位数，这样它就不能被它的任何位数整除。
**注:**n 的每个值可以有多个答案

**示例:**

> **输入:** N = 4
> **输出:** 6789
> **说明:**
> 由于数字 6789 不能被其任何一位数字整除，所以是 6、7、8、9，也是四位数。因此，它可以是所需的数字。
> 
> **输入:** N = 2
> **输出:** 57
> **说明:**
> 由于数字 57 不能被其任何一个数字整除，所以是 5 和 7，也是 2 位数。因此，它可以是所需的数字。

**进场:**问题中的关键观察是 2 和 3 是那些不相除的数字。另外，数字“23，233，2333，…”既不能被 2 整除，也不能被 3 整除。因此，对于任何 N 位数字，最高有效位将是 2，其余数字将是 3，以获得所需的数字。

**算法:**

*   检查 N 的值是否等于 1，那么没有这样的数字是可能的，因此返回-1。
*   否则，初始化一个变量 **num** ，以 2 存储该数。
*   运行一个从 1 到 N 的循环，然后，对于每次迭代，将数字乘以 10，再加上 3。

```
num = (num * 10) + 3 
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find a
// N-digit number such that the number
// it is not divisible by its digits

#include <bits/stdc++.h>
using namespace std;

typedef long long int ll;

// Function to find the number
// such that it is not divisible
// by its digits
void solve(ll n)
{
    // Base Cases
    if (n == 1)
    {
        cout << -1;
    }
    else {

        // First Digit of the
        // number will be 2
        int num = 2;

        // Next digits of the numbers
        for (ll i = 0; i < n - 1; i++) {
            num = (num * 10) + 3;
        }
        cout << num;
    }
}

// Driver Code
int main()
{
    ll n = 4;

    // Function Call
    solve(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find a
// N-digit number such that the number
// it is not divisible by its digits
class GFG {

    long ll;

    // Function to find the number
    // such that it is not divisible
    // by its digits
    static void solve(long n)
    {
        // Base Cases
        if (n == 1)
        {
            System.out.println(-1);
        }
        else {

            // First Digit of the
            // number will be 2
            int num = 2;

            // Next digits of the numbers
            for (long i = 0; i < n - 1; i++) {
                num = (num * 10) + 3;
            }
            System.out.println(num);
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        long n = 4;

            // Function Call
            solve(n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to find a
# N-digit number such that the number
# it is not divisible by its digits

# Function to find the number
# such that it is not divisible
# by its digits
def solve(n) :

    # Base Cases
    if (n == 1) :

        print(-1);

    else :

        # First Digit of the
        # number will be 2
        num = 2;

        # Next digits of the numbers
        for i in range(n - 1) :
            num = (num * 10) + 3;

        print(num);

# Driver Code
if __name__ == "__main__" :

    n = 4;

    # Function Call
    solve(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find a
// N-digit number such that the number
// it is not divisible by its digits
using System;

class GFG {

    long ll;

    // Function to find the number
    // such that it is not divisible
    // by its digits
    static void solve(long n)
    {
        // Base Cases
        if (n == 1)
        {
            Console.WriteLine(-1);
        }
        else {

            // First Digit of the
            // number will be 2
            int num = 2;

            // Next digits of the numbers
            for (long i = 0; i < n - 1; i++) {
                num = (num * 10) + 3;
            }
            Console.WriteLine(num);
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        long n = 4;

            // Function Call
            solve(n);
    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
//Javascript  implementation to find a
// N-digit number such that the number
// it is not divisible by its digits

// Function to find the number
// such that it is not divisible
// by its digits
function solve(n)
{
    // Base Cases
    if (n == 1)
    {
        document.write(  -1);
    }
    else {

        // First Digit of the
        // number will be 2
        var num = 2;

        // Next digits of the numbers
        for (var i = 0; i < n - 1; i++) {
            num = (num * 10) + 3;
        }
        document.write(  num);
    }
}

// Given N
var n = 4;
// Function Call
solve(n);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2333
```

**业绩分析:**

*   **时间复杂度:** O(N)。
*   **辅助空间:** O(1)。
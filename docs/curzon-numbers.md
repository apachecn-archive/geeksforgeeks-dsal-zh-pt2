# 寇松号

> 原文:[https://www.geeksforgeeks.org/curzon-numbers/](https://www.geeksforgeeks.org/curzon-numbers/)

给定一个整数 **N** ，检查给定的数字是否为**寇松号**。

> 如果 **2 <sup>N</sup> + 1** 可被 **2*N + 1** 整除，则一个数字 **N** 被称为**寇松数**。

**示例:**

> **输入:** N = 5
> **输出:** Yes
> **解释:**
> 2^5 + 1 = 33 和 2*5 + 1 = 11
> 既然 11 除以 33，那么 5 就是一个 curzon 数。
> 
> **输入:** N = 10
> **输出:** No
> **解释:**
> 2^10 + 1 = 1025 和 2*10 + 1 = 21
> 1025 不能被 21 整除，所以 10 不是一个 curzon 数。

**方法:**方法是计算并检查 **2 <sup>N</sup> + 1** 是否能被 **2*N + 1** 整除。

*   首先求 **2*N + 1** 的值
*   然后求 **2 <sup>N</sup> + 1** 的值
*   检查第二个值是否能被第一个值整除，那么它就是一个 **Curzon Number** ，否则不是。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is a Curzon number or not
void checkIfCurzonNumber(int N)
{

    long int powerTerm, productTerm;

    // Find 2^N + 1
    powerTerm = pow(2, N) + 1;

    // Find 2*N + 1
    productTerm = 2 * N + 1;

    // Check for divisibility
    if (powerTerm % productTerm == 0)
        cout << "Yes\n";
    else
        cout << "No\n";
}

// Driver code
int main()
{
    long int N = 5;
    checkIfCurzonNumber(N);

    N = 10;
    checkIfCurzonNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG {

// Function to check if a number
// is a Curzon number or not
static void checkIfCurzonNumber(long N)
{
    double powerTerm, productTerm;

    // Find 2^N + 1
    powerTerm = Math.pow(2, N) + 1;

    // Find 2*N + 1
    productTerm = 2 * N + 1;

    // Check for divisibility
    if (powerTerm % productTerm == 0)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    long N = 5;
    checkIfCurzonNumber(N);

    N = 10;
    checkIfCurzonNumber(N);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check if a number
# is a Curzon number or not
def checkIfCurzonNumber(N):

    powerTerm, productTerm = 0, 0

    # Find 2^N + 1
    powerTerm = pow(2, N) + 1

    # Find 2*N + 1
    productTerm = 2 * N + 1

    # Check for divisibility
    if (powerTerm % productTerm == 0):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':

    N = 5
    checkIfCurzonNumber(N)

    N = 10
    checkIfCurzonNumber(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to check if a number
// is a curzon number or not
static void checkIfCurzonNumber(long N)
{
    double powerTerm, productTerm;

    // Find 2^N + 1
    powerTerm = Math.Pow(2, N) + 1;

    // Find 2*N + 1
    productTerm = 2 * N + 1;

    // Check for divisibility
    if (powerTerm % productTerm == 0)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
static public void Main ()
{
    long N = 5;
    checkIfCurzonNumber(N);

    N = 10;
    checkIfCurzonNumber(N);
}
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check if a number
// is a Curzon number or not
function checkIfCurzonNumber(N)
{
    var powerTerm, productTerm;

    // Find 2^N + 1
    powerTerm = Math.pow(2, N) + 1;

    // Find 2*N + 1
    productTerm = 2 * N + 1;

    // Check for divisibility
    if (powerTerm % productTerm == 0)
    {
        document.write("Yes" + "</br>");
    }
    else
    {
        document.write("No");
    }
}

// Driver code
var N = 5;
checkIfCurzonNumber(N);

N = 10;
checkIfCurzonNumber(N);

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
Yes
No
```

***时间复杂度:** O(对数 N)*

***辅助空间:**O(1)*T4】
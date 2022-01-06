# D 数字

> 原文:[https://www.geeksforgeeks.org/d-numbers/](https://www.geeksforgeeks.org/d-numbers/)

**D 数字**是数字 **N** > 3，使得 n 用 gcd(k，n) = 1，1 对所有 k 除 k^(n-2)-k<k<n .

> 9, 15, 21, 33, 39, 51, 57, 63, 69, 87, 93….

### 检查一个数字是否是数字

给定一个数字 **N** ，任务是检查 **N** 是否为 **D 号**。如果 **N** 是 D 号，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 9
> **输出:** Yes
> **解释:**
> 9 是一个 d 数，因为它除了所有的数字
> 2^7-2、4^7-4、5^7-5、7^7-7 和 8^7-8，而
> 2、4、5、7、8 相对于 n 是素数。
> **输入:** N = 16
> **输出:** No

**方法:**由于 d 数是一个数**n**T6】3，所以 n 用 gcd(k，n) = 1，1 < k < n 对所有 k 除 k^(n-2)-k，所以在 k 从 2 到 n-1 的循环中，我们将检查 n 和 k 的 gcd 是否为 1。如果它是 1，那么我们将检查 k^(n-2)-k 是否能被 n 整除。如果不可分，我们将返回 false。最后我们会回到现实。
以下是上述方法的实施:

## C++

```
// C++ implementation
// for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the N-th
// icosikaipentagon number
int isDNum(int n)
{
    // number should be
    // greater than 3
    if (n < 4)
        return false;

    int numerator, hcf;

    // Check every k in range 2 to n-1
    for (int k = 2; k <= n; k++)
    {
        numerator = pow(k, n - 2) - k;
        hcf = __gcd(n, k);
    }

    // condition for D-Number
    if (hcf == 1 && (numerator % n) != 0)
        return false;

    return true;
}

// Driver Code
int main()
{
    int n = 15;
    int a = isDNum(n);
    if (a)
        cout << "Yes";
    else
        cout << "No";
}

// This code is contributed by Ritik Bansal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the
// above approach
import java.util.*;

class GFG{

// Function to find the N-th
// icosikaipentagon number
static boolean isDNum(int n)
{

    // Number should be
    // greater than 3
    if (n < 4)
        return false;

    int numerator = 0, hcf = 0;

    // Check every k in range 2 to n-1
    for(int k = 2; k <= n; k++)
    {
       numerator = (int)(Math.pow(k, n - 2) - k);
       hcf = __gcd(n, k);
    }

    // Condition for D-Number
    if (hcf == 1 && (numerator % n) != 0)
        return false;

    return true;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    int n = 15;
    boolean a = isDNum(n);

    if (a)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation
# for the above approach

import math

# Function to find the N-th
# icosikaipentagon number
def isDNum(n):
    # number should be
        # greater than 3
    if n < 4:
        return False

    # Check every k in range 2 to n-1
    for k in range(2, n):
        numerator = pow(k, n - 2) - k
        hcf = math.gcd(n, k)

        # condition for D-Number
        if(hcf ==1 and (numerator % n) != 0):
            return False
    return True

# Driver code
n = 15
if isDNum(n):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation for the
// above approach
using System;
class GFG{

// Function to find the N-th
// icosikaipentagon number
static bool isDNum(int n)
{

    // Number should be
    // greater than 3
    if (n < 4)
        return false;

    int numerator = 0, hcf = 0;

    // Check every k in range 2 to n-1
    for(int k = 2; k <= n; k++)
    {
        numerator = (int)(Math.Pow(k, n - 2) - k);
        hcf = __gcd(n, k);
    }

    // Condition for D-Number
    if (hcf == 1 && (numerator % n) != 0)
        return false;

    return true;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    int n = 15;
    bool a = isDNum(n);

    if (a)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation for the
// above approach

    // Function to find the N-th
    // icosikaipentagon number
    function isDNum( n) {

        // Number should be
        // greater than 3
        if (n < 4)
            return false;

        let numerator = 0, hcf = 0;

        // Check every k in range 2 to n-1
        for ( k = 2; k <= n; k++) {
            numerator = parseInt( (Math.pow(k, n - 2) - k));
            hcf = __gcd(n, k);
        }

        // Condition for D-Number
        if (hcf == 1 && (numerator % n) != 0)
            return false;

        return true;
    }

    function __gcd( a, b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver Code

        let n = 15;
        let a = isDNum(n);

        if (a)
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(1)*
T5】参考 : [OEIS](https://oeis.org/A033553)
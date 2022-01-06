# 通过应用给定的操作

最小化 N 的值

> 原文:[https://www . geeksforgeeks . org/通过应用给定的操作最小化 n 的值/](https://www.geeksforgeeks.org/minimize-the-value-of-n-by-applying-the-given-operations/)

给定一个整数 *N* ，以下操作可以在 *N* :
上执行任意次

1.  将 *N* 乘以任意正整数 *X* ，即 *N = N * X* 。
2.  将 *N* 替换为 *N* ( *N* 必须为整数)的平方根，即 *N = sqrt(N)* 。

任务是通过以上操作找到 *N* 可以约简到的最小整数。
**例:**

> **输入:** N = 20
> **输出:** 10
> 我们可以将 20 乘以 5，然后取 sqrt(20*5) = 10，这是给定运算下 20 可以减少到的最小数。
> **输入** : N = 36
> **输出:** 6
> 取 sqrt(36)。6 号不能再降了。

**进场:**

1.  首先对数字 *N* 进行因子分解。
2.  说起来， *12* 有因素 *2、2、5* 。只有重复的因素才能用 *sqrt(n)* 减少，即 *sqrt(2*2) = 2* 。
3.  因子中只出现一次的数字不能再减少了。
4.  所以，最终的答案将是所有不同质因数的乘积

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// function to return the product of
// distinct prime factors of a number
ll minimum(ll n)
{
    ll product = 1;

    // find distinct prime
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            while (n % i == 0)
                n = n / i;
            product = product * i;
        }
    }
    if (n >= 2)
        product = product * n;

    return product;
}

// Driver code
int main()
{
    ll n = 20;
    cout << minimum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class solution
{

 // function to return the product of
 // distinct prime factors of a number
static int minimum(int n)
{
    int product = 1;

    // find distinct prime
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            while (n % i == 0)
                n = n / i;
            product = product * i;
        }
    }
    if (n >= 2)
        product = product * n;

    return product;
}

// Driver code
public static void main(String arr[])
{
    int n = 20;
    System.out.println(minimum(n));

}
}
//This code is contributed by
//Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# function to return the product
# of distinct prime factors of a
# numberdef minSteps(str):
def minimum(n):

    product = 1

    # find distinct prime
    i = 2
    while i * i <= n:
        if n % i == 0:
            while n % i == 0:
                n = n / i
            product = product * i
        i = i + 1
    if n >= 2:
        product = product * n
    return product

# Driver code

# Get the binary string
n = 20
print(minimum(n))

# This code is contributed
# by Shashank_Sharma
```

## C#

```
// C# implementation of the above approach
class GFG
{

// function to return the product of
// distinct prime factors of a number
static int minimum(int n)
{
    int product = 1;

    // find distinct prime
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            while (n % i == 0)
                n = n / i;
            product = product * i;
        }
    }
    if (n >= 2)
        product = product * n;

    return product;
}

// Driver code
static void Main()
{
    int n = 20;
    System.Console.WriteLine(minimum(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// function to return the product of
// distinct prime factors of a number
function minimum($n)
{
    $product = 1;

    // find distinct prime
    for ($i = 2; $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {
            while ($n % $i == 0)
                $n = $n / $i;
            $product = $product * $i;
        }
    }
    if ($n >= 2)
        $product = $product * $n;

    return $product;
}

// Driver code
$n = 20;
echo minimum($n),"\n";

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// function to return the product of
// distinct prime factors of a number
function minimum( n)
{
    let product = 1;

    // find distinct prime
    for (let i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            while (n % i == 0)
                n = n / i;
            product = product * i;
        }
    }
    if (n >= 2)
        product = product * n;

    return product;
}

// Driver code

    let n = 20;
    document.write(minimum(n));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
10
```
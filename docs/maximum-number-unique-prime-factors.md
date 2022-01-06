# 唯一质因数的最大数量

> 原文:[https://www . geesforgeks . org/最大数-唯一-质因数/](https://www.geeksforgeeks.org/maximum-number-unique-prime-factors/)

给定一个数 N，求任意数在[1，N]范围内唯一质因数的最大数。
**例:**

```
Input : N = 500
Output : 4
The maximum number of prime factors
for any number in [1, 500] is 4\. A
number in range that has 4 prime 
factors is 210 (2 x 3 x 5 x 7)

Input  : N = 3
Output : 1

Input : N = 5000
Output : 5
```

**方法 1(蛮力):**
对于 1 到 N 的每个整数，[求每个整数的素因子个数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) r，求最大唯一素因子个数。
**方法 2(更好的方法):**
使用[筛选法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)对每个小于 n 的数的质因数进行计数，找出计数最大的最小数。
以下是本办法的实施情况:

## C++

```
// C++ program to find maximum number of prime
// factors for a number in range [1, N]
#include <bits/stdc++.h>
using namespace std;

// Return smallest number having maximum
// prime factors.
int maxPrimefactorNum(int N)
{
    // Sieve of eratosthenes method to count
    // number of unique prime factors.
    int arr[N + 1];
    memset(arr, 0, sizeof(arr));
    for (int i = 2; i * i <= N; i++) {
        if (!arr[i])
            for (int j = 2 * i; j <= N; j += i)
                arr[j]++;

        arr[i] = 1;
    }

    // Return maximum element in arr[]
    return *max_element(arr, arr+N);
}

// Driven Program
int main()
{
    int N = 40;
    cout << maxPrimefactorNum(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// number of prime factors for
// a number in range [1, N]
class GFG
{
static int getMax(int[] Arr)
{
    int max = Arr[0];
    for(int i = 1; i < Arr.length; i++)
    if(Arr[i] > max)
        max = Arr[i];
    return max;
}

// Return smallest number
// having maximum prime factors.
static int maxPrimefactorNum(int N)
{
    // Sieve of eratosthenes method
    // to count number of unique
    // prime factors.
    int[] arr = new int[N + 1];
    for (int i = 2; i * i <= N; i++)
    {
        if (arr[i] == 0)
            for (int j = 2 * i; j <= N; j += i)
                arr[j]++;

        arr[i] = 1;
    }

    // Return maximum element in arr[]
    return getMax(arr);
}

// Driver Code
public static void main(String[] args)
{
    int N = 40;
    System.out.println(maxPrimefactorNum(N));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find maximum number
# of prime factors for a number in range [1, N]

# Return smallest number having maximum
# prime factors.
def maxPrimefactorNum(N):

    # Sieve of eratosthenes method to count
    # number of unique prime factors.
    arr = [0] * (N + 1);
    i = 2;
    while (i * i <= N):
        if (arr[i] > 0):
            for j in range(2 * i, N + 1, i):
                arr[j] += 1;
        i += 1;

        arr[i] = 1;

    # Return maximum element in arr[]
    return max(arr);

# Driver Code
N = 40;
print(maxPrimefactorNum(N));

# This code is contributed by mits
```

## C#

```
// C# program to find maximum
// number of prime factors for
// a number in range [1, N]
using System;

class GFG
{
static int getMax(int[] Arr)
{
    int max = Arr[0];
    for(int i = 1; i < Arr.Length; i++)
    if(Arr[i] > max)
        max = Arr[i];
    return max;
}

// Return smallest number
// having maximum prime factors.
static int maxPrimefactorNum(int N)
{
    // Sieve of eratosthenes method
    // to count number of unique
    // prime factors.
    int[] arr = new int[N + 1];
    for (int i = 2; i * i <= N; i++)
    {
        if (arr[i] == 0)
            for (int j = 2 * i;
                     j <= N; j += i)
                arr[j]++;

        arr[i] = 1;
    }

    // Return maximum
    // element in arr[]
    return getMax(arr);
}

// Driver Code
public static void Main()
{
    int N = 40;
    Console.WriteLine(maxPrimefactorNum(N));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum number of prime
// factors for a number in range [1, N]

// Return smallest number having maximum
// prime factors.
function maxPrimefactorNum($N)
{
    // Sieve of eratosthenes method to count
    // number of unique prime factors.
    $arr = array_fill(0, $N + 1, 0);
    for ($i = 2; $i * $i <= $N; $i++)
    {
        if (!$arr[$i])
            for ($j = 2 * $i; $j <= $N; $j += $i)
                $arr[$j]++;

        $arr[$i] = 1;
    }

    // Return maximum element in arr[]
    return max($arr);
}

// Driver Code
$N = 40;
echo maxPrimefactorNum($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum
// number of prime factors for
// a number in range [1, N]

function getMax(Arr)
{
    let max = Arr[0];
    for(let i = 1; i < Arr.length; i++)
    if(Arr[i] > max)
        max = Arr[i];
    return max;
}

// Return smallest number
// having maximum prime factors.
function maxPrimefactorNum(N)
{
    // Sieve of eratosthenes method
    // to count number of unique
    // prime factors.
    let arr = new Array(N+1).fill(0);
    for (let i = 2; i * i <= N; i++)
    {
        if (arr[i] == 0)
            for (let j = 2 * i; j <= N; j += i)
                arr[j]++;

        arr[i] = 1;
    }

    // Return maximum element in arr[]
    return getMax(arr);
}

// driver program

       let N = 40;
    document.write(maxPrimefactorNum(N));

</script>
```

**输出:**

```
3
```

**方法 3(有效方法):**
使用[筛选](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成 N 之前的所有素数。现在，将连续的素数(从第一个素数开始)一个接一个地相乘，直到乘积小于 n。这个想法基于一个简单的事实，即第一组素数可以引起最大的唯一素数因子。
以下是本办法的实施:

## C++

```
// C++ program to find maximum number of prime
// factors in first N natural numbers
#include <bits/stdc++.h>
using namespace std;

// Return maximum number of prime factors for
// any number in [1, N]
int maxPrimefactorNum(int N)
{
    if (N < 2)
        return 0;

    // Based on Sieve of Eratosthenes
    // https://www.geeksforgeeks.org/sieve-of-eratosthenes/
    bool arr[N+1];
    memset(arr, true, sizeof(arr));
    int prod = 1, res = 0;
    for (int p=2; p*p<=N; p++)
    {
        // If p is prime
        if (arr[p] == true)
        {
            for (int i=p*2; i<=N; i += p)
                arr[i] = false;

            // We simply multiply first set
            // of prime numbers while the
            // product is smaller than N.
            prod *= p;
            if (prod > N)
                return res;
            res++;
        }
    }

    return res;
}

// Driven Program
int main()
{
    int N = 500;
    cout << maxPrimefactorNum(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// number of prime factors in
// first N natural numbers

class GFG
{
// Return maximum number
// of prime factors for
// any number in [1, N]
static int maxPrimefactorNum(int N)
{
    if (N < 2)
        return 0;

    // Based on Sieve of Eratosthenes
    // https://www.geeksforgeeks.org/sieve-of-eratosthenes/
    boolean[] arr = new boolean[N + 1];
    int prod = 1, res = 0;
    for (int p = 2; p * p <= N; p++)
    {
        // If p is prime
        if (arr[p] == false)
        {
            for (int i = p * 2;
                     i <= N; i += p)
                arr[i] = true;

            // We simply multiply first set
            // of prime numbers while the
            // product is smaller than N.
            prod *= p;
            if (prod > N)
                return res;
            res++;
        }
    }

    return res;
}

// Driver Code
public static void main(String[] args)
{
    int N = 500;
    System.out.println(maxPrimefactorNum(N));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find maximum number
# of prime factors in first N natural numbers

# Return maximum number of prime factors
# for any number in [1, N]
def maxPrimefactorNum(N):

    if (N < 2):
        return 0;

    arr = [True] * (N + 1);
    prod = 1;
    res = 0;
    p = 2;
    while (p * p <= N):

        # If p is prime
        if (arr[p] == True):
            for i in range(p * 2, N + 1, p):
                arr[i] = False;

            # We simply multiply first set
            # of prime numbers while the
            # product is smaller than N.
            prod *= p;
            if (prod > N):
                return res;
            res += 1;
        p += 1;

    return res;

# Driver Code
N = 500;
print(maxPrimefactorNum(N));

# This code is contributed by mits
```

## C#

```
// C# program to find maximum number of
// prime factors in first N natural numbers
using System;

class GFG
{

// Return maximum number of prime
// factors for any number in [1, N]
static int maxPrimefactorNum(int N)
{
    if (N < 2)
        return 0;

    // Based on Sieve of Eratosthenes
    // https://www.geeksforgeeks.org/sieve-of-eratosthenes/
    bool[] arr = new bool[N + 1];
    int prod = 1, res = 0;
    for (int p = 2; p * p <= N; p++)
    {
        // If p is prime
        if (arr[p] == false)
        {
            for (int i = p * 2;
                     i <= N; i += p)
                arr[i] = true;

            // We simply multiply first set
            // of prime numbers while the
            // product is smaller than N.
            prod *= p;
            if (prod > N)
                return res;
            res++;
        }
    }

    return res;
}

// Driver Code
public static void Main()
{
    int N = 500;
    Console.WriteLine(maxPrimefactorNum(N));
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// number of prime factors in
// first N natural numbers

// Return maximum number of
// prime factors for any
// number in [1, N]
function maxPrimefactorNum($N)
{
    if ($N < 2)
        return 0;

    $arr = array_fill(0, ($N + 1), true);
    $prod = 1;
    $res = 0;
    for ($p = 2;
         $p * $p <= $N; $p++)
    {
        // If p is prime
        if ($arr[$p] == true)
        {
            for ($i = $p * 2;
                 $i <= $N; $i += $p)
                $arr[$i] = false;

            // We simply multiply first set
            // of prime numbers while the
            // product is smaller than N.
            $prod *= $p;
            if ($prod > $N)
                return $res;
            $res++;
        }
    }

    return $res;
}

// Driver Code
$N = 500;
echo maxPrimefactorNum($N) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to find maximum
// number of prime factors in
// first N natural numbers

// Return maximum number
// of prime factors for
// any number in [1, N]
function maxPrimefactorNum(N)
{
    if (N < 2)
        return 0;

    // Based on Sieve of Eratosthenes
    // https://www.geeksforgeeks.org/sieve-of-eratosthenes/
    arr = Array.from({length: N + 1}, (_, i) => false);
    var prod = 1, res = 0;
    for (var p = 2; p * p <= N; p++)
    {
        // If p is prime
        if (arr[p] == false)
        {
            for (var i = p * 2;
                     i <= N; i += p)
                arr[i] = true;

            // We simply multiply first set
            // of prime numbers while the
            // product is smaller than N.
            prod *= p;
            if (prod > N)
                return res;
            res++;
        }
    }

    return res;
}

// Driver Code
var N = 500;
document.write(maxPrimefactorNum(N));

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
4
```

本文由 **Mohak Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
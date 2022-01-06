# 找到最大操作数，将 N 减少到 1

> 原文:[https://www . geesforgeks . org/find-max-operations-to-reduce-n-1/](https://www.geeksforgeeks.org/find-maximum-operations-to-reduce-n-to-1/)

给定两个数字 A 和 B ( A 和 B 最多可以是 10 <sup>6</sup> )，组成一个数字 **N = (A！/B！)**。任务是通过执行**最大数量的**操作，将**N 减少到 1** 。
每次操作中，如果 N 能被 X 整除，可以用 **N/X** 代替 N。
找出可能的最大操作数。
**示例:**

```
Input : A = 6, B = 3
Output : 5
Explanation : N is 120 and the divisors are 2, 2, 2, 3, 5

Input : A = 2, B = 1
Output : 1
Explanation : N is 2 and the divisor is 2.
```

观察数 A 因式分解！/B！这和数(B+1)*(B+2)*……*(A–1)* A 的因式分解一样吗？
同样，如果我们只用 N 的素因子来除 N，运算的次数将是最大的。所以，换句话说，我们需要找到包括重复项在内的 N 个质因数的计数。
我们来数一下从 2 到 1000000 每个数的因式分解中质因数的个数。
首先，用厄拉多塞的筛子找出每个数字的素除数。然后，我们可以使用公式
计算 a 的因式分解中质因数的数量

```
primefactors[num] = primefactors[num / primediviser[num]] + 1
```

现在，我们可以用前缀和数组来表示质因数，然后在区间[A，B]上求和。
以下是上述方法的实现:

## C++

```
// CPP program to find maximum
// number moves possible

#include <bits/stdc++.h>
using namespace std;
#define N 1000005

// To store number of prime
// factors of each number
int primeFactors[N];

// Function to find number of prime
// factors of each number
void findPrimeFactors()
{
    for (int i = 2; i < N; i++)
        // if i is a prime number
        if (primeFactors[i] == 0)
            for (int j = i; j < N; j += i)
                // increase value by one from
                // it's preveious multiple
                primeFactors[j] = primeFactors[j / i] + 1;

    // make prefix sum
    // this will be helpful for
    // multiple test cases
    for (int i = 1; i < N; i++)
        primeFactors[i] += primeFactors[i - 1];
}

// Driver Code
int main()
{
    // Generate primeFactors array
    findPrimeFactors();

    int a = 6, b = 3;

    // required answer
    cout << primeFactors[a] - primeFactors[b];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// number moves possible
import java.io.*;

class GFG
{

static int N= 1000005;

// To store number of prime
// factors of each number
static int primeFactors[] = new int[N];

// Function to find number of prime
// factors of each number
static void findPrimeFactors()
{
    for (int i = 2; i < N; i++)

        // if i is a prime number
        if (primeFactors[i] == 0)
            for (int j = i; j < N; j += i)

                // increase value by one from
                // it's preveious multiple
                primeFactors[j] = primeFactors[j / i] + 1;

    // make prefix sum
    // this will be helpful for
    // multiple test cases
    for (int i = 1; i < N; i++)
        primeFactors[i] += primeFactors[i - 1];
}

// Driver Code
public static void main (String[] args)
{

    // Generate primeFactors array
    findPrimeFactors();
    int a = 6, b = 3;

    // required answer
    System.out.println (primeFactors[a] -
                        primeFactors[b]);
}
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python3 program to find maximum
# number moves possible
N = 1000005

# To store number of prime
# factors of each number
primeFactors = [0] * N;

# Function to find number of prime
# factors of each number
def findPrimeFactors() :

    for i in range(2, N) :

        # if i is a prime number
        if (primeFactors[i] == 0) :
            for j in range(i, N, i) :

                # increase value by one from
                # it's preveious multiple
                primeFactors[j] = primeFactors[j // i] + 1;

    # make prefix sum this will be
    # helpful for multiple test cases
    for i in range(1, N) :
        primeFactors[i] += primeFactors[i - 1];

# Driver Code
if __name__ == "__main__" :

    # Generate primeFactors array
    findPrimeFactors();

    a = 6; b = 3;

    # required answer
    print(primeFactors[a] - primeFactors[b]);

# This code is contributed by Ryuga
```

## C#

```
// C# program to find maximum
// number moves possible
using System;

class GFG
{
    static int N = 1000005;

    // To store number of prime
    // factors of each number
    static int []primeFactors = new int[N];

    // Function to find number of prime
    // factors of each number
    static void findPrimeFactors()
    {
        for (int i = 2; i < N; i++)

        // if i is a prime number
        if (primeFactors[i] == 0)
            for (int j = i; j < N; j += i)

                // increase value by one from
                // it's preveious multiple
                primeFactors[j] = primeFactors[j / i] + 1;

        // make prefix sum
        // this will be helpful for
        // multiple test cases
        for (int i = 1; i < N; i++)
            primeFactors[i] += primeFactors[i - 1];
    }

    // Driver Code
    static public void Main ()
    {

    // Generate primeFactors array
    findPrimeFactors();
    int a = 6, b = 3;

    // required answer
    Console.WriteLine(primeFactors[a] -
                        primeFactors[b]);
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// number moves possible

$N = 10005;

// To store number of prime
// factors of each number
$primeFactors = array_fill(0, $N, 0);

// Function to find number of prime
// factors of each number
function findPrimeFactors()
{
    global $N,$primeFactors;
    for ($i = 2; $i < $N; $i++)

        // if i is a prime number
        if ($primeFactors[$i] == 0)
            for ($j = $i; $j < $N; $j += $i)

                // increase value by one from
                // it's preveious multiple
                $primeFactors[$j] = $primeFactors[(int)($j / $i)] + 1;

    // make prefix sum
    // this will be helpful for
    // multiple test cases
    for ($i = 1; $i < $N; $i++)
        $primeFactors[$i] += $primeFactors[$i - 1];
}

    // Driver Code

    // Generate primeFactors array
    findPrimeFactors();

    $a = 6;
    $b = 3;

    // required answer
    print(($primeFactors[$a] - $primeFactors[$b]));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum number moves possible

    let N = 1000005;

    // To store number of prime
    // factors of each number
    let primeFactors = new Array(N);
    primeFactors.fill(0);

    // Function to find number of prime
    // factors of each number
    function findPrimeFactors()
    {
        for (let i = 2; i < N; i++)

        // if i is a prime number
        if (primeFactors[i] == 0)
            for (let j = i; j < N; j += i)

                // increase value by one from
                // it's preveious multiple
                primeFactors[j] = primeFactors[parseInt(j / i, 10)] + 1;

        // make prefix sum
        // this will be helpful for
        // multiple test cases
        for (let i = 1; i < N; i++)
            primeFactors[i] += primeFactors[i - 1];
    }

    // Generate primeFactors array
    findPrimeFactors();
    let a = 6, b = 3;

    // required answer
    document.write(primeFactors[a] -
                        primeFactors[b]);

</script>
```

**Output:** 

```
5
```
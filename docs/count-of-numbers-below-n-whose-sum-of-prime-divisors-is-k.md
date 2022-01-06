# 素数之和为 K 的 N 以下数的计数

> 原文:[https://www . geesforgeks . org/count-of-numbers-below-n-what-sum-of-prime-dividers-is-k/](https://www.geeksforgeeks.org/count-of-numbers-below-n-whose-sum-of-prime-divisors-is-k/)

给定两个整数 **K** 和 **N** ，任务是从素数之和为 **K**
**的范围**【2，N–1】**中找出整数的个数【示例:**

> **输入:** N = 20，K = 7
> **输出:** 2
> 7 和 10 是唯一有效的数字。
> sumPFactors(7)= 7
> sumPFactors(10)= 2+5 = 7
> **输入:** N = 25，K = 5
> **输出:** 5

**方法:**创建一个数组 **sumPF[]** ，其中 **sumPF[i]** 存储 **i** 的素数之和，可以使用本文中使用的方法轻松计算。现在，初始化变量**计数= 0** 并运行从 **2** 到**N–1**的循环，对于每个元素 **i** 如果 **sumPF[i] = K** ，则增加**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

#define MAX 1000001

// Function to return the count of numbers
// below N whose sum of prime factors is K
int countNum(int N, int K)
{
    // To store the sum of prime factors
    // for all the numbers
    int sumPF[MAX] = { 0 };

    for (int i = 2; i < N; i++) {

        // If i is prime
        if (sumPF[i] == 0) {

            // Add i to all the numbers
            // which are divisible by i
            for (int j = i; j < N; j += i) {
                sumPF[j] += i;
            }
        }
    }

    // To store the count of required numbers
    int count = 0;
    for (int i = 2; i < N; i++) {
        if (sumPF[i] == K)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    int N = 20, K = 7;

    cout << countNum(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 1000001;

// Function to return the count of numbers
// below N whose sum of prime factors is K
static int countNum(int N, int K)
{
    // To store the sum of prime factors
    // for all the numbers
    int []sumPF = new int[MAX];

    for (int i = 2; i < N; i++)
    {

        // If i is prime
        if (sumPF[i] == 0)
        {

            // Add i to all the numbers
            // which are divisible by i
            for (int j = i; j < N; j += i)
            {
                sumPF[j] += i;
            }
        }
    }

    // To store the count of required numbers
    int count = 0;
    for (int i = 2; i < N; i++)
    {
        if (sumPF[i] == K)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
public static void main(String[] args)
{
    int N = 20, K = 7;

    System.out.println(countNum(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 1000001

# Function to return the count of numbers
# below N whose sum of prime factors is K
def countNum(N, K) :

    # To store the sum of prime factors
    # for all the numbers
    sumPF = [0] * MAX;

    for i in range(2, N) :

        # If i is prime
        if (sumPF[i] == 0) :

            # Add i to all the numbers
            # which are divisible by i
            for j in range(i, N, i) :
                sumPF[j] += i;

    # To store the count of required numbers
    count = 0;
    for i in range(2, N) :
        if (sumPF[i] == K) :
            count += 1;

    # Return the required count
    return count;

# Driver code
if __name__ == "__main__" :

    N = 20; K = 7;

    print(countNum(N, K));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 1000001;

// Function to return the count of numbers
// below N whose sum of prime factors is K
static int countNum(int N, int K)
{
    // To store the sum of prime factors
    // for all the numbers
    int []sumPF = new int[MAX];

    for (int i = 2; i < N; i++)
    {

        // If i is prime
        if (sumPF[i] == 0)
        {

            // Add i to all the numbers
            // which are divisible by i
            for (int j = i; j < N; j += i)
            {
                sumPF[j] += i;
            }
        }
    }

    // To store the count of required numbers
    int count = 0;
    for (int i = 2; i < N; i++)
    {
        if (sumPF[i] == K)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int N = 20, K = 7;

    Console.WriteLine(countNum(N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const MAX = 1000001;

// Function to return the count of numbers
// below N whose sum of prime factors is K
function countNum(N, K)
{
    // To store the sum of prime factors
    // for all the numbers
    let sumPF = new Array(MAX).fill(0);

    for (let i = 2; i < N; i++) {

        // If i is prime
        if (sumPF[i] == 0) {

            // Add i to all the numbers
            // which are divisible by i
            for (let j = i; j < N; j += i) {
                sumPF[j] += i;
            }
        }
    }

    // To store the count of required numbers
    let count = 0;
    for (let i = 2; i < N; i++) {
        if (sumPF[i] == K)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
    let N = 20, K = 7;

    document.write(countNum(N, K));

</script>
```

**Output:** 

```
2
```
# 计算前两个元素之和等于第三个数字

的素数三元组

> 原文:[https://www . geesforgeks . org/count-prime-triples-up-n-having-sum-first-two-elements-等于第三个数/](https://www.geeksforgeeks.org/count-prime-triplets-upto-n-having-sum-of-first-two-elements-equal-to-the-third-number/)

给定一个整数 **N** ，任务是从范围**【1，N】**中找出不同的[素数三元组](https://www.geeksforgeeks.org/prime-triplet/)的数量，其中前两个数之和等于第三个数。

**示例:**

> **输入:** N = 7
> **输出:** 2
> **解释:**所有有效的三元组为(2，3，5)和(2，5，7)。因此，所需的输出为 2。
> 
> **输入:**N = 4
> T3】输出: 0

**进场:**思路是用厄拉多塞的[筛子。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，说**素数[]** ，用厄拉多塞的[筛标记所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素数](https://www.geeksforgeeks.org/prime-numbers/)到 **N** 。
*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如说**cnttriple【】**，来存储满足上述条件的[素数 triplets】到 **N** 的计数。](https://www.geeksforgeeks.org/prime-triplet/)
*   [在索引**【3，N】**上遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **【碳三重体】**，并检查以下条件:
    *   如果**质数【I】**和**质数【I–2】**是[质数](https://www.geeksforgeeks.org/prime-numbers/)，则通过 **1** 更新**CNT triple【I】**。
    *   否则，分配**碳三元组[i] =碳三元组[I–1]**。
*   最后，打印**CNT triple【N】**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAX 1000001

// Boolean array to
// mark prime numbers
bool prime[MAX];

// To count the prime triplets
// having the sum of the first two
// numbers equal to the third element
int cntTriplet[MAX];

// Function to count prime triplets
// having sum of the first two elements
// equal to the third element
void primeTriplet(long N)
{
    // Sieve of Eratosthenes
    memset(prime, true, sizeof(prime));

    prime[0] = prime[1] = false;

    for (int i = 2; i * i <= N; i++) {

        if (prime[i]) {

            for (int j = i * i; j <= N; j += i) {

                prime[j] = false;
            }
        }
    }

    for (int i = 3; i <= N; i++) {

        // Checks for the prime numbers
        // having difference equal to2
        if (prime[i] && prime[i - 2]) {

            // Update count of triplets
            cntTriplet[i] = cntTriplet[i - 1] + 1;
        }
        else {

            cntTriplet[i] = cntTriplet[i - 1];
        }
    }

    // Print the answer
    cout << cntTriplet[N];
}

// Driver Code
int main()
{
    long N = 7;
    primeTriplet(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{
static int MAX = 1000001;

// Boolean array to
// mark prime numbers
static boolean[] prime = new boolean[MAX];

// To count the prime triplets
// having the sum of the first two
// numbers equal to the third element
static int[] cntTriplet = new int[MAX];

// Function to count prime triplets
// having sum of the first two elements
// equal to the third element
static void primeTriplet(int N)
{
    // Sieve of Eratosthenes
    Arrays.fill(prime, true);
    prime[0] = prime[1] = false;

    for (int i = 2; i * i <= N; i++)
    {
        if (prime[i])
        {
            for (int j = i * i; j <= N; j += i)
            {
                prime[j] = false;
            }
        }
    }

    for (int i = 3; i <= N; i++)
    {

        // Checks for the prime numbers
        // having difference equal to2
        if (prime[i] && prime[i - 2])
        {

            // Update count of triplets
            cntTriplet[i] = cntTriplet[i - 1] + 1;
        }
        else
        {
            cntTriplet[i] = cntTriplet[i - 1];
        }
    }

    // Print the answer
    System.out.println(cntTriplet[N]);
}

// Driver Code
public static void main(String[] args)
{
    int N = 7;
    primeTriplet(N);
}
}

// This code is contributed by susmitakundugoaldagna.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count prime triplets
# having sum of the first two elements
# equal to the third element
def primeTriplet( N):

    # Sieve of Eratosthenes   
    # Boolean array to
    # mark prime numbers
    prime = [True for i in range(1000001)]

    # To count the prime triplets
    # having the sum of the first two
    # numbers equal to the third element
    cntTriplet = [ 0 for i in range(1000001)]   
    prime[0] = prime[1] = False
    i = 2
    while i * i <= N:
        if (prime[i]):
            j = i * i
            while j <= N:
                prime[j] = False
                j += i
        i += 1
    for i in range(3, N + 1):

        # Checks for the prime numbers
        # having difference equal to2
        if (prime[i] and prime[i - 2]):

            # Update count of triplets
            cntTriplet[i] = cntTriplet[i - 1] + 1
        else:
            cntTriplet[i] = cntTriplet[i - 1]

    # Print the answer
    print(cntTriplet[N])

# Driver Code
N = 7
primeTriplet(N)

# This code is contributed by rohitsingh07052
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{
static int MAX = 1000001;

// Boolean array to
// mark prime numbers
static bool[] prime = new bool[MAX];

// To count the prime triplets
// having the sum of the first two
// numbers equal to the third element
static int[] cntTriplet = new int[MAX];

// Function to count prime triplets
// having sum of the first two elements
// equal to the third element
static void primeTriplet(int N)
{
    // Sieve of Eratosthenes
    for(int i = 0; i <= N; i++)
    {
        prime[i] = true;
    }
    prime[0] = prime[1] = false;

    for (int i = 2; i * i <= N; i++)
    {
        if (prime[i])
        {
            for (int j = i * i; j <= N; j += i)
            {
                prime[j] = false;
            }
        }
    }

    for (int i = 3; i <= N; i++)
    {

        // Checks for the prime numbers
        // having difference equal to2
        if (prime[i] && prime[i - 2])
        {

            // Update count of triplets
            cntTriplet[i] = cntTriplet[i - 1] + 1;
        }
        else
        {
            cntTriplet[i] = cntTriplet[i - 1];
        }
    }

    // Print the answer
   Console.WriteLine(cntTriplet[N]);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 7;
    primeTriplet(N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let MAX = 1000001

// Boolean array to
// mark prime numbers
let prime = new Array(MAX).fill(true);

// To count the prime triplets
// having the sum of the first two
// numbers equal to the third element
let cntTriplet = new Array(MAX).fill(0);

// Function to count prime triplets
// having sum of the first two elements
// equal to the third element
function primeTriplet(N)
{

    prime[0] = false;
    prime[1] = false;

    for (let i = 2; i * i <= N; i++) {

        if (prime[i]) {

            for (let j = i * i; j <= N; j += i)
            {

                prime[j] = false;
            }
        }
    }

    for (let i = 3; i <= N; i++) {

        // Checks for the prime numbers
        // having difference equal to2
        if (prime[i] && prime[i - 2]) {

            // Update count of triplets
            cntTriplet[i] = cntTriplet[i - 1] + 1;
        }
        else {

            cntTriplet[i] = cntTriplet[i - 1];
        }
    }

    // Print the answer
    document.write(cntTriplet[N]);
}

// Driver Code

let N = 7;
primeTriplet(N);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
```

***时间复杂度:****O(N * log(log(N)))*
***辅助空间:** O(N)*
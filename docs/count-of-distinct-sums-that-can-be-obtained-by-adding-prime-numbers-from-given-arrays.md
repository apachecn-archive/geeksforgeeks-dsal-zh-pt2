# 通过给定数组中的素数相加得到的不同和的计数

> 原文:[https://www . geeksforgeeks . org/从给定数组中添加质数可以获得的不同和的计数/](https://www.geeksforgeeks.org/count-of-distinct-sums-that-can-be-obtained-by-adding-prime-numbers-from-given-arrays/)

给定两个数组 **arr1[]** 和 **arr2[]** 。任务是计算在从**arr 1【】**中选择一个素元素和从**arr 2【】**中选择另一个素元素时可以获得的不同和。
**举例:**

> **输入:** arr1[] = {2，3}，arr2[] = {2，2，4，7}
> **输出:** 4
> 所有可能的素数对分别为(2，2)，(2，2)，(2，7)，(3，2)，(3，2)
> 和(3，7)，其和分别为 4，4，9，5，5 和 10。
> **输入:** arr1[] = {3，1，4，2，5}，arr2[] = {8，7，10，6，5}
> **输出:** 5

**方法:**使用厄拉多塞的[筛检查一个数是否是素数，然后对于每个素数对，将其总和存储在](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，以避免重复。最终集的大小将是必需的答案。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define MAX 1000000
using namespace std;

bool prime[MAX];
void sieve()
{
    memset(prime, true, sizeof(prime));
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= MAX; p++) {
        if (prime[p] == true) {
            for (int i = p * p; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the distinct sums
// that can be obtained by adding prime
// numbers from the given arrays
int distinctSum(int arr1[], int arr2[], int m, int n)
{
    sieve();

    // Set to store distinct sums
    set<int, greater<int> > sumSet;

    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            if (prime[arr1[i]] && prime[arr2[j]])
                sumSet.insert(arr1[i] + arr2[j]);

    return sumSet.size();
}

// Driver code
int main()
{
    int arr1[] = { 2, 3 };
    int arr2[] = { 2, 2, 4, 7 };
    int m = sizeof(arr1) / sizeof(arr1[0]);
    int n = sizeof(arr2) / sizeof(arr2[0]);
    cout << distinctSum(arr1, arr2, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 1000000;

static boolean []prime = new boolean[MAX + 1];
static void sieve()
{
    Arrays.fill(prime, true);
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= MAX; p++)
    {
        if (prime[p] == true)
        {
            for (int i = p * p;
                     i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the distinct sums
// that can be obtained by adding prime
// numbers from the given arrays
static int distinctSum(int arr1[],
                       int arr2[],
                       int m, int n)
{
    sieve();

    // Set to store distinct sums
    Set<Integer> sumSet = new HashSet<Integer>();

    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            if (prime[arr1[i]] && prime[arr2[j]])
                sumSet.add(arr1[i] + arr2[j]);

    return sumSet.size();
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = { 2, 3 };
    int arr2[] = { 2, 2, 4, 7 };
    int m = arr1.length;
    int n = arr2.length;
    System.out.println(distinctSum(arr1, arr2, m, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 1000000

prime = [True for i in range(MAX + 1)]

def sieve():

    prime[0], prime[1] = False, False

    for p in range(2, MAX + 1):
        if p * p > MAX:
            break
        if (prime[p] == True):
            for i in range(2 * p, MAX + 1, p):
                prime[i] = False

# Function to return the distinct sums
# that can be obtained by adding prime
# numbers from the given arrays
def distinctSum(arr1, arr2, m, n):
    sieve()

    # Set to store distinct sums
    sumSet = dict()

    for i in range(m):
        for j in range(n):
            if (prime[arr1[i]] and
                prime[arr2[j]]):
                sumSet[arr1[i] + arr2[j]] = 1

    return len(sumSet)

# Driver code
arr1 = [2, 3 ]
arr2 = [2, 2, 4, 7 ]
m = len(arr1)
n = len(arr2)
print(distinctSum(arr1, arr2, m, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int MAX = 1000000;

static bool []prime = new bool[MAX + 1];
static void sieve()
{
    for (int i = 0; i < MAX + 1; i++)
        prime[i] = true;
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= MAX; p++)
    {
        if (prime[p] == true)
        {
            for (int i = p * p;
                     i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the distinct sums
// that can be obtained by adding prime
// numbers from the given arrays
static int distinctSum(int []arr1,
                       int []arr2,
                       int m, int n)
{
    sieve();

    // Set to store distinct sums
    HashSet<int> sumSet = new HashSet<int>();

    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            if (prime[arr1[i]] && prime[arr2[j]])
                sumSet.Add(arr1[i] + arr2[j]);

    return sumSet.Count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr1 = { 2, 3 };
    int []arr2 = { 2, 2, 4, 7 };
    int m = arr1.Length;
    int n = arr2.Length;
    Console.WriteLine(distinctSum(arr1, arr2, m, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let MAX = 1000000

let prime = new Array(MAX);

function sieve() {
    prime.fill(true)
    prime[0] = prime[1] = false;
    for (let p = 2; p * p <= MAX; p++) {
        if (prime[p] == true) {
            for (let i = p * p; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the distinct sums
// that can be obtained by adding prime
// numbers from the given arrays
function distinctSum(arr1, arr2, m, n) {
    sieve();

    // Set to store distinct sums
    let sumSet = new Set();

    for (let i = 0; i < m; i++)
        for (let j = 0; j < n; j++)
            if (prime[arr1[i]] && prime[arr2[j]])
                sumSet.add(arr1[i] + arr2[j]);

    return sumSet.size;
}

// Driver code

let arr1 = [2, 3];
let arr2 = [2, 2, 4, 7];
let m = arr1.length;
let n = arr2.length;
document.write(distinctSum(arr1, arr2, m, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N * M * log (N * M) + MAX * log(MAX))

**辅助空间:** O(MAX + N * M)
# 乘积为完美平方的数组中的对的计数

> 原文:[https://www . geeksforgeeks . org/阵列中的成对计数-谁的产品是完美的正方形/](https://www.geeksforgeeks.org/count-of-pairs-in-an-array-whose-product-is-a-perfect-square/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出对的数量 **(arr[i]，arr[j])** ，使得 **arr[i]*arr[j]** 是一个完美的正方形。

**示例:**

> **输入:** arr[] = { 1，2，4，8，5，6}
> **输出:** 2
> **解释:**
> 元素乘积完全平方的对是(1，4)和(8，2)。
> 
> **输入:** arr[] = { 1，2，3，4，5，6，7，8，9 }
> **输出:** 4
> **解释:**
> 元素乘积完全平方的对是(1，4)，(1，9)，(2，8)和(4，9)。

**天真方法:**
从 **1 到 n** 跑两个圈，统计所有的对 **(i，j)** ，其中 **arr[i]*arr[j]** 是一个完美的正方形。这种方法的时间复杂度将是 **O(N <sup>2</sup> )** 。

**有效方法:**
**arr【】**中的每个整数可以用以下形式表示:

```
arr[i] = k*x          ..............(1)
where k is not divisible by any perfect square other than 1,
and x = perfect square,
```

**步骤:**

*   用等式(1)表示每个元素。
*   那么，对于每一对 **(arr[i]，arr[j])**中的**arr[]**可以表示为:

```
arr[i] = ki*x;
arr[j] = kj*y;
where x and y are perfect square
```

*   对于对 **(arr[i]、arr[j])** ，当且仅当 **k <sub>i</sub> = k <sub>j</sub>** 时， **arr[i]** 和 **arr[j]** 的乘积可以完全平方
*   使用厄拉多塞的[筛预先计算](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**中每个元素的 **k** 的值。
*   在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中存储**arr【】**中每个元素的 **k** 的频率。
*   因此，总对数由频率大于 1 的元素形成的对数给出。
*   由 n 个元素形成的对的总数由下式给出:

```
Number of Pairs = (f*(f-1))/2
where f is the frequency of an element.
```

下面是上述方法的实现:

## C++

```
// C++ program to calculate the number of
// pairs with product is perfect square
#include <bits/stdc++.h>
using namespace std;

// Prime[] array to calculate Prime Number
int prime[100001] = { 0 };

// Array k[] to store the value of k for
// each element in arr[]
int k[100001] = { 0 };

// For value of k, Sieve function is
// implemented
void Sieve()
{
    // Initialize k[i] to i
    for (int i = 1; i < 100001; i++)
        k[i] = i;

    // Prime Sieve
    for (int i = 2; i < 100001; i++) {

        // If i is prime then remove all
        // factors of prime from it
        if (prime[i] == 0)
            for (int j = i; j < 100001; j += i) {

                // Update that j is not
                // prime
                prime[j] = 1;

                // Remove all square divisors
                // i.e. if k[j] is divisible
                // by i*i then divide it by i*i
                while (k[j] % (i * i) == 0)
                    k[j] /= (i * i);
            }
    }
}

// Function that return total count
// of pairs with perfect square product
int countPairs(int arr[], int n)
{
    // Map used to store the frequency of k
    unordered_map<int, int> freq;

    // Store the frequency of k
    for (int i = 0; i < n; i++) {
        freq[k[arr[i]]]++;
    }

    int sum = 0;

    // The total number of pairs is the
    // summation of (fi * (fi - 1))/2
    for (auto i : freq) {
        sum += ((i.second - 1) * i.second) / 2;
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 8, 5, 6 };

    // Size of arr[]
    int n = sizeof(arr) / sizeof(int);

    // To pre-compute the value of k
    Sieve();

    // Function that return total count
    // of pairs with perfect square product
    cout << countPairs(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the number of
// pairs with product is perfect square
import java.util.*;

class GFG{

// Prime[] array to calculate Prime Number
static int []prime = new int[100001];

// Array k[] to store the value of k for
// each element in arr[]
static int []k = new int[100001];

// For value of k, Sieve function is
// implemented
static void Sieve()
{
    // Initialize k[i] to i
    for (int i = 1; i < 100001; i++)
        k[i] = i;

    // Prime Sieve
    for (int i = 2; i < 100001; i++) {

        // If i is prime then remove all
        // factors of prime from it
        if (prime[i] == 0)
            for (int j = i; j < 100001; j += i) {

                // Update that j is not
                // prime
                prime[j] = 1;

                // Remove all square divisors
                // i.e. if k[j] is divisible
                // by i*i then divide it by i*i
                while (k[j] % (i * i) == 0)
                    k[j] /= (i * i);
            }
    }
}

// Function that return total count
// of pairs with perfect square product
static int countPairs(int arr[], int n)
{
    // Map used to store the frequency of k
    HashMap<Integer,Integer> freq = new HashMap<Integer,Integer>();

    // Store the frequency of k
    for (int i = 0; i < n; i++) {
        if(freq.containsKey(k[arr[i]])) {
            freq.put(k[arr[i]], freq.get(k[arr[i]])+1);
        }
        else
            freq.put(k[arr[i]], 1);
    }

    int sum = 0;

    // The total number of pairs is the
    // summation of (fi * (fi - 1))/2
    for (Map.Entry<Integer,Integer> i : freq.entrySet()){
        sum += ((i.getValue() - 1) * i.getValue()) / 2;
    }

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 8, 5, 6 };

    // Size of arr[]
    int n = arr.length;

    // To pre-compute the value of k
    Sieve();

    // Function that return total count
    // of pairs with perfect square product
    System.out.print(countPairs(arr, n) +"\n");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to calculate the number 
# of pairs with product is perfect square

# prime[] array to calculate Prime Number
prime = [0] * 100001

# Array to store the value of k
# for each element in arr[]
k = [0] * 100001

# For value of k, Sieve implemented
def Sieve():

    # Initialize k[i] to i
    for i in range(1, 100001):
        k[i] = i

    # Prime sieve
    for i in range(2, 100001):

        # If i is prime then remove all
        # factors of prime from it
        if (prime[i] == 0):
            for j in range(i, 100001, i):

                # Update that j is not prime
                prime[j] = 1

                # Remove all square divisors
                # i.e if k[j] is divisible by
                # i*i then divide it by i*i
                while (k[j] % (i * i) == 0):
                    k[j] /= (i * i)

# Function that return total count of
# pairs with perfect square product
def countPairs (arr, n):

    # Store the frequency of k
    freq = dict()

    for i in range(n):
        if k[arr[i]] in freq.keys():
            freq[k[arr[i]]] += 1
        else:
            freq[k[arr[i]]] = 1

    Sum = 0

    # The total number of pairs is the
    # summation of (fi * (fi - 1))/2
    for i in freq:
        Sum += (freq[i] * (freq[i] - 1)) / 2

    return Sum

# Driver code
arr = [ 1, 2, 4, 8, 5, 6 ]

# Length of arr
n = len(arr)

# To pre-compute the value of k
Sieve()

# Function that return total count
# of pairs with perfect square product
print(int(countPairs(arr, n)))

# This code is contributed by himanshu77
```

## C#

```
// C# program to calculate the number of
// pairs with product is perfect square
using System;
using System.Collections.Generic;

class GFG{

// Prime[] array to calculate Prime Number
static int []prime = new int[100001];

// Array k[] to store the value of k for
// each element in []arr
static int []k = new int[100001];

// For value of k, Sieve function is
// implemented
static void Sieve()
{
    // Initialize k[i] to i
    for (int i = 1; i < 100001; i++)
        k[i] = i;

    // Prime Sieve
    for (int i = 2; i < 100001; i++) {

        // If i is prime then remove all
        // factors of prime from it
        if (prime[i] == 0)
            for (int j = i; j < 100001; j += i) {

                // Update that j is not
                // prime
                prime[j] = 1;

                // Remove all square divisors
                // i.e. if k[j] is divisible
                // by i*i then divide it by i*i
                while (k[j] % (i * i) == 0)
                    k[j] /= (i * i);
            }
    }
}

// Function that return total count
// of pairs with perfect square product
static int countPairs(int []arr, int n)
{
    // Map used to store the frequency of k
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Store the frequency of k
    for (int i = 0; i < n; i++) {
        if(freq.ContainsKey(k[arr[i]])) {
            freq[k[arr[i]]] = freq[k[arr[i]]]+1;
        }
        else
            freq.Add(k[arr[i]], 1);
    }

    int sum = 0;

    // The total number of pairs is the
    // summation of (fi * (fi - 1))/2
    foreach (KeyValuePair<int,int> i in freq){
        sum += ((i.Value - 1) * i.Value) / 2;
    }

    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 4, 8, 5, 6 };

    // Size of []arr
    int n = arr.Length;

    // To pre-compute the value of k
    Sieve();

    // Function that return total count
    // of pairs with perfect square product
    Console.Write(countPairs(arr, n) +"\n"); 
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to calculate the number of
// pairs with product is perfect square

// Prime[] array to calculate Prime Number
let prime = new Array(100001).fill(0);

// Array k[] to store the value of k for
// each element in arr[]
let k = new Array(100001).fill(0);

// For value of k, Sieve function is
// implemented
function Sieve()
{
    // Initialize k[i] to i
    for (let i = 1; i < 100001; i++)
        k[i] = i;

    // Prime Sieve
    for (let i = 2; i < 100001; i++) {

        // If i is prime then remove all
        // factors of prime from it
        if (prime[i] == 0)
            for (let j = i; j < 100001; j += i) {

                // Update that j is not
                // prime
                prime[j] = 1;

                // Remove all square divisors
                // i.e. if k[j] is divisible
                // by i*i then divide it by i*i
                while (k[j] % (i * i) == 0)
                    k[j] /= (i * i);
            }
    }
}

// Function that return total count
// of pairs with perfect square product
function countPairs(arr, n)
{
    // Map used to store the frequency of k
    let freq = new Map();

    // Store the frequency of k
    for (let i = 0; i < n; i++) {
        if(freq.has(k[arr[i]])) {
            freq.set(k[arr[i]], freq.get(k[arr[i]])+1);
        }
        else
            freq.set(k[arr[i]], 1);
    }

    let sum = 0;

    // The total number of pairs is the
    // summation of (fi * (fi - 1))/2
    for (let i of freq) {
        sum += ((i[1] - 1) * i[1]) / 2;
    }

    return sum;
}

// Driver code

let arr = [ 1, 2, 4, 8, 5, 6 ];

// Size of arr[]
let n = arr.length;

// To pre-compute the value of k
Sieve();

// Function that return total count
// of pairs with perfect square product
document.write(countPairs(arr, n) + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N*log(log N))

**辅助空间:** O(N + 10 <sup>5</sup> )
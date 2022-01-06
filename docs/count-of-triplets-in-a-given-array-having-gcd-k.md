# 给定数组中具有 GCD K 的三元组的计数

> 原文:[https://www . geesforgeks . org/给定数组中的三元组计数-having-gcd-k/](https://www.geeksforgeeks.org/count-of-triplets-in-a-given-array-having-gcd-k/)

给定一个整数数组 **arr[]** 和一个整数 **K** ，任务是计算 GCD 等于 **K** 的所有三元组。
**举例:**

> **输入:** arr[] = {1，4，8，14，20}，K = 2
> **输出:** 3
> **解释:**
> 三元组(4，14，20)、(8，14，20)和(4，8，14)的 GCD 等于 2。
> **输入:** arr[] = {1，2，3，4，5}，K = 7
> **输出:** 0

**进场:**
按照以下步骤解决问题:

1.  保持一个数组**CNT【I】**，表示数组中三个一组的数目 **GCD = i** 。
2.  现在，要找到**CNT【I】**，首先计算存储在另一个数组**mul【I】**中的数组中 **i** 的所有倍数。
3.  现在从 **mul[i]** 中选择任意三个值。选择三个值的方式数为**<sup>mul【I】</sup>C<sub>3</sub>**，将该值存储在**CNT【I】**中。
4.  但也包括 GCD 为 **i** 倍数的三胞胎。因此，我们再次迭代所有倍数的 **i** 并从 **cnt[i]** 中减去 **cnt[j]** ，其中 **j** 是 **i** 的倍数。
5.  最后返回**CNT【K】**。

以下是上述方法的实现:

## C++

```
// C++ program to count the
// number of triplets in the
// array with GCD equal to K
#include <bits/stdc++.h>
using namespace std;

const int MAXN = 1e6 + 1;

// frequency array
int freq[MAXN] = { 0 };

// mul[i] stores the count
// of multiples of i
int mul[MAXN] = { 0 };

// cnt[i] stores the count
// of triplets with gcd = i
int cnt[MAXN] = { 0 };

// Return nC3
int nC3(int n)
{
    if (n < 3)
        return 0;
    return (n * (n - 1) * (n - 2)) / 6;
}

// Function to count and return
// the number of triplets in the
// array with GCD equal to K
void count_triplet(vector<int> arr,
                   int N, int K)
{
    for (int i = 0; i < N; i++) {

        // Store frequency of
        // array elements
        freq[arr[i]]++;
    }
    for (int i = 1; i <= 1000000; i++) {
        for (int j = i; j <= 1000000;
             j += i) {
            // Store the multiples of
            // i present in the array
            mul[i] += freq[j];
        }
        // Count triplets with gcd
        // equal to any multiple of i
        cnt[i] = nC3(mul[i]);
    }

    // Remove all triplets which have gcd
    // equal to a multiple of i
    for (int i = 1000000; i >= 1; i--) {
        for (int j = 2 * i; j <= 1000000;
             j += i) {
            cnt[i] -= cnt[j];
        }
    }
    cout << "Number of triplets "
         << "with GCD " << K;
    cout << " are " << cnt[K];
}
// Driver Program
int main()
{
    vector<int> arr = { 1, 7, 12, 6,
                        15, 9 };
    int N = 6, K = 3;
    count_triplet(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the
// number of triplets in the
// array with GCD equal to K
class GFG{

static int MAXN = 1000001;

// Frequency array
static int freq[] = new int[MAXN];

// mul[i] stores the count
// of multiples of i
static int mul[] = new int[MAXN];

// cnt[i] stores the count
// of triplets with gcd = i
static int cnt[] = new int[MAXN];

// Return nC3
static int nC3(int n)
{
    if (n < 3)
        return 0;

    return (n * (n - 1) * (n - 2)) / 6;
}

// Function to count and return
// the number of triplets in the
// array with GCD equal to K
static void count_triplet(int[] arr,
                          int N, int K)
{
    int i, j;
    for(i = 0; i < N; i++)
    {

       // Store frequency of
       // array elements
       freq[arr[i]]++;
    }

    for(i = 1; i <= 1000000; i++)
    {
       for(j = i; j <= 1000000; j += i)
       {

          // Store the multiples of
          // i present in the array
          mul[i] += freq[j];
       }

       // Count triplets with gcd
       // equal to any multiple of i
       cnt[i] = nC3(mul[i]);
    }

    // Remove all triplets which have gcd
    // equal to a multiple of i
    for(i = 1000000; i >= 1; i--)
    {
       for(j = 2 * i; j <= 1000000; j += i)
       {
          cnt[i] -= cnt[j];
       }
    }
    System.out.print("Number of triplets " +
                     "with GCD " + K);
    System.out.print(" are " + cnt[K]);
}

// Driver code
public static void main (String []args)
{
    int []arr = { 1, 7, 12, 6, 15, 9 };
    int N = 6, K = 3;

    count_triplet(arr, N, K);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to count the number of
# triplets in the array with GCD equal to K
MAXN = int(1e6 + 1)

# Frequency array
freq = [0] * MAXN

# mul[i] stores the count
# of multiples of i
mul = [0] * MAXN

# cnt[i] stores the count
# of triplets with gcd = i
cnt = [0] * MAXN

# Return nC3
def nC3(n):

    if(n < 3):
        return 0
    return (n * (n - 1) * (n - 2)) / 6

# Function to count and return
# the number of triplets in the
# array with GCD equal to K
def count_triplet(arr, N, K):

    for i in range(N):

        # Store frequency of
        # array elements
        freq[arr[i]] += 1

    for i in range(1, 1000000 + 1):
        for j in range(i, 1000000 + 1, i):

            # Store the multiples of
            # i present in the array
            mul[i] += freq[j]

        # Count triplets with gcd
        # equal to any multiple of i
        cnt[i] = nC3(mul[i])

    # Remove all triplets which have gcd
    # equal to a multiple of i
    for i in range(1000000, 0, -1):
        for j in range(2 * i, 1000000 + 1, i):
            cnt[i] -= cnt[j]

    print("Number of triplets with GCD"
          " {0} are {1}".format(K, int(cnt[K])))

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 7, 12, 6, 15, 9 ]
    N = 6
    K = 3

    count_triplet(arr, N, K)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to count the
// number of triplets in the
// array with GCD equal to K
using System;
class GFG{

static int MAXN = 1000001;

// Frequency array
static int []freq = new int[MAXN];

// mul[i] stores the count
// of multiples of i
static int []mul = new int[MAXN];

// cnt[i] stores the count
// of triplets with gcd = i
static int []cnt = new int[MAXN];

// Return nC3
static int nC3(int n)
{
    if (n < 3)
        return 0;

    return (n * (n - 1) * (n - 2)) / 6;
}

// Function to count and return
// the number of triplets in the
// array with GCD equal to K
static void count_triplet(int[] arr,
                          int N, int K)
{
    int i, j;
    for(i = 0; i < N; i++)
    {

       // Store frequency of
       // array elements
       freq[arr[i]]++;
    }

    for(i = 1; i <= 1000000; i++)
    {
       for(j = i; j <= 1000000; j += i)
       {

          // Store the multiples of
          // i present in the array
          mul[i] += freq[j];
       }

       // Count triplets with gcd
       // equal to any multiple of i
       cnt[i] = nC3(mul[i]);
    }

    // Remove all triplets which have gcd
    // equal to a multiple of i
    for(i = 1000000; i >= 1; i--)
    {
       for(j = 2 * i; j <= 1000000; j += i)
       {
          cnt[i] -= cnt[j];
       }
    }
    Console.Write("Number of triplets " +
                        "with GCD " + K);
    Console.Write(" are " + cnt[K]);
}

// Driver code
public static void Main (string []args)
{
    int []arr = { 1, 7, 12, 6, 15, 9 };
    int N = 6, K = 3;

    count_triplet(arr, N, K);
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// Javascript program to count the
// number of triplets in the
// array with GCD equal to K

var MAXN = 1000001;

// frequency array
var freq = Array(MAXN).fill(0);

// mul[i] stores the count
// of multiples of i
var mul = Array(MAXN).fill(0);

// cnt[i] stores the count
// of triplets with gcd = i
var cnt = Array(MAXN).fill(0);

// Return nC3
function nC3(n)
{
    if (n < 3)
        return 0;
    return (n * (n - 1) * (n - 2)) / 6;
}

// Function to count and return
// the number of triplets in the
// array with GCD equal to K
function count_triplet(arr, N, K)
{
    for (var i = 0; i < N; i++) {

        // Store frequency of
        // array elements
        freq[arr[i]]++;
    }
    for (var i = 1; i <= 1000000; i++) {
        for (var j = i; j <= 1000000;
             j += i) {
            // Store the multiples of
            // i present in the array
            mul[i] += freq[j];
        }
        // Count triplets with gcd
        // equal to any multiple of i
        cnt[i] = nC3(mul[i]);
    }

    // Remove all triplets which have gcd
    // equal to a multiple of i
    for (var i = 1000000; i >= 1; i--) {
        for (var j = 2 * i; j <= 1000000;
             j += i) {
            cnt[i] -= cnt[j];
        }
    }
    document.write( "Number of triplets "
         + "with GCD " + K);
    document.write( " are " + cnt[K]);
}
// Driver Program
var arr = [ 1, 7, 12, 6,
                    15, 9 ];
var N = 6, K = 3;
count_triplet(arr, N, K);

</script>
```

**Output:** 

```
Number of triplets with GCD 3 are 4
```

***时间复杂度:** O (N * log N)*
***辅助空间:** O(N)*
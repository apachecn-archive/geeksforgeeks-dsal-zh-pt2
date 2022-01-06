# 通过精确删除 k 个子数组来最大化数组的大小，使数组成为素数

> 原文:[https://www . geeksforgeeks . org/通过精确删除 k 个子数组来最大化数组大小，以使数组成为质数/](https://www.geeksforgeeks.org/maximize-the-size-of-array-by-deleting-exactly-k-sub-arrays-to-make-array-prime/)

给定一个由正整数 **N** 和非负整数 **K** 组成的数组 **arr[]** 。任务是从数组中精确删除 **K** 子数组，使得数组的所有剩余元素都是质数，并且剩余数组的大小尽可能最大。

**示例:**

> **输入:** arr[] = {2，4，2，2，4，2}，k = 2
> **输出:** 4
> 删除子阵 arr[1]和 arr[4…6]，
> 剩下的素阵将是{2，2，2，2}
> 
> **输入:** arr[] = {2，4，2，2，4，2，4，2}，k = 3
> **输出:** 5

一种简单的方法是搜索所有耗费我们时间复杂度的子阵列，然后跟踪特定长度子阵列中素数或复合数。

一种有效的方法是跟踪两个连续合成体之间的素数。

1.  **预处理步骤:**使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)将所有素数存储在素数数组中
2.  计算向量 v 中所有复合数的指数。
3.  计算向量差中上述向量的两个连续索引之间的距离，因为这将存储任意两个连续合成之间的素数。
4.  对这个向量进行排序。经过排序，我们得到包含最少素数到最高素数的子阵。
5.  计算这个向量的前缀和。现在 diff 的每个索引表示 k 值，diff 中的值表示删除 k 个子矩阵时要删除的素数。第 0 个索引表示小于 v 大小的最大 k，第 1 个索引表示第二大 k，依此类推。所以，从前缀和向量，我们直接得到要删除的素数。

执行上述步骤后，我们的解决方案取决于三种情况:

1.  如果 k 为 0，并且数组中有复合整数，这是不可能的情况。
2.  如果 k 大于或等于复合数，那么我们可以删除全复合整数和额外的素数，使 k 值相等。这些子阵的大小都是 1，这给了我们最优的答案。
3.  如果 k 小于复合整数的个数，那么我们必须删除那些包含所有复合整数的子阵，以及落入这些子阵的素数的个数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int N = 1e7 + 5;
bool prime[N];

// Sieve of Eratosthenes
void sieve()
{
    for (int i = 2; i < N; i++) {
        if (!prime[i]) {
            for (int j = i + i; j < N; j += i) {
                prime[j] = 1;
            }
        }
    }
    prime[1] = 1;
}

// Function to return the size
// of the maximized array
int maxSizeArr(int* arr, int n, int k)
{
    vector<int> v, diff;

    // Insert the indices of composite numbers
    for (int i = 0; i < n; i++) {
        if (prime[arr[i]])
            v.push_back(i);
    }

    // Compute the number of prime between
    // two consecutive composite
    for (int i = 1; i < v.size(); i++) {
        diff.push_back(v[i] - v[i - 1] - 1);
    }

    // Sort the diff vector
    sort(diff.begin(), diff.end());

    // Compute the prefix sum of diff vector
    for (int i = 1; i < diff.size(); i++) {
        diff[i] += diff[i - 1];
    }

    // Impossible case
    if (k > n || (k == 0 && v.size())) {
        return -1;
    }

    // Delete sub-arrays of length 1
    else if (v.size() <= k) {
        return (n - k);
    }

    // Find the number of primes to be deleted
    // when deleting the sub-arrays
    else if (v.size() > k) {
        int tt = v.size() - k;
        int sum = 0;
        sum += diff[tt - 1];
        int res = n - (v.size() + sum);
        return res;
    }
}

// Driver code
int main()
{
    seive();
    int arr[] = { 2, 4, 2, 2, 4, 2, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << maxSizeArr(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int N = 10000005;
static int []prime = new int[N];

// Sieve of Eratosthenes
static void sieve()
{
    for (int i = 2; i < N; i++)
    {
        if (prime[i] == 0)
        {
            for (int j = i + i; j < N; j += i)
            {
                prime[j] = 1;
            }
        }
    }
    prime[1] = 1;
}

// Function to return the size
// of the maximized array
static int maxSizeArr(int arr[], int n, int k)
{
    ArrayList<Integer> v = new ArrayList<Integer>();
    ArrayList<Integer> diff = new ArrayList<Integer>();

    // Insert the indices of composite numbers
    int num = 0;
    for (int i = 0; i < n; i++)
    {
        if (prime[arr[i]] == 1)
        {
            v.add(i);
        }
    }

    // Compute the number of prime between
    // two consecutive composite
    num = 0;
    for (int i = 1; i < v.size(); i++)
    {
        diff.add(v.get(i) - v.get(i - 1) - 1);
    }

    // Sort the diff vector
    Collections.sort(diff);

    // Compute the prefix sum of diff vector
    for (int i = 1; i < diff.size(); i++)
    {
        diff.set(i, diff.get(i) + diff.get(i - 1));
    }

    // Impossible case
    if (k > n || (k == 0 && v.size() > 0))
    {
        return -1;
    }

    // Delete sub-arrays of length 1
    else if (v.size() <= k)
    {
        return (n - k);
    }

    // Find the number of primes to be deleted
    // when deleting the sub-arrays
    else if (v.size() > k)
    {
        int tt = v.size() - k;
        int sum = 0;
        sum += diff.get(tt - 1);
        int res = n - (v.size() + sum);
        return res;
    }
    return 1;
}

// Driver code
public static void main(String []args)
{
    seive();
    int []arr = { 2, 4, 2, 2, 4, 2, 4, 2 };
    int n = arr.length;
    int k = 2;
    System.out.println(maxSizeArr(arr, n, k));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python implementation of above approach

N = 10000005
prime = [False]*N

# Sieve of Eratosthenes
def sieve():
    for i in range(2,N):
        if not prime[i]:
            for j in range(i+1,N):
                prime[j] = True

    prime[1] = True

# Function to return the size
# of the maximized array
def maxSizeArr(arr, n, k):
    v, diff = [], []

    # Insert the indices of composite numbers
    for i in range(n):
        if prime[arr[i]]:
            v.append(i)

    # Compute the number of prime between
    # two consecutive composite
    for i in range(1, len(v)):
        diff.append(v[i] - v[i-1] -1)

    # Sort the diff vector
    diff.sort()

    # Compute the prefix sum of diff vector
    for i in range(1, len(diff)):
        diff[i] += diff[i-1]

    # Impossible case
    if k > n or (k == 0 and len(v)):
        return -1

    # Delete sub-arrays of length 1
    elif len(v) <= k:
        return (n-k)

    # Find the number of primes to be deleted
    # when deleting the sub-arrays
    elif len(v) > k:
        tt = len(v) - k
        s = 0
        s += diff[tt-1]
        res = n - (len(v) + s)
        return res

# Driver code
if __name__ == "__main__":

    seive()

    arr = [2, 4, 2, 2, 4, 2, 4, 2]
    n = len(arr)
    k = 2

    print(maxSizeArr(arr, n, k))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

static int N = 1000005;
static int []prime = new int[N];

// Sieve of Eratosthenes
static void sieve()
{
    for(int i = 2; i < N; i++)
    {
        if (prime[i] == 0)
        {
            for(int j = i + i;
                    j < N; j += i)
            {
                prime[j] = 1;
            }
        }
    }
    prime[1] = 1;
}

// Function to return the size
// of the maximized array
static int maxSizeArr(int []arr, int n,
                                 int k)
{
    List<int> v = new List<int>();
    List<int> diff = new List<int>();

    // Insert the indices of composite numbers
    //int num = 0;

    for(int i = 0; i < n; i++)
    {
        if (prime[arr[i]] == 1)
        {
            v.Add(i);
        }
    }

    // Compute the number of prime between
    // two consecutive composite
    //num = 0;
    for(int i = 1; i < v.Count; i++)
    {
        diff.Add(v[i] - v[i - 1] - 1);
    }

    // Sort the diff vector
    diff.Sort();

    // Compute the prefix sum of diff vector
    for(int i = 1; i < diff.Count; i++)
    {
        diff[i] = diff[i] + diff[i - 1];
    }

    // Impossible case
    if (k > n || (k == 0 && v.Count > 0))
    {
        return -1;
    }

    // Delete sub-arrays of length 1
    else if (v.Count <= k)
    {
        return (n - k);
    }

    // Find the number of primes to be deleted
    // when deleting the sub-arrays
    else if (v.Count > k)
    {
        int tt = v.Count - k;
        int sum = 0;
        sum += diff[tt - 1];
        int res = n - (v.Count + sum);
        return res;
    }
    return 1;
}

// Driver code
public static void Main(String []args)
{
    seive();
    int []arr = { 2, 4, 2, 2, 4, 2, 4, 2 };
    int n = arr.Length;
    int k = 2;

    Console.WriteLine(maxSizeArr(arr, n, k));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

const N = 1e7 + 5;
let prime = new Array(N);

// Sieve of Eratosthenes
function sieve() {
    for (let i = 2; i < N; i++) {
        if (!prime[i]) {
            for (let j = i + i; j < N; j += i) {
                prime[j] = 1;
            }
        }
    }
    prime[1] = 1;
}

// Function to return the size
// of the maximized array
function maxSizeArr(arr, n, k) {
    let v = new Array();
    let diff = new Array();

    // Insert the indices of composite numbers
    for (let i = 0; i < n; i++) {
        if (prime[arr[i]])
            v.push(i);
    }

    // Compute the number of prime between
    // two consecutive composite
    for (let i = 1; i < v.length; i++) {
        diff.push(v[i] - v[i - 1] - 1);
    }

    // Sort the diff vector
    diff.sort((a, b) => a - b);

    // Compute the prefix sum of diff vector
    for (let i = 1; i < diff.length; i++) {
        diff[i] += diff[i - 1];
    }

    // Impossible case
    if (k > n || (k == 0 && v.length)) {
        return -1;
    }

    // Delete sub-arrays of length 1
    else if (v.length <= k) {
        return (n - k);
    }

    // Find the number of primes to be deleted
    // when deleting the sub-arrays
    else if (v.length > k) {
        let tt = v.length - k;
        let sum = 0;
        sum += diff[tt - 1];
        let res = n - (v.length + sum);
        return res;
    }
}

// Driver code

seive();
let arr = [2, 4, 2, 2, 4, 2, 4, 2];
let n = arr.length;
let k = 2;
document.write(maxSizeArr(arr, n, k));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
4
```
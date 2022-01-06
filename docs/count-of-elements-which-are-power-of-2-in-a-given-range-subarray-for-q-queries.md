# Q 查询给定范围子数组中 2 的幂的元素计数

> 原文:[https://www . geesforgeks . org/给定范围内 2 次方元素计数-q 查询子数组/](https://www.geeksforgeeks.org/count-of-elements-which-are-power-of-2-in-a-given-range-subarray-for-q-queries/)

给定由正数 **N** 和形式为**【L，R】**的 **Q** 查询组成的数组 **arr[]** ，任务是为每个查询找到子数组【L，R】中 2 的幂的元素数量。

**示例:**

> **输入:** arr[] = { 3，8，5，2，5，10 }，Q = {{0，4}，{ 3，5}}
> **输出:**
> 2
> 1
> **解释:**
> 对于查询 1，子阵列[3，8，5，2，5]有 2 个元素，它们是 2 的幂，8 和 2。
> 对于查询 2，子阵列{2，5，10}有 1 个元素是 2 的幂，2。
> **输入:** arr[] = { 1，2，3，4，5，6 }，Q = {{0，4}，{ 1，5}}
> **输出:**
> 3
> 2

**朴素方法:**解决上述问题的朴素方法是，对于所有的 Q 查询，我们可以迭代数组中的每一个 L 和 R，找到子数组[L，R]中 2 的幂的元素个数。
***时间复杂度:** O(N * Q)*

**高效方法:**
为了优化上面的方法，这里的想法是使用一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

*   最初，前缀和数组包含所有索引的 0。
*   遍历给定的数组，如果当前数组元素是 2 的幂，则将该索引的前缀数组设置为 1，否则将其保留为 0。
*   现在，通过将先前的索引前缀数组值相加来计算当前索引的前缀和，从而获得前缀和。前缀[i]将存储从 1 到 I 的 2 的幂的元素的数量
*   一旦我们有了前缀数组，我们只需要为每个查询返回**前缀【r】–前缀【l-1】**。

下面是上述方法的实现，

## C++

```
// C++ implementation to find
// elements that are a power of two

#include <bits/stdc++.h>
using namespace std;
const int MAX = 10000;

// prefix[i] is going to store the
// number of elements which are a
// power of two till i (including i).
int prefix[MAX + 1];

bool isPowerOfTwo(int x)
{
    if (x && (!(x & (x - 1))))
        return true;
    return false;
}

// Function to find the maximum range
// whose sum is divisible by M.
void computePrefix(int n, int a[])
{

    // Calculate the prefix sum
    if (isPowerOfTwo(a[0]))
        prefix[0] = 1;
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1];

        if (isPowerOfTwo(a[i]))
            prefix[i]++;
    }
}

// Function to return the number of elements
// which are a power of two in a subarray
int query(int L, int R)
{
    return prefix[R] - prefix[L - 1];
}

// Driver code
int main()
{
    int A[] = { 3, 8, 5, 2, 5, 10 };
    int N = sizeof(A) / sizeof(A[0]);
    int Q = 2;

    computePrefix(N, A);
    cout << query(0, 4) << "\n";
    cout << query(3, 5) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// elements that are a power of two
import java.util.*;
class GFG{

static final int MAX = 10000;

// prefix[i] is going to store the
// number of elements which are a
// power of two till i (including i).
static int[] prefix = new int[MAX + 1];

static boolean isPowerOfTwo(int x)
{
    if (x != 0 && ((x & (x - 1)) == 0))
        return true;
    return false;
}

// Function to find the maximum range
// whose sum is divisible by M.
static void computePrefix(int n, int a[])
{

    // Calculate the prefix sum
    if (isPowerOfTwo(a[0]))
        prefix[0] = 1;
    for (int i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1];

        if (isPowerOfTwo(a[i]))
            prefix[i]++;
    }
}

// Function to return the number of elements
// which are a power of two in a subarray
static int query(int L, int R)
{
    if (L == 0)
        return prefix[R];

    return prefix[R] - prefix[L - 1];
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 3, 8, 5, 2, 5, 10 };
    int N = A.length;
    int Q = 2;

    computePrefix(N, A);
    System.out.println(query(0, 4));
    System.out.println(query(3, 5));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find
# elements that are a power of two
MAX = 10000

# prefix[i] is going to store the
# number of elements which are a
# power of two till i (including i).
prefix = [0] * (MAX + 1)

def isPowerOfTwo(x):

    if (x and (not (x & (x - 1)))):
        return True
    return False

# Function to find the maximum range
# whose sum is divisible by M.
def computePrefix(n, a):

    # Calculate the prefix sum
    if (isPowerOfTwo(a[0])):
        prefix[0] = 1

    for i in range(1, n):
        prefix[i] = prefix[i - 1]

        if (isPowerOfTwo(a[i])):
            prefix[i] += 1

# Function to return the number of elements
# which are a power of two in a subarray
def query(L, R):

    return prefix[R] - prefix[L - 1]

# Driver code
if __name__ == "__main__":

    A = [ 3, 8, 5, 2, 5, 10 ]
    N = len(A)
    Q = 2

    computePrefix(N, A)
    print(query(0, 4))
    print(query(3, 5))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find
// elements that are a power of two
using System;
class GFG{

static int MAX = 10000;

// prefix[i] is going to store the
// number of elements which are a
// power of two till i (including i).
static int[] prefix = new int[MAX + 1];

static bool isPowerOfTwo(int x)
{
    if (x != 0 && ((x & (x - 1)) == 0))
        return true;
    return false;
}

// Function to find the maximum range
// whose sum is divisible by M.
static void computePrefix(int n, int []a)
{

    // Calculate the prefix sum
    if (isPowerOfTwo(a[0]))
        prefix[0] = 1;
    for (int i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1];

        if (isPowerOfTwo(a[i]))
            prefix[i]++;
    }
}

// Function to return the number of elements
// which are a power of two in a subarray
static int query(int L, int R)
{
    if (L == 0)
        return prefix[R];

    return prefix[R] - prefix[L - 1];
}

// Driver code
public static void Main()
{
    int []A = { 3, 8, 5, 2, 5, 10 };
    int N = A.Length;

    computePrefix(N, A);
    Console.WriteLine(query(0, 4));
    Console.WriteLine(query(3, 5));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to find
// elements that are a power of two

let MAX = 10000;

// prefix[i] is going to store the
// number of elements which are a
// power of two till i (including i).
let prefix = Array.from({length: MAX + 1}, (_, i) => 0);

function isPowerOfTwo(x)
{
    if (x != 0 && ((x & (x - 1)) == 0))
        return true;
    return false;
}

// Function to find the maximum range
// whose sum is divisible by M.
function computePrefix(n, a)
{

    // Calculate the prefix sum
    if (isPowerOfTwo(a[0]))
        prefix[0] = 1;
    for (let i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1];

        if (isPowerOfTwo(a[i]))
            prefix[i]++;
    }
}

// Function to return the number of elements
// which are a power of two in a subarray
function query(L, R)
{
    if (L == 0)
        return prefix[R];

    return prefix[R] - prefix[L - 1];
}

// Driver Code

    let A = [ 3, 8, 5, 2, 5, 10 ];
    let N = A.length;

    computePrefix(N, A);
    document.write(query(0, 4) + "<br/>");
    document.write(query(3, 5));

</script>
```

**Output:** 

```
2
1
```

***时间复杂度:** O(max(Q，N))*
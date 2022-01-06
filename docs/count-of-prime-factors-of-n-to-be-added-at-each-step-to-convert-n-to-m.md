# 计算每一步要相加的 N 的质因数，将 N 转换为 M

> 原文:[https://www . geeksforgeeks . org/每一步添加 n 个质因数以将 n 转换为 m/](https://www.geeksforgeeks.org/count-of-prime-factors-of-n-to-be-added-at-each-step-to-convert-n-to-m/)

给定两个整数 **N** 和 **M** ，任务是找出将 **N** 转换为 **M** 所需的最小操作数。每个操作都包括将 **N** 当前值的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)之一相加。如果有可能获得 M，打印操作次数。否则，打印 **-1** 。

**示例:**

> **输入:** N = 6，M = 10
> **输出:** 2
> **说明:**
> 6 的素因子为[2，3]。
> N 加 2，得到 8。
> 8 的质因数为[2]。
> N 加 2，得到 10，这是期望的结果。
> 因此，总步数= 2
> 
> **输入:** N = 2，M = 3
> **输出:** -1
> **说明:**
> 没有办法把 N = 2 转换成 M = 3。

**逼近:**
利用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 获得到达 M 的最小步数和厄拉多塞的[筛预计算素数即可解决问题。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   使用筛子存储和预计算所有质数。
*   现在，如果 N 已经等于 M，则打印 0，因为不需要加法操作。
*   将此问题想象成图形问题来执行 **BFS** 。通过添加质因数，在每一级存储前一级中 N 值的可达数。
*   现在，首先在队列中插入 **(N，0)** ，其中 N 表示值，0 表示达到该值的操作数。
*   在队列的每一层，通过提取[前面的元素来逐个遍历所有元素，并执行以下操作:](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)
    1.  存储 **q.front()。第一个()**在**纽 Num** 和 **q.front()。第二个()**在**距离**中，其中 **newNum** 为当前值，**距离**为达到该值所需的操作次数。
    2.  将**新数值**的所有质因数存储在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。
    3.  如果**纽数**等于 **M** ，则打印距离，因为这是所需的最小操作。
    4.  如果 **newNum** 大于 M，则断开。
    5.  否则，newNum 小于 m，因此，通过逐个添加其质因数 I 来更新 newNum，并将 **(newNum + i，distance + 1)** 存储在队列中，并对下一级重复上述步骤。
*   如果搜索继续到队列变空的级别，这意味着 M 不能从 N. Print -1 获得。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum
// steps required to convert a number
// N to M.
#include <bits/stdc++.h>
using namespace std;

// Array to store shortest prime
// factor of every integer
int spf[100009];

// Function to precompute
// shortest prime factors
void sieve()
{
    memset(spf, -1, 100005);
    for (int i = 2; i * i <= 100005; i++) {
        for (int j = i; j <= 100005; j += i) {
            if (spf[j] == -1) {
                spf[j] = i;
            }
        }
    }
}

// Function to insert distinct prime factors
// of every integer into a set
set<int> findPrimeFactors(set<int> s,
                          int n)
{
    // Store distinct prime
    // factors
    while (n > 1) {
        s.insert(spf[n]);
        n /= spf[n];
    }
    return s;
}

// Function to return minimum
// steps using BFS
int MinimumSteps(int n, int m)
{

    // Queue of pairs to store
    // the current number and
    // distance from root.
    queue<pair<int, int> > q;

    // Set to store distinct
    // prime factors
    set<int> s;

    // Run BFS
    q.push({ n, 0 });
    while (!q.empty()) {

        int newNum = q.front().first;
        int distance = q.front().second;

        q.pop();

        // Find out the prime factors of newNum
        set<int> k = findPrimeFactors(s,
                                      newNum);

        // Iterate over every prime
        // factor of newNum.
        for (auto i : k) {

            // If M is obtained
            if (newNum == m) {

                // Return number of
                // operations
                return distance;
            }

            // If M is exceeded
            else if (newNum > m) {
                break;
            }

            // Otherwise
            else {

                // Update and store the new
                // number obtained by prime factor
                q.push({ newNum + i,
                         distance + 1 });
            }
        }
    }

    // If M cannot be obtained
    return -1;
}

// Driver code
int main()
{
    int N = 7, M = 16;

    sieve();

    cout << MinimumSteps(N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// steps required to convert a number
// N to M.
import java.util.*;

class GFG{

static class pair
{
    int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Array to store shortest prime
// factor of every integer
static int []spf = new int[100009];

// Function to precompute
// shortest prime factors
static void sieve()
{
    for(int i = 0; i < 100005; i++)
        spf[i] = -1;

    for(int i = 2; i * i <= 100005; i++)
    {
        for(int j = i; j <= 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to insert distinct prime factors
// of every integer into a set
static HashSet<Integer> findPrimeFactors(HashSet<Integer> s,
                                         int n)
{

    // Store distinct prime
    // factors
    while (n > 1)
    {
        s.add(spf[n]);
        n /= spf[n];
    }
    return s;
}

// Function to return minimum
// steps using BFS
static int MinimumSteps(int n, int m)
{

    // Queue of pairs to store
    // the current number and
    // distance from root.
    Queue<pair > q = new LinkedList<>();

    // Set to store distinct
    // prime factors
    HashSet<Integer> s = new HashSet<Integer>();

    // Run BFS
    q.add(new pair(n, 0));

    while (!q.isEmpty())
    {
        int newNum = q.peek().first;
        int distance = q.peek().second;

        q.remove();

        // Find out the prime factors of newNum
        HashSet<Integer> k = findPrimeFactors(s,
                                      newNum);

        // Iterate over every prime
        // factor of newNum.
        for(int i : k)
        {

            // If M is obtained
            if (newNum == m)
            {

                // Return number of
                // operations
                return distance;
            }

            // If M is exceeded
            else if (newNum > m)
            {
                break;
            }

            // Otherwise
            else
            {

                // Update and store the new
                // number obtained by prime factor
                q.add(new pair(newNum + i,
                             distance + 1 ));
            }
        }
    }

    // If M cannot be obtained
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int N = 7, M = 16;

    sieve();

    System.out.print(MinimumSteps(N, M));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# steps required to convert a number
# N to M.

# Array to store shortest prime
# factor of every integer
spf = [-1 for i in range(100009)];

# Function to precompute
# shortest prime factors
def sieve():

    i=2

    while(i * i <= 100006):
        for j in range(i, 100006, i):
            if (spf[j] == -1):
                spf[j] = i;
        i += 1

# Function to append distinct prime factors
# of every integer into a set
def findPrimeFactors(s, n):

    # Store distinct prime
    # factors
    while (n > 1):
        s.add(spf[n]);
        n //= spf[n];

    return s;

# Function to return minimum
# steps using BFS
def MinimumSteps( n, m):

    # Queue of pairs to store
    # the current number and
    # distance from root.
    q = []

    # Set to store distinct
    # prime factors
    s = set()

    # Run BFS
    q.append([ n, 0 ])

    while (len(q) != 0):

        newNum = q[0][0]
        distance = q[0][1]

        q.pop(0);

        # Find out the prime factors of newNum
        k = findPrimeFactors(s, newNum);

        # Iterate over every prime
        # factor of newNum.
        for i in k:

            # If M is obtained
            if (newNum == m):

                # Return number of
                # operations
                return distance;

            # If M is exceeded
            elif (newNum > m):
                break;

            # Otherwise
            else:

                # Update and store the new
                # number obtained by prime factor
                q.append([ newNum + i, distance + 1 ]);

    # If M cannot be obtained
    return -1;

# Driver code
if __name__=='__main__':

    N = 7
    M = 16;

    sieve();

    print( MinimumSteps(N, M))

  # This code is contributed by rutvik_56
```

## C#

```
// C# program to find the minimum
// steps required to convert a number
// N to M.
using System;
using System.Collections.Generic;

class GFG{

class pair
{
    public int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Array to store shortest prime
// factor of every integer
static int []spf = new int[100009];

// Function to precompute
// shortest prime factors
static void sieve()
{
    for(int i = 0; i < 100005; i++)
        spf[i] = -1;

    for(int i = 2; i * i <= 100005; i++)
    {
        for(int j = i; j <= 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to insert distinct prime factors
// of every integer into a set
static HashSet<int> findPrimeFactors(HashSet<int> s,
                                             int n)
{

    // Store distinct prime
    // factors
    while (n > 1)
    {
        s.Add(spf[n]);
        n /= spf[n];
    }
    return s;
}

// Function to return minimum
// steps using BFS
static int MinimumSteps(int n, int m)
{

    // Queue of pairs to store
    // the current number and
    // distance from root.
    Queue<pair> q = new Queue<pair>();

    // Set to store distinct
    // prime factors
    HashSet<int> s = new HashSet<int>();

    // Run BFS
    q.Enqueue(new pair(n, 0));

    while (q.Count != 0)
    {
        int newNum = q.Peek().first;
        int distance = q.Peek().second;

        q.Dequeue();

        // Find out the prime factors of newNum
        HashSet<int> k = findPrimeFactors(s,
                                          newNum);

        // Iterate over every prime
        // factor of newNum.
        foreach(int i in k)
        {

            // If M is obtained
            if (newNum == m)
            {

                // Return number of
                // operations
                return distance;
            }

            // If M is exceeded
            else if (newNum > m)
            {
                break;
            }

            // Otherwise
            else
            {

                // Update and store the new
                // number obtained by prime factor
                q.Enqueue(new pair(newNum + i,
                                 distance + 1));
            }
        }
    }

    // If M cannot be obtained
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int N = 7, M = 16;

    sieve();

    Console.Write(MinimumSteps(N, M));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find the minimum
// steps required to convert a number
// N to M.

class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// Array to store shortest prime
// factor of every integer
var spf = Array(100009).fill(0);

// Function to precompute
// shortest prime factors
function sieve()
{
    for(var i = 0; i < 100005; i++)
        spf[i] = -1;

    for(var i = 2; i * i <= 100005; i++)
    {
        for(var j = i; j <= 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to insert distinct prime factors
// of every integer into a set
function findPrimeFactors(s, n)
{

    // Store distinct prime
    // factors
    while (n > 1)
    {
        s.add(spf[n]);
        n /= spf[n];
    }
    return s;
}

// Function to return minimum
// steps using BFS
function MinimumSteps(n, m)
{

    // Queue of pairs to store
    // the current number and
    // distance from root.
    var q = [];

    // Set to store distinct
    // prime factors
    var s = new Set();

    // Run BFS
    q.push(new pair(n, 0));

    while (q.length != 0)
    {
        var newNum = q[0].first;
        var distance = q[0].second;

        q.shift();

        // Find out the prime factors of newNum
        var k = findPrimeFactors(s,
                                          newNum);

        // Iterate over every prime
        // factor of newNum.
        for(var i of k)
        {

            // If M is obtained
            if (newNum == m)
            {

                // Return number of
                // operations
                return distance;
            }

            // If M is exceeded
            else if (newNum > m)
            {
                break;
            }

            // Otherwise
            else
            {

                // Update and store the new
                // number obtained by prime factor
                q.push(new pair(newNum + i,
                                 distance + 1));
            }
        }
    }

    // If M cannot be obtained
    return -1;
}

// Driver code
var N = 7, M = 16;
sieve();
document.write(MinimumSteps(N, M));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N* log(N))*
***辅助空间:** O(N)*
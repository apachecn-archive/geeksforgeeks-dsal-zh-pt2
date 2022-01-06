# 给定范围内不同的 Primonacci 数的计数[L，R]

> 原文:[https://www . geesforgeks . org/count-of-distinct-primonacci-numbers-in-a-给定范围-l-r/](https://www.geeksforgeeks.org/count-of-distinct-primonacci-numbers-in-a-given-range-l-r/)

给定两个整数**【L，R】**，任务是统计**【L，R】**范围内的**李波纳契数**的个数。

> **普里莫纳契数列:**T2【F(1)= F(2)= 1
> F(3)= 3–F(3–2)= F(1)= 1
> F(4)= F(4–2)+F(4–3)= F(2)+F(1)= 1+1 = 2
> F(5)= F(5–2)+F(5–3)= F(3)+F(2)= 1+1 = 2
> …**+F(N–K)，其中 K 表示小于 N 的最近素数**

**示例:**

> **输入:** L = 1， r = 10
> T3】输出:5
> T6】说明:T8】F(1)=**1**T11】F(2)= 1
> F(3)= 1
> F(4)=**2**T16】F(5)= 2
> F(6)= F(6–2)+F(6–3)+F(6–5)= F(4)+F(3)+F = F(5)+F(4)+F(2)= 2+2+1 =**5**
> F(8)= F(8–2)+F(8–3)+F(8–5)+F(8–7)= F(6)+F(5)+F(3)+F(1)= 4+2+1+1 =**8**
> 因此，不同的报时数为{1，2，4，5，8}。
> 
> **输入:** L = 6，R = 50
> T3】输出: 6

**方法:**
使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[厄拉多塞](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)筛可以解决问题。按照以下步骤解决问题:

*   使用厄拉多塞的[筛生成所有素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   初始化一个 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 来存储不同的 Primonacci 数。
*   初始化一个数组 **dp[ ]** ，使得 **dp[i]** 存储 **i <sup>第</sup>个普里莫纳契数**。
*   设置 **dp[1] = dp[2] = 1** 。
*   对于每个 **i** ，迭代所有小于 I 的素数 **p** ，并通过添加**DP【I–p】**来不断更新**DP【I】**。
*   如果**DP【I】**在**【L，R】**范围内，[插入 **HashSet**](https://www.geeksforgeeks.org/hashset-add-method-in-java/) 。
*   最后，如果**DP【I】**超过 **R** ，打印 **HashSet** 的[尺寸。](https://www.geeksforgeeks.org/hashset-size-method-in-java/)

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Stores list of all primes
static vector<int> primes;
int M = 100005;

// Function to find all primes
void sieve()
{

    // To mark the prime ones
    bool mark[M];
    for(int i = 0; i < M; i++)
       mark[i] = false;

    // Initially all indices as prime
    for(int i = 2; i < M; i++)
        mark[i] = true;

    for(int i = 2; i * i < M; i++)
    {

        // If i is prime
        if (mark[i])
        {

            // Set all multiples
            // of i as non-prime
            for(int j = i * i;
                    j < M; j += i)
                mark[j] = false;
        }
    }

    // Adding all primes to a list
    for(int i = 2; i < M; i++)
        if (mark[i])
            primes.push_back(i);
}

// Function to return the count of
// Primonacci Numbers in the range [l, r]
void countPrimonacci(int l, int r)
{

    // dp[i] contains ith Primonacci Number
    vector<int> dp;
    dp.push_back(1);
    dp.push_back(1);
    int i = 2;

    // Stores the Primonacci Numbers
    set<int> s;
    while (true)
    {
        int x = 0;

        // Iterate over all smaller primes
        for(int j = 0; j < primes.size(); j++)
        {
            int p = primes[j];

            if (p >= i)
                break;

            x += dp[i - p];
        }

        // If Primonacci number lies
        // within the range [L, R]
        if (x >= l && x <= r)
            s.insert(x);

        if (x > r)
            break;

        dp.push_back(x);
        i++;
    }

    // Count of Primonacci Numbers
    cout << s.size();
}

// Driver Code
int main()
{
    sieve();

    int L = 1, R = 10;

    countPrimonacci(L, R);
}

// This code is contributed by bgangwar59
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG {

    // Stores list of all primes
    static ArrayList<Integer> primes;
    static int M = 100005;

    // Function to find all primes
    static void sieve()
    {
        primes = new ArrayList<>();

        // To mark the prime ones
        boolean mark[] = new boolean[M];

        // Initially all indices as prime
        for (int i = 2; i < M; i++)
            mark[i] = true;

        for (int i = 2; i * i < M; i++) {

            // If i is prime
            if (mark[i]) {

                // Set all multiples
                // of i as non-prime
                for (int j = i * i;
                     j < M; j += i)

                    mark[j] = false;
            }
        }

        // Adding all primes to a list
        for (int i = 2; i < M; i++)
            if (mark[i])
                primes.add(i);
    }

    // Function to return the count of
    // Primonacci Numbers in the range [l, r]
    static void countPrimonacci(int l, int r)
    {

        // dp[i] contains ith Primonacci Number
        ArrayList<Integer> dp = new ArrayList<>();
        dp.add(1);
        dp.add(1);
        int i = 2;

        // Stores the Primonacci Numbers
        HashSet<Integer> s = new HashSet<>();
        while (true) {

            int x = 0;

            // Iterate over all smaller primes
            for (int j = 0; j < primes.size();
                 j++) {

                int p = primes.get(j);

                if (p >= i)
                    break;

                x += dp.get(i - p);
            }

            // If Primonacci number lies
            // within the range [L, R]
            if (x >= l && x <= r)
                s.add(x);

            if (x > r)
                break;

            dp.add(x);
            i++;
        }

        // Count of Primonacci Numbers
        System.out.println(s.size());
    }

    // Driver Code
    public static void main(String[] args)
    {
        sieve();

        int L = 1, R = 10;

        countPrimonacci(L, R);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
M = 100005

# Stores list of all primes
primes = []

# Function to find all primes
def sieve():

    # To mark the prime ones
    mark = [False] * M

    # Initially all indices as prime
    for i in range(2, M):
        mark[i] = True

    i = 2
    while i * i < M:

        # If i is prime
        if(mark[i]):

            # Set all multiples
            # of i as non-prime
            j = i * i
            while j < M:
                mark[j] = False
                j += i

        i += 1

    # Adding all primes to a list
    for i in range(2, M):
        if(mark[i]):
            primes.append(i)

# Function to return the count of
# Primonacci Numbers in the range [l, r]
def countPrimonacci(l, r):

    # dp[i] contains ith Primonacci Number
    dp = []
    dp.append(1)
    dp.append(1)
    i = 2

    # Stores the Primonacci Numbers
    s = set()

    while(True):
        x = 0

        # Iterate over all smaller primes
        for j in range(len(primes)):
            p = primes[j]

            if(p >= i):
                break

            x += dp[i - p]

        # If Primonacci number lies
        # within the range [L, R]
        if(x >= l and x <= r):
            s.add(x)

        if(x > r):
            break

        dp.append(x)
        i += 1

    # Count of Primonacci Numbers
    print(len(s))

# Driver Code
if __name__ == '__main__':

    sieve()
    L, R = 1, 10

    countPrimonacci(L, R)

# This code is contributed by Shivam Singh
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

    // Stores list of all primes
    static List<int> primes;
    static int M = 100005;

    // Function to find all primes
    static void sieve()
    {
        primes = new List<int>();

        // To mark the prime ones
        bool[] mark = new bool[M];

        // Initially all indices as prime
        for (int i = 2; i < M; i++)
            mark[i] = true;

        for (int i = 2; i * i < M; i++)
        {

            // If i is prime
            if (mark[i])
            {

                // Set all multiples
                // of i as non-prime
                for (int j = i * i; j < M; j += i)
                    mark[j] = false;
            }
        }

        // Adding all primes to a list
        for (int i = 2; i < M; i++)
            if (mark[i])
                primes.Add(i);
    }

    // Function to return the count of
    // Primonacci Numbers in the range [l, r]
    static void countPrimonacci(int l, int r)
    {

        // dp[i] contains ith Primonacci Number
        List<int> dp = new List<int>();
        dp.Add(1);
        dp.Add(1);
        int i = 2;

        // Stores the Primonacci Numbers
        HashSet<int> s = new HashSet<int>();
        while (true)
        {
            int x = 0;

            // Iterate over all smaller primes
            for (int j = 0; j < primes.Count; j++)
            {
                int p = primes[j];
                if (p >= i)
                    break;
                x += dp[i - p];
            }

            // If Primonacci number lies
            // within the range [L, R]
            if (x >= l && x <= r)
                s.Add(x);

            if (x > r)
                break;
            dp.Add(x);
            i++;
        }

        // Count of Primonacci Numbers
        Console.WriteLine(s.Count);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        sieve();
        int L = 1, R = 10;
        countPrimonacci(L, R);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Stores list of all primes
let primes = new Array();
let M = 100005;

// Function to find all primes
function sieve()
{

    // To mark the prime ones
    let mark = new Array(M);
    for(let i = 0; i < M; i++)
    mark[i] = false;

    // Initially all indices as prime
    for(let i = 2; i < M; i++)
        mark[i] = true;

    for(let i = 2; i * i < M; i++)
    {

        // If i is prime
        if (mark[i])
        {

            // Set all multiples
            // of i as non-prime
            for(let j = i * i;
                    j < M; j += i)
                mark[j] = false;
        }
    }

    // Adding all primes to a list
    for(let i = 2; i < M; i++)
        if (mark[i])
            primes.push(i);
}

// Function to return the count of
// Primonacci Numbers in the range [l, r]
function countPrimonacci(l, r)
{

    // dp[i] contains ith Primonacci Number
    let dp = new Array();
    dp.push(1);
    dp.push(1);
    let i = 2;

    // Stores the Primonacci Numbers
    let s = new Set();
    while (true)
    {
        let x = 0;

        // Iterate over all smaller primes
        for(let j = 0; j < primes.length; j++)
        {
            let p = primes[j];

            if (p >= i)
                break;

            x += dp[i - p];
        }

        // If Primonacci number lies
        // within the range [L, R]
        if (x >= l && x <= r)
            s.add(x);

        if (x > r)
            break;

        dp.push(x);
        i++;
    }

    // Count of Primonacci Numbers
    document.write(s.size);
}

// Driver Code

    sieve();

    let L = 1, R = 10;

    countPrimonacci(L, R);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N * P)，其中 P 是到 R*
***的素数辅助空间:** O(N)*
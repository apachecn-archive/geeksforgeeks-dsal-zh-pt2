# 属于至少一个给定全球定位系统的前 N 项的不同整数的计数

> 原文:[https://www . geesforgeks . org/属于给定至少一个全球定位系统的第一个 n 项的非重复整数计数/](https://www.geeksforgeeks.org/count-of-distinct-integers-belonging-to-first-n-terms-of-at-least-one-of-given-gps/)

给定两个[几何级数](https://www.geeksforgeeks.org/geometric-progression/) **(a1，r1)** 和 **(a2，r2)** ，其中 **(x，y)** 表示 **GP** ，具有初始项 **x** 和公共比 **y** 以及一个整数 **N** ，任务是找到属于第一个 **N** 项的不同整数[的计数](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)

**示例:**

> **输入:** N = 5，a1 = 3，r1 = 2，a2 = 6，r2 = 2
> **输出:** 6
> **说明:**给定几何级数的前 5 项分别为{3，6，12，24，48}和{6，12，24，48，96}。因此，GP 中不同整数的总数是 6。
> 
> **输入:** N = 5，a1 = 3，r1 = 2，a2 = 2，r2 = 3
> **输出:** 9
> **说明:**给定几何级数的前 5 项分别为{3，6，12，24，48}和{2，6，18，54，162}。因此，GP 中不同整数的总数是 9。

**方法:**给定的问题可以通过以下观察来解决:不同整数的总[计数](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)可以通过[生成两个几何级数的前 N 项](https://www.geeksforgeeks.org/program-to-print-gp-geometric-progression/)并移除重复项来计算。这可以通过使用[设置数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)来实现。首先，生成 1 <sup>st</sup> GP 的所有 N 个术语，并将这些术语插入一个集合 **S** 。同样，将 2 <sup>nd</sup> GP 的术语插入到集合 **S** 中。设置 **S** 的大小就是需要的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of distinct
// integers that belong to the first N
// terms of at least one of them is GP
int UniqueGeometricTerms(int N, int a1,
                         int r1, int a2,
                         int r2)
{
    // Stores the integers that occur in
    // GPs in a set data-structure
    set<int> S;

    // Stores the current integer of
    // the first GP
    long long p1 = a1;

    // Iterate first N terms of first GP
    for (int i = 0; i < N; i++) {

        // Insert the ith term of GP in S
        S.insert(p1);
        p1 = (long long)(p1 * r1);
    }

    // Stores the current integer
    // of the second GP
    long long p2 = a2;

    // Iterate first N terms of second GP
    for (int i = 0; i < N; i++) {
        S.insert(p2);
        p2 = (long long)(p2 * r2);
    }

    // Return Answer
    return S.size();
}

// Driver Code
int main()
{
    int N = 5;
    int a1 = 3, r1 = 2, a2 = 2, r2 = 3;

    cout << UniqueGeometricTerms(
        N, a1, r1, a2, r2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find the count of distinct
// integers that belong to the first N
// terms of at least one of them is GP
static int UniqueGeometricTerms(int N, int a1,
                         int r1, int a2,
                         int r2)
{
    // Stores the integers that occur in
    // GPs in a set data-structure
    HashSet<Integer> S=new HashSet<Integer>();

    // Stores the current integer of
    // the first GP
    int p1 = a1;

    // Iterate first N terms of first GP
    for (int i = 0; i < N; i++) {

        // Insert the ith term of GP in S
        S.add(p1);
        p1 = (p1 * r1);
    }

    // Stores the current integer
    // of the second GP
    int p2 = a2;

    // Iterate first N terms of second GP
    for (int i = 0; i < N; i++) {
        S.add(p2);
        p2 = (p2 * r2);
    }

    // Return Answer
    return S.size();
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    int a1 = 3, r1 = 2, a2 = 2, r2 = 3;

    System.out.print(UniqueGeometricTerms(
        N, a1, r1, a2, r2));

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the count of distinct
# integers that belong to the first N
# terms of at least one of them is GP
def UniqueGeometricTerms(N, a1, r1, a2, r2):

    # Stores the integers that occur in
    # GPs in a set data-structure
    S = set()

    # Stores the current integer of
    # the first GP
    p1 = a1

    # Iterate first N terms of first GP
    for i in range(N):

        # Insert the ith term of GP in S
        S.add(p1)
        p1 = (p1 * r1)

    # Stores the current integer
    # of the second GP
    p2 = a2

    # Iterate first N terms of second GP
    for i in range(N):
        S.add(p2)
        p2 = (p2 * r2)

    # Return Answer
    return len(S)

# Driver Code
if __name__ == '__main__':
    N = 5
    a1 = 3
    r1 = 2
    a2 = 2
    r2 = 3

    print(UniqueGeometricTerms(N, a1, r1, a2, r2))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find the count of distinct
// integers that belong to the first N
// terms of at least one of them is GP
static int UniqueGeometricTerms(int N, int a1,
                         int r1, int a2,
                         int r2)
{
    // Stores the integers that occur in
    // GPs in a set data-structure
    HashSet<int> S=new HashSet<int>();

    // Stores the current integer of
    // the first GP
    int p1 = a1;

    // Iterate first N terms of first GP
    for (int i = 0; i < N; i++) {

        // Insert the ith term of GP in S
        S.Add(p1);
        p1 = (p1 * r1);
    }

    // Stores the current integer
    // of the second GP
    int p2 = a2;

    // Iterate first N terms of second GP
    for (int i = 0; i < N; i++) {
        S.Add(p2);
        p2 = (p2 * r2);
    }

    // Return Answer
    return S.Count;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 5;
    int a1 = 3, r1 = 2, a2 = 2, r2 = 3;

    Console.Write(UniqueGeometricTerms(
        N, a1, r1, a2, r2));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the count of distinct
        // integers that belong to the first N
        // terms of at least one of them is GP
        function UniqueGeometricTerms(N, a1,
            r1, a2,
            r2)
       {

            // Stores the integers that occur in
            // GPs in a set data-structure
            let S = new Set();

            // Stores the current integer of
            // the first GP
            let p1 = a1;

            // Iterate first N terms of first GP
            for (let i = 0; i < N; i++) {

                // Insert the ith term of GP in S
                S.add(p1);
                p1 = (p1 * r1);
            }

            // Stores the current integer
            // of the second GP
            let p2 = a2;

            // Iterate first N terms of second GP
            for (let i = 0; i < N; i++) {
                S.add(p2);
                p2 = (p2 * r2);
            }

            // Return Answer
            return S.size;
        }

        // Driver Code

        let N = 5;
        let a1 = 3, r1 = 2, a2 = 2, r2 = 3;

        document.write(UniqueGeometricTerms(
            N, a1, r1, a2, r2));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*
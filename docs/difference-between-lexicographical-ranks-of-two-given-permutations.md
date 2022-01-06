# 两个给定排列的词典等级之间的差异

> 原文:[https://www . geeksforgeeks . org/两个给定排列的字典序差/](https://www.geeksforgeeks.org/difference-between-lexicographical-ranks-of-two-given-permutations/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **P[]** 和 **Q[]** ，这是第一个 **N** 自然数的排列。如果 **P[]** 和 **Q[]** 分别是**【1，N】**的 **a <sup>第</sup>T15】和 **b <sup>第</sup>T19】个词汇上最小的排列，那么任务就是找到**a | b |**。****

**示例:**

> **输入:** P[] = {1，3，2}，Q[] = {3，1，2}
> **输出:** 3
> **解释:**按字典顺序排列的[1，3]的 6 个排列为{{1，2，3}，{1，3，2}，{2，1，3}，{2，3，1}，{3，1，2}，{3，2，1}}。所以 P[]的秩为 2，Q[]的秩为 5。因此，差别是| 2–5 | = 3。
> 
> **输入:** P[] = {1，2}，Q[] = {1，2}
> **输出:** 0
> **解释:**按字典顺序排列的[1，2]的 2 个排列为{{1，2}，{2，1}}。所以 P[]的秩为 1，Q[]的秩为 1。因此，差异为|2-2| = 0。

**方法:**按照以下步骤解决问题:

1.  使用[next _ replacement()](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)函数来查找两个置换的等级。
2.  初始化一个数组 **temp[]** 来存储第一个 **N** 个自然数的最小排列。另外，用 **0** 初始化两个变量 **a** 和 **b** ，以存储两个排列的字典顺序。
3.  检查**温度[]** 是否等于**压力[]** 。如果发现是真的，打破循环。否则，将 **a** 增加 **1** 并检查下一个排列
4.  同样，找到排列的字典顺序 **Q[]** 并存储在 **b** 中。
5.  最后打印 **a** 和 **b** 的绝对差作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function the print the difference
// between the lexicographical ranks
void findDifference(vector<int>& p,
                    vector<int>& q, int N)
{

    // Store the permutations
// in lexicographic order
    vector<int> A(N);

    // Intital permutation
    for (int i = 0; i < N; i++)
        A[i] = i + 1;

    // Initial variables
    bool IsCorrect;
    int a = 1, b = 1;

    // Check permutation
    do {
        IsCorrect = true;
        for (int i = 0; i < N; i++) {
            if (A[i] != p[i]) {
                IsCorrect = false;
                break;
            }
        }
        if (IsCorrect)
            break;
        a++;
    } while (next_permutation(A.begin(),
                              A.end()));

    // Initialize second permutation
    for (int i = 0; i < N; i++)
        A[i] = i + 1;

    // Check permutation
    do {
        IsCorrect = true;
        for (int i = 0; i < N; i++) {
            if (A[i] != q[i]) {
                IsCorrect = false;
                break;
            }
        }
        if (IsCorrect)
            break;
        b++;
    } while (next_permutation(A.begin(),
                              A.end()));

    // Print difference
    cout << abs(a - b) << endl;
}

// Driver Code
int main()
{

    // Given array P[]
    vector<int> p = { 1, 3, 2 };

    // Given array Q[]
    vector<int> q = { 3, 1, 2 };

    // Given size
    int n = p.size();

    // Function call
    findDifference(p, q, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function the print the difference
// between the lexicographical ranks
static void findDifference(int[] p,
                           int[] q,
                           int N)
{

    // Store the permutations
    // in lexicographic order
    int[] A = new int[N];

    // Intital permutation
    for(int i = 0; i < N; i++)
        A[i] = i + 1;

    // Initial variables
    boolean IsCorrect;
    int a = 1, b = 1;

    // Check permutation
    do
    {
        IsCorrect = true;
        for(int i = 0; i < N; i++)
        {
            if (A[i] != p[i])
            {
                IsCorrect = false;
                break;
            }
        }

        if (IsCorrect)
            break;

        a++;
    } while (next_permutation(A));

    // Initialize second permutation
    for(int i = 0; i < N; i++)
        A[i] = i + 1;

    // Check permutation
    do
    {
        IsCorrect = true;
        for(int i = 0; i < N; i++)
        {
            if (A[i] != q[i])
            {
                IsCorrect = false;
                break;
            }
        }
        if (IsCorrect)
            break;

        b++;
    } while (next_permutation(A));

    // Print difference
    System.out.print(Math.abs(a - b) + "\n");
}

static boolean next_permutation(int[] p)
{
    for(int a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])

            for(int b = p.length - 1;; --b)
                if (p[b] > p[a])
                {
                    int t = p[a];
                    p[a] = p[b];
                    p[b] = t;

                    for(++a, b = p.length - 1;
                             a < b; ++a, --b)
                    {
                        t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                    }
                    return true;
                }

    return false;
}

// Driver Code
public static void main(String[] args)
{

    // Given array P[]
    int[] p = { 1, 3, 2 };

    // Given array Q[]
    int[] q = { 3, 1, 2 };

    // Given size
    int n = p.length;

    // Function call
    findDifference(p, q, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function the print the difference
# between the lexicographical ranks
def findDifference(p, q, N):

    # Store the permutations
    # in lexicographic order
    A = [0] * N

    # Initial permutation
    for i in range(N):
        A[i] = i + 1

    # Initial variables
    IsCorrect = False
    a, b = 1, 1

    # Check permutation
    while True:
        IsCorrect = True
        for i in range(N):

            if (A[i] != p[i]):
                IsCorrect = False
                break

        if (IsCorrect):
            break

        a += 1

        if (not next_permutation(A)):
            break

    # Initialize second permutation
    for i in range(N):
        A[i] = i + 1

    # Check permutation
    while True:
        IsCorrect = True
        for i in range(N):

            if (A[i] != q[i]):
                IsCorrect = False
                break

        if (IsCorrect):
            break

        b += 1

        if (not next_permutation(A)):
            break

    # Print difference
    print(abs(a - b))

def next_permutation(p):

    for a in range(len(p) - 2, -1, -1):
        if (p[a] < p[a + 1]):

            b = len(p) - 1
            while True:
                if (p[b] > p[a]):
                    t = p[a]
                    p[a] = p[b]
                    p[b] = t

                    a += 1
                    b = len(p) - 1

                    while a < b:
                        t = p[a]
                        p[a] = p[b]
                        p[b] = t
                        a += 1
                        b -= 1

                    return True

                b -= 1

    return False

# Driver Code

# Given array P[]
p = [ 1, 3, 2 ]

# Given array Q[]
q = [ 3, 1, 2 ]

# Given size
n = len(p)

# Function call
findDifference(p, q, n)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function the print the difference
// between the lexicographical ranks
static void findDifference(int[] p,
                           int[] q,
                           int N)
{

    // Store the permutations
    // in lexicographic order
    int[] A = new int[N];

    // Intital permutation
    for(int i = 0; i < N; i++)
        A[i] = i + 1;

    // Initial variables
    bool IsCorrect;
    int a = 1, b = 1;

    // Check permutation
    do
    {
        IsCorrect = true;
        for(int i = 0; i < N; i++)
        {
            if (A[i] != p[i])
            {
                IsCorrect = false;
                break;
            }
        }

        if (IsCorrect)
            break;

        a++;
    } while (next_permutation(A));

    // Initialize second permutation
    for(int i = 0; i < N; i++)
        A[i] = i + 1;

    // Check permutation
    do
    {
        IsCorrect = true;
        for(int i = 0; i < N; i++)
        {
            if (A[i] != q[i])
            {
                IsCorrect = false;
                break;
            }
        }
        if (IsCorrect)
            break;

        b++;
    } while (next_permutation(A));

    // Print difference
    Console.Write(Math.Abs(a - b) + "\n");
}

static bool next_permutation(int[] p)
{
    for(int a = p.Length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])

            for(int b = p.Length - 1;; --b)
                if (p[b] > p[a])
                {
                    int t = p[a];
                    p[a] = p[b];
                    p[b] = t;

                    for(++a, b = p.Length - 1;
                             a < b; ++a, --b)
                    {
                        t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                    }
                    return true;
                }

    return false;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array P[]
    int[] p = { 1, 3, 2 };

    // Given array Q[]
    int[] q = { 3, 1, 2 };

    // Given size
    int n = p.Length;

    // Function call
    findDifference(p, q, n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function the prvar the difference
    // between the lexicographical ranks
    function findDifference(p,  q , N)
    {

        // Store the permutations
        // in lexicographic order
        var A = Array(N).fill(0);

        // Intital permutation
        for (var i = 0; i < N; i++)
            A[i] = i + 1;

        // Initial variables
        var IsCorrect;
        var a = 1, b = 1;

        // Check permutation
        do {
            IsCorrect = true;
            for (i = 0; i < N; i++) {
                if (A[i] != p[i]) {
                    IsCorrect = false;
                    break;
                }
            }

            if (IsCorrect)
                break;

            a++;
        } while (next_permutation(A));

        // Initialize second permutation
        for (i = 0; i < N; i++)
            A[i] = i + 1;

        // Check permutation
        do {
            IsCorrect = true;
            for (i = 0; i < N; i++) {
                if (A[i] != q[i]) {
                    IsCorrect = false;
                    break;
                }
            }
            if (IsCorrect)
                break;

            b++;
        } while (next_permutation(A));

        // Prvar difference
        document.write(Math.abs(a - b) + "\n");
    }

    function next_permutation(p) {
        for (a = p.length - 2; a >= 0; --a)
            if (p[a] < p[a + 1])

                for (b = p.length - 1;; --b)
                    if (p[b] > p[a]) {
                        var t = p[a];
                        p[a] = p[b];
                        p[b] = t;

                        for (++a, b = p.length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }

        return false;
    }

    // Driver Code

        // Given array P
        var p = [ 1, 3, 2 ];

        // Given array Q
        var q = [ 3, 1, 2 ];

        // Given size
        var n = p.length;

        // Function call
        findDifference(p, q, n);

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * max(a，b))，其中 N 是排列的给定大小，a 和 b 是排列的字典顺序。*
***辅助空间:** O(N)*
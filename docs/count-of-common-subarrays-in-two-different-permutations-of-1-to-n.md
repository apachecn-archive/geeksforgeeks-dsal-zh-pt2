# 1 到 N 两个不同排列中的公共子阵列的计数

> 原文:[https://www . geeksforgeeks . org/1 对 n 两种不同排列的公共子阵列计数/](https://www.geeksforgeeks.org/count-of-common-subarrays-in-two-different-permutations-of-1-to-n/)

给定两个长度相同的阵列 **A** 和**B****N**，填充从 **1** 到 **N** 的自然数排列，任务是统计 **A** 和 **B** 中常见子阵列的数量。
**举例:**

> **输入:**A =【1，2，3】，B =【2，3，1】
> **输出:** 4
> **解释:**
> 常见的子阵有【1】、【2】、【3】、【2，3】
> 因此，总计数= 4
> **输入:**A =【1，2，3，4，5】，B =【2，3，1，4，5】

**天真方法:**
想法是分别生成 **A** 和 **B** 的所有子阵列，每个阵列取 **O(N <sup>2</sup> )** 。现在，将 A 的所有子阵列与 B 的所有子阵列进行比较，并计算公共子阵列。需要 **O(N <sup>4</sup> )** 。
**高效方法:**
思路是用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)高效解决这个问题。

1.  创建一个大小为 **N+1** 的哈希数组 **H** 。
2.  用各自的指数表示 **A** 的所有元素:

```
Element      Representation
A[0]      0
A[1]      1
A[2]      2
.
.
and so on.
```

3.使用数组 H 存储该表示， **H[ A[ i ] ] = i**

4.使用 H、 **B[ i ] = H[ B[ i ] ]** 根据这个新表示更新 **B** 的元素

5.现在，数组 A 可以表示为[0，1，2，..N]，因此只需计算 B 中具有连续元素的子阵列的数量。一旦我们得到连续元素的子阵列的长度 **K** ，使用以下关系计算总的可能子阵列:

> **子阵总数**=(**K***(**K**+**1**)/**2**

看这个例子来详细了解这个方法:

> **例:**
> A = [4，3，1，2，5]
> B = [3，1，2，4，5]
> 常见的子阵有[1]，[2]，[3]，[4]，[5]，[3，1]，[1，2]，[3，1，2] = 8
> **1。**将 A[i]表示为 I，在 H 中存储为 H[A[i]] = i，现在数组 H 从索引 1 到 N 为，
> H = [2，3，1，0，4]
> **2。**根据 H 更新 B，B[i] = H[B[i]]
> B = [1，2，3，0，4]
> **3。**在 B 中寻找具有连续元素的子阵列，
> 从索引 0 到 2 的子阵列为[1，2，3]，由长度为 K = 3 的连续元素组成
> 索引 3 处的元素形成长度为 K = 1 的子阵列[0]
> 索引 4 处的元素形成长度为 K = 1 的子阵列[4]
> **4。**普通子阵列总数=
> (3 *(3+1))/2+(1 *(1+1))/2+(1 *(1+1))/2 = 6+1+1 = 8

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include<bits/stdc++.h>
using namespace std;

int commonSubarrays(int *A, int *B, int N)
{
    // Initialising Map for
    // Index Mapping
    int Map[N + 1];

    // Mapping elements of A
    for(int i = 0 ; i< N; i++)
        Map[*(A + i)] = i;

    // Modify elements of B
    // according to Map
    for (int i = 0; i < N; i++)
    {
        // Changing B[i] as
        // the index of B[i] in A
        *(B + i) = Map[*(B + i)];
    }

    // Count of common subarrays
    int count = 0;

    // Traversing array B
    int i = 0, K;
    while (i < N)
    {
        K = 1;
        i+= 1;

        // While consecutive elements
        // are found, we increment K
        while (i < N && B[i] == B[i - 1] + 1)
        {
            i += 1;
            K += 1;
        }

        // Add number of subarrays
        //with length K
        // to total count
        count = count + ((K) * (K + 1)) / 2;
    }
    return count;
}

// Driver code
int main()
{
    int N = 3;
    int A[] = {1, 2, 3};
    int B[] = {2, 3, 1};
    cout << (commonSubarrays(A, B, N))
         << endl;

    N = 5;
    int C[] = {1, 2, 3, 4, 5};
    int D[] = {2, 3, 1, 4, 5};
    cout << (commonSubarrays(C, D, N));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

static int commonSubarrays(int []A,
                           int []B, int N)
{

    // Initialising Map for
    // Index Mapping
    int []Map = new int[N + 1];

    // Mapping elements of A
    for(int i = 0; i< N; i++)
       Map[A[i]] = i;

    // Modify elements of B
    // according to Map
    for(int i = 0; i < N; i++)
    {

       // Changing B[i] as
       // the index of B[i] in A
       B[i] = Map[B[i]];
    }

    // Count of common subarrays
    int count = 0;

    // Traversing array B
    int i = 0, K;
    while (i < N)
    {
        K = 1;
        i+= 1;

        // While consecutive elements
        // are found, we increment K
        while (i < N && B[i] == B[i - 1] + 1)
        {
            i += 1;
            K += 1;
        }

        // Add number of subarrays
        //with length K
        // to total count
        count = count + ((K) * (K + 1)) / 2;
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int N = 3;
    int A[] = {1, 2, 3};
    int B[] = {2, 3, 1};
    System.out.print(commonSubarrays(A, B, N));
    System.out.print("\n");

    N = 5;
    int C[] = {1, 2, 3, 4, 5};
    int D[] = {2, 3, 1, 4, 5};
    System.out.print(commonSubarrays(C, D, N));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of above approach

def commonSubarrays(A, B, N):

    # Initialising Map for
    # Index Mapping
    Map = [0 for i in range(N + 1)]

    # Mapping elements of A
    for i in range(N):
        Map[A[i]]= i

    # Modify elements of B
    # according to Map
    for i in range(N)    :

        # Changing B[i] as
        # the index of B[i] in A
        B[i]= Map[B[i]]

    # Count of common subarrays
    count = 0

    # Traversing array B
    i = 0
    while i<N:
        K = 1
        i+= 1

        # While consecutive elements
        # are found, we increment K
        while i<N and B[i]== B[i-1]+1:
            i+= 1
            K+= 1

        # Add number of subarrays
        # with length K
        # to total count
        count = count + (
                   (K)*(K + 1))//2

    return count       

# Driver code
N = 3
A =[1, 2, 3]
B =[2, 3, 1]
print(commonSubarrays(A, B, N))

N = 5
A =[1, 2, 3, 4, 5]
B =[2, 3, 1, 4, 5]
print(commonSubarrays(A, B, N))
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

static int commonSubarrays(int []A,
                           int []B,
                           int N)
{

    // Initialising Map for
    // Index Mapping
    int []Map = new int[N + 1];

    // Mapping elements of A
    for(int i = 0; i < N; i++)
       Map[A[i]] = i;

    // Modify elements of B
    // according to Map
    for(int i = 0; i < N; i++)
    {

       // Changing B[i] as
       // the index of B[i] in A
       B[i] = Map[B[i]];
    }

    // Count of common subarrays
    int count = 0;

    // Traversing array B
    int a = 0, K;
    while (a < N)
    {
        K = 1;
        a += 1;

        // While consecutive elements
        // are found, we increment K
        while (a < N && B[a] == B[a - 1] + 1)
        {
            a += 1;
            K += 1;
        }

        // Add number of subarrays
        //with length K
        // to total count
        count = count + ((K) * (K + 1)) / 2;
    }
    return count;
}

// Driver code
public static void Main()
{
    int N = 3;
    int []A = {1, 2, 3};
    int []B = {2, 3, 1};
    Console.Write(commonSubarrays(A, B, N));
    Console.Write("\n");

    N = 5;
    int []C = {1, 2, 3, 4, 5};
    int []D = {2, 3, 1, 4, 5};
    Console.Write(commonSubarrays(C, D, N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

function commonSubarrays(A, B, N)
{

    // Initialising Map for
    // Index Mapping
    let Map = Array.from({length: N+1}, (_, i) => 0);

    // Mapping elements of A
    for(let i = 0; i< N; i++)
       Map[A[i]] = i;

    // Modify elements of B
    // according to Map
    for(let i = 0; i < N; i++)
    {

       // Changing B[i] as
       // the index of B[i] in A
       B[i] = Map[B[i]];
    }

    // Count of common subarrays
    let count = 0;

    // Traversing array B
    let i = 0, K;
    while (i < N)
    {
        K = 1;
        i+= 1;

        // While consecutive elements
        // are found, we increment K
        while (i < N && B[i] == B[i - 1] + 1)
        {
            i += 1;
            K += 1;
        }

        // Add number of subarrays
        //with length K
        // to total count
        count = count + ((K) * (K + 1)) / 2;
    }
    return count;
}

  // Driver Code
    let N = 3;
    let A = [1, 2, 3];
    let B = [2, 3, 1];
    document.write(commonSubarrays(A, B, N));
    document.write("<br/>");

    N = 5;
    let C = [1, 2, 3, 4, 5];
    let D = [2, 3, 1, 4, 5];
    document.write(commonSubarrays(C, D, N));  

    // This code is contributed by target_2.
</script>
```

**Output:** 

```
4
7
```

***时间复杂度:**O(N)*
T5**辅助空间** : O(N)
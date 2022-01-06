# A * C 大于 B*B 的三元组(A，B，C)的计数

> 原文:[https://www . geesforgeks . org/count-of-triples-a-B- c-其中-AC-大于-bb/](https://www.geeksforgeeks.org/count-of-triples-a-b-c-where-ac-is-greater-than-bb/)

给定三个整数 **A** 、 **B** 和 **C** 。任务是统计三倍 **(a，B，c)** 的数量，使得 **a * c > b <sup>2</sup>** ，其中 **0 < a < = A** ， **0 < b < = B** ， **0 < c < = C** 。
**例:**

> **输入:** A = 3，B = 2，C = 2
> **输出:** 6
> 以下三元组计数:
> (1，1，2)、(2，1，1)、(2，1，2)、(3，1，1)、(3，1，2)和(3，2，2)。
> **输入:** A = 3，B = 3，C = 3
> **输出:** 11

**天真法:**
蛮力法是考虑所有可能的三元组 **(a，b，c)** 并统计那些满足约束**a* c>b<sup>2</sup>T8】的三元组。
下面是给定方法的实现。** 

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// function to return the count
// of the valid triplets
long long countTriplets(int A, int B, int C)
{
    long long ans = 0;
    for (int i = 1; i <= A; i++) {
        for (int j = 1; j <= B; j++) {
            for (int k = 1; k <= C; k++) {
                if (i * k > j * j)
                    ans++;
            }
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int A, B, C;
    A = 3, B = 2, C = 2;

    // function calling
    cout << countTriplets(A, B, C);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// function to return the count
// of the valid triplets
static long countTriplets(int A, int B, int C)
{
    long ans = 0;
    for (int i = 1; i <= A; i++)
    {
        for (int j = 1; j <= B; j++)
        {
            for (int k = 1; k <= C; k++)
            {
                if (i * k > j * j)
                    ans++;
            }
        }
    }
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int A = 3, B = 2, C = 2;

    // function calling
    System.out.println(countTriplets(A, B, C));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation for above approach

# function to return the count
# of the valid triplets
def countTriplets(A, B, C):
    ans = 0
    for i in range(1, A + 1):
        for j in range(1, B + 1):
            for k in range(1, C + 1):
                if (i * k > j * j):
                    ans += 1

    return ans

# Driver Code
A = 3
B = 2
C = 2

# function calling
print(countTriplets(A, B, C))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// function to return the count
// of the valid triplets
static long countTriplets(int A,
                          int B, int C)
{
    long ans = 0;
    for (int i = 1; i <= A; i++)
    {
        for (int j = 1; j <= B; j++)
        {
            for (int k = 1; k <= C; k++)
            {
                if (i * k > j * j)
                    ans++;
            }
        }
    }
    return ans;
}

// Driver Code
public static void Main (String[] args)
{
    int A = 3, B = 2, C = 2;

    // function calling
    Console.WriteLine(countTriplets(A, B, C));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation

// function to return the count
// of the valid triplets
function countTriplets(A, B, C)
{
    let ans = 0;
    for (let i = 1; i <= A; i++) {
        for (let j = 1; j <= B; j++) {
            for (let k = 1; k <= C; k++) {
                if (i * k > j * j)
                    ans++;
            }
        }
    }
    return ans;
}

// Driver Code
    let A, B, C;
    A = 3, B = 2, C = 2;

    // function calling
    document.write(countTriplets(A, B, C));

</script>
```

**Output:** 

```
6
```
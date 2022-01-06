# 求数组 B[]的每个元素加到数组 A[]

所有元素的 GCD

> 原文:[https://www . geeksforgeeks . org/find-gcd-数组的每个元素-b-添加到数组的所有元素-a/](https://www.geeksforgeeks.org/find-gcd-of-each-element-of-array-b-added-to-all-elements-of-array-a/)

给定两个长度分别为 ***n*** 和 ***m*** 的[数组 **a[]** 和**b[]**T7】，任务是找出**的**](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **[**最大公约数(GCD)**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/){ a[0]+b[I]，a[1] + b[i]，a[2] + b[i]，…，…**

> **输入:** a[] = {1，10，22，64}，b[] = {5，23，14，13 }
> T3】输出:3 3 1
> T6】解释:
> 
> *   i = 1 : GCD(5+1，5+10，5+22，5+64) = GCD(6，15，27，69) = 3
> *   i = 2 : GCD(23+1，23+10，23+22，23+64) = GCD(24，33，45，87) = 3
> *   i = 3 : GCD(14+1，14+10，14+22，14+64) = GCD(15，24，36，78) = 3
> *   i = 4 : GCD(13+1，13+10，13+22，13+64) = GCD(14，23，35，77) = 1
> 
> **输入:** a[] = {12，30}，b[] = {5，23，14，13}
> **输出:** 1 1 2 1

**方法:**利用 [**欧几里德 GCD 算法**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 的性质可以高效地解决问题，该算法规定 **GCD(x，y)= GCD(x-y，y)** 。这同样适用于多个参数 **GCD(x，y，z，…)= GCD(x-y . y，z，…)** 。应用此属性，可以使用下面给出的步骤解决问题:

*   要计算 **GCD(a[0] + b[i]，…，a[n–1]+b[I])**，从所有其他参数中减去 **a[0] + b[i]** 。
*   现在， **GCD ( a[0] + b[i]，…，a[n–1]+b[I])= GCD(a[0]+b[I]，a[1]a[0]，…，a[n–1]a[0])**。
*   求**G = GCD(a[1]a[0]，…，a[n–1]a[0])**，则任意 **i** 的 GCD 可计算为 **GCD(a[0] + b[i]，G)** 。
*   迭代 **i** 从 **1** 到 **m** 的每个可能值，计算 gcd 为 **G(i) = GCD(a[1]+b[i]，G)**并打印 **G(i)。**

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to calculate gcd for every i
void findGCDs(vector<ll> a, vector<ll> b)
{
    ll g = 0;

    int n = a.size();
    int m = b.size();

    // Update GCD of a[1] - a[0],
    // a[2] - a[0], .... a[n - 1] - a[0]
    for (int i = 1; i < n; i++) {

        g = __gcd(g, a[i] - a[0]);
    }

    // Print gcd(g, a[0] + b[j])
    for (int j = 0; j < m; j++) {

        cout << __gcd(g, a[0] + b[j]) << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    vector<ll> a = { 1, 10, 22, 64 },
               b = { 5, 23, 14, 13 };

    // Function Call
    findGCDs(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
public class GFG{
    static int gcd(int a, int b)
    {    
       if (b == 0)
          return a;
       return gcd(b, a % b);
    }

    // Function to calculate gcd for every i
    static void findGCDs(int[] a, int[] b)
    {
        int g = 0;

        int n = a.length;
        int m = b.length;

        // Update GCD of a[1] - a[0],
        // a[2] - a[0], .... a[n - 1] - a[0]
        for (int i = 1; i < n; i++) {

            g = gcd(g, a[i] - a[0]);
        }

        // Print gcd(g, a[0] + b[j])
        for (int j = 0; j < m; j++) {

            System.out.print(gcd(g, a[0] + b[j]) + " ");
        }
    }

    // Driver Code
public static void main(String args[])
   {

    // Given Input
    int[] a = { 1, 10, 22, 64 },
        b = { 5, 23, 14, 13 };

    // Function Call
    findGCDs(a, b);
   }
}

// This code is contributed by SoumikMondal.
```

## 蟒蛇 3

```
# Python program for above approach
import math

# Function to calculate gcd for every i
def findGCDs( a,  b):
    g = 0
    n = len(a)
    m = len(b)

    # Update GCD of a[1] - a[0],
    # a[2] - a[0], .... a[n - 1] - a[0]
    for i in range(1,n):
        g = math.gcd(g, a[i] - a[0])

    # Pr gcd(g, a[0] + b[j])
    for j in range(m):
        print(math.gcd(g, a[0] + b[j]), end=" ")

# Driver Code

# Given Input
a = [1, 10, 22, 64]
b = [5, 23, 14, 13]

# Function Call
findGCDs(a, b)

#This code is contributed by shubhamsingh10
```

## C#

```
//C# code for the above approach
using System;

public class GFG{
    static int gcd(int a, int b)
    {    
       if (b == 0)
          return a;
       return gcd(b, a % b);
    }

    // Function to calculate gcd for every i
    static void findGCDs(int[] a, int[] b)
    {
        int g = 0;

        int n = a.Length;
        int m = b.Length;

        // Update GCD of a[1] - a[0],
        // a[2] - a[0], .... a[n - 1] - a[0]
        for (int i = 1; i < n; i++) {

            g = gcd(g, a[i] - a[0]);
        }

        // Print gcd(g, a[0] + b[j])
        for (int j = 0; j < m; j++) {

            Console.Write(gcd(g, a[0] + b[j]) + " ");
        }
    }

    // Driver Code
    static public void Main ()
   {

    // Given Input
    int[] a = { 1, 10, 22, 64 },
        b = { 5, 23, 14, 13 };

    // Function Call
    findGCDs(a, b);
   }
}

// This code is contributed by shubhamsingh10.
```

## java 描述语言

```
<script>
    // JavaScript Program for the above approach

    // Function to calculate gcd for every i
    function gcd(a, b)
    {

        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a - b, b);
        return gcd(a, b - a);
    }
    function findGCDs(a, b) {
        let g = 0;

        let n = a.length;
        let m = b.length;

        // Update GCD of a[1] - a[0],
        // a[2] - a[0], .... a[n - 1] - a[0]
        for (let i = 1; i < n; i++) {

            g = gcd(g, a[i] - a[0]);
        }

        // Print gcd(g, a[0] + b[j])
        for (let j = 0; j < m; j++) {

            document.write(gcd(g, a[0] + b[j]) + " ");
        }
    }

    // Driver Code

    // Given Input
    let a = [1, 10, 22, 64]
    let b = [5, 23, 14, 13];

    // Function Call
    findGCDs(a, b);

// This code is contributed by Potta Lokesh
</script>
```

**Output:** 

```
3 3 3 1
```

***时间复杂度:*** O((N + M) * log(X))，其中 **M** 为[数组中最大元素 **a[]** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
[***辅助空间:*** O(1)](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
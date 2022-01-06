# 从 1 到 N 的所有可能的整数不相交子集对的计数

> 原文:[https://www . geesforgeks . org/从 1 到 n 的所有可能不相交整数子集对的计数/](https://www.geeksforgeeks.org/count-of-all-possible-pairs-of-disjoint-subsets-of-integers-from-1-to-n/)

给定一个整数 N，考虑前 N 个自然数的集合 **A = {1，2，3，…，N}** 。让 M 和 P 为 a 的两个**非空**子集，任务是统计(M，P)无序对的数量，使得 M 和 P 为[不相交集](https://en.wikipedia.org/wiki/Disjoint_sets)。请注意，M 和 P 的顺序并不重要。

**示例:**

> **输入:** N = 3
> **输出:** 6
> 无序对为({1}、{2})、({1}、{3})、
> ({2}、{3})、({1}、{2，3})、({2}、{1，3})、({3}、{1，2})。
> 
> **输入:**N = 2
> T3】输出: 1
> 
> **输入:**N = 10
> T3】输出: 28501

**进场:**

1.  假设集合{1，2，3，4，5，6}中只有 6 个元素。
2.  当你把 1 作为第一个子集的一个元素来计算子集的数量时，结果是 211。
3.  用 2 作为第一个子集的元素之一来计算子集的数量，结果是 65，因为 1 不包括在集合的顺序中并不重要。
4.  计算第一个集合的元素之一为 3 的子集的数量，结果是 65，这里可以观察到一个模式。
5.  图案:

    > 5 = 3 * 1+2
    > 19 = 3 * 5+4
    > 65 = 3 * 19+8
    > 211 = 3 * 65+16
    > S(n)= 3 * S(n-1)+2<sup>(n-2)</sup>

6.  将其展开至 n->2(表示元素数 n-2+1 = n-1)
    2<sup>(n-2)</sup>* 3<sup>(0)</sup>+2<sup>(n–3)</sup>* 3<sup>1</sup>+2<sup>(n–4)</sup>* 3<sup>2</sup>+2<sup>(n–5)</sup>* 3<sup>3</sup>+…+2 a+a * r<sup>0</sup>+a * r<sup>1</sup>+…+a * r<sup>(n–1)</sup>= a *(r<sup>n</sup>–1)/(r–1)
7.  **S(n)= 3<sup>(n–1)</sup>–2<sup>(n–1)</sup>**。记住 S(n)是子集的数量，1 是第一个子集的元素之一，但要得到所需的结果，用**T(n)= S(1)+S(2)+S(3)+…+S(n)**表示
8.  它也形成一个几何级数，所以我们用 GP
    **T(n)=(3<sup>n</sup>–2<sup>n+1</sup>+1)/2**的和公式来计算
9.  由于我们需要 T(n) % p，其中 p = 10 <sup>9</sup> + 7
    我们必须使用[费马斯小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)T5】a<sup>-1</sup>= a<sup>(m–2)</sup>(mod m)进行模除法

    以下是上述方法的实现:

    ## C++

    ```
    // C++ implementation of the approach

    #include <bits/stdc++.h>
    using namespace std;
    #define p 1000000007

    // Modulo exponentiation function
    long long power(long long x, long long y)
    {
        // Function to calculate (x^y)%p in O(log(y))
        long long res = 1;
        x = x % p;

        while (y > 0) {
            if (y & 1)
                res = (res * x) % p;
            y = y >> 1;
            x = (x * x) % p;
        }

        return res % p;
    }

    // Driver function
    int main()
    {
        long long n = 3;

        // Evaluating ((3^n-2^(n+1)+1)/2)%p
        long long x = (power(3, n) % p + 1) % p;

        x = (x - power(2, n + 1) + p) % p;

        // From  Fermats’s little theorem
        // a^-1 ? a^(m-2) (mod m)

        x = (x * power(2, p - 2)) % p;
        cout << x << "\n";
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation of the approach
    class GFG 
    { 
    static int p = 1000000007;

    // Modulo exponentiation function
    static long power(long x, long y)
    {
        // Function to calculate (x^y)%p in O(log(y))
        long res = 1;
        x = x % p;

        while (y > 0)
        {
            if (y % 2 == 1)
                res = (res * x) % p;
            y = y >> 1;
            x = (x * x) % p;
        }
        return res % p;
    }

    // Driver Code
    public static void main(String[] args) 
    {
        long n = 3;

        // Evaluating ((3^n-2^(n+1)+1)/2)%p
        long x = (power(3, n) % p + 1) % p;

        x = (x - power(2, n + 1) + p) % p;

        // From Fermats's little theorem
        // a^-1 ? a^(m-2) (mod m)

        x = (x * power(2, p - 2)) % p;
        System.out.println(x);
    }
    }

    // This code is contributed by Rajput-Ji
    ```

    ## 蟒蛇 3

    ```
    # Python3 implementation of the approach
    p = 1000000007

    # Modulo exponentiation function
    def power(x, y):

        # Function to calculate (x^y)%p in O(log(y))
        res = 1
        x = x % p

        while (y > 0):
            if (y & 1):
                res = (res * x) % p;
            y = y >> 1
            x = (x * x) % p

        return res % p

    # Driver Code
    n = 3

    # Evaluating ((3^n-2^(n+1)+1)/2)%p
    x = (power(3, n) % p + 1) % p

    x = (x - power(2, n + 1) + p) % p

    # From Fermats’s little theorem
    # a^-1 ? a^(m-2) (mod m)
    x = (x * power(2, p - 2)) % p

    print(x)

    # This code is contributed by Mohit Kumar
    ```

    ## C#

    ```
    // C# implementation of the approach
    using System;

    class GFG
    {
    static int p = 1000000007;

    // Modulo exponentiation function
    static long power(long x, long y)
    {
        // Function to calculate (x^y)%p in O(log(y))
        long res = 1;
        x = x % p;

        while (y > 0)
        {
            if (y % 2 == 1)
                res = (res * x) % p;
            y = y >> 1;
            x = (x * x) % p;
        }
        return res % p;
    }

    // Driver Code
    static public void Main ()
    {
        long n = 3;

        // Evaluating ((3^n-2^(n+1)+1)/2)%p
        long x = (power(3, n) % p + 1) % p;

        x = (x - power(2, n + 1) + p) % p;

        // From Fermats's little theorem
        // a^-1 ? a^(m-2) (mod m)

        x = (x * power(2, p - 2)) % p;
        Console.Write(x);
    }
    }

    // This code is contributed by ajit.
    ```

    **Output:**

    ```
    6

    ```
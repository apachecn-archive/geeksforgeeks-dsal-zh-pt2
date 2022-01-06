# 使两个数相等所需的最小操作数

> 原文:[https://www . geesforgeks . org/minimum-operations-required-make-two-numbers-equal/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-two-numbers-equal/)

给定两个整数 **A** 和 **B** 。任务是找到使 A 和 B 相等所需的最小操作数。在每个操作中，可以执行以下任一步骤:

*   用初始值递增 A 或 B。
*   用初始值递增 A 和 B

**例:**

> **输入:** A = 4，B = 10
> **输出:** 4
> **解释:**
> 最初 A = 4，B = 10
> 操作 1:仅增量 A:A = A+4 = 8
> 操作 2:仅增量 A:A = A+4 = 12
> 操作 3:仅增量 A:A = A+4 = 16
> 操作 4:增量 A 和 B: A = A + 4 = 20 和
> **输入:** A = 7，B = 23
> **输出:** 22
> **解释:**
> 最初 A = 7，B = 23
> 运算 1–7:增量 A 和 B: A = 56 和 B = 161
> 运算 8–22:增量 A: A = 161 和 B = 161
> 它们现在相等。

**方法:**这个问题可以使用 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 解决。

1.  如果 A 大于 B，那么交换 A 和 B。
2.  现在减少 B，这样 A 和 B 的 gcd 变成 1。
3.  因此，达到相等值所需的最小操作是(B–1)。

**例如:**如果 A = 4，B = 10:

*   *第一步:*比较 4 和 10，因为我们总是需要 B 作为较大的值。这里 B 已经大于 a 了。所以，现在不需要交换。
*   *第二步:* GCD(4，10) = 2。所以，我们把 B 简化为 B/2。现在 A = 4，B = 5。
    GCD(4，5) = 1，这是目标。
*   *第 3 步:*(B–1 的当前值)将是所需的计数。这里，电流 B = 5。因此(5–1 = 4)，即总共需要 4 次操作。

下面是上述方法的实现。

## C++

```
// C++ program to find minimum
// operations required to
// make two numbers equal

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// minimum operations required
long long int minOperations(
    long long int A,
    long long int B)
{

    // Keeping B always greater
    if (A > B)
        swap(A, B);

    // Reduce B such that
    // gcd(A, B) becomes 1.
    B = B / __gcd(A, B);

    return B - 1;
}

// Driver code
int main()
{
    long long int A = 7, B = 15;

    cout << minOperations(A, B)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// operations required to
// make two numbers equal
class GFG{

// Function to return the
// minimum operations required
static int  minOperations(
    int  A,
    int  B)
{

    // Keeping B always greater
    if (A > B) {
        A = A+B;
        B = A-B;
        A = A-B;
    }

    // Reduce B such that
    // gcd(A, B) becomes 1.
    B = B / __gcd(A, B);

    return B - 1;
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int  A = 7, B = 15;

    System.out.print(minOperations(A, B)
         +"\n");

}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python program to find minimum
# operations required to
# make two numbers equal
import math

# Function to return the
# minimum operations required
def minOperations(A, B):

    # Keeping B always greater
    if (A > B):
        swap(A, B)

    # Reduce B such that
    # gcd(A, B) becomes 1.
    B = B // math.gcd(A, B);

    return B - 1

# Driver code
A = 7
B = 15

print(minOperations(A, B))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find minimum
// operations required to
// make two numbers equal
using System;

class GFG{

// Function to return the
// minimum operations required
static int  minOperations(
    int  A,
    int  B)
{

    // Keeping B always greater
    if (A > B) {
        A = A+B;
        B = A-B;
        A = A-B;
    }

    // Reduce B such that
    // gcd(A, B) becomes 1.
    B = B / __gcd(A, B);

    return B - 1;
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int  A = 7, B = 15;

    Console.Write(minOperations(A, B)
         +"\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// javascript program to find minimum
// operations required to
// make two numbers equal   
// Function to return the
    // minimum operations required
    function minOperations(A, B)
{

        // Keeping B always greater
        if (A > B) {
            A = A + B;
            B = A - B;
            A = A - B;
        }

        // Reduce B such that
        // gcd(A, B) becomes 1.
        B = B / __gcd(A, B);

        return B - 1;
    }

    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code
        var A = 7, B = 15;
        document.write(minOperations(A, B) + "\n");

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(log(max(A，B))*

***辅助空间:** O(log(max(A，B))*
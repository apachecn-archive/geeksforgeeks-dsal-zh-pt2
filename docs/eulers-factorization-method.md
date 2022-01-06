# 欧拉因子分解法

> 原文:[https://www.geeksforgeeks.org/eulers-factorization-method/](https://www.geeksforgeeks.org/eulers-factorization-method/)

给定一个数字 **N** ，任务是找到 N 的因子
T3【例:

> **输入:** N = 1000009
> **输出:** 293 3413
> **解释:**
> 293 * 3413 = 1000009
> **输入:** N = 100000
> **输出:** 800 125
> **解释:**
> 800 * 125

**欧拉因式分解法:**欧拉因式分解法的工作原理是把所有可以用两种不同方式写成二次幂之和的数 N 都可以分解成两个数，即(A)**N = A<sup>2</sup>+B<sup>2</sup>= C<sup>2</sup>+D<sup>2</sup>**其中 A！= C 和 A！= D，那么 N 存在两个因子
**算法的工作:**让 N 是我们需要找到因子的数。

*   所以，最初，我们需要找到两种方法，将 N 表示为两个数的幂之和。

```
N = A2 + B2
N = C2 + D2
Therefore,
N = A2 + B2 = C2 + D2
```

*   现在，对上述方程进行代数运算，将方程转换为:

```
N = A2 + B2 = C2 + D2
-> N = A2 - C2 = D2 - B2
-> N = (A - C)(A + C) = (D - B)(D + B)
```

*   设 K 为(A–C)和(D–B)的 GCD。所以，

```
A - C = K * L
D - B = K * M
where GCD(L, M) is 1.
```

*   显然，L =(A–C)/K 和 M =(D–B)/K。在初始方程中代入时:

```
N = K * L * (A + C) = K * M * (D + B)
-> L * (A + C) = M * (D + B)
-&gtl (A + C)/(D + B) = M/L
```

*   因此:

```
(A + C) = M * H 
(D + B) = L * H
where,
H = gcd((A + C), (D + B))
```

*   让 Q =(K<sup>2</sup>+H<sup>2</sup>)(L<sup>2</sup>+M<sup>2</sup>)。

```
-> ((KL)2 + (KM)2 + (HL)2 + (HM)2)
-> ((A - C)2 + (D - B)2 + (D + B)2 + (A + C)2)
-> ((2 * A)2 + (2 * B)2 + (2 * C)2 + (2 * D)2)
-> 4 * N
```

*   因此，

```
N = ((K/2)2 + (H/2)2)(L2 + M2)
```

*   使得存在一对都是偶数的 K 和 H。

让我们通过一个例子来形象化上面的方法。设 N = 221。

1.  221 = 11<sup>2</sup>+10<sup>2</sup>= 5<sup>2</sup>+14<sup>2</sup>
2.  从上面的等式中:

```
A = 11 - 5 = 6
B = 11 + 5 = 15
C = 14 - 10 = 4
D = 14 + 10 = 24
```

*   因此，上述数值可用于计算 K、H、L 和 m 的值。

```
K = GCD(6, 4) = 2
H = GCD(16, 24) = 8
L = GCD(6, 24) = 3
M = GCD(16, 4) = 2
```

*   因此:

```
221 = ((2/2)2 + (8/2)2) * (32 + 22)
221 = 17 * 13
```

**方法:**为了实现上述方法，计算以下步骤:

1.  通过从 1 到 sqrt(N)的循环迭代求平方和，因为除了 N 之外[sqrt(N，N]之间不存在因子，求两个平方和等于 N 的对
2.  将值存储在 A、B、C、d 中
3.  使用上述方法中提到的公式求出 K、H、L 和 M 的值。
4.  用 K，H，L 和 M 的值来寻找因子。检查两个数都是偶数的那对，把它们分成两半，找出因子。

以下是上述方法的实现:

## C++

```
// C++ program to implement Eulers
// Factorization algorithm

#include <bits/stdc++.h>
using namespace std;

// Function to return N as the sum of
// two squares in two possible ways
void sumOfSquares(int n, vector<pair<int, int> >& vp)
{
    // Iterate a loop from 1 to sqrt(n)
    for (int i = 1; i <= sqrt(n); i++) {

        // If i*i is square check if there
        // exists another integer such that
        // h is a perfect square and i*i + h = n
        int h = n - i * i, h1 = sqrt(h);

        // If h is perfect square
        if (h1 * h1 == h) {

            // Store in the sorted way
            int a = max(h1, i), b = min(h1, i);

            // If there is already a pair
            // check if pairs are equal or not
            if (vp.size() == 1 && a != vp[0].first)
                vp.push_back(make_pair(a, b));

            // Insert the first pair
            if (vp.size() == 0)
                vp.push_back(make_pair(a, b));

            // If two pairs are found
            if (vp.size() == 2)
                return;
        }
    }
}

// Function to find the factors
void findFactors(int n)
{

    // Get pairs where a^2 + b^2 = n
    vector<pair<int, int> > vp;
    sumOfSquares(n, vp);

    // Number cannot be represented
    // as sum of squares in two ways
    if (vp.size() != 2)
        cout << "Factors Not Possible";

    // Assign a, b, c, d
    int a, b, c, d;

    a = vp[0].first;
    b = vp[0].second;

    c = vp[1].first;
    d = vp[1].second;

    // Swap if a < c because
    // if a - c < 0,
    // GCD cant be computed.
    if (a < c) {
        int t = a;
        a = c;
        c = t;
        t = b;
        b = d;
        d = t;
    }

    // Compute the values of k, h, l, m
    // using the formula mentioned
    // in the approach
    int k, h, l, m;
    k = __gcd(a - c, d - b);
    h = __gcd(a + c, d + b);
    l = (a - c) / k;
    m = (d - b) / k;

    // Print the values of a, b, c, d
    // and k, l, m, h
    cout << "a = " << a
         << "\t\t(A) a - c = " << (a - c)
         << "\t\tk = gcd[A, C] = "
         << k << endl;

    cout << "b = " << b
         << "\t\t(B) a + c = " << (a + c)
         << "\t\th = gcd[B, D] = "
         << h << endl;

    cout << "c = " << c
         << "\t\t(C) d - b = " << (d - b)
         << "\t\tl = A/k = "
         << l << endl;

    cout << "d = " << d
         << "\t\t(D) d + b = " << (d + b)
         << "\t\tm = c/k = "
         << m << endl;

    // Printing the factors
    if (k % 2 == 0 && h % 2 == 0) {
        k = k / 2;
        h = h / 2;

        cout << "Factors are: "
             << ((k) * (k) + (h) * (h))
             << " " << (l * l + m * m)
             << endl;
    }
    else {
        l = l / 2;
        m = m / 2;

        cout << "Factors are: "
             << ((l) * (l) + (m) * (m))
             << " " << (k * k + h * h)
             << endl;
    }
}

// Driver code
int main()
{
    int n = 100000;

    findFactors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Eulers
// Factorization algorithm
import java.util.*;
class GFG{

static class pair
{
  int first, second;
  public pair(int first,
              int second) 
  {
    this.first = first;
    this.second = second;
  }   
}

// Recursive function to
// return gcd of a and b 
static int __gcd(int a, int b) 
{ 
  return b == 0 ? a :
         __gcd(b, a % b);    
}

// Function to return N as the sum of
// two squares in two possible ways
static void sumOfSquares(int n,
                         Vector<pair> vp)
{
  // Iterate a loop from 1 to Math.sqrt(n)
  for (int i = 1; i <= Math.sqrt(n); i++)
  {
    // If i*i is square check if there
    // exists another integer such that
    // h is a perfect square and i*i + h = n
    int h = n - i * i, h1 = (int)Math.sqrt(h);

    // If h is perfect square
    if (h1 * h1 == h)
    {
      // Store in the sorted way
      int a = Math.max(h1, i),
          b = Math.min(h1, i);

      // If there is already a pair
      // check if pairs are equal or not
      if (vp.size() == 1 &&
          a != vp.get(0).first)
        vp.add(new pair(a, b));

      // Insert the first pair
      if (vp.size() == 0)
        vp.add(new pair(a, b));

      // If two pairs are found
      if (vp.size() == 2)
        return;
    }
  }
}

// Function to find the factors
static void findFactors(int n)
{
  // Get pairs where a^2 + b^2 = n
  Vector<pair> vp = new Vector<>();
  sumOfSquares(n, vp);

  // Number cannot be represented
  // as sum of squares in two ways
  if (vp.size() != 2)
    System.out.print("Factors Not Possible");

  // Assign a, b, c, d
  int a, b, c, d;

  a = vp.get(0).first;
  b = vp.get(0).second;

  c = vp.get(1).first;
  d = vp.get(1).second;

  // Swap if a < c because
  // if a - c < 0,
  // GCD cant be computed.
  if (a < c)
  {
    int t = a;
    a = c;
    c = t;
    t = b;
    b = d;
    d = t;
  }

  // Compute the values of k, h, l, m
  // using the formula mentioned
  // in the approach
  int k, h, l, m;
  k = __gcd(a - c, d - b);
  h = __gcd(a + c, d + b);
  l = (a - c) / k;
  m = (d - b) / k;

  // Print the values of a, b, c, d
  // and k, l, m, h
  System.out.print("a = " + a +
                   "\t\t(A) a - c = " + 
                   (a - c) +
                   "\t\tk = gcd[A, C] = " +
                   k + "\n");

  System.out.print("b = " + b +
                   "\t\t(B) a + c = " + 
                   (a + c) +
                   "\t\th = gcd[B, D] = " +
                   h + "\n");

  System.out.print("c = " +  c +
                   "\t\t(C) d - b = " + 
                   (d - b) +
                   "\t\tl = A/k = " +
                   l + "\n");

  System.out.print("d = " +  d +
                   "\t\t(D) d + b = " +
                   (d + b) +
                   "\t\tm = c/k = " +
                   m + "\n");

  // Printing the factors
  if (k % 2 == 0 && h % 2 == 0)
  {
    k = k / 2;
    h = h / 2;
    System.out.print("Factors are: " +
                     ((k) * (k) + (h) * (h)) +
                     " " + (l * l + m * m) + "\n");
  }
  else
  {
    l = l / 2;
    m = m / 2;
    System.out.print("Factors are: " +
                     ((l) * (l) + (m) * (m)) +
                     " " + (k * k + h * h) + "\n");
  }
}

// Driver code
public static void main(String[] args)
{
  int n = 100000;
  findFactors(n);
}
}

// This code is contributed by gauravrajput1
```

## C#

```
// C# program to implement Eulers
// Factorization algorithm
using System;
using System.Collections.Generic;
class GFG{

public class pair
{
  public int first, second;
  public pair(int first,
              int second) 
  {
    this.first = first;
    this.second = second;
  }   
}

// Recursive function to
// return gcd of a and b 
static int __gcd(int a, int b) 
{ 
  return b == 0 ? a :
         __gcd(b, a % b);    
}

// Function to return N as the sum of
// two squares in two possible ways
static void sumOfSquares(int n,
                         List<pair> vp)
{
  // Iterate a loop from 1 to Math.Sqrt(n)
  for (int i = 1; i <= Math.Sqrt(n); i++)
  {
    // If i*i is square check if there
    // exists another integer such that
    // h is a perfect square and i*i + h = n
    int h = n - i * i, h1 = (int)Math.Sqrt(h);

    // If h is perfect square
    if (h1 * h1 == h)
    {
      // Store in the sorted way
      int a = Math.Max(h1, i),
          b = Math.Min(h1, i);

      // If there is already a pair
      // check if pairs are equal or not
      if (vp.Count == 1 &&
          a != vp[0].first)
        vp.Add(new pair(a, b));

      // Insert the first pair
      if (vp.Count == 0)
        vp.Add(new pair(a, b));

      // If two pairs are found
      if (vp.Count == 2)
        return;
    }
  }
}

// Function to find the factors
static void findFactors(int n)
{
  // Get pairs where a^2 + b^2 = n
  List<pair> vp = new List<pair>();
  sumOfSquares(n, vp);

  // Number cannot be represented
  // as sum of squares in two ways
  if (vp.Count != 2)
    Console.Write("Factors Not Possible");

  // Assign a, b, c, d
  int a, b, c, d;

  a = vp[0].first;
  b = vp[0].second;

  c = vp[1].first;
  d = vp[1].second;

  // Swap if a < c because
  // if a - c < 0,
  // GCD cant be computed.
  if (a < c)
  {
    int t = a;
    a = c;
    c = t;
    t = b;
    b = d;
    d = t;
  }

  // Compute the values of k, h, l, m
  // using the formula mentioned
  // in the approach
  int k, h, l, m;
  k = __gcd(a - c, d - b);
  h = __gcd(a + c, d + b);
  l = (a - c) / k;
  m = (d - b) / k;

  // Print the values of a, b, c, d
  // and k, l, m, h
  Console.Write("a = " + a +
                "\t\t(A) a - c = " + 
                (a - c) +
                "\t\tk = gcd[A, C] = " +                   
                k + "\n");

  Console.Write("b = " + b +
                "\t\t(B) a + c = " + 
                (a + c) +
                "\t\th = gcd[B, D] = " +
                h + "\n");

  Console.Write("c = " +  c +
                "\t\t(C) d - b = " + 
                (d - b) +
                "\t\tl = A/k = " +
                l + "\n");

  Console.Write("d = " +  d +
                "\t\t(D) d + b = " +
                (d + b) +
                "\t\tm = c/k = " +
                m + "\n");

  // Printing the factors
  if (k % 2 == 0 && h % 2 == 0)
  {
    k = k / 2;
    h = h / 2;
    Console.Write("Factors are: " +
                  ((k) * (k) + (h) * (h)) +
                  " " + (l * l + m * m) + "\n");
  }
  else
  {
    l = l / 2;
    m = m / 2;
    Console.Write("Factors are: " +
                  ((l) * (l) + (m) * (m)) +
                  " " + (k * k + h * h) + "\n");
  }
}

// Driver code
public static void Main(String[] args)
{
  int n = 100000;
  findFactors(n);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to implement Eulers
// Factorization algorithm

class pair
{
    constructor(first,second)
    {
        this.first = first;
        this.second = second;
    }
}

// Recursive function to
// return gcd of a and b
function __gcd(a,b)
{
    return b == 0 ? a :
         __gcd(b, a % b);   
}

// Function to return N as the sum of
// two squares in two possible ways
function sumOfSquares(n,vp)
{
    // Iterate a loop from 1 to Math.sqrt(n)
  for (let i = 1; i <= Math.sqrt(n); i++)
  {
    // If i*i is square check if there
    // exists another integer such that
    // h is a perfect square and i*i + h = n
    let h = n - i * i, h1 = Math.floor(Math.sqrt(h));

    // If h is perfect square
    if (h1 * h1 == h)
    {
      // Store in the sorted way
      let a = Math.max(h1, i),
          b = Math.min(h1, i);

      // If there is already a pair
      // check if pairs are equal or not
      if (vp.length == 1 &&
          a != vp[0].first)
        vp.push(new pair(a, b));

      // Insert the first pair
      if (vp.length == 0)
        vp.push(new pair(a, b));

      // If two pairs are found
      if (vp.length == 2)
        return;
    }
  }
}

// Function to find the factors
function findFactors(n)
{
    // Get pairs where a^2 + b^2 = n
  let vp = [];
  sumOfSquares(n, vp);

  // Number cannot be represented
  // as sum of squares in two ways
  if (vp.length != 2)
    document.write("Factors Not Possible");

  // Assign a, b, c, d
  let a, b, c, d;

  a = vp[0].first;
  b = vp[0].second;

  c = vp[1].first;
  d = vp[1].second;

  // Swap if a < c because
  // if a - c < 0,
  // GCD cant be computed.
  if (a < c)
  {
    let t = a;
    a = c;
    c = t;
    t = b;
    b = d;
    d = t;
  }

  // Compute the values of k, h, l, m
  // using the formula mentioned
  // in the approach
  let k, h, l, m;
  k = __gcd(a - c, d - b);
  h = __gcd(a + c, d + b);
  l = (a - c) / k;
  m = (d - b) / k;

  // Print the values of a, b, c, d
  // and k, l, m, h
  document.write("a = " + a +
                   "       (A) a - c = " +
                   (a - c) +
                   "      k = gcd[A, C] = " +
                   k + "<br>");

  document.write("b = " + b +
                   "      (B) a + c = " +
                   (a + c) +
                   "      h = gcd[B, D] = " +
                   h + "<br>");

  document.write("c = " +  c +
                   "      (C) d - b = " +
                   (d - b) +
                   "      l = A/k = " +
                   l + "<br>");

  document.write("d = " +  d +
                   "      (D) d + b = " +
                   (d + b) +
                   "      m = c/k = " +
                   m + "<br>");

  // Printing the factors
  if (k % 2 == 0 && h % 2 == 0)
  {
    k = k / 2;
    h = h / 2;
    document.write("Factors are: " +
                     ((k) * (k) + (h) * (h)) +
                     " " + (l * l + m * m) + "<br>");
  }
  else
  {
    l = l / 2;
    m = m / 2;
    document.write("Factors are: " +
                     ((l) * (l) + (m) * (m)) +
                     " " + (k * k + h * h) + "<br>");
  }
}

// Driver code
let n = 100000;
findFactors(n);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
a = 316        (A) a - c = 16        k = gcd[A, C] = 8
b = 12        (B) a + c = 616        h = gcd[B, D] = 56
c = 300        (C) d - b = 88        l = A/k = 2
d = 100        (D) d + b = 112        m = c/k = 11
Factors are: 800 125
```

**复杂度分析:**
**时间复杂度:** *O(sqrt(N))* ，其中 N 为给定数
**空间复杂度:** O(1)
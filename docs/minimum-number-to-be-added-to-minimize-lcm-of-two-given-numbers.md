# 为最小化两个给定数值的 LCM 而添加的最小数值

> 原文:[https://www . geeksforgeeks . org/两个给定数字的最小添加数-最小化-LCM/](https://www.geeksforgeeks.org/minimum-number-to-be-added-to-minimize-lcm-of-two-given-numbers/)

给定两个数字 **A** 和 **B** ，任务是找到需要添加到 **A** 和 **B** 的最小数字，以使它们的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 最小。

**示例:**

> **输入:** A = 6，B = 10
> **输出:** 2
> **说明:**A 和 B 加 2，数值分别变成 8 和 12。8 和 12 的 LCM 是 24，这是可能的最小 LCM。
> 
> **输入:** A = 5，B = 10
> **输出:** 0
> **说明:**
> 10 已经是两个给定数的最小 LCM。
> 因此，添加的最小数量为 0。

**进场:**思路基于**(A+x)****(B+x)**的 LCM 等于**(A+x)*(B+x)/**[**GCD**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)**(A+x，B + x)** 的广义公式。可以观察到**(A+x)****(B+x)**的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 等于**(B–A)****(A+x)**的 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 。所以，gcd 是**(B- A)**的除数。

因此，迭代**(B- A)**的所有[除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)，如果 **A % M = B % M** (如果 **M** 是除数之一)，那么 **X** 的值(必须加上最小值)等于**M A % M**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function for finding all divisors
// of a given number
vector<int> getDivisors(int diff)
{
    // Stores the divisors of the
    // number diff
    vector<int> divisor;

    for (int i = 1; i * i <= diff; i++) {

        // If diff is a perfect square
        if (i == diff / i) {
            divisor.push_back(i);
            continue;
        }

        // If i divides diff then
        // diff / i also a divisor
        if (diff % i == 0) {
            divisor.push_back(i);
            divisor.push_back(diff / i);
        }
    }

    // Return the divisors stored
    return divisor;
}

// Function to find smallest integer x
// such that LCM of (A + X) and (B + X)
// is minimized
int findTheSmallestX(int a, int b)
{
    int diff = b - a;

    // Find all the divisors of diff
    vector<int> divisor
        = getDivisors(diff);

    // Find LCM of a and b
    int lcm = (a * b) / __gcd(a, b);

    int ans = 0;

    for (int i = 0;
         i < (int)divisor.size(); i++) {

        // From equation x = M - a % M
        // here M = divisor[i]
        int x = (divisor[i]
                 - (a % divisor[i]));

        // If already checked for x == 0
        if (!x)
            continue;

        // Find the product
        int product = (b + x) * (a + x);

        // Find the GCD
        int tempGCD = __gcd(a + x, b + x);
        int tempLCM = product / tempGCD;

        // If current lcm is minimum
        // than previous lcm, update ans
        if (lcm > tempLCM) {
            ans = x;
            lcm = tempLCM;
        }
    }

    // Print the number added
    cout << ans;
}

// Driver Code
int main()
{
    // Given A & B
    int A = 6, B = 10;

    // Function Call
    findTheSmallestX(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Recursive function to
// return gcd of a and b 
static int __gcd(int a, int b) 
{ 
  return b == 0 ? a :
         __gcd(b, a % b);    
}

// Function for finding all
// divisors of a given number
static int[] getDivisors(int diff)
{
  // Stores the divisors of
  // the number diff
  Vector<Integer> divisor =
         new Vector<>() ;

  for (int i = 1;
           i * i <= diff; i++)
  {
    // If diff is a perfect
    // square
    if (i == diff / i)
    {
      divisor.add(i);
      continue;
    }

    // If i divides diff then
    // diff / i also a divisor
    if (diff % i == 0)
    {
      divisor.add(i);
      divisor.add(diff / i);
    }
  }

  int []ans = new int[divisor.size()];
  int j = 0;

  for(int i: divisor)
    ans[j] = i;

  // Return the divisors
  // stored
  return ans;
}

// Function to find smallest integer
// x such that LCM of (A + X) and
// (B + X) is minimized
static void findTheSmallestX(int a,
                             int b)
{
  int diff = b - a;

  // Find all the divisors
  // of diff
  int[] divisor =
        getDivisors(diff);

  // Find LCM of a and b
  int lcm = (a * b) /
             __gcd(a, b);

  int ans = 0;

  for (int i = 0;
           i <divisor.length; i++)
  {
    // From equation x = M - a % M
    // here M = divisor[i]
    int x = 0;

    if(divisor[i] != 0)
      x = (divisor[i] -
          (a % divisor[i]));

    // If already checked for
    // x == 0
    if (x == 0)
      continue;

    // Find the product
    int product = (b + x) *
                  (a + x);

    // Find the GCD
    int tempGCD = __gcd(a + x,
                        b + x);
    int tempLCM = product /
                  tempGCD;

    // If current lcm is
    // minimum than previous
    // lcm, update ans
    if (lcm > tempLCM)
    {
      ans = x;
      lcm = tempLCM;
    }
  }

  // Print the number
  // added
  System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
  // Given A & B
  int A = 6, B = 10;

  // Function Call
  findTheSmallestX(A, B);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import gcd

# Function for finding all divisors
# of a given number
def getDivisors(diff):

    # Stores the divisors of the
    # number diff
    divisor = []

    for i in range(1, diff):
        if i * i > diff:
            break

        # If diff is a perfect square
        if (i == diff // i):
            divisor.append(i)
            continue

        # If i divides diff then
        # diff / i also a divisor
        if (diff % i == 0):
            divisor.append(i)
            divisor.append(diff // i)

    # Return the divisors stored
    return divisor

# Function to find smallest integer x
# such that LCM of (A + X) and (B + X)
# is minimized
def findTheSmallestX(a, b):

    diff = b - a

    # Find all the divisors of diff
    divisor = getDivisors(diff)

    # Find LCM of a and b
    lcm = (a * b) // gcd(a, b)

    ans = 0

    for i in range(len(divisor)):

        # From equation x = M - a % M
        # here M = divisor[i]
        x = (divisor[i] - (a % divisor[i]))

        # If already checked for x == 0
        if (not x):
            continue

        # Find the product
        product = (b + x) * (a + x)

        # Find the GCD
        tempGCD = gcd(a + x, b + x)
        tempLCM = product // tempGCD

        # If current lcm is minimum
        # than previous lcm, update ans
        if (lcm > tempLCM):
            ans = x
            lcm = tempLCM

    # Print the number added
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given A & B
    A = 6
    B = 10

    # Function Call
    findTheSmallestX(A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Recursive function to
// return gcd of a and b 
static int __gcd(int a, int b) 
{ 
  return b == 0 ? a :
         __gcd(b, a % b);    
}

// Function for finding all
// divisors of a given number
static int[] getDivisors(int diff)
{

  // Stores the divisors of
  // the number diff
  List<int> divisor = new List<int>();

  for(int i = 1; i * i <= diff; i++)
  {

    // If diff is a perfect
    // square
    if (i == diff / i)
    {
      divisor.Add(i);
      continue;
    }

    // If i divides diff then
    // diff / i also a divisor
    if (diff % i == 0)
    {
      divisor.Add(i);
      divisor.Add(diff / i);
    }
  }

  int []ans = new int[divisor.Count];
  int j = 0;

  foreach(int i in divisor)
    ans[j] = i;

  // Return the divisors
  // stored
  return ans;
}

// Function to find smallest integer
// x such that LCM of (A + X) and
// (B + X) is minimized
static void findTheSmallestX(int a,
                             int b)
{
  int diff = b - a;

  // Find all the divisors
  // of diff
  int[] divisor = getDivisors(diff);

  // Find LCM of a and b
  int lcm = (a * b) / __gcd(a, b);

  int ans = 0;

  for(int i = 0;
          i < divisor.Length; i++)
  {

    // From equation x = M - a % M
    // here M = divisor[i]
    int x = 0;

    if (divisor[i] != 0)
      x = (divisor[i] -
      (a % divisor[i]));

    // If already checked for
    // x == 0
    if (x == 0)
      continue;

    // Find the product
    int product = (b + x) *
                  (a + x);

    // Find the GCD
    int tempGCD = __gcd(a + x,
                        b + x);
    int tempLCM = product /
                  tempGCD;

    // If current lcm is
    // minimum than previous
    // lcm, update ans
    if (lcm > tempLCM)
    {
      ans = x;
      lcm = tempLCM;
    }
  }

  // Print the number
  // added
  Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{

  // Given A & B
  int A = 6, B = 10;

  // Function Call
  findTheSmallestX(A, B);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the
// above approach

// Recursive function to
// return gcd of a and b
function __gcd(a,b)
{
    return b == 0 ? a :
         __gcd(b, a % b);   
}

// Function for finding all
// divisors of a given number
function getDivisors(diff)
{
     // Stores the divisors of
  // the number diff
  let divisor = [];

  for (let i = 1;
           i * i <= diff; i++)
  {
    // If diff is a perfect
    // square
    if (i == diff / i)
    {
      divisor.push(i);
      continue;
    }

    // If i divides diff then
    // diff / i also a divisor
    if (diff % i == 0)
    {
      divisor.push(i);
      divisor.push(diff / i);
    }
  }

  let ans = new Array(divisor.length);
  let j = 0;

  for(let i=0;i< divisor.length;i++)
    ans[i] = divisor[i];

  // Return the divisors
  // stored
  return ans;
}

// Function to find smallest integer
// x such that LCM of (A + X) and
// (B + X) is minimized
function findTheSmallestX(a,b)
{
    let diff = b - a;

  // Find all the divisors
  // of diff
  let divisor =
        getDivisors(diff);

  // Find LCM of a and b
  let lcm = (a * b) /
             __gcd(a, b);

  let ans = 0;

  for (let i = 0;
           i <divisor.length; i++)
  {
    // From equation x = M - a % M
    // here M = divisor[i]
    let x = 0;

    if(divisor[i] != 0)
      x = (divisor[i] -
          (a % divisor[i]));

    // If already checked for
    // x == 0
    if (x == 0)
      continue;

    // Find the product
    let product = (b + x) *
                  (a + x);

    // Find the GCD
    let tempGCD = __gcd(a + x,
                        b + x);
    let tempLCM = product /
                  tempGCD;

    // If current lcm is
    // minimum than previous
    // lcm, update ans
    if (lcm > tempLCM)
    {
      ans = x;
      lcm = tempLCM;
    }
  }

  // Print the number
  // added
  document.write(ans);
}

// Driver Code

// Given A & B
let A = 6, B = 10;

// Function Call
findTheSmallestX(A, B);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(sqrt(B–A))*
***辅助空间:** O(max(A，B))*
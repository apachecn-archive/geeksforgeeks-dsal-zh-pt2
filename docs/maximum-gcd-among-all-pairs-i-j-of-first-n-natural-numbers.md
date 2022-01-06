# 前 N 个自然数的所有对(I，j)中的最大 GCD

> 原文:[https://www . geesforgeks . org/maximum-gcd-all-pairs-I-j-of-first-n-natural-numbers/](https://www.geeksforgeeks.org/maximum-gcd-among-all-pairs-i-j-of-first-n-natural-numbers/)

给定一个正整数 **N > 1** ，任务是在所有对 **(i，j)** 中找到最大 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) ，使得 **i < j < N** 。
**示例:**

> **输入:** N = 3
> **输出:** 3
> **解释:**
> 所有可能的对都是:(1，2) (1，3) (2，3)带有 GCD 1。
> **输入:** N = 4
> **输出:** 2
> **解释:**
> 在所有可能的对中，GCD 最大的对是(2，4)，值为 2。

**天真方法:**从范围**【1，N】**中生成所有可能的整数对，并计算所有对的 GCD。最后，打印获得的最大 GCD。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum gcd
// of all pairs possible from
// first n natural numbers
int maxGCD(int n)
{
    // Stores maximum gcd
    int maxHcf = INT_MIN;

    // Iterate over all possible pairs
    for (int i = 1; i <= n; i++) {
        for (int j = i + 1; j <= n; j++) {

            // Update maximum GCD
            maxHcf
                = max(maxHcf, __gcd(i, j));
        }
    }

    return maxHcf;
}

// Driver Code
int main()
{
    int n = 4;
    cout << maxGCD(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find maximum gcd
// of all pairs possible from
// first n natural numbers
static int maxGCD(int n)
{
  // Stores maximum gcd
  int maxHcf = Integer.MIN_VALUE;

  // Iterate over all possible pairs
  for (int i = 1; i <= n; i++)
  {
    for (int j = i + 1; j <= n; j++)
    {
      // Update maximum GCD
      maxHcf = Math.max(maxHcf,
                        __gcd(i, j));
    }
  }

  return maxHcf;
}

static int __gcd(int a, int b) 
{ 
  return b == 0 ? a :
         __gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
  int n = 4;
  System.out.print(maxGCD(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
def __gcd(a, b):
    if(b == 0):
        return a;
    else:
        return __gcd(b, a % b);

# Function to find maximum gcd
# of all pairs possible from
# first n natural numbers
def maxGCD(n):

    # Stores maximum gcd
    maxHcf = -2391734235435;

    # Iterate over all possible pairs
    for i in range(1, n + 1):
        for j in range(i + 1, n + 1):

            # Update maximum GCD
            maxHcf = max(maxHcf, __gcd(i, j));
    return maxHcf;

# Driver Code
if __name__ == '__main__':
    n = 4;
    print(maxGCD(n));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find maximum gcd
// of all pairs possible from
// first n natural numbers
static int maxGCD(int n)
{
  // Stores maximum gcd
  int maxHcf = int.MinValue;

  // Iterate over all possible pairs
  for (int i = 1; i <= n; i++)
  {
    for (int j = i + 1; j <= n; j++)
    {
      // Update maximum GCD
      maxHcf = Math.Max(maxHcf,
                        __gcd(i, j));
    }
  }

  return maxHcf;
}

static int __gcd(int a, int b) 
{ 
  return b == 0 ? a :
         __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
  int n = 4;
  Console.Write(maxGCD(n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for
// the above approach

    // Function to find maximum gcd
    // of all pairs possible from
    // first n natural numbers
    function maxGCD(n) {
        // Stores maximum gcd
        var maxHcf = Number.MIN_VALUE;

        // Iterate over all possible pairs
        for (i = 1; i <= n; i++) {
            for (j = i + 1; j <= n; j++) {
                // Update maximum GCD
                maxHcf = Math.max(maxHcf, __gcd(i, j));
            }
        }

        return maxHcf;
    }

    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver Code

        var n = 4;
        document.write(maxGCD(n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N<sup>2</sup>log N)
T5】辅助空间:O(1)
T8】高效进场:N**N**和 **N / 2** 的 GCD 为 **N / 2** ，这是从 1 到 **N** 的任意一对可能的所有 GCD 的最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum GCD
// among all the pairs from
// first n natural numbers
int maxGCD(int n)
{

    // Return max GCD
    return (n / 2);
}

// Driver Code
int main()
{
    int n = 4;
    cout << maxGCD(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find the maximum GCD
// among all the pairs from
// first n natural numbers
static int maxGCD(int n)
{

    // Return max GCD
    return (n / 2);
}

// Driver code
public static void main(String[] args)
{
    int n = 4;

    System.out.print(maxGCD(n));
}
}

// This code is contributed by Dewanti
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the maximum GCD
# among all the pairs from first n
# natural numbers
def maxGCD(n):

    # Return max GCD
    return (n // 2);

# Driver code
if __name__ == '__main__':

    n = 4;

    print(maxGCD(n));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to find the maximum GCD
// among all the pairs from
// first n natural numbers
static int maxGCD(int n)
{
  // Return max GCD
  return (n / 2);
}

// Driver code
public static void Main(String[] args)
{
  int n = 4;
  Console.Write(maxGCD(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the maximum GCD
// among all the pairs from
// first n natural numbers
function maxGCD(n)
{

    // Return max GCD
    return parseInt(n / 2);
}

// Driver Code
var n = 4;
document.write( maxGCD(n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
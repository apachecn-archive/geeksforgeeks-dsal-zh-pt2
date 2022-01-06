# 最大化最大数字 K，使得 K 的按位“与”直到 N 为 0

> 原文:[https://www . geeksforgeeks . org/maximum-最大数字-k-so-k-bit-and-of-t-n-is-0/](https://www.geeksforgeeks.org/maximize-the-largest-number-k-such-that-bitwise-and-of-k-till-n-is-0/)

给定一个整数 **N，**的任务是找到 **K** 的最大值，使得**N&(N-1)&(N-2)&……&(K)= 0。**这里 **&** 代表[按位 AND](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 运算符。

**示例:**

> **输入:** N = 5
> **输出:** 3
> **解释:**表达式的值 **5 & 4 & 3 = 0** 。任何大于 3 的值(例 4)都不会满足
> 给定的条件
> 
> **输入:**N = 17
> T3】输出: 15

**天真法:**蛮力法是从 N-1 开始，进行按位 and 运算，直到得到 0。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum value of k
// which makes bitwise AND zero.
int findMaxK(int N)
{
    // Take k = N initially
    int K = N;

    // Start traversing from N-1 till 0
    for (int i = N - 1; i >= 0; i--) {
        K &= i;

        // Whenever we get AND as 0
        // we stop and return
        if (K == 0) {
            return i;
        }
    }
    return 0;
}

// Driver Code
int main()
{
    int N = 5;
    cout << findMaxK(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
  // Function to find maximum value of k
// which makes bitwise AND zero.
static int findMaxK(int N)
{
    // Take k = N initially
    int K = N;

    // Start traversing from N-1 till 0
    for (int i = N - 1; i >= 0; i--) {
        K &= i;

        // Whenever we get AND as 0
        // we stop and return
        if (K == 0) {
            return i;
        }
    }
    return 0;
}
// Driver Code
    public static void main (String[] args) {
       int N = 5;
        System.out.println(findMaxK(N));
    }
}
// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for above approach

# Function to find maximum value of k
# which makes bitwise AND zero.
def findMaxK(N):
    # Take k = N initially
    K = N

    # Start traversing from N-1 till 0
    i = N-1
    while(i >= 0):
        K &= i

        # Whenever we get AND as 0
        # we stop and return
        if (K == 0):
            return i
        i -= 1
    return 0

# Driver Code
if __name__ == '__main__':
    N = 5
    print(findMaxK(N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  // Function to find maximum value of k
  // which makes bitwise AND zero.
  static int findMaxK(int N)
  {

    // Take k = N initially
    int K = N;

    // Start traversing from N-1 till 0
    for (int i = N - 1; i >= 0; i--) {
      K &= i;

      // Whenever we get AND as 0
      // we stop and return
      if (K == 0) {
        return i;
      }
    }
    return 0;
  }

  // Driver Code
  public static void Main (String[] args)
  {
    int N = 5;
    Console.Write(findMaxK(N));
  }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
  <script>
        // JavaScript Program to implement
        // the above approach

  // Function to find maximum value of k
// which makes bitwise AND zero.
function findMaxK(N)
{

    // Take k = N initially
    let K = N;

    // Start traversing from N-1 till 0
    for (let i = N - 1; i >= 0; i--) {
        K &= i;

        // Whenever we get AND as 0
        // we stop and return
        if (K == 0) {
            return i;
        }
    }
    return 0;
}

 // Driver Code
      let N = 5;
      document.write(findMaxK(N));

// This code is contributed by sanjoy_62.
    </script>
```

**Output**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间 : O(1)

**高效逼近:**通过一些观察可以看出，答案总是等于[的最高次方 2，](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)小于或等于(N-1)。最后，答案总是等于 2^K -1，其中 k 是某个值。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum value of k
// which makes bitwise AND zero.
int findMaxK(int N)
{
    // Finding the power less than N
    int p = log2(N);
    return pow(2, p);
}

// Driver Code
int main()
{
    int N = 5;
    cout << findMaxK(N) - 1 << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG {

    // Function to find maximum value of k
    // which makes bitwise AND zero.
    static int findMaxK(int N)
    {
        // Finding the power less than N
        int p = (int)(Math.log(N) / Math.log(2));
        return (int)Math.pow(2, p);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5;
        System.out.println(findMaxK(N) - 1);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
import math

# Function to find maximum value of k
# which makes bitwise AND zero.
def findMaxK(N):

    # Finding the power less than N
    p = math.log(N) // math.log(2);
    return int(pow(2, p));

# Driver Code
N = 5;
print(findMaxK(N) - 1);

# This code is contributed by _saurabh_jaiswal
```

## C#

```
/*package whatever //do not write package name here */
using System;

class GFG
{

    // Function to find maximum value of k
    // which makes bitwise AND zero.
    static int findMaxK(int N)
    {

        // Finding the power less than N
        int p = (int)(Math.Log(N) / Math.Log(2));
        return (int)Math.Pow(2, p);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 5;
        Console.Write(findMaxK(N) - 1);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
/*package whatever //do not write package name here */

// Function to find maximum value of k
// which makes bitwise AND zero.
function findMaxK(N)
{
// Finding the power less than N
var p = Math.log(N) / Math.log(2);
return parseInt(Math.pow(2, p));
}

    // Driver Code
var N = 5;
document.write(findMaxK(N) - 1);

// This code is contributed by 29AjayKumar
</script>
```

**Output**

```
3
```

**时间复杂度:**O(log N)
T3】辅助空间: O(1)
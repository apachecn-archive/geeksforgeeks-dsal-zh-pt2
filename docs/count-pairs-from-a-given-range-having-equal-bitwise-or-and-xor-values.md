# 对给定范围内具有相等按位“或”和“异或”值的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-from-from-a-给定-range-with-equal-bit-or-and-xor-values/](https://www.geeksforgeeks.org/count-pairs-from-a-given-range-having-equal-bitwise-or-and-xor-values/)

给定一个整数 **N** ，任务是从范围 **0 ≤ P，Q < 2 <sup>N</sup>** 中找出计数总对数 **(P，Q)** ，使得 **P OR Q = P XOR Q** 。由于计数可能很大，将其打印到[模 10 <sup>9</sup> + 7](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** N = 1
> **输出:** 3
> **说明:**满足 **P OR Q = P XOR Q** 的对(P，Q)为(0，0)，(0，1)和(1，0)。因此输出 3。
> 
> **输入:**N = 3
> T3】输出: 27

**天真方法:**最简单的方法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(P，Q)** 并计算满足 **P OR Q = P XOR Q 的对**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define MOD 1000000007
using namespace std;

// Function to calculate
// (x^y)%MOD
long long int power(int x, int y)
{

    // Initialize result
    long long int res = 1;

    // Update x if it is more than or
    // equal to MOD
    x = x % MOD;

    while (y > 0) {

        // If y is odd, multiply
        // x with result
        if (y & 1)
            res = (res * x) % MOD;

        // y must be even now
        // y = y/2
        y = y >> 1;
        x = (x * x) % MOD;
    }

    // Return (x^y)%MOD
    return res;
}

// Function to count total pairs
void countPairs(int N)
{
    // The upper bound is 2^N
    long long int high = power(2, N);

    // Stores the count of pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < high; i++) {
        for (int j = 0; j < high; j++) {

            // Find XOR of both integers
            int X = (i ^ j);

            // Find OR of both integers
            int Y = (i | j);

            // If both are equal
            if (X == Y) {

                // Increment count
                count++;
            }
        }
    }

    // Print count%MOD
    cout << count % MOD << endl;
}

// Driver Code
int main()
{
    int N = 10;

    // Function Call
    countPairs(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

static int MOD = 1000000007;

// Function to calculate
// (x^y)%MOD
static int power(int x, int y)
{

    // Initialize result
    int res = 1;

    // Update x if it is more than or
    // equal to MOD
    x = x % MOD;
    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ((y & 1) != 0)
            res = (res * x) % MOD;

        // y must be even now
        // y = y/2
        y = y >> 1;
        x = (x * x) % MOD;
    }

    // Return (x^y)%MOD
    return res;
}

// Function to count total pairs
static void countPairs(int N)
{

    // The upper bound is 2^N
    int high = power(2, N);

    // Stores the count of pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < high; i++)
    {
        for (int j = 0; j < high; j++)
        {

            // Find XOR of both integers
            int X = (i ^ j);

            // Find OR of both integers
            int Y = (i | j);

            // If both are equal
            if (X == Y)
            {

                // Increment count
                count++;
            }
        }
    }

    // Print count%MOD
    System.out.println(count % MOD);
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;

    // Function Call
    countPairs(N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate
# (x^y)%MOD
def power(x, y):
    MOD = 1000000007

    # Initialize result
    res = 1

    # Update x if it is more than or
    # equal to MOD
    x = x % MOD
    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % MOD

        # y must be even now
        #  y = y/2
        y = y >> 1
        x = (x * x) % MOD

    # Return (x^y)%MOD
    return res

# Function to count total pairs
def countPairs( N):
    MOD = 1000000007

    # The upper bound is 2^N
    high = power(2, N)

    # Stores the count of pairs
    count = 0

    # Generate all possible pairs
    for i in range(high):
        for j in range(high):

            # Find XOR of both integers
            X = (i ^ j)

            # Find OR of both integers
            Y = (i | j)

            # If both are equal
            if (X == Y):

                # Increment count
                count += 1

    # Print count%MOD
    print(count % MOD)

# Driver Code
N = 10

# Function Call
countPairs(N)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  static int MOD = 1000000007;

  // Function to calculate
  // (x^y)%MOD
  static int power(int x, int y)
  {

    // Initialize result
    int res = 1;

    // Update x if it is more than or
    // equal to MOD
    x = x % MOD;
    while (y > 0)
    {

      // If y is odd, multiply
      // x with result
      if ((y & 1) != 0)
        res = (res * x) % MOD;

      // y must be even now
      // y = y/2
      y = y >> 1;
      x = (x * x) % MOD;
    }

    // Return (x^y)%MOD
    return res;
  }

  // Function to count total pairs
  static void countPairs(int N)
  {

    // The upper bound is 2^N
    int high = power(2, N);

    // Stores the count of pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < high; i++)
    {
      for (int j = 0; j < high; j++)
      {

        // Find XOR of both integers
        int X = (i ^ j);

        // Find OR of both integers
        int Y = (i | j);

        // If both are equal
        if (X == Y)
        {

          // Increment count
          count++;
        }
      }
    }

    // Print count%MOD
    Console.WriteLine(count % MOD);
  }

  // Driver Code
  static public void Main()
  {
    int N = 10;

    // Function Call
    countPairs(N);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

     MOD = 1000000007;

    // Function to calculate
    // (x^y)%MOD
    function power(x , y) {

        // Initialize result
        var res = 1;

        // Update x if it is more than or
        // equal to MOD
        x = x % MOD;
        while (y > 0) {

            // If y is odd, multiply
            // x with result
            if ((y & 1) != 0)
                res = (res * x) % MOD;

            // y must be even now
            // y = y/2
            y = y >> 1;
            x = (x * x) % MOD;
        }

        // Return (x^y)%MOD
        return res;
    }

    // Function to count total pairs
    function countPairs(N) {

        // The upper bound is 2^N
        var high = power(2, N);

        // Stores the count of pairs
        var count = 0;

        // Generate all possible pairs
        for (i = 0; i < high; i++) {
            for (j = 0; j < high; j++) {

                // Find XOR of both integers
                var X = (i ^ j);

                // Find OR of both integers
                var Y = (i | j);

                // If both are equal
                if (X == Y) {

                    // Increment count
                    count++;
                }
            }
        }

        // Print count%MOD
        document.write(count % MOD);
    }

    // Driver Code

        var N = 10;

        // Function Call
        countPairs(N);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
59049
```

***时间复杂度:*****O(2<sup>2 * N</sup>)
***辅助空间:*** O(1)**

****高效方法:**为了优化上述方法，该想法基于以下观察:**

*   **把这一对看成 **(P，Q)** 。**修正 P** 然后找到所有满足这个等式的 **Qs** 。因此，所有在 P 中**设置**的位将在 q 中**取消设置****
*   **对于 P 中的每个**未置位位，有两个选项，即 **Q 中对应的位可以是 0 或 1** 。****
*   **所以对于任何 p，如果 p 中未设置的位数是 u(P)，那么 q 的数量将是 **ans1 = 2^u(P)** 。**
*   **使用变量 **i** 迭代范围**【0，N】**，那么对于每个 **2 <sup>i</sup>** 将有**T9】NC<sub>I</sub>**的贡献。这个数就是 **ans2** 。**
*   **所以对的计数由**∑(ans1 * ans2)=(1+2)<sup>N</sup>= 3<sup>N</sup>给出。****

****以下是上述方法的实现:****

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define MOD 1000000007
using namespace std;

// Function to find the value of (x^y)%MOD
long long int power(int x, int y)
{
    // Initialize result
    long long int res = 1;

    // Update x if it is more than or
    // equal to MOD
    x = x % MOD;

    while (y > 0) {

        // If y is odd, multiply
        // x with result
        if (y & 1)
            res = (res * x) % MOD;

        // y must be even now, then
        // update y/2
        y = y >> 1;
        x = (x * x) % MOD;
    }

    // Return (x^y)%MOD
    return res;
}

// Function to count total pairs
void countPairs(int N)
{
    // Finding 3^N % 10^9+7
    cout << power(3, N);
}

// Driver Code
int main()
{
    int N = 10;

    // Function Call
    countPairs(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG
{
  static final int MOD = 1000000007;

  // Function to find the value of (x^y)%MOD
  static int power(int x, int y)
  {

    // Initialize result
    int res = 1;

    // Update x if it is more than or
    // equal to MOD
    x = x % MOD;
    while (y > 0)
    {

      // If y is odd, multiply
      // x with result
      if (y % 2== 1)
        res = (res * x) % MOD;

      // y must be even now, then
      // update y/2
      y = y >> 1;
      x = (x * x) % MOD;
    }

    // Return (x^y)%MOD
    return res;
  }

  // Function to count total pairs
  static void countPairs(int N)
  {

    // Finding 3^N % 10^9+7
    System.out.print(power(3, N));
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 10;

    // Function Call
    countPairs(N);
  }
}

// This code is contributed by shikhasingrajput
```

## **蟒蛇 3**

```
# Python program for the above approach
MOD = 1000000007;

# Function to find the value of (x^y)%MOD
def power(x, y):

    # Initialize result
    res = 1;

    # Update x if it is more than or
    # equal to MOD
    x = x % MOD;
    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y % 2 == 1):
            res = (res * x) % MOD;

        # y must be even now, then
        # update y/2
        y = y >> 1;
        x = (x * x) % MOD;

    # Return (x^y)%MOD
    return res;

# Function to count total pairs
def countPairs(N):

    # Finding 3^N % 10^9+7
    print(power(3, N));

# Driver Code
if __name__ == '__main__':
    N = 10;

    # Function Call
    countPairs(N);

# This code is contributed by 29AjayKumar
```

## **C#**

```
// C# program for the above approach
using System;
public class GFG
{
  static readonly int MOD = 1000000007;

  // Function to find the value of (x^y)%MOD
  static int power(int x, int y)
  {

    // Initialize result
    int res = 1;

    // Update x if it is more than or
    // equal to MOD
    x = x % MOD;
    while (y > 0)
    {

      // If y is odd, multiply
      // x with result
      if (y % 2== 1)
        res = (res * x) % MOD;

      // y must be even now, then
      // update y/2
      y = y >> 1;
      x = (x * x) % MOD;
    }

    // Return (x^y)%MOD
    return res;
  }

  // Function to count total pairs
  static void countPairs(int N)
  {

    // Finding 3^N % 10^9+7
    Console.Write(power(3, N));
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 10;

    // Function Call
    countPairs(N);
  }
}

// This code contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach
     var MOD = 1000000007;

    // Function to find the value of (x^y)%MOD
    function power(x , y) {

        // Initialize result
        var res = 1;

        // Update x if it is more than or
        // equal to MOD
        x = x % MOD;
        while (y > 0) {

            // If y is odd, multiply
            // x with result
            if (y % 2 == 1)
                res = (res * x) % MOD;

            // y must be even now, then
            // update y/2
            y = y >> 1;
            x = (x * x) % MOD;
        }

        // Return (x^y)%MOD
        return res;
    }

    // Function to count total pairs
    function countPairs(N) {

        // Finding 3^N % 10^9+7
        document.write(power(3, N));
    }

    // Driver Code

        var N = 10;

        // Function Call
        countPairs(N);

// This code contributed by Rajput-Ji

</script>
```

****Output: **

```
59049
```** 

*****时间复杂度:O(log N)***
***辅助空间:O(1)*****
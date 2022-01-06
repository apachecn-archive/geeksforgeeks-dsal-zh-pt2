# 通过任意次数的加或减 A、B 或 0 形成的 C 之前的不同值的计数

> 原文:[https://www . geeksforgeeks . org/count-of-distinct-values-till-c-formed-by-add-or-减法-a-B- or-0-任意次数/](https://www.geeksforgeeks.org/count-of-distinct-values-till-c-formed-by-adding-or-substracting-a-b-or-0-any-number-of-times/)

给定三个整数 **A、B、C** 。您可以在范围 **0 <最终 _ 值≤ C** 内任意多次加减 A、B 或 0 形成新值。任务是找到这种不同的最终值的可能计数。

**示例**:

> **输入** : A = 2，B = 3，C = 10
> **输出** :10
> 可能值为:
> 0+3–2 = 1
> 0+2 = 2
> 0+3 = 3
> 2+2 = 4
> 2+3 = 5
> 3+3 = 6
> 3+2+2 = 7
> 2+2+2+2 = 8
> 2+2+2
> 
> **输入** : A = 10，B = 2，C = 10
> 输出 : 5

**方式:**思路是使用 **A 和**B 的[GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)T4【g】T5。

上述方法有效，因为每个不同的可能值都是 **xA+yB**

*   如果 A 可以写成 **g×a，** B 可以写成 **g×b**
*   那么，A 所需的最终值可以写成**xAg+yBg**=(x * g * A+y * g * b)= g *(xa+Yb)
*   由于最大可能值为 C，因此 **C = g*(xa+yb)** 。
*   因此，可能值的计数= **C/g** ，这是必需的答案。

**以下是上述方法**的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate gcd
int gcd(int A, int B)
{
    if (B == 0)
        return A;
    else
        return gcd(B, A % B);
}

// Function to find number of possible final values
int getDistinctValues(int A, int B, int C)
{

    // Find the gcd of two numbers
    int g = gcd(A, B);

    // Calculate number of distinct values
    int num_values = C / g;

    // Return values
    return num_values;
}

// Driver Code
int main()
{
    int A = 2;
    int B = 3;
    int C = 10;

    cout << (getDistinctValues(A, B, C));
    return 0;
}

// This code is contributed by subhammahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {
    // Function to calculate gcd
    static int gcd(int A, int B)
    {
        if (B == 0)
            return A;
        else
            return gcd(B, A % B);
    }

    // Function to find number of possible final values
    static int getDistinctValues(int A, int B, int C)
    {

        // Find the gcd of two numbers
        int g = gcd(A, B);

        // Calculate number of distinct values
        int num_values = C / g;

        // Return values
        return num_values;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A = 2;
        int B = 3;
        int C = 10;

        System.out.println(getDistinctValues(A, B, C));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate gcd
def gcd(A, B) :

    if (B == 0) :
        return A;
    else :
        return gcd(B, A % B);

# Function to find number of possible final values
def getDistinctValues(A, B, C) :

    # Find the gcd of two numbers
    g = gcd(A, B);

    # Calculate number of distinct values
    num_values = C / g;

    # Return values
    return int(num_values);

# Driver Code
A = 2;
B = 3;
C = 10;

print(getDistinctValues(A, B, C));

# This code is contributed by target_2.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to calculate gcd
  static int gcd(int A, int B)
  {
    if (B == 0)
      return A;
    else
      return gcd(B, A % B);
  }

  // Function to find number of possible final values
  static int getDistinctValues(int A, int B, int C)
  {

    // Find the gcd of two numbers
    int g = gcd(A, B);

    // Calculate number of distinct values
    int num_values = C / g;

    // Return values
    return num_values;
  }

  // Driver code
  static void Main()
  {
    int A = 2;
    int B = 3;
    int C = 10;

    Console.Write(getDistinctValues(A, B, C));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to calculate gcd
    function gcd(A, B)
    {
        if (B == 0)
            return A;
        else
            return gcd(B, A % B);
    }

    // Function to find number of possible final values
    function getDistinctValues(A, B, C)
    {

        // Find the gcd of two numbers
        let g = gcd(A, B);

        // Calculate number of distinct values
        let num_values = C / g;

        // Return values
        return num_values;
    }

    // Driver Code

        let A = 2;
        let B = 3;
        let C = 10;

        document.write(getDistinctValues(A, B, C));

</script>
```

**Output**

```
10
```

**时间复杂度** : O(log(最大(A，B))

**空间复杂度** : O(1)
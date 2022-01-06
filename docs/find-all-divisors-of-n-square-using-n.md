# 使用 N

查找 N2 的所有除数

> 原文:[https://www . geesforgeks . org/find-all-dividers-of-n-square-using-n/](https://www.geeksforgeeks.org/find-all-divisors-of-n-square-using-n/)

给定一个数字 **N** ，任务是打印**N<sup>2</sup>T5 的所有不同除数。**

**示例:**

> **输入:** N = 4
> **输出:** 1 2 4 8 16
> **解释:**
> N = 4，N<sup>2</sup>= 16
> 16 的除数为:1 2 4 8 16
> 
> **输入:**N = 8
> T3】输出: 1 2 4 8 16 32 64

**天真法:**
[用 sqrt(N)法求自然数的所有除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)。但是这种解决方案效率不高，因为时间复杂度是 **O(N)** 。

**高效方法:**

*   我们尝试使用 sqrt(N)方法从 N 的除数生成 N 的除数 <sup>2</sup> 。作为

**例如:**如果 N = 4，要生成 4 的除数 <sup>2</sup> = 16，我们首先要计算 4 的除数= 1，2，4。现在我们将迭代这些生成的除数来计算 4 <sup>2</sup> 的除数，它们是 1、2、4、8 和 16。
以下是上述方法的实施。

## C++

```
// C++ code to print all
// divisors of N*N using N

#include <bits/stdc++.h>
using namespace std;

// Function to find Divisor of N
void DivisorOfN(vector<int>& v,
                map<int, bool>& marked,
                int n)
{
    // sqrt(N) approach
    // to find divisors of N
    for (int i = 1; i <= sqrt(n); i++) {

        if (n % i == 0) {
            if (n / i == i) {
                v.push_back(i);
                marked[i] = true;
            }
            else {
                v.push_back(i);
                v.push_back(n / i);
                marked[i] = true;
                marked[n / i] = true;
            }
        }
    }
}

// Function to print all divisor of N*N
void PrintDivisors(int n)
{
    // Vector v to store divisors of n
    vector<int> v;

    // Map to avoid repeated divisors
    map<int, bool> marked;

    // Store all divisor of n
    DivisorOfN(v, marked, n);

    int size = v.size();

    // Iterating over vector v
    // to generate divisors of N*N
    for (int i = 0; i < size; i++) {
        for (int j = i; j < size; j++) {
            int check = v[i] * v[j];

            // Checking if element is
            // already present
            if (marked[check] != true) {
                v.push_back(v[i] * v[j]);

                // marking element true
                // after adding in vector
                marked[v[i] * v[j]] = true;
            }
        }
    }

    sort(v.begin(), v.end());

    printf("Divisors of %d are: ", n * n);
    for (int i = 0; i < v.size(); i++) {
        printf("%d ", v[i]);
    }
    printf("\n");
}

// Driver Code
int main()
{
    PrintDivisors(4);
    PrintDivisors(8);
    PrintDivisors(10);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print all
// divisors of N*N using N
import java.util.*;
class GFG
{

  // Vector v to store divisors of n
  static  List<Integer> v = new ArrayList<>();

  // Map to avoid repeated divisors
  static HashMap<Integer, Boolean> marked = new HashMap<>();

  // Function to find Divisor of N
  static void DivisorOfN(int n)
  {

    // sqrt(N) approach
    // to find divisors of N
    for (int i = 1; i <= Math.sqrt(n); i++)
    {

      if (n % i == 0)
      {
        if (n / i == i)
        {
          v.add(i);
          marked.put(i, true);
        }
        else
        {
          v.add(i);
          v.add(n / i);
          marked.put(i, true); 
          marked.put(n / i, true);
        }
      }
    }
  }

  // Function to print all divisor of N*N
  static void PrintDivisors(int n)
  {

    // Store all divisor of n
    DivisorOfN(n);
    int size = v.size();

    // Iterating over vector v
    // to generate divisors of N*N
    for (int i = 0; i < size; i++)
    {
      for (int j = i; j < size; j++)
      {
        int check = v.get(i) * v.get(j);

        // Checking if element is
        // already present
        if (!marked.containsKey(check))
        {
          v.add(v.get(i) * v.get(j));

          // marking element true
          // after adding in vector
          marked.put(v.get(i) * v.get(j), true);
        }
      }
    }

    Collections.sort(v);      
    System.out.print("Divisors of " + n * n + " are: ");
    for (int i = 0; i < v.size(); i++)
    {
      System.out.print(v.get(i) + " ");
    }
    System.out.println();
    v.clear();
    marked.clear();
  }

  // Driver code
  public static void main(String[] args)
  {
    PrintDivisors(4);
    PrintDivisors(8);
    PrintDivisors(10);
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 code to print all
# divisors of N*N using
from math import sqrt

# Function to find Divisor of N
def DivisorOfN(v, marked, n):
    # sqrt(N) approach
    # to find divisors of N
    for i in range(1,int(sqrt(n)) + 1, 1):
        if (n % i == 0):
            if (n // i == i):
                v.append(i)
                marked[i] = True
            else:
                v.append(i)
                v.append(n // i)
                marked[i] = True
                marked[n // i] = True

# Function to print all divisor of N*N
def PrintDivisors(n):
    # Vector v to store divisors of n
    v = []

    # Map to avoid repeated divisors
    marked = {i:False for i in range(1000)}

    # Store all divisor of n
    DivisorOfN(v, marked, n)

    size = len(v)

    # Iterating over vector v
    # to generate divisors of N*N
    for i in range(size):
        for j in range(i,size,1):
            check = v[i] * v[j]

            # Checking if element is
            # already present
            if (marked[check] != True):
                v.append(v[i] * v[j])

                # marking element true
                # after adding in vector
                marked[v[i] * v[j]] = True

    v.sort(reverse = False)

    print("Divisors of",n * n,"are: ",end = "")
    for i in range(len(v)):
        print(v[i],end = " ")

    print("\n",end = "")

# Driver Code
if __name__ == '__main__':
    PrintDivisors(4)
    PrintDivisors(8)
    PrintDivisors(10)

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# code to print all
// divisors of N*N using N
using System;
using System.Collections.Generic;
class GFG {

    // Vector v to store divisors of n
    static List<int> v = new List<int>();

    // Map to avoid repeated divisors
    static Dictionary<int, bool> marked = new Dictionary<int, bool>();

    // Function to find Divisor of N
    static void DivisorOfN(int n)
    {
        // sqrt(N) approach
        // to find divisors of N
        for (int i = 1; i <= Math.Sqrt(n); i++)
        {

            if (n % i == 0)
            {
                if (n / i == i)
                {
                    v.Add(i);
                    marked[i] = true;
                }
                else
                {
                    v.Add(i);
                    v.Add(n / i);
                    marked[i] = true;
                    marked[n / i] = true;
                }
            }
        }
    }

    // Function to print all divisor of N*N
    static void PrintDivisors(int n)
    {

        // Store all divisor of n
        DivisorOfN(n);

        int size = v.Count;

        // Iterating over vector v
        // to generate divisors of N*N
        for (int i = 0; i < size; i++)
        {
            for (int j = i; j < size; j++)
            {
                int check = v[i] * v[j];

                // Checking if element is
                // already present
                if (!marked.ContainsKey(check))
                {
                    v.Add(v[i] * v[j]);

                    // marking element true
                    // after adding in vector
                    marked[v[i] * v[j]] = true;
                }
            }
        }

        v.Sort();

        Console.Write("Divisors of " + n * n + " are: ");
        for (int i = 0; i < v.Count; i++)
        {
            Console.Write(v[i] + " ");
        }
        Console.WriteLine();

        v.Clear();
        marked.Clear();
    }

  // Driver code
  static void Main()
  {
    PrintDivisors(4);
    PrintDivisors(8);
    PrintDivisors(10);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript code to print all
// divisors of N*N using N

// Function to find Divisor of N
function DivisorOfN(v, marked, n)
{
    // sqrt(N) approach
    // to find divisors of N
    for (var i = 1; i <= Math.sqrt(n); i++) {

        if (n % i == 0) {
            if (n / i == i) {
                v.push(i);
                marked[i] = true;
            }
            else {
                v.push(i);
                v.push(n / i);
                marked[i] = true;
                marked[n / i] = true;
            }
        }
    }
}

// Function to print all divisor of N*N
function PrintDivisors(n)
{
    // Vector v to store divisors of n
    var v = [];

    // Map to avoid repeated divisors
    var marked = new Map();

    // Store all divisor of n
    DivisorOfN(v, marked, n);

    var size = v.length;

    // Iterating over vector v
    // to generate divisors of N*N
    for (var i = 0; i < size; i++) {
        for (var j = i; j < size; j++) {
            var check = v[i] * v[j];

            // Checking if element is
            // already present
            if (marked[check] != true) {
                v.push(v[i] * v[j]);

                // marking element true
                // after adding in vector
                marked[v[i] * v[j]] = true;
            }
        }
    }
    v.sort((a,b)=>a-b)

    document.write("Divisors of "+n*n+" are: ");
    for (var i = 0; i < v.length; i++) {
        document.write(v[i]+ " ");
    }
    document.write("<br>");
}

// Driver Code
PrintDivisors(4);
PrintDivisors(8);
PrintDivisors(10);

</script>
```

**Output:**

```
Divisors of 16 are: 1 2 4 8 16 
Divisors of 64 are: 1 2 4 8 16 32 64 
Divisors of 100 are: 1 2 4 5 10 20 25 50 100
```

***时间复杂度:** O(sqrt(N) + a <sup>2</sup> )* 其中 a 是 N 的除数
**注:**这种方法与[求自然数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)的所有除数有何不同？
设 N = 5，因此需要求 25 的所有除数。

*   **使用** [**中使用的方法查找自然数的所有除数**](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) **:** 我们将使用 I 从 1 迭代到 sqrt(25) = 5，并检查 I 和 n/I。
    ***时间复杂度:** O(sqrt(25))*

*   **使用本文中使用的方法:**我们将通过使用上述文章方法找到除数 5，这将在 sqrt(5)时间复杂度中完成。现在对于 5 的所有除数，即 1，5，我们将把它存储在一个数组中，并在两个循环的帮助下成对相乘{ (1*1，1*5，5*1，5*5) }并选择唯一的除数，即 1，5，25。这将花费 a^2 时间(其中 a 是 5 的除数，这里是 2)
    ***时间复杂度:** O(sqrt(5) + 2^2)*
    本文仅在该数的除数较少时比上述文章效果更好。
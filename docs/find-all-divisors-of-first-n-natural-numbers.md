# 求前 N 个自然数的所有除数

> 原文:[https://www . geeksforgeeks . org/find-all-divisions-of-first-n-natural-numbers/](https://www.geeksforgeeks.org/find-all-divisors-of-first-n-natural-numbers/)

给定一个整数 **N** ，任务是找出从 1 到 N 的所有数的除数
T3】注: 1？n？100000

**示例:**

> **输入:** N = 2
> **输出:**
> 1–>1
> 2–>1，2
> 
> **输入:** N = 5
> **输出:**
> 1–>1
> 2–>1、2
> 3–>1、3
> 4–>1、2、4
> 5–>1、5

**天真方法:**

*   使用循环变量迭代第一个 **N 个**自然数(比如说 **i** )
*   用循环变量迭代从 1 到 I 的自然数(比如 **j** )，并检查 i % j == 0。那么 j 是自然数 I 的除数。

下面是上述方法的实现:

## C++

```
// C++ implementation to find all
// the divisors of the first N
// natural numbers

#include <bits/stdc++.h>

using namespace std;

// Function to find the divisors
// of the first N natural numbers
void factors(int n)
{
    int i, j;
    cout << "1 -->1\n";

    // Loop to find the divisors
    for (i = 2; i <= n; i++) {
        cout << i << " -->";
        for (j = 1; j <= i / 2; j++) {
            if (i % j == 0)
                cout << j << ", ";
        }
        cout << i << "\n";
    }
}

// Driver Code
int main()
{
    int n = 5;
    factors(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find all
// the divisors of the first N
// natural numbers
class GFG{

// Function to find the divisors
// of the first N natural numbers
static void factors(int n)
{
    int i, j;
    System.out.print("1 -->1\n");

    // Loop to find the divisors
    for(i = 2; i <= n; i++)
    {
       System.out.print(i + " -->");
       for(j = 1; j <= i / 2; j++)
       {
          if (i % j == 0)
              System.out.print(j + ", ");
       }
       System.out.print(i + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    factors(n);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 implementation to find all
# the divisors of the first N
# natural numbers

# Function to find the divisors
# of the first N natural numbers
def factors(n):

    i = 0; j = 0;
    print("1 -->1");

    # Loop to find the divisors
    for i in range(2, n + 1):
        print(i, "-->", end = "");
        for j in range(1, (i // 2) + 1):
            if (i % j == 0):
                print(j, ",", end = "");

        print(i, end = "\n");

# Driver Code
n = 5;
factors(n);

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to find all
// the divisors of the first N
// natural numbers
using System;
class GFG{

// Function to find the divisors
// of the first N natural numbers
static void factors(int n)
{
    int i, j;
    Console.Write("1 -->1\n");

    // Loop to find the divisors
    for(i = 2; i <= n; i++)
    {
        Console.Write(i + " -->");
        for(j = 1; j <= i / 2; j++)
        {
            if (i % j == 0)
                Console.Write(j + ", ");
        }
        Console.Write(i + "\n");
    }
}

// Driver Code
public static void Main()
{
    int n = 5;
    factors(n);
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// JavaScript implementation to find all
// the divisors of the first N
// natural numbers

// Function to find the divisors
// of the first N natural numbers
function factors(n)
{
    let i, j;
    document.write("1 -->1<br>");

    // Loop to find the divisors
    for (i = 2; i <= n; i++) {
        document.write(i + " -->");
        for (j = 1; j <= parseInt(i / 2); j++) {
            if (i % j == 0)
                document.write(j + ", ");
        }
        document.write(i + "<br>");
    }
}

// Driver Code
let n = 5;
factors(n);

</script>
```

**Output:** 

```
1 -->1
2 -->1, 2
3 -->1, 3
4 -->1, 2, 4
5 -->1, 5
```

**时间复杂度:** O(N <sup>2</sup> )

**更好的方法:**

*   使用循环变量迭代第一个 **N 个**自然数。
*   为了让这个数找到它的除数，从 2 迭代到这个数，并检查其中的任何一个是否是给定数的除数。

下面是上述方法的实现:

## C++

```
// C++ implementation to find all
// the divisors of the first
// N natural numbers

#include <bits/stdc++.h>

using namespace std;

// Function to find the factors of
// the numbers from 1 to N
void factors(int n)
{
    int i, j;
    cout << "1 -->1\n";

    // Loop to find the factors
    // of the first N natural
    // numbers of the integer
    for (i = 2; i <= n; i++) {
        cout << i << " -->";
        for (j = 1; j * j <= i; j++) {
            if (i % j == 0){
                cout << j << ", ";
                if (i / j != j)
                cout << i/j << ", ";
            }
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{
    int n = 5;
    factors(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find all
// the divisors of the first
// N natural numbers
import java.util.*;
class GFG{

// Function to find the factors of
// the numbers from 1 to N
static void factors(int n)
{
    int i, j;
    System.out.print("1 -->1\n");

    // Loop to find the factors
    // of the first N natural
    // numbers of the integer
    for (i = 2; i <= n; i++)
    {
        System.out.print(i + " -->");
        for (j = 1; j * j <= i; j++)
        {
            if (i % j == 0)
            {
                System.out.print(j + ", ");
                if (i / j != j)
                    System.out.print(i / j + ", ");
            }
        }
        System.out.print("\n");
    }
}

// Driver Code
public static void main(String args[])
{
    int n = 5;
    factors(n);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation to find all
# the divisors of the first
# N natural numbers

# Function to find the factors of
# the numbers from 1 to N
def factors(n):

    print("1 -->1");

    # Loop to find the factors
    # of the first N natural
    # numbers of the integer
    for i in range(2, n + 1):
        print(i, " -->", end = "");

        for j in range(1, int(pow(i, 1))):
            if (i % j == 0):
                print(j, ", ", end = "");

                if (i // j != j):
                    print(i // j, ", ", end = "");

        print(end = "\n");

# Driver Code
if __name__ == '__main__':

    n = 5;
    factors(n);

# This code is contributed by gauravrajput1
```

## C#

```
// C# implementation to find all
// the divisors of the first
// N natural numbers
using System;
class GFG{

// Function to find the factors of
// the numbers from 1 to N
static void factors(int n)
{
    int i, j;
    Console.Write("1 -->1\n");

    // Loop to find the factors
    // of the first N natural
    // numbers of the integer
    for (i = 2; i <= n; i++)
    {
        Console.Write(i + " -->");
        for (j = 1; j * j <= i; j++)
        {
            if (i % j == 0)
            {
                Console.Write(j + ", ");
                if (i / j != j)
                    Console.Write(i / j + ", ");
            }
        }
        Console.Write("\n");
    }
}

// Driver Code
public static void Main()
{
    int n = 5;
    factors(n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to find all
// the divisors of the first
// N natural numbers

// Function to find the factors of
// the numbers from 1 to N
function factors(n)
{
    let i, j;
    document.write("1 -->1<br>");

    // Loop to find the factors
    // of the first N natural
    // numbers of the integer
    for(i = 2; i <= n; i++)
    {
        document.write(i + " -->");
        for(j = 1; j * j <= i; j++)
        {
            if (i % j == 0)
            {
                document.write(j + ", ");

                if (parseInt(i / j) != j)
                    document.write(parseInt(i/j) + ", ");
            }
        }
        document.write("<br>");
    }
}

// Driver Code
let n = 5;
factors(n);

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
1 -->1
2 -->1, 2, 
3 -->1, 3, 
4 -->1, 4, 2, 
5 -->1, 5, 
```

**时间复杂度:** O(N*sqrt(N))

**高效方法:**思路是借助厄拉多塞的[筛预计算数字的因子。然后最后迭代前 N 个自然数找到因子。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// factors of first N natural
// numbers

#include <bits/stdc++.h>

using namespace std;

const int MAX = 1e5;

// Initialize global divisor vector
// array of sequence container
vector<int> divisor[MAX + 1];

// Calculate all
// divisors of number
void sieve()
{
    for (int i = 1; i <= MAX; ++i) {
        for (int j = i; j <= MAX; j += i)
            divisor[j].push_back(i);
    }
}

// Function to find the
// factors of first n
// natural numbers
void findNFactors(int n){
    for(int i = 1; i <= n; i++){
        cout << i << "-->";
        for (auto &divi: divisor[i]){
            cout << divi << ", ";
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{
    int n = 5;
    sieve();

    // Function Call
    findNFactors(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// factors of first N natural
// numbers
import java.util.*;
class GFG{

static int MAX = (int) 1e5;

// Initialize global divisor vector
// array of sequence container
static Vector<Integer> []divisor = new Vector[MAX + 1];

// Calculate all
// divisors of number
static void sieve()
{
    for (int i = 1; i <= MAX; ++i)
    {
        for (int j = i; j <= MAX; j += i)
            divisor[j].add(i);
    }
}

// Function to find the
// factors of first n
// natural numbers
static void findNFactors(int n)
{
    for(int i = 1; i <= n; i++)
    {
        System.out.print(i+ "-->");
        for (int divi: divisor[i])
        {
            System.out.print(divi+ ", ");
        }
        System.out.print("\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    for (int i = 0; i < divisor.length; i++)
        divisor[i] = new Vector<Integer>();
    sieve();

    // Function Call
    findNFactors(n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the factors
# of first N natural numbers
MAX = 100001

# Initialize divisor list(array)
# of sequence container
divisor = [[] for x in range(MAX)]

# Calculate all divisors of a number
def sieve():

    for i in range(1, MAX):
        for j in range(i, MAX, i):
            divisor[j].append(i)

# Function to find the factors of
# first n natural numbers
def findNFactors (n):

    for i in range(1, n + 1):
        print(i, " --> ", end = '')

        for divi in divisor[i]:
            print(divi, ", ", end = '')
        print()

# Driver code
if __name__ == '__main__':

    n = 5
    sieve()

    # Function call
    findNFactors(n)

# This code is contributed by himanshu77
```

## C#

```
// C# implementation to find the
// factors of first N natural
// numbers
using System;
using System.Collections.Generic;

public class GFG{

static int MAX = (int) 1e5;

// Initialize global divisor vector
// array of sequence container
static List<int> []divisor = new List<int>[MAX + 1];

// Calculate all
// divisors of number
static void sieve()
{
    for (int i = 1; i <= MAX; ++i)
    {
        for (int j = i; j <= MAX; j += i)
            divisor[j].Add(i);
    }
}

// Function to find the
// factors of first n
// natural numbers
static void findNFactors(int n)
{
    for(int i = 1; i <= n; i++)
    {
        Console.Write(i+ "-->");
        foreach (int divi in divisor[i])
        {
            Console.Write(divi+ ", ");
        }
        Console.Write("\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    for (int i = 0; i < divisor.Length; i++)
        divisor[i] = new List<int>();
    sieve();

    // Function Call
    findNFactors(n);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// factors of first N natural
// numbers

var MAX = 100000;

// Initialize global divisor vector
// array of sequence container
var divisor = Array.from(Array(MAX+1),()=> Array(0));

// Calculate all
// divisors of number
function sieve()
{
    for (var i = 1; i <= MAX; ++i) {
        for (var j = i; j <= MAX; j += i)
            divisor[j].push(i);
    }
}

// Function to find the
// factors of first n
// natural numbers
function findNFactors(n){
    for(var i = 1; i <= n; i++){
        document.write( i + "-->");
        for (var j =0; j< divisor[i].length;j++){
            document.write( divisor[i][j] + ", ");
        }
        document.write( "<br>");
    }
}

// Driver Code
var n = 5;
sieve();

// Function Call
findNFactors(n);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1-->1, 
2-->1, 2, 
3-->1, 3, 
4-->1, 2, 4, 
5-->1, 5,
```
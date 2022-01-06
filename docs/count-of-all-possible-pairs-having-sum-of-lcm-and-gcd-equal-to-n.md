# LCM 和 GCD 之和等于 N 的所有可能对的计数

> 原文:[https://www . geesforgeks . org/所有可能对的计数-具有 lcm 和 gcd 之和-等于-n/](https://www.geeksforgeeks.org/count-of-all-possible-pairs-having-sum-of-lcm-and-gcd-equal-to-n/)

给定一个整数 **N** ，任务是找到所有可能的整数对( **A，B)** 的计数，使得 **GCD (A，B) + LCM (A，B) = N.**

**示例:**

> **输入:** N = 14
> **输出:** 7
> **解释:**
> 所有可能的对为{1，13}、{2，12}、{4，6}、{6，4}、{7，7}、{12，2}、{13，1}
> 
> **输入:**N = 6
> T3】输出: 5

**方法:**
按照以下步骤解决问题:

*   初始化一个变量**计数**，以存储所有可能对的计数。
*   迭代范围**【1，N】**到[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(i，j)。**使用 [__gcd()](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 功能计算 **(i，j)** 的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) ，计算 **(i，j)** 的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 。
*   现在，检查 **LCM (i，j)** 和 **GCD (i，j)** 之和是否等于 **N** 。如果是，增加**计数**。
*   完成范围遍历后，打印**计数**值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and
// return LCM of two numbers
int lcm(int a, int b)
{
    return (a * b) / __gcd(a, b);
}

// Function to count pairs
// whose sum of GCD and LCM
// is equal to N
int countPair(int N)
{
    int count = 0;
    for (int i = 1;
        i <= N; i++) {

        for (int j = 1;
            j <= N; j++) {

            if (__gcd(i, j)
                    + lcm(i, j)
                == N) {

                count++;
            }
        }
    }

    return count;
}

// Driver Code
int main()
{
    int N = 14;
    cout << countPair(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Recursive function to return gcd of a and b
static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Function to calculate and
// return LCM of two numbers
static int lcm(int a, int b)
{
    return (a * b) / __gcd(a, b);
}

// Function to count pairs
// whose sum of GCD and LCM
// is equal to N
static int countPair(int N)
{
    int count = 0;
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            if (__gcd(i, j) + lcm(i, j) == N)
            {
                count++;
            }
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int N = 14;

    System.out.print(countPair(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement 
# the above approach 

# Recursive function to return
# gcd of a and b 
def __gcd(a, b): 

    if b == 0:
        return a
    else:
        return __gcd(b, a % b)

# Function to calculate and 
# return LCM of two numbers 
def lcm(a, b):

    return (a * b) // __gcd(a, b) 

# Function to count pairs 
# whose sum of GCD and LCM 
# is equal to N 
def countPair(N): 

    count = 0

    for i in range(1, N + 1):
        for j in range(1, N + 1):
            if (__gcd(i, j) + lcm(i, j) == N): 
                count += 1 

    return count

# Driver code
if __name__=="__main__":

    N = 14 

    print(countPair(N))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Recursive function to return gcd of a and b
static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Function to calculate and
// return LCM of two numbers
static int lcm(int a, int b)
{
    return (a * b) / __gcd(a, b);
}

// Function to count pairs
// whose sum of GCD and LCM
// is equal to N
static int countPair(int N)
{
    int count = 0;
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            if (__gcd(i, j) + lcm(i, j) == N)
            {
                count++;
            }
        }
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 14;

    Console.Write(countPair(N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach    
// Recursive function to return gcd of a and b
    function __gcd(a , b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to calculate and
    // return LCM of two numbers
    function lcm(a , b) {
        return (a * b) / __gcd(a, b);
    }

    // Function to count pairs
    // whose sum of GCD and LCM
    // is equal to N
    function countPair(N)
    {
        var count = 0;
        for (i = 1; i <= N; i++) {
            for (j = 1; j <= N; j++) {
                if (__gcd(i, j) + lcm(i, j) == N) {
                    count++;
                }
            }
        }
        return count;
    }

    // Driver Code
        var N = 14;
        document.write(countPair(N));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*
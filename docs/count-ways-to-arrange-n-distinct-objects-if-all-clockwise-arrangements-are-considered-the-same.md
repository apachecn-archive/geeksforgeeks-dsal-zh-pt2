# 如果所有顺时针排列都被认为是相同的，计算排列 N 个不同物体的方法

> 原文:[https://www . geesforgeks . org/count-way-to-arrange-n-distinct-objects-if-all-顺时针排列-被认为是相同的/](https://www.geeksforgeeks.org/count-ways-to-arrange-n-distinct-objects-if-all-clockwise-arrangements-are-considered-the-same/)

给定 **N** 个不同的对象，如果所有顺时针排列都被认为是相同的，那么任务是找到 **N** 个对象的不同排列的数量。

> 如果 A、B 和 C 是三个不同的对象，则排列{A、B、C}、{C、A、B}和{B、C、A}被认为是相同的，因为所有排列都是彼此顺时针的。

**示例:**

> **输入:** N = 3
> **输出:** 2
> **解释:**
> 3 个不同对象的排列可以表示为这 6 种排列:{A、B、C}、{A、C、B}、{B、A、C}、{B、C、A}、{C、A、B}和{C、B、A}。但是排列{A，B，C}、{C，A，B}和{B，C，A}被认为是相同的。
> 安排{A、C、B}、{B、A、C}和{C、B、A}也被认为是相同的。
> 因此，只有两个不同的排列。
> 
> **输入:** N = 2
> **输出:** 1
> **说明:**
> 只能有 2 种排列:{A，B}和{B，A}。考虑到顺时针排列，这两种排列是相同的。
> 因此，只存在 1 个不同的排列。

**天真方法:**想法是[生成 **N**](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/) 不同对象的所有排列。现在，迭代所有排列，如果当前排列的顺时针旋转没有出现在以前的排列中，则递增计数器。检查所有排列后，尽可能将计数器打印为完全不同的顺时针排列。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N*N！)*

**高效方法:**想法是使用以下观察:

> 给定 N 个不同对象的排列{A <sub>1</sub> 、A <sub>2</sub> 、…、A <sub>N</sub> }。然后，可以有 N 个顺时针旋转排列，表示如下:
> 
> {A <sub>1</sub> ，A <sub>2</sub> ，…，A <sub>N</sub> }
> {A <sub>N</sub> ，A <sub>1</sub> ，…，A<sub>N-1</sub>}
> { A<sub>N-1</sub>，A <sub>N</sub> ，…，A <sub>N-2</sub> }
> {A <sub>N-2</sub>
> 
> 因此，对于长度的每个排列 **N** 存在 **N 顺时针**排列。还有，对于 N 个截然不同的物体，有 **N 个！**排列不考虑顺时针排列不变。
> 
> 因此，N*X = N！其中
> N 是长度为 N 的任何排列的顺时针排列。
> X 是考虑相同顺时针排列的排列数。
> N！是排列的总数。
> 
> 使用上面的等式:
> X = N！/N
> X =(N–1)！

因此，考虑到顺时针排列相同，不同排列的总数为**(N–1)！**。因此，任务是打印[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)**(N–1)**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to return the factorial
// of given number
unsigned int factorial(unsigned int n)
{
    // Base case
    if (n == 0)
        return 1;

    // Recursively find the factorial
    return n * factorial(n - 1);
}

// Driver Code
int main()
{
    // Given N objects
    int N = 4;

    // Function Call
    cout << factorial(N - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to return the factorial
// of given number
static int factorial(int n)
{

    // Base case
    if (n == 0)
        return 1;

    // Recursively find the factorial
    return n * factorial(n - 1);
}

// Driver Code
public static void main (String[] args)
{

    // Given N objects
    int N = 4;

    // Function Call
    System.out.print(factorial(N - 1));
}
}

// This code is contributed by math_lover
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the factorial
# of a given number
def factorial(n):

    # Base Case
    if n == 0:
        return 1

    # Recursively find the factorial
    return n * factorial(n-1)

# Driver Code

# Given N objects
N = 4

# Function Call
print(factorial(N - 1))
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to return
// the factorial
// of given number
static int factorial(int n)
{   
  // Base case
  if (n == 0)
    return 1;

  // Recursively find the
  // factorial
  return n * factorial(n - 1);
}

// Driver Code
public static void Main(String[] args)
{   
  // Given N objects
  int N = 4;

  // Function Call
  Console.Write(factorial(N - 1));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to return the factorial
// of given number
function factorial(n)
{

    // Base case
    if (n == 0)
        return 1;

    // Recursively find the factorial
    return n * factorial(n - 1);
}

    // Driver Code

    // Given N objects
    let N = 4;

    // Function Call
    document.write(factorial(N - 1));

</script>
```

**Output**

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
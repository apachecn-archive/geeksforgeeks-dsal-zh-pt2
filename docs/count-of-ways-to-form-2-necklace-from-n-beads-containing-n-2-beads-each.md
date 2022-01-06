# 从每颗含有 N/2 颗珠子的 N 颗珠子组成 2 条项链的方法计数

> 原文:[https://www . geesforgeks . org/count-of-to-form-2-项链-从-n-珠子-包含-n-2-珠子-每个/](https://www.geeksforgeeks.org/count-of-ways-to-form-2-necklace-from-n-beads-containing-n-2-beads-each/)

给定一个表示不同珠子数量的正整数 **N** ，任务是找出制作 2 条正好有 **N/2** 珠子的项链的方法数量。

**示例:**

> **输入:** N = 2
> **输出:** 1
> **说明:**
> 制作两条项链唯一可能的方法就是{1 | 2}。
> 
> ***输入:*** N = 4
> **输出:** 3
> **解释:**
> 制作两条项链的可能方式有{(1，2) | (3，4)}、{(1，3) | (2，4)}、{(1，4) | (2，3)}。

**方法:**利用[循环置换](https://www.geeksforgeeks.org/permutations-to-arrange-n-persons-around-a-circular-table/)和[组合学](https://www.geeksforgeeks.org/combinatorics-gq/)的概念可以解决问题。按照以下步骤解决问题:

*   定义一个函数，比如说[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)来计算一个数的阶乘，方法如下:
    *   **基本情况:**如果 **n = 0** ，则返回 **1** 。
    *   如果 **n！= 0** ，然后递归调用函数并返回 **n *阶乘(n-1)** 。
*   初始化一个变量，比如说 **ans** 为 **C(N，N/2)**，这是从 **N** 珠子中选择 **N/2** 珠子的方法数。
*   因为项链是圆形的，所以置换 **N/2** 珠子的方式数是**阶乘(N/2-1)**，所以将 **ans** 的值乘以**阶乘(N/2-1)*阶乘(N/2-1)** 因为有两条项链。
*   现在将**和**除以 **2。**因为对称分布。例如，对于 **N=2** ，分布 **{1 | 2}** 和 **{2 | 1}** 被认为是相同的。
*   最后，完成以上步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate factorial
int factorial(int n)
{
    if (n == 0)
        return 1;
    return n * factorial(n - 1);
}

// Function to count number of ways
// to make 2 necklace having exactly
// N/2 beads if each bead is
// considered different
long long numOfNecklace(int N)
{
    // Number of ways to choose N/2 beads
    // from N beads
    long long ans = factorial(N)
                    / (factorial(N / 2) * factorial(N / 2));

    // Number of ways to permute N/2 beads
    ans = ans * factorial(N / 2 - 1);
    ans = ans * factorial(N / 2 - 1);

    // Divide ans by 2 to remove repetitions
    ans /= 2;

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int N = 4;

    // Function Call
    cout << numOfNecklace(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Function to calculate factorial
    static int factorial(int n)
    {
        if (n == 0)
            return 1;
        return n * factorial(n - 1);
    }

    // Function to count number of ways
    // to make 2 necklace having exactly
    // N/2 beads if each bead is
    // considered different
    static long numOfNecklace(int N)
    {

        // Number of ways to choose N/2 beads
        // from N beads
        long ans = factorial(N)
                   / (factorial(N / 2) * factorial(N / 2));

        // Number of ways to permute N/2 beads
        ans = ans * factorial(N / 2 - 1);
        ans = ans * factorial(N / 2 - 1);

        // Divide ans by 2 to remove repetitions
        ans /= 2;

        // Return ans
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int N = 4;

        // Function Call
        System.out.println(numOfNecklace(N));

    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to calculate factorial
def factorial(n):
    if (n == 0):
        return 1
    return n * factorial(n - 1)

# Function to count number of ways
# to make 2 necklace having exactly
# N/2 beads if each bead is
# considered different
def numOfNecklace(N):

    # Number of ways to choose N/2 beads
    # from N beads
    ans = factorial(N) // (factorial(N // 2) * factorial(N // 2))

    # Number of ways to permute N/2 beads
    ans = ans * factorial(N // 2 - 1)
    ans = ans * factorial(N // 2 - 1)

    # Divide ans by 2 to remove repetitions
    ans //= 2

    # Return ans
    return ans

# Driver Code
if __name__ == '__main__':
    # Given Input
    N = 4

    # Function Call
    print(numOfNecklace(N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate factorial
static int factorial(int n)
{
    if (n == 0)
        return 1;

    return n * factorial(n - 1);
}

// Function to count number of ways
// to make 2 necklace having exactly
// N/2 beads if each bead is
// considered different
static long numOfNecklace(int N)
{

    // Number of ways to choose N/2 beads
    // from N beads
    long ans = factorial(N) /
              (factorial(N / 2) *
               factorial(N / 2));

    // Number of ways to permute N/2 beads
    ans = ans * factorial(N / 2 - 1);
    ans = ans * factorial(N / 2 - 1);

    // Divide ans by 2 to remove repetitions
    ans /= 2;

    // Return ans
    return ans;
}

// Driver Code
static public void Main ()
{

    // Given Input
    int N = 4;

    // Function Call
    Console.Write( numOfNecklace(N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate factorial
function factorial(n)
{
    if (n == 0)
        return 1;
    return n * factorial(n - 1);
}

// Function to count number of ways
// to make 2 necklace having exactly
// N/2 beads if each bead is
// considered different
function numOfNecklace(N)
{

    // Number of ways to choose N/2 beads
    // from N beads
    var ans = factorial(N)
                    / (factorial(N / 2) * factorial(N / 2));

    // Number of ways to permute N/2 beads
    ans = ans * factorial(N / 2 - 1);
    ans = ans * factorial(N / 2 - 1);

    // Divide ans by 2 to remove repetitions
    ans /= 2;

    // Return ans
    return ans;
}

// Driver Cod
    // Given Input
    var N = 4;

    // Function Call
    document.write(numOfNecklace(N));

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
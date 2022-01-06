# 从给定的整数 N 开始计算达到 0 的最小步数

> 原文:[https://www . geesforgeks . org/count-从给定整数 n 开始到达 0 的最小步数/](https://www.geeksforgeeks.org/count-the-minimum-steps-to-reach-0-from-the-given-integer-n/)

给定**两个整数 N 和 K** ，其中 K 表示允许我们直接从 N 减少到 N–K 的跳跃次数，我们的任务是在给定的操作后计算达到 0 的最小步数:

*   我们可以从 N 跳一个量，也就是 N = N–K
*   将 N 减 1，即 N = N -1。

**示例:**

> **输入:** N = 11，K = 4
> **输出:** 5
> **解释:**
> 对于给定值 N，我们可以按照给定的顺序执行操作:11->7->3->2->1->0
> 
> **输入:** N = 6，K = 3
> **输出:** 2
> **说明:**
> 对于给定值 N，我们可以按照给定的顺序进行操作:6 - > 3 - > 0。

**方法:**
要解决上面提到的问题，我们知道需要 **N / K** 步直接从 N 值跳转到 K 可分性最小的值， **N % K** 步递减 1，如将计数减为 0。因此**从 N 到达 0 所需的总步数为**

> **(N / K) + (N % K)**

下面是上述方法的实现:

## C++

```
// C++ program to Count the minimum steps
// to reach 0 from the given integer N

#include <bits/stdc++.h>
using namespace std;

// Function returns min step
// to reach 0 from N
int getMinSteps(int n, int jump)
{
    // Direct possible
    // reduction of value N
    int quotient = n / jump;

    // Remaining steps needs
    // to be reduced by 1
    int remainder = n % jump;

    // Summation of both the values
    int steps = quotient + remainder;

    // Return the final answer
    return steps;
}

// Driver code
int main()
{
    int N = 6, K = 3;

    cout << getMinSteps(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the minimum steps
// to reach 0 from the given integer N
class GFG{

// Function returns min step
// to reach 0 from N
static int getMinSteps(int n, int jump)
{

    // Direct possible
    // reduction of value N
    int quotient = n / jump;

    // Remaining steps needs
    // to be reduced by 1
    int remainder = n % jump;

    // Summation of both the values
    int steps = quotient + remainder;

    // Return the final answer
    return steps;
}

// Driver code
public static void main(String[] args)
{
    int N = 6, K = 3;

    System.out.print(getMinSteps(N, K));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to Count the minimum steps
# to reach 0 from the given integer N

# Function returns min step
# to reach 0 from N
def getMinSteps(n, jump):

    # Direct possible
    # reduction of value N
    quotient = int(n / jump)

    # Remaining steps needs
    # to be reduced by 1
    remainder = n % jump

    # Summation of both the values
    steps = quotient + remainder

    # Return the final answer
    return steps

# Driver code
N = 6
K = 3

print (getMinSteps(N, K))

# This code is contributed by PratikBasu
```

## C#

```
// C# program to count the minimum steps
// to reach 0 from the given integer N
using System;

class GFG{

// Function returns min step
// to reach 0 from N
static int getMinSteps(int n, int jump)
{

    // Direct possible
    // reduction of value N
    int quotient = n / jump;

    // Remaining steps needs
    // to be reduced by 1
    int remainder = n % jump;

    // Summation of both the values
    int steps = quotient + remainder;

    // Return the final answer
    return steps;
}

// Driver code
public static void Main(string[] args)
{
    int N = 6, K = 3;

    Console.Write(getMinSteps(N, K));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// JavaScript program to Count the minimum steps
// to reach 0 from the given integer N

// Function returns min step
// to reach 0 from N
function getMinSteps(n, jump)
{

    // Direct possible
    // reduction of value N
    let quotient = Math.floor(n / jump);

    // Remaining steps needs
    // to be reduced by 1
    let remainder = n % jump;

    // Summation of both the values
    let steps = quotient + remainder;

    // Return the final answer
    return steps;
}

// Driver code
    let N = 6, K = 3;
    document.write(getMinSteps(N, K));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
2
```
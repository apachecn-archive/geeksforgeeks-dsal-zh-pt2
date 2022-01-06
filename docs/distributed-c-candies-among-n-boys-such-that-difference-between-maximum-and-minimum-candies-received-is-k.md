# 在 N 个男孩中分发 C 糖果，使得收到的最大和最小糖果之间的差异为 K

> 原文:[https://www . geeksforgeeks . org/distributed-c-candes-in-n-boys-这样-收到的最大糖果和最小糖果之间的差异是-k/](https://www.geeksforgeeks.org/distributed-c-candies-among-n-boys-such-that-difference-between-maximum-and-minimum-candies-received-is-k/)

给定两个整数 **N** 和 **C** ，代表男孩和糖果的数量，以及一个整数 **K** ，任务是计算任何男孩收到的糖果的最大和最小数量，使得它们之间的差值为 **K** 。

**示例:**

> **输入:** N = 4，C = 12，K = 3
> **输出:**
> 最大值= 5
> 最小值= 2
> **说明:**
> 将{2，2，3，5}颗糖果分发给 N (= 4)个男生。
> 因此，最大值和最小值之差为 5–2 = 3(= K)。
> 
> **输入:** N = 2，C = 8，K = 2
> **输出:**
> 最大值= 5
> 最小值= 3。

**方法:**给定的问题可以基于以下观察来解决:

1.  **如果 K > = C :** 所有的 **C** 糖果都可以分给 1 <sup>圣</sup>小子。因此，糖果的最大数量为 **C** ，最小数量为 **0** 。
2.  否则，将糖果分发给男生，保持最大和最小计数至**≤**

> **图解:**参照下表观察糖果的分布规律。
> 
> <figure class="table">
> 
> | **男孩 A** | **男生 B** | **男生 C** | **差异** |
> | K | Zero | Zero | K |
> | K | one | one | K-1 |
> | K+1 | one | one | K |
> | K+1 | Two | Two | K-1 |
> | K+2 | Two | Two | K |
> 
> 最初，将 **K** 糖果分发给 **1** <sup>st</sup> 男孩。
> 现在，将剩余的**C–K**糖果从 **2** 第二个男孩分发到 **N** 第一个男孩，然后再从 1 <sup>st</sup> 分发到 **N** 第一个男孩，依此类推。
> 
> </figure>

按照以下步骤解决问题:

1.  初始化两个变量，比如**最大**和**最小，**来存储一个男孩可以拥有的最大糖果数和最小糖果数。
2.  **如果 N = 1:** 设置**最大值= C** 和**最小值= C**
3.  **如果 K > = C:** 设置**最大值** **= C** 和**最小值** **= 0**
4.  否则，如果 **K < C** ，设置**最大值= K** 和**最小值= 0** 。现在，按照以下步骤操作:
    1.  初始化一个变量，说**保留 _candy，**并将其设置为**C–k .**
    2.  在**最大**和**最小**上加上(**resist _ candy/N**)。
    3.  如果(**剩余 _ 糖果% N == N-1** ，增加**最小值**。
5.  打印**最小值**和**最大值**值。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// maximum and minimum number
// of candies a boy can possess
int max_min(int N, int C, int K)
{
    int maximum, minimum;

    if (N == 1) {

        // All candies will be
        // given to one boy
        maximum = minimum = C;
    }

    else if (K >= C) {

        // All the candies will
        // be given to 1 boy
        maximum = C;
        minimum = 0;
    }

    else {

        // Give K candies to 1st
        // boy initially
        maximum = K;
        minimum = 0;

        // Count remaining candies
        int remain_candy = C - K;

        maximum += remain_candy / N;
        minimum = remain_candy / N;

        // If the last candy of remaining candies
        // is given to the last boy, i.e Nth boy
        if (remain_candy % N == N - 1) {

            // Increase minimum count
            minimum++;
        }
    }

    cout << "Maximum = " << maximum << endl;
    cout << "Minimum = " << minimum;

    return 0;
}

// Driver Code
int main()
{
    int N = 4;
    int C = 12;
    int K = 3;

    max_min(N, C, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate the
// maximum and minimum number
// of candies a boy can possess
static void max_min(int N, int C, int K)
{
    int maximum, minimum;

    if (N == 1)
    {

        // All candies will be
        // given to one boy
        maximum = minimum = C;
    }

    else if (K >= C)
    {

        // All the candies will
        // be given to 1 boy
        maximum = C;
        minimum = 0;
    }

    else
    {

        // Give K candies to 1st
        // boy initially
        maximum = K;
        minimum = 0;

        // Count remaining candies
        int remain_candy = C - K;

        maximum += remain_candy / N;
        minimum = remain_candy / N;

        // If the last candy of remaining candies
        // is given to the last boy, i.e Nth boy
        if (remain_candy % N == N - 1)
        {

            // Increase minimum count
            minimum++;
        }
    }
    System.out.println("Maximum = " + maximum);
    System.out.println("Minimum = " + minimum);
}

// Driver code
public static void main(String[] args)
{
    int N = 4;
    int C = 12;
    int K = 3;

    max_min(N, C, K);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the
# maximum and minimum number
# of candies a boy can possess
def max_min(N, C, K):

    maximum = 0
    minimum = 0

    if (N == 1):

        # All candies will be
        # given to one boy
        maximum = minimum = C

    elif (K >= C):

        # All the candies will
        # be given to 1 boy
        maximum = C
        minimum = 0

    else:

        # Give K candies to 1st
        # boy initially
        maximum = K
        minimum = 0

        # Count remaining candies
        remain_candy = C - K

        maximum += remain_candy // N
        minimum = remain_candy // N

    # If the last candy of remaining candies
    # is given to the last boy, i.e Nth boy
    if (remain_candy % N == N - 1):

        # Increase minimum count
        minimum += 1

    print("Maximum = {}".format(maximum))
    print("Minimum = {}".format(minimum))

# Driver code
N = 4
C = 12
K = 3

max_min(N, C, K)

# This code is contributed by abhinavjain194
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate the
// maximum and minimum number
// of candies a boy can possess
static void max_min(int N, int C, int K)
{
    int maximum, minimum;

    if (N == 1)
    {

        // All candies will be
        // given to one boy
        maximum = minimum = C;
    }

    else if (K >= C)
    {

        // All the candies will
        // be given to 1 boy
        maximum = C;
        minimum = 0;
    }

    else
    {

        // Give K candies to 1st
        // boy initially
        maximum = K;
        minimum = 0;

        // Count remaining candies
        int remain_candy = C - K;

        maximum += remain_candy / N;
        minimum = remain_candy / N;

        // If the last candy of remaining candies
        // is given to the last boy, i.e Nth boy
        if (remain_candy % N == N - 1)
        {

            // Increase minimum count
            minimum++;
        }
    }
    Console.WriteLine("Maximum = " + maximum);
    Console.WriteLine("Minimum = " + minimum);
}

// Driver code
static void Main()
{
    int N = 4;
    int C = 12;
    int K = 3;

    max_min(N, C, K);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate the
// maximum and minimum number
// of candies a boy can possess
function max_min(N, C, K)
{
    let maximum, minimum;

    if (N == 1)
    {

        // All candies will be
        // given to one boy
        maximum = minimum = C;
    }

    else if (K >= C)
    {

        // All the candies will
        // be given to 1 boy
        maximum = C;
        minimum = 0;
    }

    else
    {

        // Give K candies to 1st
        // boy initially
        maximum = K;
        minimum = 0;

        // Count remaining candies
        let remain_candy = C - K;

        maximum += Math.floor(remain_candy / N);
        minimum = Math.floor(remain_candy / N);

        // If the last candy of remaining candies
        // is given to the last boy, i.e Nth boy
        if (remain_candy % N == N - 1)
        {

            // Increase minimum count
            minimum++;
        }
    }
    document.write("Maximum = " + maximum + "<br/>");
    document.write("Minimum = " + minimum);
}

// Driver code

    let N = 4;
    let C = 12;
    let K = 3;

    max_min(N, C, K);

</script>
```

**Output:** 

```
Maximum = 5
Minimum = 2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)
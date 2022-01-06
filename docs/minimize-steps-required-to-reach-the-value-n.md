# 尽量减少达到数值 N 所需的步骤

> 原文:[https://www . geesforgeks . org/minimum-达到价值所需的步骤-n/](https://www.geeksforgeeks.org/minimize-steps-required-to-reach-the-value-n/)

给定范围 **[-INFINITY，+INFINITY]** 中的一个无限数线和一个整数 **N** ，任务是从 **0** 开始，通过向前移动 **i** 步或在每次 **i <sup>第</sup>T15】步中向后移动 **1** 步，找到到达 **N** 所需的最小步数。**

**示例:**

> ***输入:** N = 18*
> ***输出:** 6*
> ***解释:***
> *要达到给定值 N，按以下顺序进行运算:1–1+3+4+5+6 = 18*
> *因此，总共需要 6 次运算。*
> 
> ***Inpu*****t:**N = 3
> ***Output:**2*
> ***解释:***
> *要达到给定值 N，按以下顺序进行运算:1 + 2 = 3*
> *因此，总共需要 2 次运算。*

**进场:**思路是最初，继续加 **1、2、3。。。。K** ，直到大于或等于要求值 **N** 。然后，计算需要从当前总和中减去的数字。按照以下步骤解决问题:

*   最初，增加 **K** 直到 **N** 大于当前值。现在，在某个位置
    停止。+步数=步数∗(步数+ 1) / 2 ≥ N.
    ***注:**0≤pos–N<步数*。否则，最后一步是不可能的。
    *   **案例 1:** 如果 **pos = N** 那么，‘steps’就是要求的答案。
    *   **情况 2:** 如果**位置≠ N** ，那么将 **K** 的任意迭代替换为-1。
*   通过将任意 **K** 替换为 **-1** ，**pos = pos –( K+1)**的修改值。既然**K∈1，步骤】**，那么**pos∈pos–步骤–1，位置–2】**。
*   很明显**位置–步骤< N** 。如果**N<pos–1**，则选择对应的**K = pos–N–1**，将 **K** 替换为 **-1** ，直奔主题 **N** 。
*   如果 **N + 1 = pos** ，只需要一次 **-1** 操作。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum steps
// required to reach N by either moving
// i steps forward or 1 steps backward
int minimumsteps(int N)
{

    // Stores the required count
    int steps = 0;

    // IF total moves required
    // is less than double of N
    while (steps * (steps + 1) < 2 * N) {

        // Update steps
        steps++;
    }

    // Steps required to reach N
    if (steps * (steps + 1) / 2 == N + 1) {

        // Update steps
        steps++;
    }

    cout << steps;
}

// Driver Code
int main()
{

    // Given value of N
    int N = 18;
    minimumsteps(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the minimum steps
// required to reach N by either moving
// i steps forward or 1 steps backward
static void minimumsteps(int N)
{

    // Stores the required count
    int steps = 0;

    // IF total moves required
    // is less than double of N
    while (steps * (steps + 1) < 2 * N)
    {

        // Update steps
        steps++;
    }

    // Steps required to reach N
    if (steps * (steps + 1) / 2 == N + 1)
    {

        // Update steps
        steps++;
    }

    System.out.println(steps);
}

// Driver code
public static void main(String[] args)
{

    // Given value of N
    int N = 18;
    minimumsteps(N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Function to find the minimum steps
# required to reach N by either moving
# i steps forward or 1 steps backward

def minimumsteps(N) :

    # Stores the required count
    steps = 0

    # IF total moves required
    # is less than double of N
    while (steps * (steps + 1) < 2 * N) :

        # Update steps
        steps += 1

    # Steps required to reach N
    if (steps * (steps + 1) / 2 == N + 1) :

        # Update steps
        steps += 1
    print(steps)

# Driver code
N = 18;
minimumsteps(N)

# This code is contributed by Dharanendra L V
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the minimum steps
    // required to reach N by either moving
    // i steps forward or 1 steps backward
    static void minimumsteps(int N)
    {

        // Stores the required count
        int steps = 0;

        // IF total moves required
        // is less than double of N
        while (steps * (steps + 1) < 2 * N) {

            // Update steps
            steps++;
        }

        // Steps required to reach N
        if (steps * (steps + 1) / 2 == N + 1) {

            // Update steps
            steps++;
        }

        Console.WriteLine(steps);
    }

    // Driver code
    static public void Main()
    {

        // Given value of N
        int N = 18;
        minimumsteps(N);
    }
}

// This code is contributed by Dharanendra LV
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum steps
// required to reach N by either moving
// i steps forward or 1 steps backward
function minimumsteps(N)
{

    // Stores the required count
    let steps = 0;

    // IF total moves required
    // is less than double of N
    while (steps * (steps + 1) < 2 * N)
    {

        // Update steps
        steps++;
    }

    // Steps required to reach N
    if (steps * Math.floor((steps + 1) / 2) == N + 1)
    {

        // Update steps
        steps++;
    }

    document.write(steps);
}

// Driver Code

// Given value of N
let N = 18;

minimumsteps(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
6
```

***时间完成时间:** O(sqrt(N))*
***宇宙空间:** O(1)*
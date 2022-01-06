# 通过允许的两种不同操作从 0 到达 N 点的最小成本

> 原文:[https://www . geesforgeks . org/允许两种不同操作的 0 到 n 点最小到达成本/](https://www.geeksforgeeks.org/minimum-cost-to-reach-a-point-n-from-0-with-two-different-operations-allowed/)

给定整数 *N、P 和 Q* ，其中 *N* 表示目的地位置。任务是以最小的成本从位置 *0* 移动到位置 *N* 并打印计算出的成本。所有有效运动为:

1.  从位置 *X* 可以到位置 *X + 1* 花费 *P*
2.  或者，你可以花费 *Q* 去 *2 * X* 的位置

**例:**

> **输入:** N = 1，P = 3，Q = 4
> **输出:** 3
> 从位置 0 移动到位置 1，成本= 3。
> **输入:** N = 9，P = 5，Q = 1
> **输出:** 13
> 从位置 0 移动到位置 1，成本= 5，
> 然后第 1 到第 2，成本= 1，
> 然后第 2 到第 4，成本= 1，
> 然后第 4 到第 8，成本= 1，
> 最后第 8 到第 9，成本= 5。
> 总成本= 5 + 1 + 1 + 1 + 5 = 13。

**进场:**我们可以开始从目的地移动到初始位置，并记录跳跃的成本，而不是从头走到目的地。

*   如果 *N* 是奇数，那么唯一能让我们到这里的有效移动是 *N-1 到 N* ，代价是 *P* 。
*   如果 *N* 为偶数，那么我们计算从 *N 到 N/2* 位置的两个移动的成本，取其中的最小值。
*   当 *N* 等于 *0* 时，我们返回我们的总计算成本。

以下是上述方法的实现:

## C++

```
// CPP implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return minimum
// cost to reach destination
int minCost(int N, int P, int Q)
{
    // Initialize cost to 0
    int cost = 0;

    // going backwards until we
    // reach initial position
    while (N > 0) {

        if (N & 1) {
            cost += P;
            N--;
        }
        else {
            int temp = N / 2;

            // if 2*X jump is
            // better than X+1
            if (temp * P > Q)
                cost += Q;
            // if X+1 jump is better
            else
                cost += P * temp;

            N /= 2;
        }
    }

    // return cost
    return cost;
}

// Driver program
int main()
{
    int N = 9, P = 5, Q = 1;

    cout << minCost(N, P, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG{
// Function to return minimum
// cost to reach destination
static int minCost(int N, int P, int Q)
{
    // Initialize cost to 0
    int cost = 0;

    // going backwards until we
    // reach initial position
    while (N > 0) {

        if ((N & 1)>0) {
            cost += P;
            N--;
        }
        else {
            int temp = N / 2;

            // if 2*X jump is
            // better than X+1
            if (temp * P > Q)
                cost += Q;
            // if X+1 jump is better
            else
                cost += P * temp;

            N /= 2;
        }
    }

    // return cost
    return cost;
}

// Driver program
public static void main(String[] args)
{
    int N = 9, P = 5, Q = 1;

    System.out.println(minCost(N, P, Q));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python implementation of above approach

# Function to return minimum
# cost to reach destination

def minCost(N,P,Q):
    # Initialize cost to 0
    cost = 0

    # going backwards until we
    # reach initial position
    while (N > 0): 
        if (N & 1):
            cost += P
            N-=1
        else:
            temp = N // 2;

            # if 2*X jump is
            # better than X+1
            if (temp * P > Q):
                cost += Q
            # if X+1 jump is better
            else:
                cost += P * temp
            N //= 2
    return cost

# Driver program
N = 9
P = 5
Q = 1
print(minCost(N, P, Q))
#this code is improved by sahilshelangia
```

## C#

```
// C# implementation of above approach

class GFG
{
// Function to return minimum
// cost to reach destination
static int minCost(int N, int P, int Q)
{
    // Initialize cost to 0
    int cost = 0;

    // going backwards until we
    // reach initial position
    while (N > 0)
    {

        if ((N & 1) > 0)
        {
            cost += P;
            N--;
        }
        else
        {
            int temp = N / 2;

            // if 2*X jump is
            // better than X+1
            if (temp * P > Q)
                cost += Q;

            // if X+1 jump is better
            else
                cost += P * temp;

            N /= 2;
        }
    }

    // return cost
    return cost;
}

// Driver Code
static void Main()
{
    int N = 9, P = 5, Q = 1;

    System.Console.WriteLine(minCost(N, P, Q));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to return minimum
// cost to reach destination
function minCost($N, $P, $Q)
{
    // Initialize cost to 0
    $cost = 0;

    // going backwards until we
    // reach initial position
    while ($N > 0)
    {

        if ($N & 1)
        {
            $cost += $P;
            $N--;
        }
        else
        {
            $temp = $N / 2;

            // if 2*X jump is
            // better than X+1
            if ($temp * $P > $Q)
                $cost += $Q;

            // if X+1 jump is better
            else
                $cost += $P * $temp;

            $N /= 2;
        }
    }

    // return cost
    return $cost;
}

// Driver Code
$N = 9; $P = 5; $Q = 1;

echo minCost($N, $P, $Q);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
//Javascript implementation of above approach

// Function to return minimum
// cost to reach destination
function minCost( N, P, Q)
{
    // Initialize cost to 0
    var cost = 0;

    // going backwards until we
    // reach initial position
    while (N > 0) {

        if (N & 1) {
            cost += P;
            N--;
        }
        else {
            var temp =parseInt( N / 2);

            // if 2*X jump is
            // better than X+1
            if (temp * P > Q)
                cost += Q;
            // if X+1 jump is better
            else
                cost += P * temp;

            N = parseInt(N / 2);
        }
    }

    // return cost
    return cost;
}
var N = 9, P = 5, Q = 1;

document.write( minCost(N, P, Q));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
13
```

**时间复杂度:** O(N)

**辅助空间:** O(1)
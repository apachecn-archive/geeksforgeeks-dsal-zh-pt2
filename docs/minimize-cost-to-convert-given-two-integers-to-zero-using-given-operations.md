# 使用给定操作将给定的两个整数转换为零的成本最小化

> 原文:[https://www . geesforgeks . org/最小化使用给定运算将给定两个整数转换为零的成本/](https://www.geeksforgeeks.org/minimize-cost-to-convert-given-two-integers-to-zero-using-given-operations/)

给定两个整数 **X** 和 **Y** ，以及两个值 **cost1** 和 **cost2** ，任务是通过执行以下两种类型的操作，以最小的成本将给定的两个数字转换为零:

*   以**成本 1** 将其中任何一个**增加或减少 1。**
*   以**成本 2** 将两者**增加或减少 1。**

****示例:****

> ****输入:** X = 1，Y = 3，cost1 = 391，cost2 = 555
> **输出:** 1337
> **解释:**
> 使用第一个操作将 Y 减少为 1 两次，使用第二个操作将 X 和 Y 都从 1 转换为 0。
> 因此，总成本= 391 * 2 + 555 = 1337。**
> 
> ****输入:** X = 12，Y = 7，cost1 = 12，cost2 = 7
> **输出:** 4
> **解释:**
> 使用第一个操作将 X 减少到 7，然后使用第二个操作将 X 和 Y 都转换为 0。
> 因此，总成本= 12 * 5 + 7 * 7 = 109**

****方法:**
解决问题的最佳方法是:**

*   **使用第一次操作将 X 和 Y 的[最大值减小到最小值。这会增加**ABS(X–Y)*成本 1** 。](https://www.geeksforgeeks.org/compute-the-minimum-or-maximum-max-of-two-integers-without-branching/)**
*   **然后，使用第二个操作将 X 和 Y 都减少到 0。这将使成本增加**最小(X，Y) *成本 2** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation to find the minimum
// cost to make the two integers equal
// to zero using given operations
#include <bits/stdc++.h>
using namespace std;

// Function to find out the minimum cost to
// make two number X and Y equal to zero
int makeZero(int x, int y, int a, int b)
{

    // If x is greater than y then swap
    if(x > y)
       x = y,
       y = x;

    // Cost of making y equal to x
    int tot_cost = (y - x) * a;

    // Cost if we choose 1st operation
    int cost1 = 2 * x * a;

    // Cost if we choose 2nd operation
    int cost2 = x * b;

    // Total cost
    tot_cost += min(cost1, cost2);

    cout << tot_cost;
}

// Driver code
int main()
{
    int X = 1, Y = 3;
    int cost1 = 391, cost2 = 555;

    makeZero(X, Y, cost1, cost2);
}

// This code is contributed by coder001
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to find the minimum
// cost to make the two integers equal
// to zero using given operations
import java.util.*;
class GFG{

// Function to find out the minimum cost to
// make two number X and Y equal to zero
static void makeZero(int x, int y, int a, int b)
{

    // If x is greater than y then swap
    if(x > y)
    {
        int temp = x;
        x = y;
        y = temp;
    }

    // Cost of making y equal to x
    int tot_cost = (y - x) * a;

    // Cost if we choose 1st operation
    int cost1 = 2 * x * a;

    // Cost if we choose 2nd operation
    int cost2 = x * b;

    // Total cost
    tot_cost += Math.min(cost1, cost2);

    System.out.print(tot_cost);
}

// Driver code
public static void main(String args[])
{
    int X = 1, Y = 3;
    int cost1 = 391, cost2 = 555;

    makeZero(X, Y, cost1, cost2);
}
}

// This code is contributed by Code_Mech
```

## **蟒蛇 3**

```
# Python3 implementation to find the
# minimum cost to make the two integers
# equal to zero using given operations

# Function to find out the minimum cost to make
# two number X and Y equal to zero
def makeZero(x, y, a, b):

    # If x is greater than y then swap
    if(x > y):
        x, y = y, x

    # Cost of making y equal to x
    tot_cost = (y - x) * a

    # Cost if we choose 1st operation
    cost1 = 2 * x * a

    # Cost if we choose 2nd operation
    cost2 = x * b

    # Total cost
    tot_cost+= min(cost1, cost2)

    print(tot_cost)

if __name__ =="__main__":

    X, Y = 1, 3

    cost1, cost2 = 391, 555

    makeZero(X, Y, cost1, cost2)

```

## **C#**

```
// C# implementation to find the minimum
// cost to make the two integers equal
// to zero using given operations
using System;

class GFG{

// Function to find out the minimum cost to
// make two number X and Y equal to zero
static void makeZero(int x, int y, int a, int b)
{

    // If x is greater than y then swap
    if(x > y)
    {
        int temp = x;
        x = y;
        y = temp;
    }

    // Cost of making y equal to x
    int tot_cost = (y - x) * a;

    // Cost if we choose 1st operation
    int cost1 = 2 * x * a;

    // Cost if we choose 2nd operation
    int cost2 = x * b;

    // Total cost
    tot_cost += Math.Min(cost1, cost2);

    Console.Write(tot_cost);
}

// Driver code
public static void Main()
{
    int X = 1, Y = 3;
    int cost1 = 391, cost2 = 555;

    makeZero(X, Y, cost1, cost2);
}
}

// This code is contributed by Code_Mech
```

## **java 描述语言**

```
<script>

// Javascript implementation to find the minimum
// cost to make the two integers equal
// to zero using given operations

// Function to find out the minimum cost to
// make two number X and Y equal to zero
function makeZero(x, y, a, b)
{

    // If x is greater than y then swap
    if (x > y)
    {
        let temp = x;
        x = y;
        y = temp;
    }

    // Cost of making y equal to x
    let tot_cost = (y - x) * a;

    // Cost if we choose 1st operation
    let cost1 = 2 * x * a;

    // Cost if we choose 2nd operation
    let cost2 = x * b;

    // Total cost
    tot_cost += Math.min(cost1, cost2);

    document.write(tot_cost);
}

// Driver code
let X = 1, Y = 3;
let cost1 = 391, cost2 = 555;

makeZero(X, Y, cost1, cost2);

// This code is contributed by rameshtravel07  

</script>
```

****Output:** 

```
1337
```** 

****时间复杂度:***O(1)*
T5】辅助空间: *O(1)***
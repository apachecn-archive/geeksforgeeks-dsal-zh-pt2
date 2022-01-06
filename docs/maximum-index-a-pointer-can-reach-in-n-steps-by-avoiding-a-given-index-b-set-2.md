# 通过避开给定的索引 B | Set 2

，指针在 N 步内可以达到的最大索引

> 原文:[https://www . geesforgeks . org/maximum-index-a-pointer-can-in-steps-by-避让-a-给定-index-b-set-2/](https://www.geeksforgeeks.org/maximum-index-a-pointer-can-reach-in-n-steps-by-avoiding-a-given-index-b-set-2/)

给定两个整数 **N** 和 **B** ，任务是从 **0** <sup>第</sup>个索引开始，在 **N** 步中打印一个可以达到的数组中的最大索引，而不将其自身放在索引 **B** 的任何点上，其中在每一个 **i** <sup>第</sup>步中，指针可以向右移动 **i** 个索引。

**示例:**

> **输入:** N = 4，B = 6
> **输出:** 9
> **说明:**接下来的一系列动作最大化了可以达到的指标。
> 
> *   第一步:最初，pos = 0。保持同样的姿势。
> *   第二步:向右移动两个索引。因此，当前位置= 0 + 2 = 2。
> *   第三步:向右移动 3 个索引。因此，当前位置= 2 + 3 = 5。
> *   第四步:向右移动 4 个索引。因此，当前位置= 5 + 4 = 9。
> 
> **输入:** N = 2，B = 2
> T3】输出: 3

**天真的做法:**参考[之前的](https://www.geeksforgeeks.org/maximum-index-a-pointer-can-reach-in-n-steps-by-avoiding-a-given-index-b/)帖子，了解解决问题最简单的方法。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**解决问题的最佳思路基于以下观察:

> **观察:**
> 
> *   如果仔细观察，答案要么是步骤算术和的序列，要么是**步骤–1 的算术和的序列。**
> *   这是因为，在不考虑 **B** 的情况下，通过不等待(这将给出算术和)可以达到最高可能数。
> *   但是如果 **B** 是该序列的一部分，那么在第一步中在 **0** 处的等待确保该序列不与没有等待而获得的序列相交(因为它总是落后 1)。
> *   任何其他序列(即在任何其他点等待一次或多次)将总是产生较小的最大可达索引。

按照以下步骤解决问题:

*   初始化两个指针 **i = 0** 和 **j = 1。**
*   初始化一个变量，说**和，**存储第一个 **N 个**自然数 **，**即 **N * (N + 1) / 2 的[和。](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)**
*   初始化一个变量，说 **cnt = 0** 另一个变量，说 **flag = false。**
*   迭代直到 **cnt** 小于**n**
    *   用 **j** 递增 **i** 。
    *   增量 **j** 。
    *   增加 **cnt** 。
    *   如果在任何迭代中， **i** 等于 **B** ，则设置**标志=真**和[将](https://www.geeksforgeeks.org/break-statement-cc/)从循环中断开。
*   如果**标志**为**假**，则打印**和**。否则，打印**sum–1。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// index the pointer can reach
int maximumIndex(int N, int B)
{
    // Initialize two pointers
    int i = 0, j = 1;

    // Stores number of steps
    int cnt = 0;

    // Stores sum of first N
    // natural numbers
    int sum = N * (N + 1) / 2;

    bool flag = false;

    while (cnt < N) {

        // Increment i with j
        i += j;

        // Increment j with 1
        j++;

        // Increment count
        cnt++;

        // If i points to B
        if (i == B) {

            // Break
            flag = true;
            break;
        }
    }

    // Print the pointer index
    if (!flag) {
        cout << sum;
    }
    else
        cout << sum - 1;
}

// Driver Code
int main()
{
    // Given value of N & B
    int N = 4, B = 6;

    // Function call to find maximum
    // index the pointer can reach
    maximumIndex(N, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum
// index the pointer can reach
static void maximumIndex(int N, int B)
{

    // Initialize two pointers
    int i = 0, j = 1;

    // Stores number of steps
    int cnt = 0;

    // Stores sum of first N
    // natural numbers
    int sum = N * (N + 1) / 2;

    boolean flag = false;

    while (cnt < N)
    {

        // Increment i with j
        i += j;

        // Increment j with 1
        j++;

        // Increment count
        cnt++;

        // If i points to B
        if (i == B)
        {

            // Break
            flag = true;
            break;
        }
    }

    // Print the pointer index
    if (!flag == true)
    {
        System.out.print(sum);
    }
    else
    {
        System.out.print(sum - 1);
    }
}

// Driver Code
public static void main (String[] args)
{

    // Given value of N & B
    int N = 4, B = 6;

    // Function call to find maximum
    // index the pointer can reach
    maximumIndex(N, B);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum
# index the pointer can reach
def maximumIndex(N, B):

    # Initialize two pointers
    i, j = 0, 1

    # Stores number of steps
    cnt = 0

    # Stores sum of first N
    # natural numbers
    sum = N * (N + 1) // 2

    flag = False

    while (cnt < N):

        # Increment i with j
        i += j

        # Increment j with 1
        j += 1

        # Increment count
        cnt += 1

        # If i points to B
        if (i == B):

            # Break
            flag = True
            break

    # Print the pointer index
    if (not flag):
        print (sum)
    else:
        print(sum - 1)

# Driver Code
if __name__ == '__main__':

    # Given value of N & B
    N, B = 4, 6

    # Function call to find maximum
    # index the pointer can reach
    maximumIndex(N, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum
// index the pointer can reach
static void maximumIndex(int N, int B)
{

    // Initialize two pointers
    int i = 0, j = 1;

    // Stores number of steps
    int cnt = 0;

    // Stores sum of first N
    // natural numbers
    int sum = N * (N + 1) / 2;

    bool flag = false;

    while (cnt < N)
    {

        // Increment i with j
        i += j;

        // Increment j with 1
        j++;

        // Increment count
        cnt++;

        // If i points to B
        if (i == B)
        {

            // Break
            flag = true;
            break;
        }
    }

    // Print the pointer index
    if (!flag == true)
    {
        Console.Write(sum);
    }
    else
    {
       Console.Write(sum - 1);
    }
}

// Driver Code
static public void Main ()
{

    // Given value of N & B
    int N = 4, B = 6;

    // Function call to find maximum
    // index the pointer can reach
    maximumIndex(N, B);
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the maximum
// index the pointer can reach
function maximumIndex(N, B)
{
    // Initialize two pointers
    let i = 0, j = 1;

    // Stores number of steps
    let cnt = 0;

    // Stores sum of first N
    // natural numbers
    let sum = Math.floor(N * (N + 1) / 2);

    let flag = false;

    while (cnt < N) {

        // Increment i with j
        i += j;

        // Increment j with 1
        j++;

        // Increment count
        cnt++;

        // If i points to B
        if (i == B) {

            // Break
            flag = true;
            break;
        }
    }

    // Print the pointer index
    if (!flag) {
        document.write(sum);
    }
    else
        document.write(sum - 1);
}

// Driver Code

    // Given value of N & B
    let N = 4, B = 6;

    // Function call to find maximum
    // index the pointer can reach
    maximumIndex(N, B);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
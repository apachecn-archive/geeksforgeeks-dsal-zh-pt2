# 落蛋拼图| DP-11

> 原文:[https://www.geeksforgeeks.org/egg-dropping-puzzle-dp-11/](https://www.geeksforgeeks.org/egg-dropping-puzzle-dp-11/)

下面是这个著名的谜题的描述，涉及 n=2 个鸡蛋和一个 k=36 层的建筑。
假设我们希望知道 36 层建筑中哪些楼层可以安全掉蛋，哪些楼层会导致鸡蛋落地破碎。我们做几个假设:
…..一个从跌落中幸存下来的鸡蛋可以再次使用。
…..打碎的鸡蛋必须扔掉。
…..跌倒对所有鸡蛋的影响都是一样的。
…..如果鸡蛋掉下去会碎，那么从更高的地板上掉下去就会碎。
…..如果一个鸡蛋在秋天存活下来，那么它会在更短的秋天存活下来。
…..不排除一楼窗户打碎鸡蛋，也不排除 36 楼没有导致鸡蛋打碎。
如果只有一个鸡蛋，并且我们希望确保获得正确的结果，那么实验只能以一种方式进行。把鸡蛋从一楼窗户扔下去；如果它活下来了，就从二楼的窗户扔出去。继续向上直到断裂。在最坏的情况下，这种方法可能需要 36 滴。假设有两个鸡蛋。保证在所有情况下都能正常工作的最少鸡蛋量是多少？
问题实际上并不是要找到临界楼层，而只是要决定应该从哪些楼层掉鸡蛋，从而尽量减少试验的总次数。
*来源:* [*动态编程维基*](http://en.wikipedia.org/wiki/Dynamic_programming#Egg_dropping_puzzle)

**<u>方法 1</u> :** 递归。
在这篇文章中，我们将讨论一个具有“n”个鸡蛋和“k”个地板的一般问题的解决方案。解决方法是尝试从每一层楼(从 1 到 k)掉一个鸡蛋，并递归计算最坏情况下所需的最小掉蛋次数。在最坏情况下给出最小值的下限将是解决方案的一部分。
在下面的解决方案中，我们返回最坏情况下的最小试验次数；这些解决方案可以很容易地修改，以打印每个试验的楼层号。
最差情况的含义:最差情况给予用户阈值下限的保证。例如，如果我们有“1”个鸡蛋和“k”个楼层，我们将从第一层开始丢鸡蛋，直到鸡蛋在第“k”层破裂，因此尝试给我们保证的次数是“k”。
**1)最优子结构:**
当我们从 x 楼掉下一个鸡蛋时，可以有两种情况(1)鸡蛋破了(2)鸡蛋没破。

1.  如果鸡蛋从第' x '层掉下后破裂，那么我们只需要检查有剩余鸡蛋的低于' x '的楼层，因为应该有低于' x '的楼层存在，鸡蛋不会破裂；所以问题简化为 x-1 层和 n-1 个鸡蛋。
2.  如果鸡蛋从第' x '层掉下后没有破裂，那么我们只需要检查高于' x '层的楼层；所以这个问题简化为“k-x”层和 n 个鸡蛋。

由于我们需要在*最坏的*情况下尽量减少试验次数，所以我们取两种情况的最大值。我们考虑每一层以上两种情况的最大值，并选择产生最小试验次数的层。

> k == >楼层数
> n == >鸡蛋数
> 鸡蛋下降(n，k) == >最差情况下找到关键
> 楼层所需的最小试验次数。
> eggDrop(n，k)= 1+min { max(eggDrop(n–1，x–1)，egg drop(n，k–x))，其中 x 在{1，2，…，k}}
> **最坏情况的概念:**
> 例如:
> 假设有‘2’个鸡蛋和‘2’个楼层，那么-:
> 如果我们尝试从‘1’层投掷:
> 最坏情况下的尝试次数= 1+max(0，1)
> 
> 1= >如果鸡蛋没有从一楼打破，我们现在将有‘2’个鸡蛋和 1 层来测试，这将给出答案为
> ‘1’。(最坏情况的可能性)
> 我们考虑最坏情况的可能性，所以 1+max(0，1)=2
> 如果我们尝试从‘2’楼投掷:
> 最坏情况下的尝试次数= 1+max(1，0)
> 1= >如果鸡蛋从二楼打碎，那么我们将有 1 个鸡蛋和 1 层楼来寻找门槛楼层。(最差情况)
> 0= >如果鸡蛋没有从二楼破开，那么就是门槛楼层。(最佳情况)
> 我们以最坏情况可能性为保证，所以 1+max(1，0)=2。
> 最终答案是 min(1、2、3…..，kth 楼)
> 所以这里的答案是‘2’。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// A utility function to get
// maximum of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

// Function to get minimum
// number of trials needed in worst
// case with n eggs and k floors
int eggDrop(int n, int k)
{
    // If there are no floors,
    // then no trials needed.
    // OR if there is one floor,
    // one trial needed.
    if (k == 1 || k == 0)
        return k;

    // We need k trials for one
    // egg and k floors
    if (n == 1)
        return k;

    int min = INT_MAX, x, res;

    // Consider all droppings from
    // 1st floor to kth floor and
    // return the minimum of these
    // values plus 1.
    for (x = 1; x <= k; x++) {
        res = max(
            eggDrop(n - 1, x - 1),
            eggDrop(n, k - x));
        if (res < min)
            min = res;
    }

    return min + 1;
}

// Driver program to test
// to print printDups
int main()
{
    int n = 2, k = 10;
    cout << "Minimum number of trials "
            "in worst case with "
         << n << " eggs and " << k
         << " floors is "
         << eggDrop(n, k) << endl;
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
#include <limits.h>
#include <stdio.h>

// A utility function to get
// maximum of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

/* Function to get minimum number of
 trials needed in worst case with n eggs
 and k floors */
int eggDrop(int n, int k)
{
    // If there are no floors, then no
    // trials needed. OR if there is
    // one floor, one trial needed.
    if (k == 1 || k == 0)
        return k;

    // We need k trials for one egg and
    // k floors
    if (n == 1)
        return k;

    int min = INT_MAX, x, res;

    // Consider all droppings from 1st
    // floor to kth floor and
    // return the minimum of these values
    // plus 1.
    for (x = 1; x <= k; x++) {
        res = max(
            eggDrop(n - 1, x - 1),
            eggDrop(n, k - x));
        if (res < min)
            min = res;
    }

    return min + 1;
}

/* Driver program to test to pront printDups*/
int main()
{
    int n = 2, k = 10;
    printf("nMinimum number of trials in "
           "worst case with %d eggs and "
           "%d floors is %d \n",
           n, k, eggDrop(n, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class GFG {

    /* Function to get minimum number of
    trials needed in worst case with n
    eggs and k floors */
    static int eggDrop(int n, int k)
    {
        // If there are no floors, then
        // no trials needed. OR if there
        // is one floor, one trial needed.
        if (k == 1 || k == 0)
            return k;

        // We need k trials for one egg
        // and k floors
        if (n == 1)
            return k;

        int min = Integer.MAX_VALUE;
        int x, res;

        // Consider all droppings from
        // 1st floor to kth floor and
        // return the minimum of these
        // values plus 1.
        for (x = 1; x <= k; x++) {
            res = Math.max(eggDrop(n - 1, x - 1),
                           eggDrop(n, k - x));
            if (res < min)
                min = res;
        }

        return min + 1;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 2, k = 10;
        System.out.print("Minimum number of "
                         + "trials in worst case with "
                         + n + " eggs and " + k
                         + " floors is " + eggDrop(n, k));
    }
    // This code is contributed by Ryuga.
}
```

## 蟒蛇 3

```
import sys

# Function to get minimum number of trials
# needed in worst case with n eggs and k floors
def eggDrop(n, k):

    # If there are no floors, then no trials
    # needed. OR if there is one floor, one
    # trial needed.
    if (k == 1 or k == 0):
        return k

    # We need k trials for one egg
    # and k floors
    if (n == 1):
        return k

    min = sys.maxsize

    # Consider all droppings from 1st
    # floor to kth floor and return
    # the minimum of these values plus 1.
    for x in range(1, k + 1):

        res = max(eggDrop(n - 1, x - 1),
                  eggDrop(n, k - x))
        if (res < min):
            min = res

    return min + 1

# Driver Code
if __name__ == "__main__":

    n = 2
    k = 10
    print("Minimum number of trials in worst case with",
           n, "eggs and", k, "floors is", eggDrop(n, k))

# This code is contributed by ita_c
```

## C#

```
using System;

class GFG {

    /* Function to get minimum number of
    trials needed in worst case with n
    eggs and k floors */
    static int eggDrop(int n, int k)
    {
        // If there are no floors, then
        // no trials needed. OR if there
        // is one floor, one trial needed.
        if (k == 1 || k == 0)
            return k;

        // We need k trials for one egg
        // and k floors
        if (n == 1)
            return k;

        int min = int.MaxValue;
        int x, res;

        // Consider all droppings from
        // 1st floor to kth floor and
        // return the minimum of these
        // values plus 1.
        for (x = 1; x <= k; x++) {
            res = Math.Max(eggDrop(n - 1, x - 1),
                           eggDrop(n, k - x));
            if (res < min)
                min = res;
        }

        return min + 1;
    }

    // Driver code
    static void Main()
    {
        int n = 2, k = 10;
        Console.Write("Minimum number of "
                      + "trials in worst case with "
                      + n + " eggs and " + k
                      + " floors is " + eggDrop(n, k));
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>

    /* Function to get minimum number of 
    trials needed in worst case with n 
    eggs and k floors */
    function eggDrop(n,k)
    {

        // If there are no floors, then
        // no trials needed. OR if there
        // is one floor, one trial needed.
        if (k == 1 || k == 0)
            return k;

        // We need k trials for one egg
        // and k floors
        if (n == 1)
            return k;

        let min = Number.MAX_VALUE;
        let x, res;

        // Consider all droppings from
        // 1st floor to kth floor and
        // return the minimum of these
        // values plus 1.
        for (x = 1; x <= k; x++)
        {
            res = Math.max(eggDrop(n - 1, x - 1),
                           eggDrop(n, k - x));
            if (res < min)
                min = res;
        }
        return min + 1;
    }

    // Driver code
    let n = 2, k = 10;
    document.write("Minimum number of "
                         + "trials in worst case with "
                         + n + " eggs and " + k
                         + " floors is " + eggDrop(n, k));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
Minimum number of trials in worst case with 2 eggs and 10 floors is 4
```

**输出:**

```
Minimum number of trials in worst 
case with 2 eggs and 10 floors is 4
```

需要注意的是，上面的函数一次又一次地计算相同的子问题。参见下面的部分递归树，E(2，2)被求值两次。当你画出完整的递归树时，即使对于 n 和 k 的小值，也会有许多重复的子问题

```
                         E(2, 4)
                           |                      
          ------------------------------------- 
          |             |           |         |   
          |             |           |         |       
      x=1/          x=2/      x=3/     x=4/ 
        /             /         ....      ....
       /             /    
 E(1, 0)  E(2, 3)     E(1, 1)  E(2, 2)
          /  /...         /  
      x=1/                 .....
        /    
     E(1, 0)  E(2, 2)
            /   
            ......

Partial recursion tree for 2 eggs and 4 floors.
```

**复杂度分析:**

*   **时间复杂度:**由于存在子问题重叠的情况，时间复杂度是指数级的。
*   **辅助空间:** O(1)。因为没有使用任何数据结构来存储值。

由于相同的子问题被再次调用，这个问题具有重叠子问题的性质。所以蛋花拼图同时具有动态规划问题的两个属性(见[这个](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[这个](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/))。像其他典型的[动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)一样，相同子问题的重新计算可以通过以自下而上的方式构建临时数组 eggFloor[][]来避免。
**<u>方法二</u> :** 动态编程。
在这种方法中，我们采用与上述**相同的思路，忽略了反复计算子问题答案的情况。**。方法是制作一个存储子问题结果的表格，以便解决子问题，只需要从表格中查找，该表格需要**恒定时间**，而之前需要**指数时间**。
正式用于填充 DP[i][j]状态，其中‘I’是鸡蛋的数量，‘j’是楼层的数量:

*   我们必须遍历从“1”到“j”的每一层“x ”,找到以下最小值:

```
(1 + max( DP[i-1][j-1], DP[i][j-x] )).
```

这个模拟会把事情说清楚:

> i = >蛋的数量
> j = >楼层的数量
> 查找查找最大值
> 让我们为以下情况填充表格:
> 楼层= '4'
> 蛋= ' 2 '
> 1 2 3 4
> 1 2 3 4 =>1
> 1 2 2 3 =>2
> 对于'蛋-1 '每个情况都是基本情况，因此
> 的尝试次数等于楼层数量。
> 对于“鸡蛋-2”，1 楼
> 需要“1”次尝试，这是基本情况。
> 对于楼层-2 = >
> 取 1 楼 1 +最大值(0，DP[1][1])
> 取 2 楼 1 +最大值(DP[1][1]，0)
> DP[2][2] =最小值(1 +最大值(0，DP[1][1])，1 +最大值(DP[1][1]，0))
> 对于楼层-3 = >
> 取 1 楼 1 +最大值(0，DP[2][2])
> 取 DP[2][3])
> 取二楼 1 +最大值(DP[1][1]，DP[2][2])
> 取三楼 1 +最大值(DP[1][2]，DP[2][1])
> 取四楼 1 +最大值(0，DP[2][3])
> DP[2][4]=最小值('全部四层')= 3

## C++

```
// A Dynamic Programming based for
// the Egg Dropping Puzzle
#include <bits/stdc++.h>
using namespace std;

// A utility function to get
// maximum of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

/* Function to get minimum
number of trials needed in worst
case with n eggs and k floors */
int eggDrop(int n, int k)
{
    /* A 2D table where entry
    eggFloor[i][j] will represent
    minimum number of trials needed for
    i eggs and j floors. */
    int eggFloor[n + 1][k + 1];
    int res;
    int i, j, x;

    // We need one trial for one floor and 0
    // trials for 0 floors
    for (i = 1; i <= n; i++) {
        eggFloor[i][1] = 1;
        eggFloor[i][0] = 0;
    }

    // We always need j trials for one egg
    // and j floors.
    for (j = 1; j <= k; j++)
        eggFloor[1][j] = j;

    // Fill rest of the entries in table using
    // optimal substructure property
    for (i = 2; i <= n; i++) {
        for (j = 2; j <= k; j++) {
            eggFloor[i][j] = INT_MAX;
            for (x = 1; x <= j; x++) {
                res = 1 + max(
                            eggFloor[i - 1][x - 1],
                            eggFloor[i][j - x]);
                if (res < eggFloor[i][j])
                    eggFloor[i][j] = res;
            }
        }
    }

    // eggFloor[n][k] holds the result
    return eggFloor[n][k];
}

/* Driver program to test to print printDups*/
int main()
{
    int n = 2, k = 36;
    cout << "\nMinimum number of trials "
        "in worst case with " << n<< " eggs and "<< k<<
        " floors is "<< eggDrop(n, k);
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// A Dynamic Programming based for
// the Egg Dropping Puzzle
#include <limits.h>
#include <stdio.h>

// A utility function to get
// maximum of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

/* Function to get minimum
number of trials needed in worst
case with n eggs and k floors */
int eggDrop(int n, int k)
{
    /* A 2D table where entry
    eggFloor[i][j] will represent
    minimum number of trials needed for
    i eggs and j floors. */
    int eggFloor[n + 1][k + 1];
    int res;
    int i, j, x;

    // We need one trial for one floor and 0
    // trials for 0 floors
    for (i = 1; i <= n; i++) {
        eggFloor[i][1] = 1;
        eggFloor[i][0] = 0;
    }

    // We always need j trials for one egg
    // and j floors.
    for (j = 1; j <= k; j++)
        eggFloor[1][j] = j;

    // Fill rest of the entries in table using
    // optimal substructure property
    for (i = 2; i <= n; i++) {
        for (j = 2; j <= k; j++) {
            eggFloor[i][j] = INT_MAX;
            for (x = 1; x <= j; x++) {
                res = 1 + max(
                              eggFloor[i - 1][x - 1],
                              eggFloor[i][j - x]);
                if (res < eggFloor[i][j])
                    eggFloor[i][j] = res;
            }
        }
    }

    // eggFloor[n][k] holds the result
    return eggFloor[n][k];
}

/* Driver program to test to print printDups*/
int main()
{
    int n = 2, k = 36;
    printf("\nMinimum number of trials "
           "in worst case with %d eggs and "
           "%d floors is %d \n",
           n, k, eggDrop(n, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based Java
// Program for the Egg Dropping Puzzle
class EggDrop {

    // A utility function to get
    // maximum of two integers
    static int max(int a, int b)
    {
        return (a > b) ? a : b;
    }

    /* Function to get minimum number
 of trials needed in worst
    case with n eggs and k floors */
    static int eggDrop(int n, int k)
    {
        /* A 2D table where entry eggFloor[i][j]
 will represent minimum number of trials
needed for i eggs and j floors. */
        int eggFloor[][] = new int[n + 1][k + 1];
        int res;
        int i, j, x;

        // We need one trial for one floor and
        // 0 trials for 0 floors
        for (i = 1; i <= n; i++) {
            eggFloor[i][1] = 1;
            eggFloor[i][0] = 0;
        }

        // We always need j trials for one egg
        // and j floors.
        for (j = 1; j <= k; j++)
            eggFloor[1][j] = j;

        // Fill rest of the entries in table using
        // optimal substructure property
        for (i = 2; i <= n; i++) {
            for (j = 2; j <= k; j++) {
                eggFloor[i][j] = Integer.MAX_VALUE;
                for (x = 1; x <= j; x++) {
                    res = 1 + max(
                                  eggFloor[i - 1][x - 1],
                                  eggFloor[i][j - x]);
                    if (res < eggFloor[i][j])
                        eggFloor[i][j] = res;
                }
            }
        }

        // eggFloor[n][k] holds the result
        return eggFloor[n][k];
    }

    /* Driver program to test to print printDups*/
    public static void main(String args[])
    {
        int n = 2, k = 10;
        System.out.println("Minimum number of trials in worst"
                           + " case with "
                           + n + "  eggs and "
                           + k + " floors is " + eggDrop(n, k));
    }
}
/*This code is contributed by Rajat Mishra*/
```

## 计算机编程语言

```
# A Dynamic Programming based Python Program for the Egg Dropping Puzzle
INT_MAX = 32767

# Function to get minimum number of trials needed in worst
# case with n eggs and k floors
def eggDrop(n, k):
    # A 2D table where entry eggFloor[i][j] will represent minimum
    # number of trials needed for i eggs and j floors.
    eggFloor = [[0 for x in range(k + 1)] for x in range(n + 1)]

    # We need one trial for one floor and0 trials for 0 floors
    for i in range(1, n + 1):
        eggFloor[i][1] = 1
        eggFloor[i][0] = 0

    # We always need j trials for one egg and j floors.
    for j in range(1, k + 1):
        eggFloor[1][j] = j

    # Fill rest of the entries in table using optimal substructure
    # property
    for i in range(2, n + 1):
        for j in range(2, k + 1):
            eggFloor[i][j] = INT_MAX
            for x in range(1, j + 1):
                res = 1 + max(eggFloor[i-1][x-1], eggFloor[i][j-x])
                if res < eggFloor[i][j]:
                    eggFloor[i][j] = res

    # eggFloor[n][k] holds the result
    return eggFloor[n][k]

# Driver program to test to print printDups
n = 2
k = 36
print("Minimum number of trials in worst case with" + str(n) + "eggs and "
       + str(k) + " floors is " + str(eggDrop(n, k)))

# This code is contributed by Bhavya Jain
```

## C#

```
// A Dynamic Programming based C# Program
// for the Egg Dropping Puzzle
using System;

class GFG {

    // A utility function to get maximum of
    // two integers
    static int max(int a, int b)
    {
        return (a > b) ? a : b;
    }

    /* Function to get minimum number of
    trials needed in worst case with n
    eggs and k floors */
    static int eggDrop(int n, int k)
    {

        /* A 2D table where entry eggFloor[i][j]
        will represent minimum number of trials
        needed for i eggs and j floors. */
        int[, ] eggFloor = new int[n + 1, k + 1];
        int res;
        int i, j, x;

        // We need one trial for one floor and0
        // trials for 0 floors
        for (i = 1; i <= n; i++) {
            eggFloor[i, 1] = 1;
            eggFloor[i, 0] = 0;
        }

        // We always need j trials for one egg
        // and j floors.
        for (j = 1; j <= k; j++)
            eggFloor[1, j] = j;

        // Fill rest of the entries in table
        // using optimal substructure property
        for (i = 2; i <= n; i++) {
            for (j = 2; j <= k; j++) {
                eggFloor[i, j] = int.MaxValue;
                for (x = 1; x <= j; x++) {
                    res = 1 + max(eggFloor[i - 1, x - 1],
                                  eggFloor[i, j - x]);
                    if (res < eggFloor[i, j])
                        eggFloor[i, j] = res;
                }
            }
        }

        // eggFloor[n][k] holds the result
        return eggFloor[n, k];
    }

    // Driver function
    public static void Main()
    {
        int n = 2, k = 36;
        Console.WriteLine("Minimum number of trials "
                          + "in worst case with " + n + " eggs and "
                          + k + "floors is " + eggDrop(n, k));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based PHP
// Program for the Egg Dropping Puzzle

/* Function to get minimum number
   of trials needed in worst
   case with n eggs and k floors */
function eggDrop($n, $k)
{

    /* A 2D table where entry eggFloor[i][j]
       will represent minimum number of
       trials needed for i eggs and j floors. */
    $eggFloor = array(array());;

    // We need one trial for one
    // floor and0 trials for 0 floors
    for ($i = 1; $i <=$n;$i++)
    {
        $eggFloor[$i][1] = 1;
        $eggFloor[$i][0] = 0;
    }

    // We always need j trials
    // for one egg and j floors.
    for ($j = 1; $j <= $k; $j++)
        $eggFloor[1][$j] = $j;

    // Fill rest of the entries in
    // table using optimal substructure
    // property
    for ($i = 2; $i <= $n; $i++)
    {
        for ($j = 2; $j <= $k; $j++)
        {
            $eggFloor[$i][$j] = 999999;
            for ($x = 1; $x <= $j; $x++)
            {
                $res = 1 + max($eggFloor[$i - 1][$x - 1],
                                 $eggFloor[$i][$j - $x]);
                if ($res < $eggFloor[$i][$j])
                    $eggFloor[$i][$j] = $res;
            }
        }
    }

    // eggFloor[n][k] holds the result
    return $eggFloor[$n][$k];
}

    // Driver Code
    $n = 2;
    $k = 36;
    echo "Minimum number of trials in worst case with " .$n. " eggs and "
                                    .$k. " floors is " .eggDrop($n, $k) ;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// A Dynamic Programming based Javascript
// Program for the Egg Dropping Puzzle

// A utility function to get
    // maximum of two integers
function max(a,b)
{
    return (a > b) ? a : b;
}

/* Function to get minimum number
 of trials needed in worst
    case with n eggs and k floors */
function eggDrop(n,k)
{
    /* A 2D table where entry eggFloor[i][j]
 will represent minimum number of trials
needed for i eggs and j floors. */
        let eggFloor = new Array(n + 1);
        for(let i=0;i<(n+1);i++)
        {
            eggFloor[i]=new Array(k+1);
        }
        let res;
        let i, j, x;

        // We need one trial for one floor and
        // 0 trials for 0 floors
        for (i = 1; i <= n; i++) {
            eggFloor[i][1] = 1;
            eggFloor[i][0] = 0;
        }

        // We always need j trials for one egg
        // and j floors.
        for (j = 1; j <= k; j++)
            eggFloor[1][j] = j;

        // Fill rest of the entries in table using
        // optimal substructure property
        for (i = 2; i <= n; i++) {
            for (j = 2; j <= k; j++) {
                eggFloor[i][j] = Number.MAX_VALUE;
                for (x = 1; x <= j; x++) {
                    res = 1 + max(
                                  eggFloor[i - 1][x - 1],
                                  eggFloor[i][j - x]);
                    if (res < eggFloor[i][j])
                        eggFloor[i][j] = res;
                }
            }
        }

        // eggFloor[n][k] holds the result
        return eggFloor[n][k];
}

/* Driver program to test to print printDups*/
let n = 2, k = 36;
document.write("Minimum number of trials in worst"
                           + " case with "
                           + n + "  eggs and "
                           + k + " floors is " + eggDrop(n, k));

// This code is contributed by ab2127

</script>
```

**Output**

```
Minimum number of trials in worst case with 2 eggs and 36 floors is 8 
```

**复杂度分析:**

*   **时间复杂度:** O(n*k^2).
    其中‘n’是蛋的数量,‘k’是楼层的数量，因为我们对每个蛋使用嵌套的循环'k^2'时间
*   **辅助空间:** O(n*k)。
    作为二维数组的大小‘n * k’被用来存储元素。

**方法 3:** 使用记忆的动态规划。

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000

vector<vector<int>> memo(MAX, vector<int> (MAX, -1));
int solveEggDrop(int n, int k) {

    if(memo[n][k] != -1) { return memo[n][k];}

    if (k == 1 || k == 0)
      return k;

    if (n == 1)
      return k;

    int min = INT_MAX, x, res;

    for (x = 1; x <= k; x++) {
      res = max(
        solveEggDrop(n - 1, x - 1),
        solveEggDrop(n, k - x));
      if (res < min)
        min = res;
    }

    memo[n][k] = min+1;
    return min + 1;
  }

int main() {

    int n = 2, k = 36;
    cout<<solveEggDrop(n, k);
    return 0;
}

// contributed by Shivam Agrawal(shivamagrawal3)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

class GFG {
    static final int MAX = 1000;

    static int[][] memo = new int[MAX][MAX];

    static int solveEggDrop(int n, int k)
    {

        if (memo[n][k] != -1) {
            return memo[n][k];
        }

        if (k == 1 || k == 0)
            return k;

        if (n == 1)
            return k;

        int min = Integer.MAX_VALUE, x, res;

        for (x = 1; x <= k; x++) {
            res = Math.max(solveEggDrop(n - 1, x - 1),
                           solveEggDrop(n, k - x));
            if (res < min)
                min = res;
        }

        memo[n][k] = min + 1;
        return min + 1;
    }

    public static void main(String[] args)
    {
        for (int i = 0; i < memo.length; i++)
            Arrays.fill(memo[i], -1);
        int n = 2, k = 36;
        System.out.print(solveEggDrop(n, k));
    }
}

// This code IS contributed by umadevi9616
```

## 蟒蛇 3

```
import sys

MAX = 1000;

memo = [[-1 for i in range(MAX)] for j in range(MAX)] ;

def solveEggDrop(n, k):

    if (memo[n][k] != -1):
        return memo[n][k];

    if (k == 1 or k == 0):
        return k;

    if (n == 1):
        return k;

    min = sys.maxsize;
    res = 0;

    for x in range(1,k+1):
        res = max(solveEggDrop(n - 1, x - 1), solveEggDrop(n, k - x));
        if (res < min):
            min = res;

    memo[n][k] = min + 1;
    return min + 1;

# Driver code
if __name__ == '__main__':
    n = 2;
    k = 36;
    print(solveEggDrop(n, k));

# This code is contributed by gauravrajput1
```

## C#

```
using System;

public class GFG {
    static readonly int MAX = 1000;

    static int[,] memo = new int[MAX,MAX];

    static int solveEggDrop(int n, int k)
    {

        if (memo[n,k] != -1) {
            return memo[n,k];
        }

        if (k == 1 || k == 0)
            return k;

        if (n == 1)
            return k;

        int min = int.MaxValue, x, res;

        for (x = 1; x <= k; x++) {
            res = Math.Max(solveEggDrop(n - 1, x - 1),
                           solveEggDrop(n, k - x));
            if (res < min)
                min = res;
        }

        memo[n,k] = min + 1;
        return min + 1;
    }

    public static void Main(String[] args)
    {
        for (int i = 0; i < memo.GetLength(0); i++)
            for(int j =0;j<memo.GetLength(1);j++)
                memo[i,j] = -1;
        int n = 2, k = 36;
        Console.Write(solveEggDrop(n, k));
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
var MAX = 1000;

     var memo = Array(MAX).fill().map(()=>Array(MAX).fill(-1));

    function solveEggDrop(n , k)
    {

        if (memo[n][k] != -1) {
            return memo[n][k];
        }

        if (k == 1 || k == 0)
            return k;

        if (n == 1)
            return k;

        var min = Number.MAX_VALUE, x, res;

        for (x = 1; x <= k; x++) {
            res = Math.max(solveEggDrop(n - 1, x - 1),
                           solveEggDrop(n, k - x));
            if (res < min)
                min = res;
        }

        memo[n][k] = min + 1;
        return min + 1;
    }

        var n = 2, k = 36;
        document.write(solveEggDrop(n, k));

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
8
```

作为练习，您可以尝试修改上述 DP 解决方案，以打印所有中间楼层(用于最低试用解决方案的楼层)。
**更高效的解决方案** : [落蛋拼图(二项式系数和二分搜索法解)](https://www.geeksforgeeks.org/eggs-dropping-puzzle-binomial-coefficient-and-binary-search-solution/)
[2 蛋 K 层落蛋拼图](https://www.geeksforgeeks.org/egg-dropping-puzzle-with-2-eggs-and-k-floors/)
[2 蛋 100 层拼图](http://geeksquiz.com/puzzle-set-35-2-eggs-and-100-floors/)

&t=3s
**参考文献:**
[http://archive . ite . journal . informs . org/vol 4 no 1/Sniedovich/index . PHP](http://archive.ite.journal.informs.org/Vol4No1/Sniedovich/index.php)
如发现任何不正确的地方，请写评论，或者想分享更多关于以上讨论主题的信息。
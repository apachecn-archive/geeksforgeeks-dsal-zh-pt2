# 通过将球排成一排来确定比赛的获胜者

> 原文:[https://www . geesforgeks . org/通过连续排列球来确定比赛获胜者/](https://www.geeksforgeeks.org/determine-winner-of-the-game-by-arranging-balls-in-a-row/)

分别给定大小球 **N** 和 **M** 的数量，任务是找出如果玩家 **X** 和 **Y** 都通过以下两个动作进行最佳打法，哪个玩家获胜:

*   玩家 X 会尽量保持**同类型的球**，即小球后面跟着另一个小球或者大球后面跟着一个大球。
*   玩家 Y 将放入**不同类型的球**，即小球后跟大球，反之亦然。

不能移动的玩家输掉游戏。任务是找出哪个玩家在给定的球数下赢得了比赛。给定的是，玩家 X 总是先开始。

**示例:**

> **输入:** N = 3 M = 1
> **输出:** X
> **说明:**
> 由于只有 1 个大球，玩家 X 会放在第一位。
> 玩家 Y 把一个小球放在大球旁边，因为他可以把不同类型的球放在旁边。
> 然后玩家 X 放一个小球(同类型)。现在玩家 Y 不能持球，因此不能移动
> 序列= {大，小，小}，因此得分为 X = 2，Y = 1。
> 因此，玩家 X 获胜。
> 
> **输入:** N = 4 M = 4
> **输出:** Y
> **说明:**
> 玩家 X 第一招=小，玩家 Y 第一招=大(N = 4，M = 3 )
> 玩家 X 第二招=大，玩家 Y 第二招=小(N = 3，M = 2 )
> 玩家 X 第三招=小，玩家 Y 第三招=大(N = 2， M = 1 )
> 玩家 X 第四招=大，玩家 Y 第四招=小(N = 1，M = 0)。
> 因此，玩家 Y 赢了，因为玩家 X 不能移动。

**方法:**按照下面给出的步骤解决问题:

*   检查小球的**数量是否大于或等于大球的** **数量**，那么玩家 **X** 将有分数**N–1**由于玩家 **X** 会先放小球，那么玩家 **Y** 会立即放不同类型的球，现在玩家 **X** 会放与玩家 **Y** 相同类型的球。这个过程将持续到游戏结束。
*   否则，如果**大球大于小球**，那么玩家 X 将有**M–1**的得分，玩家 **Y** 的得分为 **N** ，进场方式同上。这里玩家 **X** 会先从守大球开始。
*   最后，比较双方玩家的分数，打印出胜者作为输出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the winner of the
// Game by arranging the balls in a row
void findWinner(int n, int m)
{
    int X = 0;
    int Y = 0;

    // Check if small balls are greater
    // or equal to the large ones
    if (n >= m) {

        // X can place balls
        // therefore scores n-1
        X = n - 1;
        Y = m;
    }

    // Condition if large balls
    // are greater than small
    else {

        // X can have m-1 as a score
        // since greater number of
        // balls can only be adjacent
        X = m - 1;
        Y = n;
    }

    // Compare the score
    if (X > Y)
        cout << "X";

    else if (Y > X)
        cout << "Y";

    else
        cout << "-1";
}

// Driver Code
int main()
{
    // Given number of small balls(N)
    // and number of large balls(M)
    int n = 3, m = 1;

    // Function call
    findWinner(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the winner of the
// Game by arranging the balls in a row
static void findWinner(int n, int m)
{
    int X = 0;
    int Y = 0;

    // Check if small balls are greater
    // or equal to the large ones
    if (n >= m)
    {

        // X can place balls
        // therefore scores n-1
        X = n - 1;
        Y = m;
    }

    // Condition if large balls
    // are greater than small
    else
    {

        // X can have m-1 as a score
        // since greater number of
        // balls can only be adjacent
        X = m - 1;
        Y = n;
    }

    // Compare the score
    if (X > Y)
        System.out.print("X");

    else if (Y > X)
        System.out.print("Y");

    else
        System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{
    // Given number of small balls(N)
    // and number of large balls(M)
    int n = 3, m = 1;

    // Function call
    findWinner(n, m);
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the winner of the
# Game by arranging the balls in a row
def findWinner(n, m):
    X = 0;
    Y = 0;

    # Check if small balls are greater
    # or equal to the large ones
    if (n >= m):

        # X can place balls
        # therefore scores n-1
        X = n - 1;
        Y = m;

    # Condition if large balls
    # are greater than small
    else:

        # X can have m-1 as a score
        # since greater number of
        # balls can only be adjacent
        X = m - 1;
        Y = n;

    # Compare the score
    if (X > Y):
        print("X");

    elif(Y > X):
        print("Y");

    else:
        print("-1");

# Driver Code
if __name__ == '__main__':

    # Given number of small balls(N)
    # and number of large balls(M)
    n = 3;
    m = 1;

    # Function call
    findWinner(n, m);

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the winner of the
// Game by arranging the balls in a row
static void findWinner(int n, int m)
{
    int X = 0;
    int Y = 0;

    // Check if small balls are greater
    // or equal to the large ones
    if (n >= m)
    {

        // X can place balls
        // therefore scores n-1
        X = n - 1;
        Y = m;
    }

    // Condition if large balls
    // are greater than small
    else
    {

        // X can have m-1 as a score
        // since greater number of
        // balls can only be adjacent
        X = m - 1;
        Y = n;
    }

    // Compare the score
    if (X > Y)
        Console.Write("X");

    else if (Y > X)
        Console.Write("Y");

    else
        Console.Write("-1");
}

// Driver Code
public static void Main(String[] args)
{
    // Given number of small balls(N)
    // and number of large balls(M)
    int n = 3, m = 1;

    // Function call
    findWinner(n, m);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the winner of the
// Game by arranging the balls in a row
function findWinner(n, m)
{
    let X = 0;
    let Y = 0;

    // Check if small balls are greater
    // or equal to the large ones
    if (n >= m)
    {

        // X can place balls
        // therefore scores n-1
        X = n - 1;
        Y = m;
    }

    // Condition if large balls
    // are greater than small
    else
    {

        // X can have m-1 as a score
        // since greater number of
        // balls can only be adjacent
        X = m - 1;
        Y = n;
    }

    // Compare the score
    if (X > Y)
        document.write("X");

    else if (Y > X)
        document.write("Y");

    else
        document.write("-1");
}

// Driver code

// Given number of small balls(N)
// and number of large balls(M)
let n = 3, m = 1;

// Function call
findWinner(n, m);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
X
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)
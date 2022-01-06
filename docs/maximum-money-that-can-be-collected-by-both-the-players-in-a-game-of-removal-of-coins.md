# 在一个移除硬币的游戏中两个玩家可以收集的最大金额

> 原文:[https://www . geeksforgeeks . org/游戏币移除游戏中两个玩家可以收集的最大金额/](https://www.geeksforgeeks.org/maximum-money-that-can-be-collected-by-both-the-players-in-a-game-of-removal-of-coins/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，使得**arr【I】**代表硬币的价值，任务是找出当两个玩家 **A** 和 **B** 按照以下规则进行最佳游戏时，每个玩家可以获得的最大金额:

*   玩家 **A** 总是开始游戏。
*   在每一回合中，玩家必须从给定的阵列中取出恰好 1 枚硬币。
*   在每一回合中，玩家 **B** ，必须从给定的阵中取出**正好 2 个硬币**。

**示例:**

> **输入:** arr[] = {1，1，1，1}
> **输出:** (A : 2)，(B : 2)
> **说明:**
> 以下是两位玩家的弃币顺序:
> 
> *   玩家 A 移除 arr[0](= 1)。
> *   玩家 B 移除 arr[1](= 1)和 arr[2](= 1)。
> *   玩家 A 移除 arr[3](= 1)。
> 
> 因此，玩家 A 获得的硬币总数为 2，玩家 B 获得的硬币总数为 2。
> 
> **输入:** arr[] = {1，1，1}
> **输出:** (A : 1)，(B : 2)

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:

*   初始化两个变量，将 **amountA** 和 **amountB** 表示为 **0** ，存储玩家 **A** 和 **B** 获得的金钱总额。
*   [给定数组按降序排序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   如果 **N** 的值为 **1** ，则将 **amountA** 的值更新为**arr【0】**。
*   如果 **N** 的值大于或等于 **2** ，则将 **amountA** 的值更新为**arr【0】**，将 **amountB** 的值更新为**arr【1】**。
*   [使用变量 **i** 在范围**【2，N】**上遍历数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，如果 [i 的值为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将值 **arr[i]** 加到 **amountB** 上。否则，将值 **arr[i]** 加到 **amountA** 上。
*   完成以上步骤后，将 **amountA** 和 **amountB** 的值分别打印为双方选手 **A** 和 **B** 的成绩分数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum score
// obtained by the players A and B
void findAmountPlayers(int arr[], int N)
{
    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());

    // Stores the maximum amount of
    // money obtained by A
    int amountA = 0;

    // Stores the maximum amount of
    // money obtained by B
    int amountB = 0;

    // If the value of N is 1
    if (N == 1) {

        // Update the amountA
        amountA += arr[0];

        // Print the amount of money
        // obtained by both players
        cout << "(A : " << amountA << "), "
             << "(B : " << amountB << ")";
        return;
    }

    // Update the amountA
    amountA = arr[0];

    // Update the amountB
    amountB = arr[1];

    // Traverse the array arr[]
    for (int i = 2; i < N; i++) {

        // If i is an odd number
        if (i % 2 == 0) {

            // Update the amountB
            amountB += arr[i];
        }
        else {

            // Update the amountA
            amountA += arr[i];
        }
    }

    // Print the amount of money
    // obtained by both the players
    cout << "(A : " << amountA << ")\n"
         << "(B : " << amountB << ")";
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findAmountPlayers(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum score
// obtained by the players A and B
static void findAmountPlayers(int[] arr, int N)
{

    // Sort the array in descending order
    Arrays.sort(arr);
    reverse(arr, N);

    // Stores the maximum amount of
    // money obtained by A
    int amountA = 0;

    // Stores the maximum amount of
    // money obtained by B
    int amountB = 0;

    // If the value of N is 1
    if (N == 1)
    {

        // Update the amountA
        amountA += arr[0];

        // Print the amount of money
        // obtained by both players
        System.out.println("(A : " + amountA + "), " +
                           "(B : " + amountB + ")");
        return;
    }

    // Update the amountA
    amountA = arr[0];

    // Update the amountB
    amountB = arr[1];

    // Traverse the array arr[]
    for(int i = 2; i < N; i++)
    {

        // If i is an odd number
        if (i % 2 == 0)
        {

            // Update the amountB
            amountB += arr[i];
        }
        else
        {

            // Update the amountA
            amountA += arr[i];
        }
    }

    // Print the amount of money
    // obtained by both the players
    System.out.println("(A : " + amountA + ")");
    System.out.println("(B : " + amountB + ")");
}

static void reverse(int a[], int n)
{
    int[] b = new int[n];
    int j = n;

    for(int i = 0; i < n; i++)
    {
        b[j - 1] = a[i];
        j = j - 1;
    }
}

// Driver code
public static void main(String []args)
{
    int[] arr = { 1, 1, 1 };
    int N = arr.length;

    findAmountPlayers(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum score
# obtained by the players A and B
def findAmountPlayers(arr, N):
    # Sort the array in descending order
    arr = sorted(arr)[::-1]

    # Stores the maximum amount of
    # money obtained by A
    amountA = 0

    # Stores the maximum amount of
    # money obtained by B
    amountB = 0

    # If the value of N is 1
    if (N == 1):

        # Update the amountA
        amountA += arr[0]

        # Print the amount of money
        # obtained by both players
        print("(A :",mountA,"), (B :",str(amountB)+")")
        return

    # Update the amountA
    amountA = arr[0]

    # Update the amountB
    amountB = arr[1]

    # Traverse the array arr[]
    for i in range(2, N):

        # If i is an odd number
        if (i % 2 == 0):

            # Update the amountB
            amountB += arr[i]

        else:

            # Update the amountA
            amountA += arr[i]

    # Print amount of money
    # obtained by both the players
    print("(A :",str(amountA)+")\n(B :",str(amountB)+")")

# Driver Code
if __name__ == '__main__':
    arr = [1, 1, 1]
    N = len(arr)
    findAmountPlayers(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the maximum score
    // obtained by the players A and B
    static void findAmountPlayers(int[] arr, int N)
    {

        // Sort the array in descending order
        Array.Sort(arr);
        Array.Reverse(arr);

        // Stores the maximum amount of
        // money obtained by A
        int amountA = 0;

        // Stores the maximum amount of
        // money obtained by B
        int amountB = 0;

        // If the value of N is 1
        if (N == 1) {

            // Update the amountA
            amountA += arr[0];

            // Print the amount of money
            // obtained by both players
            Console.WriteLine("(A : " + amountA + "), "
                              + "(B : " + amountB + ")");
            return;
        }

        // Update the amountA
        amountA = arr[0];

        // Update the amountB
        amountB = arr[1];

        // Traverse the array arr[]
        for (int i = 2; i < N; i++) {

            // If i is an odd number
            if (i % 2 == 0) {

                // Update the amountB
                amountB += arr[i];
            }
            else {

                // Update the amountA
                amountA += arr[i];
            }
        }

        // Print the amount of money
        // obtained by both the players
        Console.WriteLine("(A : " + amountA + ")");
        Console.WriteLine("(B : " + amountB + ")");
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 1, 1 };
        int N = arr.Length;
        findAmountPlayers(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum score
// obtained by the players A and B
function findAmountPlayers(arr, N) {
    // Sort the array in descending order
    arr.sort((a, b) => b - a)

    // Stores the maximum amount of
    // money obtained by A
    let amountA = 0;

    // Stores the maximum amount of
    // money obtained by B
    let amountB = 0;

    // If the value of N is 1
    if (N == 1) {

        // Update the amountA
        amountA += arr[0];

        // Print the amount of money
        // obtained by both players
        document.write("(A : " + amountA + "), "
            + "(B : " + amountB + ")");
        return;
    }

    // Update the amountA
    amountA = arr[0];

    // Update the amountB
    amountB = arr[1];

    // Traverse the array arr[]
    for (let i = 2; i < N; i++) {

        // If i is an odd number
        if (i % 2 == 0) {

            // Update the amountB
            amountB += arr[i];
        }
        else {

            // Update the amountA
            amountA += arr[i];
        }
    }

    // Print the amount of money
    // obtained by both the players
    document.write("(A : " + amountA + ")<br>"
        + "(B : " + amountB + ")");
}

// Driver Code

let arr = [1, 1, 1];
let N = arr.length
findAmountPlayers(arr, N);

// This code is contributed _saurabh_jaiswal
</script>
```

**Output:** 

```
(A : 1)
(B : 2)
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
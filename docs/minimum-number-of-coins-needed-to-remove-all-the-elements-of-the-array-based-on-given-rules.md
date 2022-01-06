# 根据给定规则移除数组中所有元素所需的最小硬币数量

> 原文:[https://www . geeksforgeeks . org/基于给定规则移除数组中所有元素所需的最小硬币数/](https://www.geeksforgeeks.org/minimum-number-of-coins-needed-to-remove-all-the-elements-of-the-array-based-on-given-rules/)

给定长度为 **N** 的数组 **arr** ，值 1 和 2 表示类型 1 和类型 2 元素以及两个玩家，玩家 1 和玩家 2。任务是找到按照数组中给定的顺序移除所有元素所需的最小硬币数。必须遵守以下规则:

*   玩家 1 和玩家 2 轮流移除元素，玩家 1 先开始
*   两者最多只能移除 2 个相邻元素，并且必须在轮到它们时移除至少一个元素
*   2 型元素可以不用硬币就被他们两个移除
*   玩家 2 可以不带硬币移除类型 1 元素，但是玩家 1 需要硬币来移除元素

**示例:**

> **输入:** N = 8 arr = [1，2，1，1，2，1，1]
> **输出:** 2
> **说明:**player 1 需要的硬币总数为 2。以下是每个玩家回合中移除的元素:
> 
> *   玩家 1 将使用一枚硬币移除类型 1 的第一个元素，不使用硬币移除类型 2 的第二个元素
> *   玩家 2 将移除接下来的两个元素
> *   玩家 1 将开始其操作，并且只移除类型 2 的下一个元素而不移除硬币
> *   玩家 2 将开始其操作，并移除数组中索引 5 和 6 处的下两个元素
> *   玩家 1 将使用一枚硬币移除类型 1 的最后一个元素
> 
> **输入:** N = 4 arr = [1，1，2，2]
> **输出:** 2
> **说明:**玩家 1 需要的硬币总数为 1。下面是每个玩家回合中移除的元素
> 
> *   玩家 1 将使用一枚硬币移除类型 1 的第一个元素
> *   玩家 2 将移除第二个和第三个元素
> *   玩家 1 将不带硬币移除类型 2 的第 4 个元素

**方法:**给定的问题可以使用两个指针用贪婪方法解决。可以遵循以下步骤来解决问题:

*   第一个要素单独考虑。如果是类型 1，那么 1 将被添加到需要移除元素的硬币总数中
*   考虑到轮到 Player1，从第二个索引开始迭代数组
*   如果轮到玩家 1，并且第一个元素是类型 2，下一个元素是类型 1，那么玩家 1 将只移除类型 2 的元素，然后玩家 2 可以开始操作
*   如果轮到玩家 1 和类型 2 的两个连续元素，那么在该操作中玩家 1 将移除这两个元素
*   如果轮到玩家 1，并且有 3 个连续的类型 1 元素，那么玩家 1 将只使用一枚硬币移除第一个元素，而玩家 2 可以移除接下来的两个元素
*   考虑到以上三种情况，可以观察到类型 1 元素的每个块都是从 Player2 的操作开始的
*   因此，对于类型 1 的每三个连续元素，可以看出玩家 1 需要一枚硬币来移除一个元素，玩家 2 将移除两个元素

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum
// number of coins needed
int minimumcoins(int arr[], int N)
{

    int coins = 0;
    int j = 0;

    // Consider the first element
    // separately, add 1 to the total
    // if it's of type 1
    if (arr[0] == 1)
        coins++;

    // Iterate from the second element
    for (int i = 1; i < N; i++) {
        // If the current element is
        // of type 2 then any Player
        // can remove the element
        if (arr[i] == 2)
            continue;

        // Second pointer to reach end of
        // type 1 elements
        j = i;

        // Increment j until arr[j]
        // is equal to 1 and j is not
        // out of bounds
        while (j < N && arr[j] == 1) {
            j++;
        }

        // Number of type 1 elements
        // in a continuous chunk
        int x = (j - i);
        coins += x / 3;

        // From next iteration i
        // pointer will start from
        // index of j
        i = j - 1;
    }

    // Return the minimum count of coins
    return coins;
}

int main()

{

    int N = 8;

    int arr[] = { 1, 2, 1, 1, 2, 1, 1, 1 };

    cout << minimumcoins(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.io.*;
import java.util.*;
class GFG {

    // Function to calculate minimum
    // number of coins needed
    static int minimumcoins(int arr[], int N)
    {

        int coins = 0;
        int j = 0;

        // Consider the first element
        // separately, add 1 to the total
        // if it's of type 1
        if (arr[0] == 1)
            coins++;

        // Iterate from the second element
        for (int i = 1; i < N; i++) {
            // If the current element is
            // of type 2 then any Player
            // can remove the element
            if (arr[i] == 2)
                continue;

            // Second pointer to reach end of
            // type 1 elements
            j = i;

            // Increment j until arr[j]
            // is equal to 1 and j is not
            // out of bounds
            while (j < N && arr[j] == 1) {
                j++;
            }

            // Number of type 1 elements
            // in a continuous chunk
            int x = (j - i);
            coins += x / 3;

            // From next iteration i
            // pointer will start from
            // index of j
            i = j - 1;
        }

        // Return the minimum count of coins
        return coins;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 8;

        int arr[] = { 1, 2, 1, 1, 2, 1, 1, 1 };
        // Function Call
        System.out.println(minimumcoins(arr, N));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate minimum
# number of coins needed
def minimumcoins(arr, N) :

    coins = 0
    j = 0

    # Consider the first element
    # separately, add 1 to the total
    # if it's of type 1
    if (arr[0] == 1) :
        coins += 1

    # Iterate from the second element
    for i in range(1, N) :
        # If the current element is
        # of type 2 then any Player
        # can remove the element
        if (arr[i] == 2) :
            continue

        # Second pointer to reach end of
        # type 1 elements
        j = i

        # Increment j until arr[j]
        # is equal to 1 and j is not
        # out of bounds
        while (j < N and arr[j] == 1) :
            j += 1

        # Number of type 1 elements
        # in a continuous chunk
        x = (j - i)
        coins += x // 3

        # From next iteration i
        # pointer will start from
        # index of j
        i = j - 1

    # Return the minimum count of coins
    return coins

# Driver Code
N = 8
arr = [ 1, 2, 1, 1, 2, 1, 1, 1 ]

print(minimumcoins(arr, N))

# This code is contributed by sanjoy_62.
```

## C#

```
// C# implementation for the above approach
using System;

public class GFG {

    // Function to calculate minimum
    // number of coins needed
    static int minimumcoins(int []arr, int N)
    {

        int coins = 0;
        int j = 0;

        // Consider the first element
        // separately, add 1 to the total
        // if it's of type 1
        if (arr[0] == 1)
            coins++;

        // Iterate from the second element
        for (int i = 1; i < N; i++) {
            // If the current element is
            // of type 2 then any Player
            // can remove the element
            if (arr[i] == 2)
                continue;

            // Second pointer to reach end of
            // type 1 elements
            j = i;

            // Increment j until arr[j]
            // is equal to 1 and j is not
            // out of bounds
            while (j < N && arr[j] == 1) {
                j++;
            }

            // Number of type 1 elements
            // in a continuous chunk
            int x = (j - i);
            coins += x / 3;

            // From next iteration i
            // pointer will start from
            // index of j
            i = j - 1;
        }

        // Return the minimum count of coins
        return coins;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 8;

        int []arr = { 1, 2, 1, 1, 2, 1, 1, 1 };

        // Function Call
        Console.WriteLine(minimumcoins(arr, N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// JavaScript implementation for the above approach

// Function to calculate minimum
// number of coins needed
function minimumcoins(arr, N)
{
    let coins = 0;
    let j = 0;

    // Consider the first element
    // separately, add 1 to the total
    // if it's of type 1
    if (arr[0] == 1)
        coins++;

    // Iterate from the second element
    for(let i = 1; i < N; i++)
    {

        // If the current element is
        // of type 2 then any Player
        // can remove the element
        if (arr[i] == 2)
            continue;

        // Second pointer to reach end of
        // type 1 elements
        j = i;

        // Increment j until arr[j]
        // is equal to 1 and j is not
        // out of bounds
        while (j < N && arr[j] == 1)
        {
            j++;
        }

        // Number of type 1 elements
        // in a continuous chunk
        let x = (j - i);
        coins += Math.floor(x / 3);

        // From next iteration i
        // pointer will start from
        // index of j
        i = j - 1;
    }

    // Return the minimum count of coins
    return coins;
}

// Driver code
let N = 8;
let arr = [ 1, 2, 1, 1, 2, 1, 1, 1 ];

document.write(minimumcoins(arr, N));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)
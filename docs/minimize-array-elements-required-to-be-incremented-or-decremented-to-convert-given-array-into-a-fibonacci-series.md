# 最小化需要递增或递减的数组元素，以将给定的数组转换为斐波那契数列

> 原文:[https://www . geesforgeks . org/minimum-array-elements-需要递增或递减才能将给定数组转换为斐波那契数列/](https://www.geeksforgeeks.org/minimize-array-elements-required-to-be-incremented-or-decremented-to-convert-given-array-into-a-fibonacci-series/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到将该数组转换为[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)所需的最小增量或减量 1。如果不可能，则打印 **-1** 。
***注意:**每个数组元素只能递增或递减一次。*

**示例:**

> **输入:** arr[] = {4，8，9，17，21}
> **输出:** 3
> **解释:**
> 数组可以三步转换成斐波那契数列:
> 将 4 转换成 3，arr[] = {3，8，9，17，21}
> 将 8 转换成 7，arr[] = {3，7，9，17，21}
> 将 9 转换成 10，arr[]= =
> 
> **输入:** arr[] = {3，8，7，2}
> **输出:** -1
> **解释:**
> 给定数组不能转换成斐波那契数列。

**方法:**解决问题的思路是利用斐波那契数列的前两个元素足以计算出[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)以及后续元素的公差。因此，检查前两个数字的所有操作排列，并计算最小移动量，以将其余元素转换为斐波那契数列。
按照以下步骤实施上述方法:

*   如果数组中的元素个数小于 3，那么就已经是[斐波那契数列](https://www.geeksforgeeks.org/python-program-for-n-th-fibonacci-number/)了。
*   否则，尝试前两个元素的所有排列:
    *   对于每个排列，计算数组其余元素的运算次数:
        *   如果最多一次操作不能改变元素，那么数组就不能转换成斐波那契数列。
        *   否则，更新所需的操作数。
    *   用操作数更新答案。
*   返回答案。

以下是我们方法的实施情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum
// number of moves to make the
// sequence a Fibonacci series
int minMoves(vector<int> arr)
{
    int N = arr.size();

    // If number of elements
    // is less than 3
    if (N <= 2)
        return 0;

    // Initialize the value
    // of the result
    int ans = INT_MAX;

    // Try all permutations of
    // the first two elements
    for (int i = -1; i <= 1; i++) {
        for (int j = -1; j <= 1; j++) {

            // Value of first element
            // after operation
            int num1 = arr[0] + i;

            // Value of second element
            // after operation
            int num2 = arr[1] + j;

            int flag = 1;
            int moves = abs(i) + abs(j);

            // Calculate number of moves
            // for rest of the elements
            // of the array
            for (int idx = 2; idx < N; idx++) {

                // Element at idx index
                int num = num1 + num2;

                // If it is not possible
                // to change the element
                // in atmost one move
                if (abs(arr[idx] - num) > 1)
                    flag = 0;

                // Otherwise
                else
                    moves += abs(arr[idx] - num);

                num1 = num2;
                num2 = num;
            }

            // Update the answer
            if (flag)
                ans = min(ans, moves);
        }
    }

    // Return the answer
    if (ans == INT_MAX)
        return -1;
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 8, 9, 17, 27 };
    cout << minMoves(arr) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate minimum
// number of moves to make the
// sequence a Fibonacci series
static int minMoves(int []arr)
{
    int N = arr.length;

    // If number of elements
    // is less than 3
    if (N <= 2)
        return 0;

    // Initialize the value
    // of the result
    int ans = Integer.MAX_VALUE;

    // Try all permutations of
    // the first two elements
    for (int i = -1; i <= 1; i++)
    {
        for (int j = -1; j <= 1; j++)
        {

            // Value of first element
            // after operation
            int num1 = arr[0] + i;

            // Value of second element
            // after operation
            int num2 = arr[1] + j;
            int flag = 1;
            int moves = Math.abs(i) + Math.abs(j);

            // Calculate number of moves
            // for rest of the elements
            // of the array
            for (int idx = 2; idx < N; idx++)
            {

                // Element at idx index
                int num = num1 + num2;

                // If it is not possible
                // to change the element
                // in atmost one move
                if (Math.abs(arr[idx] - num) > 1)
                    flag = 0;

                // Otherwise
                else
                    moves += Math.abs(arr[idx] - num);
                num1 = num2;
                num2 = num;
            }

            // Update the answer
            if (flag > 0)
                ans = Math.min(ans, moves);
        }
    }

    // Return the answer
    if (ans == Integer.MAX_VALUE)
        return -1;
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 4, 8, 9, 17, 27 };
    System.out.print(minMoves(arr));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to calculate minimum
# number of moves to make the
# sequence a Fibonacci series
def minMoves(arr):
    N = len(arr)

    # If number of elements
    # is less than 3
    if (N <= 2):
        return 0

    # Initialize the value
    # of the result
    ans = sys.maxsize

    # Try all permutations of
    # the first two elements
    for i in range(-1, 2):
        for j in range(-1, 2):

            # Value of first element
            # after operation
            num1 = arr[0] + i

            # Value of second element
            # after operation
            num2 = arr[1] + j
            flag = 1
            moves = abs(i) + abs(j)

            # Calculate number of moves
            # for rest of the elements
            # of the array
            for idx in range(2, N):

                # Element at idx index
                num = num1 + num2

                # If it is not possible
                # to change the element
                # in atmost one move
                if (abs(arr[idx] - num) > 1):
                    flag = 0

                # Otherwise
                else:
                    moves += abs(arr[idx] - num)
                num1 = num2
                num2 = num

            # Update the answer
            if (flag):
                ans = min(ans, moves)

    # Return the answer
    if (ans == sys.maxsize):
        return -1
    return ans

# Driver Code
if __name__ == "__main__":
    arr = [4, 8, 9, 17, 27]
    print(minMoves(arr))

    # This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

// Function to calculate minimum
// number of moves to make the
// sequence a Fibonacci series
class GFG{

static int minMoves(List<int> arr)
{
    int N = arr.Count;

    // If number of elements
    // is less than 3
    if (N <= 2)
        return 0;

    // Initialize the value
    // of the result
    int ans = Int32.MaxValue;

    // Try all permutations of
    // the first two elements
    for(int i = -1; i <= 1; i++)
    {
        for(int j = -1; j <= 1; j++)
        {

            // Value of first element
            // after operation
            int num1 = arr[0] + i;

            // Value of second element
            // after operation
            int num2 = arr[1] + j;

            int flag = 1;
            int moves = Math.Abs(i) + Math.Abs(j);

            // Calculate number of moves
            // for rest of the elements
            // of the array
            for(int idx = 2; idx < N; idx++)
            {

                // Element at idx index
                int num = num1 + num2;

                // If it is not possible
                // to change the element
                // in atmost one move
                if (Math.Abs(arr[idx] - num) > 1)
                    flag = 0;

                // Otherwise
                else
                    moves += Math.Abs(arr[idx] - num);

                num1 = num2;
                num2 = num;
            }

            // Update the answer
            if (flag != 0)
                ans = Math.Min(ans, moves);
        }
    }

    // Return the answer
    if (ans == Int32.MaxValue)
        return -1;

    return ans;
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){ 4, 8, 9, 17, 27 };

    Console.WriteLine(minMoves(arr));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to calculate minimum
// number of moves to make the
// sequence a Fibonacci series
function minMoves(arr)
{
    let N = arr.length;

    // If number of elements
    // is less than 3
    if (N <= 2)
        return 0;

    // Initialize the value
    // of the result
    let ans = Number.MAX_VALUE;

    // Try all permutations of
    // the first two elements
    for (let i = -1; i <= 1; i++)
    {
        for (let j = -1; j <= 1; j++)
        {

            // Value of first element
            // after operation
            let num1 = arr[0] + i;

            // Value of second element
            // after operation
            let num2 = arr[1] + j;
            let flag = 1;
            let moves = Math.abs(i) + Math.abs(j);

            // Calculate number of moves
            // for rest of the elements
            // of the array
            for (let idx = 2; idx < N; idx++)
            {

                // Element at idx index
                let num = num1 + num2;

                // If it is not possible
                // to change the element
                // in atmost one move
                if (Math.abs(arr[idx] - num) > 1)
                    flag = 0;

                // Otherwise
                else
                    moves += Math.abs(arr[idx] - num);
                num1 = num2;
                num2 = num;
            }

            // Update the answer
            if (flag > 0)
                ans = Math.min(ans, moves);
        }
    }

    // Return the answer
    if (ans == Number.MAX_VALUE)
        return -1;
    return ans;
}

    // Driver Code

    let arr = [ 4, 8, 9, 17, 27 ];
    document.write(minMoves(arr));

 // This code is contributed by chinmoy1997pal.
</script>
```

**Output:** 

```
3
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)
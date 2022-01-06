# 使所有数组元素在 AP 中所需的最小增量或减量 1

> 原文:[https://www . geeksforgeeks . org/最小增量或减 1-需要在 ap 中生成所有数组元素/](https://www.geeksforgeeks.org/minimum-increments-or-decrements-by-1-required-to-make-all-array-elements-in-ap/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出对数组元素执行增量/减量 1 所需的最小次数，以使给定数组的所有元素 **arr[]** 都在 [AP](https://www.geeksforgeeks.org/progressions-ap-gp-hp/) 中。如果无法在 AP 中制作阵列，则打印**-1”**。

**示例:**

> **输入:** arr[] = {19，16，9，5，0}
> **输出:** 3
> **解释:**
> 数组元素的递增/递减顺序如下:
> 
> 1.  将数组元素 arr[0](= 19)增加 1。
> 2.  将数组元素 arr[1](= 16)减 1。
> 3.  将数组元素 arr[2](= 9)增加 1。
> 
> 经过上述操作后，数组 arr[]修改为{20，15，10，5，0}，与第一项 20 和公共差-5 在 AP 中。因此，元素的总数是 3。
> 
> **输入:** arr[] = {1，2，3，4，10}
> **输出:** -1

**方法:**可以通过从前两个元素中找到第一项和[公共差](https://www.geeksforgeeks.org/arithmetic-progression-common-difference-and-nth-term-class-10-maths/)来解决给定的问题，然后通过简单地[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)来检查是否所有元素都可以被改变为具有给定的第一项和公共差的 AP 序列。按照以下步骤解决问题:

*   如果 **N** 小于等于 **2** ，则**T5】打印 **0** ，因为每个这样的序列都是一个[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)。**
*   初始化一个变量，说 **res** 为 **N + 1** 来存储答案。
*   [使用变量 **a** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【-1，1】**中迭代，并执行以下步骤:
    *   [使用变量 **b** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【-1，1】**中迭代，并执行以下步骤:
        *   初始化一个变量，比如说**将**更改为 **0** ，以存储[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]中已更改元素的计数。**
        *   如果 **a** 不等于 **0** ，那么将**的值增加 **1** 来改变**。
        *   如果 **b** 不等于 **0** ，那么将**的值增加 **1** 来改变**。
        *   初始化一个变量，比如说 **orig** 为 **arr[0] + a** 存储第一个元素， **diff** 为**(arr[1]+b)–(arr[0]+a)**存储[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的[公差](https://www.geeksforgeeks.org/arithmetic-progression-common-difference-and-nth-term-class-10-maths/)。
        *   初始化一个变量，说**好**为**真**以存储带有第一项 **orig** 和公共差 **diff** 的[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)序列是否可能。
        *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，N-1】**中迭代，并执行以下步骤:
            *   将变量**实际值**初始化为 **orig+i*diff** 以存储索引 **i** 处的[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的实际元素。
            *   如果 **abs(实际–arr[I])**大于 **1** ，那么这样的算术级数是不可达的。然后将**好**的值设置为假[断开](https://www.geeksforgeeks.org/break-statement-cc/)回路。
            *   否则，如果**实际**不等于**arr【I】，**将**的值增加 **1** 来改变**。
        *   遍历循环的内部[后，将 **res** 的值更新为 **min(变化，res)。**](https://www.geeksforgeeks.org/range-based-loop-c/)
*   完成上述步骤后，如果 res 大于 **N** ，则将-1 分配给 **res** 。否则，打印 **res** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of elements to be changed to convert
// the array into an AP
int findMinimumMoves(int N, int arr[])
{
    // If N is less than 3
    if (N <= 2) {
        return 0;
    }

    // Stores the answer
    int res = N + 1;

    // Iterate in the range [-1, 1]
    for (int a = -1; a <= 1; a++) {

        // Iterate in the range [-1, 1]
        for (int b = -1; b <= 1; b++) {

            // Stores the total changes
            int changes = 0;

            if (a != 0) {
                changes++;
            }

            if (b != 0) {
                changes++;
            }

            // Stores the first element
            // of the AP
            int orig = (arr[0] + a);

            // Stores the common difference
            // of the AP
            int diff = (arr[1] + b) - (arr[0] + a);

            // Stores whether it is
            // possible to convert the
            // array into AP
            bool good = true;

            // Iterate in the range [2, N-1]
            for (int i = 2; i < N; i++) {

                // Stores the ith element
                // of the AP
                int actual = orig + i * diff;

                // If abs(actual-arr[i])
                // is greater than 1
                if (abs(actual - arr[i]) > 1) {

                    // Mark as false
                    good = false;
                    break;
                }
                // If actual is not
                // equal to arr[i]
                if (actual != arr[i])
                    changes++;
            }
            if (!good)
                continue;

            // Update the value of res
            res = min(res, changes);
        }
    }

    // If res is greater than N
    if (res > N)
        res = -1;

    // Return the value of res
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 19, 16, 9, 5, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findMinimumMoves(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum number
// of elements to be changed to convert
// the array into an AP
static int findMinimumMoves(int N, int arr[])
{

    // If N is less than 3
    if (N <= 2)
    {
        return 0;
    }

    // Stores the answer
    int res = N + 1;

    // Iterate in the range [-1, 1]
    for(int a = -1; a <= 1; a++)
    {

        // Iterate in the range [-1, 1]
        for(int b = -1; b <= 1; b++)
        {

            // Stores the total changes
            int changes = 0;

            if (a != 0)
            {
                changes++;
            }

            if (b != 0)
            {
                changes++;
            }

            // Stores the first element
            // of the AP
            int orig = (arr[0] + a);

            // Stores the common difference
            // of the AP
            int diff = (arr[1] + b) - (arr[0] + a);

            // Stores whether it is
            // possible to convert the
            // array into AP
            boolean good = true;

            // Iterate in the range [2, N-1]
            for(int i = 2; i < N; i++)
            {

                // Stores the ith element
                // of the AP
                int actual = orig + i * diff;

                // If abs(actual-arr[i])
                // is greater than 1
                if (Math.abs(actual - arr[i]) > 1)
                {

                    // Mark as false
                    good = false;
                    break;
                }

                // If actual is not
                // equal to arr[i]
                if (actual != arr[i])
                    changes++;
            }
            if (!good)
                continue;

            // Update the value of res
            res = Math.min(res, changes);
        }
    }

    // If res is greater than N
    if (res > N)
        res = -1;

    // Return the value of res
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 19, 16, 9, 5, 0 };
    int N = arr.length;

    System.out.println(findMinimumMoves(N, arr));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of elements to be changed to convert
# the array into an AP
def findMinimumMoves(N, arr):

    # If N is less than 3
    if (N <= 2):
        return 0

    # Stores the answer
    res = N + 1

    # Iterate in the range [-1, 1]
    for a in range(-1, 2, 1):

        # Iterate in the range [-1, 1]
        for b in range(-1, 2, 1):

            # Stores the total changes
            changes = 0

            if (a != 0):
                changes += 1

            if (b != 0):
                changes += 1

            # Stores the first element
            # of the AP
            orig = (arr[0] + a)

            # Stores the common difference
            # of the AP
            diff = (arr[1] + b) - (arr[0] + a)

            # Stores whether it is
            # possible to convert the
            # array into AP
            good = True

            # Iterate in the range [2, N-1]
            for i in range(2, N, 1):

                # Stores the ith element
                # of the AP
                actual = orig + i * diff

                # If abs(actual-arr[i])
                # is greater than 1
                if (abs(actual - arr[i]) > 1):

                    # Mark as false
                    good = False
                    break

                # If actual is not
                # equal to arr[i]
                if (actual != arr[i]):
                    changes += 1

            if (good == False):
                continue

            # Update the value of res
            res = min(res, changes)

    # If res is greater than N
    if (res > N):
        res = -1

    # Return the value of res
    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 19, 16, 9, 5, 0 ]
    N = len(arr)

    print(findMinimumMoves(N, arr))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of elements to be changed to convert
// the array into an AP
static int findMinimumMoves(int N, int[] arr)
{

    // If N is less than 3
    if (N <= 2)
    {
        return 0;
    }

    // Stores the answer
    int res = N + 1;

    // Iterate in the range [-1, 1]
    for(int a = -1; a <= 1; a++)
    {

        // Iterate in the range [-1, 1]
        for(int b = -1; b <= 1; b++)
        {

            // Stores the total changes
            int changes = 0;

            if (a != 0)
            {
                changes++;
            }

            if (b != 0)
            {
                changes++;
            }

            // Stores the first element
            // of the AP
            int orig = (arr[0] + a);

            // Stores the common difference
            // of the AP
            int diff = (arr[1] + b) - (arr[0] + a);

            // Stores whether it is
            // possible to convert the
            // array into AP
            bool good = true;

            // Iterate in the range [2, N-1]
            for(int i = 2; i < N; i++)
            {

                // Stores the ith element
                // of the AP
                int actual = orig + i * diff;

                // If abs(actual-arr[i])
                // is greater than 1
                if (Math.Abs(actual - arr[i]) > 1)
                {

                    // Mark as false
                    good = false;
                    break;
                }

                // If actual is not
                // equal to arr[i]
                if (actual != arr[i])
                    changes++;
            }
            if (!good)
                continue;

            // Update the value of res
            res = Math.Min(res, changes);
        }
    }

    // If res is greater than N
    if (res > N)
        res = -1;

    // Return the value of res
    return res;
}

// Driver code
static public void Main()
{
    int[] arr = { 19, 16, 9, 5, 0 };
    int N = arr.Length;

    Console.WriteLine(findMinimumMoves(N, arr));
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of elements to be changed to convert
// the array into an AP
function findMinimumMoves(N, arr)
{

    // If N is less than 3
    if (N <= 2)
    {
        return 0;
    }

    // Stores the answer
    let res = N + 1;

    // Iterate in the range [-1, 1]
    for(let a = -1; a <= 1; a++)
    {

        // Iterate in the range [-1, 1]
        for(let b = -1; b <= 1; b++)
        {

            // Stores the total changes
            let changes = 0;

            if (a != 0)
            {
                changes++;
            }

            if (b != 0)
            {
                changes++;
            }

            // Stores the first element
            // of the AP
            let orig = (arr[0] + a);

            // Stores the common difference
            // of the AP
            let diff = (arr[1] + b) - (arr[0] + a);

            // Stores whether it is
            // possible to convert the
            // array into AP
            let good = true;

            // Iterate in the range [2, N-1]
            for(let i = 2; i < N; i++)
            {

                // Stores the ith element
                // of the AP
                let actual = orig + i * diff;

                // If abs(actual-arr[i])
                // is greater than 1
                if (Math.abs(actual - arr[i]) > 1)
                {

                    // Mark as false
                    good = false;
                    break;
                }

                // If actual is not
                // equal to arr[i]
                if (actual != arr[i])
                    changes++;
            }
            if (!good)
                continue;

            // Update the value of res
            res = Math.min(res, changes);
        }
    }

    // If res is greater than N
    if (res > N)
        res = -1;

    // Return the value of res
    return res;
}

// Driver Code
let arr = [ 19, 16, 9, 5, 0 ];
let N = arr.length;

document.write(findMinimumMoves(N, arr));

// This code is contributed by target_2

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
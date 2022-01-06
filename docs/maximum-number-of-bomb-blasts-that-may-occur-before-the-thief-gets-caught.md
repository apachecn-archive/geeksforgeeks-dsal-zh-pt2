# 小偷被抓前可能发生的最大炸弹爆炸次数

> 原文:[https://www . geesforgeks . org/小偷被抓前可能发生的最大炸弹爆炸次数/](https://www.geeksforgeeks.org/maximum-number-of-bomb-blasts-that-may-occur-before-the-thief-gets-caught/)

给定一个由 **M** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、**arr【】**，其中 **i <sup>第</sup>** 个元素表示 **i <sup>第</sup>个**炸弹投放后爆炸的时间，三个整数 **N、X、**和 **Y** 表示 **X 坐标**上相邻连续单元的数量，以及初始单元任务是找出在小偷被抓住之前可能发生的最大炸弹爆炸次数，如果小偷可以在每一秒钟投放一枚炸弹，或者移动到警察没有去过的现有牢房的左边或右边。

**示例:**

> **输入:** arr[] = {1，4}，N = 7，X = 3，Y = 6
> **输出:** 2
> **解释:**
> 一种可能的方式是:
> 
> 1.  t = 0 时:盗贼掉落激活时间等于 4 的炸弹。与此同时，警察将一间牢房移向小偷。此后，小偷和警察的位置分别为 3 和 5。
> 2.  t = 1:警察向小偷移动一个牢房，小偷向其左侧移动一个牢房。此后，小偷和警察的位置分别为 2 和 4。
> 3.  t = 2:警察向小偷移动一个牢房，小偷向其左侧移动一个牢房。此后，小偷和警察的位置分别为 1 和 3。
> 4.  t = 3 时:警察向小偷移动一个牢房，小偷扔下激活时间等于 1 的炸弹。此后，小偷和警察的位置分别是 1 和 2。
> 5.  t = 4 时:炸弹在时间点(t= 3，t = 0)爆炸。现在小偷不能移动到任何牢房，也没有炸弹了。警察将一间牢房移向小偷，最终在 1 号牢房将其抓获。
> 
> 因此，小偷被抓之前发生的最大炸弹爆炸是 2。
> 
> **输入:** arr[] = {5，1}，N = 7，X = 3，Y = 6
> T3】输出: 1

**方法:**给定的问题可以基于以下观察来解决:

1.  如果警察和小偷都以最佳状态移动，那么每一秒钟，警察都会向小偷移动。因此，小偷在被抓住之前的最长时间是他们位置之间的距离。
2.  可以观察到，最好的选择是先投放激活时间多的炸弹，而不是激活时间少的炸弹。如果先投时间少的炸弹，再投激活时间多的炸弹，可能会超过小偷被抓之前的时间。

按照以下步骤解决问题:

*   [按降序排列数组 arr[]](https://www.geeksforgeeks.org/sort-c-stl/) 。
*   初始化两个变量，用值 **0** 表示**计数**和**时间**，以存储可能发生的炸弹爆炸的最大计数和经过的时间。
*   找出 **X** 和 **Y** 的绝对差值，并存储在一个变量中，比如 **maxSec** 。
*   [使用变量 **i** 在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M-1】**范围内迭代，并执行以下步骤:
    *   如果**电流元素**和**时间**之和小于或等于**最大秒**，那么将**计数**和**时间**增加 **1** 。
*   完成上述步骤后，将**计数**更新为**计数=分钟(计数，绝对值(X-Y)-1)。**
*   最后，完成以上步骤后，打印**的数值，计**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of bomb that can be blasted before
// the thief gets caught
int findMaxBomb(int N, int M, int X, int Y, int arr[])
{
    // Sort the array arr[] in
    // descending order
    sort(arr, arr + M, greater<int>());

    // Stores the maxtime the thief
    // has before getting caught
    int maxSec;

    // If Y is less than X
    if (Y < X) {
        maxSec = N - Y;
    }
    // Otherwise
    else {
        maxSec = Y - 1;
    }

    // Stores the current
    // second
    int time = 1;

    // Stores the count of
    // bomb blasts
    int count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < M; i++) {

        // If arr[i]+time is less
        // than or equal to the
        // maxSec
        if (arr[i] + time <= maxSec) {
            // Increment time and
            // count by 1
            time++;
            count++;
        }
    }

    // Update count
    count = min(count, abs(X - Y) - 1);

    // Return the value of count
    return count;
}

// Driver Code
int main()
{
    // Given Input
    int N = 7, X = 3, Y = 6;
    int arr[] = { 1, 4 };
    int M = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findMaxBomb(N, M, X, Y, arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
import java.util.Collections;

public class GFG {

    // Function to find the maximum number
    // of bomb that can be blasted before
    // the thief gets caught
    static int findMaxBomb(int N, int M, int X, int Y,
                           Integer arr[])
    {
        // Sort the array arr[] in
        // descending order
        Arrays.sort(arr, Collections.reverseOrder());

        // Stores the maxtime the thief
        // has before getting caught
        int maxSec;

        // If Y is less than X
        if (Y < X) {
            maxSec = N - Y;
        }
        // Otherwise
        else {
            maxSec = Y - 1;
        }

        // Stores the current
        // second
        int time = 1;

        // Stores the count of
        // bomb blasts
        int count = 0;

        // Traverse the array arr[]
        for (int i = 0; i < M; i++) {

            // If arr[i]+time is less
            // than or equal to the
            // maxSec
            if (arr[i] + time <= maxSec) {
                // Increment time and
                // count by 1
                time++;
                count++;
            }
        }

        // Update count
        count = Math.min(count, Math.abs(X - Y) - 1);

        // Return the value of count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        int N = 7, X = 3, Y = 6;
        Integer arr[] = { 1, 4 };
        int M = arr.length;

        // Function Call
        System.out.println(findMaxBomb(N, M, X, Y, arr));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number
# of bomb that can be blasted before
# the thief gets caught
def findMaxBomb(N, M, X, Y, arr):

    # Sort the array arr[] in
    # descending order
    arr.sort(reverse = True)

    # Stores the maxtime the thief
    # has before getting caught
    maxSec = 0

    # If Y is less than X
    if (Y < X):
        maxSec = N - Y

    # Otherwise
    else:
        maxSec = Y - 1

    # Stores the current
    # second
    time = 1

    # Stores the count of
    # bomb blasts
    count = 0

    # Traverse the array arr[]
    for i in range(M):

        # If arr[i]+time is less
        # than or equal to the
        # maxSec
        if (arr[i] + time <= maxSec):

            # Increment time and
            # count by 1
            time += 1
            count += 1

    # Update count
    count = min(count, abs(X - Y) - 1)

    # Return the value of count
    return count

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 7
    X = 3
    Y = 6
    arr = [ 1, 4 ]
    M = len(arr)

    # Function Call
    print(findMaxBomb(N, M, X, Y, arr))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum number
// of bomb that can be blasted before
// the thief gets caught
static int findMaxBomb(int N, int M, int X,
                       int Y, int[] arr)
{

    // Sort the array arr[] in
    // descending order
    Array.Sort(arr);

    // Reverse array
    Array.Reverse(arr);

    // Stores the maxtime the thief
    // has before getting caught
    int maxSec;

    // If Y is less than X
    if (Y < X)
    {
        maxSec = N - Y;
    }

    // Otherwise
    else
    {
        maxSec = Y - 1;
    }

    // Stores the current
    // second
    int time = 1;

    // Stores the count of
    // bomb blasts
    int count = 0;

    // Traverse the array arr[]
    for(int i = 0; i < M; i++)
    {

        // If arr[i]+time is less
        // than or equal to the
        // maxSec
        if (arr[i] + time <= maxSec)
        {

            // Increment time and
            // count by 1
            time++;
            count++;
        }
    }

    // Update count
    count = Math.Min(count, Math.Abs(X - Y) - 1);

    // Return the value of count
    return count;
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int N = 7, X = 3, Y = 6;
    int[] arr = { 1, 4 };
    int M = arr.Length;

    // Function Call
    Console.WriteLine(findMaxBomb(N, M, X, Y, arr));
}
}

// This code is contributed by target_2
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the maximum number
        // of bomb that can be blasted before
        // the thief gets caught
        function findMaxBomb(N, M, X, Y, arr) {
            // Sort the array arr[] in
            // descending order
            arr.sort(function (a, b) { return b - a })

            // Stores the maxtime the thief
            // has before getting caught
            let maxSec;

            // If Y is less than X
            if (Y < X) {
                maxSec = N - Y;
            }
            // Otherwise
            else {
                maxSec = Y - 1;
            }

            // Stores the current
            // second
            let time = 1;

            // Stores the count of
            // bomb blasts
            let count = 0;

            // Traverse the array arr[]
            for (let i = 0; i < M; i++) {

                // If arr[i]+time is less
                // than or equal to the
                // maxSec
                if (arr[i] + time <= maxSec) {
                    // Increment time and
                    // count by 1
                    time++;
                    count++;
                }
            }

            // Update count
            count = Math.min(count, Math.abs(X - Y) - 1);

            // Return the value of count
            return count;
        }

        // Driver Code

        // Given Input
        let N = 7, X = 3, Y = 6;
        let arr = [1, 4];
        let M = arr.length;

        // Function Call
        document.write(findMaxBomb(N, M, X, Y, arr));

    // This code is contributed by Potta Lokesh

</script>
```

**Output**

```
2
```

***时间复杂度:** O(M*log(M))，其中 **M** 是数组 **arr[]的大小。***
***辅助空间:** O(1)*
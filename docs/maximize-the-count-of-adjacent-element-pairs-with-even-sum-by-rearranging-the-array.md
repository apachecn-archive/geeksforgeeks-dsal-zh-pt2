# 通过重新排列数组

最大化具有偶数和的相邻元素对的数量

> 原文:[https://www . geeksforgeeks . org/通过重新排列数组最大化偶和相邻元素对的数量/](https://www.geeksforgeeks.org/maximize-the-count-of-adjacent-element-pairs-with-even-sum-by-rearranging-the-array/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** ，任务是以偶数和找到相邻[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的最大可能计数，重新排列数组 **arr[]。**

**示例:**

> **输入:** arr[] = {5，5，1}
> **输出:** 2
> **解释:**
> 给定的数组已经被安排为以偶数和给出相邻对的最大计数。
> 
> 1.  {arr[0](= 5)，arr[1](= 5}，元素之和为 10，为偶数。
> 2.  {arr[1](= 5)，arr[2](= 1}，元素之和为 6，为偶数。
> 
> 因此，两个相邻对的总和为偶数。这也是最大可能的计数。
> 
> **输入:** arr[] = {9，13，15，3，16，9，13，18}
> **输出:** 6
> **解释:**
> 获得最大计数的一种方法是将数组重新排列为{9，9，3，13，13，15，16，18}。
> 
> 1.  {arr[0](= 9)，arr[1](= 9}，元素之和为 18，为偶数。
> 2.  {arr[1](= 9)，arr[2](= 3}，元素之和为 12，为偶数。
> 3.  {arr[2](= 3)，arr[3](= 13}，元素之和为 16，为偶数。
> 4.  {arr[3](= 13)，arr[4](= 13}，元素之和为 26，为偶数。
> 5.  {arr[4](= 13)，arr[5](= 15}，元素之和为 28，为偶数。
> 6.  {arr[5](= 15)，arr[6](= 16}，元素之和是 31，不是偶数。
> 7.  {arr[6](= 16)，arr[7](= 18}，元素之和为 34，为偶数。
> 
> 因此，总共有 6 个偶数和的相邻对。这也是最大可能的计数。

**天真法:**最简单的方法是尝试元素的每一种可能的排列方式，然后用偶数和计算相邻对的数量。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

1.  众所周知:
    *   **奇数+奇数=偶数**
    *   **偶数+偶数=偶数**
    *   **偶数+奇数=奇数**
    *   **奇数+偶数=奇数**
2.  相邻对的总数为 **N-1。**
3.  因此，最大计数可以通过将所有偶数放在一起，然后将所有奇数放在一起来获得，反之亦然。
4.  以上述方式重新排列，将只有一对奇数和的相邻元素，它们将处于偶数和奇数的结合处。

按照以下步骤解决问题:

*   [找出数组中奇数和偶数的个数](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)然后存储在变量中比如**奇数**和**偶数**。
*   如果**奇数**和**偶数**都大于 **0，**则打印总计数 **N-2** 作为答案**。**
*   否则，打印 **N-1** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum count
// pair of adjacent elements with
// even sum
int maximumCount(int arr[], int N)
{
    // Stores count of odd numbers
    int odd = 0;

    // Stores count of even numbers
    int even = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i]%2 is 1
        if (arr[i] % 2)
            odd++;
        // Else
        else
            even++;
    }

    // If odd and even both
    // are greater than 0
    if (odd and even)
        return N - 2;
    // Otherwise
    else
        return N - 1;
}

// Driver Code
int main()

{
    int arr[] = { 9, 13, 15, 3, 16, 9, 13, 18 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maximumCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    // Function to find maximum count
    // pair of adjacent elements with
    // even sum
    static int maximumCount(int arr[], int N)
    {
        // Stores count of odd numbers
        int odd = 0;

        // Stores count of even numbers
        int even = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // If arr[i]%2 is 1
            if (arr[i] % 2 == 1)
                odd++;
            // Else
            else
                even++;
        }

        // If odd and even both
        // are greater than 0
        if (odd > 0 && even > 0)
            return N - 2;
        // Otherwise
        else
            return N - 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 9, 13, 15, 3, 16, 9, 13, 18 };
        int N = arr.length;

        System.out.println(maximumCount(arr, N));
    }
}

    // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find maximum count
# pair of adjacent elements with
# even sum
def maximumCount(arr, N):

    # Stores count of odd numbers
    odd = 0

    # Stores count of even numbers
    even = 0

    # Traverse the array arr[]
    for i in range(N):

        # If arr[i]%2 is 1
        if (arr[i] % 2):
            odd += 1
        # Else
        else:
            even += 1

    # If odd and even both
    # are greater than 0
    if (odd and even):
        return N - 2
    # Otherwise
    else:
        return N - 1

# Driver Code
if __name__ == '__main__':
    arr = [9, 13, 15, 3, 16, 9, 13, 18]
    N = len(arr)

    print(maximumCount(arr, N))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum count
// pair of adjacent elements with
// even sum
static int maximumCount(int []arr, int N)
{
    // Stores count of odd numbers
    int odd = 0;

    // Stores count of even numbers
    int even = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i]%2 is 1
        if (arr[i] % 2 !=0)
            odd++;
        // Else
        else
            even++;
    }

    // If odd and even both
    // are greater than 0
    if (odd!=0 && even!=0)
        return N - 2;
    // Otherwise
    else
        return N - 1;
}

// Driver Code
public static void Main()

{
    int []arr = { 9, 13, 15, 3, 16, 9, 13, 18 };
    int N = arr.Length;

    Console.Write(maximumCount(arr, N));

}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to find maximum count
        // pair of adjacent elements with
        // even sum
        function maximumCount(arr, N)
        {

            // Stores count of odd numbers
            let odd = 0;

            // Stores count of even numbers
            let even = 0;

            // Traverse the array arr[]
            for (let i = 0; i < N; i++) {

                // If arr[i]%2 is 1
                if (arr[i] % 2)
                    odd++;
                // Else
                else
                    even++;
            }

            // If odd and even both
            // are greater than 0
            if (odd && even)
                return N - 2;
            // Otherwise
            else
                return N - 1;
        }

        // Driver Code

        let arr = [9, 13, 15, 3, 16, 9, 13, 18];
        let N = arr.length;

        document.write(maximumCount(arr, N));

    // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
# 查找大于数组中一半元素的元素|集合 2

> 原文:[https://www . geesforgeks . org/find-elements-大于数组中元素的一半-set-2/](https://www.geeksforgeeks.org/find-elements-larger-than-half-of-the-elements-in-an-array-set-2/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出大于至少一半数组元素的元素。

**示例:**

> **输入:** arr[] = {1，6，3，4}
> **输出:** 4 6
> **说明:**
> 阵的大小为 4。大于数组中至少 N/2(= 4/2 = 2)个元素的元素是 4 和 6。
> 
> **输入:** arr[] = {10，4，2，8，9 }
> T3】输出: 10 9 8

**幼稚的做法:**幼稚的做法请参考本文[之前的帖子](https://www.geeksforgeeks.org/find-elements-larger-half-elements-array/)。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**基于排序的方式:**基于排序的方式请参考本文[前一篇](https://www.geeksforgeeks.org/find-elements-larger-half-elements-array/)。

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*

**方法:**通过跟踪数组元素的[计数，使用](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) [**散列**](https://www.geeksforgeeks.org/hashing-set-1-introduction/) 也可以优化上述方法。在[找到每个元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率后，以非递增的顺序打印元素，直到 **N/2** 元素打印完毕。按照以下步骤解决问题:

*   初始化一个变量，说**中间**为 **(N + 1)/2** 来存储数组的中间索引。
*   初始化一个变量，说 **max** 来存储数组的[最大元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **计数[]** 来存储每个元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，将**计数【arr[I]】**增加 1。
*   使用变量 **i** 从后面遍历阵 **计数[]** ，并执行以下步骤:
    *   [重复直到](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)计数[i]的值为正，并执行以下步骤:
        *   打印 **i** 的值，将**计数【I】**和**中间**的值减少 **1** 。
        *   如果**中间**的值为 **0** ，则[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   如果**中间**的值为 **0** ，则[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the element that
// are larger than half of elements
// of the array
void findLarger(int arr[], int n)
{
    // Find the value of mid
    int mid = (n + 1) / 2;

    // Stores the maximum element
    int mx = *max_element(arr, arr + n);

    // Stores the frequency of each
    // array element
    int count[mx + 1] = { 0 };
    for (int i = 0; i < n; i++) {
        count[arr[i]]++;
    }

    // Traverse the array in the
    // reverse order
    for (int i = mx; i >= 0; i--) {

        while (count[i] > 0) {

            // Decrement the value
            // of count[i] and mid
            count[i]--;
            mid--;

            // Print the current element
            cout << i << ' ';

            // Check if the value of
            // mid is equal to 0
            if (mid == 0)
                break;
        }
        if (mid == 0)
            break;
    }
}

// Driver Code
int main()
{
    int arr[] = { 10, 4, 2, 8, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findLarger(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the element that
// are larger than half of elements
// of the array
static void findLarger(int arr[], int n)
{
    // Find the value of mid
    int mid = (n + 1) / 2;

    // Stores the maximum element
    int mx = Arrays.stream(arr).max().getAsInt();

    // Stores the frequency of each
    // array element
    int count[] = new int[mx+1];
    for (int i = 0; i < mx+1; i++) {
        count[i] = 0;
    }

    for (int i = 0; i < n; i++) {
        count[arr[i]]++;
    }

    // Traverse the array in the
    // reverse order
    for (int i = mx; i >= 0; i--) {

        while (count[i] > 0) {

            // Decrement the value
            // of count[i] and mid
            count[i]--;
            mid--;

            // Print the current element
            System.out.print(i + " ");

            // Check if the value of
            // mid is equal to 0
            if (mid == 0)
                break;
        }
        if (mid == 0)
            break;
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 10, 4, 2, 8, 9 };
    int N = arr.length;
    findLarger(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the element that
# are larger than half of elements
# of the array
def findLarger(arr, n):
    # Find the value of mid
    mid = (n + 1) // 2

    # Stores the maximum element
    mx = max(arr)

    # Stores the frequency of each
    # array element
    count = [0]*(mx + 1)

    for i in range(n):
        count[arr[i]] += 1

    # Traverse the array in the
    # reverse order
    for i in range(mx,-1, -1):
        while (count[i] > 0):

            # Decrement the value
            # of count[i] and mid
            count[i] -= 1
            mid -= 1

            # Prthe current element
            print(i, end = " ")

            # Check if the value of
            # mid is equal to 0
            if (mid == 0):
                break
        if (mid == 0):
            break

# Driver Code
if __name__ == '__main__':
    arr = [10, 4, 2, 8, 9 ]
    N = len(arr)
    findLarger(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the element that
// are larger than half of elements
// of the array
static void findLarger(int []arr, int n)
{
    // Find the value of mid
    int mid = (n + 1) / 2;

    // Stores the maximum element
    int mx = Int32.MinValue;
    for(int i=0;i<n;i++){
        if(arr[i]>mx)
            mx = arr[i];
    }

    // Stores the frequency of each
    // array element
    int []count = new int[mx + 1];
    Array.Clear(count,0,mx+1);
    for (int i = 0; i < n; i++) {
        count[arr[i]]++;
    }

    // Traverse the array in the
    // reverse order
    for (int i = mx; i >= 0; i--) {

        while (count[i] > 0) {

            // Decrement the value
            // of count[i] and mid
            count[i]--;
            mid--;

            // Print the current element
            Console.Write(i+" ");

            // Check if the value of
            // mid is equal to 0
            if (mid == 0)
                break;
        }
        if (mid == 0)
            break;
    }
}

// Driver Code
public static void Main()
{
    int []arr = { 10, 4, 2, 8, 9 };
    int N = arr.Length;
    findLarger(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the element that
        // are larger than half of elements
        // of the array
        function findLarger(arr, n) {
            // Find the value of mid
            let mid = (n + 1) / 2;

            // Stores the maximum element
            let mx = Math.max.apply(null, arr)

            // Stores the frequency of each
            // array element
            var count = new Array(mx + 1).fill(0);
            for (let i = 0; i < n; i++) {
                count[arr[i]]++;
            }

            // Traverse the array in the
            // reverse order
            for (let i = mx; i >= 0; i--) {

                while (count[i] > 0) {

                    // Decrement the value
                    // of count[i] and mid
                    count[i]--;
                    mid--;

                    // Print the current element
                    document.write(i + ' ');

                    // Check if the value of
                    // mid is equal to 0
                    if (mid == 0)
                        break;
                }
                if (mid == 0)
                    break;
            }
        }

        // Driver Code

        var arr = [10, 4, 2, 8, 9];
        var N = 5;
        findLarger(arr, N);

    </script>
```

**Output:** 

```
10 9 8
```

***时间复杂度:** O(M)，其中 M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)***arr【】***
***辅助空间:** O(M)*
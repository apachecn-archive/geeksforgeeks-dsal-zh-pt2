# 借助给定的初始位置和速度，最大化每秒可停止的飞机数量

> 原文:[https://www . geesforgeks . org/借助给定的初始位置和速度最大化每秒可停止的飞机数量/](https://www.geeksforgeeks.org/maximize-count-of-planes-that-can-be-stopped-per-second-with-help-of-given-initial-position-and-speed/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** 由 **N** 个整数组成，其中 **A[i]** 代表 **i <sup>th</sup>** 飞机的初始位置， **B[i]** 是飞机着陆的速度，任务是通过每秒钟射击一架飞机来打印可以停止着陆的飞机编号。

**示例:**

> **输入:** A[] = {1，3，5，4，8}，B[] = {1，2，2，1，2 }
> T3】输出:4
> T6】解释:
> 
> 1.  在第二个 1，在索引 0 拍摄飞机，飞机的位置现在是 A[] = {_，1，3，3，6}。
> 2.  在第二个 2，在索引 1 拍摄飞机，飞机的位置现在是 A[] = {_，_，1，2，4}。
> 3.  在第二个 3，在索引 2 拍摄飞机，飞机的位置现在是 A[] = {_，_，_，1，2}。
> 4.  在第二个 4，在索引 4 或 5 拍摄飞机，飞机的位置现在是 A[] = {_，_，_，_，_}。
> 
> 因此，总共可以阻止 4 架飞机着陆。
> 
> **输入:** A[] = {2，8，2，3，1}，B[] = {1，4，2，2，2 }
> T3】输出: 2

**方法:**给定的问题可以基于以下观察来解决:

*   可以观察到，可以停止的飞机数量是每架飞机着陆所需的不同时间的集合，因为在同一时间，只有一架飞机可以被摧毁。
*   飞机降落所需的时间是**A【I/B【I】**可以用公式计算:**时间=距离/速度**

按照以下步骤解决问题:

*   初始化一个[哈希集](https://www.geeksforgeeks.org/hashset-in-java/)，比如说 **S** ，存储飞机着陆所需的时间。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N】**，并执行以下任务:
    *   初始化一个变量，如果 **A[i]%B[i]** 的值大于 **0** ，则说 **t** 为 **1** 。否则，将变量 **t** 更新为 **0** 。
    *   将**A【I/B【I】**的值加到变量中，说 **t** 。
    *   [将 **t** 的值加入到 HashSet](https://www.geeksforgeeks.org/hashset-add-method-in-java/)S 中。
*   执行上述步骤后，返回 HashSet 的[大小作为结果答案。](https://www.geeksforgeeks.org/hashset-size-method-in-java/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum number
// of planes that can be stopped
// from landing
int maxPlanes(int A[], int B[], int N)
{

    // Stores the times needed for
    // landing for each plane
    set<int> St;

    // Iterate over the arrays
    for (int i = 0; i < N; i++) {

        // Stores the time needed for
        // landing of current plane
        int t = (A[i] % B[i] > 0) ? 1 : 0;

        // Update the value of t
        t += (A[i] / B[i]) + t;

        // Append the t in set St
        St.insert(t);
    }

    // Return the answer
    return St.size();
}

 // Driver Code
int main() {

    int A[] = { 1, 3, 5, 4, 8 };
    int B[] = { 1, 2, 2, 1, 2 };
      int N = sizeof(A)/sizeof(A[0]);

    cout << maxPlanes(A, B, N);

    return 0;
}

// This code is contributed by Dharanendra L V.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find maximum number
    // of planes that can be stopped
    // from landing
    static int maxPlanes(int[] A, int[] B)
    {
        // Stores the times needed for
        // landing for each plane
        Set<Integer> St = new HashSet<>();

        // Iterate over the arrays
        for (int i = 0; i < A.length; i++) {

            // Stores the time needed for
            // landing of current plane
            int t = (A[i] % B[i] > 0) ? 1 : 0;

            // Update the value of t
            t += (A[i] / B[i]) + t;

            // Append the t in set St
            St.add(t);
        }

        // Return the answer
        return St.size();
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] A = { 1, 3, 5, 4, 8 };
        int[] B = { 1, 2, 2, 1, 2 };
        System.out.println(
            maxPlanes(A, B));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find maximum number
# of planes that can be stopped
# from landing
def maxPlanes(A, B, N):

    # Stores the times needed for
    # landing for each plane
    St = set()

    # Iterate over the arrays
    for i in range(N):

        # Stores the time needed for
        # landing of current plane
        t = 1 if (A[i] % B[i] > 0) else 0

        # Update the value of t
        t += (A[i] // B[i]) + t

        # Append the t in set St
        St.add(t)

    # Return the answer
    return len(St)

# Driver Code
A = [ 1, 3, 5, 4, 8 ]
B = [ 1, 2, 2, 1, 2 ]
N = len(A)
print(maxPlanes(A, B, N))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

    // Function to find maximum number
    // of planes that can be stopped
    // from landing
    static int maxPlanes(int[] A, int[] B)
    {

        // Stores the times needed for
        // landing for each plane
         HashSet<int> St = new HashSet<int>();

        // Iterate over the arrays
        for (int i = 0; i < A.Length; i++) {

            // Stores the time needed for
            // landing of current plane
            int t = (A[i] % B[i] > 0) ? 1 : 0;

            // Update the value of t
            t += (A[i] / B[i]) + t;

            // Append the t in set St
            St.Add(t);
        }

        // Return the answer
        return St.Count;
    }

  // Driver code
    static public void Main (){

       int[] A = { 1, 3, 5, 4, 8 };
        int[] B = { 1, 2, 2, 1, 2 };
        Console.WriteLine(
            maxPlanes(A, B));
    }
}

// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>

    // Function to find maximum number
    // of planes that can be stopped
    // from landing
    function maxPlanes(A, B)
    {

        // Stores the times needed for
        // landing for each plane
        let St = new Set();

        // Iterate over the arrays
        for (let i = 0; i < A.length; i++) {

            // Stores the time needed for
            // landing of current plane
            let t = (A[i] % B[i] > 0) ? 1 : 0;

            // Update the value of t
            t += Math.floor(A[i] / B[i]) + t;

            // Append the t in set St
            St.add(t);
        }

        // Return the answer
        return St.size;
    }

// Driver Code
        let A = [ 1, 3, 5, 4, 8 ];
        let B = [ 1, 2, 2, 1, 2 ];
        document.write(
            maxPlanes(A, B));

    // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
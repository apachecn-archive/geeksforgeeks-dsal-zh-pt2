# 从某人开始分发 M 个对象，这样每个人都会得到一个对象

> 原文:[https://www . geesforgeks . org/distribute-m-objects-start-from-this-person-this-with-person-arri-objects/](https://www.geeksforgeeks.org/distribute-m-objects-starting-from-sth-person-such-that-every-ith-person-gets-arri-objects/)

给定一个由 **N** 个整数( *1 基索引*)和两个整数 **M** 和 **S** 组成的[数组**arr【】**，任务是从位置 **S** 开始，在 N 个人中分配 **M** 个对象，使得第 i <sup>个</sup>个人每次最多获得**arr【I】**个对象](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> **输入:** arr[] = {2，3，2，1，4}，M = 11，S = 2
> **输出:** 1，3，2，1，4
> **说明:**从 S <sup>第</sup> (= 2)个人开始的 M (= 11)个对象的分布如下:
> 
> *   **为 arr[2](= 3):** 给 2 <sup>第</sup>T4 人 3 个物体。现在，对象总数减少到(11–3)= 8。
> *   **为 arr[3] (= 2):** 给 3 <sup>第</sup>T4 人 2 个物体。现在，对象总数减少到(8–2)= 6。
> *   **对于 arr[4] (= 1):** 给第 4 个<sup>人 1 个对象。现在，对象总数减少到(6–1)= 5。</sup>
> *   **对于 arr[5] (= 4):** 给第 5 个<sup>人 4 个物体。现在，对象总数减少到(5–4)= 1。</sup>
> *   **为 arr[1] (= 1):** 给 1 <sup>圣</sup>人 1 个对象。现在，对象总数减少到(1–1)= 0。
> 
> 因此，对象的分布是{1，3，2，1，4}。
> 
> **输入:** arr[] = {2，3，2，1，4}，M = 3，S = 4
> **输出:** 0 0 0 1 2

**方法:**给定的问题可以通过[从给定的起始索引 **S** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将最大对象分配给每个数组元素来解决。按照以下步骤解决给定的问题:

*   初始化一个辅助数组，说**分布[]** ，所有元素为 **0** ，存储 **M 个对象**的分布。
*   初始化两个变量，分别称 **ptr** 和 **rem** 为 **S** 和 **M** ，存储起始索引和剩余 **M 个对象**。
*   重复直到 **rem** 为正，并执行以下步骤:
    *   如果 **rem** 的值至少是**索引 **ptr** 处的元素，即**arr【ptr】**，那么将**分布【ptr】**的值增加**arr【ptr】**，将 **rem** 的值减少**arr【ptr】**。**
    *   **否则，将**分布【ptr】**增加**雷姆**，并将**雷姆**更新为等于 **0** 。**
    *   **更新 **ptr** 等于 **(ptr + 1) % N** 以循环方式迭代给定数组 **arr[]** 。**
*   **完成以上步骤后，打印**分布[]** 作为对象的合成分布。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find distribution of
// M objects among all array elements
void distribute(int N, int K,
                int M, int arr[])
{
    // Stores the distribution
    // of M objects
    int distribution[N] = { 0 };

    // Stores the indices
    // of distribution
    int ptr = K - 1;

    // Stores the remaining objects
    int rem = M;

    // Iterate until rem is positive
    while (rem > 0) {

        // If the number of remaining
        // objects exceeds required
        // the number of objects
        if (rem >= arr[ptr]) {

            // Increase the number of objects
            // for the index ptr by arr[ptr]
            distribution[ptr] += arr[ptr];

            // Decrease remaining
            // objects by arr[ptr]
            rem -= arr[ptr];
        }
        else {

            // Increase the number of objects
            // for the index ptr by rem
            distribution[ptr] += rem;

            // Decrease remaining
            // objects to 0
            rem = 0;
        }

        // Increase ptr by 1
        ptr = (ptr + 1) % N;
    }

    // Print the final distribution
    for (int i = 0; i < N; i++) {
        cout << distribution[i]
             << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 2, 1, 4 };
    int M = 11, S = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    distribute(N, S, M, arr);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to find distribution of
  // M objects among all array elements
  static void distribute(int N, int K, int M, int arr[])
  {
    // Stores the distribution
    // of M objects
    int distribution[] = new int[N];

    // Stores the indices
    // of distribution
    int ptr = K - 1;

    // Stores the remaining objects
    int rem = M;

    // Iterate until rem is positive
    while (rem > 0) {

      // If the number of remaining
      // objects exceeds required
      // the number of objects
      if (rem >= arr[ptr]) {

        // Increase the number of objects
        // for the index ptr by arr[ptr]
        distribution[ptr] += arr[ptr];

        // Decrease remaining
        // objects by arr[ptr]
        rem -= arr[ptr];
      }
      else {

        // Increase the number of objects
        // for the index ptr by rem
        distribution[ptr] += rem;

        // Decrease remaining
        // objects to 0
        rem = 0;
      }

      // Increase ptr by 1
      ptr = (ptr + 1) % N;
    }

    // Print the final distribution
    for (int i = 0; i < N; i++) {
      System.out.print(distribution[i] + " ");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 2, 3, 2, 1, 4 };
    int M = 11, S = 2;
    int N = arr.length;

    distribute(N, S, M, arr);
  }
}

// This code is contributed by Kingash.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find distribution of
# M objects among all array elements
def distribute(N, K, M, arr):

    # Stores the distribution
    # of M objects
    distribution = [0] * N

    # Stores the indices
    # of distribution
    ptr = K - 1

    # Stores the remaining objects
    rem = M

    # Iterate until rem is positive
    while (rem > 0):

        # If the number of remaining
        # objects exceeds required
        # the number of objects
        if (rem >= arr[ptr]):

            # Increase the number of objects
            # for the index ptr by arr[ptr]
            distribution[ptr] += arr[ptr]

            # Decrease remaining
            # objects by arr[ptr]
            rem -= arr[ptr]

        else:

            # Increase the number of objects
            # for the index ptr by rem
            distribution[ptr] += rem

            # Decrease remaining
            # objects to 0
            rem = 0

        # Increase ptr by 1
        ptr = (ptr + 1) % N

    # Print the final distribution
    for i in range(N):
        print(distribution[i], end = " ")

# Driver Code
arr = [ 2, 3, 2, 1, 4 ]
M = 11
S = 2
N = len(arr)

distribute(N, S, M, arr)

# This code is contributed by sanjoy_62
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to find distribution of
// M objects among all array elements
static void distribute(int N, int K,
                       int M, int []arr)
{

    // Stores the distribution
    // of M objects
    int []distribution = new int[N];

    // Stores the indices
    // of distribution
    int ptr = K - 1;

    // Stores the remaining objects
    int rem = M;

    // Iterate until rem is positive
    while (rem > 0)
    {

        // If the number of remaining
        // objects exceeds required
        // the number of objects
        if (rem >= arr[ptr])
        {

            // Increase the number of objects
            // for the index ptr by arr[ptr]
            distribution[ptr] += arr[ptr];

            // Decrease remaining
            // objects by arr[ptr]
            rem -= arr[ptr];
        }
        else
        {

            // Increase the number of objects
            // for the index ptr by rem
            distribution[ptr] += rem;

            // Decrease remaining
            // objects to 0
            rem = 0;
        }

        // Increase ptr by 1
        ptr = (ptr + 1) % N;
    }

    // Print the final distribution
    for(int i = 0; i < N; i++)
    {
        Console.Write(distribution[i] + " ");
    }
}

// Driver Code
public static void Main(string[] args)
{
    int []arr = { 2, 3, 2, 1, 4 };
    int M = 11, S = 2;
    int N = arr.Length;

    distribute(N, S, M, arr);
}
}

// This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
        // Javascript program for the above approach

        // Function to find distribution of
        // M objects among all array elements
        function distribute( N,  K,
             M,  arr)
        {
            // Stores the distribution
            // of M objects
            let distribution = new Array(N)

            for (let i = 0; i < N; i++) {
                distribution[i]=0
            }
            // Stores the indices
            // of distribution
            let ptr = K - 1;

            // Stores the remaining objects
            let rem = M;

            // Iterate until rem is positive
            while (rem > 0) {

                // If the number of remaining
                // objects exceeds required
                // the number of objects
                if (rem >= arr[ptr]) {

                    // Increase the number of objects
                    // for the index ptr by arr[ptr]
                    distribution[ptr] += arr[ptr];

                    // Decrease remaining
                    // objects by arr[ptr]
                    rem -= arr[ptr];
                }
                else {

                    // Increase the number of objects
                    // for the index ptr by rem
                    distribution[ptr] += rem;

                    // Decrease remaining
                    // objects to 0
                    rem = 0;
                }

                // Increase ptr by 1
                ptr = (ptr + 1) % N;
            }

            // Print the final distribution
            for (let i = 0; i < N; i++) {
                document.write(distribution[i]+" ")
            }
        }

        // Driver Code

        let arr = [ 2, 3, 2, 1, 4 ];
        let M = 11, S = 2;
        let N = arr.length
        distribute(N, S, M, arr);

        // This code is contributed by Hritik
    </script>
```

****Output:** 

```
1 3 2 1 4
```** 

*****时间复杂度:** O(M)*
***辅助空间:** O(N)***
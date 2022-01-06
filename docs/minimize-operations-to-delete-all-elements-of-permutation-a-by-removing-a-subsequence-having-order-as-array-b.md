# 通过移除具有与数组 B 相同顺序的子序列，最小化删除排列 A 的所有元素的操作

> 原文:[https://www . geeksforgeeks . org/最小化-操作-删除-通过移除-a-子序列-具有-作为-b-数组的-顺序-来删除-a-排列的所有元素/](https://www.geeksforgeeks.org/minimize-operations-to-delete-all-elements-of-permutation-a-by-removing-a-subsequence-having-order-as-array-b/)

给定第一个 **N** [**自然数**](https://www.geeksforgeeks.org/natural-numbers/) 的两个[置换数组](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)**A【】**和**B【】**，任务是找到移除所有数组元素**A【】**所需的最小操作数，从而在每个操作中移除顺序与数组**B【】**中相同的数组元素[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)**A【】**

**示例:**

> **输入:** A[] = { 4，2，1，3 }，B[] = { 1，3，2，4 }
> **输出:** 3
> **解释:**
> 给定的例子可以按照给定的步骤求解:
> 
> 1.  在第一次操作期间，数组 A[]中索引 2 和 3 处的整数可以被删除。因此，数组 A[] = {4，2}。
> 2.  在 2st 操作期间，可以删除数组 A[]中索引 1 处的整数。因此，数组 A[] = {4}。
> 3.  在第三次操作期间，可以删除数组 A[]中索引 0 处的整数。因此，数组 A[] = {}。
> 
> 删除元素的顺序是{1，3，2，4}，等于 b。因此至少需要 3 次操作。
> 
> **输入:** A[] = {2，4，6，1，5，3}，B[] = {6，5，4，2，3，1}
> **输出:** 4

**方法:**给定的问题可以使用下面讨论的步骤来解决:

1.  创建两个变量 **i** 和 **j** ，其中 **i** 记录下一个要删除的 **B** 的当前元素的索引，而 **j** 记录 **A** 的当前元素。最初， **i=0** 和 **j=0** 。
2.  [对范围**【0，N-1】**中 **j** 的所有值，使用 **j** 遍历排列数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** 。如果 **A[j] = B[i]** ，则将 **i** 的值增加 1，继续遍历数组 **A[]** 。
3.  在数组**A【】**被完全遍历后，增加 **cnt** 变量的值，该变量保持所需操作的计数。
4.  重复步骤 **2** 和 **3** 直到 **i < N** 。
5.  完成上述步骤后，存储在 **cnt** 中的值即为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// operations to delete all elements of
// permutation A in order described by B
int minOperations(int A[], int B[], int N)
{
    // Stores the count of operations
    int cnt = 0;

    // Stores the index of current integer
    // in B to be deleted
    int i = 0;

    // Loop to iterate over all values of B
    while (i < N) {

        // Stores the current index in A
        int j = 0;

        // Iterate over all values A
        while (j < N && i < N) {

            // If current integer of B and A
            // equal, increment the index of
            // the current integer of B
            if (B[i] == A[j]) {
                i++;
            }
            j++;
        }

        // As the permutation A has been
        // traversed completelly, increment
        // the count of operations by 1
        cnt++;
    }

    // Return Answer
    return cnt;
}

// Driver Code
int main()
{
    int A[] = { 2, 4, 6, 1, 5, 3 };
    int B[] = { 6, 5, 4, 2, 3, 1 };
    int N = sizeof(A) / sizeof(A[0]);

    cout << minOperations(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum number of
// operations to delete all elements of
// permutation A in order described by B
static int minOperations(int A[], int B[], int N)
{

    // Stores the count of operations
    int cnt = 0;

    // Stores the index of current integer
    // in B to be deleted
    int i = 0;

    // Loop to iterate over all values of B
    while (i < N) {

        // Stores the current index in A
        int j = 0;

        // Iterate over all values A
        while (j < N && i < N) {

            // If current integer of B and A
            // equal, increment the index of
            // the current integer of B
            if (B[i] == A[j]) {
                i++;
            }
            j++;
        }

        // As the permutation A has been
        // traversed completely, increment
        // the count of operations by 1
        cnt++;
    }

    // Return Answer
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 4, 6, 1, 5, 3 };
    int B[] = { 6, 5, 4, 2, 3, 1 };
    int N = A.length;

    System.out.print(minOperations(A, B, N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum number of
# operations to delete all elements of
# permutation A in order described by B
def minOperations(A, B, N):

    # Stores the count of operations
    cnt = 0

    # Stores the index of current integer
    # in B to be deleted
    i = 0

    # Loop to iterate over all values of B
    while(i < N):

        # Stores the current index in A
        j = 0

        # Iterate over all values A
        while (j < N and i < N):

            # If current integer of B and A
            # equal, increment the index of
            # the current integer of B
            if (B[i] == A[j]):
                i += 1
            j += 1

        # As the permutation A has been
        # traversed completely, increment
        # the count of operations by 1
        cnt += 1

    # Return Answer
    return cnt

# Driver Code
if __name__ == '__main__':
    A = [2, 4, 6, 1, 5, 3]
    B = [6, 5, 4, 2, 3, 1]
    N = len(A)

    print(minOperations(A, B, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the minimum number of
    // operations to delete all elements of
    // permutation A in order described by B
    static int minOperations(int[] A, int[] B, int N)
    {

        // Stores the count of operations
        int cnt = 0;

        // Stores the index of current integer
        // in B to be deleted
        int i = 0;

        // Loop to iterate over all values of B
        while (i < N) {

            // Stores the current index in A
            int j = 0;

            // Iterate over all values A
            while (j < N && i < N) {

                // If current integer of B and A
                // equal, increment the index of
                // the current integer of B
                if (B[i] == A[j]) {
                    i++;
                }
                j++;
            }

            // As the permutation A has been
            // traversed completely, increment
            // the count of operations by 1
            cnt++;
        }

        // Return Answer
        return cnt;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] A = { 2, 4, 6, 1, 5, 3 };
        int[] B = { 6, 5, 4, 2, 3, 1 };
        int N = A.Length;

        Console.WriteLine(minOperations(A, B, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the minimum number of
       // operations to delete all elements of
       // permutation A in order described by B
       function minOperations(A, B, N) {
           // Stores the count of operations
           let cnt = 0;

           // Stores the index of current integer
           // in B to be deleted
           let i = 0;

           // Loop to iterate over all values of B
           while (i < N) {

               // Stores the current index in A
               let j = 0;

               // Iterate over all values A
               while (j < N && i < N) {

                   // If current integer of B and A
                   // equal, increment the index of
                   // the current integer of B
                   if (B[i] == A[j]) {
                       i++;
                   }
                   j++;
               }

               // As the permutation A has been
               // traversed completely, increment
               // the count of operations by 1
               cnt++;
           }

           // Return Answer
           return cnt;
       }

       // Driver Code

       let A = [2, 4, 6, 1, 5, 3];
       let B = [6, 5, 4, 2, 3, 1];
       let N = A.length;

       document.write(minOperations(A, B, N));

    // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
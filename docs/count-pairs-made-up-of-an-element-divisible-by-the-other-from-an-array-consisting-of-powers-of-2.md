# 从一个 2 的幂组成的数组中计数由一个可被另一个整除的元素组成的对

> 原文:[https://www . geesforgeks . org/count-pairs-由 2 的幂组成的数组中的一个元素可被另一个整除/](https://www.geeksforgeeks.org/count-pairs-made-up-of-an-element-divisible-by-the-other-from-an-array-consisting-of-powers-of-2/)

给定一个由 **2** 的**N**T6【次方】组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算对的数量 **(arr[i]，arr[j])** ，使得 **i < j** 和 **arr[j]** 可被 **arr[i]** 整除。

**示例:**

> **输入:** arr[] = {4，16，8，64}
> **输出:** 5
> **解释:**
> 满足给定条件的对为{4，16}、{4，8}、{4，64}、{16，64}、{8，64}。
> 
> **输入:** arr[] = {2，4，8，16}
> **输出:** 6
> **解释:**
> 满足给定条件的对为{2，4}、{2，8}、{2，16}、{4，8}、{4，16}、{8，16}。

**天真方法:**最简单的方法是[生成给定数组的所有对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **arr[]** ，对于每一对，检查 **arr[j] % arr[i]** 是否为 **0** 。如果发现为真，将**计数**增加 1。最后，检查所有对后，打印**计数**的值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:2 的任何**幂在其[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中只有**一个设置位**。对于任何这样的元素 **arr[j]** ，其设置位位于小于或等于 **arr[j]** 的设置位位置的 2 的所有乘方将满足给定条件。按照以下步骤解决问题:**

*   初始化一个大小等于 **31** 的辅助数组**设置位**，初始化**计数**为 **0** ，存储所需的对数。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下操作:
    *   将**最左边的设置位[存储在**位**中。](https://www.geeksforgeeks.org/find-significant-set-bit-number/)**
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，位位置】**中迭代，并在每一步中通过**设置位【j】**增加**计数**。
    *   将**设置位**增加 **1** 。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs as per the given conditions
void numberOfPairs(int arr[], int N)
{
    // Initialize array set_bits as 0
    int set_bits[31] = { 0 };

    // Store the total number of
    // required pairs
    int count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Store arr[i] in x
        int x = arr[i];

        // Store the position of the
        // leftmost set bit in arr[i]
        int bitpos = -1;

        while (x > 0) {

            // Increase bit position
            bitpos++;

            // Divide by 2 to shift bits
            // in right at each step
            x /= 2;
        }

        // Count of pairs for index i
        // till its set bit position
        for (int j = 0;
             j <= bitpos; j++) {
            count += set_bits[j];
        }

        // Increasing count of set bit
        // position of current elelement
        set_bits[bitpos]++;
    }

    // Print the answer
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 4, 16, 8, 64 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    numberOfPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count the number of
// pairs as per the given conditions
static void numberOfPairs(int arr[], int N)
{

    // Initialize array set_bits as 0
    int []set_bits = new int[31];
    Arrays.fill(set_bits, 0);

    // Store the total number of
    // required pairs
    int count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Store arr[i] in x
        int x = arr[i];

        // Store the position of the
        // leftmost set bit in arr[i]
        int bitpos = -1;
        while (x > 0)
        {

            // Increase bit position
            bitpos++;

            // Divide by 2 to shift bits
            // in right at each step
            x /= 2;
        }

        // Count of pairs for index i
        // till its set bit position
        for (int j = 0;
             j <= bitpos; j++)
        {
            count += set_bits[j];
        }

        // Increasing count of set bit
        // position of current elelement
        set_bits[bitpos]++;
    }

    // Print the answer
    System.out.println(count);
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 4, 16, 8, 64 };
    int N = arr.length;

    // Function Call
    numberOfPairs(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# pairs as per the given conditions
def numberOfPairs(arr, N):

    # Initialize array set_bits as 0
    set_bits = [0]*31

    # Store the total number of
    # required pairs
    count = 0

    # Traverse the array arr[]
    for i in range(N):

        # Store arr[i] in x
        x = arr[i]

        # Store the position of the
        # leftmost set bit in arr[i]
        bitpos = -1

        while (x > 0):

            # Increase bit position
            bitpos += 1

            # Divide by 2 to shift bits
            # in right at each step
            x //= 2

        # Count of pairs for index i
        # till its set bit position
        for j in range(bitpos + 1):
            count += set_bits[j]

        # Increasing count of set bit
        # position of current elelement
        set_bits[bitpos] += 1

    # Prthe answer
    print (count)

# Driver Code
if __name__ == '__main__':
    arr = [4, 16, 8, 64]
    N = len(arr)

    # Function Call
    numberOfPairs(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to count the number of
// pairs as per the given conditions
static void numberOfPairs(int[] arr, int N)
{

    // Initialize array set_bits as 0
    int []set_bits = new int[31];
    for (int i = 0; i < N; i++)
    {
        set_bits[i] = 0;
    }

    // Store the total number of
    // required pairs
    int count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Store arr[i] in x
        int x = arr[i];

        // Store the position of the
        // leftmost set bit in arr[i]
        int bitpos = -1;
        while (x > 0)
        {

            // Increase bit position
            bitpos++;

            // Divide by 2 to shift bits
            // in right at each step
            x /= 2;
        }

        // Count of pairs for index i
        // till its set bit position
        for (int j = 0;
             j <= bitpos; j++)
        {
            count += set_bits[j];
        }

        // Increasing count of set bit
        // position of current elelement
        set_bits[bitpos]++;
    }

    // Print the answer
    Console.Write(count);
}

// Driver Code
static public void Main()
{
    int[] arr = { 4, 16, 8, 64 };
    int N = arr.Length;

    // Function Call
    numberOfPairs(arr, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// pairs as per the given conditions
function numberOfPairs(arr, N)
{

    // Initialize array set_bits as 0
    let set_bits = [];
    for (let i = 0; i < 31; i++)
    {
        set_bits[i] = 0;
    }

    // Store the total number of
    // required pairs
    let count = 0;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++)
    {

        // Store arr[i] in x
        let x = arr[i];

        // Store the position of the
        // leftmost set bit in arr[i]
        let bitpos = -1;
        while (x > 0)
        {

            // Increase bit position
            bitpos++;

            // Divide by 2 to shift bits
            // in right at each step
            x = Math.floor( x / 2 );
        }

        // Count of pairs for index i
        // till its set bit position
        for (let j = 0;
             j <= bitpos; j++)
        {
            count += set_bits[j];
        }

        // Increasing count of set bit
        // position of current elelement
        set_bits[bitpos]++;
    }

    // Print the answer
    document.write(count);
}

// Driver Code

      let arr = [ 4, 16, 8, 64 ];
    let N = arr.length;

    // Function Call
    numberOfPairs(arr, N);

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*log M)，其中 M 为阵中* [*最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) 。
***辅助空间:** O(1)*
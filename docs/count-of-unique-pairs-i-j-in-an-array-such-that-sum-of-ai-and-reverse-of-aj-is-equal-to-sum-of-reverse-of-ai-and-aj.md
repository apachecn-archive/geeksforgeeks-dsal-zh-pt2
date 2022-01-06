# 阵列中唯一对(I，j)的计数，使得 A[i]和 A[j]的倒数之和等于 A[i]和 A[j]的倒数之和

> 原文:[https://www . geeksforgeeks . org/唯一对计数-I-j-in-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a](https://www.geeksforgeeks.org/count-of-unique-pairs-i-j-in-an-array-such-that-sum-of-ai-and-reverse-of-aj-is-equal-to-sum-of-reverse-of-ai-and-aj/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出唯一对 **(i，j)** 的计数，使得 **arr[i]** 和**反向(arr[j])** 的和与**反向(arr[i])** 和 **arr[j]** 的和相同。

**示例:**

> **输入:** arr[] = {2，15，11，7}
> **输出:** 3
> **解释:**
> 配对为(0，2)、(0，3)和(2，3)。
> 
> *   (0，2):arr[0]+reverse(arr[2])(= 2+11 = 13)和 reverse(arr[0])+arr[2](= 2+11 = 13)。
> *   (0，3):arr[0]+reverse(arr[3])(= 2+7 = 9)和 reverse(arr[0]) + arr[3](= 2 + 7 = 9)。
> *   (2，3):arr[2]+reverse(arr[3])(= 11+7 = 18)和 reverse(arr[2])+arr[3](= 11+7 = 18)。
> 
> **输入:** A[] = {22，115，7，313，17，23，22 }
> T3】输出: 6

**简单方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能对，如果任何一对元素满足给定条件，则计算这些对。完成上述步骤后，打印**计数**的值作为结果。

***时间复杂度:** O(N <sup>2</sup> *log M)，其中 M 是 A[]*
***辅助空间中的最大元素:** O(1)*

**有效方法:**上述方法可以通过使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)技术并将等式重写为:
来优化

> A[i] +倒车(A[j]) =倒车(A[I])+A[j]
> =>A[I]–倒车(A[I])= A[j]–倒车(A[j])

现在，想法是为每个元素**arr【I】**计算**(A[I]–反向(A[I])**的频率，然后计算满足给定条件的有效对的可能数量。按照以下步骤解决问题:

*   维护一个 [Hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，说 **u_map** 到[存储任意指标 **i** 的](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)**A【I】–反向(A【I】)**的频率计数。
*   初始化一个变量**对**，以存储满足给定条件的对的数量。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** ，并执行以下操作:
    *   将**A[I]–反向(A[i])** 的频率存储在**值**中。
    *   将**对**增加**值**。
    *   更新 **u_map** 中**值**的频率。
*   完成以上步骤后，打印**对**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// reverse of the number n
int reverse(int n)
{
    int temp = n, rev = 0, r;

    // Iterate until temp is 0
    while (temp) {

        r = temp % 10;
        rev = rev * 10 + r;
        temp /= 10;
    }

    // Return the reversed number
    return rev;
}

// Function to count number of unique
// pairs (i, j) from the array A[]
// which satisfies the given condition
void countPairs(int A[], int N)
{
    // Store the frequency of keys
    // as A[i] - reverse(A[i])
    unordered_map<int, int> u_map;

    // Stores count of desired pairs
    int pairs = 0;

    // Iterate the array A[]
    for (int i = 0; i < N; i++) {

        int val = A[i] - reverse(A[i]);

        // Add frequency of val
        // to the required answer
        pairs += u_map[val];

        // Increment frequency of val
        u_map[val]++;
    }

    // Print the number of pairs
    cout << pairs;
}

// Driver Code
int main()
{
    int arr[] = { 2, 15, 11, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the
// reverse of the number n
static int reverse(int n)
{
    int temp = n, rev = 0, r;

    // Iterate until temp is 0
    while (temp > 0)
    {
        r = temp % 10;
        rev = rev * 10 + r;
        temp /= 10;
    }

    // Return the reversed number
    return rev;
}

// Function to count number of unique
// pairs (i, j) from the array A[]
// which satisfies the given condition
static void countPairs(int A[], int N)
{

    // Store the frequency of keys
    // as A[i] - reverse(A[i])
    HashMap<Integer, Integer> map = new HashMap<>();

    // Stores count of desired pairs
    int pairs = 0;

    // Iterate the array A[]
    for(int i = 0; i < N; i++)
    {
        int val = A[i] - reverse(A[i]);

        // Add frequency of val
        // to the required answer
        pairs += map.getOrDefault(val, 0);

        // Increment frequency of val
        map.put(val, map.getOrDefault(val, 0) + 1);
    }

    // Print the number of pairs
    System.out.println(pairs);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 15, 11, 7 };
    int N = arr.length;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to find the
# reverse of the number n
def reverse(n):
    temp = n
    rev = 0

    # Iterate until temp is 0
    while (temp):
        r = temp % 10
        rev = rev * 10 + r
        temp //= 10

    # Return the reversed number
    return rev

# Function to count number of unique
# pairs (i, j) from the array A[]
# which satisfies the given condition
def countPairs(A, N):

    # Store the frequency of keys
    # as A[i] - reverse(A[i])
    u_map = defaultdict(int)

    # Stores count of desired pairs
    pairs = 0

    # Iterate the array A[]
    for i in range(N):
        val = A[i] - reverse(A[i])

        # Add frequency of val
        # to the required answer
        pairs += u_map[val]

        # Increment frequency of val
        u_map[val] += 1

    # Print the number of pairs
    print(pairs)

# Driver Code
if __name__ == "__main__":

    arr = [2, 15, 11, 7]
    N = len(arr)

    # Function Call
    countPairs(arr, N)

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the
// reverse of the number n
static int reverse(int n)
{
    int temp = n, rev = 0, r;

    // Iterate until temp is 0
    while (temp > 0)
    {
        r = temp % 10;
        rev = rev * 10 + r;
        temp /= 10;
    }

    // Return the reversed number
    return rev;
}

// Function to count number of unique
// pairs (i, j) from the array A[]
// which satisfies the given condition
static void countPairs(int []A, int N)
{

    // Store the frequency of keys
    // as A[i] - reverse(A[i])
    Dictionary<int,
               int> u_map = new Dictionary<int,
                                           int>();

    // Stores count of desired pairs
    int pairs = 0;

    // Iterate the array A[]
    for(int i = 0; i < N; i++)
    {
        int val = A[i] - reverse(A[i]);

        // Add frequency of val
        // to the required answer
        if (u_map.ContainsKey(val))
            pairs += u_map[val];

        // Increment frequency of val
        if (u_map.ContainsKey(val))
            u_map[val]++;
        else
            u_map.Add(val, 1);
    }

    // Print the number of pairs
    Console.Write(pairs);
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 15, 11, 7 };
    int N = arr.Length;

    // Function Call
    countPairs(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the
// reverse of the number n
function reverse(n)
{
    var temp = n, rev = 0, r;

    // Iterate until temp is 0
    while (temp) {

        r = temp % 10;
        rev = rev * 10 + r;
        temp = parseInt(temp/10);
    }

    // Return the reversed number
    return rev;
}

// Function to count number of unique
// pairs (i, j) from the array A[]
// which satisfies the given condition
function countPairs(A, N)
{
    // Store the frequency of keys
    // as A[i] - reverse(A[i])
    var u_map = new Map();

    // Stores count of desired pairs
    var pairs = 0;

    // Iterate the array A[]
    for (var i = 0; i < N; i++) {

        var val = A[i] - reverse(A[i]);

        // Add frequency of val
        // to the required answer
        pairs += u_map.has(val)?u_map.get(val):0;

        // Increment frequency of val
        if(u_map.has(val))
            u_map.set(val, u_map.get(val)+1)
        else
            u_map.set(val, 1)
    }

    // Print the number of pairs
    document.write( pairs);
}

// Driver Code
var arr = [2, 15, 11, 7];
var N = arr.length;

// Function Call
countPairs(arr, N);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log M)，其中 **M** 是阵中* [*最大的元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*
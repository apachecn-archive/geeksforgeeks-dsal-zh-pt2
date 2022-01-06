# 对阵列中的{X，Y}对进行计数，使得 X ⊕ Y 中的设置位的计数和 X & Y 中的设置位的计数的两倍之和为 M

> 原文:[https://www . geeksforgeeks . org/数组中的对计数-x-y-x-y-x-y-is-m 中的集合位计数总和-% E2 % 8a % 95-y-y-is-m 中的集合位计数的两倍/](https://www.geeksforgeeks.org/count-of-pairs-x-y-from-an-array-such-that-sum-of-count-of-set-bits-in-x-%e2%8a%95-y-and-twice-the-count-of-set-bits-in-x-y-is-m/)

给定一个由 **N** 个非负整数和一个整数 **M** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找出满足条件**set bits(x⊕y)+2 * set bits(x&y)= m**的数组元素的无序对 **{X，Y}** 的计数，其中 **⊕** 表示[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和

****示例:****

> ****输入:** arr[] = {30，0，4，5 }，M = 2
> **输出:** 2
> **说明:**满足必要条件的对为{{3，0}，{0，5}}。**
> 
> ****输入:** arr[] = {1，2，3，4}，M = 3
> **输出:** 3
> **说明:**满足必要条件的对为{{1，3}，{2，3}，{3，4}}。**

****天真方法:**最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并对每个对检查必要条件是否满足。增加满足给定条件的对的计数，最后，打印对的计数。**

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)***

****高效方法:**上述方法可以基于以下观察进行优化:**

> ***   Bitwise XOR from the attribute of [:](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)
>     *   **七位元(a 85b)=七位元(a | b)-七位元(a & b)**
>     *   **七位元(a | b)=七位元(a)+七位元(b)─七位元(a & b)***   Therefore, the given equation becomes:
>     *   **(set bits(x | y)-set bits(x&y))+(2×set bits(x&y))= m**
>     *   **7 位(x)+7 位(y)─7 位(x&y)+(2×7 位(X & Y))= M**
>     *   **七位(X)+ = M***   Therefore, the task is simplified to count the element pairs whose sum of set bits is equal to **m.****

**按照以下步骤解决问题:**

*   **第一，[遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。**
*   **对于每个数组元素 **arr[i]，**更新 **arr[i]** ，其中存在设置位的[计数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)**。****
*   **现在[打印数组中总和等于 m 的对的计数](https://www.geeksforgeeks.org/count-pairs-with-given-sum/)**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number
// of setbits in the number n
int countsetbits(int n)
{
    // Stores the count of setbits
    int count = 0;

    // Iterate while N is
    // greater than 0
    while (n) {

        // Increment count by 1
        // if N is odd
        count += n & 1;

        // Right shift N
        n >>= 1;
    }

    // Return the count of set bits
    return (count);
}

// Function to find total count of
// given pairs satisfying the equation
int countPairs(int a[], int N, int M)
{

    for (int i = 0; i < N; i++) {

        // Update arr[i] with the count
        // of set bits of arr[i]
        a[i] = countsetbits(a[i]);
    }

    // Stores the frequency
    // of each array element
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Increment the count
        // of arr[i] in mp
        mp[a[i]]++;
    }

    // Stores the total count of pairs
    int count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Increment count by mp[M - a[i]]
        count += mp[M - a[i]];

        // If a[i] is equal to M-a[i]
        if (a[i] == M - a[i]) {

            // Decrement count by 1
            count--;
        }
    }

    // Return count/2
    return (count / 2);
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 3, 0, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 2;

    cout << countPairs(arr, N, M);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to count number
// of setbits in the number n
static int countsetbits(int n)
{

    // Stores the count of setbits
    int count = 0;

    // Iterate while N is
    // greater than 0
    while (n != 0)
    {

        // Increment count by 1
        // if N is odd
        count += n & 1;

        // Right shift N
        n >>= 1;
    }

    // Return the count of set bits
    return (count);
}

// Function to find total count of
// given pairs satisfying the equation
static int countPairs(int[] a, int N, int M)
{
    for(int i = 0; i < N; i++)
    {

        // Update arr[i] with the count
        // of set bits of arr[i]
        a[i] = countsetbits(a[i]);
    }

    // Stores the frequency
    // of each array element
     HashMap<Integer,
             Integer> mp = new HashMap<Integer,
                                       Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        if (mp.containsKey(a[i]))
        {
            mp.put(a[i], mp.get(a[i]) + 1);
        }
        else
        {
            mp.put(a[i], 1);
        }
    }

    // Stores the total count of pairs
    int count = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Increment count by mp[M - a[i]]
        count += mp.get(M - a[i]);

        // If a[i] is equal to M-a[i]
        if (a[i] == M - a[i])
        {

            // Decrement count by 1
            count--;
        }
    }

    // Return count/2
    return (count / 2);
}   

// Driver Code
public static void main(String[] args)
{

    // Input
    int[] arr = { 3, 0, 4, 5 };
    int N = arr.length;
    int M = 2;

    System.out.println(countPairs(arr, N, M));
}
}

// This code is contributed by avijitmondal1998
```

## **蟒蛇 3**

```
# Python3 Program for the above approach

# Function to count number
# of setbits in the number n
def  countSetBits(n):

    # Stores the count of setbits
    count = 0

    # Iterate while N is
    # greater than 0
    while (n):

        # Increment count by 1
        # if N is odd
        count += n & 1

        # Right shift N
        n >>= 1

    # Return the count of set bits
    return count

def countPairs(arr, N, M):
    for i in range(0, N):

        # Update arr[i] with the count
        # of set bits of arr[i]
        arr[i] = countSetBits(arr[i])

    # Store counts of all elements in a dictionary
    mp = {}
    for i in range(0, N):
        if arr[i] in mp:
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1
    twice_count = 0

    # Iterate through each element and increment
    # the count (Notice that every pair is
    # counted twice)
    for i in range(0, N):
        if M - arr[i] in mp.keys():
            twice_count += mp[M - arr[i]]

        # if (arr[i], arr[i]) pair satisfies the
        # condition, then we need to ensure that
        # the count is  decreased by one such
        # that the (arr[i], arr[i]) pair is not
        # considered
        if (M - arr[i] == arr[i]):
            twice_count -= 1

    # return the half of twice_count
    return int(twice_count / 2)

# Driver code
# Input
arr = [ 3, 0, 4, 5]
N = len(arr)
M = 2
print(countPairs(arr, N, M))

# This cose is contributed by santhoshcharan.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count number
// of setbits in the number n
static int countsetbits(int n)
{

    // Stores the count of setbits
    int count = 0;

    // Iterate while N is
    // greater than 0
    while (n != 0)
    {

        // Increment count by 1
        // if N is odd
        count += n & 1;

        // Right shift N
        n >>= 1;
    }

    // Return the count of set bits
    return (count);
}

// Function to find total count of
// given pairs satisfying the equation
static int countPairs(int[] a, int N, int M)
{
    for(int i = 0; i < N; i++)
    {

        // Update arr[i] with the count
        // of set bits of arr[i]
        a[i] = countsetbits(a[i]);
    }

    // Stores the frequency
    // of each array element
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse the array
    for(int i = 0; i < N; ++i)
    {

        // Update frequency of
        // each array element
        if (mp.ContainsKey(a[i]) == true)
            mp[a[i]] += 1;
        else
            mp[a[i]] = 1;
    }

    // Stores the total count of pairs
    int count = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Increment count by mp[M - a[i]]
        count += mp[M - a[i]];

        // If a[i] is equal to M-a[i]
        if (a[i] == M - a[i])
        {

            // Decrement count by 1
            count--;
        }
    }

    // Return count/2
    return (count / 2);
}

// Driver Code
static public void Main()
{

    // Input
    int[] arr = { 3, 0, 4, 5 };
    int N = arr.Length;
    int M = 2;

    Console.WriteLine(countPairs(arr, N, M));
}
}

// This code is contributed by sanjoy_62
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to count number
// of setbits in the number n
function countsetbits(n)
{
    // Stores the count of setbits
    var count = 0;

    // Iterate while N is
    // greater than 0
    while (n) {

        // Increment count by 1
        // if N is odd
        count += n & 1;

        // Right shift N
        n >>= 1;
    }

    // Return the count of set bits
    return (count);
}

// Function to find total count of
// given pairs satisfying the equation
function countPairs(a, N, M)
{

    for (var i = 0; i < N; i++) {

        // Update arr[i] with the count
        // of set bits of arr[i]
        a[i] = countsetbits(a[i]);
    }

    // Stores the frequency
    // of each array element
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Increment the count
        // of arr[i] in mp
        if(mp.has(a[i]))
            mp.set(a[i], mp.get(a[i])+1)
        else
            mp.set(a[i], 1)
    }

    // Stores the total count of pairs
    var count = 0;

    // Traverse the array arr[]
    for (var i = 0; i < N; i++) {

        // Increment count by mp[M - a[i]]
        count += mp.get(M - a[i]);

        // If a[i] is equal to M-a[i]
        if (a[i] == M - a[i]) {

            // Decrement count by 1
            count--;
        }
    }

    // Return count/2
    return (count / 2);
}

// Driver Code
// Input
var arr = [3, 0, 4, 5];
var N = arr.length;
var M = 2;
document.write( countPairs(arr, N, M));

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**
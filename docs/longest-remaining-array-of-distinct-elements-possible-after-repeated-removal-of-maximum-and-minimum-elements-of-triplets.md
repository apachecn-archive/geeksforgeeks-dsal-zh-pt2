# 重复删除三元组的最大和最小元素后，可能剩余最长的不同元素数组

> 原文:[https://www . geeksforgeeks . org/最长剩余不同元素数组-重复删除三元组中的最大和最小元素后可能出现的情况/](https://www.geeksforgeeks.org/longest-remaining-array-of-distinct-elements-possible-after-repeated-removal-of-maximum-and-minimum-elements-of-triplets/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**，任务是在每次操作中重复选择三元组并从三元组中移除最大和最小元素，使得剩余的数组具有最长的可能长度，并且只由不同的元素组成。

**示例:**

> **输入:** N = 5，arr[] = {1，2，1，3，7} <
> **输出:** 3
> **解释:**选择三元组(1，2，1)并移除 1 和 2。剩下的数组是[1，3，7]，其中所有元素成对不同。
> 
> **输入:** N = 6，arr[] = {8，8，8，9，9，9 }
> T3】输出: 2

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，计算每个数组元素的频率。
*   对于每个不同的元素，检查其频率是偶数还是奇数，并相应地执行以下操作:
    *   **如果频率为奇数(除 1 外):**
        *   通过在三元组中选择相同的元素，在每个操作中移除 2 个元素。在一系列操作之后，将只保留元素的一次出现。
    *   **如果频率为偶数(除 2 外):**
        *   通过在三元组中选择相同的值，在每个操作中删除 2 个元素。在一系列操作之后，该元素将只保留两次出现
        *   现在，初始化一个变量，比如 **cnt** ，来存储所有偶数频繁数组元素的计数。
        *   如果 **cnt** 是偶数，那么使所有偶数元素唯一，而不通过仅从偶数频繁元素中选择三元组来从数组中移除任何唯一元素。
        *   否则，移除 1 个唯一元素以使数组成对不同。

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return length of longest
// remaining array of pairwise distinct
// array possible by removing triplets
int maxUniqueElements(int A[], int N)
{
    // Stores the frequency of array elements
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        mp[A[i]]++;
    }

    // Iterate through the map
    int cnt = 0;

    for (auto x : mp) {

        // If frequency of current
        // element is even
        if (x.second % 2 == 0) {
            cnt++;
        }
    }

    // Stores the required count
    // of unique elements remaining
    int ans = mp.size();

    // If count is odd
    if (cnt % 2 == 1) {
        ans--;
    }
    return ans;
}

// Driver Code
int main()
{
    int N = 5;
    int A[] = { 1, 2, 1, 3, 7 };
    cout << maxUniqueElements(A, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to return length of longest
    // remaining array of pairwise distinct
    // array possible by removing triplets
    static int maxUniqueElements(int[] Arr, int N)
    {

        // Stores the frequency of array elements
        HashMap<Integer, Integer> mp = new HashMap<>();

        // Traverse the array
        for (int i = 0; i < N; i++) {
            if (mp.containsKey(Arr[i])) {
                mp.put(Arr[i], mp.get(Arr[i]) + 1);
            }
            else {
                mp.put(Arr[i], 1);
            }
        }

        // Iterate through the map
        int cnt = 0;

        for (Map.Entry<Integer, Integer> entry :
             mp.entrySet()) {

            // If frequency of current
            // element is even
            if ((entry.getValue()) % 2 == 0) {
                cnt++;
            }
        }

        // Stores the required count
        // of unique elements remaining
        int ans = mp.size();

        // If count is odd
        if (cnt % 2 == 1) {
            ans--;
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 5;
        int A[] = { 1, 2, 1, 3, 7 };
        System.out.println(maxUniqueElements(A, N));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to return length of longest
# remaining array of pairwise distinct
# array possible by removing triplets
def maxUniqueElements(A, N):
    # Stores the frequency of array elements
    mp  = {}

    # Traverse the array
    for i in range(N):
        if A[i] in mp:
            mp[A[i]] += 1
        else:
            mp[A[i]] = 1

    # Iterate through the map
    cnt = 0

    for key,value in mp.items():
        # If frequency of current
        # element is even
        if (value % 2 == 0):
            cnt += 1

    # Stores the required count
    # of unique elements remaining
    ans = len(mp)

    # If count is odd
    if (cnt % 2 == 1):
        ans -= 1
    return ans

# Driver Code
if __name__ == '__main__':
    N = 5
    A = [1, 2, 1, 3, 7]
    print(maxUniqueElements(A, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to return length of longest
    // remaining array of pairwise distinct
    // array possible by removing triplets
    static int maxUniqueElements(int[] Arr, int N)
    {

        // Stores the frequency of array elements
        Dictionary<int, int> mp
            = new Dictionary<int, int>();

        // Traverse the array
        for (int i = 0; i < N; i++) {
            if (mp.ContainsKey(Arr[i])) {
                mp[Arr[i]] += 1;
            }
            else {
                mp[Arr[i]] = 1;
            }
        }

        // Iterate through the map
        int cnt = 0;

        foreach(KeyValuePair<int, int> entry in mp)
        {

            // If frequency of current
            // element is even
            if ((entry.Value) % 2 == 0) {
                cnt++;
            }
        }

        // Stores the required count
        // of unique elements remaining
        int ans = mp.Count;

        // If count is odd
        if (cnt % 2 == 1) {
            ans--;
        }
        return ans;
    }

    // Driver Code
    public static void Main(string[] args)
    {

        int N = 5;
        int[] A = { 1, 2, 1, 3, 7 };
        Console.Write(maxUniqueElements(A, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to return length of longest
// remaining array of pairwise distinct
// array possible by removing triplets
function maxUniqueElements(A, N)
{

    // Stores the frequency of array elements
    let mp = new Map();

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        if (mp.has(A[i]))
        {
            mp.set(mp.get(A[i]), mp.get(A[i]) + 1);
        }
        else
        {
            mp.set(A[i], 1);
        }
    }

    // Iterate through the map
    let cnt = 0;

    for(let [key, value] of mp)
    {

        // If frequency of current
        // element is even
        if (value % 2 == 0)
        {
            cnt++;
        }
    }

    // Stores the required count
    // of unique elements remaining
    let ans = mp.size;

    // If count is odd
    if (cnt % 2 == 1)
    {
        ans--;
    }
    return ans;
}

// Driver Code
let N = 5;
let A = [ 1, 2, 1, 3, 7 ];

document.write(maxUniqueElements(A, N));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
3
```
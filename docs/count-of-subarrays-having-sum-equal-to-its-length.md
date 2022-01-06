# 总和等于其长度的子阵列的计数

> 原文:[https://www . geeksforgeeks . org/子阵列计数-总和等于其长度/](https://www.geeksforgeeks.org/count-of-subarrays-having-sum-equal-to-its-length/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到子阵列的[数量，其元素之和](https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/)等于其中的元素数量。

**示例:**

> **输入** : N = 3，arr[] = {1，0，2}
> **输出:** 3
> **说明:**
> 子阵总数为 6，即{1}、{0}、{2}、{1，0}、{0，2}、{1，0}、{1，0，2}。
> 在 6 个子阵列中，只有 3 个子阵列的元素数量等于其元素的总和，即
> 1) {1}，总和= 1，长度= 1。
> 2) {0，2}，sum = 2，length = 2。
> 3) {1，0，2}，和= 3，长= 3。
> 
> **输入:** N = 3，arr[] = {1，1，0}
> **输出:** 3
> **说明:**
> 子阵总数为 6，即{1}、{1}、{0}、{1，1}、{1，0}、{1，1，0}、{1，1，0}。
> 在 6 个子阵列中，只有 3 个子阵列的元素数量等于其元素的总和，即
> 1) {1}，总和= 1，长度= 1。
> 2) {1}，总和= 1，长度= 1。
> 3) {1，1}，总和= 2，长度= 2。

**天真的方法:**想法是[生成阵列的所有子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，如果子阵列的元素之和等于其中的元素数量，那么计算这个子阵列。检查所有子阵列后打印计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效途径:**这个问题可以通过观察转化为更简单的问题。如果数组的所有**元素递减 1** ，那么数组 arr[ ]的所有子数组的和等于其元素数，这与在新数组中找到的总和为 0 的子数组的[数量相同(通过将 arr[]的所有元素递减 1 而形成)。以下是步骤:](https://www.geeksforgeeks.org/print-all-subarrays-with-0-sum/)

1.  将所有数组元素减 1。
2.  用**前缀【0】= arr【0】**初始化前缀数组。
3.  [从左到右遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，从索引 1 开始，将一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)更新为 **pref[i] = pref[i-1] + arr[i]** 。
4.  将**答案**初始化为 0。
5.  从左到右迭代前缀数组 **pref[]** ，并在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中按当前元素的值递增答案。
6.  增加地图中当前元素的值。
7.  完成上述步骤后，打印**答案**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the subarrays
// with sum of its elements as its length
int countOfSubarray(int arr[], int N)
{
    // Decrementing all the elements
    // of the array by 1
    for (int i = 0; i < N; i++)
        arr[i]--;

    // Making prefix sum array
    int pref[N];
    pref[0] = arr[0];

    for (int i = 1; i < N; i++)
        pref[i] = pref[i - 1] + arr[i];

    // Declare map to store count of
    // elements upto current element
    map<int, int> mp;
    int answer = 0;

    // To count all the subarrays
    // whose prefix sum is 0
    mp[0]++;

    // Iterate the array
    for (int i = 0; i < N; i++) {

        // Increment answer by count of
        // current element of prefix array
        answer += mp[pref[i]];
        mp[pref[i]]++;
    }

    // Return the answer
    return answer;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 1, 0 };
    int N = sizeof arr / sizeof arr[0];

    // Function call
    cout << countOfSubarray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function that counts the subarrays
// with sum of its elements as its length
static int countOfSubarray(int arr[], int N)
{
    // Decrementing all the elements
    // of the array by 1
    for (int i = 0; i < N; i++)
        arr[i]--;

    // Making prefix sum array
    int []pref = new int[N];
    pref[0] = arr[0];

    for (int i = 1; i < N; i++)
        pref[i] = pref[i - 1] + arr[i];

    // Declare map to store count of
    // elements upto current element
    HashMap<Integer,
              Integer> mp = new HashMap<Integer,
                                        Integer>();
    int answer = 0;

    // To count all the subarrays
    // whose prefix sum is 0
    mp.put(0, 1);

    // Iterate the array
    for (int i = 0; i < N; i++)
    {

        // Increment answer by count of
        // current element of prefix array

        if(mp.containsKey(pref[i]))
        {
            answer += mp.get(pref[i]);
            mp.put(pref[i], mp.get(pref[i]) + 1);

        }
        else
        {
            mp.put(pref[i], 1);
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 1, 1, 0 };
    int N = arr.length;

    // Function call
    System.out.print(countOfSubarray(arr, N));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function that counts the subarrays
# with sum of its elements as its length
def countOfSubarray(arr, N):

    # Decrementing all the elements
    # of the array by 1
    for i in range(N):
        arr[i] -= 1

    # Making prefix sum array
    pref = [0] * N
    pref[0] = arr[0]

    for i in range(1, N):
        pref[i] = pref[i - 1] + arr[i]

    # Declare map to store count of
    # elements upto current element
    mp = defaultdict(lambda : 0)
    answer = 0

    # To count all the subarrays
    # whose prefix sum is 0
    mp[0] += 1

    # Iterate the array
    for i in range(N):

        # Increment answer by count of
        # current element of prefix array
        answer += mp[pref[i]]
        mp[pref[i]] += 1

    # Return the answer
    return answer

# Driver Code

# Given array arr[]
arr = [ 1, 1, 0 ]
N = len(arr)

# Function call
print(countOfSubarray(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that counts the subarrays
// with sum of its elements as its length
static int countOfSubarray(int []arr, int N)
{
    // Decrementing all the elements
    // of the array by 1
    for (int i = 0; i < N; i++)
        arr[i]--;

    // Making prefix sum array
    int []pref = new int[N];
    pref[0] = arr[0];

    for (int i = 1; i < N; i++)
        pref[i] = pref[i - 1] + arr[i];

    // Declare map to store count of
    // elements upto current element
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    int answer = 0;

    // To count all the subarrays
    // whose prefix sum is 0
    mp.Add(0, 1);

    // Iterate the array
    for (int i = 0; i < N; i++)
    {

        // Increment answer by count of
        // current element of prefix array

        if(mp.ContainsKey(pref[i]))
        {
            answer += mp[pref[i]];
            mp[pref[i]]= mp[pref[i]] + 1;   
        }
        else
        {
            mp.Add(pref[i], 1);
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int []arr = { 1, 1, 0 };
    int N = arr.Length;

    // Function call
    Console.Write(countOfSubarray(arr, N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Js program for the above approach

// Function that counts the subarrays
// with sum of its elements as its length
function countOfSubarray( arr, N){
    // Decrementing all the elements
    // of the array by 1
    for (let i = 0; i < N; i++)
        arr[i]--;

    // Making prefix sum array
    let pref = [];
    pref[0] = arr[0];

    for (let i = 1; i < N; i++)
        pref[i] = pref[i - 1] + arr[i];

    // Declare map to store count of
    // elements upto current element
    let mp = new Map;
    let answer = 0;

    // To count all the subarrays
    // whose prefix sum is 0
    if(mp[0])
    mp[0]++;
    else
    mp[0] = 1;

    // Iterate the array
    for (let i = 0; i < N; i++) {
        // Increment answer by count of
        // current element of prefix array
        if(mp[pref[i]]){
        answer += mp[pref[i]];
        mp[pref[i]]++;
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
// Given array arr[]
let arr = [ 1, 1, 0 ];
let N = arr.length;
// Function call
document.write(countOfSubarray(arr, N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * Log(N))*
***辅助空间:** O(N)*
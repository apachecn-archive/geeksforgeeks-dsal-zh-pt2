# 从一个其“与”和“异或”之和等于 K 的数组中计数对

> 原文:[https://www . geeksforgeeks . org/从一个数组中计数对，该数组有两次等于 k 的和/异或/](https://www.geeksforgeeks.org/count-pairs-from-an-array-having-sum-of-twice-of-their-and-and-xor-equal-to-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是计算满足等式**2 *(arr[I]&arr[j])+(arr[I]^ arr[j])= k .**

**示例:**

> **输入:** arr[] = {1，5，4，8，7}，K = 9
> **输出:** 2
> **解释:**
> 
> 1.  索引 0 和 3 处的元素，即 arr[i] = 1，arr[j] = 8，满足给定的等式。
> 2.  索引 1 和 2 处的元素，即 arr[i] = 5，arr[j] = 4，满足给定的等式。
> 
> **输入:** arr[] = {1，2，2，4，5}，K = 3
> T3】输出: 2

**天真方法:**最简单的方法是[从数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并针对每一对，检查该对是否满足给定的等式。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> ***观察:***
> 
> *A + B = (A ^ B) + 2 * (A & B)*
> 
> *计算和时，如果两个位都是 **1** (即 AND 为 1)，则合成位是 **0** ，加上 **1** 作为进位，这意味着**和**中的每个位都是* [*左移*](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)*1，即**和**的值乘以 **2***
> 
> 因此，A + B =给定的方程。
> 
> *因此，这验证了上述观察。*

按照以下步骤解决问题:

*   问题现在简化为[两个和问题](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/)，任务简化为计算和等于 **K.** 的对
*   初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如说 **mp** ，和一个变量，比如说 **cnt** ，来计算满足给定条件的对的数量。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素:
    *   如果**MP[K–arr[I]]**不为零，则将其值添加到 **cnt** 中。
    *   更新**地图**中**arr【I】**的频率。
*   打印 **cnt** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of pairs
// satisfying the given conditions
void countPairs(int arr[], int N, int K)
{
    // Stores the frequency of array elements
    unordered_map<int, int> mp;

    // Stores the total number of pairs
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Add it to cnt
        cnt += mp[K - arr[i]];

        // Update frequency of
        // current array element
        mp[arr[i]]++;
    }

    // Print the count
    cout << cnt;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 5, 4, 8, 7 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of K
    int K = 9;

    countPairs(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

    // Function to count number of pairs
    // satisfying the given conditions
    static void countPairs(int arr[], int N, int K)
    {

        // Stores the frequency of array elements
        Map<Integer, Integer> mp = new HashMap<>();

        // Stores the total number of pairs
        int cnt = 0;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Add it to cnt
            if (mp.get(K - arr[i]) != null)
                cnt += mp.get(K - arr[i]);

            // Update frequency of
            // current array element
            mp.put(arr[i], mp.get(arr[i]) == null
                               ? 1
                               : mp.get(arr[i]) + 1);
        }

        // Print the count
        System.out.println(cnt);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int arr[] = { 1, 5, 4, 8, 7 };

        // Size of the array
        int N = arr.length;

        // Given value of K
        int K = 9;

        countPairs(arr, N, K);
    }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function to count number of pairs
# satisfying the given conditions
def countPairs(arr, N, K) :

    # Stores the frequency of array elements
    mp = defaultdict(int)

    # Stores the total number of pairs
    cnt = 0

    # Traverse the array
    for i in range(N):

        # Add it to cnt
        cnt += mp[K - arr[i]]

        # Update frequency of
        # current array element
        mp[arr[i]] += 1

    # Print the count
    print(cnt)

# Driver Code
# Given array
arr = [ 1, 5, 4, 8, 7 ]

# Size of the array
N = len(arr)

# Given value of K
K = 9
countPairs(arr, N, K)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

    // Function to count number of pairs
    // satisfying the given conditions
    static void countPairs(int[] arr, int N, int K)
    {

        // Stores the frequency of array elements
        Dictionary<int, int> mp
            = new Dictionary<int, int>();

        // Stores the total number of pairs
        int cnt = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Add it to cnt
            if (mp.ContainsKey(K - arr[i]))
                cnt += mp[K - arr[i]];

            // Update frequency of
            // current array element
            if (mp.ContainsKey(arr[i])) {

                var val = mp[arr[i]];
                mp.Remove(arr[i]);
                mp.Add(arr[i], val + 1);
            }
            else {

                mp.Add(arr[i], 1);
            }
        }

        // Print the count
        Console.WriteLine(cnt);
    }

    // Driver Code
    static public void Main()
    {

        // Given array
        int[] arr = { 1, 5, 4, 8, 7 };

        // Size of the array
        int N = arr.Length;

        // Given value of K
        int K = 9;
        countPairs(arr, N, K);
    }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach
    // Function to count number of pairs
    // satisfying the given conditions
    function countPairs(arr,N,K)
    {
        // Stores the frequency of array elements
        let mp = new Map();

        // Stores the total number of pairs
        let cnt = 0;

        // Traverse the array
        for (let i = 0; i < N; i++) {

            // Add it to cnt
            if(mp.has(K - arr[i]))
            {
                cnt += mp.get(K - arr[i]);
            }

            // Update frequency of
            // current array element
            if(mp.has(arr[i]))
            {
                mp.set(arr[i], mp.get(arr[i]) + 1);
            }
            else{
                mp.set(arr[i], 1);
            }
        }

        // Print the count
        document.write(cnt);
    }

    // Driver Code

    // Given array
    let arr = [ 1, 5, 4, 8, 7 ];

    // Size of the array
    let N = arr.length;

    // Given value of K
    let K = 9;

    countPairs(arr, N, K);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
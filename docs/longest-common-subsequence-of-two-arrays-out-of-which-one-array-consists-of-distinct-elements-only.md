# 两个数组中最长的公共子序列，其中一个数组仅由不同的元素组成

> 原文:[https://www . geesforgeks . org/两个数组中最长的公共子序列-其中一个数组仅由不同的元素组成/](https://www.geeksforgeeks.org/longest-common-subsequence-of-two-arrays-out-of-which-one-array-consists-of-distinct-elements-only/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **firstArr[]** ，仅由不同的元素组成，以及**secondar[]**，任务是找出这两个数组之间 [LCS](https://www.geeksforgeeks.org/longest-common-subsequence/) 的长度。

**示例:**

> **输入:** firstArr[] = {3，5，1，8}，secondar[]= { 3，3，5，3，8 }
> T3】输出: 3。
> **说明:**这两个数组之间的 LCS 是{3，5，8}。
> 
> **输入** : firstArr[] = {1，2，1}、second[]=
> **输出:** 0

**天真方法:**按照以下步骤，用最简单的方法解决问题:

*   初始化数组 **dp[][]** ，使得 **dp[i][j]** 存储**第一个 Arr[ :i]** 和**第二个**的[最长公共子序列](https://www.geeksforgeeks.org/printing-longest-common-subsequence/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **firstArr[]** 对于数组的每个数组元素 **firstArr[]** ，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**secondar[]**。
*   **如果 first arr[I]= second[j]:**set**DP[I][j]= DP[I–1][j–1]+1**。
*   **否则:**设置 **dp[i][j] =最大值(DP[I–1][j]，DP[I][j–1])**。

***时间复杂度:** O(N * M)，其中 N 和 M 分别是数组 firstArr[]和 secondArr 的大小。*
***辅助空间:** O(N * M)*

**高效方法:**要优化上述方法，请执行以下步骤:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说 **mp** ，来存储映射**映射【first arr[I]】= I**，即将第一个数组的元素映射到它们各自的索引。
*   由于存在于**次要元素[]** 中但不存在于**第一个元素[]** 中的元素根本没有用，因为它们永远不可能是公共子序列的一部分，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **次要元素[]** ，对于每个数组元素，[检查它是否存在于**映射**中。](https://www.geeksforgeeks.org/check-key-present-cpp-map-unordered_map/)
*   如果发现是真的，[将](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) **地图【次级【I】】**推至临时阵中。否则忽略它。
*   找到获得的临时数组的[最长递增子序列(LIS)](https://www.geeksforgeeks.org/longest-increasing-subsequence/) ，并将其长度打印为所需答案。

插图:

> firstArr[] = {3，5，1，8 }
> secondar = { 3，3，4，5，3，8}
> **映射** : 3- > 0，5- > 1，1- > 2，8->3(From first arr)
> **tempArr[]**= {0，0，1，0，3}
> 因此，tempArr[] = 3 的 LIS 长度({ 0，1，3})

下面是上述方法的实现:

## C++

```
// C++ program to to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the Longest Common
// Subsequence between the two arrays
int LCS(vector<int>& firstArr,
        vector<int>& secondArr)
{

    // Maps elements of firstArr[]
    // to their respective indices
    unordered_map<int, int> mp;

    // Traverse the array firstArr[]
    for (int i = 0; i < firstArr.size(); i++) {
        mp[firstArr[i]] = i + 1;
    }

    // Stores the indices of common elements
    // between firstArr[] and secondArr[]
    vector<int> tempArr;

    // Traverse the array secondArr[]
    for (int i = 0; i < secondArr.size(); i++) {

        // If current element exists in the Map
        if (mp.find(secondArr[i]) != mp.end()) {

            tempArr.push_back(mp[secondArr[i]]);
        }
    }

    // Stores lIS from tempArr[]
    vector<int> tail;

    tail.push_back(tempArr[0]);

    for (int i = 1; i < tempArr.size(); i++) {

        if (tempArr[i] > tail.back())
            tail.push_back(tempArr[i]);

        else if (tempArr[i] < tail[0])
            tail[0] = tempArr[i];

        else {
            auto it = lower_bound(tail.begin(),
                                  tail.end(),
                                  tempArr[i]);
            *it = tempArr[i];
        }
    }
    return (int)tail.size();
}

// Driver Code
int main()
{
    vector<int> firstArr = { 3, 5, 1, 8 };
    vector<int> secondArr = { 3, 3, 5, 3, 8 };
    cout << LCS(firstArr, secondArr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find the Longest Common
// Subsequence between the two arrays
static int LCS(int[] firstArr,int[] secondArr)
{

    // Maps elements of firstArr[]
    // to their respective indices
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Traverse the array firstArr[]
    for (int i = 0; i < firstArr.length; i++)
    {
        mp.put(firstArr[i], i + 1); 
    }

    // Stores the indices of common elements
    // between firstArr[] and secondArr[]
    Vector<Integer> tempArr = new Vector<>();

    // Traverse the array secondArr[]
    for (int i = 0; i < secondArr.length; i++)
    {

        // If current element exists in the Map
        if (mp.containsKey(secondArr[i]))
        {
            tempArr.add(mp.get(secondArr[i]));
        }
    }

    // Stores lIS from tempArr[]
    Vector<Integer> tail = new Vector<>();
    tail.add(tempArr.get(0));

    for (int i = 1; i < tempArr.size(); i++)
    {
        if (tempArr.get(i) > tail.lastElement())
            tail.add(tempArr.get(i));
        else if (tempArr.get(i) < tail.get(0))
            tail.add(0, tempArr.get(i));     
    }
    return (int)tail.size();
}

// Driver Code
public static void main(String[] args)
{
    int[] firstArr = { 3, 5, 1, 8 };
    int[] secondArr = { 3, 3, 5, 3, 8 };
    System.out.print(LCS(firstArr, secondArr));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to to implement
# the above approach
from bisect import bisect_left

# Function to find the Longest Common
# Subsequence between the two arrays
def LCS(firstArr, secondArr):

    # Maps elements of firstArr[]
    # to their respective indices
    mp = {}

    # Traverse the array firstArr[]
    for i in range(len(firstArr)):
        mp[firstArr[i]] = i + 1

    # Stores the indices of common elements
    # between firstArr[] and secondArr[]
    tempArr = []

    # Traverse the array secondArr[]
    for i in range(len(secondArr)):

        # If current element exists in the Map
        if (secondArr[i] in  mp):
            tempArr.append(mp[secondArr[i]])

    # Stores lIS from tempArr[]
    tail = []
    tail.append(tempArr[0])
    for i in range(1, len(tempArr)):
        if (tempArr[i] > tail[-1]):
            tail.append(tempArr[i])
        elif (tempArr[i] < tail[0]):
            tail[0] = tempArr[i]
        else :
            it = bisect_left(tail, tempArr[i])
            it = tempArr[i]
    return len(tail)

# Driver Code
if __name__ == '__main__':
    firstArr = [3, 5, 1, 8 ]
    secondArr = [3, 3, 5, 3, 8 ]
    print (LCS(firstArr, secondArr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to to implement
// the above approach
using System;
using System.Collections.Generic;
public class GFG
{

// Function to find the longest Common
// Subsequence between the two arrays
static int LCS(int[] firstArr,int[] secondArr)
{

    // Maps elements of firstArr[]
    // to their respective indices
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Traverse the array firstArr[]
    for (int i = 0; i < firstArr.Length; i++)
    {
        mp.Add(firstArr[i], i + 1); 
    }

    // Stores the indices of common elements
    // between firstArr[] and secondArr[]
    List<int> tempArr = new List<int>();

    // Traverse the array secondArr[]
    for (int i = 0; i < secondArr.Length; i++)
    {

        // If current element exists in the Map
        if (mp.ContainsKey(secondArr[i]))
        {
            tempArr.Add(mp[secondArr[i]]);
        }
    }

    // Stores lIS from tempArr[]
    List<int> tail = new List<int>();
    tail.Add(tempArr[0]);

    for (int i = 1; i < tempArr.Count; i++)
    {
        if (tempArr[i] > tail[tail.Count-1])
            tail.Add(tempArr[i]);
        else if (tempArr[i] < tail[0])
            tail.Insert(0, tempArr[i]);     
    }
    return (int)tail.Count;
}

// Driver Code
public static void Main(String[] args)
{
    int[] firstArr = { 3, 5, 1, 8 };
    int[] secondArr = { 3, 3, 5, 3, 8 };
    Console.Write(LCS(firstArr, secondArr));
}
}

// This code is contributed by Rajput-Ji.
```

## java 描述语言

```
<script>

// Javascript program to to implement
// the above approach

// Function to find the longest Common
// Subsequence between the two arrays
function LCS(firstArr, secondArr)
{

    // Maps elements of firstArr[]
    // to their respective indices
    let mp = new Map()

    // Traverse the array firstArr[]
    for(let i = 0; i < firstArr.length; i++)
    {
        mp.set(firstArr[i], i + 1);
    }

    // Stores the indices of common elements
    // between firstArr[] and secondArr[]
    let tempArr = [];

    // Traverse the array secondArr[]
    for(let i = 0; i < secondArr.length; i++)
    {

        // If current element exists in the Map
        if (mp.has(secondArr[i]))
        {
            tempArr.push(mp.get(secondArr[i]));
        }
    }

    // Stores lIS from tempArr[]
    let tail = [];
    tail.push(tempArr[0]);

    for(let i = 1; i < tempArr.length; i++)
    {
        if (tempArr[i] > tail[tail.length - 1])
            tail.push(tempArr[i]);

        else if (tempArr[i] < tail[0])
            tail.unshift(0, tempArr[i]);   
    }
    return tail.length;
}

// Driver Code
let firstArr = [ 3, 5, 1, 8 ];
let secondArr = [ 3, 3, 5, 3, 8 ];

document.write(LCS(firstArr, secondArr));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*
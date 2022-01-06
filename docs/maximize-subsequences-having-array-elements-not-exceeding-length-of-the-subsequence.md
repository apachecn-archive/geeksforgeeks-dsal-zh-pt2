# 最大化数组元素不超过子序列长度的子序列

> 原文:[https://www . geeksforgeeks . org/maximize-子序列-具有数组元素-不超过子序列长度/](https://www.geeksforgeeks.org/maximize-subsequences-having-array-elements-not-exceeding-length-of-the-subsequence/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是最大化从数组中获得的子序列的数量，使得作为任何子序列一部分的每个元素**arr【I】**不超过该子序列的长度。

**示例:**

> **输入:** arr[] = {1，1，1，1}
> **输出:** 4
> **解释:**
> 形成满足给定条件{1}、{1}、{1}、{1}的 4 个子序列 1。
> 
> **输入:** arr[] = {2，2，3，1，2，1}
> **输出:** 3
> **解释:**
> 可能的组是{1}、{1}、{2，2}
> 所以，输出是 3。

**进场:**思路是用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题。按照以下步骤解决问题:

1.  初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)到[存储每个数组元素](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)的频率。
2.  初始化一个变量，比如说**计数**到 0，以存储获得的子序列总数。
3.  记录要添加的元素数量。
4.  现在，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并计算特定组中可以包含的元素数量。
5.  继续在有效子序列上添加元素。
6.  完成上述步骤后，打印子序列的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number
// of subsequences that can be formed
int No_Of_subsequences(map<int, int> mp)
{
    // Stores the number of subsequences
    int count = 0;
    int left = 0;

    // Iterate over the map
    for (auto x : mp) {

        x.second += left;

        // Count the number of subsequences
        // that can be formed from x.first
        count += (x.second / x.first);

        // Number of occurrences of
        // x.first which are left
        left = x.second % x.first;
    }

    // Return the number of subsequences
    return count;
}

// Function to create the maximum count
// of subsequences that can be formed
void maximumsubsequences(int arr[], int n)
{
    // Stores the frequency of arr[]
    map<int, int> mp;

    // Update the frequency
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // Print the number of subsequences
    cout << No_Of_subsequences(mp);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 1, 1, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maximumsubsequences(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate the number
// of subsequences that can be formed
public static int No_Of_subsequences(HashMap<Integer,
                                             Integer> mp)
{

    // Stores the number of subsequences
    int count = 0;
    int left = 0;

    // Iterate over the map
    for(Map.Entry<Integer, Integer> x : mp.entrySet())
    {
        mp.replace(x.getKey(), x.getValue() + left);

        // Count the number of subsequences
        // that can be formed from x.first
        count += (x.getValue() / x.getKey());

        // Number of occurrences of
        // x.first which are left
        left = x.getValue() % x.getKey();
    }

    // Return the number of subsequences
    return count;
}

// Function to create the maximum count
// of subsequences that can be formed
public static void maximumsubsequences(int[] arr,
                                       int n)
{

    // Stores the frequency of arr[]
    HashMap<Integer, Integer> mp = new HashMap<>();

    // Update the frequency
    for(int i = 0; i < n; i++)
    {
        if (mp.containsKey(arr[i]))
        {
            mp.replace(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    // Print the number of subsequences
    System.out.println(No_Of_subsequences(mp));
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 1, 1, 1 };

    int N = arr.length;

    // Function call
    maximumsubsequences(arr, N);
}
}

// This code is contributed divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
from collections import defaultdict

# Function to calculate
# the number of subsequences
# that can be formed
def No_Of_subsequences(mp):

    # Stores the number
    # of subsequences
    count = 0
    left = 0

    # Iterate over the map
    for x in mp:

        mp[x] += left

        # Count the number of
        # subsequences that can
        # be formed from x.first
        count += (mp[x] // x)

        # Number of occurrences of
        # x.first which are left
        left = mp[x] % x

    # Return the number
    # of subsequences
    return count

# Function to create the
# maximum count of subsequences
# that can be formed
def maximumsubsequences(arr, n):

    # Stores the frequency of arr[]
    mp = defaultdict (int)

    # Update the frequency
    for i in range (n):
        mp[arr[i]] += 1

    # Print the number of subsequences
    print(No_Of_subsequences(mp))

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 1, 1, 1]

    N = len(arr)

    # Function Call
    maximumsubsequences(arr, N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to calculate the number
// of subsequences that can be formed
public static int No_Of_subsequences(Dictionary<int,
                                                int> mp)
{
  // Stores the number
  // of subsequences
  int count = 0;
  int left = 0;

  // Iterate over the map
  foreach(KeyValuePair<int,
                       int> x in mp)
  {
    if(!mp.ContainsKey(x.Key))
      mp.Add(x.Key, x.Value + left);

    // Count the number of subsequences
    // that can be formed from x.first
    count += (x.Value / x.Key);

    // Number of occurrences of
    // x.first which are left
    left = x.Value % x.Key;
  }

  // Return the number of subsequences
  return count;
}

// Function to create the maximum count
// of subsequences that can be formed
public static void maximumsubsequences(int[] arr,
                                       int n)
{
  // Stores the frequency of []arr
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>();

  // Update the frequency
  for(int i = 0; i < n; i++)
  {
    if (mp.ContainsKey(arr[i]))
    {
      mp[arr[i]] =  mp[arr[i]] + 1;
    }
    else
    {
      mp.Add(arr[i], 1);
    }
  }

  // Print the number of subsequences
  Console.WriteLine(No_Of_subsequences(mp));
}

// Driver code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 1, 1, 1};

  int N = arr.Length;

  // Function call
  maximumsubsequences(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate the number
// of subsequences that can be formed
function No_Of_subsequences(mp)
{
    // Stores the number of subsequences
    var count = 0;
    var left = 0;

    // Iterate over the map
    mp.forEach((value, key) => {

        value += left;

        // Count the number of subsequences
        // that can be formed from key
        count += (value / key);

        // Number of occurrences of
        // x.first which are left
        left = value % key;
    });

    // Return the number of subsequences
    return count;
}

// Function to create the maximum count
// of subsequences that can be formed
function maximumsubsequences(arr, n)
{

    // Stores the frequency of arr[]
    var mp = new Map();

    // Update the frequency
    for (var i = 0; i < n; i++)
    {
        if(mp.has(arr[i]))
            mp.set(arr[i], mp.get(arr[i])+1)
        else
            mp.set(arr[i], 1);
    }

    // Print the number of subsequences
    document.write( No_Of_subsequences(mp));
}

// Driver Code

// Given array arr[]
var arr = [1, 1, 1, 1];
var N = arr.length;

// Function Call
maximumsubsequences(arr, N);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*
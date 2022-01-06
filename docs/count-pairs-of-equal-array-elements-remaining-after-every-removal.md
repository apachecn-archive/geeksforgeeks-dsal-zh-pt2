# 计算每次移除后剩余的相等数组元素对

> 原文:[https://www . geesforgeks . org/count-对等数组元素-每次移除后剩余的数量/](https://www.geeksforgeeks.org/count-pairs-of-equal-array-elements-remaining-after-every-removal/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，每个数组元素 **arr[i]** 的任务是计算通过从数组中移除 **arr[i]** 可以获得的相等元素对的数量。

**示例:**

> **输入:** arr[] = { 1，1，1，2 }
> **输出:** 1 1 1 3
> **解释:**
> 从数组中移除 arr[0]会将 arr[]修改为{ 1，1，2 }，相等元素对的计数= 1
> 从数组中移除 arr[1]会将 arr[]修改为{ 1，1，2 }，相等元素对的计数= 1
> 从数组中移除 arr[2]会将 arr[]修改为{ 1，2 } 2 }并且相等元素对的计数= 1
> 从数组中移除 arr[3]会将 arr[]修改为{ 1，1，1 }并且相等元素对的计数= 3
> 因此，所需的输出为 1 1 1 3。
> 
> **输入:** arr[] = { 2，3，4，3，2 }
> T3】输出:1 1 2 1 1 1

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个**I<sup>th</sup>T7】元素，从数组中移除**arr【I】**，并打印数组中剩余的相等数组元素对的计数。**

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp** ，来存储数组中每个不同元素的[频率。](https://www.geeksforgeeks.org/c-program-to-count-frequency-of-each-element-in-an-array/)
*   初始化一个变量，比如 **cntPairs** ，来存储相等数组元素对的总数。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并通过将 **cntPairs** 的值增加**(MP[I]*(MP[I]–1))/2**来存储相等元素对的总数。
*   最后[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。对于每个 **i <sup>第</sup>T5】个元素，打印**(cntPairs–MP[I]+1)**的值，通过从数组中移除 **arr[i]** 来表示相等数组元素对的计数。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs of equal elements
// by removing arr[i] from the array
void pairs_after_removing(int arr[], int N)
{
    // Stores total count of
    // pairs of equal elements
    int cntPairs = 0;

    // Store frequency of each
    // distinct array element
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of arr[i]
        mp[arr[i]]++;
    }

    // Traverse the map
    for (auto element : mp) {

        // Stores key of an element
        int i = element.first;
        cntPairs += mp[i] * (mp[i] - 1) / 2;
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores count of pairs of equal
        // element by removing arr[i]
        int pairs_after_arr_i_removed
            = cntPairs + 1 - mp[arr[i]];

        cout << pairs_after_arr_i_removed << ' ';
    }
    return;
}

// Driver Code
int main()
{
    // Given Array
    int arr[] = { 2, 3, 4, 3, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    pairs_after_removing(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count pairs of equal elements
// by removing arr[i] from the array
static void pairs_after_removing(int arr[], int N)
{

    // Stores total count of
    // pairs of equal elements
    int cntPairs = 0;

    // Store frequency of each
    // distinct array element
    Map<Integer,
        Integer> mp = new HashMap<Integer,
                                  Integer>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency of arr[i]
        mp.put(arr[i], mp.getOrDefault(arr[i], 0) + 1);
    }

    // Traverse the map
    for(Map.Entry<Integer,
                  Integer> element : mp.entrySet())
    {

        // Stores key of an element
        int i = element.getKey();
        cntPairs += mp.get(i) * (mp.get(i) - 1) / 2;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores count of pairs of equal
        // element by removing arr[i]
        int pairs_after_arr_i_removed = cntPairs +
                           1 - mp.get(arr[i]);

        System.out.print(pairs_after_arr_i_removed + " ");
    }
    return;
}

// Driver code
public static void main(String[] args)
{

    // Given Array
    int arr[] = { 2, 3, 4, 3, 2 };
    int N = arr.length;

    pairs_after_removing(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# python program to implement
# the above approach

# Function to count pairs of equal elements
# by removing arr[i] from the array
def pairs_after_removing(arr, N):

    # Stores total count of
    # pairs of equal elements
    cntPairs = 0

    # Store frequency of each
    # distinct array element
    mp = {}

    # Traverse the array
    for i in arr:

        # Update frequency of arr[i]
        mp[i] = mp.get(i, 0) + 1

    # Traverse the map
    for element in mp:

        # Stores key of an element
        i = element
        cntPairs += mp[i] * (mp[i] - 1) // 2

    # Traverse the array
    for i in range(N):

        # Stores count of pairs of equal
        # element by removing arr[i]
        pairs_after_arr_i_removed = cntPairs + 1 - mp[arr[i]]

        print(pairs_after_arr_i_removed, end = ' ')
    return

# Driver Code
if __name__ == '__main__':

    # Given Array
    arr = [2, 3, 4, 3, 2]
    N = len(arr)
    pairs_after_removing(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to count pairs of equal elements
// by removing arr[i] from the array
static void pairs_after_removing(int[] arr, int N)
{

    // Stores total count of
    // pairs of equal elements
    int cntPairs = 0;

    // Store frequency of each
    // distinct array element
     Dictionary<int,
            int> mp = new Dictionary<int,
                                      int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency of arr[i]
        if(mp.ContainsKey(arr[i]))
            {
                mp[arr[i]]++;
            }
            else
            {
                mp[arr[i]] = 1;
            }
    }

    // Traverse the map
    foreach(KeyValuePair<int,
                             int> element in mp)
    {

        // Stores key of an element
        int i = element.Key;
        cntPairs += mp[i] * (mp[i] - 1) / 2;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores count of pairs of equal
        // element by removing arr[i]
        int pairs_after_arr_i_removed = cntPairs +
                           1 - mp[arr[i]];

        Console.Write(pairs_after_arr_i_removed + " ");
    }
    return;
}

// Driver code
public static void Main()
{

    // Given Array
    int[] arr = { 2, 3, 4, 3, 2 };
    int N = arr.Length;

    pairs_after_removing(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to count pairs of equal elements
// by removing arr[i] from the array
function pairs_after_removing(arr, N)
{
    // Stores total count of
    // pairs of equal elements
    var cntPairs = 0;

    // Store frequency of each
    // distinct array element
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Update frequency of arr[i]
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i])+1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // Traverse the map
    mp.forEach((value, key) => {
         // Stores key of an element
         var i = key;
        cntPairs += mp.get(i) * (mp.get(i) - 1) / 2;
    });

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Stores count of pairs of equal
        // element by removing arr[i]
        var pairs_after_arr_i_removed
            = cntPairs + 1 - mp.get(arr[i]);

        document.write( pairs_after_arr_i_removed + ' ');
    }
    return;
}

// Driver Code
// Given Array
var arr = [2, 3, 4, 3, 2];
var N = arr.length;
pairs_after_removing(arr, N);

</script>
```

**Output:** 

```
1 1 2 1 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
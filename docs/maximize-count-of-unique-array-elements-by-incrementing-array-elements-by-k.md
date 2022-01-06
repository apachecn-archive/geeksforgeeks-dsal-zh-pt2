# 通过将数组元素增加 K 来最大化唯一数组元素的计数

> 原文:[https://www . geeksforgeeks . org/最大化唯一数组元素的计数-按 k 递增数组元素/](https://www.geeksforgeeks.org/maximize-count-of-unique-array-elements-by-incrementing-array-elements-by-k/)

给定一个由 **N** 个整数和一个整数 **K、**组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是通过将任意数组元素只增加 **K** 次来找到可能的唯一元素的最大数量。

**示例:**

> **输入:** arr[] = {0，2，4，3，4}，K = 1
> **输出:** 5
> **说明:**
> 将 arr[2] ( = 4)增加 K ( = 1)。因此，新数组是{0，2，4，3，5}，它有 5 个唯一的元素。
> 
> **输入:** arr[] = {2，3，2，4，5，5，7，4}，K = 2
> **输出:** 7
> **说明:**
> 增加 4 乘 2 = 6。
> 元素 7 增加 2 = 9
> 元素 5 增加 2 = 7。
> 新数组为{2，3，2，4，5，7，9，6}，包含 7 个唯一元素。

**方法:**解决这个问题的思路是[将数组](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)元素的频率存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，在将任意值递增 **K** 后，相应地改变数组元素，得到数组中唯一的元素。按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[将每个数组元素的频率存储在一个地图](https://www.geeksforgeeks.org/program-to-find-frequency-of-each-element-in-a-vector-using-map-in-c/)中。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并执行以下步骤:
    *   如果当前元素的计数是 **1** ，那么不要改变数组元素。
    *   如果当前元素的计数**大于 1** ，则在**图**中，将当前元素增加 **K** ，将 **(current_element + K)** 的计数增加 **1** 。
*   完成上述步骤后，打印地图 的 [**尺寸作为数组中唯一元素的最大数量。**](https://www.geeksforgeeks.org/mapsize-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum unique
// elements in array after incrementing
// any element by K
void maxDifferent(int arr[], int N, int K)
{
    // Stores the count of element
    // in array
    map<int, int> M;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Increase the counter of
        // the array element by 1
        M[arr[i]]++;
    }

    // Traverse the map
    for (auto it = M.begin();
         it != M.end(); it++) {

        // Extract the current element
        int current_element = it->first;

        // Number of times the current
        // element is present in array
        int count = it->second;

        // If element is present only
        // once, then do not change it
        if (count == 1)
            continue;

        // If the count > 1 then change
        // one of the same current
        // elements to (current_element + K)
        // and increase its count by 1
        M[current_element + K]++;
    }

    // The size of the map is the
    // required answer
    cout << M.size();
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 2, 4, 5, 5, 7, 4 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxDifferent(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the maximum unique
// elements in array after incrementing
// any element by K
static void maxDifferent(int arr[], int N, int K)
{

    // Stores the count of element
    // in array
    HashMap<Integer,
            Integer> M = new HashMap<Integer,
                                     Integer>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Increase the counter of
        // the array element by 1
        Integer count = M.get(arr[i]);

        if (count == null)
        {
            M.put(arr[i], 1);
        }
        else
        {
            M.put(arr[i], count + 1);
        }
    }

    // Iterator itr = M.entrySet().iterator();
    Iterator<Map.Entry<Integer,
                       Integer>> itr = M.entrySet().iterator();

    int[] ar1 = new int[N];

    // Traverse the map
    while (itr.hasNext())
    {
        Map.Entry<Integer, Integer> Element = itr.next();

        // Extract the current element
        int current_element = (int)Element.getKey();

        // Number of times the current
        // element is present in array
        int count = (int)Element.getValue();

        // If element is present only
        // once, then do not change it
        if (count == 1)
            continue;

        // If the count > 1 then change
        // one of the same current
        // elements to (current_element + K)
        // and increase its count by 1
        ar1[current_element + K]++;
    }

    for(int i = 0; i < N; i++)
    {
        if (ar1[i] >= 0)
        {
            Integer count = M.get(ar1[i]);

              if (count == null)
              {
                  M.put(ar1[i], 1);
            }
            else
            {
                M.put(ar1[i], count + 1);
            }
        }
    }

    // The size of the map is the
    // required answer
    System.out.println(M.size());
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 2, 4, 5, 5, 7, 4 };
    int K = 2;
    int N = arr.length;

    // Function Call
    maxDifferent(arr, N, K);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum unique
# elements in array after incrementing
# any element by K
def maxDifferent(arr, N, K):

    # Stores the count of element
    # in array
    M = {}

    # Traverse the array
    for i in range(N):

        # Increase the counter of
        # the array element by 1
        M[arr[i]] = M.get(arr[i], 0) + 1

    # Traverse the map
    for it in list(M.keys()):

        # Extract the current element
        current_element = it

        # Number of times the current
        # element is present in array
        count = M[it]

        # If element is present only
        # once, then do not change it
        if (count == 1):
            continue

        # If the count > 1 then change
        # one of the same current
        # elements to (current_element + K)
        # and increase its count by 1
        M[current_element + K] = M.get(current_element, 0) + 1

    # The size of the map is the
    # required answer
    print(len(M))

# Driver Code
if __name__ == '__main__':
    arr=[2, 3, 2, 4, 5, 5, 7, 4]
    K = 2
    N = len(arr)

    # Function Call
    maxDifferent(arr, N, K)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find the maximum unique
// elements in array after incrementing
// any element by K
static void maxDifferent(int []arr, int N, int K)
{

    // Stores the count of element
    // in array
    Dictionary<int,
            int> M = new Dictionary<int,
                                     int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Increase the counter of
        // the array element by 1
        int count = M.ContainsKey(arr[i]) ? M[arr[i]] : 0;

        if (count == 0)
        {
            M.Add(arr[i], 1);
        }
        else
        {
            M[arr[i]] = count + 1;
        }
    }

    int[] ar1 = new int[N];

    // Traverse the map
    foreach(KeyValuePair<int, int> Element in M)
    {

        // Extract the current element
        int current_element = (int)Element.Key;

        // Number of times the current
        // element is present in array
        int count = (int)Element.Value;

        // If element is present only
        // once, then do not change it
        if (count == 1)
            continue;

        // If the count > 1 then change
        // one of the same current
        // elements to (current_element + K)
        // and increase its count by 1
        ar1[current_element + K]++;
    }

    for(int i = 0; i < N; i++)
    {
        if (ar1[i] >= 0)
        {
            int count = M.ContainsKey(ar1[i]) ? M[ar1[i]] : 0;           
              if (count == 0)
              {
                  M.Add(ar1[i], 1);
            }
            else
            {
                M[ar1[i]] = count + 1;
            }
        }
    }

    // The size of the map is the
    // required answer
    Console.WriteLine(M.Count);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 2, 4, 5, 5, 7, 4 };
    int K = 2;
    int N = arr.Length;

    // Function Call
    maxDifferent(arr, N, K);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum unique
// elements in array after incrementing
// any element by K
function maxDifferent(arr, N, K)
{
    // Stores the count of element
    // in array
    var M = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Increase the counter of
        // the array element by 1
        if(M.has(arr[i]))
        {
            M.set(arr[i], M.get(arr[i])+1);
        }
        else
        {
            M.set(arr[i],1);
        }
    }

    M.forEach((value, key) => {

        // Extract the current element
        var current_element = key;

        // Number of times the current
        // element is present in array
        var count = value;

        // If element is present only
        // once, then do not change it
        if (count != 1)
        {

        // If the count > 1 then change
        // one of the same current
        // elements to (current_element + K)
        // and increase its count by 1
        if(M.has(current_element+K))
        {
            M.set(current_element+K,
            M.get(current_element+K)+1)
        }
        else
        {
            M.set(current_element+K,1);
        }

        }
    });

    // The size of the map is the
    // required answer
    document.write( M.size);
}

// Driver Code
var arr = [2, 3, 2, 4, 5, 5, 7, 4];
var K = 2;
var N = arr.length;

// Function Call
maxDifferent(arr, N, K);

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
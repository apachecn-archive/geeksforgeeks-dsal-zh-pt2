# 对具有单一独特元素的子阵列进行计数，该元素可以从给定的阵列中获得

> 原文:[https://www . geeksforgeeks . org/count-subarrays-拥有一个可以从给定数组中获得的单一独特元素/](https://www.geeksforgeeks.org/count-subarrays-having-a-single-distinct-element-that-can-be-obtained-from-a-given-array/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算由单个不同元素组成的[子阵列](https://www.geeksforgeeks.org/tag/subarray/)的数量，该元素可以从给定的阵列中获得。

示例:

> **输入:** N = 4，arr[] = {2，2，2，2}
> **输出:** 7
> **解释:**所有这样的子阵 ***{{2}、{2}、{2}、{2}、{2，2 }、{ 2，2，2 }、{ 2，2，2}}*** 。因此，这种子阵列的总数是 7。
> 
> **输入:** N = 3，arr[] = { 1，1，3 }
> T3】输出: 4

**方法:**按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并更新地图中每个元素的频率。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)检查当前元素的频率是否大于 1。

*   如果发现为真，则将子阵列计数增加当前元素的**频率–1**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays of
// single distinct element into
// which given array can be split
void divisionalArrays(int arr[3], int N)
{
    // Stores the count
    int sum = N;

    // Stores frequency of
    // array elements
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        mp[arr[i]]++;
    }

    // Traverse the map
    for (auto x : mp) {
        if (x.second > 1) {

            // Increase count of
            // subarrays by (frequency-1)
            sum += x.second - 1;
        }
    }
    cout << sum << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 3 };
    int N = sizeof(arr)
            / sizeof(arr[0]);
    divisionalArrays(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // Function to count subarrays of
  // single distinct element into
  // which given array can be split
  static void divisionalArrays(int arr[], int N)
  {

    // Stores the count
    int sum = N;

    // Stores frequency of
    // array elements
    HashMap<Integer, Integer> mp
      = new HashMap<Integer, Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
      if (mp.containsKey(arr[i]))
      {
        mp.put(arr[i], mp.get(arr[i]) + 1);
      }
      else
      {
        mp.put(arr[i], 1);
      }
    }

    // Traverse the map
    for (Map.Entry x : mp.entrySet())
    {

      if ((int)x.getValue() > 1)
      {

        // Increase count of
        // subarrays by (frequency-1)
        sum += (int)x.getValue() - 1;
      }
    }

    System.out.println(sum);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 1, 1, 3 };
    int N = arr.length;
    divisionalArrays(arr, N);
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# python 3 program for the above approach
from collections import defaultdict

# Function to count subarrays of
# single distinct element into
# which given array can be split
def divisionalArrays(arr, N):

    # Stores the count
    sum = N

    # Stores frequency of
    # array elements
    mp = defaultdict(int)

    # Traverse the array
    for i in range(N):
        mp[arr[i]] += 1

    # Traverse the map
    for x in mp:
        if (mp[x] > 1):

            # Increase count of
            # subarrays by (frequency-1)
            sum += mp[x] - 1
    print(sum)

# Driver Code
if __name__ == "__main__":

    arr = [1, 1, 3]
    N = len(arr)
    divisionalArrays(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count subarrays of
// single distinct element into
// which given array can be split
static void divisionalArrays(int []arr, int N)
{

    // Stores the count
    int sum = N;

    // Stores frequency of
    // array elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse the array
    for (int i = 0; i < N; i++)
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

    // Traverse the map
    foreach(KeyValuePair<int, int> x in mp)
    {
        if ((int)x.Value > 1)
        {

            // Increase count of
            // subarrays by (frequency-1)
            sum += (int)x.Value - 1;
        }
    }

    Console.WriteLine(sum);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 3 };
    int N = arr.Length;

    divisionalArrays(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count subarrays of
// single distinct element into
// which given array can be split
function divisionalArrays(arr, N)
{
    // Stores the count
    var sum = N;

    // Stores frequency of
    // array elements
    var mp = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i])+1);
        }
        else
        {
            mp.set(arr[i],1);
        }
    }

    // Traverse the map
    mp.forEach((value, key) => {
        if (value > 1) {

            // Increase count of
            // subarrays by (frequency-1)
            sum += value - 1;
        }
    });

    document.write( sum);
}

// Driver Code
var arr =[1, 1, 3];
var N = arr.length;
divisionalArrays(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
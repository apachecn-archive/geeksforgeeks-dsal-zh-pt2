# 通过排除每个数组元素一次来计数可能的相等元素对

> 原文:[https://www . geeksforgeeks . org/count-对相等元素进行计数-通过排除每个数组元素来可能-一次/](https://www.geeksforgeeks.org/count-pairs-of-equal-elements-possible-by-excluding-each-array-element-once/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，每个数组元素的任务是找到选择一对两个相等元素(当前元素除外)的方法数。

**示例:**

> **输入:** arr[] = {1，1，2，1，2}
> **输出:** 2 2 3 2 3
> **解释:**
> 对于 arr[0] (= 1):剩余数组元素为{1，2，1，2}。可能的配对选择是(1，1)，(2，2)。因此，计数为 2。
> 对于 arr[1] (= 1):剩余的数组元素是{1，2，1，2}。因此，计数为 2。
> 对于 arr[2] (= 2):剩余的数组元素是{1，1，1，2}。配对可能选择有(arr[0]、arr[1])、(arr[1]、arr[2])和(arr[0]、arr[2])。因此，计数为 3。
> 对于 arr[3] (= 1):其余元素为{1，1，2，2}。因此，计数为 2。
> 对于 arr[4] (= 2):其余元素为{1，1，2，1}。因此，计数为 3。
> 
> **输入:** arr[] = {1，2，1，4，2，1，4，1}
> **输出:**5 7 5 7 5 7 5 7 5 7 5

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)对于每个数组元素，从剩余数组中计数所有可能的相等元素对。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以基于以下观察进行优化:对于任何**I**T4 指数**(1≤I≤N)**计算以下两个值:

*   从数组中选择两个具有相同值的不同元素的方法数。
*   从除了第 **i <sup>第</sup>T5】元素之外的第**n1**数组元素中选择一个元素的方法数量，使得它们的值与第 **i <sup>第</sup>T9】元素的值相同。****

按照以下步骤解决问题:

1.  初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp** ，存储每个阵元的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
2.  [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)统计由相等值组成的对的数量。将计数存储在变量中，例如**总计**。
3.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个 **i** <sup>th</sup> 索引，打印**total –( MP[arr[I]]–1)**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// required pairs for every array element
void countEqualElementPairs(int arr[], int N)
{
    // Initialize a map
    unordered_map<int, int> mp;

    // Update the frequency
    // of every element
    for (int i = 0; i < N; i++) {
        mp[arr[i]] += 1;
    }

    // Stores the count of pairs
    int total = 0;

    // Traverse the map
    for (auto i : mp) {

        // Count the number of ways to
        // select pairs consisting of
        // equal elements only
        total += (i.second * (i.second - 1)) / 2;
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Print the count for
        // every array element
        cout << total - (mp[arr[i]] - 1)
             << " ";
    }
}

// Driver code
int main()
{
    // Given array
    int arr[] = { 1, 1, 2, 1, 2 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    countEqualElementPairs(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.util.Map;
import java.util.HashMap;

class GFG
{

  // Function to count the number of
  // required pairs for every array element
  public static void countEqualElementPairs(int arr[],
                                            int N)
  {

    // Initialize a map
    HashMap<Integer, Integer> map = new HashMap<>();

    // Update the frequency
    // of every element
    for (int i = 0; i < N; i++)
    {
      Integer k = map.get(arr[i]);
      map.put(arr[i], (k == null) ? 1 : k + 1);
    }

    // Stores the count of pairs
    int total = 0;

    // Traverse the map
    for (Map.Entry<Integer, Integer> e :
         map.entrySet())
    {

      // Count the number of ways to
      // select pairs consisting of
      // equal elements only
      total
        += (e.getValue() * (e.getValue() - 1)) / 2;
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Print the count for
      // every array element
      System.out.print(total - (map.get(arr[i]) - 1)
                       + " ");
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 1, 1, 2, 1, 2 };

    // Size of the array
    int N = 5;

    countEqualElementPairs(arr, N);
  }
}

// This code is contributed by adity7409.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# required pairs for every array element
def countEqualElementPairs(arr, N):

    # Initialize a map
    mp = {}

    # Update the frequency
    # of every element
    for i in range(N):
        if arr[i] in mp:
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    # Stores the count of pairs
    total = 0

    # Traverse the map
    for key,value in mp.items():

        # Count the number of ways to
        # select pairs consisting of
        # equal elements only
        total += (value * (value - 1)) / 2

    # Traverse the array
    for i in range(N):

        # Print the count for
        # every array element
        print(int(total - (mp[arr[i]] - 1)),end = " ")

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [1, 1, 2, 1, 2]

    # Size of the array
    N = len(arr)

    countEqualElementPairs(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of
// required pairs for every array element
static void countEqualElementPairs(int[] arr, int N)
{

    // Initialize a map
    Dictionary<int,
               int> map = new Dictionary<int,
                                         int>();

    // Update the frequency
    // of every element
    for(int i = 0; i < N; i++)
    {
        if (!map.ContainsKey(arr[i]))
            map[arr[i]] = 1;
        else
            map[arr[i]]++;
    }

    // Stores the count of pairs
    int total = 0;

    // Traverse the map
    foreach(KeyValuePair<int, int> e in map)
    {

        // Count the number of ways to
        // select pairs consisting of
        // equal elements only
        total += (e.Value * (e.Value - 1)) / 2;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Print the count for
        // every array element
        Console.Write(total - (map[arr[i]] - 1) + " ");
    }
}

// Driver code
public static void Main()
{

    // Given array
    int[] arr = { 1, 1, 2, 1, 2 };

    // Size of the array
    int N = 5;

    countEqualElementPairs(arr, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// required pairs for every array element
function countEqualElementPairs(arr, N)
{

    // Initialize a map
    var mp = new Map();

    // Update the frequency
    // of every element
    for(var i = 0; i < N; i++)
    {
        if (mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // Stores the count of pairs
    var total = 0;

    // Traverse the map
    mp.forEach((value, key) => {

        // Count the number of ways to
        // select pairs consisting of
        // equal elements only
        total += (value * (value - 1)) / 2;
    });

    // Traverse the array
    for(var i = 0; i < N; i++)
    {

        // Print the count for
        // every array element
        document.write(total -
                      (mp.get(arr[i]) - 1) + " ");
    }
}

// Driver code

// Given array
var arr = [ 1, 1, 2, 1, 2 ];

// Size of the array
var N = arr.length;
countEqualElementPairs(arr, N);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
2 2 3 2 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
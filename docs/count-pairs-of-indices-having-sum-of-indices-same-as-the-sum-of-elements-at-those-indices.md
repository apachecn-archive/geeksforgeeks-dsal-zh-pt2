# 计数指数总和与这些指数中元素总和相同的指数对

> 原文:[https://www . geeksforgeeks . org/count-对索引-具有索引总和-与那些索引中的元素总和相同/](https://www.geeksforgeeks.org/count-pairs-of-indices-having-sum-of-indices-same-as-the-sum-of-elements-at-those-indices/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出索引和与索引处的元素和相同的对 **(i，j)** 的数量。

**示例:**

> **输入:** arr[] = {0，1，7，4，3，2}
> **输出:** 1
> **说明:**只存在满足条件为{(0，1)}的对。
> 
> **输入:** arr[] = {1，6，2，4，5，6}
> **输出:** 0

**天真方法:**解决给定问题的简单方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，如果任何对的和与其索引的和相同，则计算这一对。检查所有对后，打印获得的总计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible pairs
// of the given array such that the sum
// of arr[i] + arr[j] is i + j
void countPairs(int arr[], int N)
{
    // Stores the total count of pairs
    int answer = 0;

    // Iterate over the range
    for (int i = 0; i < N; i++) {

        // Iterate over the range
        for (int j = i + 1; j < N; j++) {
            if (arr[i] + arr[j] == i + j) {
                answer++;
            }
        }
    }

    // Print the total count
    cout << answer;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find all possible pairs
// of the given array such that the sum
// of arr[i] + arr[j] is i + j
public static void countPairs(int arr[], int N)
{

    // Stores the total count of pairs
    int answer = 0;

    // Iterate over the range
    for(int i = 0; i < N; i++)
    {

        // Iterate over the range
        for(int j = i + 1; j < N; j++)
        {
            if (arr[i] + arr[j] == i + j)
            {
                answer++;
            }
        }
    }

    // Print the total count
    System.out.println(answer);
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 0, 1, 2, 3, 4, 5 };
    int N = arr.length;

    countPairs(arr, N);
}
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all possible pairs
# of the given array such that the sum
# of arr[i] + arr[j] is i + j
def countPairs(arr, N):

    # Stores the total count of pairs
    answer = 0

    # Iterate over the range
    for i in range(N):

        # Iterate over the range
        for j in range(i + 1, N):
            if arr[i] + arr[j] == i + j:
                answer += 1

    # Print the total count            
    print(answer)

# Driver code
arr = [ 0, 1, 2, 3, 4, 5 ]
N = len(arr)

countPairs(arr, N)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find all possible pairs
// of the given array such that the sum
// of arr[i] + arr[j] is i + j
static void countPairs(int[] arr, int N)
{

    // Stores the total count of pairs
    int answer = 0;

    // Iterate over the range
    for(int i = 0; i < N; i++)
    {

        // Iterate over the range
        for(int j = i + 1; j < N; j++)
        {
            if (arr[i] + arr[j] == i + j)
            {
                answer++;
            }
        }
    }

    // Print the total count
    Console.Write(answer);
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 0, 1, 2, 3, 4, 5 };
    int N = arr.Length;

    countPairs(arr, N);
}
}

// This code is contributed by target_2
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find all possible pairs
        // of the given array such that the sum
        // of arr[i] + arr[j] is i + j
        function countPairs(arr, N)
        {

            // Stores the total count of pairs
            let answer = 0;

            // Iterate over the range
            for (let i = 0; i < N; i++) {

                // Iterate over the range
                for (let j = i + 1; j < N; j++) {
                    if (arr[i] + arr[j] == i + j) {
                        answer++;
                    }
                }
            }

            // Print the total count
            document.write(answer);
        }

        // Driver Code
        let arr = [0, 1, 2, 3, 4, 5];
        let N = arr.length;

        countPairs(arr, N);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过使用[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)来优化，以在[数组](https://www.geeksforgeeks.org/array-data-structure/)中存储具有**(arr[I]–I)**值的元素计数 **arr[]** 。按照以下步骤解决问题:

*   初始化变量，说**回答**为 **0** 以存储在[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]中的对的计数。**
*   初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)**MP【】**来存储[数组](https://www.geeksforgeeks.org/array-data-structure/)中一个元素的[频率，数组**arr【】**的值为**(arr[I]–I)**。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   将变量**键值**初始化为**的值(arr[I]–I)**。
    *   通过 **1** 增加[无序地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)**MP【】**中**键值**的值。
*   [使用变量 **i** 遍历无序地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **mp[]** ，并执行以下步骤:
    *   将变量**大小**初始化为**一秒**无序地图的值 **mp[]** 。
    *   将**尺寸*(尺寸–1)/2**的值添加到变量**答案**中。
*   执行上述步骤后，打印**答案**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible pairs
// of the given array such that the sum
// of arr[i] + arr[j] is i + j
void countPairs(int arr[], int N)
{
    // Stores the total count of pairs
    int answer = 0;

    unordered_map<int, int> mp;

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {
        int keyValue = arr[i] - i;
        mp[keyValue]++;
    }

    // Iterate over the range [0, N]
    for (auto i : mp) {
        int size = i.second;
        answer += (size * (size - 1)) / 2;
    }

    // Print the answer
    cout << answer;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

  // Function to find all possible pairs
// of the given array such that the sum
// of arr[i] + arr[j] is i + j
    public static void countPairs(int[] arr, int n)
    {

          // Stores the total count of pairs
        int answer = 0;
        HashMap<Integer, Integer> mp
            = new HashMap<Integer, Integer>();

          // Iterate over the range [0, N]
        for (int i = 0; i < n; i++) {
            int value = arr[i] - i;
            if (mp.containsKey(value)) {
                mp.put(value, mp.get(value) + 1);
            }
            else {
                mp.put(value, 1);
            }
        }

          // Iterate over the range [0, N]
        for (Map.Entry<Integer, Integer> map :
             mp.entrySet()) {
            int temp = map.getValue();
            answer += temp * (temp - 1) / 2;
        }

          // Print the answer
        System.out.println(answer);
    }

  // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 0, 1, 2, 3, 4, 5 };
        int n = 6;
        countPairs(arr, n);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all possible pairs
# of the given array such that the sum
# of arr[i] + arr[j] is i + j
def countPairs(arr, N):

    # Stores the total count of pairs
    answer = 0
    mp = {}

    # Iterate over the range [0, N]
    for i in range(N):
        keyValue = arr[i] - i
        if keyValue in mp.keys():
            mp[keyValue] += 1
        else:
            mp[keyValue] = 1

    # Iterate over the range [0, N]
    for size in mp.values():
        answer += (size * (size - 1)) // 2

    print(answer)

# Driver code
arr = [ 0, 1, 2, 3, 4, 5 ]
N = len(arr)

countPairs(arr, N)

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find all possible pairs
// of the given array such that the sum
// of arr[i] + arr[j] is i + j
static void countPairs(int []arr, int N)
{
    // Stores the total count of pairs
    int answer = 0;

    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Iterate over the range [0, N]
    for (int i = 0; i < N; i++) {
        int keyValue = arr[i] - i;
        if(mp.ContainsKey(keyValue))
          mp[keyValue]++;
        else
          mp.Add(keyValue,1);
    }

    // Iterate over the range [0, N]
    foreach(KeyValuePair<int,int> entry in mp)
    {
        int size = entry.Value;
        answer += (size * (size - 1)) / 2;
    }

    // Print the answer
    Console.Write(answer);
}

// Driver Code
public static void Main()
{
    int []arr = {0, 1, 2, 3, 4, 5 };
    int N = arr.Length;
    countPairs(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find all possible pairs
// of the given array such that the sum
// of arr[i] + arr[j] is i + j
function countPairs(arr, N) {
  // Stores the total count of pairs
  let answer = 0;

  let mp = new Map();

  // Iterate over the range [0, N]
  for (let i = 0; i < N; i++) {
    let keyValue = arr[i] - i;

    if (mp.has(keyValue)) {
      mp.set(keyValue, mp.get(keyValue) + 1);
    } else {
      mp.set(keyValue, 1);
    }
  }

  // Iterate over the range [0, N]
  for (let i of mp) {
    let size = i[1];
    answer += (size * (size - 1)) / 2;
  }

  // Print the answer
  document.write(answer);
}

// Driver Code

let arr = [0, 1, 2, 3, 4, 5];
let N = arr.length;

countPairs(arr, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
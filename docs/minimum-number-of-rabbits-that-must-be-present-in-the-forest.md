# 森林中必须存在的最小兔子数量

> 原文:[https://www . geesforgeks . org/森林中必须存在的最小兔子数量/](https://www.geeksforgeeks.org/minimum-number-of-rabbits-that-must-be-present-in-the-forest/)

森林里有一些彩色的**兔子**。给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，使得 **arr[i]** 表示与 **i** <sup>th</sup> 兔子具有相同颜色的兔子数量，任务是找到森林中可能的最小兔子数量。

**示例:**

> **输入:** arr[] = {2，2，0}
> **输出:** 4
> **解释:**考虑到 1 <sup>st</sup> 和 2 <sup>nd</sup> 兔子的颜色相同，**如** **蓝色**，应该有 **3** 蓝色兔子。第三只兔子是唯一的那种颜色的兔子。因此，森林中可能存在的最小兔子数量是= 3 + 1 = 4。
> 
> **输入:** arr[] = {10，10，10}
> **输出:** 11
> **解释:**考虑到所有兔子的颜色相同，森林中存在的最小兔子数量为 10 + 1 = 11。

**方法:**解决这个问题的方法是**找出颜色相同的兔子组**的数量和每组兔子的**数量。以下是步骤:**

*   初始化一个变量**计数**来存储每组兔子的数量。
*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)和[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，其关键字为**arr【I】**，值为给定数组中 arr【I】出现的**。**
*   现在，如果 **y** 兔子回答 **x** ，那么:
    *   如果 **(y%(x + 1))** 是 **0** ，那么一定有 **(y / (x + 1))** 组 **(x + 1)** 兔。
    *   如果 **(y % (x + 1))** 非零，那么一定有 **(y / (x + 1)) + 1 组 **(x + 1)** 兔。**
*   将组数与每组兔子数的乘积加到变量**计数**中。
*   经过以上步骤，**计数**的值给出森林中兔子的最小数量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of rabbits in the forest
int minNumberOfRabbits(int answers[], int N)
{

    // Initialize map
    map<int, int> Map;

    // Traverse array and map arr[i]
    // to the number of occurences
    for (int a = 0; a < N; a++) {
        Map[answers[a]]++;
    }

    // Initialize count as 0;
    int count = 0;

    // Find the number groups and
    // no. of rabbits in each group
    for (auto a : Map) {
        int x = a.first;
        int y = a.second;

        // Find number of groups and
        // multiply them with number
        // of rabbits in each group
        if (y % (x + 1) == 0)
            count = count + (y / (x + 1)) * (x + 1);
        else
            count = count + ((y / (x + 1)) + 1) * (x + 1);
    }

    // count gives minimum number
    // of rabbits in the forest
    return count;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << minNumberOfRabbits(arr, N) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the minimum
    // number of rabbits in the forest
    public static int minNumberOfRabbits(int[] answers,
                                         int N)
    {
        // Initialize map
        Map<Integer, Integer> map
            = new HashMap<Integer, Integer>();

        // Traverse array and map arr[i]
        // to the number of occurences
        for (int a : answers) {
            map.put(a, map.getOrDefault(a, 0) + 1);
        }

        // Initialize count as 0;
        int count = 0;

        // Find the number groups and
        // no. of rabbits in each group
        for (int a : map.keySet()) {
            int x = a;
            int y = map.get(a);

            // Find number of groups and
            // multiply them with number
            // of rabbits in each group
            if (y % (x + 1) == 0) {
                count = count + (y / (x + 1)) * (x + 1);
            }
            else
                count
                    = count + ((y / (x + 1)) + 1) * (x + 1);
        }

        // count gives minimum number
        // of rabbits in the forest
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, 2, 0 };
        int N = arr.length;

        // Function Call
        System.out.println(minNumberOfRabbits(arr, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# number of rabbits in the forest

def minNumberOfRabbits(answers, N):

    # Initialize map
    Map = {}

    # Traverse array and map arr[i]
    # to the number of occurences
    for a in range(N):

        if answers[a] in Map:
            Map[answers[a]] += 1
        else:
            Map[answers[a]] = 1

    # Initialize count as 0;
    count = 0

    # Find the number groups and
    # no. of rabbits in each group
    for a in Map:

        x = a
        y = Map[a]

        # Find number of groups and
        # multiply them with number
        # of rabbits in each group
        if (y % (x + 1) == 0):
            count = count + (y // (x + 1)) * (x + 1)
        else:
            count = count + ((y // (x + 1)) + 1) * (x + 1)

    # count gives minimum number
    # of rabbits in the forest
    return count

# Driver code
arr = [2, 2, 0]
N = len(arr)

# Function Call
print(minNumberOfRabbits(arr, N))

# This code is contributed by divyesh072019
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG {

    // Function to find the minimum
    // number of rabbits in the forest
    public static int minNumberOfRabbits(int[] answers,
                                         int N)
    {

        // Initialize map
        Dictionary<int, int> map
            = new Dictionary<int, int>();

        // Traverse array and map arr[i]
        // to the number of occurences
        for (int a = 0; a < N; a++) {
            if (map.ContainsKey(answers[a]))
                map[answers[a]] += 1;
            else
                map.Add(answers[a], 1);
        }

        // Initialize count as 0;
        int count = 0;

        // Find the number groups and
        // no. of rabbits in each group
        for (int a = 0; a < map.Count; a++) {
            int x = map.Keys.ElementAt(a);
            int y = map[x];

            // Find number of groups and
            // multiply them with number
            // of rabbits in each group
            if (y % (x + 1) == 0) {
                count = count + (y / (x + 1)) * (x + 1);
            }
            else
                count
                    = count + ((y / (x + 1)) + 1) * (x + 1);
        }

        // count gives minimum number
        // of rabbits in the forest
        return count;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 2, 2, 0 };
        int N = arr.Length;

        // Function Call
        Console.WriteLine(minNumberOfRabbits(arr, N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum
// number of rabbits in the forest
function minNumberOfRabbits(answers, N)
{

    // Initialize map
    var map = new Map();

    // Traverse array and map arr[i]
    // to the number of occurences
    for (var a = 0; a < N; a++) {
        if(map.has(answers[a]))
            map.set(answers[a], map.get(answers[a])+1)
        else
            map.set(answers[a], 1)
    }

    // Initialize count as 0;
    var count = 0;

    // Find the number groups and
    // no. of rabbits in each group
    map.forEach((value, key) => {

        var x = key;
        var y = value;

        // Find number of groups and
        // multiply them with number
        // of rabbits in each group
        if (y % (x + 1) == 0)
            count = count + parseInt(y / (x + 1)) * (x + 1);
        else
            count = count + (parseInt(y / (x + 1)) + 1) * (x + 1);
    });

    // count gives minimum number
    // of rabbits in the forest
    return count;
}

// Driver code
var arr = [2, 2, 0];
var N = arr.length;

// Function Call
document.write( minNumberOfRabbits(arr, N));

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**另一种解决方案**是使用计数的 HashMap，并在每次遇到相同的**答案【I】**时减少计数。如果相同的**答案【I】**再次出现并且**计数**为零，则用**答案【I】+1**重置计数并添加到答案变量中。以下是步骤:

*   用零初始化变量**计数**。
*   使用无序地图 mp。
*   遍历数组并执行以下操作:
    *   如果**答案[i]** 设置为零，则设置 **mp【答案[I]】=答案[i]+1** 和**计数=计数+答案[i]+1**
    *   最后从地图上减去计数，**MP[答案[I]]–**；
*   返回 cnt 作为答案。

## C++

```
// C++ program for the above approach
#include <iostream>
#include <unordered_map>

using namespace std;

// Function to find the minimum
// number of rabbits in the forest
int minNumberOfRabbits(int answers[], int n)
{
    // Initialize cnt variable
    int count = 0;
    // Initialize map
    unordered_map<int, int> mp;
    for (int i = 0; i < n; ++i) {

        // Add to the count if not found or
        // has exhausted the count of all the
        // number of rabbits of same colour
        if (mp[answers[i]] == 0) {
            count += answers[i] + 1;
            mp[answers[i]] = answers[i] + 1;
        }
        mp[answers[i]]--;
    }

    // count gives minimum number
    // of rabbits in the forest
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 10, 10, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << minNumberOfRabbits(arr, N) << endl;

    return 0;
}

// This code is contributed by Bhavna Soni - bhavna23
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum
# number of rabbits in the forest
def minNumberOfRabbits(answers, n):

    # Initialize cnt variable
    count = 0

    # Initialize map
    mp = {}
    for i in range(n):

        # Add to the count if not found or
        # has exhausted the count of all the
        # number of rabbits of same colour
        if (answers[i] not in mp):
            count += answers[i] + 1
            mp[answers[i]] = answers[i] + 1

        mp[answers[i]] -= 1

    # count gives minimum number
    # of rabbits in the forest
    return count

# Driver Code
if __name__ == "__main__":

    arr = [10, 10, 0]
    N = len(arr)

    # Function Call
    print(minNumberOfRabbits(arr, N))

    # This code is contributed by ukasp.
```

**Output**

```
12

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
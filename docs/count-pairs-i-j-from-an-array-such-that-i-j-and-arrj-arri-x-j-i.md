# 对数组中的对(I，j)进行计数，使得 i < j 和 arr[j]–arr[I]= X *(j–I)

> 原文:[https://www . geesforgeks . org/count-pairs-I-j-from-a-a-I-j-so-I-j-and-arrj-arri-x-j-I/](https://www.geeksforgeeks.org/count-pairs-i-j-from-an-array-such-that-i-j-and-arrj-arri-x-j-i/)

给定一个由 **N** 个整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算对 **(i，j)** 的数量，使得 **i < j** 和**arr[I]–arr[j]= X *(j–I)**。

**示例:**

> ***输入:** N = 5，X = 2，arr[] = {1，5，5，7，11}*
> ***输出:** 4*
> ***解释:**所有的对(I，j)使得 **i < j** 和 arr[j]–arr[I]= X *(j–I)是(0，2)，(0，3)，(1，4)和(2)*
> *对于(0，2)，arr[2]–arr[0]= 5–1 = 4 和 x *(j–I)= 2 *(2–0)= 4，满足条件 arr[j]–arr[I]= x *(j–I)，其中 j = 2，i = 1 和 x = 2。*
> *同样，对(0，3)、(1，4)和(2，3)也满足给定条件。*
> 
> ***输入:** N = 6，X = 3，arr[] = {5，4，8，11，13，16}*
> ***输出:** 4*

**天真方法:**解决问题最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并针对每个对检查给定的等式是否满足。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**这个问题可以使用 [HashMap](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 解决。按照以下步骤解决此问题:

*   给定的条件是**arr[j]–arr[I]= X *(j–I)。**这个等式可以改写为**arr[j]–arr[I]= x * j–x * I，**可以改写为**arr[j]–x * j = arr[I]–x * I .**
*   所以现在情况变了，找到配对 **(i，j)** ，这样 **i < j** 和**arr[j]–x * j = arr[I]–x * I**。
*   所以所有**arr【index】–x * index**相同的索引，都可以配对。假设经过所有迭代后， **arr【索引】–x * index**的计数为 **y** 。所以现在从 **y** 指数中选择两个不同的指数。无非是 **yC2、**等于 **(y*(y-1))/2** 。
*   现在，[使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代:
    *   在每次迭代中执行 **arr【索引】–x * index**。同时增加**arr[索引]–x *索引的计数。**
*   遍历[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/):
    *   在每次迭代期间，执行**计数=计数+(y *(y–1))/2。，其中 **y** 是[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)的第二个值。这只是**arr[index]–x * index 的计数。****

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs (i, j) such that i < j and
// arr[i] - arr[j] = X*( j - i )
void countPairs(int arr[], int n, int x)
{

    // Stores the count of all such
    // pairs that satisfies the condition.
    int count = 0;

    map<int, int> mp;

    for (int i = 0; i < n; i++) {

        // Stores count of distinct
        // values of arr[i] - x * i
        mp[arr[i] - x * i]++;
    }

    // Iterate over the Map
    for (auto x : mp) {

        int n = x.second;

        // Increase count of pairs
        count += (n * (n - 1)) / 2;
    }

    // Print the count of such pairs
    cout << count;
}

// Driver Code
int main()
{
    int n = 6, x = 3;
    int arr[] = { 5, 4, 8, 11, 13, 16 };

    countPairs(arr, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count the number of
// pairs (i, j) such that i < j and
// arr[i] - arr[j] = X*( j - i )
static void countPairs(int arr[], int n, int x)
{

    // Stores the count of all such
    // pairs that satisfies the condition.
    int count = 0;

    HashMap<Integer, Integer> mp = new HashMap<>();

    for(int i = 0; i < n; i++)
    {

        // Stores count of distinct
        // values of arr[i] - x * i
        mp.put(arr[i] - x * i,
               mp.getOrDefault(arr[i] - x * i, 0) + 1);
    }

    // Iterate over the Map
    for(int v : mp.values())
    {

        // Increase count of pairs
        count += (v * (v - 1)) / 2;
    }

    // Print the count of such pairs
    System.out.println(count);
}

// Driver Code
public static void main(String[] args)
{
    int n = 6, x = 3;
    int arr[] = { 5, 4, 8, 11, 13, 16 };

    countPairs(arr, n, x);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# pairs (i, j) such that i < j and
# arr[i] - arr[j] = X*( j - i )
def countPairs(arr, n, x):

    # Stores the count of all such
    # pairs that satisfies the condition.
    count = 0

    mp = {}

    for i in range(n):

        # Stores count of distinct
        # values of arr[i] - x * i
        if ((arr[i] - x * i) in mp):
            mp[arr[i] - x * i] += 1
        else:
            mp[arr[i] - x * i] = 1

    # Iterate over the Map
    for key, value in mp.items():
        n = value

        # Increase count of pairs
        count += (n * (n - 1)) // 2

    # Print the count of such pairs
    print(count)

# Driver Code
if __name__ == '__main__':

    n = 6
    x = 3
    arr = [ 5, 4, 8, 11, 13, 16 ]

    countPairs(arr, n, x)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of
// pairs (i, j) such that i < j and
// arr[i] - arr[j] = X*( j - i )
static void countPairs(int[] arr, int n, int x)
{

    // Stores the count of all such
    // pairs that satisfies the condition.
    int count = 0;

    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    for(int i = 0; i < n; i++)
    {

        // Stores count of distinct
        // values of arr[i] - x * i
        if (!mp.ContainsKey(arr[i] - x * i))
            mp[arr[i] - x * i] = 0;

        mp[arr[i] - x * i] = mp[arr[i] - x * i] + 1;
    }

    // Iterate over the Map
    foreach(KeyValuePair<int, int> v in mp)
    {

        // Increase count of pairs
        count += (v.Value * (v.Value - 1)) / 2;
    }

    // Print the count of such pairs
    Console.WriteLine(count);
}

// Driver Code
public static void Main(string[] args)
{
    int n = 6, x = 3;
    int[] arr = { 5, 4, 8, 11, 13, 16 };

    countPairs(arr, n, x);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the number of
// pairs (i, j) such that i < j and
// arr[i] - arr[j] = X*( j - i )
function countPairs(arr, n, x)
{

    // Stores the count of all such
    // pairs that satisfies the condition.
    let count = 0;

    let mp = new Map();

    for (let i = 0; i < n; i++) {

        // Stores count of distinct
        // values of arr[i] - x * i
        if (mp.has(arr[i] - x * i)) {
            mp.set(arr[i] - x * i, mp.get(arr[i] - x * i) + 1)
        } else {
            mp.set(arr[i] - x * i, 1)
        }
    }

    // Iterate over the Map
    for (let x of mp) {

        let n = x[1];

        // Increase count of pairs
        count += Math.floor((n * (n - 1)) / 2);
    }

    // Print the count of such pairs
    document.write(count);
}

// Driver Code

let n = 6, x = 3;
let arr = [5, 4, 8, 11, 13, 16];

countPairs(arr, n, x);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
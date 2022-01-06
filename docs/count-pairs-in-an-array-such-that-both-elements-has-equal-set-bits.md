# 对数组中的对进行计数，使两个元素具有相等的设置位

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-a-array-so-elements-都有相等的设置位/](https://www.geeksforgeeks.org/count-pairs-in-an-array-such-that-both-elements-has-equal-set-bits/)

给定一个具有唯一元素的数组 *arr* ，任务是计算具有相等设置位计数的元素对的总数。
**例:**

> **输入:** arr[] = {2，5，8，1，3}
> **输出:** 4
> 为{2，5，8，1，3}设置的位数为{1，2，1，1，2}
> 所有设置位数相同的对为{2，8}、{2，1}、{5，3}、{8，1}
> **输入:** arr[] = {1，11，7，3}

**进场:**

*   从左到右遍历数组，[统计每个整数的设置位总数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。
*   使用映射存储具有相同设置位计数的元素数量，设置位作为关键字，计数作为值。
*   然后迭代器遍历地图元素，计算 n 个元素(对于地图的每个元素)可以组成多少个两个元素对，即 *(n * (n-1)) / 2* 。
*   最终结果将是上一步对地图每个元素的输出总和。

以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count all pairs
// with equal set bits count
int totalPairs(int arr[], int n)
{
    // map to store count of elements
    // with equal number of set bits
    map<int, int> m;
    for (int i = 0; i < n; i++) {

        // inbuilt function that returns the
        // count of set bits of the number
        m[__builtin_popcount(arr[i])]++;
    }

    map<int, int>::iterator it;
    int result = 0;
    for (it = m.begin(); it != m.end(); it++) {

        // there can be (n*(n-1)/2) unique two-
        // element pairs to choose from n elements
        result
            += (*it).second * ((*it).second - 1) / 2;
    }

    return result;
}

// Driver code
int main()
{
    int arr[] = { 7, 5, 3, 9, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << totalPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG {

    /* Function to get no of set 
    bits in binary representation 
    of passed binary no. */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            n &= (n - 1) ;
            count++;
        }
        return count;
    }

    // Function to count all pairs
    // with equal set bits count
    static int totalPairs(int arr[], int n)
    {
        // map to store count of elements
        // with equal number of set bits
        HashMap<Integer, Integer> m = new HashMap<>();
        for (int i = 0; i < n; i++) {

            // function that returns the
            // count of set bits of the number
            int count = countSetBits(arr[i]);
            if(m.containsKey(count))
                m.put(count, m.get(count) + 1);
            else
                m.put(count, 1);
        }

        int result = 0;
        for (Map.Entry<Integer, Integer> entry : m.entrySet()) {
            int value = entry.getValue();

            // there can be (n*(n-1)/2) unique two-
            // element pairs to choose from n elements
            result += ((value * (value -1)) / 2);
        }

        return result;
    }

    public static void main (String[] args) {
        int arr[] = { 7, 5, 3, 9, 1, 2 };
        int n = arr.length;
        System.out.println(totalPairs(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count all pairs
# with equal set bits count
def totalPairs(arr, n):

    # map to store count of elements
    # with equal number of set bits
    m = dict()

    for i in range(n):

        # inbuilt function that returns the
        # count of set bits of the number
        x = bin(arr[i]).count('1')

        m[x] = m.get(x, 0) + 1;

    result = 0
    for it in m:

        # there can be (n*(n-1)/2) unique two-
        # element pairs to choose from n elements
        result+= (m[it] * (m[it] - 1)) // 2

    return result

# Driver code
arr = [7, 5, 3, 9, 1, 2]
n = len(arr)

print(totalPairs(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to rearrange a string so that all same
// characters become atleast d distance away
using System;
using System.Collections.Generic;

class GFG
{

    /* Function to get no of set
    bits in binary representation
    of passed binary no. */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            n &= (n - 1) ;
            count++;
        }
        return count;
    }

    // Function to count all pairs
    // with equal set bits count
    static int totalPairs(int []arr, int n)
    {
        // map to store count of elements
        // with equal number of set bits
        Dictionary<int,int> mp = new Dictionary<int,int>();
        for (int i = 0 ; i < n; i++)
        {
            // function that returns the
            // count of set bits of the number
            int count = countSetBits(arr[i]);
            if(mp.ContainsKey(count))
            {
                var val = mp[count];
                mp.Remove(count);
                mp.Add(count, val + 1);
            }
            else
            {
                mp.Add(count, 1);
            }
        }

        int result = 0;
        foreach(KeyValuePair<int, int> entry in mp){
            int values = entry.Value;

            // there can be (n*(n-1)/2) unique two-
            // element pairs to choose from n elements
            result += ((values * (values -1)) / 2);
        }

        return result;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 7, 5, 3, 9, 1, 2 };
        int n = arr.Length;
        Console.WriteLine(totalPairs(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

 /* Function to get no of set
bits in binary representation
of passed binary no. */
function countSetBits(n)
{
    var count = 0;
    while (n > 0)
    {
        n &= (n - 1) ;
        count++;
    }
    return count;
}

// Function to count all pairs
// with equal set bits count
function totalPairs(arr, n)
{
    // map to store count of elements
    // with equal number of set bits
    var m = new Map();
    for (var i = 0; i < n; i++) {

        // inbuilt function that returns the
        // count of set bits of the number
        if(m.has(arr[i]))
        {
            m.set(countSetBits(arr[i]), m.get(countSetBits(arr[i]))+1);
        }
        else{
            m.set(countSetBits(arr[i]), 1);
        }

    }

    var result = 0;
    m.forEach((value, key) => {
        // there can be (n*(n-1)/2) unique two-
        // element pairs to choose from n elements
        result += parseInt(key * (key - 1) / 2);
    });

    return result;
}

// Driver code
var arr = [7, 5, 3, 9, 1, 2 ];
var n = arr.length;
document.write( totalPairs(arr, n));

</script>
```

**Output:** 

```
4
```
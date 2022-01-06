# 所需的最小删除量，以使任何数字 X 恰好出现 X 次

> 原文:[https://www . geesforgeks . org/minimum-deletions-required-so-any-number-x-将要发生-恰好-x-times/](https://www.geeksforgeeks.org/minimum-deletions-required-such-that-any-number-x-will-occur-exactly-x-times/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到所需的最小删除量，以便对于 **i** 的所有可能值， **arr[i]** 的频率正好是数组中的 **arr[i]** 。
**举例:**

> **输入:** arr[] = {1，2，2，3，3}
> **输出:** 2
> 频率(1) = 1
> 频率(2) = 2
> 频率(3) = 2，频率不能增加
> 所以，删除 3 的每一个出现。
> **输入:** arr[] = {2，3，2，3，4，4，4，4，5}
> **输出:** 3

**进场:**有两种情况:

*   如果 X 的频率大于或等于 0，那么我们删除 X 的额外频率，以精确地得到 X 值的 X 个元素
*   如果 X 的频率小于 X，那么我们删除 X 的所有出现，因为不可能得到额外的 X 值元素

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// deletions required
int MinDeletion(int a[], int n)
{

    // To store the frequency of
    // the array elements
    unordered_map<int, int> map;

    // Store frequency of each element
    for (int i = 0; i < n; i++)
        map[a[i]]++;

    // To store the minimum deletions required
    int ans = 0;

    for (auto i : map) {

        // Value
        int x = i.first;

        // It's frequency
        int frequency = i.second;

        // If number less than or equal
        // to it's frequency
        if (x <= frequency) {

            // Delete extra occurrences
            ans += (frequency - x);
        }

        // Delete every occurrence of x
        else
            ans += frequency;
    }

    return ans;
}

// Driver code
int main()
{
    int a[] = { 2, 3, 2, 3, 4, 4, 4, 4, 5 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MinDeletion(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of above approach
import java.util.*;

class GFG
{

// Function to return the minimum
// deletions required
static int MinDeletion(int a[], int n)
{

    // To store the frequency of
    // the array elements
    Map<Integer,Integer> mp = new HashMap<>();

    // Store frequency of each element
    for (int i = 0 ; i < n; i++)
    {
        if(mp.containsKey(a[i]))
        {
            mp.put(a[i], mp.get(a[i])+1);
        }
        else
        {
            mp.put(a[i], 1);
        }
    }
    // To store the minimum deletions required
    int ans = 0;

    for (Map.Entry<Integer,Integer> i : mp.entrySet())
    {

        // Value
        int x = i.getKey();

        // It's frequency
        int frequency = i.getValue();

        // If number less than or equal
        // to it's frequency
        if (x <= frequency)
        {

            // Delete extra occurrences
            ans += (frequency - x);
        }

        // Delete every occurrence of x
        else
            ans += frequency;
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 2, 3, 2, 3, 4, 4, 4, 4, 5 };
    int n = a.length;

    System.out.println(MinDeletion(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# deletions required
def MinDeletion(a, n) :

    # To store the frequency of
    # the array elements
    map = dict.fromkeys(a, 0);

    # Store frequency of each element
    for i in range(n) :
        map[a[i]] += 1;

    # To store the minimum deletions required
    ans = 0;

    for key,value in map.items() :

        # Value
        x = key;

        # It's frequency
        frequency = value;

        # If number less than or equal
        # to it's frequency
        if (x <= frequency) :

            # Delete extra occurrences
            ans += (frequency - x);

        # Delete every occurrence of x
        else :
            ans += frequency;

    return ans;

# Driver code
if __name__ == "__main__" :

    a = [ 2, 3, 2, 3, 4, 4, 4, 4, 5 ];
    n = len(a);

    print(MinDeletion(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# Implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the minimum
// deletions required
static int MinDeletion(int []a, int n)
{

    // To store the frequency of
    // the array elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Store frequency of each element
    for (int i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(a[i]))
        {
            var val = mp[a[i]];
            mp.Remove(a[i]);
            mp.Add(a[i], val + 1);
        }
        else
        {
            mp.Add(a[i], 1);
        }
    }

    // To store the minimum deletions required
    int ans = 0;

    foreach(KeyValuePair<int, int> i in mp)
    {

        // Value
        int x = i.Key;

        // It's frequency
        int frequency = i.Value;

        // If number less than or equal
        // to it's frequency
        if (x <= frequency)
        {

            // Delete extra occurrences
            ans += (frequency - x);
        }

        // Delete every occurrence of x
        else
            ans += frequency;
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 2, 3, 2, 3, 4, 4, 4, 4, 5 };
    int n = a.Length;

    Console.WriteLine(MinDeletion(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javaScript implementation of the approach

// Function to return the minimum
// deletions required
function MinDeletion( a, n){
    // To store the frequency of
    // the array elements
    let map = new Map();

    // Store frequency of each element
    for (let i = 0; i < n; i++){
        if(map[a[i]])
            map[a[i]]++;
        else
            map[a[i]] = 1
     }

    // To store the minimum deletions required
    let ans = 0;
    for(var m in map){

        // Value
        let x = m;

        // It's frequency
        let frequency = map[m];

        // If number less than or equal
        // to it's frequency
        if (x <= frequency) {

            // Delete extra occurrences
            ans += (frequency - x);
        }

        // Delete every occurrence of x
        else
            ans += frequency;
    };

    return ans;
}

// Driver code
let a = [ 2, 3, 2, 3, 4, 4, 4, 4, 5 ];
let n = a.length;
document.write( MinDeletion(a, n));

// This code is contributed by rohitsingh07052.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)
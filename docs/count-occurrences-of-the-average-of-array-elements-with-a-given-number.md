# 计算给定数量的数组元素平均值的出现次数

> 原文:[https://www . geesforgeks . org/count-给定数量数组元素的平均出现次数/](https://www.geeksforgeeks.org/count-occurrences-of-the-average-of-array-elements-with-a-given-number/)

给定一组![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")整数和一个整数![x   ](img/7af94c6fbe791dbc443f7dd499ff3372.png "Rendered by QuickLaTeX.com")。对于数组 **a[i]** 的每个整数，任务是计算数组中数值等于元素 a[i]和 x 的**平均值的数字的计数。即数组中元素 a[i]和 x 的(*平均值)的出现次数。***

**示例:**

> **输入** : arr[] = {2，0，4，6，2}，x = 2
> **输出** : 2 0 0 1 2
> 对于 x = 2，2，0，4，6，2 的平均值分别为 2，1，3，4，2。因此，计数数组将产生 2，0，0，1，2。
> 
> **输入** : arr[] = {9，5，2，4，0，3}，x = 3
> **输出** : 0 1 1 1 0 1
> 对于 x = 3，9，5，2，4，0，3 的平均值分别为 6，4，2，3，1，2。因此，计数数组将产生 0，1，1，1，0，1。

**进场:**

1.  遍历数组，用数组中的出现次数映射每个元素。
2.  现在再次遍历数组，取数组元素的平均值并给定![x   ](img/7af94c6fbe791dbc443f7dd499ff3372.png "Rendered by QuickLaTeX.com")，检查其在地图中的值。

下面是上述方法的实现:

## C++

```
// CPP program to find the count of
// occurrences of the average of array
// elements with a given number
#include<bits/stdc++.h>

using namespace std;

    // Function to find the count of
    // occurrences of the average of array
    // elements with a given number
    void getAverageCountArray(int a[], int x, int N)
    {
        // mp to store count of occurrence
        // of every array element in the array
        map<int,int> mp;

        // Array that stores the average
        // count for given array
        int avg[N] = {0};
        int val, av;

        for (int i = 0; i < N; i++)
        {
            // first occurrence of a[i]
            if (mp[a[i]] == 0)
                mp[a[i]] = 1;

            else
            mp[a[i]]++;

            // element has already occurred before
            // so increase its count
        }

        for (int i = 0; i < N; i++)
        {
            av = int((a[i] + x) / 2);
            if (mp.find(av) != mp.end())
            {
                val = mp[av];
                avg[i] = val;
            }
        }

        // Printing the average count array
        for (int i = 0; i < N; i++)
        {
            cout << avg[i] << " ";
        }
    }

    // Driver code
    int main()
    {
        int a[] = { 2, 0, 4, 6, 2 };
        int x = 2;

        int N = sizeof(a)/sizeof(a[0]);
        getAverageCountArray(a, x, N);
    }

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// occurrences of the average of array
// elements with a given number
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    // Function to find the count of
    // occurrences of the average of array
    // elements with a given number
    static void getAverageCountArray(int[] a, int x, int N)
    {
        // Map to store count of occurrence
        // of every array element in the array
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();

        // Array that stores the average
        // count for given array
        int[] avg = new int[N];
        int val, av;

        for (int i = 0; i < N; i++) {
            // first occurrence of a[i]
            if (!map.containsKey(a[i])) {
                map.put(a[i], 1);
            }

            // element has already occurred before
            // so increase its count
            else {
                // gives current count of a[i]
                val = map.get(a[i]);
                val++;
                map.remove(a[i]);
                map.put(a[i], val);
            }
        }

        for (int i = 0; i < N; i++) {
            av = (a[i] + x) / 2;
            if (map.containsKey(av)) {
                val = map.get(av);
                avg[i] = val;
            }
        }

        // Printing the average count array
        for (int i = 0; i < N; i++) {
            System.out.print(avg[i] + " ");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int[] a = { 2, 0, 4, 6, 2 };
        int x = 2;

        int N = a.length;

        getAverageCountArray(a, x, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the count of
# occurrences of the average of array
# elements with a given number

# Function to find the count of
# occurrences of the average of array
# elements with a given number
def getAverageCountArray(a, x, N):

    # Dictionary to store count of occurrence
    # of every array element in the array
    map = {}

    # Array that stores the average
    # count for given array
    avg = [0] * N

    for i in range(N): 
        # first occurrence of a[i]
        if a[i] not in map: 
            map[a[i]] =  1

        # element has already occurred before
        # so increase its count
        else:
            # gives current count of a[i]
            map[a[i]] += 1

    for i in range(N): 
        av = (a[i] + x) // 2

        if av in map:
            val = map[av]
            avg[i] = val

    # Printing the average count array
    for i in range(N):
        print(avg[i], end = " ")

if __name__ == "__main__":

    a = [2, 0, 4, 6, 2] 
    x = 2

    N = len(a)
    getAverageCountArray(a, x, N)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the count of
// occurrences of the average of array
// elements with a given number
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the count of
// occurrences of the average of array
// elements with a given number
static void getAverageCountArray(int[] a, int x,
                                          int N)
{
    // Map to store count of occurrence
    // of every array element in the array
    Dictionary<int,
               int> map = new Dictionary<int,
                                         int>();

    // Array that stores the average
    // count for given array
    int[] avg = new int[N];
    int val, av;

    for (int i = 0; i < N; i++)
    {
        // first occurrence of a[i]
        if (!map.ContainsKey(a[i]))
        {
            map.Add(a[i], 1);
        }

        // element has already occurred before
        // so increase its count
        else
        {
            // gives current count of a[i]
            val = map[a[i]];
            val++;
            map.Remove(a[i]);
            map.Add(a[i], val);
        }
    }

    for (int i = 0; i < N; i++)
    {
        av = (a[i] + x) / 2;
        if (map.ContainsKey(av))
        {
            val = map[av];
            avg[i] = val;
        }
    }

    // Printing the average count array
    for (int i = 0; i < N; i++)
    {
        Console.Write(avg[i] + " ");
    }
}

// Driver code
public static void Main()
{
    int[] a = { 2, 0, 4, 6, 2 };
    int x = 2;

    int N = a.Length;

    getAverageCountArray(a, x, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the count of
// occurrences of the average of array
// elements with a given number

    // Function to find the count of
    // occurrences of the average of array
    // elements with a given number
    function getAverageCountArray(a, x, N)
    {
        // Map to store count of occurrence
        // of every array element in the array
        let map = new Map();

        // Array that stores the average
        // count for given array
        let avg = Array.from({length: N}, (_, i) => 0);
        let val, av;

        for (let i = 0; i < N; i++) {
            // first occurrence of a[i]
            if (!map.has(a[i])) {
                map.set(a[i], 1);
            }

            // element has already occurred before
            // so increase its count
            else {
                // gives current count of a[i]
                val = map.get(a[i]);
                val++;
                map.delete(a[i]);
                map.set(a[i], val);
            }
        }

        for (let i = 0; i < N; i++) {
            av = (a[i] + x) / 2;
            if (map.has(av)) {
                val = map.get(av);
                avg[i] = val;
            }
        }

        // Printing the average count array
        for (let i = 0; i < N; i++) {
            document.write(avg[i] + " ");
        }
    }

// Driver Code

           let a = [ 2, 0, 4, 6, 2 ];
        let x = 2;

        let N = a.length;

        getAverageCountArray(a, x, N);

</script>
```

**Output:** 

```
2 0 0 1 2
```
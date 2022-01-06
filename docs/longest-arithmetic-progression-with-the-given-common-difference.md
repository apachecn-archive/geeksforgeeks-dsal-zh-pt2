# 给定公共差的最长算术级数

> 原文:[https://www . geeksforgeeks . org/给定公差的最长算术级数/](https://www.geeksforgeeks.org/longest-arithmetic-progression-with-the-given-common-difference/)

给定一个大小为 n 的未排序数组和一个整数 d，这是它们的共同区别，任务是找到最长 AP 的长度。
对于所有 j，大于一些 i( < n)，

```
if a[j] = a[i] + (j-i) * d
```

即 a[j]在从索引 I 到 j 的 a[i]的 AP 中。
**示例:**

> **输入:** n = 6，d = 2
> arr[] = {1，2，5，7，9，85}
> **输出:** 4
> 考虑到指数，最长的 AP 是【1，5，7，9】
> ，因为 5 比 1 领先 2 个指数，如果从指数 0 开始
> 将适合 AP。as 5 = 1+(2–0)* 2。所以输出是 4。
> **输入:** n = 10，d = 3
> arr[] = {1，4，2，5，20，11，56，100，20，23}
> **输出:** 5
> 考虑到指数，最长的 AP 是【2，5，11，20，23】
> ，因为 11 是领先 5 的 2 个指数，20 是领先 11 的 3 个指数。因此，如果从索引 2 开始，它们
> 将适合 AP。

**简单方法:**对于每个元素，计算它可能形成的最长 AP 的长度，并打印其中的最大值。它涉及到 **O(n <sup>2</sup> )** 时间复杂度。
一种有效的**方法是使用哈希。
创建一个地图，其中键是一个 ap 的起始元素，其值是该 AP 中的元素数量。其思想是每当索引 j( > i)处的元素可能在“a”(作为起始元素)的 ap 中时，将键“a”(位于索引 I 处且其起始元素尚未在映射中)处的值更新 1。然后我们打印地图中所有值中的最大值。** 

## C++

```
// C++ code for finding the
// maximum length of AP

#include <bits/stdc++.h>
using namespace std;
int maxlenAP(int* a, int n, int d)
{
    // key=starting element of an AP,
    // value=length of AP
    unordered_map<int, int> m;

    // since the length of longest AP is at least
    // one i.e. the number itself.
    int maxt = 1;

    // if element a[i]'s starting element(i.e., a[i]-i*d)
    // is not in map then its value is 1 else there already
    // exists a starting element of an AP of which a[i]
    // can be a part.
    for (int i = 0; i < n; i++) {
        m[a[i] - i * d]++;
    }

    // auto operator stores the key,
    // value pair type from the map.
    for (auto& it : m)
        if (it.second > maxt)

            // calculating the length of longest AP.
            maxt = it.second;

    return maxt;
}

// Driver code
int main()
{
    int n = 10, d = 3;
    int a[10] = { 1, 4, 2, 5, 20, 11, 56, 100, 20, 23 };

    cout << maxlenAP(a, n, d) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for finding the
// maximum length of AP
import java.io.*;
import java.util.HashMap;
import java.util.Map.Entry;
import java.util.Map;
import java.lang.*;

class GFG
{
static int maxlenAP(int a[],
                    int n, int d)
{
    // key=starting element of an AP,
    // value=length of AP
    HashMap<Integer, Integer> m =
                    new HashMap<Integer, Integer>();

    // since the length of longest
    // AP is at least one i.e.
    // the number itself.
    int maxt = 1;

    // if element a[i]'s starting
    // element(i.e., a[i]-i*d)
    // is not in map then its value
    // is 1 else there already
    // exists a starting element of
    // an AP of which a[i] can be
    // a part.
    for (int i = 0; i < n; i++)
    {
        if(m.containsKey(a[i] - i * d))
        {
            int freq = m.get(a[i] - i * d);
            freq++;
            m.put(a[i] - i * d, freq);
        }
        else
        {
            m.put(a[i] - i * d, 1);
        }
    }

    // auto operator stores the key,
    // value pair type from the map.
    for(Entry<Integer, Integer> val: m.entrySet())
    {
        if (maxt < val.getValue())
            maxt = val.getValue();
    }
    return maxt;
}

// Driver code
public static void main(String[] args)
{
    int n = 10, d = 3;
    int a[] = new int[]{ 1, 4, 2, 5, 20, 11,
                         56, 100, 20, 23 };

    System.out.print(maxlenAP(a, n, d) + "\n");
}
}
```

## C#

```
// C# code for finding the
// maximum length of AP
using System;
using System.Collections.Generic;

class GFG
{
    static int maxlenAP(int []a,
                    int n, int d)
    {
        // key=starting element of an AP,
        // value=length of AP
        Dictionary<int,int> m =
                    new Dictionary<int,int>();

        // since the length of longest
        // AP is at least one i.e.
        // the number itself.
        int maxt = 1;

        // if element a[i]'s starting
        // element(i.e., a[i]-i*d)
        // is not in map then its value
        // is 1 else there already
        // exists a starting element of
        // an AP of which a[i] can be
        // a part.
        for (int i = 0; i < n; i++)
        {
            if(m.ContainsKey(a[i] - i * d))
            {
                int freq = m[a[i] - i * d];
                freq++;
                m.Remove(a[i] - i * d);
                m.Add(a[i] - i * d, freq);
            }
            else
            {
                m.Add(a[i] - i * d, 1);
            }
        }

        // auto operator stores the key,
        // value pair type from the map.
        foreach(var val in m)
        {
            if (maxt < val.Value)
                maxt = val.Value;
        }
        return maxt;
}

// Driver code
public static void Main(String[] args)
{
    int n = 10, d = 3;
    int []a = new int[]{ 1, 4, 2, 5, 20, 11,
                        56, 100, 20, 23 };

    Console.Write(maxlenAP(a, n, d) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for finding the
# maximum length of AP

def maxlenAP(a, n, d):

    # key = starting element of an AP,
    # value = length of AP
    m = dict()

    # since the length of longest AP is at least
    # one i.e. the number itself.
    maxt = 1

    # if element a[i]'s starting element(i.e., a[i]-i*d)
    # is not in map then its value is 1 else there already
    # exists a starting element of an AP of which a[i]
    # can be a part.
    for i in range(n):
        if (a[i] - i * d) in m:
            m[a[i] - i * d] += 1
        else:
            m[a[i] - i * d] = 1

    # In this it variable will be
    # storing key value of dictionary.
    for it in m:
        if m[it] > maxt:

            # calculating the length of longest AP.
            maxt = m[it]

    return maxt

# Driver code
if __name__ == "__main__":
    n, d = 10, 3
    a = [1, 4, 2, 5, 20, 11, 56, 100, 20, 23]
    print(maxlenAP(a, n, d))

# This code is contributed by
# sanjeev2552
```

## java 描述语言

```
<script>

// JavaScript code for finding the
// maximum length of AP

function maxlenAP(a, n, d) {
    // key=starting element of an AP,
    // value=length of AP
    let m = new Map();

    // since the length of longest AP is at least
    // one i.e. the number itself.
    let maxt = 1;

    // if element a[i]'s starting element(i.e., a[i]-i*d)
    // is not in map then its value is 1 else there already
    // exists a starting element of an AP of which a[i]
    // can be a part.
    for (let i = 0; i < n; i++) {
        if (m.has(a[i] - i * d)) {
            m.set(a[i] - i * d, m.get(a[i] - i * d) + 1)
        } else {
            m.set(a[i] - i * d, 1)
        }
    }

    // auto operator stores the key,
    // value pair type from the map.
    for (let it of m)
        if (it[1] > maxt)

            // calculating the length of longest AP.
            maxt = it[1];

    return maxt;
}

// Driver code

let n = 10, d = 3;
let a = [1, 4, 2, 5, 20, 11, 56, 100, 20, 23];

document.write(maxlenAP(a, n, d) + "<br>");

</script>
```

**Output:** 

```
5
```
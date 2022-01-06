# 求积和最大等于 N 的 N 的四个因子|集合-2

> 原文:[https://www . geesforgeks . org/find-四因子 n 与最大积和等于 n-set-2/](https://www.geeksforgeeks.org/find-four-factors-of-n-with-maximum-product-and-sum-equal-to-n-set-2/)

给定一个整数![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")。任务是找到 N 的所有因子，打印 N 的四个因子的乘积，如:

*   四个因素之和等于 n。
*   四个因素的乘积最大。

如果找不到 4 个这样的因素，则打印**“不可能”**。
**注:**这四个因素可以互相等同，使产品最大化。
**示例** :

```
Input : N = 24
Output : Product -> 1296
All factors are -> 1 2 3 4 6 8 12 24 
Choose the factor 6 four times,
Therefore, 6+6+6+6 = 24 and product is maximum.

Input : N = 100
Output : Product -> 390625
All the factors are -> 1 2 4 5 10 10 20 25 50 100 
Choose the factor 25 four times.
```

一种采用 O(M^3 复杂度的方法),其中 m 是 n 的因子数，这在之前的文章中已经讨论过。
时间复杂度 O(N^2 的有效方法可以通过以下步骤获得。

*   将给定数量的所有因子存储在一个容器中。
*   对所有对进行迭代，并将它们的和存储在不同的容器中。
*   用对(element1，element2)标记索引(element1 + element2 ),以获得得出总和的元素。
*   对所有的 pair_sum 进行迭代，并检查 n-pair_sum 是否存在于同一个容器中，然后这两个对形成四元组。
*   使用配对散列数组来获取组成配对的元素。
*   存储所有这类四倍的最大值，并在最后打印出来。

以下是上述方法的实现:

## C++

```
// C++ program to find four factors of N
// with maximum product and sum equal to N
#include <bits/stdc++.h>

using namespace std;

// Function to find factors
// and to print those four factors
void findfactors(int n)
{
    unordered_map<int, int> mpp;

    vector<int> v, v1;

    // push all the factors in the container
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            v.push_back(i);
            if (i != (n / i) && i != 1)
                v.push_back(n / i);
        }
    }

    // number of factors
    int s = v.size();

    // Initial maximum
    int maxi = -1;

    // hash-array to mark the
    // pairs
    pair<int, int> mp1[n + 5];

    for (int i = 0; i < s; i++) {

        // form all the pair sums
        for (int j = i; j < s; j++) {

            // if the pair sum is less than n
            if (v[i] + v[j] < n) {

                // push in another container
                v1.push_back(v[i] + v[j]);

                // mark the sum with the elements
                // formed
                mp1[v[i] + v[j]] = { v[i], v[j] };

                // mark in the map that v[i]+v[j]
                // is present
                mpp[v[i] + v[j]] = 1;
            }
        }
    }

    // new size of all the pair sums
    s = v1.size();

    // iterate for all pair sum
    for (int i = 0; i < s; i++) {

        // the required part
        int el = n - (v1[i]);

        // if the required part is also
        // present in pair sum
        if (mpp[el] == 1) {

            // find the elements with
            // which the first pair is formed
            int a = mp1[v1[i]].first;
            int b = mp1[v1[i]].second;

            // find the elements with
            // which the second pair is formed
            int c = mp1[n - v1[i]].first;
            int d = mp1[n - v1[i]].second;

            // check for previous maximum
            maxi = max(a * b * c * d, maxi);
        }
    }

    if (maxi == -1)
        cout << "Not Possible\n";
    else {
        cout << "The maximum product is " << maxi << endl;
    }
}

// Driver code
int main()
{
    int n = 50;

    findfactors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find four factors of N
// with maximum product and sum equal to N
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to find factors
// and to print those four factors
static void findfactors(int n)
{
    HashMap<Integer,
            Integer> mpp = new HashMap<>();

    Vector<Integer> v = new Vector<Integer>(),
                   v1 = new Vector<Integer>();

    // push all the factors in the container
    for (int i = 1; i <= (int)Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {
            v.add(i);
            if (i != (n / i) && i != 1)
                v.add(n / i);
        }
    }

    // number of factors
    int s = v.size();

    // Initial maximum
    int maxi = -1;

    // hash-array to mark the
    // pairs
    int mp1_first[] = new int[n + 5],
        mp1_second[] = new int[n + 5];

    for (int i = 0; i < s; i++)
    {

        // form all the pair sums
        for (int j = i; j < s; j++)
        {

            // if the pair sum is less than n
            if (v.get(i) + v.get(j) < n)
            {

                // push in another container
                v1.add(v.get(i) + v.get(j));

                // mark the sum with the elements
                // formed
                mp1_first[v.get(i) +
                          v.get(j)] = v.get(i);
                mp1_second[v.get(i) +
                           v.get(j)] = v.get(j);

                // mark in the map that
                // v.get(i)+v.get(j) is present
                mpp.put(v.get(i) + v.get(j), 1);
            }
        }
    }

    // new size of all the pair sums
    s = v1.size();

    // iterate for all pair sum
    for (int i = 0; i < s; i++)
    {

        // the required part
        int el = n - (v1.get(i));

        // if the required part is also
        // present in pair sum
        if (mpp.get(el) != null)
        {

            // find the elements with
            // which the first pair is formed
            int a = mp1_first[v1.get(i)];
            int b = mp1_second[v1.get(i)];

            // find the elements with
            // which the second pair is formed
            int c = mp1_first[n - v1.get(i)];
            int d = mp1_second[n - v1.get(i)];

            // check for previous maximum
            maxi = Math.max(a * b * c * d, maxi);
        }
    }

    if (maxi == -1)
        System.out.println("Not Possible");
    else
    {
        System.out.println("The maximum product" +
                                   " is " + maxi);
    }
}

// Driver code
public static void main(String args[])
{
    int n = 50;

    findfactors(n);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find four factors of N
# with maximum product and sum equal to N
from math import sqrt, ceil, floor

# Function to find factors
# and to prthose four factors
def findfactors(n):
    mpp = dict()

    v = []
    v1 = []

    # push all the factors in the container
    for i in range(1,ceil(sqrt(n)) + 1):
        if (n % i == 0):
            v.append(i)
            if (i != (n // i) and i != 1):
                v.append(n // i)

    # number of factors
    s = len(v)

    # Initial maximum
    maxi = -1

    # hash-array to mark the
    # pairs
    mp1 = [0]*(n + 5)

    for i in range(s):

        # form all the pair sums
        for j in range(i, s):

            # if the pair sum is less than n
            if (v[i] + v[j] < n):

                # push in another container
                v1.append(v[i] + v[j])

                # mark the sum with the elements
                # formed
                mp1[v[i] + v[j]] =[v[i], v[j]]

                # mark in the map that v[i]+v[j]
                # is present
                mpp[v[i] + v[j]] = 1

    # new size of all the pair sums
    s = len(v1)

    # iterate for all pair sum
    for i in range(s):

        # the required part
        el = n - (v1[i])

        # if the required part is also
        # present in pair sum
        if (el in mpp):

            # find the elements with
            # which the first pair is formed
            a = mp1[v1[i]][0]
            b = mp1[v1[i]][1]

            # find the elements with
            # which the second pair is formed
            c = mp1[n - v1[i]][0]
            d = mp1[n - v1[i]][1]

            # check for previous maximum
            maxi = max(a * b * c * d, maxi)

    if (maxi == -1):
        print("Not Possible")
    else :
        print("The maximum product is ", maxi)

# Driver code
n = 50

findfactors(n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find four factors of N
// with maximum product and sum equal to N
using System;
using System.Collections.Generic;

class GFG
{

// Function to find factors
// and to print those four factors
static void findfactors(int n)
{
    Dictionary<int,
            int> mpp = new Dictionary<int,int>();

    List<int> v = new List<int>(),
                v1 = new List<int>();

    // push all the factors in the container
    for (int i = 1; i <= (int)Math.Sqrt(n); i++)
    {
        if (n % i == 0)
        {
            v.Add(i);
            if (i != (n / i) && i != 1)
                v.Add(n / i);
        }
    }

    // number of factors
    int s = v.Count;

    // Initial maximum
    int maxi = -1;

    // hash-array to mark the
    // pairs
    int []mp1_first = new int[n + 5];
    int []mp1_second = new int[n + 5];

    for (int i = 0; i < s; i++)
    {

        // form all the pair sums
        for (int j = i; j < s; j++)
        {

            // if the pair sum is less than n
            if (v[i] + v[j] < n)
            {

                // push in another container
                v1.Add(v[i] + v[j]);

                // mark the sum with the elements
                // formed
                mp1_first[v[i] +
                        v[j]] = v[i];
                mp1_second[v[i] +
                        v[j]] = v[j];

                // mark in the map that
                // v[i]+v[j] is present
                mpp.Add(v[i] + v[j], 1);
            }
        }
    }

    // new size of all the pair sums
    s = v1.Count;

    // iterate for all pair sum
    for (int i = 0; i < s; i++)
    {

        // the required part
        int el = n - (v1[i]);

        // if the required part is also
        // present in pair sum
        if (mpp.ContainsKey(el))
        {

            // find the elements with
            // which the first pair is formed
            int a = mp1_first[v1[i]];
            int b = mp1_second[v1[i]];

            // find the elements with
            // which the second pair is formed
            int c = mp1_first[n - v1[i]];
            int d = mp1_second[n - v1[i]];

            // check for previous maximum
            maxi = Math.Max(a * b * c * d, maxi);
        }
    }

    if (maxi == -1)
        Console.WriteLine("Not Possible");
    else
    {
        Console.WriteLine("The maximum product" +
                                " is " + maxi);
    }
}

// Driver code
public static void Main(String []args)
{
    int n = 50;

    findfactors(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find four factors of N
// with maximum product and sum equal to N

// Function to find factors
// and to print those four factors
function findfactors(n)
{
    let mpp = new Map();

    let v = [];
    let v1 = [];

    // push all the factors in the container
    for (let i = 1; i <= Math.floor(Math.sqrt(n)); i++)
    {
        if (n % i == 0)
        {
            v.push(i);
            if (i != Math.floor(n / i) && i != 1)
                v.push(Math.floor(n / i));
        }
    }

    // number of factors
    let s = v.length;

    // Initial maximum
    let maxi = -1;

    // hash-array to mark the
    // pairs
    let mp1_first = new Array(n + 5),
        mp1_second = new Array(n + 5);

    for (let i = 0; i < s; i++)
    {

        // form all the pair sums
        for (let j = i; j < s; j++)
        {

            // if the pair sum is less than n
            if (v[i] + v[j] < n)
            {

                // push in another container
                v1.push(v[i] + v[j]);

                // mark the sum with the elements
                // formed
                mp1_first[v[i] +
                          v[j]] = v[i];
                mp1_second[v[i] +
                           v[j]] = v[j];

                // mark in the map that
                // v.get(i)+v.get(j) is present
                mpp.set(v[i] + v[j], 1);
            }
        }
    }

    // new size of all the pair sums
    s = v1.length;

    // iterate for all pair sum
    for (let i = 0; i < s; i++)
    {

        // the required part
        let el = n - (v1[i]);

        // if the required part is also
        // present in pair sum
        if (mpp.get(el) != null)
        {

            // find the elements with
            // which the first pair is formed
            let a = mp1_first[v1[i]];
           let b = mp1_second[v1[i]];

            // find the elements with
            // which the second pair is formed
            let c = mp1_first[n - v1[i]];
            let d = mp1_second[n - v1[i]];

            // check for previous maximum
            maxi = Math.max(a * b * c * d, maxi);
        }
    }

    if (maxi == -1)
        document.write("Not Possible<br>");
    else
    {
        document.write("The maximum product" +
                                   " is " + maxi);
    }
}

// Driver code
let n = 50;
findfactors(n);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
The maximum product is 12500
```
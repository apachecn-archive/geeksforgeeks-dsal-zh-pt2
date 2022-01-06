# 间隔内最大出现除数

> 原文:[https://www . geesforgeks . org/max-in-interval 除数/](https://www.geeksforgeeks.org/max-occurring-divisor-in-an-interval/)

给定一个区间[x，y]。在[x，y]范围内的除数中，找出除“1”外出现次数最多的除数。
**例:**

```
Input : [2, 5]
Output : 2
Explanation : Divisors of 2, 3, 4, 5 except 1 are:
              2 -> 2
              3 -> 3
              4 -> 2, 4
              5 -> 5
              Among all the divisors 2 occurs 
              maximum time, i.e two times.

Input : [3, 3]
Output : 3
```

**蛮力法**:最简单的方法是遍历从 x 到 y 的所有数字，计算它们的所有除数，并将除数和它们的计数存储在地图中。最后，遍历地图，找出除数出现的最大次数。你可以参考[](https://www.geeksforgeeks.org/find-divisors-natural-number-</br>set-1/”>this</a> article on how to efficiently print all divisors of a natural number.<br />Below is the implementation of above approach: <br /> </p>
<div class=)

## [c++](https://www.geeksforgeeks.org/find-divisors-natural-number-</br>set-1/”>this</a> article on how to efficiently print all divisors of a natural number.<br />Below is the implementation of above approach: <br /> </p>
<div class=)

```
// Simple CPP program to find maximum occurring
// factor in an interval
#include <bits/stdc++.h>
using namespace std;

// function to find max occurring
// divisor in interval [x, y]
int findDivisor(int x, int y)
{
    // map to store count of divisors
    unordered_map<int, int> m;

    // iterate for every number in the
    // interval
    for (int num = x; num <= y; num++) {
        // find all divisors of num
        for (int i = 2; i <= sqrt(num) + 1; i++) {
            if (num % i == 0) {

                // If divisors are equal, print only one
                if (num / i == i) {
                    if (m.find(i) == m.end())
                        m.insert(make_pair(i, 1));
                    else
                        m[i]++;
                }
                else {

                    // insert first one to map
                    if (m.find(i) == m.end())
                        m.insert(make_pair(i, 1));
                    else
                        m[i]++;

                    // insert second to map
                    if (m.find(num / i) == m.end())
                        m.insert(make_pair(num / i, 1));
                    else
                        m[num / i]++;
                }
            }
        }
    }

    int divisor = 0;
    int divisorCount = INT_MIN;

    // iterate on map
    for (auto itr = m.begin(); itr != m.end(); itr++) {
        if (itr->second > divisorCount) {
            divisorCount = itr->second;
            divisor = itr->first;
        }
    }

    return divisor;
}

// Driver code
int main()
{
    int x = 3, y = 16;
    cout << findDivisor(x, y);
    return 0;
}
```

## [Java](https://www.geeksforgeeks.org/find-divisors-natural-number-</br>set-1/”>this</a> article on how to efficiently print all divisors of a natural number.<br />Below is the implementation of above approach: <br /> </p>
<div class=)

```
// Java program to find Max
// occurring divisor in an interval
import java.io.*;
import java.util.*;

class GFG {

// function to find max occurring
// divisor in interval [x, y]
static int findDivisor(int x, int y)
{
    // map to store count of divisors
    HashMap<Integer, Integer> m = new HashMap<Integer,
                                            Integer>();

    // iterate for every number
    // in the interval
    for (int num = x; num <= y; num++) {

        // find all divisors of num
        for (int i = 2; i <= Math.sqrt(num) + 1; i++) {
            if (num % i == 0) {

                // If divisors are equal,
                // print only one
                if (num / i == i) {
                    if (m.containsKey(i) != true)
                        m.put(i, 1);
                    else
                        {
                            int val = m.get(i);
                            m.put(i, ++val);
                        }
                }
                else {

                    // insert first one to map
                    if (m.containsKey(i) != true)
                        m.put(i, 1);
                    else
                        {
                            int val=m.get(i);
                            m.put(i,++val);
                        }

                    // insert second to map
                    if (m.containsKey(num / i) != true)
                        m.put(num / i, 1);
                    else
                        {
                            int k = num / i;
                            int val = m.get(k);
                            m.put( k, ++val);
                        }
                }
            }
        }
    }

    int divisor = 0;
    int divisorCount = Integer.MIN_VALUE;

    // iterate on map
    for(Map.Entry<Integer, Integer> entry:m.entrySet()){
        int key = entry.getKey();
        int value = entry.getValue();

        if (value > divisorCount) {
            divisorCount = value;
            divisor = key;
        }
    }

    return divisor;
}

/* Driver program to test above function */
public static void main(String[] args)
{
    int x = 3, y = 16;
    System.out.println(findDivisor(x, y));
}
}

// This code is contributed by Gitanjali
```

## [Python](https://www.geeksforgeeks.org/find-divisors-natural-number-</br>set-1/”>this</a> article on how to efficiently print all divisors of a natural number.<br />Below is the implementation of above approach: <br /> </p>
<div class=)

```
# Simple python program to find maximum
# occurring factor in an interval
import math

# Function to find max occurring
# divisor in interval [x, y]
def findDivisor( x, y):
    # Map to store count of divisors
    m = {}

    # Iterate for every number in the interval
    for num in range(x, y + 1):

        # Find all divisors of num
        for i in range(2, int(math.sqrt(num)) + 2):
            if (num % i == 0):

                # If divisors are equal, print only one
                if (num / i == i):
                    if i not in m:
                        m[i]= 1
                    else:
                        m[i]+= 1

                else:
                    # Insert first one to map
                    if (i not in m):
                        m[i]= 1
                    else:
                        m[i]= m[i]+1

                    # Insert second to map
                    if (num / i not in m ):
                        m[num / i]= 1
                    else:
                        m[num / i]= m[num / i]+1

    divisor = 0
    divisorCount = -999999

    # Iterate on map
    for itr in m :
        if m[itr] > divisorCount:
            divisorCount = m[itr]
            divisor = itr

    return divisor

# Driver method
x = 3
y = 16
print (findDivisor(x, y))

# This code is contributed by 'Gitanjali'.
```

## [c#](https://www.geeksforgeeks.org/find-divisors-natural-number-</br>set-1/”>this</a> article on how to efficiently print all divisors of a natural number.<br />Below is the implementation of above approach: <br /> </p>
<div class=)

```
// C# program to find Max
// occurring divisor in an interval
using System;
using System.Collections.Generic;

class GFG
{

// function to find max occurring
// divisor in interval [x, y]
static int findDivisor(int x, int y)
{
    // map to store count of divisors
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    // iterate for every number
    // in the interval
    for (int num = x; num <= y; num++)
    {

        // find all divisors of num
        for (int i = 2; i <= Math.Sqrt(num) + 1; i++)
        {
            if (num % i == 0)
            {

                // If divisors are equal,
                // print only one
                if (num / i == i)
                {
                    if (m.ContainsKey(i) != true)
                        m.Add(i, 1);
                    else
                    {
                        int val = m[i];
                        m[i] = ++val;
                    }
                }
                else
                {

                    // insert first one to map
                    if (m.ContainsKey(i) != true)
                        m.Add(i, 1);
                    else
                    {
                        int val = m[i];
                        m[i] = ++val;
                    }

                    // insert second to map
                    if (m.ContainsKey(num / i) != true)
                        m.Add(num / i, 1);
                    else
                    {
                        int k = num / i;
                        int val = m[k];
                        m[k] = ++val;
                    }
                }
            }
        }
    }

    int divisor = 0;
    int divisorCount = int.MinValue;

    // iterate on map
    foreach(KeyValuePair<int, int> entry in m)
    {
        int key = entry.Key;
        int value = entry.Value;

        if (value > divisorCount)
        {
            divisorCount = value;
            divisor = key;
        }
    }

    return divisor;
}

// Driver Code
public static void Main(String[] args)
{
    int x = 3, y = 16;
    Console.WriteLine(findDivisor(x, y));
}
}

// This code is contributed by 29AjayKumar
```
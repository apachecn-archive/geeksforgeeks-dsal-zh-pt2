# 数组中每个元素前的倍数计数

> 原文:[https://www . geesforgeks . org/每元素前的数组倍数计数/](https://www.geeksforgeeks.org/count-of-multiples-in-an-array-before-every-element/)

给定一个大小为 **N** 的数组 **arr** ，任务是计算索引 **j (j < i)** 的数量，使得**a【I】**为所有有效索引 **i** 划分**a【j】**。
**示例:**

> **输入:** arr[] = {8，1，28，4，2，6，7}
> **输出:** 0，1，0，2，3，0，1
> 自身前各元素的倍数–
> N(8)= 0()
> N(1)= 1(8)
> N(28)= 0()
> N(4)= 2(28，8)
> N(2) = 3 (4，28)

**简单方法:**遍历所有有效指数 **j，范围为【0，i-1】，**每个指数**I**；并计算每个索引的除数。
*时间复杂度:**O(N<sup>2</sup>)***
*空间复杂度: **O(1)***
**高效途径:**这种途径就是使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。遍历数组时，增加映射中因子的计数，并在映射中查找该计数，以找到所有有效的 **j ( < i)** ，而无需往回遍历。
以下是上述办法的实施情况。

## C++

```
// C++ program to count of multiples
// in an Array before every element

#include <bits/stdc++.h>
using namespace std;

// Function to find all factors of N
// and keep their count in map
void add_factors(int n,
                 unordered_map<int, int>& mp)
{
    // Traverse from 1 to sqrt(N)
    // if i divides N,
    // increment i and N/i in map
    for (int i = 1; i <= int(sqrt(n)); i++) {
        if (n % i == 0) {
            if (n / i == i)
                mp[i]++;
            else {
                mp[i]++;
                mp[n / i]++;
            }
        }
    }
}

// Function to count of multiples
// in an Array before every element
void count_divisors(int a[], int n)
{

    // To store factors all of all numbers
    unordered_map<int, int> mp;

    // Traverse for all possible i's
    for (int i = 0; i < n; i++) {
        // Printing value of a[i] in map
        cout << mp[a[i]] << " ";

        // Now updating the factors
        // of a[i] in the map
        add_factors(a[i], mp);
    }
}

// Driver code
int main()
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    count_divisors(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of multiples
// in an Array before every element
import java.util.*;

class GFG{

// Function to find all factors of N
// and keep their count in map
static void add_factors(int n,
                 HashMap<Integer,Integer> mp)
{
    // Traverse from 1 to Math.sqrt(N)
    // if i divides N,
    // increment i and N/i in map
    for (int i = 1; i <= (Math.sqrt(n)); i++) {
        if (n % i == 0) {
            if (n / i == i) {
                if(mp.containsKey(i))
                    mp.put(i, mp.get(i) + 1);
                else
                    mp.put(i, 1);
            }
            else {
                if(mp.containsKey(i))
                    mp.put(i, mp.get(i) + 1);
                else
                    mp.put(i, 1);
                if(mp.containsKey(n / i))
                    mp.put(n / i, mp.get(n / i) + 1);
                else
                    mp.put(n / i, 1);
            }
        }
    }
}

// Function to count of multiples
// in an Array before every element
static void count_divisors(int a[], int n)
{

    // To store factors all of all numbers
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Traverse for all possible i's
    for (int i = 0; i < n; i++) {
        // Printing value of a[i] in map
        System.out.print(mp.get(a[i]) == null ? 0 + " " : mp.get(a[i]) + " ");

        // Now updating the factors
        // of a[i] in the map
        add_factors(a[i], mp);
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.length;

    // Function call
    count_divisors(arr, n);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to count of multiples
# in an Array before every element
from collections import defaultdict
import math

# Function to find all factors of N
# and keep their count in map
def add_factors(n, mp):

    # Traverse from 1 to sqrt(N)
    # if i divides N,
    # increment i and N/i in map
    for i in range(1, int(math.sqrt(n)) + 1,):
        if (n % i == 0):
            if (n // i == i):
                mp[i] += 1
            else :
                mp[i] += 1
                mp[n // i] += 1

# Function to count of multiples
# in an Array before every element
def count_divisors(a, n):

    # To store factors all of all numbers
    mp = defaultdict(int)

    # Traverse for all possible i's
    for i in range(n) :
        # Printing value of a[i] in map
        print(mp[a[i]], end=" ")

        # Now updating the factors
        # of a[i] in the map
        add_factors(a[i], mp)

# Driver code
if __name__ == "__main__":

    arr = [ 8, 1, 28, 4, 2, 6, 7 ]
    n = len(arr)

    # Function call
    count_divisors(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# program to count of multiples
// in an Array before every element
using System;
using System.Collections.Generic;

class GFG{

// Function to find all factors of N
// and keep their count in map
static void add_factors(int n,
                 Dictionary<int,int> mp)
{
    // Traverse from 1 to Math.Sqrt(N)
    // if i divides N,
    // increment i and N/i in map
    for (int i = 1; i <= (Math.Sqrt(n)); i++) {
        if (n % i == 0) {
            if (n / i == i) {
                if(mp.ContainsKey(i))
                    mp[i] = mp[i] + 1;
                else
                    mp.Add(i, 1);
            }
            else {
                if(mp.ContainsKey(i))
                    mp[i] = mp[i] + 1;
                else
                    mp.Add(i, 1);
                if(mp.ContainsKey(n / i))
                    mp[n / i] = mp[n / i] + 1;
                else
                    mp.Add(n / i, 1);
            }
        }
    }
}

// Function to count of multiples
// in an Array before every element
static void count_divisors(int []a, int n)
{

    // To store factors all of all numbers
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Traverse for all possible i's
    for (int i = 0; i < n; i++) {
        // Printing value of a[i] in map
        Console.Write(!mp.ContainsKey(a[i]) ? 0 + " " : mp[a[i]] + " ");

        // Now updating the factors
        // of a[i] in the map
        add_factors(a[i], mp);
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.Length;

    // Function call
    count_divisors(arr, n);

}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to count of multiples
// in an Array before every element

// Function to find all factors of N
// and keep their count in map
function add_factors(n, mp)
{

    // Traverse from 1 to sqrt(N)
    // if i divides N,
    // increment i and N/i in map
    for (var i = 1; i <= parseInt(Math.sqrt(n)); i++) {
        if (n % i == 0) {
            if (parseInt(n / i) == i)
            {
                if(mp.has(i))
                    mp.set(i, mp.get(i)+1)
                else
                    mp.set(i, 1)
            }
            else {

                if(mp.has(i))
                    mp.set(i, mp.get(i)+1)
                else
                    mp.set(i, 1)

                if(mp.has(parseInt(n/i)))
                    mp.set(parseInt(n/i), mp.get(parseInt(n/i))+1)
                else
                    mp.set(parseInt(n/i), 1)

            }
        }
    }
    return mp;
}

// Function to count of multiples
// in an Array before every element
function count_divisors(a, n)
{

    // To store factors all of all numbers
    var mp = new Map();

    // Traverse for all possible i's
    for (var i = 0; i < n; i++)
    {

        // Printing value of a[i] in map
        document.write( (mp.has(a[i])?mp.get(a[i]):0) + " ");

        // Now updating the factors
        // of a[i] in the map
        mp = add_factors(a[i], mp);

    }
}

// Driver code
var arr = [8, 1, 28, 4, 2, 6, 7];
var n = arr.length;

// Function call
count_divisors(arr, n);

// This code is contributed by famously.
</script>
```

**Output:** 

```
0 1 0 2 3 0 1
```

***时间复杂度:** O(N * sqrt(N))*

***辅助空间:**O(N)*T4】
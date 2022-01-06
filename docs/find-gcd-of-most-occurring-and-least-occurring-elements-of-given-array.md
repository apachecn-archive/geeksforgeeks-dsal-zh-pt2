# 找出给定数组中出现次数最多和最少的元素的 GCD

> 原文:[https://www . geesforgeks . org/find-gcd-给定数组中出现次数最多和出现次数最少的元素/](https://www.geeksforgeeks.org/find-gcd-of-most-occurring-and-least-occurring-elements-of-given-array/)

给定一个大小为 **n** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在给定数组中找到[最高和最低频率元素的](https://www.geeksforgeeks.org/difference-between-highest-and-least-frequencies-in-an-array/) [GCD](http://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。

**示例:**

> **输入:** arr[] = {2，2，4，4，5，5，6，6，6}
> **输出:** 2
> **解释:**上述数组中元素的频率为
> freq(2) = 2，
> freq(4) = 2，
> freq(5) = 2，
> freq(6) = 4，
> 最小频率为 2(元素 2，4 因此 2 将被选为 2、4 和 5 中最少的。
> 最大频率为 4(元素 6)。
> 因此 GCD 为 2 和 6 = gcd(2，6)为 2。
> 
> **输入:** arr[] = {3，2，2，44，44，44，44}
> **输出:** 1

**方法:**思路是[统计所有元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)和[将它们存储在一个向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，然后找到出现频率最高和最少的元素的 gcd。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find frequency and find gcd
int find_gcd(vector<int> v, int n)
{
    map<int, int> mp;

    // Update the frequency
    for (int i = 0; i < n; i++) {
        mp[v[i]]++;
    }

    int mini = v[0], maxi = v[0];

    for (auto it : mp) {
        mini = mp[mini] < it.second
                   ? it.first
                   : mini;
    }
    for (auto it : mp) {
        maxi = mp[maxi] > it.second
                   ? it.first
                   : maxi;
    }

    // Find gcd
    int res = __gcd(mini, maxi);
    return res;
}

// Drive Code
int main()
{
    vector<int> v = { 2, 2, 4, 4, 5, 5, 6, 6, 6, 6 };
    int n = v.size();
    cout << find_gcd(v, n) << endl;

    vector<int> v1 = { 3, 2, 2, 44, 44, 44, 44 };
    cout << find_gcd(v1, v1.size()) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find frequency and find gcd
static int find_gcd(int []v, int n)
{
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Update the frequency
    for (int i = 0; i < n; i++) {
         if(mp.containsKey(v[i])){
                mp.put(v[i], mp.get(v[i])+1);
            }
            else{
                mp.put(v[i], 1);
            }
    }

    int mini = v[0], maxi = v[0];

    for (Map.Entry<Integer,Integer> it : mp.entrySet()) {
        mini = mp.get(mini) < it.getValue()
                   ? it.getKey()
                   : mini;
    }
    for (Map.Entry<Integer,Integer> it : mp.entrySet()) {
        maxi = mp.get(maxi) > it.getValue()
                   ? it.getKey()
                   : maxi;
    }

    // Find gcd
    int res = __gcd(mini, maxi);
    return res;
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Drive Code
public static void main(String[] args)
{
    int [] v = { 2, 2, 4, 4, 5, 5, 6, 6, 6, 6 };
    int n = v.length;
    System.out.print(find_gcd(v, n) +"\n");

    int [] v1 = { 3, 2, 2, 44, 44, 44, 44 };
    System.out.print(find_gcd(v1, v1.length) +"\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function to find frequency and find gcd
def find_gcd(v, n):

    mp = {}

    # Update the frequency
    for i in range(0, n):
        if v[i] in mp:
            mp[v[i]] += 1
        else:
            mp[v[i]] = 1

    mini = v[0]
    maxi = v[0]

    for it in mp:
        if mini in mp and mp[mini] < mp[it]:
            mini = it

    for it in mp:
        if mp[maxi] > mp[it]:
            maxi = it

        # Find gcd
    res = math.gcd(mini, maxi)
    return res

# Drive Code
if __name__ == "__main__":

    v = [2, 2, 4, 4, 5, 5, 6, 6, 6, 6]
    n = len(v)
    print(find_gcd(v, n))

    v1 = [3, 2, 2, 44, 44, 44, 44]
    print(find_gcd(v1, len(v1)))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to find frequency and find gcd
    static int find_gcd(int[] v, int n)
    {
        Dictionary<int, int> mp
            = new Dictionary<int, int>();

        // Update the frequency
        for (int i = 0; i < n; i++) {
            if (mp.ContainsKey(v[i])) {
                mp[v[i]] += 1;
            }
            else {
                mp[v[i]] = 1;
            }
        }

        int mini = v[0], maxi = v[0];

        foreach(KeyValuePair<int, int> it in mp)
        {
            mini = mp[mini] < it.Value ? it.Key : mini;
        }
        foreach(KeyValuePair<int, int> it in mp)
        {
            maxi = mp[maxi] > it.Value ? it.Key : maxi;
        }

        // Find gcd
        int res = __gcd(mini, maxi);
        return res;
    }

    // Drive Code
    public static void Main()
    {
        int[] v = { 2, 2, 4, 4, 5, 5, 6, 6, 6, 6 };
        int n = v.Length;
        Console.WriteLine(find_gcd(v, n));

        int[] v1 = { 3, 2, 2, 44, 44, 44, 44 };
        Console.WriteLine(find_gcd(v1, v1.Length));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach
       function __gcd(a, b) {
           // Everything divides 0
           if (a == 0)
               return b;
           if (b == 0)
               return a;

           // base case
           if (a == b)
               return a;

           // a is greater
           if (a > b)
               return __gcd(a - b, b);
           return __gcd(a, b - a);
       }
       // Function to find frequency and find gcd
       function find_gcd(v, n) {
           let mp = new Map();

           // Update the frequency
           for (let i = 0; i < n; i++) {

               if (!mp.has(v[i]))
                   mp.set(v[i], 1);
               else
                   mp.set(v[i], mp.get(v[i]) + 1)
           }

           let mini = v[0], maxi = v[0];

           for (let [key, val] of mp) {
               mini = mp.get(mini) < val
                   ? key
                   : mini;
           }
           for (let [key, val] of mp) {
               maxi = mp.get(maxi) > val
                   ? key
                   : maxi;
           }

           // Find gcd
           let res = __gcd(mini, maxi);
           return res;
       }

       // Drive Code
       let v = [2, 2, 4, 4, 5, 5, 6, 6, 6, 6];
       let n = v.length;
       document.write(find_gcd(v, n) + '<br>');

       let v1 = [3, 2, 2, 44, 44, 44, 44];
       document.write(find_gcd(v1, v1.length) + '<br>');

 // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
2
1
```

***时间复杂度:** O(n*log(n))*
***辅助空间:** O(n)*
# 尽量减少具有不同奇偶校验的相邻对的数量

> 原文:[https://www . geeksforgeeks . org/最小化具有不同奇偶校验的相邻对的数量/](https://www.geeksforgeeks.org/minimize-the-count-of-adjacent-pairs-with-different-parity/)

给定一个大小为 **N** 的数组 **arr** ，该数组包含剩余索引中的范围**【1，N】**和 **-1** 中的一些整数，任务是用来自**【1，N】**的剩余整数替换 **-1** ，使得具有不同奇偶性的相邻元素对的计数最小化。

**示例:**

> **输入:** arr = {-1，5，-1，2，3}
> **输出:** 2
> **解释:**
> 将元素替换为{1 5 4 2 3}后，我们得到的计数等于 2，因为只有(5，4)和(2，3)是具有不同奇偶性的相邻元素对。
> 
> **输入:** ar = {1，-1，-1，5，-1，-1，2}
> **输出:** 1
> **解释:**
> 通过替换数组元素得到{1，3，7，5，6，4，2}我们只得到一对奇偶性不同的相邻元素(5，6)。

**进场:**这个问题可以[递归](https://www.geeksforgeeks.org/recursion/)解决。计算数组中不存在的偶数和奇数，并在数组中逐一替换，递归计算不同奇偶性的最小相邻对。

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Recursive function to calculate
// minimum adjacent pairs
// with different parity
void parity(vector<int> even,
            vector<int> odd,
            vector<int> v,
            int i, int& min)
{
    // If all the numbers are placed
    if (i == v.size()
        || even.size() == 0
               && odd.size() == 0) {
        int count = 0;

        for (int j = 0; j < v.size() - 1; j++) {
            if (v[j] % 2 != v[j + 1] % 2)
                count++;
        }
        if (count < min)
            min = count;
        return;
    }

    // If replacement is not required
    if (v[i] != -1)
        parity(even, odd, v, i + 1, min);

    // If replacement is required
    else {
        if (even.size() != 0) {
            int x = even.back();
            even.pop_back();
            v[i] = x;

            parity(even, odd, v, i + 1, min);

            // backtracking
            even.push_back(x);
        }

        if (odd.size() != 0) {
            int x = odd.back();
            odd.pop_back();
            v[i] = x;

            parity(even, odd, v, i + 1, min);

            // backtracking
            odd.push_back(x);
        }
    }
}

// Function to display the minimum number of
// adjacent elements with different parity
void minDiffParity(vector<int> v, int n)
{
    // Store no of even numbers
    // not present in the array
    vector<int> even;

    // Store no of odd numbers
    // not present in the array
    vector<int> odd;

    unordered_map<int, int> m;

    for (int i = 1; i <= n; i++)
        m[i] = 1;

    for (int i = 0; i < v.size(); i++) {

        // Erase exisiting numbers
        if (v[i] != -1)
            m.erase(v[i]);
    }

    // Store non-exisiting
    // even and odd numbers
    for (auto i : m) {
        if (i.first % 2 == 0)
            even.push_back(i.first);
        else
            odd.push_back(i.first);
    }

    int min = 1000;
    parity(even, odd, v, 0, min);
    cout << min << endl;
}

// Driver code
int main()
{
    int n = 8;
    vector<int> v = { 2, 1, 4, -1,
                      -1, 6, -1, 8 };
    minDiffParity(v, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach 
import java.util.*;
public class Main
{
    static int min;

    // Recursive function to calculate 
    // minimum adjacent pairs with 
    // different parity 
    static void parity(List<Integer> even, 
                       List<Integer> odd, 
                       List<Integer> v, 
                       int i) 
    { 

        // If all the numbers are placed 
        if (i == v.size() || even.size() == 0 && 
            odd.size() == 0) 
        {
            int count = 0; 

            for(int j = 0; j < v.size() - 1; j++)
            {
                if (v.get(j) % 2 != v.get(j + 1) % 2) 
                    count++; 
            } 
            if (count < min) 
                min = count; 

            return; 
        } 

        // If replacement is not required 
        if (v.get(i) != -1) 
            parity(even, odd, v, i + 1); 

        // If replacement is required 
        else
        {
            if (even.size() != 0)
            { 
                int x = even.get(even.size() - 1); 
                even.remove(even.size() - 1); 
                v.set(i,x); 

                parity(even, odd, v, i + 1); 

                // Backtracking 
                even.add(x); 
            } 

            if (odd.size() != 0)
            { 
                int x = odd.get(odd.size() - 1); 
                odd.remove(odd.size() - 1); 
                v.set(i, x); 

                parity(even, odd, v, i + 1); 

                // Backtracking 
                odd.add(x); 
            } 
        } 
    } 

    // Function to display the minimum number of 
    // adjacent elements with different parity 
    static void minDiffParity(List<Integer> v, int n) 
    { 

        // Store no of even numbers 
        // not present in the array 
        List<Integer> even = new ArrayList<Integer>(); 

        // Store no of odd numbers 
        // not present in the array 
        List<Integer> odd = new ArrayList<Integer>(); 

        HashMap<Integer, Integer> m = new HashMap<>(); 

        for(int i = 1; i <= n; i++)
        {
            if (m.containsKey(i))
            {
                m.replace(i, 1);
            }
            else
            {
                m.put(i, 1);
            }
        }

        for(int i = 0; i < v.size(); i++)
        { 

            // Erase exisiting numbers 
            if (v.get(i) != -1) 
                m.remove(v.get(i)); 
        } 

        // Store non-exisiting 
        // even and odd numbers 
        for (Map.Entry<Integer, Integer> i : m.entrySet()) 
        {
            if (i.getKey() % 2 == 0) 
            {
                even.add(i.getKey()); 
            }
            else
            {
                odd.add(i.getKey());
            }
        }

        min = 1000;
        parity(even, odd, v, 0); 
        System.out.println(min); 
    } 

    public static void main(String[] args) {
        int n = 8; 
        List<Integer> v = new ArrayList<Integer>(); 
        v.add(2);
        v.add(1);
        v.add(4);
        v.add(-1);
        v.add(-1);
        v.add(6);
        v.add(-1);
        v.add(8);

        minDiffParity(v, n); 
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of above approach
mn = 1000

# Recursive function to calculate
# minimum adjacent pairs
# with different parity
def parity(even,odd,v,i):
    global mn

    # If all the numbers are placed
    if (i == len(v) or len(even) == 0 or len(odd) == 0):
        count = 0

        for j in range(len(v)- 1):
            if (v[j] % 2 != v[j + 1] % 2):
                count += 1
        if (count < mn):
            mn = count
        return

    # If replacement is not required
    if (v[i] != -1):
        parity(even, odd, v, i + 1)

    # If replacement is required
    else:
        if (len(even) != 0):
            x = even[len(even) - 1]
            even.remove(even[len(even) - 1])
            v[i] = x

            parity(even, odd, v, i + 1)

            # backtracking
            even.append(x)

        if (len(odd) != 0):
            x = odd[len(odd) - 1]
            odd.remove(odd[len(odd) - 1])
            v[i] = x

            parity(even, odd, v, i + 1)

            # backtracking
            odd.append(x)

# Function to display the minimum number of
# adjacent elements with different parity
def mnDiffParity(v, n):
    global mn

    # Store no of even numbers
    # not present in the array
    even = []

    # Store no of odd numbers
    # not present in the array
    odd = []

    m = {i:0 for i in range(100)}

    for i in range(1, n + 1):
        m[i] = 1

    for i in range(len(v)):

        # Erase exisiting numbers
        if (v[i] != -1):
            m.pop(v[i])

    # Store non-exisiting
    # even and odd numbers
    for key in m.keys():
        if (key % 2 == 0):
            even.append(key)
        else:
            odd.append(key)

    parity(even, odd, v, 0)
    print(mn + 4)

# Driver code
if __name__ == '__main__':
    n = 8
    v = [2, 1, 4, -1,-1, 6, -1, 8]
    mnDiffParity(v, n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of above approach 
using System;
using System.Collections.Generic; 

class GFG{

static int min;

// Recursive function to calculate 
// minimum adjacent pairs with 
// different parity 
static void parity(List<int> even, 
                   List<int> odd, 
                   List<int> v, 
                   int i) 
{ 

    // If all the numbers are placed 
    if (i == v.Count || even.Count == 0 && 
        odd.Count == 0) 
    {
        int count = 0; 

        for(int j = 0; j < v.Count - 1; j++)
        {
            if (v[j] % 2 != v[j + 1] % 2) 
                count++; 
        } 
        if (count < min) 
            min = count; 

        return; 
    } 

    // If replacement is not required 
    if (v[i] != -1) 
        parity(even, odd, v, i + 1); 

    // If replacement is required 
    else 
    {
        if (even.Count != 0)
        { 
            int x = even[even.Count - 1]; 
            even.RemoveAt(even.Count - 1); 
            v[i] = x; 

            parity(even, odd, v, i + 1); 

            // Backtracking 
            even.Add(x); 
        } 

        if (odd.Count != 0)
        { 
            int x = odd[odd.Count - 1]; 
            odd.RemoveAt(odd.Count - 1); 
            v[i] = x; 

            parity(even, odd, v, i + 1); 

            // Backtracking 
            odd.Add(x); 
        } 
    } 
} 

// Function to display the minimum number of 
// adjacent elements with different parity 
static void minDiffParity(List<int> v, int n) 
{ 

    // Store no of even numbers 
    // not present in the array 
    List<int> even = new List<int>();

    // Store no of odd numbers 
    // not present in the array 
    List<int> odd = new List<int>();

    Dictionary<int, 
               int> m = new Dictionary<int, 
                                       int>();  

    for(int i = 1; i <= n; i++)
    {
        if (m.ContainsKey(i))
        {
            m[i] = 1;
        }
        else
        {
            m.Add(i, 1);
        }
    }

    for(int i = 0; i < v.Count; i++)
    { 

        // Erase exisiting numbers 
        if (v[i] != -1) 
            m.Remove(v[i]); 
    } 

    // Store non-exisiting 
    // even and odd numbers 
    foreach(KeyValuePair<int, int> i in m)
    {      
        if (i.Key % 2 == 0) 
        {
            even.Add(i.Key); 
        }
        else
        {
            odd.Add(i.Key);
        }
    } 

    min = 1000;
    parity(even, odd, v, 0); 
    Console.WriteLine(min); 
} 

// Driver Code
static void Main() 
{
    int n = 8; 
    List<int> v = new List<int>(); 
    v.Add(2);
    v.Add(1);
    v.Add(4);
    v.Add(-1);
    v.Add(-1);
    v.Add(6);
    v.Add(-1);
    v.Add(8);

    minDiffParity(v, n); 
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

var min = 10000;

// Recursive function to calculate
// minimum adjacent pairs
// with different parity
function parity(even, odd, v, i)
{

    // If all the numbers are placed
    if (i == v.length
        || even.length == 0
               && odd.length == 0) {
        var count = 0;

        for (var j = 0; j < v.length - 1; j++) {
            if (v[j] % 2 != v[j + 1] % 2)
                count++;
        }
        if (count < min)
            min = count;
        return min;
    }

    // If replacement is not required
    if (v[i] != -1)
        min = parity(even, odd, v, i + 1);

    // If replacement is required
    else {
        if (even.length != 0) {
            var x = even.back();
            even.pop();
            v[i] = x;

            min = parity(even, odd, v, i + 1);

            // backtracking
            even.push(x);
        }

        if (odd.length != 0) {
            var x = odd[odd.length-1];
            odd.pop();
            v[i] = x;

            min = parity(even, odd, v, i + 1);

            // backtracking
            odd.push(x);
        }
    }
    return min;
}

// Function to display the minimum number of
// adjacent elements with different parity
function minDiffParity(v, n)
{

    // Store no of even numbers
    // not present in the array
    var even = [];

    // Store no of odd numbers
    // not present in the array
    var odd = [];

    var m = new Map();

    for (var i = 1; i <= n; i++)
        m.set(i, 1);

    for (var i = 0; i < v.length; i++) {

        // Erase exisiting numbers
        if (v[i] != -1)
            m.delete(v[i]);
    }

    // Store non-exisiting
    // even and odd numbers
    m.forEach((value, key) => {

        if (i.first % 2 == 0)
            even.push(key);
        else
            odd.push(key);
    });

    min = parity(even, odd, v, 0);
    document.write( min );
}

// Driver code
var n = 8;
var v = [2, 1, 4, -1,
                  -1, 6, -1, 8];
minDiffParity(v, n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
6
```
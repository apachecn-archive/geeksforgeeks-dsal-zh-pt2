# 使用给定容量的箱子可能的最小堆数

> 原文:[https://www . geesforgeks . org/最小堆数-可能使用给定容量的箱子/](https://www.geeksforgeeks.org/minimum-number-of-stacks-possible-using-boxes-of-given-capacities/)

给定 **N** 个箱子，它们的容量表示箱子上面能容纳的箱子总数。只要每个箱子上面的箱子总数小于或等于其容量，您就可以将箱子一个叠在另一个上面。找出使用所有盒子可以制作的最小堆叠数量。

**示例:**

> **输入:** arr[] = {0，0，1，1，2}
> **输出:** 2
> 第一叠(从上到下):0 1 2
> 第二叠(从上到下):0 1
> 
> **输入:** arr[] = {1，1，4，4}
> **输出:** 1
> 所有的箱子都可以放在一堆。

**方法:**我们来看一张地图，其中地图[X]表示我们可以使用的容量为 X 的箱子数量。让我们一个接一个地建立堆栈。最初堆栈的大小为 0，然后我们遍历地图，贪婪地选择尽可能多的当前容量。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of minimum stacks
int countPiles(int n, int a[])
{

    // Keep track of occurrence
    // of each capacity
    map<int, int> occ;

    // Fill the occurrence map
    for (int i = 0; i < n; i++)
        occ[a[i]]++;

    // Number of piles is 0 initially
    int pile = 0;

    // Traverse occurrences in increasing
    // order of capacities.
    while (occ.size()) {

        // Adding a new pile
        pile++;
        int size = 0;
        unordered_set<int> toRemove;

        // Traverse all piles in increasing
        // order of capacities
        for (auto tm : occ) {
            int mx = tm.first;
            int ct = tm.second;

            // Number of boxes of capacity mx
            // that can be added to current pile
            int use = min(ct, mx - size + 1);

            // Update the occurrence
            occ[mx] -= use;

            // Update the size of the pile
            size += use;
            if (occ[mx] == 0)
                toRemove.insert(mx);
        }

        // Remove capacities that are
        // no longer available
        for (auto tm : toRemove)
            occ.erase(tm);
    }
    return pile;
}

// Driver code
int main()
{
    int a[] = { 0, 0, 1, 1, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countPiles(n, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;
import java.util.HashSet;

class GFG
{

    // Function to return the count
    // of minimum stacks
    static int countPiles(int n, int[] a)
    {

        // Keep track of occurrence
        // of each capacity
        HashMap<Integer,
                Integer> occ = new HashMap<>();

        // Fill the occurrence map
        for (int i = 0; i < n; i++)
            occ.put(a[i], occ.get(a[i]) == null ? 1 :
                          occ.get(a[i]) + 1);

        // Number of piles is 0 initially
        int pile = 0;

        // Traverse occurrences in increasing
        // order of capacities.
        while (!occ.isEmpty())
        {

            // Adding a new pile
            pile++;
            int size = 0;
            HashSet<Integer> toRemove = new HashSet<>();

            // Traverse all piles in increasing
            // order of capacities
            for (HashMap.Entry<Integer,
                               Integer> tm : occ.entrySet())
            {
                int mx = tm.getKey();
                int ct = tm.getValue();

                // Number of boxes of capacity mx
                // that can be added to current pile
                int use = Math.min(ct, mx - size + 1);

                // Update the occurrence
                occ.put(mx, occ.get(mx) - use);

                // Update the size of the pile
                size += use;
                if (occ.get(mx) == 0)
                    toRemove.add(mx);
            }

            // Remove capacities that are
            // no longer available
            for (int tm : toRemove)
                occ.remove(tm);
        }
        return pile;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 0, 0, 1, 1, 2 };
        int n = a.length;

        System.out.println(countPiles(n, a));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of minimum stacks
def countPiles(n, a):

    # Keep track of occurrence
    # of each capacity
    occ = dict()

    # Fill the occurrence map
    for i in a:
        if i in occ.keys():
            occ[i] += 1
        else:
            occ[i] = 1

    # Number of piles is 0 initially
    pile = 0

    # Traverse occurrences in increasing
    # order of capacities.
    while (len(occ) > 0):

        # Adding a new pile
        pile += 1
        size = 0
        toRemove = dict()

        # Traverse all piles in increasing
        # order of capacities
        for tm in occ:
            mx = tm
            ct = occ[tm]

            # Number of boxes of capacity mx
            # that can be added to current pile
            use = min(ct, mx - size + 1)

            # Update the occurrence
            occ[mx] -= use

            # Update the size of the pile
            size += use
            if (occ[mx] == 0):
                toRemove[mx] = 1

        # Remove capacities that are
        # no longer available
        for tm in toRemove:
            del occ[tm]

    return pile

# Driver code
a = [0, 0, 1, 1, 2]
n = len(a)
print(countPiles(n, a))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class GFG
{

  // Function to return the count
  // of minimum stacks
  static int countPiles(int n, int[] a)
  {

    // Keep track of occurrence
    // of each capacity
    Dictionary<int,
    int> occ = new Dictionary<int,int>();

    // Fill the occurrence map
    for (int i = 0; i < n; i++)
    {
      if(!occ.ContainsKey(a[i]))
      {
        occ[a[i]]=0;
      }

      occ[a[i]]++;
    }

    // Number of piles is 0 initially
    int pile = 0;

    // Traverse occurrences in increasing
    // order of capacities.
    while(occ.Count!=0)
    {

      // Adding a new pile
      pile++;
      int size = 0;
      HashSet<int> toRemove = new HashSet<int>();

      Dictionary<int,int> tmp = occ;

      // Traverse all piles in increasing
      // order of capacities
      foreach(var tm in occ.Keys.ToList())
      {
        int mx = tm;
        int ct = occ[tm];

        // Number of boxes of capacity mx
        // that can be added to current pile
        int use = Math.Min(ct, mx - size + 1);

        // Update the occurrence
        occ[mx]-= use;

        // Update the size of the pile
        size += use;

        if (occ[mx] == 0)
          toRemove.Add(mx);
      }

      occ = tmp;

      // Remove capacities that are
      // no longer available
      foreach(int tm in toRemove.ToList())
        occ.Remove(tm);
    }
    return pile;
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] a = { 0, 0, 1, 1, 2 };
    int n = a.Length;

    Console.WriteLine(countPiles(n, a));
  }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of minimum stacks
function countPiles(n, a)
{

    // Keep track of occurrence
    // of each capacity
    let occ = new Map();

    // Fill the occurrence map
    for(let i = 0; i < n; i++)
        occ.set(a[i], occ.get(a[i]) == null ? 1 :
                      occ.get(a[i]) + 1);

    // Number of piles is 0 initially
    let pile = 0;

    // Traverse occurrences in increasing
    // order of capacities.
    while (occ.size != 0)
    {

        // Adding a new pile
        pile++;
        let size = 0;
        let toRemove = new Set();

        // Traverse all piles in increasing
        // order of capacities
        for(let [key, value] of occ.entries())
        {
            let mx = key;
            let ct = value;

            // Number of boxes of capacity mx
            // that can be added to current pile
            let use = Math.min(ct, mx - size + 1);

            // Update the occurrence
            occ.set(mx, occ.get(mx) - use);

            // Update the size of the pile
            size += use;

            if (occ.get(mx) == 0)
                toRemove.add(mx);
        }

        // Remove capacities that are
        // no longer available
        for(let tm of toRemove.values())
            occ.delete(tm);
    }
    return pile;
}

// Driver Code
let a = [ 0, 0, 1, 1, 2 ];
let n = a.length;

document.write(countPiles(n, a));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(NlogN)
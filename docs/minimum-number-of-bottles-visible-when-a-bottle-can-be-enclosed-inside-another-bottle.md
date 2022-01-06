# 当一个瓶子可以装入另一个瓶子时可见的最小瓶子数量

> 原文:[https://www . geeksforgeeks . org/最小瓶子数量-当一个瓶子可以装入另一个瓶子时可见/](https://www.geeksforgeeks.org/minimum-number-of-bottles-visible-when-a-bottle-can-be-enclosed-inside-another-bottle/)

给定 N 瓶。第一个瓶子的半径为。一旦一个瓶子被封在另一个瓶子里，它就不再可见了。任务是尽量减少可见瓶子的数量。如果满足以下条件，您可以将 i <sup>th</sup> 瓶放入 j <sup>th</sup> 瓶。

1.  i <sup>第</sup>个瓶子本身没有封装在另一个瓶子中。
2.  j <sup>第</sup>个瓶子不包含任何其他瓶子。
3.  瓶子 I 的半径小于瓶子 j(即 A[i] < A[j])。

**例:**

```
Input :
8
1 1 2 3 4 5 5 4  
Output :
2
Explanation:
1 -> 2 [1, 2, 3, 4, 5, 5, 4]
2 -> 3 [1, 3, 4, 5, 5, 4]
3 -> 4 [1, 4, 5, 5, 4]
4 -> 5 [1, 5, 5, 4]
1 -> 4 [5, 5, 4]
4 -> 5 [5, 5]

Finally, there are 2 bottles
left which are visible. 
Hence the answer is 2\. 
```

**进场:**如果仔细观察，会发现最小可见瓶数将等于**最大重复瓶数**。直觉告诉我们，因为这些重复的瓶子不能装在一个更大的瓶子里，所以我们至少需要和重复瓶子数量一样多的更大的瓶子。
以下是上述方法的实施:

## C++

```
#include <bits/stdc++.h>
using namespace std;

void min_visible_bottles(int* arr, int n)
{
    map<int, int> m;
    int ans = 0;
    for (int i = 0; i < n; i++) {
        m[arr[i]]++;
        ans = max(ans, m[arr[i]]);
    }

    cout << "Minimum number of "
         << "Visible Bottles are: "
         << ans << endl;
}

// Driver code
int main()
{
    int n = 8;
    int arr[] = { 1, 1, 2, 3, 4, 5, 5, 4 };

    // Find the solution
    min_visible_bottles(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG
{
    static void min_visible_bottles(int[] arr, int n)
    {
        HashMap<Integer,
                Integer> mp = new HashMap<Integer,
                                          Integer>();
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            if (mp.containsKey(arr[i]))
            {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }
            else
            {
                mp.put(arr[i], 1);
            }
            ans = Math.max(ans, mp.get(arr[i]));
        }

        System.out.print("Minimum number of " +
                      "Visible Bottles are: " +
                                   ans + "\n");
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 8;
        int arr[] = { 1, 1, 2, 3, 4, 5, 5, 4 };

        // Find the solution
        min_visible_bottles(arr, n);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code for the above approach
def min_visible_bottles(arr, n):

    m = dict()
    ans = 0
    for i in range(n):
        m[arr[i]] = m.get(arr[i], 0) + 1
        ans = max(ans, m[arr[i]])

    print("Minimum number of",
          "Visible Bottles are: ", ans)

# Driver code
n = 8
arr = [1, 1, 2, 3, 4, 5, 5, 4]

# Find the solution
min_visible_bottles(arr, n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG
{
    static void min_visible_bottles(int[] arr, int n)
    {
        Dictionary<int,
                   int> mp = new Dictionary<int,
                                            int>();
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            if (mp.ContainsKey(arr[i]))
            {
                mp[arr[i]] = mp[arr[i]] + 1;
            }
            else
            {
                mp.Add(arr[i], 1);
            }
            ans = Math.Max(ans, mp[arr[i]]);
        }

        Console.Write("Minimum number of " +
                   "Visible Bottles are: " +
                                ans + "\n");
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 8;
        int []arr = { 1, 1, 2, 3, 4, 5, 5, 4 };

        // Find the solution
        min_visible_bottles(arr, n);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

function min_visible_bottles(arr, n) {
    let m = new Map();
    let ans = 0;
    for (let i = 0; i < n; i++) {
        if(m.has(arr[i])){
            m.set(arr[i], m.get(arr[i]) + 1)
        }else{
            m.set(arr[i], 1)
        }
        ans = Math.max(ans, m.get(arr[i]));
    }

    document.write("Minimum number of " +
    "Visible Bottles are: " + ans + "<br>");
}

// Driver code

    let n = 8;
    let arr = [1, 1, 2, 3, 4, 5, 5, 4];

    // Find the solution
    min_visible_bottles(arr, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
Minimum number of Visible Bottles are: 2
```
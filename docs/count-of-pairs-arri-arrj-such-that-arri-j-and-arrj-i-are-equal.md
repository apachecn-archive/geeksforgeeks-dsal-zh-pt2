# 对(arr[i]，arr[j])进行计数，使得 arr[i] + j 和 arr[j] + i 相等

> 原文:[https://www . geesforgeks . org/对计数-arri-arrj-这样-arri-j-和-arrj-I-相等/](https://www.geeksforgeeks.org/count-of-pairs-arri-arrj-such-that-arri-j-and-arrj-i-are-equal/)

给定一个数组 **arr[]** ，任务是计算成对的 **i，j** ，这样， **i < j** 和 **arr[i] + j = arr[j] + i** 。

**示例:**

> **输入:** arr[] = {4，1，2，3}
> **输出:** 3
> **说明:**总共有三对满足给定条件，它们是{1，2}、{2，3}和{1，3}。
> 那么，最终答案是 3。
> 
> **输入:** arr[] = {1，5，6 }
> T3】输出: 1

**天真方法:**解决这个问题的天真方法是针对给定条件检查数组中的每一对，并对这些对进行计数。

**时间复杂度:** O(N)，其中 N 是 arr[]的大小。
**辅助空间:** O(1)。

**高效途径:**这个问题可以通过使用 hashmaps 来解决。首先，我们可以扭曲给我们的条件，我们可以将 **arr[j] + i= arr[i]+ j** 改为**arr[j]–j = arr[I]–I，**这意味着两个不同的数字在值和指数上有相同的差异。这很容易，现在按照下面的步骤来解决给定的问题。

*   创建一个地图 **mp** 和一个变量，比如说 **ans = 0** ，来存储答案。
*   用说 I 遍历整个数组 **arr[]**
    *   对于每个元素，我们将找出其值和索引的差异，简单来说就是**a[I]–I**。
    *   如果地图上有某个值，这意味着还有其他数字具有相同的值，所以我们将把这些频率添加到答案中。
    *   增加**MP【a[I]–I]**的值。
*   返回 **ans** 作为最终答案。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs with given properties
int solve(int N, int arr[])
{
    // Map for the storing the frequency
    // of a given difference
    map<int, int> mp;

    // Variable to store the final ans
    int ans = 0;

    // Traverse the array and update mp
    for (int i = 0; i < N; i++) {
        ans += mp[arr[i] - i];
        mp[arr[i] - i]++;
    }

    // Return the final result
    return ans;
}

int main()
{
    int N = 4;
    int arr[] = { 4, 1, 2, 3 };

    // Print the result
    cout << solve(N, arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

// Function to count pairs with given properties
static int solve(int N, int arr[])
{

    // Map for the storing the frequency
    // of a given difference
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Variable to store the final ans
    int ans = 0;

    // Traverse the array and update mp
    for (int i = 0; i < N; i++) {
        if(mp.containsKey(arr[i]-i)){
            ans+=mp.get(arr[i]-i);
            mp.put(arr[i]-i, mp.get(arr[i]-i)+1);
        }
        else{
            mp.put(arr[i]-i, 1);
        }
    }

    // Return the final result
    return ans;
}

public static void main(String[] args)
{
    int N = 4;
    int arr[] = { 4, 1, 2, 3 };

    // Print the result
    System.out.print(solve(N, arr));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to count pairs with given properties
def solve(N, arr):

    # Map for the storing the frequency
    # of a given difference
    mp = dict()

    # Variable to store the final ans
    ans = 0

    # Traverse the array and update mp
    for i in range(N):

        if ((arr[i] - i) not in mp):
            mp[arr[i] - i] = 0

        ans += mp[arr[i] - i]
        mp[arr[i] - i] = mp[arr[i] - i] + 1

    # Return the final result
    return ans

N = 4
arr = [4, 1, 2, 3]

# Print the result
print(solve(N, arr))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
using System;
using System.Collections.Generic;

public class GFG{

// Function to count pairs with given properties
static int solve(int N, int []arr)
{

    // Map for the storing the frequency
    // of a given difference
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Variable to store the readonly ans
    int ans = 0;

    // Traverse the array and update mp
    for (int i = 0; i < N; i++) {
        if(mp.ContainsKey(arr[i]-i)){
            ans+=mp[arr[i]-i];
            mp[arr[i]-i]= mp[arr[i]-i]+1;
        }
        else{
            mp.Add(arr[i]-i, 1);
        }
    }

    // Return the readonly result
    return ans;
}

public static void Main(String[] args)
{
    int N = 4;
    int []arr = { 4, 1, 2, 3 };

    // Print the result
    Console.Write(solve(N, arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to count pairs with given properties
        function solve(N, arr)
        {

            // Map for the storing the frequency
            // of a given difference
            let mp = new Map();

            // Variable to store the final ans
            let ans = 0;

            // Traverse the array and update mp
            for (let i = 0; i < N; i++) {

                if (mp.has(arr[i] - i) == false) {
                    mp.set(arr[i] - i, 0)
                }
                ans += mp.get(arr[i] - i);
                mp.set(arr[i] - i, mp.get(arr[i] - i) + 1);
            }

            // Return the final result
            return ans;
        }

        let N = 4;
        let arr = [4, 1, 2, 3];

        // Print the result
        document.write(solve(N, arr));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
3
```

**时间复杂度:** ![O(N)          ](img/e1bf409fd0abdb6d36cc96c519a4f7cc.png "Rendered by QuickLaTeX.com")，其中 N 是数组的大小。

**辅助空间:** O(N)，其中 N 是数组的大小。
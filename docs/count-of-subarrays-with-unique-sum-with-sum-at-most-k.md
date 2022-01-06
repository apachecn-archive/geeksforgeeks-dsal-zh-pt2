# 和最多为 K 的唯一和的子阵计数

> 原文:[https://www . geeksforgeeks . org/带唯一和的子数组计数-最多和-k/](https://www.geeksforgeeks.org/count-of-subarrays-with-unique-sum-with-sum-at-most-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和一个整数 **K** 。，任务是最多用 sum**k**统计唯一和的子阵个数

**示例**:

> **输入** : N = 3，arr[] = {1，0，1}，K = 1
> **输出** : 3
> **解释**:所有子阵分别为[1]，[0]，[1]，0]，[0，1]，[1，0，1] &这些子阵的和分别为{1，0，1，1，1，2}。只有两个不同的可能和小于或等于 1
> **输入** : N = 1，arr[] = {1}，K = 0
> **输出** : 0

**逼近**:通过计算每个**子阵**的**和**并将其存储在 **HashMap** 中，即可解决任务。迭代 **HashMap** ，如果总和最多为 **K** ，则**递增**计数

下面是上述方法的实现

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the valid sums
void solve(int arr[], int n, int k)
{

    // Store the distinct subarray sums
    unordered_map<int, int> occ;

    int cur = 0;
    for (int i = 0; i < n; i++) {
        cur = 0;
        for (int j = i; j < n; j++) {
            cur += arr[j];
            occ[cur]++;
        }
    }

    // Stores the answer
    int ans = 0;
    for (auto x : occ) {
        if (x.first <= k)
            ans++;
    }

    cout << ans << endl;
}

// Driver Code
int main()
{
    int N = 3, K = 1;
    int arr[3] = { 1, 0, 1 };

    solve(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate the valid sums
static void solve(int arr[], int n, int k)
{

    // Store the distinct subarray sums
    HashMap<Integer,Integer> occ = new HashMap<Integer,Integer>();

    int cur = 0;
    for (int i = 0; i < n; i++) {
        cur = 0;
        for (int j = i; j < n; j++) {
            cur += arr[j];
            if(occ.containsKey(cur)){
                occ.put(cur, occ.get(cur)+1);
            }
            else{
                occ.put(cur, 1);
            }
        }
    }

    // Stores the answer
    int ans = 0;
    for (Map.Entry<Integer,Integer> x : occ.entrySet()) {
        if (x.getKey() <= k)
            ans++;
    }

    System.out.print(ans +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 3, K = 1;
    int arr[] = { 1, 0, 1 };

    solve(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for the above approach

# Function to calculate the valid sums
def solve(arr, n, k):

    # Store the distinct subarray sums
    occ = {}

    cur = 0
    for i in range(0, n):
        cur = 0
        for j in range(i, n):
            cur += arr[j]
            if cur in occ:
                occ[cur] += 1
            else:
                occ[cur] = 1

        # Stores the answer
    ans = 0
    for x in occ:
        if (x <= k):
            ans += 1

    print(ans)

# Driver Code
if __name__ == "__main__":
    N = 3
    K = 1

    arr = [1, 0, 1]
    solve(arr, N, K)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to calculate the valid sums
    static void solve(int[] arr, int n, int k)
    {

        // Store the distinct subarray sums
        Dictionary<int, int> occ
            = new Dictionary<int, int>();

        int cur = 0;
        for (int i = 0; i < n; i++) {
            cur = 0;
            for (int j = i; j < n; j++) {
                cur += arr[j];
                if (!occ.ContainsKey(cur))
                    occ[cur] = 0;
                else
                    occ[cur]++;
            }
        }

        // Stores the answer
        int ans = 0;
        foreach(KeyValuePair<int, int> x in occ)
        {
            if (x.Key <= k)
                ans++;
        }

        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main()
    {
        int N = 3, K = 1;
        int[] arr = { 1, 0, 1 };

        solve(arr, N, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript code for the above approach

// Function to calculate the valid sums
function solve(arr, n, k)
{

    // Store the distinct subarray sums
    let occ = new Map();

    let cur = 0;
    for(let i = 0; i < n; i++)
    {
        cur = 0;
        for(let j = i; j < n; j++)
        {
            cur += arr[j];
            if (occ.has(cur))
            {
                occ.set(cur, occ.get(cur) + 1)
            }
            else
            {
                occ.set(cur, 1);
            }
        }
    }

    // Stores the answer
    let ans = 0;
    for(let[key, value] of occ)
    {
        if (key <= k)
            ans++;
    }
    document.write(ans + '<br>');
}

// Driver Code
let N = 3, K = 1;
let arr = [ 1, 0, 1 ];

solve(arr, N, K);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
2
```

***时间复杂度***:O(N<sup>2</sup>)
***辅助空间*** : O(N)
# 对数组中的对进行计数，使得 LCM(arr[i]，arr[j]) > min(arr[i]，arr[j])

> 原文:[https://www . geesforgeks . org/count-pairs-in-in-a-array-arrj-minariarj/](https://www.geeksforgeeks.org/count-pairs-in-an-array-such-that-lcmarri-arrj-minarriarrj/)

给定一个数组 **arr[]** ，任务是找到数组中的对的计数，使得 **LCM(arr[i]，arr[j]) > min(arr[i]，arr[j])**
**注:** Pairs **(arr[i]，arr[j])** 和 **(arr[j]，arr[i])** 被认为是相同的，将只计数一次。

**示例:**

> **输入:** arr[] = {1，1，4，9}
> **输出:** 5
> 所有有效对为(1，4)、(1，9)、(1，4)、(1，9)和(4，9)。
> 
> **输入:** arr[] = {2，4，5，2，5，7，2，8 }
> T3】输出: 24

**方法:**观察到只有形式为 **(arr[i]，arr[j])** 的对 **arr[i] = arr[j]** 不满足给定条件。所以，现在问题简化为找到配对数 **(arr[i]，arr[j])** ，这样 **arr[i]！= arr[j]** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of valid pairs
int count_pairs(int n, int a[])
{
    // Store frequencies of array elements
    unordered_map<int, int> frequency;
    for (int i = 0; i < n; i++) {
        frequency[a[i]]++;
    }

    int count = 0;

    // Count of pairs (arr[i], arr[j])
    // where arr[i] = arr[j]
    for (auto x : frequency) {
        int f = x.second;
        count += f * (f - 1) / 2;
    }

    // Count of pairs (arr[i], arr[j]) where
    // arr[i] != arr[j], i.e. Total pairs - pairs
    // where arr[i] = arr[j]
    return ((n * (n - 1)) / 2) - count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 5, 2, 5, 7, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << count_pairs(n, arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;
import java.util.Map;

class GfG
{

    // Function to return the count of valid pairs
    static int count_pairs(int n, int a[])
    {
        // Store frequencies of array elements
        HashMap<Integer, Integer> frequency = new HashMap<>();
        for (int i = 0; i < n; i++)
        {

            if (!frequency.containsKey(a[i]))
                frequency.put(a[i], 0);
            frequency.put(a[i], frequency.get(a[i])+1);
        }

        int count = 0;

        // Count of pairs (arr[i], arr[j])
        // where arr[i] = arr[j]
        for (Map.Entry<Integer, Integer> x: frequency.entrySet())
        {
            int f = x.getValue();
            count += f * (f - 1) / 2;
        }

        // Count of pairs (arr[i], arr[j]) where
        // arr[i] != arr[j], i.e. Total pairs - pairs
        // where arr[i] = arr[j]
        return ((n * (n - 1)) / 2) - count;
    }

    // Driver code
    public static void main(String []args)
    {

        int arr[] = { 2, 4, 5, 2, 5, 7, 2, 8 };
        int n = arr.length;
        System.out.println(count_pairs(n, arr));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of valid pairs
def count_pairs(n, a) :

    # Store frequencies of array elements
    frequency = dict.fromkeys(a, 0)
    for i in range(n) :
        frequency[a[i]] += 1

    count = 0

    # Count of pairs (arr[i], arr[j])
    # where arr[i] = arr[j]
    for f in frequency.values() :
        count += f * (f - 1) // 2

    # Count of pairs (arr[i], arr[j]) where
    # arr[i] != arr[j], i.e. Total pairs - pairs
    # where arr[i] = arr[j]
    return ((n * (n - 1)) // 2) - count

# Driver Code
if __name__ == "__main__" :

    arr = [ 2, 4, 5, 2,
            5, 7, 2, 8 ]
    n = len(arr)
    print(count_pairs(n, arr))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GfG
{

    // Function to return the count of valid pairs
    static int count_pairs(int n, int []arr)
    {
        // Store frequencies of array elements
        Dictionary<int,int> mp = new Dictionary<int,int>();
        for (int i = 0 ; i < n; i++)
        {
            if(mp.ContainsKey(arr[i]))
            {
                var val = mp[arr[i]];
                mp.Remove(arr[i]);
                mp.Add(arr[i], val + 1);
            }
            else
            {
                mp.Add(arr[i], 1);
            }
        }
        int count = 0;

        // Count of pairs (arr[i], arr[j])
        // where arr[i] = arr[j]
        foreach(KeyValuePair<int, int> x in mp)
        {
            int f = x.Value;
            count += f * (f - 1) / 2;
        }

        // Count of pairs (arr[i], arr[j]) where
        // arr[i] != arr[j], i.e. Total pairs - pairs
        // where arr[i] = arr[j]
        return ((n * (n - 1)) / 2) - count;
    }

    // Driver code
    public static void Main(String []args)
    {

        int []arr = { 2, 4, 5, 2, 5, 7, 2, 8 };
        int n = arr.Length;
        Console.WriteLine(count_pairs(n, arr));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of valid pairs
function count_pairs(n, a)
{
    // Store frequencies of array elements
    var frequency = new Map();
    for (var i = 0; i < n; i++) {
        if(frequency.has(a[i]))
            frequency.set(a[i], frequency.get(a[i])+1)
        else
            frequency.set(a[i], 1)
    }

    var count = 0;

    // Count of pairs (arr[i], arr[j])
    // where arr[i] = arr[j]
    frequency.forEach((value, key) => {

        var f = value;
        count += f * (f - 1) / 2;
    });

    // Count of pairs (arr[i], arr[j]) where
    // arr[i] != arr[j], i.e. Total pairs - pairs
    // where arr[i] = arr[j]
    return ((n * (n - 1)) / 2) - count;
}

// Driver Code
var arr = [2, 4, 5, 2, 5, 7, 2, 8];
var n = arr.length;
document.write( count_pairs(n, arr));

</script>
```

**Output:** 

```
24
```
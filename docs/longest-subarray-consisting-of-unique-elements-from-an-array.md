# 由阵列中的唯一元素组成的最长子阵列

> 原文:[https://www . geesforgeks . org/最长子数组-由数组中的唯一元素组成/](https://www.geeksforgeeks.org/longest-subarray-consisting-of-unique-elements-from-an-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到仅由唯一元素组成的最大子数组。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，1，2，3}
> **输出:** 5
> **解释:**一个可能的子阵列是{1，2，3，4，5}。
> 
> **输入:** arr[]={1，2，4，4，5，6，7，8，3，4，5，5，3，4，5，6，7，8，1，2，3，4}
> **输出:** 8
> **解释:**唯一可能的子阵是{3，4，5，6，7，8，1，2}。

**天真的方法:**解决问题最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中生成所有的子阵，并检查它是否包含任何副本或者不使用 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 。找到满足条件的最长子阵。
***时间复杂度:**O(N)<sup>3</sup>logN)*
***辅助空间:** O(N)*

**高效途径:**以上途径可以通过 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 进行优化。按照以下步骤解决问题:

1.  初始化一个变量 **j** ，以存储索引的最大值，使得索引 **i 和 j** 之间没有重复的元素
2.  遍历数组，并根据 HashMap 中存储的[i]的前一次出现继续更新 **j** 。
3.  更新 **j** 后，相应更新 **ans** 以存储所需子阵列的最大长度。
4.  打印 **ans** ，遍历完毕。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find largest
// subarray with no duplicates
int largest_subarray(int a[], int n)
{
    // Stores index of array elements
    unordered_map<int, int> index;
    int ans = 0;
    for (int i = 0, j = 0; i < n; i++) {

        // Update j based on previous
        // occurrence of a[i]
        j = max(index[a[i]], j);

        // Update ans to store maximum
        // length of subarray
        ans = max(ans, i - j + 1);

        // Store the index of current
        // occurrence of a[i]
        index[a[i]] = i + 1;
    }

    // Return final ans
    return ans;
}

// Driver Code
int32_t main()
{
    int arr[] = { 1, 2, 3, 4, 5, 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << largest_subarray(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find largest
// subarray with no duplicates
static int largest_subarray(int a[], int n)
{
    // Stores index of array elements
    HashMap<Integer,
            Integer> index = new HashMap<Integer,
                                         Integer>();
    int ans = 0;
    for(int i = 0, j = 0; i < n; i++)
    {

        // Update j based on previous
        // occurrence of a[i]
        j = Math.max(index.containsKey(a[i]) ? 
                             index.get(a[i]) : 0, j);

        // Update ans to store maximum
        // length of subarray
        ans = Math.max(ans, i - j + 1);

        // Store the index of current
        // occurrence of a[i]
        index.put(a[i], i + 1);
    }

    // Return final ans
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 1, 2, 3 };
    int n = arr.length;
    System.out.print(largest_subarray(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import defaultdict

# Function to find largest
# subarray with no duplicates
def largest_subarray(a, n):

    # Stores index of array elements
    index = defaultdict(lambda : 0)

    ans = 0
    j = 0

    for i in range(n):

        # Update j based on previous
        # occurrence of a[i]
        j = max(index[a[i]], j)

        # Update ans to store maximum
        # length of subarray
        ans = max(ans, i - j + 1)

        # Store the index of current
        # occurrence of a[i]
        index[a[i]] = i + 1

        i += 1

    # Return final ans 
    return ans

# Driver Code
arr = [ 1, 2, 3, 4, 5, 1, 2, 3 ]
n = len(arr)

# Function call
print(largest_subarray(arr, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find largest
// subarray with no duplicates
static int largest_subarray(int []a, int n)
{

    // Stores index of array elements
    Dictionary<int,
               int> index = new Dictionary<int,
                                           int>();
    int ans = 0;
    for(int i = 0, j = 0; i < n; i++)
    {

        // Update j based on previous
        // occurrence of a[i]
        j = Math.Max(index.ContainsKey(a[i]) ? 
                                 index[a[i]] : 0, j);

        // Update ans to store maximum
        // length of subarray
        ans = Math.Max(ans, i - j + 1);

        // Store the index of current
        // occurrence of a[i]
        if(index.ContainsKey(a[i]))
            index[a[i]] = i + 1;
        else
            index.Add(a[i], i + 1);
    }

    // Return readonly ans
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 1, 2, 3 };
    int n = arr.Length;

    Console.Write(largest_subarray(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find largest
// subarray with no duplicates
function largest_subarray(a, n)
{
    // Stores index of array elements
    let index = new Map();
    let ans = 0;
    for(let i = 0, j = 0; i < n; i++)
    {

        // Update j based on previous
        // occurrence of a[i]
        j = Math.max(index.has(a[i]) ?
                             index.get(a[i]) : 0, j);

        // Update ans to store maximum
        // length of subarray
        ans = Math.max(ans, i - j + 1);

        // Store the index of current
        // occurrence of a[i]
        index.set(a[i], i + 1);
    }

    // Return final ans
    return ans;
}

// Driver code

    let arr = [ 1, 2, 3, 4, 5, 1, 2, 3 ];
    let n = arr.length;
    document.write(largest_subarray(arr, n));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*
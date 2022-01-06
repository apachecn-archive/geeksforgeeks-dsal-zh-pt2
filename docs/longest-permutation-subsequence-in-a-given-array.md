# 给定数组中最长的置换子序列

> 原文:[https://www . geesforgeks . org/给定数组中最长排列子序列/](https://www.geeksforgeeks.org/longest-permutation-subsequence-in-a-given-array/)

给定一个包含 **N** 元素的数组 **arr** ，求最长子序列的长度，使其成为特定长度的有效排列。如果不存在这样的排列顺序，则打印 0。
**例:**

> **输入:** arr[] = {3，2，1，6，5}
> **输出:** 3
> **解释:**
> 最长的排列子序列将是[3，2，1]。
> **输入:** arr[]= {2，3，4，5}
> **输出:** 0
> **解释:**
> 元素 1 不存在有效的置换子序列。

**方法:**上述问题是关于置换子序列的，所以数组元素的顺序无关紧要，重要的是每个元素的**频率。如果数组长度为 N，则置换序列的最大可能长度为 *N* ，最小可能长度为 *0* 。如果长度为 L 的子序列是一个有效的排列，那么**从 1 到 L 的所有元素都应该存在**。** 

1.  [计算数组中[1，N]范围内元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
2.  迭代数组中从 1 到 N 的所有元素，计算迭代次数，直到观察到 0 的频率。如果元素的频率为“0”，则返回当前迭代次数作为所需长度。

**以下是上述方法的实施:**

## C++

```
// C++ Program to find length of
// Longest Permutation Subsequence
// in a given array

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// longest permutation subsequence
int longestPermutation(int a[], int n)
{

    // Map data structure to
    // count the frequency of each element
    map<int, int> freq;

    for (int i = 0; i < n; i++) {

        freq[a[i]]++;
    }

    int len = 0;

    for (int i = 1; i <= n; i++) {

        // If frequency of element is 0,
        // then we can not move forward
        // as every element should be present
        if (freq[i] == 0) {
            break;
        }

        // Increasing the length by one
        len++;
    }

    return len;
}

// Driver Code
int main()
{

    int arr[] = { 3, 2, 1, 6, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestPermutation(arr, n)
         << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find length of
// Longest Permutation Subsequence
// in a given array
import java.util.*;

class GFG{

// Function to find the
// longest permutation subsequence
static int longestPermutation(int arr[], int n)
{

    // Map data structure to
    // count the frequency of each element
    HashMap<Integer,Integer> freq = new HashMap<Integer,Integer>();

    for (int i = 0; i < n; i++) {

        if(freq.containsKey(arr[i])){
            freq.put(arr[i], freq.get(arr[i])+1);
        }else{
            freq.put(arr[i], 1);
        }
    }

    int len = 0;

    for (int i = 1; i <= n; i++) {

        // If frequency of element is 0,
        // then we can not move forward
        // as every element should be present
        if (!freq.containsKey(i)) {
            break;
        }

        // Increasing the length by one
        len++;
    }

    return len;
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 3, 2, 1, 6, 5 };
    int n = arr.length;

    System.out.print(longestPermutation(arr, n));

}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# Program to find length of
// longest Permutation Subsequence
// in a given array

using System;
using System.Collections.Generic;

public class GFG{

// Function to find the
// longest permutation subsequence
static int longestPermutation(int []arr, int n)
{

    // Map data structure to
    // count the frequency of each element
    Dictionary<int,int> freq = new Dictionary<int,int>();

    for (int i = 0; i < n; i++) {

        if(freq.ContainsKey(arr[i])){
            freq[arr[i]] = freq[arr[i]] + 1;
        }else{
            freq.Add(arr[i], 1);
        }
    }

    int len = 0;

    for (int i = 1; i <= n; i++) {

        // If frequency of element is 0,
        // then we can not move forward
        // as every element should be present
        if (!freq.ContainsKey(i)) {
            break;
        }

        // Increasing the length by one
        len++;
    }

    return len;
}

// Driver Code
public static void Main(String[] args)
{

    int []arr = { 3, 2, 1, 6, 5 };
    int n = arr.Length;

    Console.Write(longestPermutation(arr, n));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Program to find length of
# Longest Permutation Subsequence
# in a given array
from collections import defaultdict

# Function to find the
# longest permutation subsequence
def longestPermutation(a, n):

    # Map data structure to
    # count the frequency of each element
    freq = defaultdict(int)

    for i in range( n ):

        freq[a[i]] += 1

    length = 0

    for i in range(1 , n + 1):

        # If frequency of element is 0,
        # then we can not move forward
        # as every element should be present
        if (freq[i] == 0):
            break

        # Increasing the length by one
        length += 1

    return length

# Driver Code
if __name__ == "__main__":

    arr = [ 3, 2, 1, 6, 5 ]
    n = len(arr)

    print(longestPermutation(arr, n))

# This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript Program to find length of
// Longest Permutation Subsequence
// in a given array

// Function to find the
// longest permutation subsequence
function longestPermutation(arr, n)
{

    // Map data structure to
    // count the frequency of each element
    let freq = new Map();

    for (let i = 0; i < n; i++) {

        if(freq.has(arr[i])){
            freq.set(arr[i], freq.get(arr[i])+1);
        }else{
            freq.set(arr[i], 1);
        }
    }

    let len = 0;

    for (let i = 1; i <= n; i++) {

        // If frequency of element is 0,
        // then we can not move forward
        // as every element should be present
        if (!freq.has(i)) {
            break;
        }

        // Increasing the length by one
        len++;
    }

    return len;
}

// Driver code

      let arr = [ 3, 2, 1, 6, 5 ];
    let n = arr.length;

    document.write(longestPermutation(arr, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(N)*
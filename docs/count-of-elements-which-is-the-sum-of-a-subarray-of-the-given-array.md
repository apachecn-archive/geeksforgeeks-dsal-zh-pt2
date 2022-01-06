# 给定阵列的子阵列之和的元素计数

> 原文:[https://www . geesforgeks . org/给定数组的子数组的元素计数/](https://www.geeksforgeeks.org/count-of-elements-which-is-the-sum-of-a-subarray-of-the-given-array/)

给定一个数组 **arr[]** ，任务是对数组中的元素进行计数，使得存在一个和这个元素相等的子数组。
**注意:**子阵长度必须大于 1。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6， 7}
> **输出:** 4
> **说明:**
> 数组中有 4 个这样的元素–
> arr[2]= 3 =>arr[0-1]=>1+2 = 3
> arr[4]= 5 =>arr[1-2]=>2+3 = 5
> arr[5]= 6 =>arr[0-2]=>1+2+2 = > 3 + 4 = 7
> **输入:** arr[] = {1，2，3，3}
> **输出:** 2
> 数组中有 2 个这样的元素–
> arr[2]= 3 =>arr[0-1]=>1+2 = 3
> arr[3]= 3 =>arr[0-1]=>1+2 = 3

**方法:**想法是将数组元素的[频率存储在](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)中。然后，迭代[每个可能的子数组](https://www.geeksforgeeks.org/sum-of-all-subarrays/)，并检查其和是否出现在散列图中。如果是，那么将这些元素的计数增加它们的频率。

下面是上述方法的实现:

## C++

```
// C++ implementation to count the
// elements such that their exist
// a subarray whose sum is equal to
// this element

#include <bits/stdc++.h>

using namespace std;

// Function to count the elements
// such that their exist a subarray
// whose sum is equal to this element
int countElement(int arr[], int n)
{
    map<int, int> freq;
    int ans = 0;

    // Loop to count the frequency
    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // Loop to iterate over every possible
    // subarray of the array
    for (int i = 0; i < n - 1; i++) {
        int tmpsum = arr[i];
        for (int j = i + 1; j < n; j++) {
            tmpsum += arr[j];
            if (freq.find(tmpsum) != freq.end()) {
                ans += freq[tmpsum];
            }
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countElement(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// elements such that their exist
// a subarray whose sum is equal to
// this element
import java.util.*;

class GFG {

// Function to count the elements
// such that their exist a subarray
// whose sum is equal to this element
static int countElement(int arr[], int n)
{
    int freq[] = new int[n + 1];
    int ans = 0;

    // Loop to count the frequency
    for(int i = 0; i < n; i++)
    {
       freq[arr[i]]++;
    }

    // Loop to iterate over every possible
    // subarray of the array
    for(int i = 0; i < n - 1; i++)
    {
       int tmpsum = arr[i];

       for(int j = i + 1; j < n; j++)
       {
          tmpsum += arr[j];

          if (tmpsum <= n)
          {
              ans += freq[tmpsum];
              freq[tmpsum] = 0;
          }
       }
    }

    return ans;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.length;
    System.out.println(countElement(arr, n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation to count the
# elements such that their exist
# a subarray whose sum is equal to
# this element

# Function to count element such
# that their exist a subarray whose
# sum is equal to this element
def countElement(arr, n):
    freq = {}
    ans = 0

    # Loop to compute frequency
    # of the given elements
    for i in range(n):
        freq[arr[i]] = \
            freq.get(arr[i], 0) + 1

    # Loop to iterate over every
    # possible subarray of array
    for i in range(n-1):
        tmpsum = arr[i]
        for j in range(i + 1, n):
            tmpsum += arr[j]
            if tmpsum in freq:
                ans += freq[tmpsum]
    return ans

# Driver Code
if __name__ == "__main__":
    arr =[1, 2, 3, 4, 5, 6, 7]
    n = len(arr)
    print(countElement(arr, n))
```

## C#

```
// C# implementation to count the
// elements such that their exist
// a subarray whose sum is equal to
// this element
using System;

class GFG {

// Function to count the elements
// such that their exist a subarray
// whose sum is equal to this element
static int countElement(int[] arr, int n)
{
    int[] freq = new int[n + 1];
    int ans = 0;

    // Loop to count the frequency
    for(int i = 0; i < n; i++)
    {
       freq[arr[i]]++;
    }

    // Loop to iterate over every possible
    // subarray of the array
    for(int i = 0; i < n - 1; i++)
    {
       int tmpsum = arr[i];

       for(int j = i + 1; j < n; j++)
       {
          tmpsum += arr[j];

          if (tmpsum <= n)
          {
              ans += freq[tmpsum];
              freq[tmpsum] = 0;
          }   
       }
    }
    return ans;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.Length;

    Console.WriteLine(countElement(arr, n));
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// Javascript implementation to count the
// elements such that their exist
// a subarray whose sum is equal to
// this element

// Function to count the elements
// such that their exist a subarray
// whose sum is equal to this element
function countElement(arr, n)
{
    let freq = Array.from({length: n+1}, (_, i) => 0);
    let ans = 0;

    // Loop to count the frequency
    for(let i = 0; i < n; i++)
    {
       freq[arr[i]]++;
    }

    // Loop to iterate over every possible
    // subarray of the array
    for(let i = 0; i < n - 1; i++)
    {
       let tmpsum = arr[i];

       for(let j = i + 1; j < n; j++)
       {
          tmpsum += arr[j];

          if (tmpsum <= n)
          {
              ans += freq[tmpsum];
              freq[tmpsum] = 0;
          }
       }
    }

    return ans;
}

// Driver Code

    let arr = [ 1, 2, 3, 4, 5, 6, 7 ];
    let n = arr.length;
    document.write(countElement(arr, n));

</script>
```

**Output:** 

```
4
```

**时间复杂度:***O(N<sup>2</sup>)*
**空间复杂度:** *O(N)*
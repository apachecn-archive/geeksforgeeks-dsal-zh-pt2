# 数组中奇偶频繁元素之和的差

> 原文:[https://www . geesforgeks . org/数组中奇数和偶数频繁元素之和之差/](https://www.geeksforgeeks.org/difference-between-sum-of-odd-and-even-frequent-elements-in-an-array/)

给定一个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出所有奇数频繁数组元素的[和所有偶数频繁数组元素](https://www.geeksforgeeks.org/sum-of-all-odd-frequency-elements-in-an-array/)的[和之间的绝对差。](https://www.geeksforgeeks.org/sum-of-all-even-occurring-element-in-an-array/)

**示例:**

> **输入:** arr[] = {1，5，5，2，4，3，3}
> **输出:** 9
> **解释:**
> 偶频数元素为 5 和 3(均出现两次)。
> 因此，所有偶频数元素之和= 5 + 5 + 3 + 3 = 16。
> 奇数频繁元素为 1、2、4(各出现一次)。
> 因此，所有奇数频繁元素之和= 1 + 2 + 4 = 7。
> 它们之和的差= 16–7 = 9。
> 
> **输入:** arr[] = {1，1，2，2，3，3}
> **输出:** 12
> **解释:**
> 偶频数数组元素为 1，2，3(出现两次)。
> 因此，所有偶频数元素之和= 12。
> 由于数组中不存在奇数频繁元素，因此差值= 12–0 = 12

**方法:**按照以下步骤解决问题:

*   初始化一个[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)来存储数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，更新[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中数组元素的频率。
*   然后，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)将偶数频率的元素加到一个变量上，比如说**sum _ 偶数**，将奇数频率的元素加到另一个变量上，比如说**sum _ 奇数**。
*   最后，打印**sum _ 奇数**和**sum _ 偶数**的差值。

下面是上述方法的实现:

## C++

```
// C++ program to find absolute difference
// between the sum of all odd frequent and
// even frequent elements in an array

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of all even
// and odd frequent elements in an array
int findSum(int arr[], int N)
{
    // Stores the frequency of array elements
    unordered_map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency of
        // current element
        mp[arr[i]]++;
    }

    // Stores sum of odd and even
    // frequent elements
    int sum_odd = 0, sum_even = 0;

    // Traverse the map
    for (auto itr = mp.begin();
        itr != mp.end(); itr++) {

        // If frequency is odd
        if (itr->second % 2 != 0)

            // Add sum of all occurrences of
            // current element to sum_odd
            sum_odd += (itr->first)
                    * (itr->second);

        // If frequency is even
        if (itr->second % 2 == 0)

            // Add sum of all occurrences of
            // current element to sum_even
            sum_even += (itr->first)
                        * (itr->second);
    }

    // Calculate difference
    // between their sum
    int diff = sum_even - sum_odd;

    // Return diff
    return diff;
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 5, 2, 4, 3, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find absolute difference
// between the sum of all odd frequenct and
// even frequent elements in an array
import java.util.*;
import java.io.*;
import java.math.*;

class GFG{

// Function to find the sum of all even
// and odd frequent elements in an array
static int findSum(int arr[], int N)
{

    // Stores the frequency of array elements
    Map<Integer,
        Integer> map = new HashMap<Integer,
                                   Integer>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency of
        // current element
        if (!map.containsKey(arr[i]))
            map.put(arr[i], 1);
        else
            map.replace(arr[i], map.get(arr[i]) + 1);
    }

    // Stores sum of odd and even
    // frequent elements
    int sum_odd = 0, sum_even = 0;

    // Traverse the map
    Set<Map.Entry<Integer, Integer>> hmap = map.entrySet();
    for(Map.Entry<Integer, Integer> data:hmap)
    {
        int key = data.getKey();
        int val = data.getValue();

        // If frequency is odd
        if (val % 2 != 0)

            // Add sum of all occurrences of
            // current element to sum_odd
            sum_odd += (key) * (val);

        // If frequency is even
        if (val % 2 == 0)

            // Add sum of all occurrences of
            // current element to sum_even
            sum_even += (key) * (val);
    }

    // Calculate difference
    // between their sum
    int diff = sum_even - sum_odd;

    // Return diff
    return diff;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 5, 5, 2, 4, 3, 3 };
    int N = arr.length;

    System.out.println(findSum(arr, N));
}
}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Python3 program to find absolute difference
# between the sum of all odd frequenct and
# even frequent elements in an array

# Function to find the sum of all even
# and odd frequent elements in an array
def findSum(arr, N):

    # Stores the frequency of array elements
    mp = {}

    # Traverse the array
    for i in range(0, N):

        # Update frequency of
        # current element
        if arr[i] in mp:
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    # Stores sum of odd and even
    # frequent elements
    sum_odd, sum_even = 0, 0

    # Traverse the map
    for itr in mp:

        # If frequency is odd
        if (mp[itr] % 2 != 0):

            # Add sum of all occurrences of
            # current element to sum_odd
            sum_odd += (itr) * (mp[itr])

        # If frequency is even
        if (mp[itr] % 2 == 0):

            # Add sum of all occurrences of
            # current element to sum_even
            sum_even += (itr) * (mp[itr])

    # Calculate difference
    # between their sum
    diff = sum_even - sum_odd

    # Return diff
    return diff

# Driver code
arr = [ 1, 5, 5, 2, 4, 3, 3 ]
N = len(arr)

print(findSum(arr, N))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find absolute difference
// between the sum of all odd frequenct and
// even frequent elements in an array
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the sum of all even
    // and odd frequent elements in an array
    static int findSum(int[] arr, int N)
    {
        // Stores the frequency of array elements
        Dictionary<int, int> mp = new Dictionary<int, int>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update frequency of
            // current element
            if(mp.ContainsKey(arr[i]))
            {
                mp[arr[i]]++;
            }
            else{
                mp[arr[i]] = 1;
            }
        }

        // Stores sum of odd and even
        // frequent elements
        int sum_odd = 0, sum_even = 0;

        // Traverse the map
        foreach(KeyValuePair<int, int> itr in mp) {

            // If frequency is odd
            if (itr.Value % 2 != 0)

                // Add sum of all occurrences of
                // current element to sum_odd
                sum_odd += (itr.Key)
                        * (itr.Value);

            // If frequency is even
            if (itr.Value % 2 == 0)

                // Add sum of all occurrences of
                // current element to sum_even
                sum_even += (itr.Key)
                            * (itr.Value);
        }

        // Calculate difference
        // between their sum
        int diff = sum_even - sum_odd;

        // Return diff
        return diff;
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 5, 5, 2, 4, 3, 3 };
    int N = arr.Length;
    Console.Write(findSum(arr, N));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// JavaScript program to find absolute difference
// between the sum of all odd frequenct and
// even frequent elements in an array

// Function to find the sum of all even
// and odd frequent elements in an array
function findSum(arr, N)
{
    // Stores the frequency of array elements
    var mp = {};
    for(let i =0; i<N;i++)
      mp[arr[i]] = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // Update frequency of
        // current element
        mp[arr[i]]++;
    }

    // Stores sum of odd and even
    // frequent elements
    var sum_odd = 0, sum_even = 0;

    // Traverse the map
    for (let itr in mp) {

        // If frequency is odd
        if (mp[itr] % 2 != 0) {

            // Add sum of all occurrences of
            // current element to sum_odd
            sum_odd += (itr)
                    * (mp[itr]);

        }

        // If frequency is even
        if (mp[itr] % 2 == 0) {

            // Add sum of all occurrences of
            // current element to sum_even
            sum_even += (itr)
                        * (mp[itr]);

        }

    }

    // Calculate difference
    // between their sum
    var diff = sum_even - sum_odd;

    // Return diff
    return diff;
}

// Driver Code

var arr = new Array( 1, 5, 5, 2, 4, 3, 3 );
var N = arr.length;
console.log( findSum(arr, N) );

// This code is contributed by ukasp. 

</script>
```

**输出:**

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
# 计数 1 和 0 数量相等的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-equal-number-1s-0s/](https://www.geeksforgeeks.org/count-subarrays-equal-number-1s-0s/)

给定一个大小为 **n** 的数组 **arr[]** ，其中只包含 0 和 1。问题是要计算 0 和 1 数量相等的子阵列。

**示例:**

```
Input : arr[] = {1, 0, 0, 1, 0, 1, 1}
Output : 8
The index range for the 8 sub-arrays are:
(0, 1), (2, 3), (0, 3), (3, 4), (4, 5)
(2, 5), (0, 5), (1, 6)
```

问题与 0 和 1 相等的[最大子阵列密切相关。](https://www.geeksforgeeks.org/largest-subarray-with-equal-number-of-0s-and-1s/)
**方法:**步骤如下:

1.  将 arr[]中的所有 0 视为-1。
2.  创建一个哈希表，保存每个 **sum[i]** 值的计数，其中 sum[i] = sum(arr[0]+..+arr[i])，因为 i = 0 到 n-1。
3.  现在开始计算累积总和，然后我们得到该总和的增量计数 1，在哈希表中表示为索引。累积和中具有相同值的每对位置的数组构成一个 1 和 0 相等的连续范围。
4.  现在遍历散列表，得到散列表中每个元素的出现频率。让频率表示为 **freq** 。对于每个 **freq** > 1，我们可以通过**(freq *(freq–1))/2**的方式选择子阵列的任意两对索引。对所有的 **freq** 做同样的操作，结果将是所有可能的子阵列的数量，包含相同数量的 1 和 0。
5.  另外，将 0 之和的 **freq** 添加到哈希表中以获得最终结果。

**解释:**
把所有 0 都看成-1，如果和[i] ==和[j]，其中和[i] =和(arr[0]+..+arr[i])和 sum[j] = sum(arr[0]+..+arr[j])，“I”小于“j”，则求和(arr[i+1]+..+arr[j])必须为 0。如果 arr(i+1，..j)包含相等数量的 1 和 0。

## C++

```
// C++ implementation to count subarrays with
// equal number of 1's and 0's
#include <bits/stdc++.h>

using namespace std;

// function to count subarrays with
// equal number of 1's and 0's
int countSubarrWithEqualZeroAndOne(int arr[], int n)
{
    // 'um' implemented as hash table to store
    // frequency of values obtained through
    // cumulative sum
    unordered_map<int, int> um;
    int curr_sum = 0;

    // Traverse original array and compute cumulative
    // sum and increase count by 1 for this sum
    // in 'um'. Adds '-1' when arr[i] == 0
    for (int i = 0; i < n; i++) {
        curr_sum += (arr[i] == 0) ? -1 : arr[i];
        um[curr_sum]++;
    }

    int count = 0;
    // traverse the hash table 'um'
    for (auto itr = um.begin(); itr != um.end(); itr++) {

        // If there are more than one prefix subarrays
        // with a particular sum
        if (itr->second > 1)
            count += ((itr->second * (itr->second - 1)) / 2);
    }

    // add the subarrays starting from 1st element and
    // have equal number of 1's and 0's
    if (um.find(0) != um.end())
        count += um[0];

    // required count of subarrays
    return count;
}

// Driver program to test above
int main()
{
    int arr[] = { 1, 0, 0, 1, 0, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Count = "
         << countSubarrWithEqualZeroAndOne(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count subarrays with
// equal number of 1's and 0's
import java.util.*;

class GFG
{

// function to count subarrays with
// equal number of 1's and 0's
static int countSubarrWithEqualZeroAndOne(int arr[], int n)
{
    // 'um' implemented as hash table to store
    // frequency of values obtained through
    // cumulative sum
    Map<Integer,Integer> um = new HashMap<>();
    int curr_sum = 0;

    // Traverse original array and compute cumulative
    // sum and increase count by 1 for this sum
    // in 'um'. Adds '-1' when arr[i] == 0
    for (int i = 0; i < n; i++) {
        curr_sum += (arr[i] == 0) ? -1 : arr[i];
        um.put(curr_sum, um.get(curr_sum)==null?1:um.get(curr_sum)+1);
    }

    int count = 0;

    // traverse the hash table 'um'
    for (Map.Entry<Integer,Integer> itr : um.entrySet())
    {

        // If there are more than one prefix subarrays
        // with a particular sum
        if (itr.getValue() > 1)
            count += ((itr.getValue()* (itr.getValue()- 1)) / 2);
    }

    // add the subarrays starting from 1st element and
    // have equal number of 1's and 0's
    if (um.containsKey(0))
        count += um.get(0);

    // required count of subarrays
    return count;
}

// Driver program to test above
public static void main(String[] args)
{
    int arr[] = { 1, 0, 0, 1, 0, 1, 1 };
    int n = arr.length;
    System.out.println("Count = "
        + countSubarrWithEqualZeroAndOne(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to count
# subarrays with equal number
# of 1's and 0's

# function to count subarrays with
# equal number of 1's and 0's
def countSubarrWithEqualZeroAndOne (arr, n):

    # 'um' implemented as hash table
    # to store frequency of values
    # obtained through cumulative sum
    um = dict()
    curr_sum = 0

    # Traverse original array and compute
    # cumulative sum and increase count
    # by 1 for this sum in 'um'.
    # Adds '-1' when arr[i] == 0
    for i in range(n):
        curr_sum += (-1 if (arr[i] == 0) else arr[i])
        if um.get(curr_sum):
            um[curr_sum]+=1
        else:
            um[curr_sum]=1

    count = 0

    # traverse the hash table 'um'
    for itr in um:

        # If there are more than one
        # prefix subarrays with a
        # particular sum
        if um[itr] > 1:
            count += ((um[itr] * int(um[itr] - 1)) / 2)

    # add the subarrays starting from
    # 1st element and have equal
    # number of 1's and 0's
    if um.get(0):
        count += um[0]

    # required count of subarrays
    return int(count)

# Driver code to test above
arr = [ 1, 0, 0, 1, 0, 1, 1 ]
n = len(arr)
print("Count =",
    countSubarrWithEqualZeroAndOne(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# implementation to count subarrays
// with equal number of 1's and 0's
using System;
using System.Collections.Generic;

class GFG
{

// function to count subarrays with
// equal number of 1's and 0's
static int countSubarrWithEqualZeroAndOne(int []arr,
                                          int n)
{
    // 'um' implemented as hash table to store
    // frequency of values obtained through
    // cumulative sum
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    int curr_sum = 0;

    // Traverse original array and compute cumulative
    // sum and increase count by 1 for this sum
    // in 'um'. Adds '-1' when arr[i] == 0
    for (int i = 0; i < n; i++)
    {
        curr_sum += (arr[i] == 0) ? -1 : arr[i];
        if(mp.ContainsKey(curr_sum))
        {
            var v = mp[curr_sum];
            mp.Remove(curr_sum);
            mp.Add(curr_sum, ++v);
        }
        else
            mp.Add(curr_sum, 1);
    }

    int count = 0;

    // traverse the hash table 'um'
    foreach(KeyValuePair<int, int> itr in mp)
    {

        // If there are more than one prefix subarrays
        // with a particular sum
        if (itr.Value > 1)
            count += ((itr.Value* (itr.Value - 1)) / 2);
    }

    // add the subarrays starting from 1st element
    // and have equal number of 1's and 0's
    if (mp.ContainsKey(0))
        count += mp[0];

    // required count of subarrays
    return count;
}

// Driver program to test above
public static void Main(String[] args)
{
    int []arr = { 1, 0, 0, 1, 0, 1, 1 };
    int n = arr.Length;
    Console.WriteLine("Count = " +
            countSubarrWithEqualZeroAndOne(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation to count subarrays with
// equal number of 1's and 0's

// function to count subarrays with
// equal number of 1's and 0's
function countSubarrWithEqualZeroAndOne(arr, n)
{
    // 'um' implemented as hash table to store
    // frequency of values obtained through
    // cumulative sum
    var um = new Map();
    var curr_sum = 0;

    // Traverse original array and compute cumulative
    // sum and increase count by 1 for this sum
    // in 'um'. Adds '-1' when arr[i] == 0
    for (var i = 0; i < n; i++) {
        curr_sum += (arr[i] == 0) ? -1 : arr[i];
        if(um.has(curr_sum))
            um.set(curr_sum, um.get(curr_sum)+1);
        else
            um.set(curr_sum, 1)
    }

    var count = 0;
    // traverse the hash table 'um'
    um.forEach((value, key) => {

        // If there are more than one prefix subarrays
        // with a particular sum
        if (value > 1)
            count += ((value * (value - 1)) / 2);
    });

    // add the subarrays starting from 1st element and
    // have equal number of 1's and 0's
    if (um.has(0))
        count += um.get(0);

    // required count of subarrays
    return count;
}

// Driver program to test above
var arr = [1, 0, 0, 1, 0, 1, 1];
var n = arr.length;
document.write( "Count = "
      + countSubarrWithEqualZeroAndOne(arr, n));

// This code is contributed by noob2000.
</script>
```

**输出:**

```
Count = 8
```

**时间复杂度:** O(n)。
**辅助空间:** O(n)。

**另一种方法:**

## C++

```
#include <bits/stdc++.h>

using namespace std;

int countSubarrWithEqualZeroAndOne(int arr[], int n)
{
    map<int, int> mp;
    int sum = 0;
    int count = 0;
    for (int i = 0; i < n; i++) {
        // Replacing 0's in array with -1
        if (arr[i] == 0)
            arr[i] = -1;

        sum += arr[i];

        // If sum = 0, it implies number of 0's and 1's are
        // equal from arr[0]..arr[i]
        if (sum == 0)
            count++;

          //if mp[sum] exists then add "frequency-1" to count
        if (mp[sum])
            count += mp[sum];

          //if frequency of "sum" is zero then we initialize that frequency to 1
          //if its not 0, we increment it
        if (mp[sum] == 0)
            mp[sum] = 1;
        else
            mp[sum]++;
    }
    return count;
}

int main()
{
    int arr[] = { 1, 0, 0, 1, 0, 1, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "count="
         << countSubarrWithEqualZeroAndOne(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;
import java.util.Map;

// Java implementation to count subarrays with
// equal number of 1's and 0's
public class Main {

    // Function that returns count of sub arrays
    // with equal numbers of 1's and 0's
    static int countSubarrWithEqualZeroAndOne(int[] arr,
                                              int n)
    {
        Map<Integer, Integer> myMap = new HashMap<>();
        int sum = 0;
        int count = 0;
        for (int i = 0; i < n; i++) {
            // Replacing 0's in array with -1
            if (arr[i] == 0)
                arr[i] = -1;

            sum += arr[i];

            // If sum = 0, it implies number of 0's and 1's
            // are equal from arr[0]..arr[i]
            if (sum == 0)
                count++;

            if (myMap.containsKey(sum))
                count += myMap.get(sum);

            if (!myMap.containsKey(sum))
                myMap.put(sum, 1);
            else
                myMap.put(sum, myMap.get(sum) + 1);
        }
        return count;
    }

    // main function
    public static void main(String[] args)
    {
        int arr[] = { 1, 0, 0, 1, 0, 1, 1 };
        int n = arr.length;
        System.out.println(
            "Count = "
            + countSubarrWithEqualZeroAndOne(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to count subarrays
# with equal number of 1's and 0's

def countSubarrWithEqualZeroAndOne(arr, n):
    mp = dict()
    Sum = 0
    count = 0

    for i in range(n):

        # Replacing 0's in array with -1
        if (arr[i] == 0):
            arr[i] = -1

        Sum += arr[i]

        # If Sum = 0, it implies number of
        # 0's and 1's are equal from arr[0]..arr[i]
        if (Sum == 0):
            count += 1

        if (Sum in mp.keys()):
            count += mp[Sum]

        mp[Sum] = mp.get(Sum, 0) + 1

    return count

# Driver Code
arr = [1, 0, 0, 1, 0, 1, 1]

n = len(arr)

print("count =",
      countSubarrWithEqualZeroAndOne(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation to count subarrays with
// equal number of 1's and 0's
using System;
using System.Collections.Generic;

class GFG {

    // Function that returns count of sub arrays
    // with equal numbers of 1's and 0's
    static int countSubarrWithEqualZeroAndOne(int[] arr,
                                              int n)
    {
        Dictionary<int, int> myMap
            = new Dictionary<int, int>();
        int sum = 0;
        int count = 0;
        for (int i = 0; i < n; i++) {
            // Replacing 0's in array with -1
            if (arr[i] == 0)
                arr[i] = -1;

            sum += arr[i];

            // If sum = 0, it implies number of 0's and 1's
            // are equal from arr[0]..arr[i]
            if (sum == 0)
                count++;

            if (myMap.ContainsKey(sum))
                count += myMap[sum];

            if (!myMap.ContainsKey(sum))
                myMap.Add(sum, 1);
            else {
                var v = myMap[sum] + 1;
                myMap.Remove(sum);
                myMap.Add(sum, v);
            }
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 0, 0, 1, 0, 1, 1 };
        int n = arr.Length;
        Console.WriteLine(
            "Count = "
            + countSubarrWithEqualZeroAndOne(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to count subarrays with
// equal number of 1's and 0's

function countSubarrWithEqualZeroAndOne(arr, n)
{
    var mp = new Map();
    var sum = 0;
    let count = 0;

    for (var i = 0; i < n; i++) {
        //Replacing 0's in array with -1
        if (arr[i] == 0)
            arr[i] = -1;

        sum += arr[i];

        //If sum = 0, it implies number of 0's and 1's are
        //equal from arr[0]..arr[i]
        if (sum == 0)
            count += 1;

        if (mp.has(sum) == true)
            count += mp.get(sum);

        if(mp.has(sum) == false)
            mp.set(sum, 1);
        else
            mp.set(sum, mp.get(sum)+1);
    }
      return count;
}

// Driver program to test above
var arr = [1, 0, 0, 1, 0, 1, 1];
var n = arr.length;
document.write( "Count = "
      + countSubarrWithEqualZeroAndOne(arr, n));

// This code is contributed by noob2000.
</script>
```

**输出:**

```
Count = 8
```
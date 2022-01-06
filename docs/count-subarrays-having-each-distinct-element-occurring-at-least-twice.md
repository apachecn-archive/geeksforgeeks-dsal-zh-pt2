# 计数每个不同元素至少出现两次的子阵列

> 原文:[https://www . geeksforgeeks . org/count-subarrays-每个不同元素至少出现两次/](https://www.geeksforgeeks.org/count-subarrays-having-each-distinct-element-occurring-at-least-twice/)

给定大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算给定阵列中[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，使得这些子阵列中的每个不同元素至少出现两次。

**示例:**

> **输入:** arr[] = {1，1，2，2，2}
> **输出:** 6
> **解释:**每个元素至少出现两次的子阵是:{{1，1}、{1，1，2，2，2}、{1，1，2，2，2}、{2，2}、{2，2，2}、{2，2}}。
> 因此，所需输出为 6。
> 
> **输入:** arr[] = {1，2，1，2，3}
> **输出:** 1

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组的所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子数组，检查子数组中的所有元素是否至少出现两次。如果发现为真，则增加计数。最后，打印得到的**计数**。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**高效方法**:优化上述方法的思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntSub** 来存储子阵列的计数，这样子阵列中的每个元素至少出现两次。
*   创建一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **cntFreq** ，来存储每个子阵列元素的频率。
*   初始化一个变量，比如 **cntUnique** ，将元素的计数存储在一个频率为 **1** 的子阵列中。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。对于每个可能的子阵列，存储阵列中每个元素的频率，并检查 **cntUnique** 的值是否为 **0** 。如果发现为真，则增加 **cntSub** 的值。
*   最后，打印 **cntSub** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the count
// of subarrays having each
// element occurring at least twice
int cntSubarrays(int arr[], int N)
{
    // Stores count of subarrays
    // having each distinct element
    // occurring at least twice
    int cntSub = 0;

    // Stores count of unique
    // elements in a subarray
    int cntUnique = 0;

    // Store frequency of
    // each element of a subarray
    unordered_map<int, int> cntFreq;

    // Traverse the given
    // array
    for (int i = 0; i < N;
         i++) {

        // Count frequency and
        // check conditions for
        // each subarray
        for (int j = i; j < N;
             j++) {

            // Update frequency
            cntFreq[arr[j]]++;

            // Check if frequency of
            // arr[j] equal to 1
            if (cntFreq[arr[j]]
                == 1) {

                // Update Count of
                // unique elements
                cntUnique++;
            }
            else if (cntFreq[arr[j]]
                     == 2) {

                // Update count of
                // unique elements
                cntUnique--;
            }

            // If each element of subarray
            // occurs at least twice
            if (cntUnique == 0) {

                // Update cntSub
                cntSub++;
            }
        }

        // Remove all elements
        // from the subarray
        cntFreq.clear();

        // Update cntUnique
        cntUnique = 0;
    }
    return cntSub;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 2, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << cntSubarrays(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to get the count
// of subarrays having each
// element occurring at least twice
static int cntSubarrays(int arr[], int N)
{

    // Stores count of subarrays
    // having each distinct element
    // occurring at least twice
    int cntSub = 0;

    // Stores count of unique
    // elements in a subarray
    int cntUnique = 0;

    // Store frequency of
    // each element of a subarray
     Map<Integer,
         Integer> cntFreq = new HashMap<Integer,
                                        Integer>();

    // Traverse the given
    // array
    for(int i = 0; i < N; i++) 
    {

        // Count frequency and
        // check conditions for
        // each subarray
        for(int j = i; j < N; j++)
        {

            // Update frequency
            cntFreq.put(arr[j], 
                        cntFreq.getOrDefault(
                        arr[j], 0) + 1); 

            // Check if frequency of
            // arr[j] equal to 1
            if (cntFreq.get(arr[j]) == 1)
            {

                // Update Count of
                // unique elements
                cntUnique++;
            }
            else if (cntFreq.get(arr[j]) == 2) 
            {

                // Update count of
                // unique elements
                cntUnique--;
            }

            // If each element of subarray
            // occurs at least twice
            if (cntUnique == 0)
            {

                // Update cntSub
                cntSub++;
            }
        }

        // Remove all elements
        // from the subarray
        cntFreq.clear();

        // Update cntUnique
        cntUnique = 0;
    }
    return cntSub;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 1, 2, 2, 2 };
    int N = arr.length;

    System.out.println(cntSubarrays(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import defaultdict

# Function to get the count
# of subarrays having each
# element occurring at least twice 
def cntSubarrays(arr, N):

    # Stores count of subarrays
    # having each distinct element
    # occurring at least twice
    cntSub = 0

    # Stores count of unique
    # elements in a subarray
    cntUnique = 0

    # Store frequency of
    # each element of a subarray
    cntFreq = defaultdict(lambda : 0)

    # Traverse the given
    # array
    for i in range(N):

        # Count frequency and
        # check conditions for
        # each subarray
        for j in range(i, N):

            # Update frequency
            cntFreq[arr[j]] += 1

            # Check if frequency of
            # arr[j] equal to 1
            if (cntFreq[arr[j]] == 1):

                # Update Count of
                # unique elements
                cntUnique += 1

            elif (cntFreq[arr[j]] == 2):

                # Update count of
                # unique elements
                cntUnique -= 1

            # If each element of subarray
            # occurs at least twice
            if (cntUnique == 0):

                # Update cntSub
                cntSub += 1

        # Remove all elements
        # from the subarray
        cntFreq.clear()

        # Update cntUnique
        cntUnique = 0

    return cntSub

# Driver code
if __name__ == '__main__':

    arr = [ 1, 1, 2, 2, 2 ]
    N = len(arr)

    print(cntSubarrays(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to get the count
// of subarrays having each
// element occurring at least twice
static int cntSubarrays(int[] arr, int N)
{

    // Stores count of subarrays
    // having each distinct element
    // occurring at least twice
    int cntSub = 0;

    // Stores count of unique
    // elements in a subarray
    int cntUnique = 0;

    // Store frequency of
    // each element of a subarray
    Dictionary<int,
               int> cntFreq = new Dictionary<int,
                                             int>();

    // Traverse the given
    // array
    for(int i = 0; i < N; i++) 
    {

        // Count frequency and
        // check conditions for
        // each subarray
        for(int j = i; j < N; j++) 
        {

            // Update frequency
            if (cntFreq.ContainsKey(arr[j]))
            {
                var val = cntFreq[arr[j]];
                cntFreq.Remove(arr[j]);
                cntFreq.Add(arr[j], val + 1);
            }
            else 
            {
                cntFreq.Add(arr[j], 1);
            }

            // Check if frequency of
            // arr[j] equal to 1
            if (cntFreq[arr[j]] == 1) 
            {

                // Update Count of
                // unique elements
                cntUnique++;
            }
            else if (cntFreq[arr[j]] == 2) 
            {

                // Update count of
                // unique elements
                cntUnique--;
            }

            // If each element of subarray
            // occurs at least twice
            if (cntUnique == 0)
            {

                // Update cntSub
                cntSub++;
            }
        }

        // Remove all elements
        // from the subarray
        cntFreq.Clear();

        // Update cntUnique
        cntUnique = 0;
    }
    return cntSub;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 1, 2, 2, 2 };
    int N = arr.Length;

    Console.Write(cntSubarrays(arr, N));
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to get the count
// of subarrays having each
// element occurring at least twice
function cntSubarrays(arr, N)
{
    // Stores count of subarrays
    // having each distinct element
    // occurring at least twice
    var cntSub = 0;

    // Stores count of unique
    // elements in a subarray
    var cntUnique = 0;

    // Store frequency of
    // each element of a subarray
    var cntFreq = new Map();

    // Traverse the given
    // array
    for (var i = 0; i < N;
         i++) {

        // Count frequency and
        // check conditions for
        // each subarray
        for (var j = i; j < N;
             j++) {

            // Update frequency
            if(cntFreq.has(arr[j]))
                cntFreq.set(arr[j], cntFreq.get(arr[j])+1)
            else
                cntFreq.set(arr[j], 1);

            // Check if frequency of
            // arr[j] equal to 1
            if (cntFreq.get(arr[j])
                == 1) {

                // Update Count of
                // unique elements
                cntUnique++;
            }
            else if (cntFreq.get(arr[j])
                     == 2) {

                // Update count of
                // unique elements
                cntUnique--;
            }

            // If each element of subarray
            // occurs at least twice
            if (cntUnique == 0) {

                // Update cntSub
                cntSub++;
            }
        }

        // Remove all elements
        // from the subarray
        cntFreq = new Map();

        // Update cntUnique
        cntUnique = 0;
    }
    return cntSub;
}

// Driver Code
var arr = [1, 1, 2, 2, 2];
var N = arr.length;
document.write( cntSubarrays(arr, N));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
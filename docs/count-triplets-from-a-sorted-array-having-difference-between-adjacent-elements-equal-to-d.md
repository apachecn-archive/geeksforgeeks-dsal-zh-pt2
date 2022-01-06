# 从相邻元素之间的差值等于 D 的排序数组中计数三元组

> 原文:[https://www . geesforgeks . org/count-triples-from-a-sorted-array-相邻元素之间有差异-等于-d/](https://www.geeksforgeeks.org/count-triplets-from-a-sorted-array-having-difference-between-adjacent-elements-equal-to-d/)

给定一个由 **N** 正整数和一个整数 **D** 组成的排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到三元组 **(i，j，k)** 的数量，使得**arr[j]–arr[I]= D**和**arr[k]–arr[j]= D**和 **0 ≤ i < j < k 【T18**

**示例:**

> **输入:** arr[] = {1，2，4，5，7，8，10}，D = 3
> **输出:** 3
> **解释:**
> 以下是相邻元素之间有区别的三元组是 D(= 3)分别是:
> 
> 1.  {1, 4, 7}
> 2.  {4, 7, 10}
> 3.  {2, 5, 8}
> 
> 因此，三胞胎的总数是 3。
> 
> **输入:** arr[] = {1，2，4，5，7，8，10}，D = 1
> **输出:** 0

**天真方法:**解决这个问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/python-ways-to-create-triplets-from-given-list/)的所有三元组，并计算那些相邻元素之间有差异的三元组为 D(= 3)。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过将数组的每个元素视为三元组的最后一个元素并检查前面两个元素即**(arr[I]–D)**和**(arr[I]–2 * D)**是否存在于数组中来进行优化。按照以下步骤解决问题。

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，比如说 **M** ，存储数组元素的频率。
*   初始化一个变量，说 **ans** 为 **0** 。
*   [遍历给定数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，并执行以下步骤:
    *   在散列表 **M** 中，将**arr【I】**的频率增加 **1** 。
    *   现在，检查元素**(arr[I]–D)**和**(arr[I]–2 * D)**是否存在于哈希表中。如果发现**为真**，则将**和**的值增加**freq[arr[I]–D]* freq[arr[I]–2 * D]**。
*   完成上述步骤后，打印**和**的值，作为数组中三元组的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// triplets having difference
// between adjacent  elements equal to D
int countTriplets(int D, vector<int>& arr)
{
    // Stores the frequency
    // of array elements
    unordered_map<int, int> freq;

    // Stores the count of
    // resultant triplets
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < arr.size(); i++) {

        // Check if arr[i] - D and
        // arr[i] - 2 * D  exists
        // in the Hashmap or not
        if (freq.find(arr[i] - D)
                != freq.end()
            && freq.find(arr[i] - 2 * D)
                   != freq.end()) {

            // Update the value of ans
            ans += freq[arr[i] - D]
                   * freq[arr[i] - 2 * D];
        }

        // Increase the frequency
        // of the current element
        freq[arr[i]]++;
    }

    // Return the resultant count
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr{ 1, 2, 4, 5, 7, 8, 10 };
    int D = 1;
    cout << countTriplets(D, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number of
// triplets having difference
// between adjacent  elements equal to D
static int countTriplets(int D, int []arr)
{

    // Stores the frequency
    // of array elements
    HashMap<Integer,
            Integer> freq = new HashMap<Integer,
                                        Integer>();

    // Stores the count of
    // resultant triplets
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < arr.length; i++)
    {

        // Check if arr[i] - D and
        // arr[i] - 2 * D  exists
        // in the Hashmap or not
        if (freq.containsKey(arr[i] - D) &&
            freq.containsKey(arr[i] - 2 * D))
        {

            // Update the value of ans
            ans += freq.get(arr[i] - D) *
                   freq.get(arr[i] - 2 * D);
        }

        // Increase the frequency
        // of the current element
        if (freq.containsKey(arr[i]))
        {
            freq.put(arr[i], freq.get(arr[i]) + 1);
        }
        else
        {
            freq.put(arr[i], 1);
        }
    }

    // Return the resultant count
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 1, 2, 4, 5, 7, 8, 10 };
    int D = 1;

    System.out.print(countTriplets(D, arr));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# triplets having difference
# between adjacent  elements equal to D
def countTriplets(D, arr):

    # Stores the frequency
    # of array elements
    freq = {}

    # Stores the count of
    # resultant triplets
    ans = 0

    # Traverse the array
    for i in range(len(arr)):

        # Check if arr[i] - D and
        # arr[i] - 2 * D  exists
        # in the Hashmap or not
        if (((arr[i] - D) in freq) and
             (arr[i] - 2 * D) in freq):

            # Update the value of ans
            ans += (freq[arr[i] - D] *
                    freq[arr[i] - 2 * D])

        # Increase the frequency
        # of the current element
        freq[arr[i]] = freq.get(arr[i], 0) + 1

    # Return the resultant count
    return ans

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 4, 5, 7, 8, 10 ]
    D = 1

    print (countTriplets(D, arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of
// triplets having difference
// between adjacent  elements equal to D
static int countTriplets(int D, int[] arr)
{

    // Stores the frequency
    // of array elements
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    // Stores the count of
    // resultant triplets
    int ans = 0;

    // Traverse the array
    for(int i = 0; i < arr.Length; i++)
    {

        // Check if arr[i] - D and
        // arr[i] - 2 * D  exists
        // in the Hashmap or not
        if (freq.ContainsKey(arr[i] - D) &&
            freq.ContainsKey(arr[i] - 2 * D))
        {

            // Update the value of ans
            ans += freq[arr[i] - D] *
                   freq[arr[i] - 2 * D];
        }

        // Increase the frequency
        // of the current element
        if (!freq.ContainsKey(arr[i]))
            freq[arr[i]] = 0;

        freq[arr[i]]++;
    }

    // Return the resultant count
    return ans;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 4, 5, 7, 8, 10 };
    int D = 1;

    Console.WriteLine(countTriplets(D, arr));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to count the number of
// triplets having difference
// between adjacent  elements equal to D
function countTriplets(D, arr)
{
    // Stores the frequency
    // of array elements
    var freq = new Map();

    // Stores the count of
    // resultant triplets
    var ans = 0;
    var i;

    // Traverse the array
    for (i = 0; i < arr.length; i++) {

        // Check if arr[i] - D and
        // arr[i] - 2 * D  exists
        // in the Hashmap or not
        if (freq.has(arr[i] - D) && freq.has(arr[i] - 2 * D)) {

            // Update the value of ans
            ans += freq.get(arr[i] - D) * freq.get(arr[i] - 2 * D);
        }

        // Increase the frequency
        // of the current element
        freq.set(arr[i],freq.get(arr[i])+1);
    }

    // Return the resultant count
    return ans;
}

// Driver Code
    var arr = [1, 2, 4, 5, 7, 8, 10];
    var D = 1;
    document.write(countTriplets(D, arr));

</script>
```

**Output:** 

```
0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
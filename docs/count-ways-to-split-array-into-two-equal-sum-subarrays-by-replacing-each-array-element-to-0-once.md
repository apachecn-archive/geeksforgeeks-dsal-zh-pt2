# 通过将每个数组元素替换为 0 一次，计算将数组拆分为两个相等和的子数组的方法

> 原文:[https://www . geeksforgeeks . org/count-way-通过将每个数组元素替换为 0 一次将数组拆分为两个相等和的子数组/](https://www.geeksforgeeks.org/count-ways-to-split-array-into-two-equal-sum-subarrays-by-replacing-each-array-element-to-0-once/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是在将单个数组元素更改为 **0** 后，计算将[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)拆分为两个相等和的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的方法数。

**示例:**

> **输入:** arr[] = {1，2，-1，3}
> **输出:** 4
> **说明:**
> 将 arr[0]替换为 0，arr[]修改为{0，2，-1，3}。只有一个可能的拆分是{0，2}和{-1，3}。
> 将 arr[1]替换为 0，arr[]修改为{1，0，-1，3}。无法分割数组。
> 将 arr[2]替换为 0，arr[]修改为{1，2，0，3}。两种可能的拆分是{1，2，0}和{3}，{1，2}和{0，3}。
> 将 arr[3]替换为 0，arr[]修改为{1，2，-1，0}。只有一个可能的拆分是{1}和{2，-1，0}。
> 因此，拆分方式总数= 1 + 0 + 2 + 1 = 4。
> 
> **输入:** arr[] = {1，2，1，1，3，1}
> **输出:** 6
> **解释:**
> 将 arr[0]替换为 0，arr[]修改为{0，2，1，1，3，1}。只存在一个可能的拆分。
> 将 arr[1]替换为 0，arr[]修改为{1，0，1，1，3，1}。无法分割数组。
> 将 arr[2]替换为 0，arr[]修改为{1，2，0，1，3，1}。只存在一个可能的拆分。
> 将 arr[3]替换为 0，arr[]修改为{1，2，1，0，3，1}。只存在两种可能的拆分。
> 将 arr[4]替换为 0，arr[]修改为{1，2，1，1，0，1}。只存在一个可能的拆分。
> 将 arr[5]替换为 0，arr[]修改为{1，2，1，1，3，0}。只存在一个可能的拆分。
> 拆分方式总数为= 1 + 0 + 1 + 2 + 1 + 1 = 6。

**天真法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，将每个数组元素**arr【I】**转换为 **0** ，并计算[将修改后的数组拆分为两个和](https://www.geeksforgeeks.org/split-array-two-equal-sum-subarrays/)相等的子数组的方式数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 考虑两个数组 **arr1[]** 和 **arr2[]** ，数组元素的[和分别等于 **sum_arr1** 和 **sum_arr2** 。
> 设 **dif** 为 **sum_arr1** 与 **sum_arr2、**之差，即**sum _ arr 1–sum _ arr 2 = dif**。
> 现在，通过执行以下两个操作中的任意一个，可以使 **sum_arr1** 等于 **sum_arr2** :](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
> 
> *   从 **arr1[]** 中移除一个值等于 **dif** 的元素。
> *   从 **arr2[]** 中移除一个值等于 **-dif** 的元素。
> 
> 因此，获得 **sum_arr1 = sum_arr2** 的途径总数等于 arr1 中 dif 的**计数+arr 2 中(-dif)的计数**。

对于范围**【0，N–1】**中的每个指标，通过将当前指标视为分割点，使用上述过程使任意元素等于 **0** ，可以获得路的总数。按照以下步骤解决问题:

*   用 **0** 初始化变量**计数**以存储所需结果，**前缀 _ 和**用 **0** 存储[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)用 **0** 存储后缀和。
*   初始化[散列表](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **前缀计数**和**后缀计数**以存储前缀和后缀数组中的元素计数。
*   [遍历**arr【】**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[更新**后缀**中各元素](https://www.geeksforgeeks.org/program-to-find-frequency-of-each-element-in-a-vector-using-map-in-c/)的频率。
*   使用变量 **i** 在范围**【0，N–1】**内遍历 arr[]。
    *   将**arr【I】**添加到**前缀**哈希表中，并将其从**后缀**中移除。
    *   将**arr【I】**加到**前缀**上，将**后缀**设置为[数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) 和**前缀**之和的差。
    *   将子数组之和的差值存储在变量**dif = prefix _ sum–sufix sum**中。
    *   将**I<sup>th</sup>T3】索引处的拆分方式数存储在**number _ of _ subarray _ at _ I _ split**中，并等于 **prefixCount** 和**后缀 Count** 之和。**
    *   通过添加**数量 _ 子阵列 _at_i_split** 来更新**计数**。
*   完成上述步骤后，打印计数值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of ways to
// split array into 2 subarrays having
// equal sum by changing element to 0 once
int countSubArrayRemove(int arr[], int N)
{
    // Stores the count of elements
    // in prefix and suffix of
    // array elements
    unordered_map<int, int>
        prefix_element_count,
        suffix_element_count;

    // Stores the sum of array
    int total_sum_of_elements = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--) {

        total_sum_of_elements += arr[i];

        // Increase the frequency of
        // current element in suffix
        suffix_element_count[arr[i]]++;
    }

    // Stores prefix sum upto index i
    int prefix_sum = 0;

    // Stores sum of suffix of index i
    int suffix_sum = 0;

    // Stores the desired result
    int count_subarray_equal_sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Modify prefix sum
        prefix_sum += arr[i];

        // Add arr[i] to prefix map
        prefix_element_count[arr[i]]++;

        // Calculate suffix sum by
        // subtracting prefix sum
        // from total sum of elements
        suffix_sum = total_sum_of_elements
                     - prefix_sum;

        // Remove arr[i] from suffix map
        suffix_element_count[arr[i]]--;

        // Store the difference
        // between the subarrays
        int difference = prefix_sum
                         - suffix_sum;

        // Count number of ways to split
        // the array at index i such that
        // subarray sums are equal
        int number_of_subarray_at_i_split
            = prefix_element_count[difference]
              + suffix_element_count[-difference];

        // Update the final result
        count_subarray_equal_sum
            += number_of_subarray_at_i_split;
    }

    // Return the result
    return count_subarray_equal_sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 1, 1, 3, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countSubArrayRemove(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find number of ways to
// split array into 2 subarrays having
// equal sum by changing element to 0 once
static int countSubArrayRemove(int []arr, int N)
{

    // Stores the count of elements
    // in prefix and suffix of
    // array elements
    HashMap<Integer,
            Integer> prefix_element_count = new HashMap<Integer,
                                                        Integer>();
    HashMap<Integer,
            Integer> suffix_element_count = new HashMap<Integer,
                                                        Integer>();

    // Stores the sum of array
    int total_sum_of_elements = 0;

    // Traverse the array
    for(int i = N - 1; i >= 0; i--)
    {
        total_sum_of_elements += arr[i];

        // Increase the frequency of
        // current element in suffix
        if (!suffix_element_count.containsKey(arr[i]))
            suffix_element_count.put(arr[i], 1);
        else
            suffix_element_count.put(arr[i],
              suffix_element_count.get(arr[i]) + 1);
    }

    // Stores prefix sum upto index i
    int prefix_sum = 0;

    // Stores sum of suffix of index i
    int suffix_sum = 0;

    // Stores the desired result
    int count_subarray_equal_sum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Modify prefix sum
        prefix_sum += arr[i];

        // Add arr[i] to prefix map
       if (!prefix_element_count.containsKey(arr[i]))
           prefix_element_count.put(arr[i], 1);
       else
           prefix_element_count.put(arr[i],
           prefix_element_count.get(arr[i]) + 1);

        // Calculate suffix sum by
        // subtracting prefix sum
        // from total sum of elements
        suffix_sum = total_sum_of_elements -
                     prefix_sum;

        // Remove arr[i] from suffix map
        if (!suffix_element_count.containsKey(arr[i]))
            suffix_element_count.put(arr[i], 0);
        else
            suffix_element_count.put(arr[i],
            suffix_element_count.get(arr[i]) - 1);

        // Store the difference
        // between the subarrays
        int difference = prefix_sum -
                         suffix_sum;

        // Count number of ways to split
        // the array at index i such that
        // subarray sums are equal
        int number_of_subarray_at_i_split = 0;
        if (prefix_element_count.containsKey(difference))
            number_of_subarray_at_i_split =
            prefix_element_count.get(difference);
        if (suffix_element_count.containsKey(-difference))
            number_of_subarray_at_i_split +=
            suffix_element_count.get(-difference);

        // Update the final result
        count_subarray_equal_sum +=
        number_of_subarray_at_i_split;
    }

    // Return the result
    return count_subarray_equal_sum;
}  

// Driver Code
public static void main(String args[])
{
    int []arr = { 1, 2, 1, 1, 3, 1 };
    int N = arr.length;

    // Function Call
    System.out.println(countSubArrayRemove(arr, N));
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find number of ways to
# split array into 2 subarrays having
# equal sum by changing element to 0 once
def countSubArrayRemove(arr, N):

    # Stores the count of elements
    # in prefix and suffix of
    # array elements
    prefix_element_count = {}
    suffix_element_count = {}

    # Stores the sum of array
    total_sum_of_elements = 0

    # Traverse the array
    i = N - 1
    while (i >= 0):
        total_sum_of_elements += arr[i]

        # Increase the frequency of
        # current element in suffix
        suffix_element_count[arr[i]] = suffix_element_count.get(
            arr[i], 0) + 1

        i -= 1

    # Stores prefix sum upto index i
    prefix_sum = 0

    # Stores sum of suffix of index i
    suffix_sum = 0

    # Stores the desired result
    count_subarray_equal_sum = 0

    # Traverse the array
    for i in range(N):

        # Modify prefix sum
        prefix_sum += arr[i]

        # Add arr[i] to prefix map
        prefix_element_count[arr[i]] = prefix_element_count.get(
            arr[i], 0) + 1

        # Calculate suffix sum by
        # subtracting prefix sum
        # from total sum of elements
        suffix_sum = total_sum_of_elements - prefix_sum

        # Remove arr[i] from suffix map
        suffix_element_count[arr[i]] = suffix_element_count.get(
            arr[i], 0) - 1

        # Store the difference
        # between the subarrays
        difference = prefix_sum - suffix_sum

        # Count number of ways to split
        # the array at index i such that
        # subarray sums are equal
        number_of_subarray_at_i_split = (prefix_element_count.get(
                                             difference, 0) +
                                         suffix_element_count.get(
                                            -difference, 0))

        # Update the final result
        count_subarray_equal_sum += number_of_subarray_at_i_split

    # Return the result
    return count_subarray_equal_sum

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 1, 1, 3, 1 ]
    N =  len(arr)

    # Function Call
    print(countSubArrayRemove(arr, N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find number of ways to
// split array into 2 subarrays having
// equal sum by changing element to 0 once
static int countSubArrayRemove(int []arr, int N)
{

    // Stores the count of elements
    // in prefix and suffix of
    // array elements
    Dictionary<int,
               int> prefix_element_count = new Dictionary<int,
                                                          int> ();
    Dictionary<int,
               int >suffix_element_count = new Dictionary <int,
                                                           int>();

    // Stores the sum of array
    int total_sum_of_elements = 0;

    // Traverse the array
    for(int i = N - 1; i >= 0; i--)
    {
        total_sum_of_elements += arr[i];

        // Increase the frequency of
        // current element in suffix
        if (!suffix_element_count.ContainsKey(arr[i]))
            suffix_element_count[arr[i]] = 1;
        else
            suffix_element_count[arr[i]]++;
    }

    // Stores prefix sum upto index i
    int prefix_sum = 0;

    // Stores sum of suffix of index i
    int suffix_sum = 0;

    // Stores the desired result
    int count_subarray_equal_sum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Modify prefix sum
        prefix_sum += arr[i];

        // Add arr[i] to prefix map
       if (!prefix_element_count.ContainsKey(arr[i]))
           prefix_element_count[arr[i]] = 1;
       else
           prefix_element_count[arr[i]]++;

        // Calculate suffix sum by
        // subtracting prefix sum
        // from total sum of elements
        suffix_sum = total_sum_of_elements -
                     prefix_sum;

        // Remove arr[i] from suffix map
        if (!suffix_element_count.ContainsKey(arr[i]))
            suffix_element_count[arr[i]] = 0;
        else
            suffix_element_count[arr[i]]-= 1;

        // Store the difference
        // between the subarrays
        int difference = prefix_sum -
                         suffix_sum;

        // Count number of ways to split
        // the array at index i such that
        // subarray sums are equal
        int number_of_subarray_at_i_split = 0;
        if (prefix_element_count.ContainsKey(difference))
            number_of_subarray_at_i_split
            = prefix_element_count[difference];
        if (suffix_element_count.ContainsKey(-difference))
            number_of_subarray_at_i_split
            += suffix_element_count[-difference];

        // Update the final result
        count_subarray_equal_sum
            += number_of_subarray_at_i_split;
    }

    // Return the result
    return count_subarray_equal_sum;
}

// Driver Code
public static void Main(string []args)
{
    int []arr = { 1, 2, 1, 1, 3, 1 };
    int N = arr.Length;

    // Function Call
    Console.Write(countSubArrayRemove(arr, N));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find number of ways to
// split array into 2 subarrays having
// equal sum by changing element to 0 once
function countSubArrayRemove(arr, N)
{

    // Stores the count of elements
    // in prefix and suffix of
    // array elements
    let prefix_element_count = new Map();
    let suffix_element_count = new Map();

    // Stores the sum of array
    let total_sum_of_elements = 0;

    // Traverse the array
    for(let i = N - 1; i >= 0; i--)
    {
        total_sum_of_elements += arr[i];

        // Increase the frequency of
        // current element in suffix
        if (!suffix_element_count.has(arr[i]))
            suffix_element_count.set(arr[i], 1);
        else
            suffix_element_count.set(arr[i],
            suffix_element_count.get(arr[i]) + 1);
    }

    // Stores prefix sum upto index i
    let prefix_sum = 0;

    // Stores sum of suffix of index i
    let suffix_sum = 0;

    // Stores the desired result
    let count_subarray_equal_sum = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Modify prefix sum
        prefix_sum += arr[i];

        // Add arr[i] to prefix map
       if (!prefix_element_count.has(arr[i]))
           prefix_element_count.set(arr[i], 1);
       else
           prefix_element_count.set(arr[i],
           prefix_element_count.get(arr[i]) + 1);

        // Calculate suffix sum by
        // subtracting prefix sum
        // from total sum of elements
        suffix_sum = total_sum_of_elements -
                     prefix_sum;

        // Remove arr[i] from suffix map
        if (!suffix_element_count.has(arr[i]))
            suffix_element_count.set(arr[i], 0);
        else
            suffix_element_count.set(arr[i],
            suffix_element_count.get(arr[i]) - 1);

        // Store the difference
        // between the subarrays
        let difference = prefix_sum -
                         suffix_sum;

        // Count number of ways to split
        // the array at index i such that
        // subarray sums are equal
        let number_of_subarray_at_i_split = 0;
        if (prefix_element_count.has(difference))
            number_of_subarray_at_i_split =
            prefix_element_count.get(difference);
        if (suffix_element_count.has(-difference))
            number_of_subarray_at_i_split +=
            suffix_element_count.get(-difference);

        // Update the final result
        count_subarray_equal_sum +=
        number_of_subarray_at_i_split;
    }

    // Return the result
    return count_subarray_equal_sum;
}

// Driver Code
let arr = [ 1, 2, 1, 1, 3, 1 ];
let  N = arr.length;

// Function Call
document.write(countSubArrayRemove(arr, N));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
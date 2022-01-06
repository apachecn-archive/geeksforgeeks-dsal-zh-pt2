# 一对乘积等于另一对乘积的四倍计数

> 原文:[https://www . geesforgeks . org/四倍计数与剩余对的乘积相等/](https://www.geeksforgeeks.org/count-of-quadruples-with-product-of-a-pair-equal-to-the-product-of-the-remaining-pair/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算数组中唯一四元组 **(a，b，c，d)** 的数量，使得四元组的任意一对元素的乘积等于剩余一对元素的乘积。

**示例:**

> **输入:** arr[] = {2，3，4，6}
> **输出:** 8
> **解释:**
> 数组中有 8 个四元组，即(2，6，3，4)，(2，6，4，3)，(6，2，3，4)，(6，2，4，3)，(3，4，2，6)，(4，3，2，6)，(3，4，2，6)，(3，4，4，4，2，6)，(3，4，4，3，6，6，2)，满足
> 因此，四倍体的总数是 8。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 0
> **说明:**不存在满足给定条件的四元组。

**简单方法:**最简单的方法是使用四个[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)从给定的[数组](https://www.geeksforgeeks.org/array-data-structure/)生成所有可能的四元组，对于遇到的每个唯一的四元组，检查它是否满足给定的条件。最后，打印获得的这种三胞胎的计数。

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。要解决这个问题，请将每一对不同的产品存储在散列表 **M** 中。

> 满足给定条件的每一个四元组(a，b，c，d)有 8 个排列:
> 排列方式数(a，b) = 2 {(a，b)，(b，a)}
> 排列方式数(c，d) = 2 {(c，d)，(d，c)}
> 排列方式数(a，b)和(c，d) = 8 {(a，b，c，d)，(a，b，d，c)，(b，a，c，d)，(b，c，d)，(b，c，d)，(b，c，d)，(b，c，d)，(b，c，d)，(b，a，b，a，a，a，a，d)
> 因此，总路数= 8。

按照以下步骤解决问题:

*   将 **res** 初始化为 **0** 以存储最终四胞胎的计数。
*   创建一个 [hashmap](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-pairs-in-c/) **M** 来存储数组中不同对的[乘积的频率。](https://www.geeksforgeeks.org/count-all-distinct-pairs-with-product-equal-to-k/)
*   现在，生成给定数组的所有可能的不同对 **(arr[i]，arr[j])** ，并执行以下操作:
    *   将 **arr[i]** 和 **arr[j]** 的乘积存储在变量 **prod** 中。
    *   将 **(8*M【生产】)**的值添加到变量 **res** 中。
    *   通过 **1** 增加 **M** 哈希表中**戳**的频率。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// unique quadruples from an array
// that satisfies the given condition
void sameProductQuadruples(int nums[],
                           int N)
{
    // Hashmap to store
    // the product of pairs
    unordered_map<int, int> umap;

    // Store the count of
    // required quadruples
    int res = 0;

    // Traverse the array arr[] and
    // generate all possible pairs
    for (int i = 0; i < N; ++i) {
        for (int j = i + 1; j < N; ++j) {

            // Store their product
            int prod = nums[i] * nums[j];

            // Pair(a, b) can be used to
            // generate 8 unique permutations
            // with another pair (c, d)
            res += 8 * umap[prod];

            // Increment um[prod] by 1
            ++umap[prod];
        }
    }

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    sameProductQuadruples(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

// Function to count the number of
// unique quadruples from an array
// that satisfies the given condition
static void sameProductQuadruples(int[] nums,
                           int N)
{
    // Hashmap to store
    // the product of pairs
    int[] umap = new int[10000];

    // Store the count of
    // required quadruples
    int res = 0;

    // Traverse the array arr[] and
    // generate all possible pairs
    for (int i = 0; i < N; ++i)
    {
        for (int j = i + 1; j < N; ++j)
        {

            // Store their product
            int prod = nums[i] * nums[j];

            // Pair(a, b) can be used to
            // generate 8 unique permutations
            // with another pair (c, d)
            res += 8 * umap[prod];

            // Increment um[prod] by 1
            ++umap[prod];
        }
    }

    // Print the result
     System.out.println(res);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 3, 4, 6 };
    int N = arr.length;

    sameProductQuadruples(arr, N);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the number of
# unique quadruples from an array
# that satisfies the given condition
def sameProductQuadruples(nums, N) :

    # Hashmap to store
    # the product of pairs
    umap = {};

    # Store the count of
    # required quadruples
    res = 0;

    # Traverse the array arr[] and
    # generate all possible pairs
    for i in range(N) :
        for j in range(i + 1, N) :

            # Store their product
            prod = nums[i] * nums[j];   
            if prod in umap :

                # Pair(a, b) can be used to
                # generate 8 unique permutations
                # with another pair (c, d)
                res += 8 * umap[prod];

                # Increment umap[prod] by 1
                umap[prod] += 1;
            else:
                umap[prod] = 1

    # Print the result
    print(res);

# Driver Code
if __name__ == "__main__" :

    arr = [ 2, 3, 4, 6 ];
    N = len(arr);

    sameProductQuadruples(arr, N);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to count the number of
// unique quadruples from an array
// that satisfies the given condition
static void sameProductQuadruples(int[] nums,
                           int N)
{
    // Hashmap to store
    // the product of pairs
    int[] umap = new int[10000];

    // Store the count of
    // required quadruples
    int res = 0;

    // Traverse the array arr[] and
    // generate all possible pairs
    for (int i = 0; i < N; ++i)
    {
        for (int j = i + 1; j < N; ++j)
        {

            // Store their product
            int prod = nums[i] * nums[j];

            // Pair(a, b) can be used to
            // generate 8 unique permutations
            // with another pair (c, d)
            res += 8 * umap[prod];

            // Increment um[prod] by 1
            ++umap[prod];
        }
    }

    // Print the result
    Console.Write(res);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 2, 3, 4, 6 };
    int N = arr.Length;

    sameProductQuadruples(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
      // JavaScript program to implement
      // the above approach
      // Function to count the number of
      // unique quadruples from an array
      // that satisfies the given condition
      function sameProductQuadruples(nums, N) {
        // Hashmap to store
        // the product of pairs
        var umap = new Array(10000).fill(0);

        // Store the count of
        // required quadruples
        var res = 0;

        // Traverse the array arr[] and
        // generate all possible pairs
        for (var i = 0; i < N; ++i) {
          for (var j = i + 1; j < N; ++j) {
            // Store their product
            var prod = nums[i] * nums[j];

            // Pair(a, b) can be used to
            // generate 8 unique permutations
            // with another pair (c, d)
            res += 8 * umap[prod];

            // Increment um[prod] by 1
            ++umap[prod];
          }
        }

        // Print the result
        document.write(res);
      }

      // Driver Code
      var arr = [2, 3, 4, 6];
      var N = arr.length;

      sameProductQuadruples(arr, N);
</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*
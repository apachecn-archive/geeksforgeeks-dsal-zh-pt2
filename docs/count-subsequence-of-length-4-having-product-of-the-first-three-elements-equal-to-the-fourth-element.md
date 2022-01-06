# 计算长度为 4 的子序列，其前三个元素的乘积等于第四个元素

> 原文:[https://www . geeksforgeeks . org/count-长度为 4 的子序列具有等于第四个元素的前三个元素的乘积/](https://www.geeksforgeeks.org/count-subsequence-of-length-4-having-product-of-the-first-three-elements-equal-to-the-fourth-element/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出长度为 4 的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，其中前三个元素的乘积等于第四个元素。

**示例:**

> **输入:** arr[] = {10，2，2，7，40，160}
> **输出:** 2
> **解释:**
> 以下是满足给定标准的长度为 4 的子序列:
> 
> 1.  {10，2，2，40}，前三个元素的乘积是 10*2*2 = 40(=第四个元素)。
> 2.  {2，2，40，160}，前三个元素的乘积是 2*2*40 = 160(=第四个元素)。
> 
> 因此，子序列的总数是 2。
> 
> **输入:** arr[] = {1，1，1，1}
> **输出:** 1

**天真方法:**解决给定问题的最简单方法是[生成所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并对满足给定标准的子序列进行计数。检查所有子序列后，打印获得的总计数。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效法:**上述方法也可以通过找到所有长度的子序列 **3** 并将三者的乘积存储在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中，然后通过将每个元素固定为第四个元素并增加三者乘积的频率来计算子序列来进行优化。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说**和**为 **0** ，它存储结果子序列的计数。
*   初始化一个[无序地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)比如说 **M** ，存储三元组乘积的[频率。](https://www.geeksforgeeks.org/count-number-triplets-product-equal-given-number/)
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   将**和**的值增加**arr【I】**，将其视为[子序列的第四个元素。](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)
    *   [在范围**【0，I–1】**内生成所有可能的数组对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并将两者乘积的频率与**arr【I】**一起存储在地图 **M** 中。
*   完成上述步骤后，打印**和**的值作为子序列的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total number of
// subsequences satisfying the given
// criteria
int countQuadruples(int A[], int N)
{
    // Stores the count of quadruplets
    int ans = 0;

    // Stores the frequency of product
    // of the triplet
    unordered_map<int, int> freq;

    // Traverse the given array arr[]
    for (int i = 0; i < N; i++) {

        // Consider arr[i] as fourth
        // element of subsequences
        ans += freq[A[i]];

        // Generate all possible pairs
        // of the array [0, i - 1]
        for (int j = 0; j < i; j++) {

            for (int k = 0; k < j; k++) {

                // Increment the frequency
                // of the triplet
                freq[A[i] * A[j] * A[k]]++;
            }
        }
    }

    // Return the total count obtained
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 10, 2, 2, 7, 40, 160 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countQuadruples(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

    // Function to find the total number of
    // subsequences satisfying the given
    // criteria
    static int countQuadruples(int A[], int N)
    {

        // Stores the count of quadruplets
        int ans = 0;

        // Stores the frequency of product
        // of the triplet
        HashMap<Integer, Integer> freq = new HashMap<Integer, Integer>();

        // Traverse the given array arr[]
        for (int i = 0; i < N; i++) {

            // Consider arr[i] as fourth
            // element of subsequences
            if (freq.containsKey(A[i]))
                ans += freq.get(A[i]);

            // Generate all possible pairs
            // of the array [0, i - 1]
            for (int j = 0; j < i; j++) {

                for (int k = 0; k < j; k++) {

                    // Increment the frequency
                    // of the triplet
                    if (freq.containsKey(A[i] * A[j] * A[k]))
                    {
                        freq.put(A[i] * A[j] * A[k], freq.get(A[i] * A[j] * A[k]) + 1);
                    }
                  else
                  {
                        freq.put(A[i] * A[j] * A[k], 1);
                    }
                }
            }
        }

        // Return the total count obtained
        return ans;
    }

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 10, 2, 2, 7, 40, 160 };
    int N = arr.length;

    System.out.print(countQuadruples(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the total number of
# subsequences satisfying the given
# criteria
def countQuadruples(A, N):
    # Stores the count of quadruplets
    ans = 0

    # Stores the frequency of product
    # of the triplet
    freq = {}

    # Traverse the given array arr[]
    for i in range(N):

        # Consider arr[i] as fourth
        # element of subsequences
        if A[i] in freq:
            ans += freq[A[i]]
        else:
            freq[A[i]] = 0

        # Generate all possible pairs
        # of the array [0, i - 1]
        for j in range(i):
            for k in range(j):

                # Increment the frequency
                # of the triplet
                if A[i] * A[j] * A[k] in freq:
                    freq[A[i] * A[j] * A[k]] += 1
                else:
                    freq[A[i] * A[j] * A[k]] = 1

    # Return the total count obtained
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [10, 2, 2, 7, 40, 160]
    N = len(arr)

    print(countQuadruples(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the total number of
// subsequences satisfying the given
// criteria
static int countQuadruples(int []A, int N)
{

    // Stores the count of quadruplets
    int ans = 0;

    // Stores the frequency of product
    // of the triplet
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Traverse the given array arr[]
    for (int i = 0; i < N; i++) {

        // Consider arr[i] as fourth
        // element of subsequences
        if(freq.ContainsKey(A[i]))
          ans += freq[A[i]];
        else
          freq.Add(A[i],0);

        // Generate all possible pairs
        // of the array [0, i - 1]
        for (int j = 0; j < i; j++) {

            for (int k = 0; k < j; k++) {

                // Increment the frequency
                // of the triplet

              if(freq.ContainsKey(A[i] * A[j] * A[k]))
                freq[A[i] * A[j] * A[k]]++;
              else
                freq.Add(A[i] * A[j] * A[k],1);
            }
        }
    }

    // Return the total count obtained
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 10, 2, 2, 7, 40, 160 };
    int N = arr.Length;

    Console.Write(countQuadruples(arr, N));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to find the total number of
        // subsequences satisfying the given
        // criteria
        function countQuadruples(A, N)
        {

            // Stores the count of quadruplets
            let ans = 0;

            // Stores the frequency of product
            // of the triplet
            let freq = new Map();

            // Traverse the given array arr[]
            for (let i = 0; i < N; i++) {

                // Consider arr[i] as fourth
                // element of subsequences
                if (freq.has(arr[i])) {
                    ans += freq.get(A[i]);
                }

                // Generate all possible pairs
                // of the array [0, i - 1]
                for (let j = 0; j < i; j++) {

                    for (let k = 0; k < j; k++) {

                        // Increment the frequency
                        // of the triplet
                        if (freq.has(A[i] * A[j] * A[k])) {
                            freq.set(freq.get(A[i] * A[j] * A[k]), freq.get([A[i] * A[j] * A[k]]) + 1);
                        }
                        else {
                            freq.set(A[i] * A[j] * A[k], 1);
                        }
                    }
                }
            }

            // Return the total count obtained
            return ans;
        }

        // Driver Code
        let arr = [10, 2, 2, 7, 40, 160];
        let N = arr.length;
        document.write(countQuadruples(arr, N));

   // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>3</sup> )*
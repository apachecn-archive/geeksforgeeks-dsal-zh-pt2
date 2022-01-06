# 阵列中所有相邻对的总和不超过 K 所需的最小减量

> 原文:[https://www . geesforgeks . org/minimum-reductions-required-这样阵列中所有相邻对的总和就不会超过-k/](https://www.geeksforgeeks.org/minimum-decrements-required-such-that-sum-of-all-adjacent-pairs-in-an-array-does-not-exceed-k/)

给定一个由 **N** 正整数和一个整数 **K** 组成的数组**a【】**，任务是找到使相邻元素之和小于或等于 **K** 所需的最小操作数，其中，一个操作包括将任意数组元素减 1。对于给定数组中的每个第**I**元素，可以执行 **0** 到**a【I】**次操作。因为答案可以很大，所以以 **10 <sup>9</sup> + 7** 为模计算。

**示例:**

> ***输入*** **:** a[] = {11，3，13，10，8，17，22}，K = 14
> ***输出*** **:** 34
> **说明:**
> 获得所需排列所需的最小操作次数如下:
> 
> *   将[2]减少 2
> *   将[3]减 7
> *   将[5]减少 11
> *   将 a[6]减少 14
> 
> 给定数组被修改为以下排列= {11，3，11，3，8，6，8}
> 操作总数为 2 + 5 + 7 + 11 + 18 = 34。
> 
> **输入:**a[]= { 10000000000，10000000000，1000000000}，K = 0
> **输出 3:**9999999979
> **解释:**
> 由于要求相邻对之和为 0，因此需要将数组中的所有元素减为 0。
> 所以答案是数组的和(10 <sup>9</sup> + 7)。
> 数组之和为 4000000000
> 因此，需要的答案为 400000000% 10<sup>9</sup>+7 = 999999979

**进场:**

按照以下步骤解决问题:

1.  迭代数组 **a[]** ，对于每个相邻的对，检查它们的和是否小于或等于 **K.** 如果发现为真，则不需要更改。
2.  对于总和大于 **K、**的对，遵循以下步骤:
    *   如果对的第一个元素超过 **K** ，使对中第一个元素的值等于 **K** 。增加第一个元素的**值所需的操作次数–K**并将配对的第一个元素的值更新为 **K** 。
    *   现在，对第二个元素应用**对-K 的和**运算，确保对的和等于 **K** ，并将对的第二个元素更新为第一个元素的**K-值。**
3.  对所有元素重复上述步骤，并打印计算出的操作数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of operations required
int minimum_required_operations(int arr[],
                                int n, int k)
{

    // Stores the total number
    // of operations
    int answer = 0;

    long long mod = 1000000007;

    // Iterate over the array
    for(int i = 0; i < n - 1; i++)
    {

        // If the sum of pair of adjacent
        // elements exceed k.
        if (arr[i] + arr[i + 1] > k)
        {

            // If current element exceeds k
            if (arr[i] > k)
            {

                // Reduce arr[i] to k
                answer += (arr[i] - k);
                arr[i] = k;
            }

            // Update arr[i + 1] accordingly
            answer += (arr[i] + arr[i + 1]) - k;
            arr[i + 1] = (k - arr[i]);

            // Update answer
            answer %= mod;
        }
    }
    return answer;
}

// Driver Code
int main()
{
    int a[] = { 9, 50, 4, 14, 42, 89 };
    int k = 10;
    int n = sizeof(a) / sizeof(a[0]);

    cout << (minimum_required_operations(a, n, k));

    return 0;
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to calculate the minimum
// number of operations required
static int minimum_required_operations(int arr[],
                                       int n, int k)
{

    // Stores the total number
    // of operations
    int answer = 0;

    long mod = 1000000007;

    // Iterate over the array
    for(int i = 0; i < n - 1; i++)
    {

        // If the sum of pair of adjacent
        // elements exceed k.
        if (arr[i] + arr[i + 1] > k)
        {

            // If current element exceeds k
            if (arr[i] > k)
            {

                // Reduce arr[i] to k
                answer += (arr[i] - k);
                arr[i] = k;
            }

            // Update arr[i + 1] accordingly
            answer += (arr[i] + arr[i + 1]) - k;
            arr[i + 1] = (k - arr[i]);

            // Update answer
            answer %= mod;
        }
    }
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 9, 50, 4, 14, 42, 89 };
    int k = 10;
    int n = a.length;

    System.out.print(
        minimum_required_operations(a, n, k));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to calculate the minimum
# number of operations required
def minimum_required_operations(arr, n, k):

    # Stores the total number
    # of operations
    answer = 0

    mod = 10 ** 9 + 7

    # Iterate over the array
    for i in range(n - 1):

        # If the sum of pair of adjacent
        # elements exceed k.
        if arr[i] + arr[i + 1] > k:

            # If current element exceeds k
            if arr[i] > k:

              # Reduce arr[i] to k
                answer += (arr[i] - k)
                arr[i] = k

            # Update arr[i + 1] accordingly
            answer += (arr[i] + arr[i + 1]) - k
            arr[i + 1] = (k - arr[i])

            # Update answer
            answer %= mod

    return answer

# Driver Code

a = [9, 50, 4, 14, 42, 89]
k = 10

print(minimum_required_operations(a, len(a), k))
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

  // Function to calculate the minimum
  // number of operations required
  static int minimum_required_operations(int[] arr, int n,
                                         int k)
  {

    // Stores the total number
    // of operations
    int answer = 0;

    long mod = 1000000007;

    // Iterate over the array
    for (int i = 0; i < n - 1; i++)
    {

      // If the sum of pair of adjacent
      // elements exceed k.
      if (arr[i] + arr[i + 1] > k)
      {

        // If current element exceeds k
        if (arr[i] > k)
        {

          // Reduce arr[i] to k
          answer += (arr[i] - k);
          arr[i] = k;
        }

        // Update arr[i + 1] accordingly
        answer += (arr[i] + arr[i + 1]) - k;
        arr[i + 1] = (k - arr[i]);

        // Update answer
        answer = (int)(answer % mod);
      }
    }
    return answer;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] a = { 9, 50, 4, 14, 42, 89 };
    int k = 10;
    int n = a.Length;

    Console.Write(minimum_required_operations(a, n, k));
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Java Script program to implement
// the above approach

// Function to calculate the minimum
// number of operations required
function minimum_required_operations(arr,n,k)
{

    // Stores the total number
    // of operations
    let answer = 0;

    let mod = 1000000007;

    // Iterate over the array
    for(let i = 0; i < n - 1; i++)
    {

        // If the sum of pair of adjacent
        // elements exceed k.
        if (arr[i] + arr[i + 1] > k)
        {

            // If current element exceeds k
            if (arr[i] > k)
            {

                // Reduce arr[i] to k
                answer += (arr[i] - k);
                arr[i] = k;
            }

            // Update arr[i + 1] accordingly
            answer += (arr[i] + arr[i + 1]) - k;
            arr[i + 1] = (k - arr[i]);

            // Update answer
            answer %= mod;
        }
    }
    return answer;
}

// Driver Code

    let a = [ 9, 50, 4, 14, 42, 89 ];
    let k = 10;
    let n = a.length;

    document.write(
        minimum_required_operations(a, n, k));
// This code is contributed by sravan kumar Gottumukkala
</script>
```

**Output:** 

```
178
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
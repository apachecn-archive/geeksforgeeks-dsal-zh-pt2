# 在用最大数字* A 和最小数字* B 之和替换每个元素后，对具有相同 MSD 的相同奇偶索引元素对进行计数

> 原文:[https://www . geeksforgeeks . org/count-对相同奇偶校验索引元素-按最大数字 a 和最小数字 b 之和替换每个元素后/](https://www.geeksforgeeks.org/count-pairs-of-same-parity-indexed-elements-after-replacing-each-element-by-the-sum-of-maximum-digit-a-and-minimum-digits-b/)

给定一个由 **N** 个 3 位数整数和两个整数 **a** 和 **b** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是根据以下规则修改每个数组元素:

*   找到每个数组元素**arr【I】**的[最大值，比如 **M、**和最小位数，比如 **m、**T5。](https://www.geeksforgeeks.org/largest-and-smallest-digit-of-a-number/)
*   将数组元素**arr【I】**更新为 **(A * M + B * m)** 。

任务是计算对的数量，使得选择的元素仅在奇数或偶数索引处，并且[最高有效数字(MSD)](https://www.geeksforgeeks.org/round-off-number-given-number-significant-digits/) 必须相等，并且从该 MSD 形成的对的数量最多为**2**。

**示例:**

> **输入:** arr[] = {234，567，321，345，123，110，767，111}，N = 8，A = 11，B = 7
> **输出:** 3
> **解释:**
> 通过以下操作修改数组元素:
> 
> *   arr[0] (= 234)的最大和最小位数分别为 4 和 2。因此，将 arr[0]替换为 11 * 4 + 7 * 2 = 58。
> *   arr[1] (= 567)的最大和最小位数分别为 7 和 5。因此，将 arr[1]替换为 11 * 7 + 7 * 5 = 77 + 35 = 112。
> *   arr[2] (= 321)和 arr[4] (= 123)的最大和最小位数分别为 3 和 1。因此，用 11 * 3 + 7 * 1 = 40 替换它们。
> *   arr[3] (= 345)的最大和最小位数分别为 5 和 3。因此，将 arr[3]替换为 11 * 5 + 7 * 3 = 76。
> *   arr[5] (= 110)的最大和最小位数分别为 1 和 0。因此，将 arr[5]替换为 11 * 1 + 7 * 0 = 11。
> *   arr[6] (= 767)的最大和最小位数分别为 7 和 6。因此，用 11 * 7 + 7 * 6 = 77 + 42 = 119 替换 arr[6]。
> *   arr[7] (= 111)的最大和最小位数分别为 1 和 2。因此，将 arr[7]替换为 11 * 1 + 7 * 1 = 18。
> 
> 因此，arr[]数组修改为{58，12，40，76，40，11，19，18 }。
> 成对的一种可能方式是{{40，40}、{12，11}、{11，18}}。
> 
> **输入:** arr[] = {123，452，345，124，453}，N = 5，A = 11，B = 7
> **输出:** 1

**方法:**给定的问题可以使用[频率阵列](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)来解决。按照以下步骤解决给定的问题:

*   通过[找到元素](https://www.geeksforgeeks.org/largest-and-smallest-digit-of-a-number/)的最小和最大位数，用 **(A * X + B * Y)%100** 更新**arr【】**的每个数组元素，其中 **X** 和 **Y** 是**arr【I】的最大和最小位数。**
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如**MP【10】【2】，**分别存储 MSD 在偶数和奇数位置的计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，将**MP【arr[I]/10】【I % 2】**的计数增加 **1** 。
*   初始化一个变量，比如说 **res** ，来存储结果对的计数。
*   [迭代范围](https://www.geeksforgeeks.org/different-types-of-range-based-for-loop-iterators-in-c/)**【0，9】**并执行以下步骤:
    *   如果在偶数索引或奇数索引处存在至少 3 个以 **i** 作为 MSD 的**编号，即**MP[I][0]>= 3 | | MP[I][1]>= 3**，则将 **res** 的计数增加 **2** 。**
    *   否则，如果奇数索引处存在一对，偶数索引处存在一对，即**MP[I][0]= = 2&&MP[I][1]= = 2**，则将 **res** 的计数增加 **2** 。
    *   否则，如果在奇数索引或偶数索引处存在 MSD 为 **i** 的对，即 **mp[i][0] == 2 || mp[i][1] == 2** ，则 **res** 的计数增加 **1** 。
*   完成上述步骤后，打印 **res** 的值作为对的计数。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to modify N into
// A * max digit + B * min digit
// and calculate score
int bit_score(int N)
{
    // Stores maximum and minimum digit
    int maxi = 0, mini = 11;

    // Stores the val of N
    int score;

      // Find the maximum and minimum digits
    for (int i = 0; i < 3; i++) {

          // Update maximum digit
        maxi = max(maxi, N % 10);

          // Update minimum digit
        mini = min(mini, N % 10);
        N /= 10;
        if (N == 0)
            break;
    }

    // Calculate the modified number
    score = maxi * 11 + mini * 7;

      // Extract last two digits
    score = score % 100;

      // Return the final score
    return score;
}

// Function to count the number of
// pairs possible from either odd
// or even indices having same MSD
int findPairs(int arr[], int N, int a, int b)
{
    // Update the array
    for (int i = 0; i < N; i++) {
        arr[i] = bit_score(arr[i]);
    }

    // Stores the total number of pairs
    int pairs = 0;

    // Stores the count of numbers having
    // MSD at even or odd position separately
    int mp[10][2];

    // Initialize all elements as 0
    memset(mp, 0, sizeof(mp));

    // Calculate the count of a MSD
    // at even and odd positions
    for (int i = 0; i < N; i++)
        mp[arr[i] / 10][i % 2]++;

    // Iterate over range [0, 9]
    for (int i = 0; i < 10; i++) {

        if (mp[i][1] >= 3 || mp[i][0] >= 3)
            pairs += 2;
        else if (mp[i][1] == 2 && mp[i][0] == 2)
            pairs += 2;
        else if (mp[i][1] == 2 || mp[i][0] == 2)
            pairs += 1;
    }

    // Return the resultant count of pairs
    return pairs;
}

// Driver Code
int main()
{
    int arr[] = { 234, 567, 321, 345,
                  123, 110, 767, 111 };
    int N = sizeof(arr) / sizeof(arr[0]);
      int a = 11, b = 7;

    cout << findPairs(arr, N, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to modify N into
  // A * max digit + B * min digit
  // and calculate score
  static int bit_score(int N)
  {
    // Stores maximum and minimum digit
    int maxi = 0, mini = 11;

    // Stores the val of N
    int score;

    // Find the maximum and minimum digits
    for (int i = 0; i < 3; i++) {

      // Update maximum digit
      maxi = Math.max(maxi, N % 10);

      // Update minimum digit
      mini = Math.min(mini, N % 10);
      N /= 10;
      if (N == 0)
        break;
    }

    // Calculate the modified number
    score = maxi * 11 + mini * 7;

    // Extract last two digits
    score = score % 100;

    // Return the final score
    return score;
  }

  // Function to count the number of
  // pairs possible from either odd
  // or even indices having same MSD
  static int findPairs(int arr[], int N, int a, int b)
  {
    // Update the array
    for (int i = 0; i < N; i++) {
      arr[i] = bit_score(arr[i]);
    }

    // Stores the total number of pairs
    int pairs = 0;

    // Stores the count of numbers having
    // MSD at even or odd position separately
    int mp[][] = new int[10][2];

    // Calculate the count of a MSD
    // at even and odd positions
    for (int i = 0; i < N; i++)
      mp[arr[i] / 10][i % 2]++;

    // Iterate over range [0, 9]
    for (int i = 0; i < 10; i++) {

      if (mp[i][1] >= 3 || mp[i][0] >= 3)
        pairs += 2;
      else if (mp[i][1] == 2 && mp[i][0] == 2)
        pairs += 2;
      else if (mp[i][1] == 2 || mp[i][0] == 2)
        pairs += 1;
    }

    // Return the resultant count of pairs
    return pairs;
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 234, 567, 321, 345, 123, 110, 767, 111 };
    int N = arr.length;
    int a = 11, b = 7;

    System.out.println(findPairs(arr, N, a, b));
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to modify N into
# A * max digit + B * min digit
# and calculate score
def bit_score(N):

    # Stores maximum and minimum digit
    maxi , mini = 0, 11

    # Stores the val of N
    score = 0

      # Find the maximum and minimum digits
    for i in range(3):

          # Update maximum digit
        maxi = max(maxi, N % 10)

          # Update minimum digit
        mini = min(mini, N % 10)
        N //= 10
        if (N == 0):
            break

    # Calculate the modified number
    score = maxi * 11 + mini * 7

      # Extract last two digits
    score = score % 100

      # Return the final score
    return score

# Function to count the number of
# pairs possible from either odd
# or even indices having same MSD
def findPairs(arr, N, a, b):
    #Update the array
    for i in range(N):
        arr[i] = bit_score(arr[i])

    # Stores the total number of pairs
    pairs = 0

    # Stores the count of numbers having
    # MSD at even or odd position separately
    mp = [[0 for i in range(2)] for i in range(10)]

    # Initialize all elements as 0
    # memset(mp, 0, sizeof(mp))

    # Calculate the count of a MSD
    # at even and odd positions
    for i in range(N):
        mp[arr[i] // 10][i % 2] += 1

    # Iterate over range [0, 9]
    for i in range(10):
        if (mp[i][1] >= 3 or mp[i][0] >= 3):
            pairs += 2
        elif (mp[i][1] == 2 and mp[i][0] == 2):
            pairs += 2
        elif (mp[i][1] == 2 or mp[i][0] == 2):
            pairs += 1

    # Return the resultant count of pairs
    return pairs

# Driver Code
if __name__ == '__main__':
    arr = [234, 567, 321, 345, 123, 110, 767, 111]
    N = len(arr)
    a, b = 11, 7

    print (findPairs(arr, N, a, b))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to modify N into
// A * max digit + B * min digit
// and calculate score
static int bit_score(int N)
{

    // Stores maximum and minimum digit
    int maxi = 0, mini = 11;

    // Stores the val of N
    int score;

    // Find the maximum and minimum digits
    for(int i = 0; i < 3; i++)
    {

        // Update maximum digit
        maxi = Math.Max(maxi, N % 10);

        // Update minimum digit
        mini = Math.Min(mini, N % 10);
        N /= 10;

        if (N == 0)
            break;
    }

    // Calculate the modified number
    score = maxi * 11 + mini * 7;

    // Extract last two digits
    score = score % 100;

    // Return the final score
    return score;
}

// Function to count the number of
// pairs possible from either odd
// or even indices having same MSD
static int findPairs(int[] arr, int N,
                     int a, int b)
{

    // Update the array
    for(int i = 0; i < N; i++)
    {
        arr[i] = bit_score(arr[i]);
    }

    // Stores the total number of pairs
    int pairs = 0;

    // Stores the count of numbers having
    // MSD at even or odd position separately
    int[,] mp = new int[10, 2];

    // Calculate the count of a MSD
    // at even and odd positions
    for(int i = 0; i < N; i++)
        mp[arr[i] / 10, i % 2]++;

    // Iterate over range [0, 9]
    for(int i = 0; i < 10; i++)
    {
        if (mp[i, 1] >= 3 || mp[i, 0] >= 3)
            pairs += 2;
        else if (mp[i, 1] == 2 && mp[i, 0] == 2)
            pairs += 2;
        else if (mp[i, 1] == 2 || mp[i, 0] == 2)
            pairs += 1;
    }

    // Return the resultant count of pairs
    return pairs;
}

// Driver Code
public static void Main()
{
    int[] arr = { 234, 567, 321, 345,
                  123, 110, 767, 111 };
    int N = arr.Length;
    int a = 11, b = 7;

    Console.Write(findPairs(arr, N, a, b));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to modify N into
// A * max digit + B * min digit
// and calculate score
function bit_score(N)
{

    // Stores maximum and minimum digit
    let maxi = 0, mini = 11;

    // Stores the val of N
    let score;

    // Find the maximum and minimum digits
    for(let i = 0; i < 3; i++)
    {

        // Update maximum digit
        maxi = Math.max(maxi, N % 10);

        // Update minimum digit
        mini = Math.min(mini, N % 10);
        N /= 10;

        if (N == 0)
            break;
    }

    // Calculate the modified number
    score = maxi * 11 + mini * 7;

    // Extract last two digits
    score = score % 100;

    // Return the final score
    return score;
}

// Function to count the number of
// pairs possible from either odd
// or even indices having same MSD
function findPairs(arr, N, a, b)
{

    // Update the array
    for(let i = 0; i < N; i++)
    {
        arr[i] = bit_score(arr[i]);
    }

    // Stores the total number of pairs
    let pairs = 0;

    // Stores the count of numbers having
    // MSD at even or odd position separately
    let mp = new Array(10);

    // Loop to create 2D array using 1D array
    for (let i = 0; i < mp.length; i++)
    {
        mp[i] = new Array(2);
    }

    for(let i = 0; i < mp.length; i++)
    {
        for(let j = 0; j < mp.length; j++)
        {
            mp[i][j] = 0;
        }
    }

    // Calculate the count of a MSD
    // at even and odd positions
    for(let i = 0; i < N; i++)
        mp[Math.floor(arr[i] / 10)][i % 2]++;

    // Iterate over range [0, 9]
    for(let i = 0; i < 10; i++)
    {
        if (mp[i][1] >= 3 ||
            mp[i][0] >= 3)
            pairs += 2;
        else if (mp[i][1] == 2 &&
                 mp[i][0] == 2)
            pairs += 2;
        else if (mp[i][1] == 2 ||
                 mp[i][0] == 2)
            pairs += 1;
    }

    // Return the resultant count of pairs
    return pairs;
}

// Driver code

// Given Input
let arr = [ 234, 567, 321, 345,
            123, 110, 767, 111 ];
let N = arr.length;
let a = 11, b = 7;

document.write(findPairs(arr, N, a, b));

// This code is contributed by target_2 

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
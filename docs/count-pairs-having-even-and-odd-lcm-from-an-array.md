# 阵列中具有偶数和奇数 LCM 的对的计数

> 原文:[https://www . geeksforgeeks . org/count-pairs-拥有来自数组的偶数和奇数-LCM/](https://www.geeksforgeeks.org/count-pairs-having-even-and-odd-lcm-from-an-array/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算具有偶数 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 和奇数 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 的对的数量。

**示例:**

> **输入:** arr[] = {3，6，5，4}
> **输出:**偶= 5，奇= 1
> **说明:**的(3，6)LCM 为 6，的(3，5)LCM 为 15，的(3，4)LCM 为 12，的(6，5)LCM 为 30，的(6，4)LCM 为 12，的(5，4)LCM 为 20。
> 具有偶数 LCM 的对是(3，6)、(3，4)、(6，5)、(6，4)和(5，4)。
> 只有具有奇数 LCM 的对是(3，5)。
> 
> **输入:** arr[] = {4，7，2，12}
> **输出:**偶数= 6，奇数= 0
> **解释:**具有偶数 LCM = (4，7)，(4，2)，(4，12)，(7，2)，(7，12)，(2，12)的对。
> 没有一对有奇数 LCM。

**天真方法:**最简单的方法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)以获得所有不同的对，并且对于每个对，[计算它们的 LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) 。如果他们的 LCM 是偶数，那么增加偶数的计数。否则，增加奇数的计数。最后，分别打印它们的计数。
***时间复杂度:** O((N <sup>2</sup> )*log(M))，其中 M 是数组中* [*最小的元素*](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/) ****辅助空间:** O(1)**

***有效方法:**为了优化上述方法，该思想基于以下事实:当且仅当两个数字都是奇数时，2 个数字的 **LCM 是奇数**。因此，找出数组中的奇数对总数，并使用偶数 LCM 获得对的计数，从可能对的总数中减去奇数对的计数。*

*按照以下步骤解决问题:*

*   *将配对总数存储在一个变量中，比如 **totalPairs** 。将**总计配对**初始化为**(N *(N-1))/2**。*
*   *将数组中奇数元素的[计数存储在一个变量中，比如 **cnt** 。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)*
*   *将仅由奇数组成的对的计数存储在一个变量中，比如**奇数**。因此，**奇数=(CNT *(CNT–1))/2**。*
*   *完成以上步骤后，打印**奇数**作为奇数 LCM 对的计数值。打印**(总对数–奇数)**作为具有偶数 LCM 的对数。*

*下面是上述方法的实现。*

## *C++*

```
*// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of distinct
// pairs having even LCM and odd LCM
void LCMPairs(int arr[], int N)
{
    // Store the total number of pairs
    int total_pairs = (N * (N - 1)) / 2;

    // Stores the count of odd
    // numbers in the array
    int odd = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        if (arr[i] & 1)
            odd++;
    }

    // Update the count of pairs with odd LCM
    odd = (odd * (odd - 1)) / 2;

    // Print the count of required pairs
    cout << "Even = " << total_pairs - odd
         << ", Odd = " << odd;
}

// Driver Code
int main()
{
    int arr[] = { 3, 6, 5, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    LCMPairs(arr, N);

    return 0;
}*
```

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find count of distinct
// pairs having even LCM and odd LCM
static void LCMPairs(int arr[], int N)
{

    // Store the total number of pairs
    int total_pairs = (N * (N - 1)) / 2;

    // Stores the count of odd
    // numbers in the array
    int odd = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {
        if ((arr[i] & 1) != 0)
            odd++;
    }

    // Update the count of pairs with odd LCM
    odd = (odd * (odd - 1)) / 2;

    // Print the count of required pairs
    System.out.println("Even = " +
                       (total_pairs - odd)  +
                       ", Odd = " + odd);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 6, 5, 4 };
    int N = arr.length;
    LCMPairs(arr, N);
}
}

// This code is contributed by splevel62.*
```

## *蟒蛇 3*

```
*# Python 3 program for the above approach

# Function to find count of distinct
# pairs having even LCM and odd LCM
def LCMPairs(arr, N):
    # Store the total number of pairs
    total_pairs = (N * (N - 1)) / 2

    # Stores the count of odd
    # numbers in the array
    odd = 0

    # Traverse the array arr[]
    for i in range(N):
        if (arr[i] & 1):
            odd += 1

    # Update the count of pairs with odd LCM
    odd = (odd * (odd - 1)) // 2

    # Print the count of required pairs
    print("Even =",int(total_pairs - odd),","," Odd =",odd)

# Driver Code
if __name__ == '__main__':
    arr = [3, 6, 5, 4]
    N = len(arr)
    LCMPairs(arr, N)

     # This code is contributed by ipg2016107.*
```

## *C#*

```
*// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find count of distinct
  // pairs having even LCM and odd LCM
  static void LCMPairs(int[] arr, int N)
  {
    // Store the total number of pairs
    int total_pairs = (N * (N - 1)) / 2;

    // Stores the count of odd
    // numbers in the array
    int odd = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
      if ((arr[i] & 1) != 0)
        odd++;
    }

    // Update the count of pairs with odd LCM
    odd = (odd * (odd - 1)) / 2;

    // Print the count of required pairs
    Console.Write("Even = " + (total_pairs - odd) + ", Odd = " + odd);
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 3, 6, 5, 4 };
    int N = arr.Length;
    LCMPairs(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.*
```

## *java 描述语言*

```
*<script>
// javascript program to implement
// the above approach

    // Function to find count of distinct
    // pairs having even LCM and odd LCM
    function LCMPairs(arr , N) {

        // Store the total number of pairs
        var total_pairs = (N * (N - 1)) / 2;

        // Stores the count of odd
        // numbers in the array
        var odd = 0;

        // Traverse the array arr
        for (i = 0; i < N; i++) {
            if ((arr[i] & 1) != 0)
                odd++;
        }

        // Update the count of pairs with odd LCM
        odd = (odd * (odd - 1)) / 2;

        // Print the count of required pairs
        document.write("Even = " + (total_pairs - odd) + ", Odd = " + odd);
    }

    // Driver Code

        var arr = [ 3, 6, 5, 4 ];
        var N = arr.length;
        LCMPairs(arr, N);

// This code contributed by aashish1995
</script>*
```

***Output:** 

```
Even = 5, Odd = 1
```* 

****时间复杂度:**O(N)*
T5**辅助空间:** O(1)*
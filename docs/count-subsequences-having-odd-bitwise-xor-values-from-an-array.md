# 对数组中具有奇数位异或值的子序列进行计数

> 原文:[https://www . geesforgeks . org/count-subseries-having-odd-bitwise-xor-values-from-a-array/](https://www.geeksforgeeks.org/count-subsequences-having-odd-bitwise-xor-values-from-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是计算给定数组中[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值为奇数的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量。

**示例:**

> **输入:** A[] = {1，3，4}
> **输出:** 4
> **解释:**奇数位异或的子序列为{1}，{3}，{1，4}，{3，4}。
> 
> **输入:** A[] = {2，8，6}
> **输出:** 0
> **说明:**数组中不存在这样的子序列。

**天真方法:**解决问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有子序列，对于每个子序列，检查其**按位异或**值是否为奇数。如果发现是奇数，则将计数增加 1。检查所有子序列后，打印获得的计数。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该思想基于这样的观察，即只有当子序列中存在的奇数元素的数量为奇数时，该子序列才会具有奇数位异或。这是因为奇数元素的最低有效位等于 **1** 。因此，最低有效位( **1^1^1….)的 XOR**)最多奇数次设置形成的新数字的最低有效位。因此，形成的新数字是奇数。
按照以下步骤解决问题:

1.  将数组 **A[]** 中出现的偶数和奇数元素的[计数分别存储在**偶数**和**奇数**中。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)
2.  [使用变量 **i** 遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【A】
    *   如果**A【I】**的值为奇数，则将**奇数**的值增加 **1。**
    *   否则，将**甚至**的值增加 **1** 。
3.  如果**奇数**的值等于 **0** ，则打印 **0** 并返回。
4.  否则，
    *   找出奇数个奇数元素的总组合。
    *   这个可以通过**(<sup>X</sup>C<sub>1</sub>+<sup>X</sup>C<sub>3</sub>+……+<sup>X</sup>C<sub>(X-(X+1)% 2)</sub>)*(<sup>M</sup>C<sub>0</sub>+<sup>M</sup>C<sub>1</sub>+……+<sup>M</sup>C 计算**
    *   因此，打印**2<sup>N-1</sup>T3】**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>

using namespace std;

// Function to count the subsequences
// having odd bitwise XOR value
void countSubsequences(vector<int> A)
{

    // Stores count of odd elements
    int odd = 0;

    // Stores count of even elements
    int even = 0;

    // Traverse the array A[]
    for(int el : A)
    {

        // If el is odd
        if (el % 2 == 1)
            odd++;
        else
            even++;
    }

    // If count of odd elements is 0
    if (odd == 0)
        cout << (0);
    else
        cout << (1 << (A.size() - 1));
}

// Driver Code
int main()
{

    // Given array A[]
    vector<int> A = { 1, 3, 4 };

    // Function call to count subsequences
    // having odd bitwise XOR value
    countSubsequences(A);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach

import java.io.*;

class GFG {

    // Function to count the subsequences
    // having odd bitwise XOR value
    public static void countSubsequences(int[] A)
    {

        // Stores count of odd elements
        int odd = 0;

        // Stores count of even elements
        int even = 0;

        // Traverse the array A[]
        for (int el : A) {

            // If el is odd
            if (el % 2 == 1)
                odd++;
            else
                even++;
        }

        // If count of odd elements is 0
        if (odd == 0)
            System.out.println(0);

        else
            System.out.println(1 << (A.length - 1));
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array A[]
        int[] A = { 1, 3, 4 };

        // Function call to count subsequences
        // having odd bitwise XOR value
        countSubsequences(A);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the subsequences
# having odd bitwise XOR value
def countSubsequences(A):

    # Stores count of odd elements
    odd = 0

    # Stores count of even elements
    even = 0

    # Traverse the array A[]
    for el in A:

        # If el is odd
        if (el % 2 == 1):
            odd += 1
        else:
            even += 1

    # If count of odd elements is 0
    if (odd == 0):
        print(0)
    else:
        print(1 << len(A) - 1)

# Driver Code
if __name__ == "__main__":

    # Given array A[]
    A = [1, 3, 4]

    # Function call to count subsequences
    # having odd bitwise XOR value
    countSubsequences(A)

# This code is contributed by ukasp
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

  // Function to count the subsequences
  // having odd bitwise XOR value
  public static void countSubsequences(int[] A)
  {

    // Stores count of odd elements
    int odd = 0;

    // Stores count of even elements
    int even = 0;

    // Traverse the array A[]
    foreach (int el in A) {

      // If el is odd
      if (el % 2 == 1)
        odd++;
      else
        even++;
    }

    // If count of odd elements is 0
    if (odd == 0)
      Console.WriteLine(0);

    else
      Console.WriteLine(1 << (A.Length - 1));
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Given array A[]
    int[] A = { 1, 3, 4 };

    // Function call to count subsequences
    // having odd bitwise XOR value
    countSubsequences(A);
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the subsequences
// having odd bitwise XOR value
function countSubsequences( A)
{

    // Stores count of odd elements
    var odd = 0;

    // Stores count of even elements
    var even = 0;

    // Traverse the array A[]
    for(var e1 = 0; e1<A.length; e1++)
    {
        // If el is odd
        if (A[e1] % 2 == 1)
            odd++;
        else
            even++;
    }

    // If count of odd elements is 0
    if (odd == 0)
        document.write(0);
    else
        document.write((1 << (A.length - 1)));
}

// Driver Code
// Given array A[]
var A = [ 1, 3, 4 ];

// Function call to count subsequences
// having odd bitwise XOR value
countSubsequences(A);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
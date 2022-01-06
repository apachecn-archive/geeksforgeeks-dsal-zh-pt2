# 对最右边的设置位为 K 的数字进行计数，直到 N 为止

> 原文:[https://www . geesforgeks . org/count-numbers-up-n-其最右边的设置位是-k/](https://www.geeksforgeeks.org/count-numbers-up-to-n-whose-rightmost-set-bit-is-k/)

给定两个正整数 **N** 和 **K** ，任务是对范围**【1，N】**中的数字进行计数，其 K <sup>第</sup>位从右边开始，即 [LSB](https://en.wikipedia.org/wiki/Bit_numbering#Least_significant_bit) ，是最右边的[设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。

**示例:**

> **输入:** N = 15，K = 2
> **输出:** 4
> **解释:**
> (2)<sub>10</sub>=(010)<sub>2</sub>，(6) <sub>10</sub> = (110) <sub>2</sub> ，(10)<sub>10</sub>=(1010)<sub>2【t29</sub>
> 
> **输入:**N = 10k = 3
> T3】输出: 3

**天真方法:**思路是迭代范围**【1，N】**，对于范围内的每个数字，检查最右边设置位的位置是否为 **K** ，并打印这些数字的计数。
***时间复杂度:** O(N LogN)*
***辅助空间:** O(1)*

**有效方法:**想法是在每一步找到位置 **i** 处最右边设置位位置的数字。按照以下步骤解决问题:

*   使用变量迭代范围**【1，K】**，比如 **i** 。
*   找出一个数字，其最右边的设定位是 **i** <sup>th</sup> 。
*   从 **N** 中减去那个数字。
*   对 **i** 的所有值重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the numbers in the
// range [1, N] whose rightmost set bit is K
int countNumberHavingKthBitSet(int N, int K)
{
    // Stores the number whose
    // rightmost set bit is K
    int numbers_rightmost_setbit_K;

    for (int i = 1; i <= K; i++) {

        // Numbers whose rightmost set bit is i
        int numbers_rightmost_bit_i = (N + 1) / 2;

        // Subtracting the number whose
        // rightmost set bit is i, from N
        N -= numbers_rightmost_bit_i;

        // Since i = k, then the number whose
        // rightmost set bit is K is stored
        if (i == K) {
            numbers_rightmost_setbit_K
                = numbers_rightmost_bit_i;
        }
    }

    cout << numbers_rightmost_setbit_K;
}

// Driver Code
int main()
{
    int N = 15;
    int K = 2;
    countNumberHavingKthBitSet(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
class GFG
{

// Function to count the numbers in the
// range [1, N] whose rightmost set bit is K
static void countNumberHavingKthBitSet(int N, int K)
{
    // Stores the number whose
    // rightmost set bit is K
    int numbers_rightmost_setbit_K = 0;
    for (int i = 1; i <= K; i++)
    {

        // Numbers whose rightmost set bit is i
        int numbers_rightmost_bit_i = (N + 1) / 2;

        // Subtracting the number whose
        // rightmost set bit is i, from N
        N -= numbers_rightmost_bit_i;

        // Since i = k, then the number whose
        // rightmost set bit is K is stored
        if (i == K)
        {
            numbers_rightmost_setbit_K
                = numbers_rightmost_bit_i;
        }
    }
    System.out.println(numbers_rightmost_setbit_K);
}

// Driver Code
static public void main(String args[])
{
    int N = 15;
    int K = 2;
    countNumberHavingKthBitSet(N, K);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the numbers in the
# range [1, N] whose rightmost set bit is K
def countNumberHavingKthBitSet(N, K):

    # Stores the number whose
    # rightmost set bit is K
    numbers_rightmost_setbit_K = 0

    for i in range(1, K + 1):

        # Numbers whose rightmost set bit is i
        numbers_rightmost_bit_i = (N + 1) // 2

        # Subtracting the number whose
        # rightmost set bit is i, from N
        N -= numbers_rightmost_bit_i

        # Since i = k, then the number whose
        # rightmost set bit is K is stored
        if (i == K):
            numbers_rightmost_setbit_K = numbers_rightmost_bit_i

    print (numbers_rightmost_setbit_K)

# Driver Code
if __name__ == '__main__':
    N = 15
    K = 2
    countNumberHavingKthBitSet(N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  // Function to count the numbers in the
  // range [1, N] whose rightmost set bit is K
  static void countNumberHavingKthBitSet(int N, int K)
  {
    // Stores the number whose
    // rightmost set bit is K
    int numbers_rightmost_setbit_K = 0;
    for (int i = 1; i <= K; i++)
    {

      // Numbers whose rightmost set bit is i
      int numbers_rightmost_bit_i = (N + 1) / 2;

      // Subtracting the number whose
      // rightmost set bit is i, from N
      N -= numbers_rightmost_bit_i;

      // Since i = k, then the number whose
      // rightmost set bit is K is stored
      if (i == K)
      {
        numbers_rightmost_setbit_K
          = numbers_rightmost_bit_i;
      }
    }
    Console.WriteLine(numbers_rightmost_setbit_K);
  }

  // Driver Code
  static public void Main(String []args)
  {
    int N = 15;
    int K = 2;
    countNumberHavingKthBitSet(N, K);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to count the numbers in the
// range [1, N] whose rightmost set bit is K
function countNumberHavingKthBitSet(N, K)
{
    // Stores the number whose
    // rightmost set bit is K
    let numbers_rightmost_setbit_K = 0;
    for (let i = 1; i <= K; i++)
    {

        // Numbers whose rightmost set bit is i
        let numbers_rightmost_bit_i = (N + 1) / 2;

        // Subtracting the number whose
        // rightmost set bit is i, from N
        N -= numbers_rightmost_bit_i;

        // Since i = k, then the number whose
        // rightmost set bit is K is stored
        if (i == K)
        {
            numbers_rightmost_setbit_K
                = numbers_rightmost_bit_i;
        }
    }
    document.write(numbers_rightmost_setbit_K);
}

// Driver Code

    let N = 15;
    let K = 2;
    countNumberHavingKthBitSet(N, K);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*
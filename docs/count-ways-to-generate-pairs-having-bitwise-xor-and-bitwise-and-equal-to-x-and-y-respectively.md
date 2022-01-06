# 计数产生分别等于 X 和 Y 的按位异或和按位与的方式

> 原文:[https://www . geesforgeks . org/count-way-to-generate-pairs-having-bitwise-xor-and-bitwise-and-equal-to-x-and-y-分别/](https://www.geeksforgeeks.org/count-ways-to-generate-pairs-having-bitwise-xor-and-bitwise-and-equal-to-x-and-y-respectively/)

给定两个整数 **X** 和 **Y** ，任务是找出生成一对整数 **A** 和 **B** 的途径总数，使得[按位异或](https://www.geeksforgeeks.org/tag/xor/)和[按位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)在 **A** 和 **B** 之间分别为 **X** 和 **Y**

**示例:**

> **输入:** X = 2，Y = 5
> **输出:** 2
> **解释:**
> 两个可能的对是(5，7)和(7，5)。
> **对 1:** (5，7)
> 按位 AND = 5 & 7 = 2
> 按位 XOR = 5 ^ 7 = 5
> **对 2:** (7，5)
> 按位 AND = 7 & 5 = 2
> 按位 XOR = 7 ^ 5 = 5
> 
> **输入:** X = 7，Y = 5
> T3】输出: 0

**天真法:**解决问题最简单的方法是在 **X** 和 **Y** 中选择最大值，并设置其所有位，然后检查从 **0** 到该最大值的所有可能的对，比如说 **M** 。如果任意一对 **A** 和 **B** ， **A & B** 和 **A⊕B** 分别等于 **X** 和 **Y** ，则增加**计数**。检查所有可能的配对后，打印**计数**的最终值。
***时间复杂度:**O(M<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**想法是在每个位置生成所有可能的位组合。 **X** 和 **Y** 中的**I<sup>th</sup>T5】位有以下 4 种可能:**

1.  如果 X <sub>i</sub> = 0，Y <sub>i</sub> = 1，那么 A <sub>i</sub> = 1，B <sub>i</sub> = 1。
2.  如果 X <sub>i</sub> = 1，Y <sub>i</sub> = 1，则不存在可能的位分配。
3.  如果 X <sub>i</sub> = 0，Y <sub>i</sub> = 0，那么 A <sub>i</sub> = 0，B <sub>i</sub> = 0。
4.  如果 X <sub>i</sub> = 1 且 Y <sub>i</sub> = 0，则 A <sub>i</sub> = 0 且 B <sub>i</sub> = 1 或 A <sub>i</sub> = 1 且 B <sub>i</sub> = 0，其中 **A <sub>i</sub>** 、 **B <sub>i</sub>** 、 **X <sub>i</sub> 、**

按照以下步骤解决问题:

1.  将计数器初始化为 **1** 。
2.  对于 **i <sup>第</sup>位**，如果 **X <sub>i</sub>** 和 **Y <sub>i</sub>** 等于 **1** ，则打印 **0** 。
3.  如果在 **i <sup>第</sup>位**，**X<sub>I</sub>T7】是 **1** ，而**Y<sub>I</sub>T13】是 **0** ，那么将计数器乘以 **2** ，因为有 2 个选项。****
4.  之后将 **X** 和 **Y** 每次除以 **2** 。
5.  对每一个 **i <sup>第</sup>位**重复以上步骤，直到两者都变为 **0** 并打印**计数器**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to return the count of
// possible pairs of A and B whose
// Bitwise XOR is X and Y respectively
int countOfPairs(int x, int y)
{
    // Stores the count of pairs
    int counter = 1;

    // Iterate till any bit are set
    while (x || y) {

        // Extract i-th bit
        // of X and Y
        int bit1 = x % 2;
        int bit2 = y % 2;

        // Divide X and Y by 2
        x >>= 1;
        y >>= 1;

        // If Xi = 1 and Yi = 2,
        // multiply counter by 2
        if (bit1 == 1 and bit2 == 0) {

            // Increase required count
            counter *= 2;
            continue;
        }

        // If Xi =1 and Yi = 1
        if (bit1 & bit2) {

            // No answer exists
            counter = 0;
            break;
        }
    }

    // Return the final count
    return counter;
}

// Driver Code
int main()
{
    // Given X and Y
    int X = 2, Y = 5;

    // Function Call
    cout << countOfPairs(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to return the count of
// possible pairs of A and B whose
// Bitwise XOR is X and Y respectively
static int countOfPairs(int x, int y)
{
  // Stores the count of pairs
  int counter = 1;

  // Iterate till any bit are set
  while (x > 0 || y > 0)
  {
    // Extract i-th bit
    // of X and Y
    int bit1 = x % 2;
    int bit2 = y % 2;

    // Divide X and Y by 2
    x >>= 1;
    y >>= 1;

    // If Xi = 1 and Yi = 2,
    // multiply counter by 2
    if (bit1 == 1 && bit2 == 0)
    {
      // Increase required count
      counter *= 2;
      continue;
    }

    // If Xi =1 and Yi = 1
    if ((bit1 & bit2) > 0)
    {
      // No answer exists
      counter = 0;
      break;
    }
  }

  // Return the final count
  return counter;
}

// Driver Code
public static void main(String[] args)
{
  // Given X and Y
  int X = 2, Y = 5;

  // Function Call
  System.out.print(countOfPairs(X, Y));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the count of
# possible pairs of A and B whose
# Bitwise XOR is X and Y respectively
def countOfPairs(x, y):

    # Stores the count of pairs
    counter = 1

    # Iterate till any bit are set
    while(x or y):

        # Extract i-th bit
        # of X and Y
        bit1 = x % 2
        bit2 = y % 2

        # Divide X and Y by 2
        x >>= 1
        y >>= 1

        # If Xi = 1 and Yi = 2,
        # multiply counter by 2
        if (bit1 == 1 and bit2 == 0):

            # Increase required count
            counter *= 2
            continue

        # If Xi =1 and Yi = 1
        if(bit1 & bit2):

            # No answer exists
            counter = 0
            break

    # Return the final count
    return counter

# Driver Code

# Given X and Y
X = 2
Y = 5

# Function call
print(countOfPairs(X, Y))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to return the count of
// possible pairs of A and B whose
// Bitwise XOR is X and Y respectively
static int countOfPairs(int x, int y)
{
  // Stores the count of pairs
  int counter = 1;

  // Iterate till any bit are set
  while (x > 0 || y > 0)
  {
    // Extract i-th bit
    // of X and Y
    int bit1 = x % 2;
    int bit2 = y % 2;

    // Divide X and Y by 2
    x >>= 1;
    y >>= 1;

    // If Xi = 1 and Yi = 2,
    // multiply counter by 2
    if (bit1 == 1 && bit2 == 0)
    {
      // Increase required count
      counter *= 2;
      continue;
    }

    // If Xi =1 and Yi = 1
    if ((bit1 & bit2) > 0)
    {
      // No answer exists
      counter = 0;
      break;
    }
  }

  // Return the readonly count
  return counter;
}

// Driver Code
public static void Main(String[] args)
{
  // Given X and Y
  int X = 2, Y = 5;

  // Function Call
  Console.Write(countOfPairs(X, Y));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to return the count of
// possible pairs of A and B whose
// Bitwise XOR is X and Y respectively
function countOfPairs(x, y)
{
  // Stores the count of pairs
  let counter = 1;

  // Iterate till any bit are set
  while (x > 0 || y > 0)
  {
    // Extract i-th bit
    // of X and Y
    let bit1 = x % 2;
    let bit2 = y % 2;

    // Divide X and Y by 2
    x >>= 1;
    y >>= 1;

    // If Xi = 1 and Yi = 2,
    // multiply counter by 2
    if (bit1 == 1 && bit2 == 0)
    {
      // Increase required count
      counter *= 2;
      continue;
    }

    // If Xi =1 and Yi = 1
    if ((bit1 & bit2) > 0)
    {
      // No answer exists
      counter = 0;
      break;
    }
  }

  // Return the final count
  return counter;
}

// Driver code

   // Given X and Y
  let X = 2, Y = 5;

  // Function Call
  document.write(countOfPairs(X, Y));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log M)*
***辅助空间:** O(1)*
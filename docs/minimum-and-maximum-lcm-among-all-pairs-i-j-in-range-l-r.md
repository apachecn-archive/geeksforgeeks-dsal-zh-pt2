# 范围[L，R]

内所有对(I，j)的最小和最大 LCM

> 原文:[https://www . geesforgeks . org/最小和最大 LCM-all-pair-I-j-in-range-l-r/](https://www.geeksforgeeks.org/minimum-and-maximum-lcm-among-all-pairs-i-j-in-range-l-r/)

给定两个正整数 **L** 和 **R** 代表一个范围。任务是在范围**【L，R】**内找到任意一对 **(i，j)** 的最小和最大可能 [LCM](https://www.geeksforgeeks.org/lcm-gq/) ，使得 **L ≤ i < j ≤ R** 。

**示例:**

> **输入:** L = 2，R = 6
> **输出:** 4 30
> **说明:**以下是最小和最大 LCM 在范围[2，6]内的对。
> 最小 LCM–>(2，4) = 4
> 最大 LCM–>(5，6) = 30
> 
> **输入:** L = 5，R = 93
> T3】输出: 10 8556

**方法:**这个问题可以用简单的数学来解决。按照以下步骤解决给定的问题。

对于最小 [LCM](https://www.geeksforgeeks.org/lcm-gq/) ，

*   一个数字肯定是范围**【L，R】**中的最小数字。
*   选择数字时，一个是另一个的因素。
*   唯一给出最小 LCM 的 L 数是 **2*L** 。
*   检查 **2*L < = R**
    *   如果是，最小 LCM 将是 **2*L**
    *   否则，最小 LCM 将为 **L*(L+1)** 。

对于最大 [LCM](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) ，

*   一个数字肯定是**【L，R】**范围内的最大数字，即 **R** 。
*   选择第二个数，使它与 R 同素，两者的乘积最大。
*   **R** 和 **R-1** 将永远共充如果 **R！=2** 。
*   因此， **R*(R-1)** 将给出最大 LCM。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum LCM in range [L, R]
int minLCM(int L, int R)
{

    // If 2*L is within the the range
    // then minimum LCM would be 2*L
    if (2 * L <= R)
        return 2 * L;

    // Otherwise L * (L+1) would give
    // the minimum LCM
    else
        return L * (L + 1);
}

// Function to find maximum LCM in range [L, R]
int maxLCM(int L, int R)
{

    // The only possible equation that will give
    // the maximum LCM is R * (R-1)
    return R * (R - 1);
}

// Driver Code
int main()
{
    int L = 2;
    int R = 6;

    cout << minLCM(L, R) << ' ';
    cout << maxLCM(L, R);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find minimum LCM in range [L, R]
    public static int minLCM(int L, int R) {

        // If 2*L is within the the range
        // then minimum LCM would be 2*L
        if (2 * L <= R)
            return 2 * L;

        // Otherwise L * (L+1) would give
        // the minimum LCM
        else
            return L * (L + 1);
    }

    // Function to find maximum LCM in range [L, R]
    public static int maxLCM(int L, int R) {

        // The only possible equation that will give
        // the maximum LCM is R * (R-1)
        return R * (R - 1);
    }

    // Driver Code
    public static void main(String args[]) {
        int L = 2;
        int R = 6;

        System.out.print(minLCM(L, R) + " ");
        System.out.print(maxLCM(L, R));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find minimum LCM in range [L, R]
def minLCM(L, R):

  # If 2*L is within the the range
  # then minimum LCM would be 2*L
  if (2 * L <= R):
    return 2 * L

  # Otherwise L * (L+1) would give
  # the minimum LCM
  else:
    return L * (L + 1)

# Function to find maximum LCM in range [L, R]
def maxLCM(L, R):

  # The only possible equation that will give
  # the maximum LCM is R * (R-1)
  return R * (R - 1);

# Driver Code
if __name__=="__main__":

  L = 2;
  R = 6;

  print(minLCM(L, R),end=' ')
  print(maxLCM(L, R))

#This code is contributed by Akash Jha
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find minimum LCM in range [L, R]
    public static int minLCM(int L, int R)
    {

        // If 2*L is within the the range
        // then minimum LCM would be 2*L
        if (2 * L <= R)
            return 2 * L;

        // Otherwise L * (L+1) would give
        // the minimum LCM
        else
            return L * (L + 1);
    }

    // Function to find maximum LCM in range [L, R]
    public static int maxLCM(int L, int R)
    {

        // The only possible equation that will give
        // the maximum LCM is R * (R-1)
        return R * (R - 1);
    }

    // Driver Code
    public static void Main()
    {
        int L = 2;
        int R = 6;

        Console.Write(minLCM(L, R) + " ");
        Console.Write(maxLCM(L, R));
    }
}
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find minimum LCM in range [L, R]
function minLCM(L, R) {

  // If 2*L is within the the range
  // then minimum LCM would be 2*L
  if (2 * L <= R)
    return 2 * L;

  // Otherwise L * (L+1) would give
  // the minimum LCM
  else
    return L * (L + 1);
}

// Function to find maximum LCM in range [L, R]
function maxLCM(L, R) {

  // The only possible equation that will give
  // the maximum LCM is R * (R-1)
  return R * (R - 1);
}

// Driver Code

let L = 2;
let R = 6;

document.write(minLCM(L, R) + ' ');
document.write(maxLCM(L, R));
</script>
```

**Output**

```
4 30
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
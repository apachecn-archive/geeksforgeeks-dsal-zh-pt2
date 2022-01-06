# 通过用按位“与”和按位“或”替换对，最大化数组元素的平方和

> 原文:[https://www . geeksforgeeks . org/最大化数组元素的平方和-可能通过用它们的按位和按位或替换对/](https://www.geeksforgeeks.org/maximize-sum-of-squares-of-array-elements-possible-by-replacing-pairs-with-their-bitwise-and-and-bitwise-or/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过执行以下操作，从给定数组中找到可能的数组元素平方和的最大值:

*   选择任意一对数组元素 **(arr[i]，arr[j])**
*   将**arr【I】**替换为**arr【I】**和**arr【j】**
*   将**arr【j】**替换为**arr【I】**或**arr【j】**。

**示例:**

> **输入:** arr[] = {1，3，5}
> **输出:** 51
> **解释:**
> 对于对(arr[1]，arr[2])，执行以下操作:
> 将 3 替换为 3 AND 5，等于 1。
> 用 2 或 5 代替 5，等于 7。
> 上述步骤后得到的修饰数组为{1，1，7}。
> 因此，平方的最大和可以通过 1 * 1 + 1 * 1 + 7 * 7 = 51 来计算。
> 
> **输入:** arr[] = {8，9，9，1}
> **输出:** 243

**方法:**想法是观察如果 x 和 y 是两个选定的元素，那么让 **z = x** 和 **y** ， **w = x** 或 **y** ，其中 **x + y = z + w** 。

*   如果 **x ≤ y** ，不失一般性，很明显， **z ≤ w** 。因此，将表达式改写为**x+y =(x–d)+(y+d)**

> 旧平方和= M = x <sup>2</sup> + y <sup>2</sup>
> 新平方和= N =(x–d)<sup>2</sup>+(y–d)<sup>2</sup>，d > 0
> 差值= N–M = 2d(y+d–x)，d > 0

*   如果 **d > 0** ，则差值为正。因此，我们成功地增加了平方和。上面的观察是由于一个较大数字的平方大于一个较小数字的平方之和。
*   将给定的整数转换为[二进制形式](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)后，我们观察到以下情况:

> x = 3 = 0 1 1
> y = 5 = 1 0 1
> z = 1 = 0 0 1
> w = 7 = 1 1 1

*   x + y = 2 + 2 = 4 中的总设置位，z + w = 1 + 3 = 4 中的总设置位。因此，在执行该操作之后，总的设置位被保留。现在的想法是找出 **z** 和 **w** 。

> **例如:** arr[] = {5，2，3，4，5，6，7}
> 
> 1 0 1 = 5
> 0 1 0 = 2
> 0 1 1 = 3
> 1 0 0 = 4
> 1 0 1 = 5
> 1 1 0 = 6
> 1 1 = 7
> —
> 5 4 4(设置位之和)
> 现在，将这些数字的平方相加。

*   因此，对每个位位置 1 到 20 进行迭代，将总位数存储在该索引中。
*   然后在构造一个数字时，每次从每个索引中取 1 位。
*   得到数字后，把数字的平方加到答案上。
*   完成上述步骤后，打印答案的值。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the maximum value
int ans = 0;

int binary[31];

// Function to find the maximum sum
// of squares for each element of the
// array after updates
void findMaximumSum(
    const vector<int>& arr, int n)
{
    // Update the binary bit count at
    // corresponding indices for
    // each element
    for (auto x : arr) {

        int idx = 0;

        // Iterate all set bits
        while (x) {

            // If current bit is set
            if (x & 1)
                binary[idx]++;
            x >>= 1;
            idx++;
        }
    }

    // Construct number according
    // to the above defined rule
    for (int i = 0; i < n; ++i) {

        int total = 0;

        // Traverse each binary bit
        for (int j = 0; j < 21; ++j) {

            // If current bit is set
            if (binary[j] > 0) {
                total += pow(2, j);
                binary[j]--;
            }
        }

        // Square the constructed number
        ans += total * total;
    }

    // Return the answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 8, 9, 9, 1 };

    int N = arr.size();

    // Function call
    findMaximumSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Stores the maximum value
static int ans = 0;

static int []binary = new int[31];

// Function to find the maximum sum
// of squares for each element of the
// array after updates
static void findMaximumSum(int []arr, int n)
{

    // Update the binary bit count at
    // corresponding indices for
    // each element
    for(int x : arr)
    {
        int idx = 0;

        // Iterate all set bits
        while (x > 0)
        {

            // If current bit is set
            if ((x & 1) > 0)
                binary[idx]++;

            x >>= 1;
            idx++;
        }
    }

    // Connumber according
    // to the above defined rule
    for(int i = 0; i < n; ++i)
    {
        int total = 0;

        // Traverse each binary bit
        for(int j = 0; j < 21; ++j)
        {

            // If current bit is set
            if (binary[j] > 0)
            {
                total += Math.pow(2, j);
                binary[j]--;
            }
        }

        // Square the constructed number
        ans += total * total;
    }

    // Return the answer
    System.out.print(ans + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
   int[] arr = { 8, 9, 9, 1 };

    int N = arr.length;

    // Function call
    findMaximumSum(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

binary = [0] * 31

# Function to find the maximum sum
# of squares for each element of the
# array after updates
def findMaximumSum(arr, n):

    # Stores the maximum value
    ans = 0

    # Update the binary bit count at
    # corresponding indices for
    # each element
    for x in arr:
        idx = 0

        # Iterate all set bits
        while (x):

            # If current bit is set
            if (x & 1):
                binary[idx] += 1

            x >>= 1
            idx += 1

    # Construct number according
    # to the above defined rule
    for i in range(n):
        total = 0

        # Traverse each binary bit
        for j in range(21):

            # If current bit is set
            if (binary[j] > 0):
                total += int(math.pow(2, j))
                binary[j] -= 1

        # Square the constructed number
        ans += total * total

    # Return the answer
    print(ans)

# Driver Code

# Given array arr[]
arr = [ 8, 9, 9, 1 ]

N = len(arr)

# Function call
findMaximumSum(arr, N)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Stores the maximum
// value
static int ans = 0;

static int []binary =
             new int[31];

// Function to find the maximum
// sum of squares for each element
// of the array after updates
static void findMaximumSum(int []arr,
                           int n)
{
  // Update the binary bit
  // count at corresponding
  // indices for each element
  for(int i = 0; i < arr.Length; i++)
  {
    int idx = 0;

    // Iterate all set bits
    while (arr[i] > 0)
    {
      // If current bit is set
      if ((arr[i] & 1) > 0)
        binary[idx]++;

      arr[i] >>= 1;
      idx++;
    }
  }

  // Connumber according
  // to the above defined rule
  for(int i = 0; i < n; ++i)
  {
    int total = 0;

    // Traverse each binary bit
    for(int j = 0; j < 21; ++j)
    {
      // If current bit is set
      if (binary[j] > 0)
      {
        total += (int)Math.Pow(2, j);
        binary[j]--;
      }
    }

    // Square the constructed
    // number
    ans += total * total;
  }

  // Return the answer
  Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int[] arr = {8, 9, 9, 1};

  int N = arr.Length;

  // Function call
  findMaximumSum(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Stores the maximum value
var ans = 0;

var binary = Array(31).fill(0);

// Function to find the maximum sum
// of squares for each element of the
// array after updates
function findMaximumSum(arr, n)
{
    // Update the binary bit count at
    // corresponding indices for
    // each element
    var i,j;
    for (i= 0;i<arr.length;i++) {
        var x = arr[i];
        var idx = 0;

        // Iterate all set bits
        while (x) {

            // If current bit is set
            if (x & 1)
                binary[idx]++;
            x >>= 1;
            idx++;
        }
    }

    // Construct number according
    // to the above defined rule
    for (i = 0; i < n; ++i) {

        var total = 0;

        // Traverse each binary bit
        for (j = 0; j < 21; ++j) {

            // If current bit is set
            if (binary[j] > 0) {
                total += Math.pow(2, j);
                binary[j]--;
            }
        }

        // Square the constructed number
        ans += total * total;
    }

    // Return the answer
    document.write(ans);
}

// Driver Code
    // Given array arr[]
    var arr = [8, 9, 9, 1];

    var N = arr.length;

    // Function call
    findMaximumSum(arr, N);

</script>
```

**Output**

```
243
```

***时间复杂度:** O(N log <sub>2</sub> A)，其中 A 是数组的最大元素。*
***辅助空间:** O(1)*
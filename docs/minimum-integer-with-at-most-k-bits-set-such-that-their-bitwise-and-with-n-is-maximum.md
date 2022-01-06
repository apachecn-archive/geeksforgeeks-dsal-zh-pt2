# 设置最多 K 位的最小整数，使得它们与 N 的按位“与”最大

> 原文:[https://www . geeksforgeeks . org/最小整数加最多 k 位集，这样它们的按位加 n 就是最大值/](https://www.geeksforgeeks.org/minimum-integer-with-at-most-k-bits-set-such-that-their-bitwise-and-with-n-is-maximum/)

给定一个可以用 32 位表示的整数 **N** ，任务是找到另一个整数 **X** ，在其二进制表示中最多设置 K 位，并且 **X** 和 **N** 的[按位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)最大。

**示例:**

> **输入:** N = 5，K = 1
> **输出:** X = 2
> **解释:**
> 5 的二进制表示为 101，X 的可能值使其最大化 AND 为 2
> 5->101
> 2->100
> AND sum->100(2)
> 4 是我们可以用 N 和 X 得到的最大 AND 和。
> 
> **输入:** N = 10，K = 2
> **输出:** X = 10
> **解释:**
> 10 的二进制表示为 1010，X = 10 个可能的整数到给定的最大和，N 为 atmost 2 位集。
> 10->1010
> 10->1010
> AND sum->1010(10)
> 10 是我们可以用 N 和 x 得到的最大 AND 和。

**天真方法:**天真的解决方案是运行一个从 1 到 N 的循环，对 N 进行按位 and，同时检查设置的位数是否小于或等于 k。在每次迭代期间，保持按位 AND 的最大值。
**时间复杂度:** *O(N)*

**高效方法:**这个问题可以通过在比特上使用 [**贪婪方法**](https://www.geeksforgeeks.org/greedy-algorithms/) **来高效解决。因为 N 最多可以有 32 位。因此，我们将从最高有效位开始遍历，并检查它是否在 N 中被设置(或 1)，如果它没有被设置，那么就没有必要设置这个位，因为 and 操作将使它在最终答案中为零，否则我们将在我们需要的答案中设置它。此外，我们将在每次迭代中维护设置位的计数，并检查它是否不超过 k。
**时间复杂度:** *O(32)***

下面是上述有效方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find
// the integer with
// maximum bitwise with N
int find_max(int n, int k)
{
  // Store answer in the bitset
  // Initialized with 0
  bitset<32> X(0);

  // To maintain the count
  // of set bits that should
  // exceed k
  int cnt = 0;

  // Start traversing from the
  // Most significantif that bit
  // is set in n then we will set
  // in our answer i.e in X
  for (int i = 31; i >= 0 &&
           cnt != k; i--)
  {
    // Checking if the ith bit
    // is set in n or not
    if (n & (1 << i))
    {
      X[i] = 1;
      cnt++;
    }
  }

  // Converting into integer
  return X.to_ulong();
}

// Driver Code
int main()
{
  int n = 10, k = 2;

  // Function Call
  cout << find_max(n, k) <<
          endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
import java.lang.*;
class GFG{

// Function to find
// the integer with
// maximum bitwise with N
static int find_max(int n,
                    int k)
{
  // Store answer in the
  // bitset Initialized
  // with 0
  int[] X = new int[32];

  // To maintain the count
  // of set bits that should
  // exceed k
  int cnt = 0;

  // Start traversing from the
  // Most significant if that bit
  // is set in n then we will set
  // in our answer i.e in X
  for (int i = 31; i >= 0 &&
           cnt != k; i--)
  {
    // Checking if the ith bit
    // is set in n or not
    if ((n & (1 << i)) != 0)
    {
      X[i] = 1;
      cnt++;
    }
  }

  String s = "";
  for(int i = 31; i >= 0; i--)
    s += X[i] == 0 ? '0' : '1';

  // Converting into integer
  return Integer.parseInt(s,2);
}

// Driver function
public static void main (String[] args)
{
  int n = 10, k = 2;

  // Function Call
  System.out.println(find_max(n, k));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the integer with
# maximum bitwise with N
def find_max(n, k):

    # Store answer in the
    # bitset Initialized
    # with 0
    X = [0] * 32

    # To maintain the count
    # of set bits that should
    # exceed k
    cnt = 0

    # Start traversing from the
    # Most significant if that bit
    # is set in n then we will set
    # in our answer i.e in X
    i = 31

    while (i >= 0 and cnt != k):

        # Checking if the ith bit
        # is set in n or not
        if ((n & (1 << i)) != 0):
            X[i] = 1
            cnt += 1

        i -= 1

    s = ""

    for i in range(31, -1, -1):
        if X[i] == 0:
            s += '0'
        else:
            s += '1'

    # Converting into integer
    return int(s, 2)

# Driver code
n, k = 10, 2

# Function Call
print(find_max(n, k))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the integer with
// maximum bitwise with N
static int find_max(int n, int k)
{

    // Store answer in the
    // bitset Initialized
    // with 0
    int[] X = new int[32];

    // To maintain the count
    // of set bits that should
    // exceed k
    int cnt = 0;

    // Start traversing from the
    // Most significant if that bit
    // is set in n then we will set
    // in our answer i.e in X
    for(int i = 31; i >= 0 && cnt != k; i--)
    {

        // Checking if the ith bit
        // is set in n or not
        if ((n & (1 << i)) != 0)
        {
            X[i] = 1;
            cnt++;
        }
    }

    String s = "";

    for(int i = 31; i >= 0; i--)
        s += X[i] == 0 ? '0' : '1';

    // Converting into integer
    return Convert.ToInt32(s, 2);
}

// Driver code
public static void Main(String[] args)
{
    int n = 10, k = 2;

    // Function Call
    Console.Write(find_max(n, k));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to find
// the integer with
// maximum bitwise with N
function find_max(n, k)
{

  // Store answer in the
  // bitset Initialized
  // with 0
  var X = Array.from({length: 32}, (_, i) => 0);

  // To maintain the count
  // of set bits that should
  // exceed k
  var cnt = 0;

  // Start traversing from the
  // Most significant if that bit
  // is set in n then we will set
  // in our answer i.e in X
  for (i = 31; i >= 0 &&
           cnt != k; i--)
  {

    // Checking if the ith bit
    // is set in n or not
    if ((n & (1 << i)) != 0)
    {
      X[i] = 1;
      cnt++;
    }
  }

  var s = "";
  for(i = 31; i >= 0; i--)
    s += X[i] == 0 ? '0' : '1';

  // Converting into integer
  return parseInt(s,2);
}

// Driver function
var n = 10, k = 2;

// Function Call
document.write(find_max(n, k));

// This code is contributed by Princi Singh
</script>
```

**Output**

```
10
```

**性能分析:**

*   **时间复杂度:** O(32)
*   **辅助空间:** O(1
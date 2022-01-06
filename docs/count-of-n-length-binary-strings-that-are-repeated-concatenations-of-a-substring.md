# 子串重复连接的 N 长度二进制字符串的计数

> 原文:[https://www . geeksforgeeks . org/n 长度的计数-重复的二进制字符串-子字符串的串联/](https://www.geeksforgeeks.org/count-of-n-length-binary-strings-that-are-repeated-concatenations-of-a-substring/)

给定一个正整数 **N** ，任务是找出长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)的数量，这些字符串只是该字符串的一个子字符串的重复连接。

**示例:**

> **输入:** N = 4
> **输出:** 4
> **解释:**
> 以下是可能的长度为 N(= 4)的二进制字符串:
> 
> 1.  **“0000”:**该字符串是子字符串“0”的重复串联。
> 2.  **“1111”:**该字符串是子字符串“1”的重复串联。
> 3.  **“0101”:**该字符串是子字符串“01”的重复串联。
> 4.  **“1010”:**该字符串是子字符串“10”的重复串联。
> 
> 因此，这种字符串的总数是 4。因此，打印 4。
> 
> **输入:**N = 10
> T3】输出: 34

**方法:**给定的问题可以基于这样的观察来解决，即每个可能的字符串都有一个重复的子字符串，该子字符串串联起来表示 **K** 次，那么给定的字符串[长度](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/) **N** 必须被 **K** 整除才能生成所有的结果字符串。

因此，[求 **N**](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 的所有可能除数，对于每个除数，比如说 **K** 求它所能形成的所有可能串的计数，这些串的串联就是结果串，这个计数可以通过 **2 <sup>K</sup>** 来计算。现在，其中重复的字符串数也必须减去，所以对除数 **K** 进行同样的运算，从 **2 <sup>K</sup>** 中减去，得到每个[递归调用](https://www.geeksforgeeks.org/recursion/)的总计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Store the recurring recursive states
map<int, int> dp;

// Function to find the number of
// strings of length N such that it
// is a concatenation it substrings
int countStrings(int N)
{

    // Single character cant be repeated
    if (N == 1)
        return 0;

    // Check if this state has been
    // already calculated
    if (dp.find(N) != dp.end())
        return dp[N];

    // Stores the resultant count for
    // the current recursive calls
    int ret = 0;

    // Iterate over all divisors
    for(int div = 1; div <= sqrt(N); div++)
    {
        if (N % div == 0)
        {

            // Non-Repeated = Total - Repeated
            ret += (1 << div) -  countStrings(div);

            int div2 = N/div;

            if (div2 != div and div != 1)

                // Non-Repeated = Total - Repeated
                ret += (1 << div2) -  countStrings(div2);
        }
    }

    // Store the result for the
    // further calculation
    dp[N] = ret;       

    // Return resultant count
    return ret;
}

// Driver code
int main()
{
    int N = 6;

    // Function Call
    cout << countStrings(N) << endl;
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Store the recurring recursive states
static HashMap<Integer,
               Integer> dp = new HashMap<Integer,
                                         Integer>();

// Function to find the number of
// strings of length N such that it
// is a concatenation it substrings
static int countStrings(int N)
{

    // Single character cant be repeated
    if (N == 1)
        return 0;

    // Check if this state has been
    // already calculated
    if (dp.containsKey(N))
        return dp.get(N);

    // Stores the resultant count for
    // the current recursive calls
    int ret = 0;

    // Iterate over all divisors
    for(int div = 1; div <= Math.sqrt(N); div++)
    {
        if (N % div == 0)
        {

            // Non-Repeated = Total - Repeated
            ret += (1 << div) -  countStrings(div);

            int div2 = N / div;

            if (div2 != div && div != 1)

                // Non-Repeated = Total - Repeated
                ret += (1 << div2) -  countStrings(div2);
        }
    }

    // Store the result for the
    // further calculation
    dp.put(N, ret);       

    // Return resultant count
    return ret;
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;

    // Function Call
    System.out.print(countStrings(N));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python program for the above approach

# Store the recurring recursive states
dp = {}

# Function to find the number of
# strings of length N such that it
# is a concatenation it substrings
def countStrings(N):

    # Single character cant be repeated
    if N == 1:
        return 0

    # Check if this state has been
    # already calculated
    if dp.get(N, -1) != -1:
        return dp[N]

    # Stores the resultant count for
    # the current recursive calls
    ret = 0

    # Iterate over all divisors
    for div in range(1, int(N**.5)+1): 
        if N % div == 0:

            # Non-Repeated = Total - Repeated
            ret += (1 << div) -  countStrings(div)

            div2 = N//div

            if div2 != div and div != 1:

                # Non-Repeated = Total - Repeated
                ret += (1 << div2) -  countStrings(div2)

    # Store the result for the
    # further calculation
    dp[N] = ret         

    # Return resultant count
    return ret

# Driver Code
N = 6

# Function Call
print(countStrings(N))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Store the recurring recursive states
static Dictionary<int, int> dp = new Dictionary<int, int>();

// Function to find the number of
// strings of length N such that it
// is a concatenation it substrings
static int countStrings(int N)
{

    // Single character cant be repeated
    if (N == 1)
        return 0;

    // Check if this state has been
    // already calculated
    if (dp.ContainsKey(N))
        return dp[N];

    // Stores the resultant count for
    // the current recursive calls
    int ret = 0;

    // Iterate over all divisors
    for(int div = 1; div <= Math.Sqrt(N); div++)
    {
        if (N % div == 0)
        {

            // Non-Repeated = Total - Repeated
            ret += (1 << div) -  countStrings(div);

            int div2 = N / div;

            if (div2 != div && div != 1)

                // Non-Repeated = Total - Repeated
                ret += (1 << div2) -  countStrings(div2);
        }
    }

    // Store the result for the
    // further calculation
    dp[N] = ret;     

    // Return resultant count
    return ret;
}

// Driver Code
public static void Main()
{
    int N = 6;

    // Function Call
    Console.Write(countStrings(N));
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Store the recurring recursive states
let dp = new Map();

// Function to find the number of
// strings of length N such that it
// is a concatenation it substrings
function countStrings(N) {
  // Single character cant be repeated
  if (N == 1) return 0;

  // Check if this state has been
  // already calculated
  if (dp.has(N)) return dp.get(N);

  // Stores the resultant count for
  // the current recursive calls
  let ret = 0;

  // Iterate over all divisors
  for (let div = 1; div <= Math.sqrt(N); div++) {
    if (N % div == 0) {
      // Non-Repeated = Total - Repeated
      ret += (1 << div) - countStrings(div);

      let div2 = N / div;

      if (div2 != div && div != 1)
        // Non-Repeated = Total - Repeated
        ret += (1 << div2) - countStrings(div2);
    }
  }

  // Store the result for the
  // further calculation
  dp[N] = ret;

  // Return resultant count
  return ret;
}

// Driver code

let N = 6;

// Function Call
document.write(countStrings(N) + "<br>");

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
10
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
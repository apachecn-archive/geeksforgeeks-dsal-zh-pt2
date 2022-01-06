# 在[L，R]

范围内只有一个未设置位的数字计数

> 原文:[https://www . geesforgeks . org/numbers-count-with-one-unset-bit-in-range-lr/](https://www.geeksforgeeks.org/count-of-numbers-having-only-one-unset-bit-in-a-range-lr/)

给定两个整数 **L** 和 **R** ，任务是计算在**【L，R】**范围内只有一个**未设置位**的数字。

**示例:**

> **输入:** L = 4，R = 9
> **输出:** 2
> **解释:**
> 范围内所有数字的二进制表示为
> 4 =(100)<sub>2</sub>
> 5 =(101)<sub>2</sub>
> 6 =(110)<sub>2</sub>
> 7 =(111) <sub>因此，要求计数为 2。</sub>
> 
> **输入:** L = 10，R = 13
> **输出:** 2
> **解释:**
> 范围内所有数字的二进制表示【10，13】
> 10 =(1010)<sub>2</sub>
> 11 =(1011)<sub>2</sub>
> 12 =(1100)<sub>2</sub>
> 13
> 因此，需要的计数是 2。

**天真方法:**最简单的方法是检查范围内的每个数字**【L，R】**是否正好有一个未设置的位。对于每个这样的数字，递增计数。遍历整个范围后，打印**计数**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count numbers in the range
// [l, r] having exactly one unset bit
int count_numbers(int L, int R)
{
    // Stores the required count
    int ans = 0;

    // Iterate over the range
    for (int n = L; n <= R; n++) {

        // Calculate number of bits
        int no_of_bits = log2(n) + 1;

        // Calculate number of set bits
        int no_of_set_bits
            = __builtin_popcount(n);

        // If count of unset bits is 1
        if (no_of_bits
                - no_of_set_bits
            == 1) {

            // Increment answer
            ans++;
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int L = 4, R = 9;

    // Function Call
    cout << count_numbers(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to count numbers in the range
// [l, r] having exactly one unset bit
static int count_numbers(int L,
                         int R)
{
    // Stores the required count
    int ans = 0;

    // Iterate over the range
    for (int n = L; n <= R; n++)
    {
        // Calculate number of bits
        int no_of_bits = (int) (Math.log(n) + 1);

        // Calculate number of set bits
        int no_of_set_bits = Integer.bitCount(n);

        // If count of unset bits is 1
        if (no_of_bits - no_of_set_bits == 1)
        {
            // Increment answer
            ans++;
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int L = 4, R = 9;

    // Function Call
    System.out.print(count_numbers(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2

# Function to count numbers in the range
# [l, r] having exactly one unset bit
def count_numbers(L, R):

    # Stores the required count
    ans = 0

    # Iterate over the range
    for n in range(L, R + 1):

        # Calculate number of bits
        no_of_bits = int(log2(n) + 1)

        # Calculate number of set bits
        no_of_set_bits = bin(n).count('1')

        # If count of unset bits is 1
        if (no_of_bits - no_of_set_bits == 1):

            # Increment answer
            ans += 1

    # Return the answer
    return ans

# Driver Code
if __name__ == '__main__':

    L = 4
    R = 9

    # Function call
    print(count_numbers(L, R))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count numbers in the range
// [l, r] having exactly one unset bit
static int count_numbers(int L,
                         int R)
{

    // Stores the required count
    int ans = 0;

    // Iterate over the range
    for(int n = L; n <= R; n++)
    {

        // Calculate number of bits
        int no_of_bits = (int)(Math.Log(n) + 1);

        // Calculate number of set bits
        int no_of_set_bits = bitCount(n);

        // If count of unset bits is 1
        if (no_of_bits - no_of_set_bits == 1)
        {

            // Increment answer
            ans++;
        }
    }

    // Return the answer
    return ans;
}

static int bitCount(long x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code
public static void Main(String[] args)
{
    int L = 4, R = 9;

    // Function call
    Console.Write(count_numbers(L, R));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to count numbers in the range
// [l, r] having exactly one unset bit
function count_numbers(L, R)
{
    // Stores the required count
    let ans = 0;

    // Iterate over the range
    for (let n = L; n <= R; n++)
    {
        // Calculate number of bits
        let no_of_bits = Math.floor(Math.log(n) + 1);

        // Calculate number of set bits
        let no_of_set_bits = bitCount(n);

        // If count of unset bits is 1
        if (no_of_bits - no_of_set_bits == 1)
        {
            // Increment answer
            ans++;
        }
    }

    // Return the answer
    return ans;
}

function bitCount(x)
{
    let setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code

    let L = 4, R = 9;

    // Function Call
    document.write(count_numbers(L, R));

// This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*Log R)*
***辅助空间:** O(1)*

**有效方法:**由于最大位数最多为**对数 R** ，且该数在其二进制表示中应恰好包含一个零，因此将**【0，对数 R】**中的一个位置固定为未设置位，并设置所有其他位，如果生成的位数在给定范围内，则增加**计数**。
按照以下步骤解决问题:

1.  在范围**【0，对数 R】**内，循环未设置位的所有可能位置，比如**零位**
2.  将所有位设置在**零位**之前。
3.  迭代范围 **j = zero_bit + 1** 到 **log R** 并将位设置在 **j** 位置，如果形成的数字在**【L，R】**范围内，则递增**计数**。
4.  在上述步骤后打印计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count numbers in the range
// [L, R] having exactly one unset bit
int count_numbers(int L, int R)
{
    // Stores the count elements
    // having one zero in binary
    int ans = 0;

    // Stores the maximum number of
    // bits needed to represent number
    int LogR = log2(R) + 1;

    // Loop over for zero bit position
    for (int zero_bit = 0;
         zero_bit < LogR; zero_bit++) {

        // Number having zero_bit as unset
        // and remaining bits set
        int cur = 0;

        // Sets all bits before zero_bit
        for (int j = 0; j < zero_bit; j++) {

            // Set the bit at position j
            cur |= (1LL << j);
        }

        for (int j = zero_bit + 1;
             j < LogR; j++) {

            // Set the bit position at j
            cur |= (1LL << j);

            // If cur is in the range [L, R],
            // then increment ans
            if (cur >= L && cur <= R) {
                ans++;
            }
        }
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    long long L = 4, R = 9;

    // Function Call
    cout << count_numbers(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to count numbers in the range
// [L, R] having exactly one unset bit
static int count_numbers(int L, int R)
{
  // Stores the count elements
  // having one zero in binary
  int ans = 0;

  // Stores the maximum number of
  // bits needed to represent number
  int LogR = (int) (Math.log(R) + 1);

  // Loop over for zero bit position
  for (int zero_bit = 0; zero_bit < LogR;
           zero_bit++)
  {
    // Number having zero_bit as unset
    // and remaining bits set
    int cur = 0;

    // Sets all bits before zero_bit
    for (int j = 0; j < zero_bit; j++)
    {
      // Set the bit at position j
      cur |= (1L << j);
    }

    for (int j = zero_bit + 1;
             j < LogR; j++)
    {
      // Set the bit position at j
      cur |= (1L << j);

      // If cur is in the range [L, R],
      // then increment ans
      if (cur >= L && cur <= R)
      {
        ans++;
      }
    }
  }

  // Return ans
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  int L = 4, R = 9;

  // Function Call
  System.out.print(count_numbers(L, R));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
import  math

# Function to count numbers in the range
# [L, R] having exactly one unset bit
def count_numbers(L, R):

    # Stores the count elements
    # having one zero in binary
    ans = 0;

    # Stores the maximum number of
    # bits needed to represent number
    LogR = (int)(math.log(R) + 1);

    # Loop over for zero bit position
    for zero_bit in range(LogR):

        # Number having zero_bit as unset
        # and remaining bits set
        cur = 0;

        # Sets all bits before zero_bit
        for j in range(zero_bit):

            # Set the bit at position j
            cur |= (1 << j);

        for j in range(zero_bit + 1, LogR):

            # Set the bit position at j
            cur |= (1 << j);

            # If cur is in the range [L, R],
            # then increment ans
            if (cur >= L and cur <= R):
                ans += 1;

    # Return ans
    return ans;

# Driver Code
if __name__ == '__main__':
    L = 4;
    R = 9;

    # Function Call
    print(count_numbers(L, R));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for
// the above approach
using System;

public class GFG{

// Function to count numbers in the range
// [L, R] having exactly one unset bit
static int count_numbers(int L, int R)
{
  // Stores the count elements
  // having one zero in binary
  int ans = 0;

  // Stores the maximum number of
  // bits needed to represent number
  int LogR = (int) (Math.Log(R) + 1);

  // Loop over for zero bit position
  for (int zero_bit = 0; zero_bit < LogR;
           zero_bit++)
  {
    // Number having zero_bit as unset
    // and remaining bits set
    int cur = 0;

    // Sets all bits before zero_bit
    for (int j = 0; j < zero_bit; j++)
    {
      // Set the bit at position j
      cur |= (1 << j);
    }

    for (int j = zero_bit + 1;
             j < LogR; j++)
    {
      // Set the bit position at j
      cur |= (1 << j);

      // If cur is in the range [L, R],
      // then increment ans
      if (cur >= L && cur <= R)
      {
        ans++;
      }
    }
  }

  // Return ans
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  int L = 4, R = 9;

  // Function Call
  Console.Write(count_numbers(L, R));
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript  program for
//the above approach

// Function to count numbers in the range
// [L, R] having exactly one unset bit
function count_numbers(L, R)
{
  // Stores the count elements
  // having one zero in binary
  let ans = 0;

  // Stores the maximum number of
  // bits needed to represent number
  let LogR =  (Math.log(R) + 1);

  // Loop over for zero bit position
  for (let zero_bit = 0; zero_bit < LogR;
           zero_bit++)
  {
    // Number having zero_bit as unset
    // and remaining bits set
    let cur = 0;

    // Sets all bits before zero_bit
    for (let j = 0; j < zero_bit; j++)
    {
      // Set the bit at position j
      cur |= (1 << j);
    }

    for (let j = zero_bit + 1;
             j < LogR; j++)
    {
      // Set the bit position at j
      cur |= (1 << j);

      // If cur is in the range [L, R],
      // then increment ans
      if (cur >= L && cur <= R)
      {
        ans++;
      }
    }
  }

  // Return ans
  return ans;
}

// Driver Code

    let L = 4, R = 9;

  // Function Call
  document.write(count_numbers(L, R));

 // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O((log R)<sup>2</sup>)*
***辅助空间:** O(1)*
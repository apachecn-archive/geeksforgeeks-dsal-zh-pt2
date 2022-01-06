# 计数到 N 的数字，其中至少包含一个重复的数字

> 原文:[https://www . geesforgeks . org/count-numbers-up-n-其中包含至少一个重复数字/](https://www.geeksforgeeks.org/count-numbers-up-to-n-which-contains-at-least-one-repeated-digit/)

给定一个整数 **N** ，任务是对小于或等于 **N** 的数字进行计数，使得每个数字至少包含一个重复的数字。

**示例:**

> **输入:** N = 20
> **输出:** 1
> **说明:**
> 包含至少一个重复数字且小于或等于 N(= 20)的数字为{11}。
> 因此，要求的输出为 1。
> 
> **输入:** N = 100
> **输出:** 10
> **说明:**
> 包含至少一个重复数字且小于或等于 N(= 100)的数字为{11，22，33，44，55，66，77，88，99，100}。
> 因此，要求输出为 10。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **X** ，将总位数存储在 **N** 中。
*   初始化一个变量，比如 **cntNumbers** ，以存储由唯一数字组成的小于或等于 **N** 的数字的总数。
*   计算包含唯一数字的 **X** 位数字的总数，并更新**位数字**。以下是计算所有唯一数字的 **X** 位数字总数的公式。

> 所有唯一数字的 X 位数字总数= {(9 *阶乘(9)) /阶乘(10–X)}

*   通过检查小于或等于 **N** 的数字的每个可能数字处的所有可能值，计算包含唯一数字的小于或等于 **N** 的数字的总计数，并更新**计数**。
*   最后，打印**(N–cntNumbers)**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

long factorial(int n)
{
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1); 
}

// Function to count arrangements to
// select K elements from N elements 
long NPR(int n, int k)
{
    return factorial(n) / factorial(n - k);
}

// Function to count numbers less than or equal 
// to N with at least one repeated digits
int cntNumLessThanEqualNRepeatedDigits(int N)
{

    // Stores the value of N
    int temp = N;

    // Stores count of
    // digits in N
    int X = 0;

    // Store all possible
    // digits of N
    vector<int> nums;

    // Calculate digits in N
    while(temp)
    {

        // Update X
        X += 1;

        // Insert digits of N
        // into nums
        nums.push_back(temp % 10);

        // Update temp
        temp /= 10;
    }
    reverse(nums.begin(), nums.end());

    // Count numbers of (X)-digit
    // with no repeated digits
    int cntNumbers = 0;

    // Calculate count of numbers of less than
    // (X)-digit and no repeated digits
    for(int i = 1; i < X; i++)
    {

        // Update cntnumbers
        cntNumbers += 9 * (factorial(9) /
                           factorial(10 - i));
    }

    // Stores unique digits of
    // (X)-digit numbers
    unordered_set<int> vis;

    // Calculate (X) digits
    // numbers with no repeated digits
    for(int i = 0; i < nums.size(); i++)
    {

        // Stores count of unique
        // value at i_th digit
        int k = 0;

        // Stores minimum possible value of
        // i_th digit of a number
        int Min = 0;

        // If current digit is the first
        // digit of a number
        if (i == 0)
        {

            // Update Min
            Min = 1;
        }
        else
        {

            // Update Min
            Min = 0;
        }

        // Stores maximum possible value of
        // i_th digit if a number   
        int Max = 0;

        // If current digit is the last
        // digit of a number
        if (i == X - 1)
        {

            // Update Max
            Max = nums[i];
        }
        else
        {

            // Update Max
            Max = nums[i] - 1;
        }

        // Iterate over all possible value
        // of current digit
        for(int j = Min; j <= Max; j++)
        {

            // If value of current digit
            // already occurred in vis
            if (vis.find(j) != vis.end())
            {
                continue;
            }

            // Update k
            k += 1;
        }

        // Update cntNumbers
        cntNumbers += k * (NPR(9 - i,
                      X - i - 1));

        // If current value of i-th digit
        // already occurred in vis             
        if (vis.find(nums[i]) != vis.end())
        {
            break;
        }

        // Insert val in vis
        vis.insert(nums[i]);
    }

    // Return total count of numbers less
    // than or equal to N with repetition
    return (N - cntNumbers);
}

// Driver Code
int main()
{
    int N = 100;

    cout << cntNumLessThanEqualNRepeatedDigits(N);

    return 0;
}

// This code is contributed by Manu Pathria
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

public static int factorial(int n)
{
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1); 
}

// Function to count arrangements to
// select K elements from N elements 
public static int NPR(int n, int k)
{
    return factorial(n) / factorial(n - k);
}

// Function to count numbers less than or equal 
// to N with at least one repeated digits
public static int cntNumLessThanEqualNRepeatedDigits(int N)
{

    // Stores the value of N
    int temp = N;

    // Stores count of
    // digits in N
    int X = 0;

    // Store all possible
    // digits of N
    List<Integer> nums = new ArrayList<>();

    // Calculate digits in N
    while (temp > 0)
    {

        // Update X
        X += 1;

        // Insert digits of N
        // into nums
        nums.add(temp % 10);

        // Update temp
        temp /= 10;
    }
    Collections.reverse(nums);

    // Count numbers of (X)-digit
    // with no repeated digits
    int cntNumbers = 0;

    // Calculate count of numbers of less than
    // (X)-digit and no repeated digits
    for(int i = 1; i < X; i++)
    {

        // Update cntnumbers
        cntNumbers += 9 * (factorial(9) /
                           factorial(10 - i));
    }

    // Stores unique digits of
    // (X)-digit numbers
    Set<Integer> vis=new HashSet<>();

    // Calculate (X) digits
    // numbers with no repeated digits
    for(int i = 0; i < nums.size(); i++)
    {

        // Stores count of unique
        // value at i_th digit
        int k = 0;

        // Stores minimum possible value of
        // i_th digit of a number
        int Min = 0;

        // If current digit is the first
        // digit of a number
        if (i == 0)
        {

            // Update Min
            Min = 1;
        }
        else
        {

            // Update Min
            Min = 0;
        }

        // Stores maximum possible value of
        // i_th digit if a number   
        int Max = 0;

        // If current digit is the last
        // digit of a number
        if (i == X - 1)
        {

            // Update Max
            Max = nums.get(i);
        }
        else
        {

            // Update Max
            Max = nums.get(i) - 1;
        }

        // Iterate over all possible value
        // of current digit
        for(int j = Min; j <= Max; j++)
        {

            // If value of current digit
            // already occurred in vis
            if (vis.contains(j))
            {
                continue;
            }

            // Update k
            k += 1;
        }

        // Update cntNumbers
        cntNumbers += k * (NPR(9 - i,
                      X - i - 1));

        // If current value of i-th digit
        // already occurred in vis             
        if (vis.contains(nums.get(i)))
        {
            break;
        }

        // Insert val in vis
        vis.add(nums.get(i));
    }

    // Return total count of numbers less
    // than or equal to N with repetition
    return (N - cntNumbers);
}

// Driver Code
public static void main(String[] args)
{
    int N = 100;

    System.out.print(
        cntNumLessThanEqualNRepeatedDigits(N));
}
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

import math

# Function to count arrangements to
# select K elements from N elements
def NPR(n, k):
        return (math.factorial(n) //
                math.factorial(n-k))

# Function to count numbers less than or equal
# to N with at least one repeated digits
def cntNumLessThanEqualNRepeatedDigits(N):

    # Stores the value of N
    temp = N

    # Stores count of
    # digits in N
    X = 0;

    # Store all possible
    # digits of N
    nums = []

    # Calculate digits in N
    while(temp):

        # Update X
        X += 1

        # Insert digits of N
        # into nums
        nums.append(temp % 10)

        # Update temp
        temp //= 10

    # Reverse nums
    nums.reverse()

    # Count numbers of (X)-digit
    # with no repeated digits
    cntNumbers = 0

    # Calculate count of numbers of less than
    # (X)-digit and no repeated digits
    for i in range(1, X):

        # Update cntnumbers
        cntNumbers += 9 * (math.factorial(9) //
                        math.factorial(10 - i))

    # Stores unique digits of
    # (X)-digit numbers
    vis = set()

    # Calculate (X) digits
    # numbers with no repeated digits
    for i, val in enumerate(nums):

        # Stores count of unique
        # value at i_th digit
        k = 0

        # Stores minimum possible value of
        # i_th digit of a number
        Min = 0;

        # If current digit is the first
        # digit of a number
        if i == 0:

            #Update Min
            Min = 1
        else:

            # Update Min
            Min = 0

        # Stores maximum possible value of
        # i_th digit if a number   
        Max = 0;

        # If current digit is the last
        # digit of a number
        if i == X - 1:

            # Update Max
            Max = val
        else:

            # Update Max
            Max = val - 1;

        # Iterate over all possible value
        # of current digit
        for j in range(Min, Max + 1):

            # If value of current digit
            # already occurred in vis
            if (j in vis):
                continue

            # Update k
            k += 1

        # Update cntNumbers
        cntNumbers += k * (NPR(9 - i,
                      X - i - 1))

        # If current value of i-th digit
        # already occurred in vis             
        if val in vis:
            break

        # Insert val in vis
        vis.add(val)

    # Return total count of numbers less
    # than or equal to N with repetition
    return (N - cntNumbers)

# Driver Code
if __name__ == '__main__':
    N = 100

    # Function call
    print(cntNumLessThanEqualNRepeatedDigits(N))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

    static int factorial(int n)
    {
        return (n == 1 || n == 0) ? 1 :
                n * factorial(n - 1); 
    }

    // Function to count arrangements to
    // select K elements from N elements 
    static int NPR(int n, int k)
    {
        return factorial(n) / factorial(n - k);
    }

    // Function to count numbers less than or equal 
    // to N with at least one repeated digits
    static int cntNumLessThanEqualNRepeatedDigits(int N)
    {

        // Stores the value of N
        int temp = N;

        // Stores count of
        // digits in N
        int X = 0;

        // Store all possible
        // digits of N
        List<int> nums = new List<int>();

        // Calculate digits in N
        while (temp > 0)
        {

            // Update X
            X += 1;

            // Insert digits of N
            // into nums
            nums.Add(temp % 10);

            // Update temp
            temp /= 10;
        }
        nums.Reverse();

        // Count numbers of (X)-digit
        // with no repeated digits
        int cntNumbers = 0;

        // Calculate count of numbers of less than
        // (X)-digit and no repeated digits
        for(int i = 1; i < X; i++)
        {

            // Update cntnumbers
            cntNumbers += 9 * (factorial(9) /
                               factorial(10 - i));
        }

        // Stores unique digits of
        // (X)-digit numbers
        HashSet<int> vis = new HashSet<int>();

        // Calculate (X) digits
        // numbers with no repeated digits
        for(int i = 0; i < nums.Count; i++)
        {

            // Stores count of unique
            // value at i_th digit
            int k = 0;

            // Stores minimum possible value of
            // i_th digit of a number
            int Min = 0;

            // If current digit is the first
            // digit of a number
            if (i == 0)
            {

                // Update Min
                Min = 1;
            }
            else
            {

                // Update Min
                Min = 0;
            }

            // Stores maximum possible value of
            // i_th digit if a number   
            int Max = 0;

            // If current digit is the last
            // digit of a number
            if (i == X - 1)
            {

                // Update Max
                Max = nums[i];
            }
            else
            {

                // Update Max
                Max = nums[i] - 1;
            }

            // Iterate over all possible value
            // of current digit
            for(int j = Min; j <= Max; j++)
            {

                // If value of current digit
                // already occurred in vis
                if (vis.Contains(j))
                {
                    continue;
                }

                // Update k
                k += 1;
            }

            // Update cntNumbers
            cntNumbers += k * (NPR(9 - i,
                          X - i - 1));

            // If current value of i-th digit
            // already occurred in vis             
            if (vis.Contains(nums[i]))
            {
                break;
            }

            // Insert val in vis
            vis.Add(nums[i]);
        }

        // Return total count of numbers less
        // than or equal to N with repetition
        return (N - cntNumbers);
    }

  static void Main()
  {
        int N = 100;

        Console.WriteLine(cntNumLessThanEqualNRepeatedDigits(N));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

function factorial(n)
{
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1); 
}

// Function to count arrangements to
// select K elements from N elements 
function NPR(n, k)
{
    return factorial(n) / factorial(n - k);
}

// Function to count numbers less than or equal 
// to N with at least one repeated digits
function cntNumLessThanEqualNRepeatedDigits(N)
{

    // Stores the value of N
    var temp = N;

    // Stores count of
    // digits in N
    var X = 0;

    // Store all possible
    // digits of N
    var nums = [];

    // Calculate digits in N
    while(temp)
    {

        // Update X
        X += 1;

        // Insert digits of N
        // into nums
        nums.push(temp % 10);

        // Update temp
        temp = parseInt(temp/10);
    }
    nums.reverse();

    // Count numbers of (X)-digit
    // with no repeated digits
    var cntNumbers = 0;

    // Calculate count of numbers of less than
    // (X)-digit and no repeated digits
    for(var i = 1; i < X; i++)
    {

        // Update cntnumbers
        cntNumbers += 9 * (factorial(9) /
                           factorial(10 - i));
    }

    // Stores unique digits of
    // (X)-digit numbers
    var vis = new Set();

    // Calculate (X) digits
    // numbers with no repeated digits
    for(var i = 0; i < nums.length; i++)
    {

        // Stores count of unique
        // value at i_th digit
        var k = 0;

        // Stores minimum possible value of
        // i_th digit of a number
        var Min = 0;

        // If current digit is the first
        // digit of a number
        if (i == 0)
        {

            // Update Min
            Min = 1;
        }
        else
        {

            // Update Min
            Min = 0;
        }

        // Stores maximum possible value of
        // i_th digit if a number   
        var Max = 0;

        // If current digit is the last
        // digit of a number
        if (i == X - 1)
        {

            // Update Max
            Max = nums[i];
        }
        else
        {

            // Update Max
            Max = nums[i] - 1;
        }

        // Iterate over all possible value
        // of current digit
        for(var j = Min; j <= Max; j++)
        {

            // If value of current digit
            // already occurred in vis
            if (vis.has(j))
            {
                continue;
            }

            // Update k
            k += 1;
        }

        // Update cntNumbers
        cntNumbers += k * (NPR(9 - i,
                      X - i - 1));

        // If current value of i-th digit
        // already occurred in vis             
        if (vis.has(nums[i]))
        {
            break;
        }

        // Insert val in vis
        vis.add(nums[i]);
    }

    // Return total count of numbers less
    // than or equal to N with repetition
    return (N - cntNumbers);
}

// Driver Code
var N = 100;
document.write( cntNumLessThanEqualNRepeatedDigits(N));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
10
```

**时间复杂度:**O((log<sub>10</sub>N)<sup>2</sup>)
**辅助空间:** O(1)
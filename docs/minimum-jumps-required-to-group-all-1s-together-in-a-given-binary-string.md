# 给定二进制字符串中所有 1 组合在一起所需的最小跳跃次数

> 原文:[https://www . geeksforgeeks . org/最小跳转-要求在给定的二进制字符串中将所有 1 组合在一起/](https://www.geeksforgeeks.org/minimum-jumps-required-to-group-all-1s-together-in-a-given-binary-string/)

给定一个二进制字符串 **S** ，任务是计算将所有 1 组合在一起所需的最小跳跃次数。

**示例:**

> **输入:** S = "000010011000100"
> **输出:** 5
> **说明:**
> 0000**1**00110000100->0000000111000100 需要 2 跳。
> 0000000111000**1**00->000000111100000 需要 3 跳。
> 因此，将所有 1 组合在一起至少需要 5 次跳跃。
> 
> **输入:** S = "100010001"
> **输出:** 6
> **说明:**
> **1**00010001->000**1**10001 需要 3 跳。
> 00011000**1**->00011**1**000 需要 3 跳。

**进场:**
我们可以观察到，为了尽量减少将所有 1 组合在一起所需的跳跃次数，需要将它们组合在当前位置的**中间值**附近。计算中间值和将 1 移动到中间值左侧*中**0**T8】最近位置所需的移动次数。对中间位置*的*右侧进行同样的操作。
以下是上述方法的实施:*

## C++

```
// C++ Program to find the minimum
// number of jumps required to
// group all ones together in
// the binary string
#include <bits/stdc++.h>
using namespace std;

// Function to get the
// minimum jump value
int getMinJumps(string s)
{
    // Store all indices
    // of ones
    vector<int> ones;

    int jumps = 0, median = 0, ind = 0;

    // Populating one's indices
    for (int i = 0; i < s.length(); i++) {
        if (s[i] == '1')
            ones.push_back(i);
    }

    if (ones.size() == 0)
        return jumps;

    // Calculate median
    median = ones[ones.size() / 2];
    ind = median;

    // Jumps required for 1's
    // to the left of median
    for (int i = ind; i >= 0; i--) {
        if (s[i] == '1') {
            jumps += ind - i;
            ind--;
        }
    }
    ind = median;

    // Jumps required for 1's
    // to the right of median
    for (int i = ind; i < s.length(); i++) {
        if (s[i] == '1') {
            jumps += i - ind;
            ind++;
        }
    }

    // Return the final answer
    return jumps;
}

// Driver Code
int main()
{
    string S = "00100000010011";
    cout << getMinJumps(S) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum
// number of jumps required to
// group all ones together in
// the binary string
import java.io.*;
import java.util.*;

class GFG{

// Function to get the
// minimum jump value
public static int getMinJumps(String s)
{

    // Store all indices
    // of ones
    Vector<Integer> ones = new Vector<Integer>();

    int jumps = 0, median = 0, ind = 0;

    // Populating one's indices
    for(int i = 0; i < s.length(); i++)
    {
       if (s.charAt(i) == '1')
           ones.add(i);
    }

    if (ones.size() == 0)
        return jumps;

    // Calculate median
    median = (int)ones.get(ones.size() / 2);
    ind = median;

    // Jumps required for 1's
    // to the left of median
    for(int i = ind; i >= 0; i--)
    {
       if (s.charAt(i) == '1')
       {
           jumps += ind - i;
           ind--;
       }
    }
    ind = median;

    // Jumps required for 1's
    // to the right of median
    for(int i = ind; i < s.length(); i++)
    {
       if (s.charAt(i) == '1')
       {
           jumps += i - ind;
           ind++;
       }
    }

    // Return the final answer
    return jumps;
}

// Driver code
public static void main(String[] args)
{
    String S = "00100000010011";

    System.out.println(getMinJumps(S));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# number of jumps required to group
# all ones together in the binary string

# Function to get the
# minimum jump value
def getMinJumps(s):

    # Store all indices
    # of ones
    ones = []

    jumps, median, ind = 0, 0, 0

    # Populating one's indices
    for i in range(len(s)):
        if(s[i] == '1'):
            ones.append(i)

    if(len(ones) == 0):
        return jumps

    # Calculate median
    median = ones[len(ones) // 2]
    ind = median

    # Jumps required for 1's
    # to the left of median
    for i in range(ind, -1, -1):
        if(s[i] == '1'):
            jumps += ind - i
            ind -= 1

    ind = median

    # Jumps required for 1's
    # to the right of median
    for i in range(ind, len(s)):
        if(s[i] == '1'):
            jumps += i - ind
            ind += 1

    # Return the final answer
    return jumps

# Driver Code
if __name__ == '__main__':

    s = "00100000010011"

    print(getMinJumps(s))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to find the minimum
// number of jumps required to
// group all ones together in
// the binary string
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to get the
// minimum jump value
public static int getMinJumps(string s)
{

    // Store all indices
    // of ones
    ArrayList ones = new ArrayList();

    int jumps = 0, median = 0, ind = 0;

    // Populating one's indices
    for(int i = 0; i < s.Length; i++)
    {
        if (s[i] == '1')
            ones.Add(i);
    }

    if (ones.Count== 0)
        return jumps;

    // Calculate median
    median = (int)ones[ones.Count / 2];
    ind = median;

    // Jumps required for 1's
    // to the left of median
    for(int i = ind; i >= 0; i--)
    {
        if (s[i] == '1')
        {
            jumps += ind - i;
            ind--;
        }
    }
    ind = median;

    // Jumps required for 1's
    // to the right of median
    for(int i = ind; i < s.Length; i++)
    {
        if (s[i] == '1')
        {
            jumps += i - ind;
            ind++;
        }
    }

    // Return the final answer
    return jumps;
}

// Driver code
public static void Main(string[] args)
{
    string S = "00100000010011";

    Console.Write(getMinJumps(S));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
    // Javascript Program to find the minimum
    // number of jumps required to
    // group all ones together in
    // the binary string

    // Function to get the
    // minimum jump value
    function getMinJumps(s)
    {

        // Store all indices
        // of ones
        let ones = [];

        let jumps = 0, median = 0, ind = 0;

        // Populating one's indices
        for(let i = 0; i < s.length; i++)
        {
           if (s[i] == '1')
               ones.push(i);
        }

        if (ones.length == 0)
            return jumps;

        // Calculate median
        median = ones[parseInt(ones.length / 2, 10)];
        ind = median;

        // Jumps required for 1's
        // to the left of median
        for(let i = ind; i >= 0; i--)
        {
           if (s[i] == '1')
           {
               jumps += ind - i;
               ind--;
           }
        }
        ind = median;

        // Jumps required for 1's
        // to the right of median
        for(let i = ind; i < s.length; i++)
        {
           if (s[i] == '1')
           {
               jumps += i - ind;
               ind++;
           }
        }

        // Return the final answer
        return jumps;
    }

    let S = "00100000010011";

    document.write(getMinJumps(S));

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*
# 最大平衡字符串分区

> 原文:[https://www . geesforgeks . org/max-balanced-string-partitions/](https://www.geeksforgeeks.org/maximum-balanced-string-partitions/)

给定一个大小为 **N** 的平衡字符串 **str** ，具有相等数量的 **L** 和 **R** ，任务是找到一个最大数量 **X** ，这样给定的字符串可以被分割成 **X** 个平衡子字符串。如果字符串中的**L**的数量等于**R**的数量，则称为平衡字符串。
**举例:**

> **输入:** str = "LRLLRRLRRL"
> **输出:** 4
> **说明:**{“LR”、“LLRR”、“LR”、“RL”}是可能的分区。
> **输入:**“LRRRRLLRLLRL”
> **输出:** 3
> **解释:**{“LR”、“RRRLLRLL”、“RL”}是可能的分区。

**方法:**解决这个问题的方法是循环遍历字符串，每当遇到 **L** 和 **R** 时，不断递增计数。当 **L** 和 **R** 各自的计数相等的任何瞬间，形成一个平衡的括号。因此，这种实例的计数给出了期望的最大可能分区。
以下是上述方法的实施:

## C++

```
// C++ program to find a maximum number X, such
// that a given string can be partitioned
// into X substrings that are each balanced
#include <bits/stdc++.h>
using namespace std;

// Function to find a maximum number X, such
// that a given string can be partitioned
// into X substrings that are each balanced
int BalancedPartition(string str, int n)
{

    // If the size of the string is 0,
    // then answer is zero
    if (n == 0)
        return 0;

    // variable that represents the
    // number of 'R's and 'L's
    int r = 0, l = 0;

    // To store maximum number of
    // possible partitions
    int ans = 0;

    for (int i = 0; i < n; i++) {

        // increment the variable r if the
        // character in the string is 'R'
        if (str[i] == 'R') {
            r++;
        }

        // increment the variable l if the
        // character in the string is 'L'
        else if (str[i] = 'L') {
            l++;
        }

        // if r and l are equal,
        // then increment ans
        if (r == l) {
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    string str = "LLRRRLLRRL";

    int n = str.size();

    // Function call
    cout << BalancedPartition(str, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a maximum number X, such
// that a given String can be partitioned
// into X subStrings that are each balanced
import java.util.*;

class GFG{

// Function to find a maximum number X, such
// that a given String can be partitioned
// into X subStrings that are each balanced
static int BalancedPartition(String str, int n)
{

    // If the size of the String is 0,
    // then answer is zero
    if (n == 0)
        return 0;

    // Variable that represents the
    // number of 'R's and 'L's
    int r = 0, l = 0;

    // To store maximum number of
    // possible partitions
    int ans = 0;
    for(int i = 0; i < n; i++)
    {

       // Increment the variable r if the
       // character in the String is 'R'
       if (str.charAt(i) == 'R')
       {
           r++;
       }

       // Increment the variable l if the
       // character in the String is 'L'
       else if (str.charAt(i) == 'L')
       {
           l++;
       }

       // If r and l are equal,
       // then increment ans
       if (r == l)
       {
           ans++;
       }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String str = "LLRRRLLRRL";
    int n = str.length();

    // Function call
    System.out.print(BalancedPartition(str, n) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find a maximum number X,
# such that a given string can be partitioned
# into X substrings that are each balanced

# Function to find a maximum number X, such
# that a given string can be partitioned
# into X substrings that are each balanced
def BalancedPartition(str1, n):

    # If the size of the string is 0,
    # then answer is zero
    if (n == 0):
        return 0

    # Variable that represents the
    # number of 'R's and 'L's
    r = 0
    l = 0

    # To store maximum number of
    # possible partitions
    ans = 0

    for i in range(n):

        # Increment the variable r if the
        # character in the string is 'R'
        if (str1[i] == 'R'):
            r += 1

        # Increment the variable l if the
        # character in the string is 'L'
        elif (str1[i] == 'L'):
            l += 1

        # If r and l are equal,
        # then increment ans
        if (r == l):
            ans += 1

    # Return the required answer
    return ans

# Driver code
if __name__ == '__main__':

    str1 = "LLRRRLLRRL"
    n = len(str1)

    # Function call
    print(BalancedPartition(str1, n))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to find a maximum number X, such
// that a given String can be partitioned
// into X subStrings that are each balanced
using System;
class GFG{

// Function to find a maximum number X, such
// that a given String can be partitioned
// into X subStrings that are each balanced
static int BalancedPartition(string str, int n)
{

    // If the size of the String is 0,
    // then answer is zero
    if (n == 0)
        return 0;

    // Variable that represents the
    // number of 'R's and 'L's
    int r = 0, l = 0;

    // To store maximum number of
    // possible partitions
    int ans = 0;
    for(int i = 0; i < n; i++)
    {

        // Increment the variable r if the
        // character in the String is 'R'
        if (str[i] == 'R')
        {
            r++;
        }

        // Increment the variable l if the
        // character in the String is 'L'
        else if (str[i] == 'L')
        {
            l++;
        }

        // If r and l are equal,
        // then increment ans
        if (r == l)
        {
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void Main()
{
    string str = "LLRRRLLRRL";
    int n = str.Length;

    // Function call
    Console.Write(BalancedPartition(str, n) + "\n");
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>
    // Javascript program to find a maximum number X, such
    // that a given String can be partitioned
    // into X subStrings that are each balanced

    // Function to find a maximum number X, such
    // that a given String can be partitioned
    // into X subStrings that are each balanced
    function BalancedPartition(str, n)
    {

        // If the size of the String is 0,
        // then answer is zero
        if (n == 0)
            return 0;

        // Variable that represents the
        // number of 'R's and 'L's
        let r = 0, l = 0;

        // To store maximum number of
        // possible partitions
        let ans = 0;
        for(let i = 0; i < n; i++)
        {

           // Increment the variable r if the
           // character in the String is 'R'
           if (str[i] == 'R')
           {
               r++;
           }

           // Increment the variable l if the
           // character in the String is 'L'
           else if (str[i] == 'L')
           {
               l++;
           }

           // If r and l are equal,
           // then increment ans
           if (r == l)
           {
               ans++;
           }
        }

        // Return the required answer
        return ans;
    }

    let str = "LLRRRLLRRL";
    let n = str.length;

    // Function call
    document.write(BalancedPartition(str, n) + "</br>");

    // This code is contributed by divyeshrabadiya07.

</script>
```

**Output:** 

```
4
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(1)*
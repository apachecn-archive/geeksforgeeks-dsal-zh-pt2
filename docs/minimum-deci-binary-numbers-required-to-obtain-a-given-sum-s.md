# 获得给定和 S 所需的最小二进制数

> 原文:[https://www . geesforgeks . org/minimum-deci-binary-numbers-需要获得给定的总和-s/](https://www.geeksforgeeks.org/minimum-deci-binary-numbers-required-to-obtain-a-given-sum-s/)

给定一个代表正十进制整数的数字字符串**S**，任务是找到获得总和 **S** 所需的正**十进制二进制**数的最小数量。

> **十进制数字:**十进制数字，仅由 **0** s 和 **1** s 作为其数字组成。

**示例:**

> **输入:** S = "31"
> **输出:** 3
> **说明:** S 可以表示为 3 个十进制二进制数{10，10，11}的最小值之和。
> 
> **输入:** S = "82734"
> **输出:** 8
> **说明:** S 可以表示为 8 个十进制二进制数{11111，11111，10111，10101，10100，10100，10100，10000}的和最小值。

**方法:**给定的问题可以基于以下观察来解决:

> 假设需要 **X** 十进制数来获得总和 **S** 。要使 **X** 十进制数在**第 I 个**位置的和等于一个数字 **S** 中的 **d** ，则在 **X** 个在**和**位置有 **1** 的数中，必须正好有 **d** 十进制数。
> 因此，获得一个和 **S** 所需的最小十进制数等于 **S** 任一位数的最大值。

因此，要解决这个问题，[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并找到其中存在的最大数字。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of minimum
// Deci-Binary numbers required to obtain S
int minimum_deci_binary_number(string s)
{
    // Stores the minimum count
    int m = INT_MIN;

    // Iterate over the string s
    for (int i = 0; i < s.size(); i++) {

        // Convert the char to its
        // equivalent integer
        int temp = s[i] - '0';

        // If current character is
        // the maximum so far
        if (temp > m) {

            // Update the maximum digit
            m = temp;
        }
    }

    // Print the required result
    return m;
}

// Driver Code
int main()
{

    string S = "31";
    cout << minimum_deci_binary_number(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the count of minimum
// Deci-Binary numbers required to obtain S
static int minimum_deci_binary_number(String s)
{

    // Stores the minimum count
    int m = Integer.MIN_VALUE;

    // Iterate over the string s
    for(int i = 0; i < s.length(); i++)
    {

        // Convert the char to its
        // equivalent integer
        int temp = s.charAt(i) - '0';

        // If current character is
        // the maximum so far
        if (temp > m)
        {

            // Update the maximum digit
            m = temp;
        }
    }

    // Print the required result
    return m;
}

// Driver Code
public static void main (String[] args)
{
    String S = "31";

    System.out.println(minimum_deci_binary_number(S));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find the count of minimum
# Deci-Binary numbers required to obtain S
def minimum_deci_binary_number(s):

    # Stores the minimum count
    m = -10**19

    # Iterate over the string s
    for i in range(len(s)):

        # Convert the char to its
        # equivalent integer
        temp = ord(s[i]) - ord('0')

        # If current character is
        # the maximum so far
        if (temp > m):

            # Update the maximum digit
            m = temp

    # Print required result
    return m

# Driver Code
if __name__ == '__main__':

    S = "31"
    print(minimum_deci_binary_number(S))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to find the count of minimum
    // Deci-Binary numbers required to obtain S
    static int minimum_deci_binary_number(string s)
    {

        // Stores the minimum count
        int m = int.MinValue;

        // Iterate over the string s
        for(int i = 0; i < s.Length; i++)
        {

            // Convert the char to its
            // equivalent integer
            int temp = s[i] - '0';

            // If current character is
            // the maximum so far
            if (temp > m)
            {

                // Update the maximum digit
                m = temp;
            }
        }

        // Print the required result
        return m;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        string S = "31";       
        Console.WriteLine(minimum_deci_binary_number(S));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the count of minimum
// Deci-Binary numbers required to obtain S
function minimum_deci_binary_number(s)
{

    // Stores the minimum count
    let m = Number.MIN_VALUE;

    // Iterate over the string s
    for(let i = 0; i < s.length; i++)
    {

        // Convert the char to its
        // equivalent integer
        let temp = s[i] - '0';

        // If current character is
        // the maximum so far
        if (temp > m)
        {

            // Update the maximum digit
            m = temp;
        }
    }

    // Print the required result
    return m;
}

// Driver code

    let S = "31";

    document.write(minimum_deci_binary_number(S));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
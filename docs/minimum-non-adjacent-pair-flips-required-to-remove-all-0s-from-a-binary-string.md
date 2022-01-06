# 从二进制字符串中移除所有 0 所需的最小非相邻对翻转次数

> 原文:[https://www . geesforgeks . org/minimum-非相邻对翻转-需要从二进制字符串中移除所有 0/](https://www.geeksforgeeks.org/minimum-non-adjacent-pair-flips-required-to-remove-all-0s-from-a-binary-string/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S，**的任务是从二进制字符串中找到移除所有 0 所需的翻转最多两个不相邻字符的最小操作数。

**示例:**

> **输入:** S = "110010"
> **输出:** 2
> **解释:**
> **第一步:**翻转指数 2 和 5。字符串被修改为“111011”
> **步骤 2:** 仅翻转索引 3。字符串被修改为“111111”。
> 因此，所需的最小操作数为 2。
> 
> **输入:**S = " 110 "
> T3】输出: 1

**简单方法:**最简单的方法是[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。对于发现为“0”的字符串中的所有字符，向右遍历以找到下一个不与当前字符相邻的“ **0** ”。翻转两个字符，并将答案增加 1。如果右侧没有“0”，翻转当前字符，并将答案增加 1。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**想法是存储需要翻转的先前字符的索引。下面是借助步骤的图示:

*   初始化两个变量，用 **-1** 保持先前在字符串中找到的 **0** s 的索引。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并检查最后找到的两个索引是否不相邻，然后将**计数器**增加 1。此外，更新最后两个先前找到的索引的位置。
*   最后，完成遍历后，如果最后找到的两个索引都不是 **-1** ，则将**计数器**增加 **2** 。否则，如果最后找到的指标之一不是 **-1** ，则将**计数器**增加 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find minimum flips
// required to remove all 0s from
// a given binary string
int minOperation(string s)
{
  // Length of given string
  int n = s.length();

  // Stores the indices of
  // previous 0s
  int temp1 = -1, temp2 = -1;

  // Stores the minimum operations
  int ans = 0;

  // Traverse string to find minimum
  // operations to obtain required string
  for (int i = 0; i < n; i++)
  {
    // Current character
    int curr = s[i];

    // If current character is '0'
    if (curr == '0')
    {
      // Update temp1 with current
      // index, if both temp
      // variables are empty
      if (temp1 == -1 && temp2 == -1)
      {
        temp1 = i;
      }

      // Update temp2 with current
      // index, if temp1 contains
      // prev index but temp2 is empty
      else if (temp1 != -1 && temp2 == -1 &&
               i - temp1 == 1)
      {
        temp2 = i;
      }

      // If temp1 is not empty
      else if (temp1 != -1)
      {
        // Reset temp1 to -1
        temp1 = -1;

        // Increase ans
        ans++;
      }

      // If temp2 is not empty but
      // temp1 is empty
      else if (temp1 == -1 && temp2 != -1 &&
               i - temp2 != 1)
      {
        // Reset temp2 to -1
        temp2 = -1;

        // Increase ans
        ans++;
      }
    }
  }

  // If both temp variables
  // are not empty
  if (temp1 != -1 && temp2 != -1)
  {
    ans += 2;
  }
  // Otherwise
  else if (temp1 != -1 || temp2 != -1)
  {
    ans += 1;
  }

  // Return the answer
  return ans;
}

// Driver Code
int main()
{
  string s = "110010";
  cout << (minOperation(s));
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.util.*;

class GFG {

    // Function to find minimum flips
    // required to remove all 0s from
    // a given binary string
    static int minOperation(String s)
    {
        // Length of given string
        int n = s.length();

        // Stores the indices of
        // previous 0s
        int temp1 = -1, temp2 = -1;

        // Stores the minimum operations
        int ans = 0;

        // Traverse string to find minimum
        // operations to obtain required string
        for (int i = 0; i < n; i++) {
            // Current character
            int curr = s.charAt(i);

            // If current character is '0'
            if (curr == '0') {
                // Update temp1 with current
                // index, if both temp
                // variables are empty
                if (temp1 == -1 && temp2 == -1) {
                    temp1 = i;
                }

                // Update temp2 with current
                // index, if temp1 contains
                // prev index but temp2 is empty
                else if (temp1 != -1 && temp2 == -1
                         && i - temp1 == 1) {
                    temp2 = i;
                }

                // If temp1 is not empty
                else if (temp1 != -1) {
                    // Reset temp1 to -1
                    temp1 = -1;

                    // Increase ans
                    ans++;
                }

                // If temp2 is not empty but
                // temp1 is empty
                else if (temp1 == -1 && temp2 != -1
                         && i - temp2 != 1) {
                    // Reset temp2 to -1
                    temp2 = -1;

                    // Increase ans
                    ans++;
                }
            }
        }

        // If both temp variables are not empty
        if (temp1 != -1 && temp2 != -1) {
            ans += 2;
        }
        // Otherwise
        else if (temp1 != -1 || temp2 != -1) {
            ans += 1;
        }

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        String s = "110010";
        System.out.println(minOperation(s));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find minimum flips
# required to remove all 0s from
# a given binary string
def minOperation(s):

    # Length of given string
    n = len(s)

    # Stores the indices of
    # previous 0s
    temp1 = -1
    temp2 = -1

    # Stores the minimum operations
    ans = 0

    # Traverse string to find minimum
    # operations to obtain required string
    for i in range(n):

        # Current character
        curr = s[i]

        # If current character is '0'
        if (curr == '0'):

            # Update temp1 with current
            # index, if both temp
            # variables are empty
            if (temp1 == -1 and temp2 == -1):
                temp1 = i

            # Update temp2 with current
            # index, if temp1 contains
            # prev index but temp2 is empty
            elif (temp1 != -1 and temp2 == -1 and
                               i - temp1 == 1):
                temp2 = i

            # If temp1 is not empty
            elif (temp1 != -1):

                # Reset temp1 to -1
                temp1 = -1

                # Increase ans
                ans += 1

            # If temp2 is not empty but
            # temp1 is empty
            elif (temp1 == -1 and temp2 != -1 and
                              i - temp2 != 1):

                # Reset temp2 to -1
                temp2 = -1

                # Increase ans
                ans += 1

    # If both temp variables are not empty
    if (temp1 != -1 and temp2 != -1):
        ans += 2

    # Otherwise
    elif (temp1 != -1 or temp2 != -1):
        ans += 1

    # Return the answer
    return ans

# Driver Code
if __name__ == '__main__':

    s = "110010"

    print(minOperation(s))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find minimum flips
// required to remove all 0s from
// a given binary string
static int minOperation(String s)
{
  // Length of given string
  int n = s.Length;

  // Stores the indices of
  // previous 0s
  int temp1 = -1, temp2 = -1;

  // Stores the minimum operations
  int ans = 0;

  // Traverse string to find minimum
  // operations to obtain required string
  for (int i = 0; i < n; i++)
  {
    // Current character
    int curr = s[i];

    // If current character is '0'
    if (curr == '0')
    {
      // Update temp1 with current
      // index, if both temp
      // variables are empty
      if (temp1 == -1 && temp2 == -1)
      {
        temp1 = i;
      }

      // Update temp2 with current
      // index, if temp1 contains
      // prev index but temp2 is empty
      else if (temp1 != -1 &&
               temp2 == -1 &&
               i - temp1 == 1)
      {
        temp2 = i;
      }

      // If temp1 is not empty
      else if (temp1 != -1)
      {
        // Reset temp1 to -1
        temp1 = -1;

        // Increase ans
        ans++;
      }

      // If temp2 is not empty but
      // temp1 is empty
      else if (temp1 == -1 &&
               temp2 != -1 &&
               i - temp2 != 1)
      {
        // Reset temp2 to -1
        temp2 = -1;

        // Increase ans
        ans++;
      }
    }
  }

  // If both temp variables
  // are not empty
  if (temp1 != -1 && temp2 != -1)
  {
    ans += 2;
  }

  // Otherwise
  else if (temp1 != -1 || temp2 != -1)
  {
    ans += 1;
  }

  // Return the answer
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  String s = "110010";
  Console.WriteLine(minOperation(s));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function to find minimum flips
// required to remove all 0s from
// a given binary string
function minOperation(s)
{
  // Length of given string
  var n = s.length;

  // Stores the indices of
  // previous 0s
  var temp1 = -1, temp2 = -1;

  // Stores the minimum operations
  var ans = 0;

  // Traverse string to find minimum
  // operations to obtain required string
  for (var i = 0; i < n; i++)
  {
    // Current character
    var curr = s[i];

    // If current character is '0'
    if (curr == '0')
    {
      // Update temp1 with current
      // index, if both temp
      // variables are empty
      if (temp1 == -1 && temp2 == -1)
      {
        temp1 = i;
      }

      // Update temp2 with current
      // index, if temp1 contains
      // prev index but temp2 is empty
      else if (temp1 != -1 && temp2 == -1 &&
               i - temp1 == 1)
      {
        temp2 = i;
      }

      // If temp1 is not empty
      else if (temp1 != -1)
      {
        // Reset temp1 to -1
        temp1 = -1;

        // Increase ans
        ans++;
      }

      // If temp2 is not empty but
      // temp1 is empty
      else if (temp1 == -1 && temp2 != -1 &&
               i - temp2 != 1)
      {
        // Reset temp2 to -1
        temp2 = -1;

        // Increase ans
        ans++;
      }
    }
  }

  // If both temp variables
  // are not empty
  if (temp1 != -1 && temp2 != -1)
  {
    ans += 2;
  }
  // Otherwise
  else if (temp1 != -1 || temp2 != -1)
  {
    ans += 1;
  }

  // Return the answer
  return ans;
}

// Driver Code
var s = "110010";
document.write(minOperation(s));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
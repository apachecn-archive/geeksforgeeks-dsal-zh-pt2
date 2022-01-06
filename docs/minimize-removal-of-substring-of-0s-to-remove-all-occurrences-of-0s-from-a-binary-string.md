# 最小化删除 0 的子串，以从循环二进制字符串中删除所有出现的 0

> 原文:[https://www . geesforgeks . org/minimum-移除 0 的子串-移除二进制字符串中所有出现的 0/](https://www.geeksforgeeks.org/minimize-removal-of-substring-of-0s-to-remove-all-occurrences-of-0s-from-a-binary-string/)

给定大小为 **N** 的圆形[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是计算需要移除的连续 **0** s 的最小数量，使得该字符串仅包含 **1** s。

> **圆形字符串**是第一个和最后一个字符被认为是彼此相邻的字符串。

**示例:**

> **输入:** S = "11010001"
> **输出:** 2
> **解释:**
> 去掉子串{S[2]}。现在，字符串修改为“1110001”。
> 删除连续 0 的子串{S[3]，…，S[5]}。现在，字符串修改为“1111”。
> 因此，所需的最小清除次数为 2。
> 
> **输入:**S = " 00110000 "
> T3】输出: 1

**方法:**解决给定问题的思路是[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并统计[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量，子串的数量与 **0** s 相同，比如 **C** 。现在，如果字符串的第一个和最后一个字符是**‘0’**，则打印**(C–1)**的值作为所需的最小删除次数。否则，打印 **C** 的值作为结果。

**注意:**如果给定的字符串包含所有 **0s** ，那么需要的最小删除次数是 **1** 。单独考虑这个案例。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of
// removal of consecutive 0s required to
// make binary string consists only of 1s
int minRemovals(string str, int N)
{
    // Stores the count of removals
    int ans = 0;

    bool X = false;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If the current character is '0'
        if (str[i] == '0') {

            ans++;

            // Traverse until consecutive
            // characters are only '0's
            while (str[i] == '0') {
                i++;
            }
        }

        else {
            X = true;
        }
    }

    // If the binary string only
    // contains 1s, then return 1
    if (!X)
        return 1;

    // If the first and the last
    // characters are 0
    if (str[0] == '0'
        and str[N - 1] == '0') {
        ans--;
    }

    // Return the resultant count
    return ans;
}

// Driver Code
int main()
{
    string S = "11010001";
    int N = S.size();
    cout << minRemovals(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count minimum number of
// removal of consecutive 0s required to
// make binary string consists only of 1s
static int minRemovals(String str, int N)
{

    // Stores the count of removals
    int ans = 0;

    boolean X = false;

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // If the current character is '0'
        if (str.charAt(i) == '0')
        {
            ans++;

            // Traverse until consecutive
            // characters are only '0's
            while (i < N && str.charAt(i) == '0')
            {
                i++;
            }
        }

        else
        {
            X = true;
        }
    }

    // If the binary string only
    // contains 1s, then return 1
    if (!X)
        return 1;

    // If the first and the last
    // characters are 0
    if (str.charAt(0) == '0' &&
        str.charAt(N - 1) == '0')
    {
        ans--;
    }

    // Return the resultant count
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String S = "11010001";
    int N = S.length();

    System.out.println(minRemovals(S, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count minimum number of
# removal of consecutive 0s required to
# make binary string consists only of 1s
def minRemovals(str, N):

    # Stores the count of removals
    ans = 0
    X = False

    # Traverse the string S
    i = 0

    while i < N:

        # If the current character is '0'
        if (str[i] == '0'):
            ans += 1

            # Traverse until consecutive
            # characters are only '0's
            while (str[i] == '0'):
                i += 1
        else:
            X = True

        i += 1

    # If the binary string only
    # contains 1s, then return 1
    if (not X):
        return 1

    # If the first and the last
    # characters are 0
    if (str[0] == '0' and str[N - 1] == '0'):
        ans -= 1

    # Return the resultant count
    return ans

# Driver Code
S = "11010001"
N = len(S)

print(minRemovals(S, N))

# This code is contributed by rohan07
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to count minimum number of
  // removal of consecutive 0s required to
  // make binary string consists only of 1s
  static int minRemovals(string str, int N)
  {

    // Stores the count of removals
    int ans = 0;

    bool X = false;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

      // If the current character is '0'
      if (str[i] == '0') {

        ans++;

        // Traverse until consecutive
        // characters are only '0's
        while (str[i] == '0') {
          i++;
        }
      }

      else {
        X = true;
      }
    }

    // If the binary string only
    // contains 1s, then return 1
    if (!X)
      return 1;

    // If the first and the last
    // characters are 0
    if (str[0] == '0' && str[N - 1] == '0') {
      ans--;
    }

    // Return the resultant count
    return ans;
  }

  // Driver Code
  public static void Main()
  {
    string S = "11010001";
    int N = S.Length;
    Console.Write(minRemovals(S, N));
  }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>
// js program for the above approach

// Function to count minimum number of
// removal of consecutive 0s required to
// make binary consists only of 1s
function minRemovals(str, N)
{

  // Stores the count of removals
  let ans = 0;

  let X = false;

  // Traverse the S
  for (i = 0; i < N; i++) {

    // If the current character is '0'
    if (str[i] == '0') {

      ans++;

      // Traverse until consecutive
      // characters are only '0's
      while (str[i] == '0') {
        i++;
      }
    }

    else {
      X = true;
    }
  }

  // If the binary only
  // contains 1s, then return 1
  if (!X)
    return 1;

  // If the first and the last
  // characters are 0
  if (str[0] == '0' && str[N - 1] == '0') {
    ans--;
  }

  // Return the resultant count
  return ans;
}

  // Driver Code

let S = "11010001";
let N = S.length;
document.write(minRemovals(S, N));

// This code is contributed by mohit kumar 29.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
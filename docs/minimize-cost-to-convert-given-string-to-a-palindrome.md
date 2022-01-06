# 最小化将给定字符串转换为回文的成本

> 原文:[https://www . geesforgeks . org/最小化给定字符串到回文的转换成本/](https://www.geeksforgeeks.org/minimize-cost-to-convert-given-string-to-a-palindrome/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个整数 **P** 表示指向该字符串的第 P <sup>个</sup>索引的指针，任务是通过执行以下操作找到将该字符串转换为[回文](https://www.geeksforgeeks.org/tag/palindrome/)的最小成本:

*   指针 **P** 可以从索引 **i** 移动到索引 **j** ，所需费用为**| I–j |**，其中 **0 ≤ i < N** 和 **0 ≤ j < N** 。
*   在第 P<sup>索引处改变角色的成本是 **1** 。</sup>

**示例:**

> **输入:** S = "saad "，P = 1
> **输出:** 2
> **说明:**
> 最初指针在索引 1 处。
> 步骤 1:将指针移动到索引 0。因此，成本= 1–0 = 1。
> 第二步:将字符 S 改为 d，因此，成本= 1 + 1 = 2，S =“daad”
> 因此，成本为 2。
> 
> **输入:** S = "bass "，P = 3
> T3】输出:3
> T6】说明:T8】最初指针在索引 3 处。
> 第一步:将索引 P = 3 处的字符改为 b，因此，cost = 1，S =“basb”。
> 第二步:将指针移动到索引 2。因此，成本= 1 + 1 = 2。
> 步骤 3:将索引 P = 2 处的字符更改为 a。因此，成本= 3，S =“baab”
> 因此，成本为 3。

**做法:**思路是当指针在前半部分时，找到字符串前半部分需要更改的第一个和最后一个字符，如果指针在后半部分，则反转字符串，并相应调整指针。按照以下步骤解决问题:

*   如果指针在后半部分，则反转字符串并将指针更改为**(N–1–P)**。
*   现在，找到字符串前半部分左侧和右侧需要改变的最远字符位置。让他们成为 **l** 和 **r** 。
*   求改变字符的总成本，即前半部分的字符总数，这样 **S[i]！= s[N–I–1]**其中 **0 < i < N/2** 。
*   改变字符的最小遍历距离为**分钟(2 *(P–l)+r–P，2 *(r–P)+P–l)**。
*   将答案打印为更改字符的成本和最小行驶距离的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost to
// convert the string into a palindrome
int findMinCost(string str, int pos)
{

    // Length of the string
    int n = str.length();

    // If iointer is in the second half
    if (pos >= n / 2) {

        // Reverse the string
        reverse(str.begin(), str.end());
        pos = n - pos - 1;
    }

    int left, right;

    // Pointing to initial position
    left = right = pos;

    // Find the farthest index needed to
    // change on left side
    for (int i = pos; i >= 0; --i) {
        if (str[i] != str[n - i - 1]) {
            left = i;
        }
    }

    // Find the farthest index needed to
    // change on right side
    for (int i = pos; i < n / 2; ++i) {
        if (str[i] != str[n - i - 1]) {
            right = i;
        }
    }

    int ans = 0;

    for (int i = left; i <= right; ++i) {

        // Changing the variable to make
        // string palindrome
        if (str[i] != str[n - i - 1])
            ans += 1;
    }

    // min distance to travel to make
    // string palindrome
    int dis = min((2 * (pos - left)
                   + (right - pos)),
                  (2 * (right - pos)
                   + (pos - left)));

    // Total cost
    ans = ans + dis;

    // Return the minimum cost
    return ans;
}

// Driver Code
int main()
{
    // Given string S
    string S = "bass";

    // Given pointer P
    int P = 3;

    // Function Call
    cout << findMinCost(S, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum cost to
// convert the string into a palindrome
static int findMinCost(String str, int pos)
{

    // Length of the string
    int n = str.length();
    StringBuilder input1 = new StringBuilder();
    input1.append(str);

    // If iointer is in the second half
    if (pos >= n / 2)
    {

        // Reverse the string
        input1 = input1.reverse();
        pos = n - pos - 1;
    }

    int left, right;

    // Pointing to initial position
    left = right = pos;

    // Find the farthest index needed to
    // change on left side
    for(int i = pos; i >= 0; --i)
    {
        if (input1.charAt(i) !=
            input1.charAt(n - i - 1))
        {
            left = i;
        }
    }

    // Find the farthest index needed to
    // change on right side
    for(int i = pos; i < n / 2; ++i)
    {
        if (input1.charAt(i) !=
            input1.charAt(n - i - 1))
        {
            right = i;
        }
    }

    int ans = 0;

    for(int i = left; i <= right; ++i)
    {

        // Changing the variable to make
        // string palindrome
        if (input1.charAt(i) !=
            input1.charAt(n - i - 1))
            ans += 1;
    }

    // min distance to travel to make
    // string palindrome
    int dis = Math.min((2 * (pos - left) +
                          (right - pos)),
                     (2 * (right - pos) +
                            (pos - left)));

    // Total cost
    ans = ans + dis;

    // Return the minimum cost
    return ans;
}

// Driver Code
public static void main(String args[])
{

    // Given string S
    String S = "bass";

    // Given pointer P
    int P = 3;

    // Function Call
    System.out.println(findMinCost(S, P));
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost to
# convert the into a palindrome
def findMinCost(strr, pos):

    # Length of the string
    n = len(strr)

    # If iointer is in the second half
    if (pos >= n / 2):

        # Reverse the string
        strr = strr[::-1]
        pos = n - pos - 1

    left, right = pos, pos

    # Pointing to initial position
    # left = right = pos

    # Find the farthest index needed
    # to change on left side
    for i in range(pos, -1, -1):
        if (strr[i] != strr[n - i - 1]):
            left = i

    # Find the farthest index needed
    # to change on right side
    for i in range(pos, n // 2):
        if (strr[i] != strr[n - i - 1]):
            right = i

    ans = 0

    for i in range(left, right + 1):

        # Changing the variable to make
        # palindrome
        if (strr[i] != strr[n - i - 1]):
            ans += 1

    # min distance to travel to make
    # palindrome
    dis = (min((2 * (pos - left) +
                  (right - pos)),
             (2 * (right - pos) +
                    (pos - left))))

    # Total cost
    ans = ans + dis

    # Return the minimum cost
    return ans

# Driver Code
if __name__ == '__main__':

    # Given S
    S = "bass"

    # Given pointer P
    P = 3

    # Function Call
    print(findMinCost(S, P))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the minimum
// cost to convert the string
// into a palindrome
static int findMinCost(string str,
                       int pos)
{   
  // Length of the string
  int n = str.Length;

  char[] charArray =
         str.ToCharArray();

  // If iointer is in the
  // second half
  if (pos >= n / 2)
  {
    // Reverse the string
    Array.Reverse(charArray);
    pos = n - pos - 1;
  }

  int left, right;

  // Pointing to initial position
  left = right = pos;

  // Find the farthest index
  // needed to change on
  // left side
  for(int i = pos; i >= 0; --i)
  {
    if (charArray[i] !=
        charArray[n - i - 1])
    {
      left = i;
    }
  }

  // Find the farthest index
  // needed to change on right
  // side
  for(int i = pos; i < n / 2; ++i)
  {
    if (charArray[i] !=
        charArray[n - i - 1])
    {
      right = i;
    }
  }

  int ans = 0;

  for(int i = left; i <= right; ++i)
  {
    // Changing the variable to make
    // string palindrome
    if (charArray[i]!=
        charArray[n - i - 1])
      ans += 1;
  }

  // min distance to travel to make
  // string palindrome
  int dis = Math.Min((2 * (pos - left) +
                     (right - pos)),
                     (2 * (right - pos) +
                     (pos - left)));

  // Total cost
  ans = ans + dis;

  // Return the minimum cost
  return ans;
}

// Driver Code
public static void Main()
{   
  // Given string S
  string S = "bass";

  // Given pointer P
  int P = 3;

  // Function Call
  Console.Write(findMinCost(S, P));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum cost to
// convert the string into a palindrome
function findMinCost(str, pos)
{

    // Length of the string
    var n = str.length;

    // If iointer is in the second half
    if (pos >= n / 2)
    {

        // Reverse the string
        str.split('').reverse().fill('');
        pos = n - pos - 1;
    }

    var left, right;

    // Pointing to initial position
    left = right = pos;

    // Find the farthest index needed to
    // change on left side
    for(var i = pos; i >= 0; --i)
    {
        if (str[i] != str[n - i - 1])
        {
            left = i;
        }
    }

    // Find the farthest index needed to
    // change on right side
    for(var i = pos; i < n / 2; ++i)
    {
        if (str[i] != str[n - i - 1])
        {
            right = i;
        }
    }

    var ans = 0;

    for(var i = left; i <= right; ++i)
    {

        // Changing the variable to make
        // string palindrome
        if (str[i] != str[n - i - 1])
            ans += 1;
    }

    // min distance to travel to make
    // string palindrome
    var dis = Math.min((2 * (pos - left) +
                          (right - pos)),
                     (2 * (right - pos) +
                            (pos - left)));

    // Total cost
    ans = ans + dis;

    // Return the minimum cost
    return ans;
}

// Driver Code

// Given string S
var S = "bass";

// Given pointer P
var P = 3;

// Function Call
document.write(findMinCost(S, P));

// This code is contributed by itsok

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
# 最小化重新排列子字符串以将字符串转换为平衡括号序列的成本

> 原文:[https://www . geeksforgeeks . org/最小化-重新排列-子字符串-转换-字符串-平衡-括号-序列/](https://www.geeksforgeeks.org/minimize-cost-to-rearrange-substrings-to-convert-a-string-to-a-balanced-bracket-sequence/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，该字符串仅由字符**“(**和**”**组成，任务是通过从给定字符串 **S** 中选择任意子字符串并将该子字符串的字符重新排序，将给定字符串转换为平衡的括号序列。考虑每个子串的长度是每个操作的成本，最小化所需的总成本。

> 如果每一个左括号**(**有一个对应的右括号**)**，那么这个字符串就叫做平衡。

**示例:**

> **输入:**str =)((()”
> **输出:** 2
> **解释:**
> 选择子串 S[0，1](**=”(“**”)重新排列为“()”。成本= 2。
> 现在字符串修改为 S =()()，平衡了。
> 
> **输入:**S =())”
> T3】输出: -1

**做法:**思路是先[检查字符串是否能平衡](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)即统计左右括号的个数，如果不相等，则打印 **-1** 。否则，请按照以下步骤找到总最低成本:

*   初始化一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。
*   将**求和**初始化为 **0** ，用值**求和**更新数组元素。
*   [从 **i = 0** 到**N–1**遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并执行以下步骤:
    *   如果当前角色是**(“**)，那么更新**arr【I】**为 **(sum + 1)** 。否则，将 **arr[i]** 更新为**(sum–1)**。
    *   将**和**的值更新为**arr【I】**。
*   完成上述步骤后，如果**arr[N–1]**的值为非零，则字符串无法平衡，打印**-1”**。
*   如果字符串可以平衡，则打印总和为 0 的不相交[子阵列的大小总和作为结果。](https://www.geeksforgeeks.org/print-all-subarrays-with-0-sum/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of
// operations to convert the string to
// a balanced bracket sequence
void countMinMoves(string str)
{
    int n = str.size();

    // Initialize the integer array
    int a[n] = { 0 };
    int j, ans = 0, i, sum = 0;

    // Traverse the string
    for (i = 0; i < n; i++) {

        // Decrement a[i]
        if (str[i] == ')') {
            a[i] += sum - 1;
        }

        // Increment a[i]
        else {
            a[i] += sum + 1;
        }

        // Update the sum as current
        // value of arr[i]
        sum = a[i];
    }

    // If answer exists
    if (sum == 0) {

        // Traverse from i
        i = 1;

        // Find all substrings with 0 sum
        while (i < n) {
            j = i - 1;

            while (i < n && a[i] != 0)
                i++;

            if (i < n && a[i - 1] < 0) {
                ans += i - j;
                if (j == 0)
                    ans++;
            }
            i++;
        }

        // Print the sum of sizes
        cout << ans << endl;
    }

    // No answer exists
    else
        cout << "-1\n";
}

// Driver Code
int main()
{
    string str = ")(()";
    countMinMoves(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

  // Function to count minimum number of
  // operations to convert the string to
  // a balanced bracket sequence
  static void countMinMoves(String str)
  {
    int n = str.length();

    // Initialize the integer array
    int a[] = new int[n];
    int j, ans = 0, i, sum = 0;

    // Traverse the string
    for (i = 0; i < n; i++)
    {

      // Decrement a[i]
      if (str.charAt(i) == ')')
      {
        a[i] += sum - 1;
      }

      // Increment a[i]
      else
      {
        a[i] += sum + 1;
      }

      // Update the sum as current
      // value of arr[i]
      sum = a[i];
    }

    // If answer exists
    if (sum == 0)
    {

      // Traverse from i
      i = 1;

      // Find all substrings with 0 sum
      while (i < n)
      {
        j = i - 1;

        while (i < n && a[i] != 0)
          i++;

        if (i < n && a[i - 1] < 0)
        {
          ans += i - j;
          if (j == 0)
            ans++;
        }
        i++;
      }

      // Print the sum of sizes
      System.out.println(ans);
    }

    // No answer exists
    else
      System.out.println("-1");
  }

  // Driver Code
  public static void main(String[] args)
  {
    String str = ")(()";
    countMinMoves(str);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count minimum number of
# operations to convert the string to
# a balanced bracket sequence
def countMinMoves(str):

    n = len(str)

    # Initialize the integer array
    a = [0 for i in range(n)]
    j, ans, sum = 0, 0, 0

    # Traverse the string
    for i in range(n):

        # Decrement a[i]
        if (str[i] == ')'):
            a[i] += sum - 1

        # Increment a[i]
        else:
            a[i] += sum + 1

        # Update the sum as current
        # value of arr[i]
        sum = a[i]

    # If answer exists
    if (sum == 0):

        # Traverse from i
        i = 1

        # Find all substrings with 0 sum
        while (i < n):
            j = i - 1

            while (i < n and a[i] != 0):
                i += 1

            if (i < n and a[i - 1] < 0):
                ans += i - j

                if (j == 0):
                    ans += 1

            i += 1

        # Print the sum of sizes
        print(ans)

    # No answer exists
    else:
        print("-1")

# Driver Code
if __name__ == '__main__':

    str = ")(()"

    countMinMoves(str)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count minimum number of
  // operations to convert the string to
  // a balanced bracket sequence
  static void countMinMoves(string str)
  {
    int n = str.Length;

    // Initialize the integer array
    int []a = new int[n];
    int j, ans = 0, i, sum = 0;

    // Traverse the string
    for (i = 0; i < n; i++)
    {

      // Decrement a[i]
      if (str[i] == ')')
      {
        a[i] += sum - 1;
      }

      // Increment a[i]
      else
      {
        a[i] += sum + 1;
      }

      // Update the sum as current
      // value of arr[i]
      sum = a[i];
    }

    // If answer exists
    if (sum == 0)
    {

      // Traverse from i
      i = 1;

      // Find all substrings with 0 sum
      while (i < n)
      {
        j = i - 1;

        while (i < n && a[i] != 0)
          i++;

        if (i < n && a[i - 1] < 0)
        {
          ans += i - j;
          if (j == 0)
            ans++;
        }
        i++;
      }

      // Print the sum of sizes
      Console.WriteLine(ans);
    }

    // No answer exists
    else
      Console.WriteLine("-1");
  }

  // Driver Code
  public static void Main()
  {
    string str = ")(()";
    countMinMoves(str);
  }
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count minimum number of
// operations to convert the string to
// a balanced bracket sequence
function countMinMoves(str)
{
    var n = str.length;

    // Initialize the integer array
    var a = Array(n).fill(0);
    var j, ans = 0, i, sum = 0;

    // Traverse the string
    for (i = 0; i < n; i++) {

        // Decrement a[i]
        if (str[i] == ')') {
            a[i] += sum - 1;
        }

        // Increment a[i]
        else {
            a[i] += sum + 1;
        }

        // Update the sum as current
        // value of arr[i]
        sum = a[i];
    }

    // If answer exists
    if (sum == 0) {

        // Traverse from i
        i = 1;

        // Find all substrings with 0 sum
        while (i < n) {
            j = i - 1;

            while (i < n && a[i] != 0)
                i++;

            if (i < n && a[i - 1] < 0) {
                ans += i - j;
                if (j == 0)
                    ans++;
            }
            i++;
        }

        // Print the sum of sizes
        document.write( ans + "<br>");
    }

    // No answer exists
    else
        document.write( "-1<br>");
}

// Driver Code
var str = ")(()";
countMinMoves(str);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
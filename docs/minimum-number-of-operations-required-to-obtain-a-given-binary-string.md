# 获得给定二进制字符串所需的最小运算次数

> 原文:[https://www . geeksforgeeks . org/获得给定二进制字符串所需的最小操作数/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-obtain-a-given-binary-string/)

给定长度为 **N** 的二进制字符串 **S** ，任务是通过最少的运算次数从长度为 **N** 的字符串(比如 **T** 中获取 **S** 。每个操作包括从字符串 **S** 中选择任意索引 **i** ，并翻转字符串 **T** 的索引**【I，N–1】**处的所有位。
**例:**

> **输入:** S = "101"
> **输出:** 3
> **解释:**
> “000”->“111”->“100”->“101”。
> 因此，所需的最小步骤数为 3。
> **输入:** S = "10111"
> **输出:** 3
> **解释:**
> “00000”->“11111”->“10000”->“10111”。
> 因此，所需的最小步骤数为 3。

**方法:**
思路是在给定的字符串 **S** 中找到第一个出现的 **1** ，并在该索引处执行给定的操作。在这一步之后，对于特定索引处 **S** 和 **T** 字符的每一个不匹配，重复该操作。
按照以下步骤操作:

1.  迭代 **S** 并标记 **1** 的第一次出现。
2.  初始化两个变量，比如说 ***最后一个*** 和 ***ans*** ，其中**最后一个**存储执行最后一个操作的字符( **0 或 1** )，而 **ans** 记录所需的最小步数。
3.  从第一次出现的 **1** 开始迭代，直到字符串结束。
4.  如果当前字符为**0****last = 1**，则递增*T5【ans】T6*的计数，并将 **last = 0** 。
5.  否则，如果**最后= 0** ，当前字符为 **1** ，则设置**最后= 1** 。
6.  返回**和**的最终值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of operations required
// to obtain the string s
int minOperations(string s)
{
    int n = s.size();
    int pos = -1;

    // Iterate the string s
    for (int i = 0; i < s.size(); i++) {

        // If first occurrence of 1
        // is found
        if (s[i] == '1') {

            // Mark the index
            pos = i;
            break;
        }
    }

    // Base case: If no 1 occurred
    if (pos == -1) {

        // No operations required
        return 0;
    }

    // Stores the character
    // for which last operation
    // was performed
    int last = 1;

    // Stores minimum number
    // of operations
    int ans = 1;

    // Iterate from pos to n
    for (int i = pos + 1; i < n; i++) {

        // Check if s[i] is 0
        if (s[i] == '0') {

            // Check if last operation was
            // performed because of 1
            if (last == 1) {
                ans++;

                // Set last to 0
                last = 0;
            }
        }
        else {

            if (last == 0) {

                // Check if last operation was
                // performed because of 0
                ans++;

                // Set last to 1
                last = 1;
            }
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    string s = "10111";

    cout << minOperations(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to find the minimum
// number of operations required
// to obtain the string s
static int minOperations(String s)
{
    int n = s.length();
    int pos = -1;

    // Iterate the string s
    for(int i = 0; i < s.length(); i++)
    {

        // If first occurrence of 1
        // is found
        if (s.charAt(i) == '1')
        {

            // Mark the index
            pos = i;
            break;
        }
    }

    // Base case: If no 1 occurred
    if (pos == -1)
    {

        // No operations required
        return 0;
    }

    // Stores the character
    // for which last operation
    // was performed
    int last = 1;

    // Stores minimum number
    // of operations
    int ans = 1;

    // Iterate from pos to n
    for(int i = pos + 1; i < n; i++)
    {

        // Check if s[i] is 0
        if (s.charAt(i) == '0')
        {

            // Check if last operation was
            // performed because of 1
            if (last == 1)
            {
                ans++;

                // Set last to 0
                last = 0;
            }
        }
        else
        {
            if (last == 0)
            {

                // Check if last operation was
                // performed because of 0
                ans++;

                // Set last to 1
                last = 1;
            }
        }
    }

    // Return the answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "10111";

    System.out.println(minOperations(s));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum
# number of operations required
# to obtain the string s
def minOperations(s):

    n = len(s)
    pos = -1

    # Iterate the string s
    for i in range(len(s)):

        # If first occurrence of 1
        # is found
        if (s[i] == '1'):

            # Mark the index
            pos = i
            break

    # Base case: If no 1 occurred
    if (pos == -1):

        # No operations required
        return 0

    # Stores the character
    # for which last operation
    # was performed
    last = 1

    # Stores minimum number
    # of operations
    ans = 1

    # Iterate from pos to n
    for i in range(pos + 1, n):

        # Check if s[i] is 0
        if (s[i] == '0'):

            # Check if last operation was
            # performed because of 1
            if (last == 1):
                ans += 1

                # Set last to 0
                last = 0

        else:

            if (last == 0):

                # Check if last operation was
                # performed because of 0
                ans += 1

                # Set last to 1
                last = 1

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    s = "10111"

    print(minOperations(s))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement the
// above approach
using System;
class GFG{

// Function to find the minimum
// number of operations required
// to obtain the string s
static int minOperations(String s)
{
    int n = s.Length;
    int pos = -1;

    // Iterate the string s
    for(int i = 0; i < s.Length; i++)
    {

        // If first occurrence of 1
        // is found
        if (s[i] == '1')
        {

            // Mark the index
            pos = i;
            break;
        }
    }

    // Base case: If no 1 occurred
    if (pos == -1)
    {

        // No operations required
        return 0;
    }

    // Stores the character
    // for which last operation
    // was performed
    int last = 1;

    // Stores minimum number
    // of operations
    int ans = 1;

    // Iterate from pos to n
    for(int i = pos + 1; i < n; i++)
    {

        // Check if s[i] is 0
        if (s[i] == '0')
        {

            // Check if last operation was
            // performed because of 1
            if (last == 1)
            {
                ans++;

                // Set last to 0
                last = 0;
            }
        }
        else
        {
            if (last == 0)
            {

                // Check if last operation was
                // performed because of 0
                ans++;

                // Set last to 1
                last = 1;
            }
        }
    }

    // Return the answer
    return ans;
}

// Driver code
public static void Main(string[] args)
{
    String s = "10111";

    Console.Write(minOperations(s));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>
    // Javascript Program to implement
    // the above approach

    // Function to find the minimum
    // number of operations required
    // to obtain the string s
    function minOperations(s)
    {
        let n = s.length;
        let pos = -1;

        // Iterate the string s
        for (let i = 0; i < s.length; i++) {

            // If first occurrence of 1
            // is found
            if (s[i] == '1') {

                // Mark the index
                pos = i;
                break;
            }
        }

        // Base case: If no 1 occurred
        if (pos == -1) {

            // No operations required
            return 0;
        }

        // Stores the character
        // for which last operation
        // was performed
        let last = 1;

        // Stores minimum number
        // of operations
        let ans = 1;

        // Iterate from pos to n
        for (let i = pos + 1; i < n; i++) {

            // Check if s[i] is 0
            if (s[i] == '0') {

                // Check if last operation was
                // performed because of 1
                if (last == 1) {
                    ans++;

                    // Set last to 0
                    last = 0;
                }
            }
            else {

                if (last == 0) {

                    // Check if last operation was
                    // performed because of 0
                    ans++;

                    // Set last to 1
                    last = 1;
                }
            }
        }

        // Return the answer
        return ans;
    }

    let s = "10111";
    document.write(minOperations(s));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
# 使一个字符串等于另一个字符串所需的相邻字符的最小翻转或交换次数

> 原文:[https://www . geeksforgeeks . org/最小翻转或交换相邻字符-需要使一个字符串等于另一个字符串/](https://www.geeksforgeeks.org/minimum-flips-or-swapping-of-adjacent-characters-required-to-make-a-string-equal-to-another/)

给定两个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **A** 和 **B** ，任务是通过翻转 **A** 的任意字符或交换 **A** 的相邻字符的最小次数，将字符串 **A** 转换为 **B** 。如果不可能使两个字符串相等，打印 **-1** 。

**示例:**

> **输入:**A =“10010010”，B =“00001000”
> **输出:** 3
> **解释:**
> 操作 1:翻转 A[0]将 A 修改为“00010010”。
> 操作 2:翻转 A[6]将 A 修改为“00010000”。
> 操作 3:交换 A[3]和 A[4]将 A 修改为“00001000”
> 因此，操作总数为 3。
> 
> **输入:**A =“11”，B =“00”
> T3】输出: 3

**方法:**思路是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **A** ，通过首先检查相邻字符的交换条件，使索引相同的字符相等。如果这个操作不能使字符相等，那么翻转字符。按照以下步骤解决问题:

*   初始化一个变量，比如 **ans，**来存储需要的结果。
*   [使用变量遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **A** ，说出 **i** ，并执行以下操作:
    *   如果 **A[i]** 等于 **B[i]，**则[继续循环](https://www.geeksforgeeks.org/continue-statement-cpp/)中的下一次迭代。
    *   否则，如果 **A[i]** 等于 **B[i + 1]** ， **A[i + 1]** 等于 **B[i]** ，则[交换字符](https://www.geeksforgeeks.org/swap-characters-in-a-string/)，并将 **i** 和 **ans** 增加 **1** 。
    *   否则，如果 **A[i]** 不等于 **B[i]** ，则翻转当前位并将 **ans** 增加 **1** 。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum operations
// required to convert string A to B
int minimumOperation(string a, string b)
{

    // Store the size of the string
    int n = a.length();
    int i = 0;

    // Store the required result
    int minoperation = 0;

    // Traverse the string, a
    while (i < n) {

        // If a[i] is equal to b[i]
        if (a[i] == b[i]) {
            i = i + 1;
            continue;
        }

        // Check if swapping adjacent
        // characters make the same-indexed
        // characters equal or not
        else if (a[i] == b[i + 1]
                 && a[i + 1] == b[i]
                 && i < n - 1) {

            minoperation++;
            i = i + 2;
        }

        // Otherwise, flip the current bit
        else if (a[i] != b[i]) {
            minoperation++;
            i = i + 1;
        }
        else {
            ++i;
        }
    }

    // Print the minimum number of operations
    cout << minoperation;
}

// Driver Code
int main()
{
    // Given Input
    string a = "10010010", b = "00001000";

    // Function Call
    minimumOperation(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

// Function to find minimum operations
// required to convert string A to B
static void minimumOperation(String a, String b)
{

    // Store the size of the string
    int n = a.length();
    int i = 0;

    // Store the required result
    int minoperation = 0;

    // Traverse the string, a
    while (i < n)
    {

        // If a[i] is equal to b[i]
        if (a.charAt(i) == b.charAt(i))
        {
            i = i + 1;
            continue;
        }

        // Check if swapping adjacent
        // characters make the same-indexed
        // characters equal or not
        else if (a.charAt(i) == b.charAt(i + 1) && 
                 a.charAt(i + 1) == b.charAt(i) &&
                   i < n - 1)
        {
            minoperation++;
            i = i + 2;
        }

        // Otherwise, flip the current bit
        else if (a.charAt(i) != b.charAt(i))
        {
            minoperation++;
            i = i + 1;
        }
        else
        {
            ++i;
        }
    }

    // Print the minimum number of operations
    System.out.println(minoperation);
}

// Driver Code
public static void main(String []args)
{

    // Given Input
    String a = "10010010", b = "00001000";

    // Function Call
    minimumOperation(a, b);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum operations
# required to convert A to B
def minimumOperation(a, b):

    # Store the size of the string
    n = len(a)
    i = 0

    # Store the required result
    minoperation = 0

    # Traverse the string, a
    while (i < n):

        # If a[i] is equal to b[i]
        if (a[i] == b[i]):
            i = i + 1
            continue

        # Check if swapping adjacent
        # characters make the same-indexed
        # characters equal or not
        elif (a[i] == b[i + 1] and
              a[i + 1] == b[i] and i < n - 1):
            minoperation += 1
            i = i + 2

        # Otherwise, flip the current bit
        elif (a[i] != b[i]):
            minoperation += 1
            i = i + 1
        else:
            i+=1

    # Print the minimum number of operations
    print (minoperation)

# Driver Code
if __name__ == '__main__':

    # Given Input
    a = "10010010"
    b = "00001000"

    # Function Call
    minimumOperation(a, b)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum operations
// required to convert string A to B
static void minimumOperation(string a, string b)
{

    // Store the size of the string
    int n = a.Length;
    int i = 0;

    // Store the required result
    int minoperation = 0;

    // Traverse the string, a
    while (i < n)
    {

        // If a[i] is equal to b[i]
        if (a[i] == b[i])
        {
            i = i + 1;
            continue;
        }

        // Check if swapping adjacent
        // characters make the same-indexed
        // characters equal or not
        else if (a[i] == b[i + 1] && 
                 a[i + 1] == b[i] &&
                   i < n - 1)
        {
            minoperation++;
            i = i + 2;
        }

        // Otherwise, flip the current bit
        else if (a[i] != b[i])
        {
            minoperation++;
            i = i + 1;
        }
        else
        {
            ++i;
        }
    }

    // Print the minimum number of operations
    Console.WriteLine(minoperation);
}

// Driver Code
public static void Main()
{

    // Given Input
    string a = "10010010", b = "00001000";

    // Function Call
    minimumOperation(a, b);
}
}

// This code is contributed by ankThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find minimum operations
// required to convert string A to B
function minimumOperation(a, b)
{

    // Store the size of the string
    var n = a.length;
    var i = 0;

    // Store the required result
    var minoperation = 0;

    // Traverse the string, a
    while (i < n) {

        // If a[i] is equal to b[i]
        if (a[i] == b[i]) {
            i = i + 1;
            continue;
        }

        // Check if swapping adjacent
        // characters make the same-indexed
        // characters equal or not
        else if (a[i] == b[i + 1]
                 && a[i + 1] == b[i]
                 && i < n - 1) {

            minoperation++;
            i = i + 2;
        }

        // Otherwise, flip the current bit
        else if (a[i] != b[i]) {
            minoperation++;
            i = i + 1;
        }
        else {
            ++i;
        }
    }

    // Print the minimum number of operations
    document.write(minoperation);
}

// Driver Code

    // Given Input
    var a = "10010010", b = "00001000";

    // Function Call
    minimumOperation(a, b);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
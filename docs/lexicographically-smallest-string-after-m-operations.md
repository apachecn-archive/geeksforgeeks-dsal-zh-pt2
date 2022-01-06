# M 次运算后字典上最小的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-m 后最小字符串-operations/](https://www.geeksforgeeks.org/lexicographically-smallest-string-after-m-operations/)

给定一个字符串 **S** 和整数 **M** 。任务是精确地执行 **M** 运算以获得字典序最小的字符串。

*   在每个操作中，从字符串中最佳地选择一个字符，并用紧接的下一个字符(aaa -> aab)更新它，这样字符串保持字典最小。
*   允许对字符串的单个字符进行多次操作。

***注:**把‘z’的下一个看成‘a’。*
**例:**

> **输入:** S = "aazzx "，M = 6
> **输出:**aaaaab
> **解释:**
> 我们尝试为每个操作形成字典序最小串。
> 对于 m = 1:更新“aazzx”为“aaazx”
> 对于 m = 2:更新“aaazx”为“aaaaax”
> 对于 m = 3:更新“aaaaax”为“aaaaay”
> 对于 m = 4:更新“aaay”为“aaaaaaaz”
> 对于 m = 5:更新“aaaz”为“aaaaaa”
> 对于 m = 6:更新“aaaaaa”为“aaaaab”，这是字典最小的比“aaaa”
> 6 次操作后的最终串:“aaaab”。
> **输入:**S =“z”，M = 27
> **输出:** a
> **解释:**
> 尝试为每个操作形成字典最小字符串，因为只有一个字符，所以所有 27 个操作都必须在其上执行。27 运算后的最终字符串为“a”。

**方法:**想法是实现一个简单的 [**贪婪方法**](https://www.geeksforgeeks.org/greedy-algorithms/) ，从字符串的开始处开始迭代字符串，同时迭代时关注字符串的当前元素，使其尽可能小。

*   假设当前元素为 *r* ，要使 *r* 最小，即 *a* ，需要 9 次运算，让我们称该值为*距离*。
*   现在，检查 M 是否大于等于*距离*，然后将当前字符更新为“a”，并将 M 的值减少*距离*。否则继续下一个迭代。
*   随着下一个 *z* 是 *a* ，形成 26 的循环。所以字符串的最后一个字符，可以用**最后一个字符+ (M % 26)** 来更新。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// lexicographical smallest string
// after performing M operations

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// lexicographical smallest string
// after performing M operations
void smallest_string(string s, int m)
{

    // Size of the given string
    int n = s.size();

    // Declare an array a
    int a[n];

    // For each i, a[i] contain number
    // of operations to update s[i] to 'a'
    for (int i = 0; i < n; i++) {
        int distance = s[i] - 'a';
        if (distance == 0)
            a[i] = 0;

        else
            a[i] = 26 - distance;
    }

    for (int i = 0; i < n; i++) {
        // Check if m >= ar[i],
        // then update s[i] to 'a'
        // decrement k by a[i]
        if (m >= a[i]) {
            s[i] = 'a';
            m = m - a[i];
        }
    }

    // Form a cycle of 26
    m = m % 26;

    // update last element of
    // string with the value
    // s[i] + (k % 26)
    s[n - 1] = s[n - 1] + m;

    // Return the answer
    cout << s;
}

// Driver code
int main()
{
    string str = "aazzx";
    int m = 6;
    smallest_string(str, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// lexicographical smallest String
// after performing M operations
class GFG{

// Function to find the
// lexicographical smallest String
// after performing M operations
static void smallest_String(char []s, int m)
{

    // Size of the given String
    int n = s.length;

    // Declare an array a
    int []a = new int[n];

    // For each i, a[i] contain number
    // of operations to update s[i] to 'a'
    for (int i = 0; i < n; i++)
    {
        int distance = s[i] - 'a';
        if (distance == 0)
            a[i] = 0;

        else
            a[i] = 26 - distance;
    }

    for (int i = 0; i < n; i++)
    {
        // Check if m >= ar[i],
        // then update s[i] to 'a'
        // decrement k by a[i]
        if (m >= a[i])
        {
            s[i] = 'a';
            m = m - a[i];
        }
    }

    // Form a cycle of 26
    m = m % 26;

    // update last element of
    // String with the value
    // s[i] + (k % 26)
    s[n - 1] = (char) (s[n - 1] + m);

    // Return the answer
    System.out.print(String.valueOf(s));
}

// Driver code
public static void main(String[] args)
{
    String str = "aazzx";
    int m = 6;
    smallest_String(str.toCharArray(), m);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find the
# lexicographical smallest string
# after performing M operations

# Function to find the
# lexicographical smallest string
# after performing M operations
def smallest_string(s, m):

    # Size of the given string
    n = len(s);

    l = list(s)

    # Declare an array a
    a = [0] * n;

    # For each i, a[i] contain number
    # of operations to update s[i] to 'a'
    for i in range(n):
        distance = ord(s[i]) - ord('a');

        if (distance == 0):
            a[i] = 0;
        else:
            a[i] = 26 - distance;

    for i in range(n):

        # Check if m >= ar[i],
        # then update s[i] to 'a'
        # decrement k by a[i]
        if (m >= a[i]):
            l[i] = 'a';
            m = m - a[i];

    # Form a cycle of 26
    m = m % 26;

    # update last element of
    # with the value
    # s[i] + (k % 26)

    # Return the answer
    for i in range(len(l) - 1):
        print(l[i], end = "")

    print(chr(ord(l[n - 1]) + m))

# Driver code
str = "aazzx";
m = 6;

smallest_string(str, m);

# This code is contributed by grand_master
```

## C#

```
// C# implementation to find the
// lexicographical smallest String
// after performing M operations
using System;

class GFG{

// Function to find the
// lexicographical smallest String
// after performing M operations
static void smallest_String(char []s, int m)
{

    // Size of the given String
    int n = s.Length;

    // Declare an array a
    int []a = new int[n];

    // For each i, a[i] contain number
    // of operations to update s[i] to 'a'
    for(int i = 0; i < n; i++)
    {
        int distance = s[i] - 'a';
        if (distance == 0)
            a[i] = 0;
        else
            a[i] = 26 - distance;
    }

    for(int i = 0; i < n; i++)
    {

        // Check if m >= ar[i],
        // then update s[i] to 'a'
        // decrement k by a[i]
        if (m >= a[i])
        {
            s[i] = 'a';
            m = m - a[i];
        }
    }

    // Form a cycle of 26
    m = m % 26;

    // Update last element of
    // String with the value
    // s[i] + (k % 26)
    s[n - 1] = (char)(s[n - 1] + m);

    // Return the answer
    Console.Write(String.Join("", s));
}

// Driver code
public static void Main(String[] args)
{
    String str = "aazzx";
    int m = 6;

    smallest_String(str.ToCharArray(), m);
}
}

// This code is contributed by Princi Singh
```

**Output:**

```
aaaab
```

***时间复杂度:** O(N)，其中 N 为给定字符串的长度*
***辅助空间:** O(N)，其中 N 为给定字符串的长度*
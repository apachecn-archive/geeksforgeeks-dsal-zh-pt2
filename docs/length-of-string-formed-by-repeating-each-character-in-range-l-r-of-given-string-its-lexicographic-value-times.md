# 给定字符串的范围[L，R]内的每个字符重复其字典值乘以

所形成的字符串长度

> 原文:[https://www . geesforgeks . org/通过重复给定字符串的范围内每个字符形成的字符串长度-其字典值-时间/](https://www.geeksforgeeks.org/length-of-string-formed-by-repeating-each-character-in-range-l-r-of-given-string-its-lexicographic-value-times/)

给定长度为 **N、**的字符串 **S** 和范围**【L，R】**(1<= L，R < = N)。任务是找到**长度**由**在**【L，R】**范围内重复**每个字符形成的字符串，到其**字典式**值的次数。

**示例:**

> **输入:** s = "cbbde "，l = 2，r = 5
> **输出:** 13
> **解释:**结果串是在范围【2，5】内重复每个字符后形成的如下所示:
> b 重复 2 次
> b 重复 2 次
> d 重复 4 次
> e 重复 5 次
> 
> 结果字符串:“bbbbbbdddeeee”
> 因此，如此形成的结果字符串长度为 13
> 
> **输入:** s = "xyyz "，l = 1，r = 2
> T3】输出: 49

**原生方式:**形成**临时**字符串，在**【L，R】**范围内追加**字符**重复**字典式**次，最后返回结果字符串的**长度**即可解决任务。
***时间复杂度*****:**O((R-L+1)* 26)
***辅助空间*****:**O((R-L+1)* 26)

**高效方法:**该任务可以借助于一个[前缀](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)数组来解决，该数组将存储相应的**字典顺序**值的总和。
按照以下步骤解决问题:

*   创建一个前缀数组“**前缀**，以存储当前字符的**字典顺序**值的**累计**总和
*   要得到给定[L，R]的答案:找到**前缀【R】**和**前缀【L-1】**的区别，如果 L > 0 和**前缀【L】**，如果 L = 0，得到窗口的答案( **R-L+1** )。
*   **注**:这种方法在多个查询的情况下工作效率高。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// recurring substring in range [l, r]
int recurringSubstring(string s, int l, int r)
{
    // Length of the string
    int N = s.size();

    // Variable to store the index of
    // the character in the alphabet
    int a[N];

    for (int i = 0; i < N; i++) {
        a[i] = (s[i] - 'a') + 1;
    }

    // Prefix array to store the sum
    int prefix[N];
    prefix[0] = a[0];

    for (int i = 1; i < N; i++) {
        prefix[i] = prefix[i - 1] + a[i];
    }

    l = l - 1;
    r = r - 1;

    // If l is greater than 0
    if (l != 0) {
        return prefix[r] - prefix[l - 1];
    }
    // If l is less or equal to 0
    else {
        return prefix[r];
    }
}

// Driver Code
int main()
{
    string s = "cbbde";
    int l = 2, r = 5;

    cout << recurringSubstring(s, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to find the length of
// recurring substring in range [l, r]
static int recurringSubstring(String s, int l, int r)
{

    // Length of the string
    int N = s.length();

    // Variable to store the index of
    // the character in the alphabet
    int []a = new int[N];

    for (int i = 0; i < N; i++) {
        a[i] = (s.charAt(i) - 'a') + 1;
    }

    // Prefix array to store the sum
    int []prefix = new int[N];
    prefix[0] = a[0];

    for (int i = 1; i < N; i++) {
        prefix[i] = prefix[i - 1] + a[i];
    }

    l = l - 1;
    r = r - 1;

    // If l is greater than 0
    if (l != 0) {
        return prefix[r] - prefix[l - 1];
    }
    // If l is less or equal to 0
    else {
        return prefix[r];
    }
}

// Driver Code
public static void main(String args[])
{
    String s = "cbbde";
    int l = 2, r = 5;

    System.out.println(recurringSubstring(s, l, r));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the length of
# recurring substring in range [l, r]
def recurringSubstring(s, l, r):

    # Length of the string
    N = len(s)

    # Variable to store the index of
    # the character in the alphabet
    a = [0] * N

    for i in range(N):
        a[i] = (ord(s[i]) - ord('a')) + 1

    # Prefix array to store the sum
    prefix = [0] * N
    prefix[0] = a[0]

    for i in range(1, N):
        prefix[i] = prefix[i - 1] + a[i]

    l = l - 1
    r = r - 1

    # If l is greater than 0
    if (l != 0):
        return prefix[r] - prefix[l - 1]

    # If l is less or equal to 0
    else:
        return prefix[r]

# Driver Code
s = "cbbde"
l = 2
r = 5

print(recurringSubstring(s, l, r))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find the length of
// recurring substring in range [l, r]
static int recurringSubstring(string s, int l, int r)
{

    // Length of the string
    int N = s.Length;

    // Variable to store the index of
    // the character in the alphabet
    int []a = new int[N];

    for (int i = 0; i < N; i++) {
        a[i] = (s[i] - 'a') + 1;
    }

    // Prefix array to store the sum
    int []prefix = new int[N];
    prefix[0] = a[0];

    for (int i = 1; i < N; i++) {
        prefix[i] = prefix[i - 1] + a[i];
    }

    l = l - 1;
    r = r - 1;

    // If l is greater than 0
    if (l != 0) {
        return prefix[r] - prefix[l - 1];
    }

    // If l is less or equal to 0
    else {
        return prefix[r];
    }
}

// Driver Code
public static void Main()
{
    string s = "cbbde";
    int l = 2, r = 5;

    Console.Write(recurringSubstring(s, l, r));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the length of
// recurring substring in range [l, r]
function recurringSubstring(s, l, r)
{

    // Length of the string
    let N = s.length;

    // Variable to store the index of
    // the character in the alphabet
    let a = [];

    for (let i = 0; i < N; i++) {
        a[i] = (s.charCodeAt(s[i]) - s.charCodeAt('a')) + 1;
    }

    // Prefix array to store the sum
    let prefix = [];
    prefix[0] = a[0];

    for (let i = 1; i < N; i++) {
        prefix[i] = prefix[i - 1] + a[i];
    }

    l = l - 1;
    r = r - 1;

    // If l is greater than 0
    if (l != 0) {
        return prefix[r] - prefix[l - 1];
    }

    // If l is less or equal to 0
    else {
        return prefix[r];
    }
}

// Driver Code
let s = "cbbde";
let l = 2, r = 5;

document.write(recurringSubstring(s, l, r));

// This code is contributed by Samim Hossain Mondal
</script>
```

**Output**

```
13
```

***时间复杂度*** **:** O(N)，其中 N 为弦的长度
***辅助空间*** **:** O(N)

**空间优化方法**:以上方法可以通过去掉前缀数组，简单的**在给定范围内迭代**，将**对应的**字典值加入到答案中，进一步**优化**。
按照以下步骤解决问题:

*   迭代范围[L，R]，将**对应的**字典值加到答案上。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// recurring substring in range [l, r]
int recurringSubstring(string s, int l, int r)
{
    // Length of the string
    int N = s.size();

    // Length of resultant string
    int ans = 0;
    for (int i = l - 1; i <= r - 1; i++) {

        // Add lexicographic value of s[i]
        ans += (s[i] - 'a' + 1);
    }
    return ans;
}

// Driver Code
int main()
{
    string s = "cbbde";
    int l = 2, r = 5;

    cout << recurringSubstring(s, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{
// Function to find the length of
// recurring substring in range [l, r]
static int recurringSubstring(String s, int l, int r)
{
    // Length of the string
    int N = s.length();

    // Length of resultant string
    int ans = 0;
    for (int i = l - 1; i <= r - 1; i++) {

        // Add lexicographic value of s[i]
        ans += (s.charAt(i) - 'a' + 1);
    }
    return ans;
}

// Driver Code
public static void main(String args[])
{
    String s = "cbbde";
    int l = 2, r = 5;

    System.out.println(recurringSubstring(s, l, r));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the length of
# recurring substring in range [l, r]
def recurringSubstring(s,  l, r):

    # Length of the string
    N = len(s)

    # Length of resultant string
    ans = 0
    for i in range(l-1, r):

        # Add lexicographic value of s[i]
        ans = ans + (ord(s[i]) - ord('a') + 1)

    return ans

# Driver Code
s = "cbbde"
l = 2
r = 5

print(recurringSubstring(s, l, r))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
// Function to find the length of
// recurring substring in range [l, r]
static int recurringSubstring(string s, int l, int r)
{
    // Length of the string
    int N = s.Length;

    // Length of resultant string
    int ans = 0;
    for (int i = l - 1; i <= r - 1; i++) {

        // Add lexicographic value of s[i]
        ans += (s[i] - 'a' + 1);
    }
    return ans;
}

// Driver Code
public static void Main()
{
    string s = "cbbde";
    int l = 2, r = 5;

    Console.Write(recurringSubstring(s, l, r));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the length of
// recurring substring in range [l, r]
function recurringSubstring(s, l, r)
{
    // Length of the string
    let N = s.length;

    // Length of resultant string
    let ans = 0;
    for (let i = l - 1; i <= r - 1; i++) {

        // Add lexicographic value of s[i]
        ans += (s.charCodeAt(s[i]) - s.charCodeAt('a') + 1);
    }
    return ans;
}

// Driver Code
let s = "cbbde";
let l = 2, r = 5;

document.write(recurringSubstring(s, l, r));

// This code is contributed by Samim Hossain Mondal
</script>
```

**Output**

```
13
```

***时间复杂度*** **:** O(N)，其中 N 为弦的长度
***辅助空间*** **:** O(1)
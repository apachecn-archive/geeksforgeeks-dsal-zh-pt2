# 最大化二进制字符串所需的最小操作次数

> 原文:[https://www . geesforgeks . org/最小操作数-最大化二进制字符串所需的操作数/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-maximize-the-binary-string/)

给定一个二进制字符串 **S** ，任务是找到使 **S** 所代表的值最大化所需执行的最小交换次数。

**示例:**

> **输入:** S = "1010001"
> **输出:** 1
> **解释:**交换 S[2]和 S[7]，将字符串修改为 1110000，从而最大化可以从字符串生成的数量。
> **输入:** S = "110001001"
> **输出:** 2
> **解释:**用 S[6]交换 S[3]，用 S[9]交换 S[4]，我们得到 111100000，这是需要的字符串

**天真方法:**
可以观察到，为了最大化所需的字符串，字符应该被交换，使得所有的 **0** 应该在右边，所有的 **1** 在左边。因此，需要将字符串修改为“ **1…10…0** 序列。

按照以下步骤解决问题:

1.  数数串 **S** 中 **1** 的个数，说 **cnt1** 。
2.  统计子串 **S[0]，…，S[cnt1-1]** 中 **0** s 的个数，说 **cnt0** 。
3.  打印 **cnt0** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number
// of operations required
int minOperation(string s, int n)
{

    // Count of 1's
    int cnt1 = 0;
    for (int i = 0; i < n; i++) {
        if (s[i] == '1')
            cnt1++;
    }

    // Count of 0's upto (cnt1)-th index
    int cnt0 = 0;
    for (int i = 0; i < cnt1; i++) {
        if (s[i] == '0')
            cnt0++;
    }

    // Return the answer
    return cnt0;
}

// Driver Code
int main()
{
    int n = 8;

    string s = "01001011";

    int ans = minOperation(s, n);

    cout << ans << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the number
// of operations required
static int minOperation(String s, int n)
{

    // Count of 1's
    int cnt1 = 0;
    for(int i = 0; i < n; i++)
    {
        if (s.charAt(i) == '1')
            cnt1++;
    }

    // Count of 0's upto (cnt1)-th index
    int cnt0 = 0;
    for(int i = 0; i < cnt1; i++)
    {
        if (s.charAt(i) == '0')
            cnt0++;
    }

    // Return the answer
    return cnt0;
}

// Driver Code
public static void main(String[] args)
{
    int n = 8;

    String s = "01001011";

    int ans = minOperation(s, n);

    System.out.print(ans + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the number
# of operations required
def minOperation(s, n):

    # Count of 1's
    cnt1 = 0;

    for i in range(n):
        if (ord(s[i]) == ord('1')):
            cnt1 += 1;

    # Count of 0's upto (cnt1)-th index
    cnt0 = 0;

    for i in range(0, cnt1):
        if (s[i] == '0'):
            cnt0 += 1;

    # Return the answer
    return cnt0;

# Driver Code
if __name__ == '__main__':

    n = 8;
    s = "01001011";
    ans = minOperation(s, n);

    print(ans);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the number
// of operations required
static int minOperation(String s, int n)
{

    // Count of 1's
    int cnt1 = 0;
    for(int i = 0; i < n; i++)
    {
        if (s[i] == '1')
            cnt1++;
    }

    // Count of 0's upto (cnt1)-th index
    int cnt0 = 0;
    for(int i = 0; i < cnt1; i++)
    {
        if (s[i] == '0')
            cnt0++;
    }

    // Return the answer
    return cnt0;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 8;

    String s = "01001011";

    int ans = minOperation(s, n);

    Console.Write(ans + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**

使用[双指针](https://www.geeksforgeeks.org/two-pointers-technique/)技术可以进一步优化上述方法。按照以下步骤解决问题:

*   设置两个指针 **i = 0** 和**j = s . length()–1**并迭代直到 **i** 超过 **j** 。
*   增加**计数**，如果 **S[i]** 等于“**0**”**S[j]**等于“ **1** ”。
*   如果 **S[i]** 为“ **1** ”，则增加 **i** ，直到出现一个“ **0** ”。同样，减少 **j** 直到**S【j】**等于“ **1** ”。
*   打印**计**为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number
// of operations required
int minOperation(string s, int n)
{

    int ans = 0;
    int i = 0, j = n - 1;
    while (i < j) {

        // Swap 0's and 1's
        if (s[i] == '0' && s[j] == '1') {
            ans++;
            i++;
            j--;
            continue;
        }

        if (s[i] == '1') {
            i++;
        }

        if (s[j] == '0') {
            j--;
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int n = 8;

    string s = "10100101";

    int ans = minOperation(s, n);

    cout << ans << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the number
// of operations required
static int minOperation(String s, int n)
{
    int ans = 0;
    int i = 0, j = n - 1;

    while (i < j)
    {

        // Swap 0's and 1's
        if (s.charAt(i) == '0' &&
            s.charAt(j) == '1')
        {
            ans++;
            i++;
            j--;
            continue;
        }

        if (s.charAt(i) == '1')
        {
            i++;
        }

        if (s.charAt(j) == '0')
        {
            j--;
        }
    }

    // Return the answer
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int n = 8;

    String s = "10100101";

    System.out.println(minOperation(s, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the number
# of operations required
def minOperation(s, n):
    ans = 0;
    i = 0; j = n - 1;

    while (i < j):

        # Swap 0's and 1's
        if (s[i] == '0' and s[j] == '1'):
            ans += 1;
            i += 1;
            j -= 1;
            continue;

        if (s[i] == '1'):
            i += 1;

        if (s[j] == '0'):
            j -= 1;

    # Return the answer
    return ans;

# Driver code
if __name__ == '__main__':
    n = 8;

    s = "10100101";

    print(minOperation(s, n));

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the number
// of operations required
static int minOperation(String s, int n)
{
    int ans = 0;
    int i = 0, j = n - 1;

    while (i < j)
    {

        // Swap 0's and 1's
        if (s[i] == '0' &&
            s[j] == '1')
        {
            ans++;
            i++;
            j--;
            continue;
        }

        if (s[i] == '1')
        {
            i++;
        }

        if (s[j] == '0')
        {
            j--;
        }
    }

    // Return the answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 8;

    String s = "10100101";

    Console.WriteLine(minOperation(s, n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the number
// of operations required
function minOperation(s, n)
{
    let ans = 0;
    let i = 0, j = n - 1;

    while (i < j)
    {

        // Swap 0's and 1's
        if (s[i] == '0' &&
            s[j] == '1')
        {
            ans++;
            i++;
            j--;
            continue;
        }

        if (s[i]== '1')
        {
            i++;
        }

        if (s[j] == '0')
        {
            j--;
        }
    }

    // Return the answer
    return ans;
}

// Driver Code

    let n = 8;

    let s = "10100101";

    document.write(minOperation(s, n));

</script>
```

**输出:**

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
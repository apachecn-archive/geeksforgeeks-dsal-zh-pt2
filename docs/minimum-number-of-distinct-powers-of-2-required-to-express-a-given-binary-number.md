# 表示给定二进制数所需的 2 的不同幂的最小数量

> 原文:[https://www . geeksforgeeks . org/表示给定二进制数所需的最小二乘方数/](https://www.geeksforgeeks.org/minimum-number-of-distinct-powers-of-2-required-to-express-a-given-binary-number/)

给定一个二进制字符串 **S** ，任务是找到表达一个 S
T5【例:
所需的最小[2 次幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

> **输入:** S = "111"
> **输出:** 2
> **解释:**
> 使用 2 的幂的“111”(= 7)的两种可能表示是:
> 2<sup>0</sup>+2<sup>1</sup>+2<sup>2</sup>= 1+2+4 = 7
> 2<sup>3</sup>–2<sup>0</sup>
> **输入:** S = "1101101"
> **输出:** 4
> **解释:**
> 1101101 可以表示为 2<sup>7</sup>–2<sup>4</sup>–2<sup>2</sup>+2<sup>0</sup>。

**进场:**
解决这个问题的关键观察是，我们只用 2 的 2[次方就可以替换 1 的任意连续序列**。**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 

> **图解:**
> S = "1001110"
> 连续 3 个 1 的序列，“1110”可以表示为 2<sup>4</sup>–2<sup>1</sup>T8】因此，给定的字符串

按照以下步骤解决问题:

*   反转弦 **S** 。
*   迭代字符串 **S** 。
*   通过将 **1** 置于 **R+1** 并将 **-1** 置于 **L** 来替换位于索引**【L，R】**内的 **1 的每个子串。**
*   遍历整个字符串后，计算字符串中**个非零值**的个数作为所需答案。

以下是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// distinct powers of 2 required
// to express s
void findMinimum(string s)
{
    int n = s.size();

    int x[n + 1] = { 0 };

    // Reverse the string to
    // start from lower powers
    reverse(s.begin(), s.end());

    for (int i = 0; i < n; i++) {

        // Check if the character is 1
        if (s[i] == '1') {

            if (x[i] == 1) {
                x[i + 1] = 1;
                x[i] = 0;
            }

            // Add in range provided range
            else if (i and x[i - 1] == 1) {
                x[i + 1] = 1;
                x[i - 1] = -1;
            }

            else
                x[i] = 1;
        }
    }

    // Initialize the counter
    int c = 0;

    for (int i = 0; i <= n; i++) {

        // Check if the character
        // is not 0
        if (x[i] != 0)

            // Increment the counter
            c++;
    }

    // Print the result
    cout << c << endl;
}

// Driver Code
int main()
{
    string str = "111";

    findMinimum(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to return the minimum
// distinct powers of 2 required
// to express s
static void findMinimum(String s)
{
    int n = s.length();
    int[] x = new int[n + 1];

    StringBuilder s2 = new StringBuilder(s);

    // Reverse the string to
    // start from lower powers
    s2.reverse();

    String s3 = s2.toString();

    for(int i = 0; i < n; i++)
    {

        // Check if the character is 1
        if (s3.charAt(i) == '1')
        {
            if (x[i] == 1)
            {
                x[i + 1] = 1;
                x[i] = 0;
            }

            // Add in range provided range
            else if (1 <= i && (i & x[i - 1]) == 1)
            {
                x[i + 1] = 1;
                x[i - 1] = -1;
            }
            else
                x[i] = 1;
        }
    }

    // Initialize the counter
    int c = 0;

    for(int i = 0; i <= n; i++)
    {

        // Check if the character
        // is not 0
        if (x[i] != 0)

            // Increment the counter
            c++;
    }

    // Print the result
    System.out.println(c);
}

// Driver code
public static void main(String[] args)
{
    String str = "111";

    findMinimum(str);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to return the minimum
# distinct powers of 2 required
# to express s
def findMinimum(s):

    n = len(s)
    x = [0] * (n + 1)

    # Reverse the string to
    # start from lower powers
    s = s[::-1]

    for i in range(n):

        # Check if the character is 1
        if(s[i] == '1'):
            if(x[i] == 1):
                x[i + 1] = 1
                x[i] = 0

            # Add in range provided range
            elif(i and x[i - 1] == 1):
                x[i + 1] = 1
                x[i - 1] = -1

            else:
                x[i] = 1

    # Initialize the counter
    c = 0

    for i in range(n + 1):

        # Check if the character
        # is not 0
        if(x[i] != 0):

            # Increment the counter
            c += 1

    # Print the result
    print(c)

# Driver Code
if __name__ == '__main__':

    str = "111"

    # Function Call
    findMinimum(str)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Text;

class GFG{

// Function to return the minimum
// distinct powers of 2 required
// to express s
static void findMinimum(String s)
{
    int n = s.Length;
    int[] x = new int[n + 1];

    StringBuilder s2 = new StringBuilder(s);

    // Reverse the string to
    // start from lower powers
    s2 = reverse(s2.ToString());

    String s3 = s2.ToString();

    for(int i = 0; i < n; i++)
    {

        // Check if the character is 1
        if (s3[i] == '1')
        {
            if (x[i] == 1)
            {
                x[i + 1] = 1;
                x[i] = 0;
            }

            // Add in range provided range
            else if (1 <= i && (i & x[i - 1]) == 1)
            {
                x[i + 1] = 1;
                x[i - 1] = -1;
            }
            else
                x[i] = 1;
        }
    }

    // Initialize the counter
    int c = 0;

    for(int i = 0; i <= n; i++)
    {

        // Check if the character
        // is not 0
        if (x[i] != 0)

            // Increment the counter
            c++;
    }

    // Print the result
    Console.WriteLine(c);
}

static StringBuilder reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;

    for(l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return new StringBuilder(String.Join("", a));
}

// Driver code
public static void Main(String[] args)
{
    String str = "111";

    findMinimum(str);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript Program to implement the
// above approach

// Function to return the minimum
// distinct powers of 2 required
// to express s
function findMinimum(s)
{
    var n = s.length;

    var x = Array(n+1).fill(0);

    // Reverse the string to
    // start from lower powers
    s.reverse();

    for (var i = 0; i < n; i++) {

        // Check if the character is 1
        if (s[i] == '1') {

            if (x[i] == 1) {
                x[i + 1] = 1;
                x[i] = 0;
            }

            // Add in range provided range
            else if (i && x[i - 1] == 1) {
                x[i + 1] = 1;
                x[i - 1] = -1;
            }

            else
                x[i] = 1;
        }
    }

    // Initialize the counter
    var c = 0;

    for (var i = 0; i <= n; i++) {

        // Check if the character
        // is not 0
        if (x[i] != 0)

            // Increment the counter
            c++;
    }

    // Print the result
    document.write( c );
}

// Driver Code
var str = "111".split('');
findMinimum(str);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*
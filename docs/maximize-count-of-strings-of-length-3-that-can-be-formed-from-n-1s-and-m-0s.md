# 最大化可由 N ^ 1 和 M ^ 0 形成的长度为 3 的字符串的数量

> 原文:[https://www . geeksforgeeks . org/最大化由 n-1 和 m-0 形成的长度为 3 的字符串数/](https://www.geeksforgeeks.org/maximize-count-of-strings-of-length-3-that-can-be-formed-from-n-1s-and-m-0s/)

给定两个数字 **N** 和 **M** ，分别表示 1 和 0 的计数，任务是最大化长度为 3 的二进制字符串的计数，其中包括 0 和 1，可以由给定的 **N 1s** 和 **M 0s** 形成。
**示例:**

> **输入:** N = 4，M = 5
> **输出:** 3
> **解释:**
> 可能的字符串= {“001”、“011”、“001”}
> **输入:** N = 818，M = 234
> **输出:** 234

**天真方法:**三种长度的二进制串可以按照以下条件形成:

1.  **如果 N > M:** 如果 N > 2，则 N 减 2，M 减 1，由于生成了一串类型 **110** ，因此计数增加 1。
2.  **如果 N ≤ M:** 如果 M > 2，则 M 减 2，N 减 1，由于生成了一串类型 **001** ，因此计数增加 1。

因此，想法是迭代一个循环，直到 N 或 M 变为零，并根据上述条件不断更新字符串的计数。
下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the number of
// strings of length three that can be
// made with given m 0s and n 1s
void number_of_strings(int N, int M)
{
    int ans = 0;

    // Iterate until N & M are positive
    while (N > 0 && M > 0) {

        // Case 1:
        if (N > M) {
            if (N >= 2) {
                N -= 2;
                --M;
                ++ans;
            }
            else {
                break;
            }
        }

        // Case 2:
        else {
            if (M >= 2) {
                M -= 2;
                --N;
                ++ans;
            }
            else {
                break;
            }
        }
    }

    // Print the count of strings
    cout << ans;
}

// Driver Code
int main()
{
    // Given count of 1s and 0s
    int N = 4, M = 19;

    // Function Call
    number_of_strings(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function that counts the number of
// strings of length three that can be
// made with given m 0s and n 1s
static void number_of_strings(int N, int M)
{
    int ans = 0;

    // Iterate until N & M are positive
    while (N > 0 && M > 0)
    {

        // Case 1:
        if (N > M)
        {
            if (N >= 2)
            {
                N -= 2;
                --M;
                ++ans;
            }
            else
            {
                break;
            }
        }

        // Case 2:
        else
        {
            if (M >= 2)
            {
                M -= 2;
                --N;
                ++ans;
            }
            else
            {
                break;
            }
        }
    }

    // Print the count of strings
    System.out.println(ans);
}

// Driver Code
public static void main (String[] args)
{

    // Given count of 1s and 0s
    int N = 4, M = 19;

    // Function call
    number_of_strings(N, M);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the number of
# strings of length three that can be
# made with given m 0s and n 1s
def number_of_strings(N, M):

    ans = 0

    # Iterate until N & M are positive
    while (N > 0 and M > 0):

        # Case 1:
        if (N > M):
            if (N >= 2):
                N -= 2
                M -= 1
                ans += 1

            else:
                break

        # Case 2:
        else:
            if M >= 2:
                M -= 2
                N -= 1
                ans += 1

            else:
                break

    # Print the count of strings
    print(ans)

# Driver code
if __name__ == '__main__':

    # Given count of 1s and 0s
    N = 4
    M = 19

    # Function call
    number_of_strings(N, M)

# This code is contributed by jana_sayantan
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that counts the number of
// strings of length three that can be
// made with given m 0s and n 1s
static void number_of_strings(int N, int M)
{
    int ans = 0;

    // Iterate until N & M are positive
    while (N > 0 && M > 0)
    {

        // Case 1:
        if (N > M)
        {
            if (N >= 2)
            {
                N -= 2;
                --M;
                ++ans;
            }
            else
            {
                break;
            }
        }

        // Case 2:
        else
        {
            if (M >= 2)
            {
                M -= 2;
                --N;
                ++ans;
            }
            else
            {
                break;
            }
        }
    }

    // Print the count of strings
    Console.WriteLine(ans);
}

// Driver Code
public static void Main (String[] args)
{

    // Given count of 1s and 0s
    int N = 4, M = 19;

    // Function call
    number_of_strings(N, M);
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function that counts the number of
// strings of length three that can be
// made with given m 0s and n 1s
function number_of_strings(N , M)
{
    var ans = 0;

    // Iterate until N & M are positive
    while (N > 0 && M > 0)
    {

        // Case 1:
        if (N > M)
        {
            if (N >= 2)
            {
                N -= 2;
                --M;
                ++ans;
            }
            else
            {
                break;
            }
        }

        // Case 2:
        else
        {
            if (M >= 2)
            {
                M -= 2;
                --N;
                ++ans;
            }
            else
            {
                break;
            }
        }
    }

    // Print the count of strings
    document.write(ans);
}

// Driver Code

// Given count of 1s and 0s
var N = 4, M = 19;

// Function call
number_of_strings(N, M);

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(max(A，B))*
***辅助空间:** O(1)*
**高效方法:**为了优化上述方法，观察到可以形成的二进制字符串的总数将是 N、M 和(N + M)/3 的最小值，如下所示:

*   如果 N 是最小值，并且我们有 M ≥ 2*N，那么所有类型 **110** 的字符串都可以被制作。
*   如果 M 是最小值，并且我们有 N ≥ 2*M，那么所有类型 **001** 的字符串都可以被制作。
*   否则总计数将为(N + M)/3，可以制作两种类型的琴弦 **110** 和 **001** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the number of
// strings of length 3 that can be
// made with given m 0s and n 1s
void number_of_strings(int N, int M)
{

    // Print the count of strings
    cout << min(N, min(M, (N + M) / 3));
}

// Driver Code
int main()
{
    // Given count of 1s and 0s
    int N = 4, M = 19;

    // Function Call
    number_of_strings(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

// Function that counts the number of
// Strings of length 3 that can be
// made with given m 0s and n 1s
static void number_of_Strings(int N, int M)
{
  // Print the count of Strings
  System.out.print(Math.min(N,
                            Math.min(M,
                                    (N + M) /
                                     3)));
}

// Driver Code
public static void main(String[] args)
{
  // Given count of 1s and 0s
  int N = 4, M = 19;

  // Function Call
  number_of_Strings(N, M);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the number of
# strings of length 3 that can be
# made with given m 0s and n 1s
def number_of_strings(N, M):

    # Print the count of strings
    print(min(N, min(M, (N + M) // 3)))

# Driver Code
if __name__ == '__main__':

    # Given count of 1s and 0s
    N = 4
    M = 19

    # Function call
    number_of_strings(N, M)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function that counts the number of
// Strings of length 3 that can be
// made with given m 0s and n 1s
static void number_of_Strings(int N,
                              int M)
{
  // Print the count of Strings
  Console.Write(Math.Min(N,
                Math.Min(M, (N + M) / 3)));
}

// Driver Code
public static void Main(String[] args)
{
  // Given count of 1s and 0s
  int N = 4, M = 19;

  // Function Call
  number_of_Strings(N, M);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript program for
// the above approach// Function that counts the number of
// Strings of length 3 that can be
// made with given m 0s and n 1s
function number_of_Strings(N , M)
{

  // print the count of Strings
  document.write(Math.min(N,
                            Math.min(M,
                                    (N + M) /
                                     3)));
}

// Driver Code
// Given count of 1s and 0s
var N = 4, M = 19;

// Function Call
number_of_Strings(N, M);

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*
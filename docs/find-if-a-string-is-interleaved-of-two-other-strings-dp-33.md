# 查找一个字符串是否与另外两个字符串交错| DP-33

> 原文:[https://www . geesforgeks . org/find-if-a-string-is-interleaved-of-two-other-string-DP-33/](https://www.geeksforgeeks.org/find-if-a-string-is-interleaved-of-two-other-strings-dp-33/)

给定三个字符串 A、B 和 C。编写一个函数，检查 C 是否是 A 和 B 的交错。如果 C 包含 A 和 B 的所有和唯一字符，并且保留了单个字符串中所有字符的顺序，则称 C 是 A 和 B 的交错。

**示例:**

```
Input: strings: "XXXXZY", "XXY", "XXZ"
Output: XXXXZY is interleaved of XXY and XXZ
The string XXXXZY can be made by 
interleaving XXY and XXZ
String:    XXXXZY
String 1:    XX Y
String 2:  XX  Z

Input: strings: "XXY", "YX", "X"
Output: XXY is not interleaved of YX and X
XXY cannot be formed by interleaving YX and X.
The strings that can be formed are YXX and XYX
```

**<u>简单解法</u> :** 递归。
**方法:**这里讨论一个简单的解决方案:[检查一个给定的字符串是否是另外两个给定字符串的交织](https://www.geeksforgeeks.org/check-whether-a-given-string-is-an-interleaving-of-two-other-given-strings/)。
如果字符串 A 和 B 有一些共同的字符，简单的解决方案就不起作用了。例如，让给定的字符串为 A，其他字符串为 B 和 C，让 A =“XXY”，字符串 B =“XXZ”和字符串 C =“XXZXXXY”。创建一个接受参数 A、B 和 c 的递归函数。为了处理所有情况，需要考虑两种可能性。

1.  如果 C 的第一个字符与 A 的第一个字符匹配，我们在 A 和 C 中向前移动一个字符并递归检查。
2.  如果 C 的第一个字符与 B 的第一个字符匹配，我们在 B 和 C 中向前移动一个字符并递归检查。

如果以上任何一个函数返回真，或者 A、B 和 C 为空，则返回真，否则返回假。感谢弗雷德里克·T2 提出了这个方法。

## C

```
// A simple recursive function to check
// whether C is an interleaving of A and B
bool isInterleaved(
    char* A, char* B, char* C)
{
    // Base Case: If all strings are empty
    if (!(*A || *B || *C))
        return true;

    // If C is empty and any of the
    // two strings is not empty
    if (*C == '\0')
        return false;

    // If any of the above mentioned
    // two possibilities is true,
    // then return true, otherwise false
    return ((*C == *A) && isInterleaved(
                              A + 1, B, C + 1))
           || ((*C == *B) && isInterleaved(
                                 A, B + 1, C + 1));
}
```

**复杂度分析:**

*   **时间复杂度:** O(2^n)，其中 n 是给定字符串的长度。
    我们只需要迭代整个字符串一次，因此这在 O(n)中是可能的。
*   **空间复杂度:** O(1)。
    空间的复杂性是不变的。

**<u>高效求解</u> :** 动态规划。
**方法:**上面的递归解当然有很多重叠的子问题。比如我们考虑 A =“XXX”，B =“XXX”，C =“XXXXXX”，画一个递归树，会有很多重叠的子问题。因此，像任何其他典型的[动态规划问题](https://www.geeksforgeeks.org/tag/dynamic-programming/)一样，我们可以通过创建一个表并以**自下而上的方式**存储子问题的结果来解决它。上述解决方案的自顶向下方法可以通过添加哈希映射来修改。

**算法:**

1.  创建一个大小为 M*N 的 DP 数组(矩阵)，其中 M 是第一个字符串的大小，N 是第二个字符串的大小。将矩阵初始化为 false。
2.  如果较小字符串的大小之和不等于较大字符串的大小，则返回 false 并断开数组，因为它们不能交错形成较大的字符串。
3.  运行嵌套循环，外部循环从 0 到 m，内部循环从 0 到 n。循环计数器是 I 和 j
4.  如果 I 和 j 的值都为零，则将 dp[i][j]标记为真。如果 I 的值为 0，j 为非零，B 的 j-1 字符等于 C 的 j-1 字符，则将 dp[i][j]指定为 dp[i][j-1]，同样，如果 j 为 0，则匹配 C 和 A 的第 i-1 字符，如果匹配，则将 dp[i][j]指定为 dp[i-1][j]。
5.  取三个字符 x，y，z 作为 A 的第(i-1)个字符和 B 的第(j-1)个字符和 c 的第(I+j–1)个字符。
6.  如果 x 与 z 匹配，y 与 z 不匹配，则将 dp[i][j]指定为 dp[i-1][j]同样，如果 x 不等于 z，y 等于 z，则将 dp[i][j]指定为 dp[i][j-1]
7.  如果 x 等于 y，y 等于 z，那么将 dp[i][j]指定为 dp[i][j-1]和 dp[i-1][j]的按位 OR。
8.  dp[m][n]的返回值。

*感谢* [*阿比纳夫·拉玛那*](https://plus.google.com/104230157879525004164/posts) *对这种实现方法的建议。*

## C++

```
// A Dynamic Programming based program
// to check whether a string C is
// an interleaving of two other
// strings A and B.
#include <iostream>
#include <string.h>
using namespace std;

// The main function that
// returns true if C is
// an interleaving of A
// and B, otherwise false.
bool isInterleaved(
    char* A, char* B, char* C)
{
    // Find lengths of the two strings
    int M = strlen(A), N = strlen(B);

    // Let us create a 2D table
    // to store solutions of
    // subproblems.  C[i][j] will
    // be true if C[0..i+j-1]
    // is an interleaving of
    // A[0..i-1] and B[0..j-1].
    bool IL[M + 1][N + 1];

    // Initialize all values as false.
    memset(IL, 0, sizeof(IL));

    // C can be an interleaving of
    // A and B only of the sum
    // of lengths of A & B is equal
    // to the length of C.
    if ((M + N) != strlen(C))
        return false;

    // Process all characters of A and B
    for (int i = 0; i <= M; ++i) {
        for (int j = 0; j <= N; ++j) {
            // two empty strings have an
            // empty string as interleaving
            if (i == 0 && j == 0)
                IL[i][j] = true;

            // A is empty
            else if (i == 0) {
                if (B[j - 1] == C[j - 1])
                    IL[i][j] = IL[i][j - 1];
            }

            // B is empty
            else if (j == 0) {
                if (A[i - 1] == C[i - 1])
                    IL[i][j] = IL[i - 1][j];
            }

            // Current character of C matches
            // with current character of A,
            // but doesn't match with current
            // character of B
            else if (
                A[i - 1] == C[i + j - 1]
                && B[j - 1] != C[i + j - 1])
                IL[i][j] = IL[i - 1][j];

            // Current character of C matches
            // with current character of B,
            // but doesn't match with current
            // character of A
            else if (
                A[i - 1] != C[i + j - 1]
                && B[j - 1] == C[i + j - 1])
                IL[i][j] = IL[i][j - 1];

            // Current character of C matches
            // with that of both A and B
            else if (
                A[i - 1] == C[i + j - 1]
                && B[j - 1] == C[i + j - 1])
                IL[i][j]
                    = (IL[i - 1][j]
                       || IL[i][j - 1]);
        }
    }

    return IL[M][N];
}

// A function to run test cases
void test(char* A, char* B, char* C)
{
    if (isInterleaved(A, B, C))
        cout << C << " is interleaved of "
             << A << " and " << B << endl;
    else
        cout << C << " is not interleaved of "
             << A << " and " << B << endl;
}

// Driver program to test above functions
int main()
{
    test("XXY", "XXZ", "XXZXXXY");
    test("XY", "WZ", "WZXY");
    test("XY", "X", "XXY");
    test("YX", "X", "XXY");
    test("XXY", "XXZ", "XXXXZY");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based program
// to check whether a string C is
// an interleaving of two other
// strings A and B.
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG{

// The main function that returns
// true if C is an interleaving of A
// and B, otherwise false. 
static boolean isInterleaved(String A, String B,
                             String C)
{

    // Find lengths of the two strings
    int M = A.length(), N = B.length();

    // Let us create a 2D table to store
    // solutions of subproblems. C[i][j]
    // will br true if C[0..i+j-1] is an
    // interleaving of A[0..i-1] and B[0..j-1].
    boolean IL[][] = new boolean[M + 1][N + 1];

    // IL is default initialised by false

    // C can be an interleaving of A and B
    // only if the sum of lengths of A and B
    // is equal to length of C
    if ((M + N) != C.length())
        return false;

    // Process all characters of A and B

    for(int i = 0; i <= M; i++)
    {
        for(int j = 0; j <= N; j++)
        {

            // Two empty strings have an
            // empty strings as interleaving
            if (i == 0 && j == 0)
                IL[i][j] = true;

            // A is empty
            else if (i == 0)
            {
                if (B.charAt(j - 1) ==
                    C.charAt(j - 1))
                    IL[i][j] = IL[i][j - 1];
             }

            // B is empty
            else if (j == 0)
            {
                if (A.charAt(i - 1) ==
                    C.charAt(i - 1))
                    IL[i][j] = IL[i - 1][j];
            }

            // Current character of C matches
            // with current character of A,
            // but doesn't match with current
            // character if B
            else if (A.charAt(i - 1) ==
                     C.charAt(i + j - 1) &&
                     B.charAt(j - 1) !=
                     C.charAt(i + j - 1))
                IL[i][j] = IL[i - 1][j];

            // Current character of C matches
            // with current character of B, but
            // doesn't match with current
            // character if A
            else if (A.charAt(i - 1) !=
                     C.charAt(i + j - 1) &&
                     B.charAt(j - 1) ==
                     C.charAt(i + j - 1))
                IL[i][j] = IL[i][j - 1];

            // Current character of C matches
            // with that of both A and B
            else if (A.charAt(i - 1) ==
                     C.charAt(i + j - 1) &&
                     B.charAt(j - 1) ==
                     C.charAt(i + j - 1))
                IL[i][j] = (IL[i - 1][j] ||
                            IL[i][j - 1]);
         }
    }
    return IL[M][N];
}

// Function to run test cases
static void test(String A, String B, String C)
{
    if (isInterleaved(A, B, C))
        System.out.println(C + " is interleaved of " +
                           A + " and " + B);
    else
        System.out.println(C + " is not interleaved of " +
                           A + " and " + B);
}

// Driver code
public static void main(String[] args)
{
    test("XXY", "XXZ", "XXZXXXY");
    test("XY", "WZ", "WZXY");
    test("XY", "X", "XXY");
    test("YX", "X", "XXY");
    test("XXY", "XXZ", "XXXXZY");
}
}

// This code is contributed by th_aditi
```

## 蟒蛇 3

```
# A Dynamic Programming based python3 program
# to check whether a string C is an interleaving
# of two other strings A and B.

# The main function that returns true if C is
# an interleaving of A and B, otherwise false.
def isInterleaved(A, B, C):

    # Find lengths of the two strings
    M = len(A)
    N = len(B)

    # Let us create a 2D table to store solutions of
    # subproblems. C[i][j] will be true if C[0..i + j-1]
    # is an interleaving of A[0..i-1] and B[0..j-1].
    # Initialize all values as false.
    IL = [[False] * (N + 1) for i in range(M + 1)]

    # C can be an interleaving of A and B only of sum
    # of lengths of A & B is equal to length of C.
    if ((M + N) != len(C)):
        return False

    # Process all characters of A and B
    for i in range(0, M + 1):
        for j in range(0, N + 1):

            # two empty strings have an empty string
            # as interleaving
            if (i == 0 and j == 0):
                IL[i][j] = True

            # A is empty
            elif (i == 0):
                if (B[j - 1] == C[j - 1]):
                    IL[i][j] = IL[i][j - 1]

            # B is empty
            elif (j == 0):
                if (A[i - 1] == C[i - 1]):
                    IL[i][j] = IL[i - 1][j]

            # Current character of C matches with
            # current character of A, but doesn't match
            # with current character of B
            elif (A[i - 1] == C[i + j - 1] and
                  B[j - 1] != C[i + j - 1]):
                IL[i][j] = IL[i - 1][j]

            # Current character of C matches with
            # current character of B, but doesn't match
            # with current character of A
            elif (A[i - 1] != C[i + j - 1] and
                  B[j - 1] == C[i + j - 1]):
                IL[i][j] = IL[i][j - 1]

            # Current character of C matches with
            # that of both A and B
            elif (A[i - 1] == C[i + j - 1] and
                  B[j - 1] == C[i + j - 1]):
                IL[i][j] = (IL[i - 1][j] or IL[i][j - 1])

    return IL[M][N]

# A function to run test cases
def test(A, B, C):

    if (isInterleaved(A, B, C)):
        print(C, "is interleaved of", A, "and", B)
    else:
        print(C, "is not interleaved of", A, "and", B)

# Driver Code
if __name__ == '__main__':
    test("XXY", "XXZ", "XXZXXXY")
    test("XY", "WZ", "WZXY")
    test("XY", "X", "XXY")
    test("YX", "X", "XXY")
    test("XXY", "XXZ", "XXXXZY")

# This code is contributed by ashutosh450
```

## C#

```
// A Dynamic Programming based program 
// to check whether a string C is 
// an interleaving of two other 
// strings A and B.
using System;
class GFG
{

    // The main function that returns 
    // true if C is an interleaving of A 
    // and B, otherwise false.  
    static bool isInterleaved(string A, string B, 
                                 string C) 
    {

        // Find lengths of the two strings
        int M = A.Length, N = B.Length;

        // Let us create a 2D table to store
        // solutions of subproblems. C[i][j] 
        // will br true if C[0..i+j-1] is an
        // interleaving of A[0..i-1] and B[0..j-1].
        bool[ , ] IL = new bool[M + 1, N + 1];

        // IL is default initialised by false      
        // C can be an interleaving of A and B
        // only if the sum of lengths of A and B
        // is equal to length of C
        if ((M + N) != C.Length)
            return false;

        // Process all characters of A and B 
        for(int i = 0; i <= M; i++)
        {
            for(int j = 0; j <= N; j++)
            {

                // Two empty strings have an
                // empty strings as interleaving
                if (i == 0 && j == 0)
                    IL[i, j] = true;

                // A is empty
                else if (i == 0)
                {
                    if (B[j - 1] == C[j - 1])
                        IL[i, j] = IL[i, j - 1];
                 }

                // B is empty
                else if (j == 0)
                {
                    if (A[i - 1] == C[i - 1])
                        IL[i, j] = IL[i - 1, j];
                }

                // Current character of C matches
                // with current character of A, 
                // but doesn't match with current
                // character if B
                else if (A[i - 1] == C[i + j - 1] && 
                         B[j - 1] != C[i + j - 1])
                    IL[i, j] = IL[i - 1, j];

                // Current character of C matches
                // with current character of B, but
                // doesn't match with current
                // character if A
                else if (A[i - 1] != C[i + j - 1] && 
                         B[j - 1] == C[i + j - 1])
                        IL[i, j] = IL[i, j - 1];

                // Current character of C matches
                // with that of both A and B
                else if (A[i - 1] == C[i + j - 1] && 
                         B[j - 1] != C[i + j - 1])
                       IL[i, j] = (IL[i - 1, j] || 
                                IL[i, j - 1]);
             }
        }
        return IL[M, N];
    }

    // Function to run test cases
    static void test(string A, string B, string C) 
    {
        if (isInterleaved(A, B, C))
            Console.WriteLine(C + " is interleaved of " +
                               A + " and " + B);
        else
            Console.WriteLine(C + " is not interleaved of " +
                               A + " and " + B);
    }  

  // Driver code
  static void Main()
  {
    test("XXY", "XXZ", "XXZXXXY");
    test("XY", "WZ", "WZXY");
    test("XY", "X", "XXY");
    test("YX", "X", "XXY");
    test("XXY", "XXZ", "XXXXZY");
  }
}

// This code is contributed by divyeshrabadiya07
```

**输出:**

```
XXZXXXY is not interleaved of XXY and XXZ
WZXY is interleaved of XY and WZ
XXY is interleaved of XY and X
XXY is not interleaved of YX and X
XXXXZY is interleaved of XXY and XXZ
```

更多测试用例参见[本](http://ideone.com/4jnFZu)。
**复杂性分析:**

*   **时间复杂度:** O(M*N)。
    由于需要遍历 DP 数组，所以时间复杂度为 O(M*N)。
*   **空间复杂度:** O(M*N)。
    这是存储 DP 阵列所需的空间。

https://youtu.be/WBXy-sztEwI
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
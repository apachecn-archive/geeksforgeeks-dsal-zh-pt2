# 计算长度为 N 的可能的二进制字符串，不包括 P 个连续的 0 和 Q 个连续的 1

> 原文:[https://www . geesforgeks . org/count-可能的二进制长度字符串-n-不带-p-continuous-0s-和-q-continuous-1s/](https://www.geeksforgeeks.org/count-possible-binary-strings-of-length-n-without-p-consecutive-0s-and-q-consecutive-1s/)

给定三个整数 **N** 、 **P** 和 **Q** ，任务是[计算长度为**N**T9】的所有可能的不同二进制字符串，使得每个二进制字符串不包含连续 0 次的 **P** 和连续 1 次的 **Q**](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)

**示例:**

> **输入:** N = 5，P = 2，Q = 3
> **输出:** 7
> **说明:**满足给定条件的二进制字符串有{“01010”、“01011”、“01101”、“10101”、“10110”、“11010”、“11011”}。因此，所需的输出为 7。
> 
> **输入:** N = 5，P = 3，Q = 4
> T3】输出: 21

**天真方法:**这个问题可以用[递归](https://www.geeksforgeeks.org/recursion/)来解决。以下是递归关系及其基本情况:

> 在二进制字符串的每个可能的索引处，放置值“ **0** ”或放置值“ **1**
> 
> 因此， **cntBinStr(str，N，P，Q) = cntBinStr(str + '0 '，N，P，Q) + cntBinStr(str + '1 '，N，P，Q)**
> ，其中 **cntBinStr(str，N，P，Q)** 存储不包含 **P** 连续 **1** s 和 **Q** 连续 **0** s 的不同二进制字符串的计数。
> 
> **基本情况:**如果**长度(str)= N**，检查 **str** 是否满足给定条件。如果发现为真，则返回 1。否则，返回 0。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// string satisfy the given
// condition or not
bool checkStr(string str,
              int P, int Q)
{
    // Stores the length
    // of string
    int N = str.size();

    // Stores the previous
    // character of the string
    char prev = str[0];

    // Stores the count of
    // consecutive equal characters
    int cnt = 0;

    // Traverse the string
    for (int i = 0; i < N;
         i++) {

        // If current character
        // is equal to the
        // previous character
        if (str[i] == prev) {

            cnt++;
        }
        else {

            // If count of consecutive
            // 1s is more than Q
            if (prev == '1' && cnt >= Q) {

                return false;
            }

            // If count of consecutive
            // 0s is more than P
            if (prev == '0' && cnt >= P) {

                return false;
            }

            // Reset value of cnt
            cnt = 1;
        }

        prev = str[i];
    }

    // If count of consecutive
    // 1s is more than Q
    if (prev == '1' && cnt >= Q) {
        return false;
    }

    // If count of consecutive
    // 0s is more than P
    if (prev == '0' && cnt >= P) {
        return false;
    }

    return true;
}

// Function to count all distinct
// binary strings that satisfy
// the given condition
int cntBinStr(string str, int N,
              int P, int Q)
{
    // Stores the length of str
    int len = str.size();

    // If length of str is N
    if (len == N) {

        // If str satisfy
        // the given condition
        if (checkStr(str, P, Q))
            return 1;

        // If str does not satisfy
        // the given condition
        return 0;
    }

    // Append a character '0' at
    // end of str
    int X = cntBinStr(str + '0',
                      N, P, Q);

    // Append a character '1' at
    // end of str
    int Y = cntBinStr(str + '1',
                      N, P, Q);

    // Return total count
    // of binary strings
    return X + Y;
}

// Driver Code
int main()
{
    int N = 5, P = 2, Q = 3;
    cout << cntBinStr("", N, P, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach 
class GFG{

// Function to check if a
// string satisfy the given
// condition or not
static boolean checkStr(String str,
                        int P, int Q)
{

    // Stores the length
    // of string
    int N = str.length();

    // Stores the previous
    // character of the string
    char prev = str.charAt(0);

    // Stores the count of
    // consecutive equal characters
    int cnt = 0;

    // Traverse the string
    for(int i = 0; i < N; i++)
    {

        // If current character
        // is equal to the
        // previous character
        if (str.charAt(i) == prev)
        {
            cnt++;
        }
        else
        {

            // If count of consecutive
            // 1s is more than Q
            if (prev == '1' && cnt >= Q)
            {
                return false;
            }

            // If count of consecutive
            // 0s is more than P
            if (prev == '0' && cnt >= P)
            {
                return false;
            }

            // Reset value of cnt
            cnt = 1;
        }
        prev = str.charAt(i);
    }

    // If count of consecutive
    // 1s is more than Q
    if (prev == '1' && cnt >= Q)
    {
        return false;
    }

    // If count of consecutive
    // 0s is more than P
    if (prev == '0' && cnt >= P)
    {
        return false;
    }
    return true;
}

// Function to count all distinct
// binary strings that satisfy
// the given condition
static int cntBinStr(String str, int N,
                          int P, int Q)
{

    // Stores the length of str
    int len = str.length();

    // If length of str is N
    if (len == N)
    {

        // If str satisfy
        // the given condition
        if (checkStr(str, P, Q))
            return 1;

        // If str does not satisfy
        // the given condition
        return 0;
    }

    // Append a character '0' at
    // end of str
    int X = cntBinStr(str + '0',
                      N, P, Q);

    // Append a character '1' at
    // end of str
    int Y = cntBinStr(str + '1',
                      N, P, Q);

    // Return total count
    // of binary strings
    return X + Y;
}

// Driver Code
public static void main (String[] args)
{
    int N = 5, P = 2, Q = 3;

    System.out.println(cntBinStr("", N, P, Q));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a
# satisfy the given
# condition or not
def checkStr(str, P, Q):

    # Stores the length
    # of string
    N = len(str)

    # Stores the previous
    # character of the string
    prev = str[0]

    # Stores the count of
    # consecutive equal
    # characters
    cnt = 0

    # Traverse the string
    for i in range(N):

        # If current character
        # is equal to the
        # previous character
        if (str[i] == prev):
            cnt += 1

        else:

            # If count of consecutive
            # 1s is more than Q
            if (prev == '1' and
                cnt >= Q):
                return False

            # If count of consecutive
            # 0s is more than P
            if (prev == '0' and
                cnt >= P):
                return False

            # Reset value of cnt
            cnt = 1

        prev = str[i]

    # If count of consecutive
    # 1s is more than Q
    if (prev == '1'and
        cnt >= Q):
        return False

    # If count of consecutive
    # 0s is more than P
    if (prev == '0' and
        cnt >= P):
        return False

    return True

# Function to count all
# distinct binary strings
# that satisfy the given
# condition
def cntBinStr(str, N,
              P, Q):

    # Stores the length
    # of str
    lenn = len(str)

    # If length of str
    # is N
    if (lenn == N):

        # If str satisfy
        # the given condition
        if (checkStr(str, P, Q)):
            return 1

        # If str does not satisfy
        # the given condition
        return 0

    # Append a character '0'
    # at end of str
    X = cntBinStr(str + '0',
                  N, P, Q)

    # Append a character
    # '1' at end of str
    Y = cntBinStr(str + '1',
                  N, P, Q)

    # Return total count
    # of binary strings
    return X + Y

# Driver Code
if __name__ == '__main__':

    N = 5
    P = 2
    Q = 3   
    print(cntBinStr("", N,
                    P, Q))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to check if a
// string satisfy the given
// condition or not
static bool checkStr(string str,
                     int P, int Q)
{

    // Stores the length
    // of string
    int N = str.Length;

    // Stores the previous
    // character of the string
    char prev = str[0];

    // Stores the count of
    // consecutive equal characters
    int cnt = 0;

    // Traverse the string
    for(int i = 0; i < N; i++)
    {

        // If current character
        // is equal to the
        // previous character
        if (str[i] == prev)
        {
            cnt++;
        }
        else
        {

            // If count of consecutive
            // 1s is more than Q
            if (prev == '1' && cnt >= Q)
            {
                return false;
            }

            // If count of consecutive
            // 0s is more than P
            if (prev == '0' && cnt >= P)
            {
                return false;
            }

            // Reset value of cnt
            cnt = 1;
        }

        prev = str[i];
    }

    // If count of consecutive
    // 1s is more than Q
    if (prev == '1' && cnt >= Q)
    {
        return false;
    }

    // If count of consecutive
    // 0s is more than P
    if (prev == '0' && cnt >= P)
    {
        return false;
    }

    return true;
}

// Function to count all distinct
// binary strings that satisfy
// the given condition
static int cntBinStr(string str, int N,
                          int P, int Q)
{

    // Stores the length of str
    int len = str.Length;

    // If length of str is N
    if (len == N)
    {

        // If str satisfy
        // the given condition
        if (checkStr(str, P, Q))
            return 1;

        // If str does not satisfy
        // the given condition
        return 0;
    }

    // Append a character '0' at
    // end of str
    int X = cntBinStr(str + '0',
                      N, P, Q);

    // Append a character '1' at
    // end of str
    int Y = cntBinStr(str + '1',
                      N, P, Q);

    // Return total count
    // of binary strings
    return X + Y;
}

// Driver Code
public static void Main ()
{
    int N = 5, P = 2, Q = 3;

    Console.WriteLine(cntBinStr("", N, P, Q));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if a
// string satisfy the given
// condition or not
function checkStr(str, P, Q)
{

    // Stores the length
    // of string
    let N = str.length;

    // Stores the previous
    // character of the string
    let prev = str[0];

    // Stores the count of
    // consecutive equal characters
    let cnt = 0;

    // Traverse the string
    for(let i = 0; i < N; i++)
    {

        // If current character
        // is equal to the
        // previous character
        if (str[i] == prev)
        {
            cnt++;
        }
        else
        {

            // If count of consecutive
            // 1s is more than Q
            if (prev == '1' && cnt >= Q)
            {
                return false;
            }

            // If count of consecutive
            // 0s is more than P
            if (prev == '0' && cnt >= P)
            {
                return false;
            }

            // Reset value of cnt
            cnt = 1;
        }
        prev = str[i];
    }

    // If count of consecutive
    // 1s is more than Q
    if (prev == '1' && cnt >= Q)
    {
        return false;
    }

    // If count of consecutive
    // 0s is more than P
    if (prev == '0' && cnt >= P)
    {
        return false;
    }
    return true;
}

// Function to count all distinct
// binary strings that satisfy
// the given condition
function cntBinStr(str, N, P, Q)
{

    // Stores the length of str
    let len = str.length;

    // If length of str is N
    if (len == N)
    {

        // If str satisfy
        // the given condition
        if (checkStr(str, P, Q))
            return 1;

        // If str does not satisfy
        // the given condition
        return 0;
    }

    // Append a character '0' at
    // end of str
    let X = cntBinStr(str + '0',
                      N, P, Q);

    // Append a character '1' at
    // end of str
    let Y = cntBinStr(str + '1',
                      N, P, Q);

    // Return total count
    // of binary strings
    return X + Y;
}

// Driver Code

    let N = 5, P = 2, Q = 3;

    document.write(cntBinStr("", N, P, Q));

</script>
```

**Output**

```
7
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照以下步骤解决问题:

*   初始化两个 2D [](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)[阵列](https://www.geeksforgeeks.org/array-data-structure/)，说**零【N】【P】**和**一【N】【Q】**。
*   **零[i][j]** 存储长度为 **i** 的二进制字符串的计数，其具有 **j** 个连续的 0。以自下而上的方式填充**零[i][j]** 的所有值。

> 在第 i <sup>个</sup>索引处插入 0。
> **情况 1:** 如果(I–1)<sup>字符串的第</sup>个索引包含 1。
> 
> ![zero[i][1] = \sum\limits_{j=1}^{Q - 1}one[i - 1][j]                       ](img/d6d0e499dcf478f90783a1714ca73292.png "Rendered by QuickLaTeX.com")
> 
> **情况 2:** 如果字符串的(I–1)<sup>第</sup>个索引包含 0。
> 
> ![zero[i][j] = zero[i-1][j-1]                       ](img/e2cf52600a1960ab223654b360b9f679.png "Rendered by QuickLaTeX.com")
> 
> 对于[2，P–1]范围内的所有 r。

*   **1[I][j]**存储长度为 **i** 的二进制字符串的计数，这些字符串具有 **j** 个连续的 1。以自下而上的方式填充 0[I][j]的所有值。

> 在第 i <sup>个</sup>索引处插入 1。
> **情况 1:** 如果(i-1) <sup>字符串的第</sup>个索引包含 0。
> 
> ![one[i][1] = \sum\limits_{j=1}^{P - 1}zero[i - 1][j]                       ](img/b770acac6841e326bb20b8ee32abfd23.png "Rendered by QuickLaTeX.com")
> 
> **情况 2:** 如果(i-1) <sup>字符串的第</sup>个索引包含 1。
> 
> ![one[i][j] = one[i-1][j-1]                       ](img/8fcab9e456c6025aeecb5730fca72797.png "Rendered by QuickLaTeX.com")
> 
> 对于[2，Q–1]范围内的所有 j。

*   最后，打印满足给定条件的子阵列数。

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count binary strings
// that satisfy the given condition
int cntBinStr(int N, int P, int Q)
{
    // zero[i][j] stores count
    // of binary strings of length i
    // having j consecutive 0s
    int zero[N + 1][P];

    // one[i][j] stores count
    // of binary strings of length i
    // having j consecutive 1s
    int one[N + 1][Q];

    // Set all values of
    // zero[][] array to 0
    memset(zero, 0, sizeof(zero));

    // Set all values of
    // one[i][j] array to 0
    memset(one, 0, sizeof(one));

    // Base case
    zero[1][1] = one[1][1] = 1;

    // Fill all the values of zero[i][j]
    // and one[i][j] in bottom up manner
    for (int i = 2; i <= N; i++) {

        for (int j = 2; j < P;
             j++) {
            zero[i][j] = zero[i - 1][j - 1];
        }

        for (int j = 1; j < Q;
             j++) {
            zero[i][1] = zero[i][1] + one[i - 1][j];
        }

        for (int j = 2; j < Q;
             j++) {
            one[i][j] = one[i - 1][j - 1];
        }

        for (int j = 1; j < P;
             j++) {
            one[i][1] = one[i][1] + zero[i - 1][j];
        }
    }

    // Stores count of binary strings
    // that satisfy the given condition
    int res = 0;

    // Count binary strings of
    // length N having less than
    // P consecutive 0s
    for (int i = 1; i < P; i++) {
        res = res + zero[N][i];
    }

    // Count binary strings of
    // length N having less than
    // Q consecutive 1s
    for (int i = 1; i < Q; i++) {
        res = res + one[N][i];
    }

    return res;
}

// Driver Code
int main()
{
    int N = 5, P = 2, Q = 3;
    cout << cntBinStr(N, P, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count binary Strings
// that satisfy the given condition
static int cntBinStr(int N, int P, int Q)
{

    // zero[i][j] stores count
    // of binary Strings of length i
    // having j consecutive 0s
    int [][]zero = new int[N + 1][P];

    // one[i][j] stores count
    // of binary Strings of length i
    // having j consecutive 1s
    int [][]one = new int[N + 1][Q];

    // Base case
    zero[1][1] = one[1][1] = 1;

    // Fill all the values of zero[i][j]
    // and one[i][j] in bottom up manner
    for(int i = 2; i <= N; i++)
    {
        for(int j = 2; j < P; j++)
        {
            zero[i][j] = zero[i - 1][j - 1];
        }

        for(int j = 1; j < Q; j++)
        {
            zero[i][1] = zero[i][1] +
                          one[i - 1][j];
        }

        for(int j = 2; j < Q; j++)
        {
            one[i][j] = one[i - 1][j - 1];
        }

        for(int j = 1; j < P; j++)
        {
            one[i][1] = one[i][1] +
                       zero[i - 1][j];
        }
    }

    // Stores count of binary Strings
    // that satisfy the given condition
    int res = 0;

    // Count binary Strings of
    // length N having less than
    // P consecutive 0s
    for(int i = 1; i < P; i++)
    {
        res = res + zero[N][i];
    }

    // Count binary Strings of
    // length N having less than
    // Q consecutive 1s
    for(int i = 1; i < Q; i++)
    {
        res = res + one[N][i];
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int N = 5, P = 2, Q = 3;

    System.out.print(cntBinStr(N, P, Q));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count binary
# Strings that satisfy the
# given condition
def cntBinStr(N, P, Q):

    # zero[i][j] stores count
    # of binary Strings of length i
    # having j consecutive 0s
    zero = [[0 for i in range(P)]
               for j in range(N + 1)];

    # one[i][j] stores count
    # of binary Strings of length i
    # having j consecutive 1s
    one = [[0 for i in range(Q)]
              for j in range(N + 1)];

    # Base case
    zero[1][1] = one[1][1] = 1;

    # Fill all the values of
    # zero[i][j] and one[i][j]
    # in bottom up manner
    for i in range(2, N + 1):
        for j in range(2, P):
            zero[i][j] = zero[i - 1][j - 1];

        for j in range(1, Q):
            zero[i][1] = (zero[i][1] +
                          one[i - 1][j]);

        for j in range(2, Q):
            one[i][j] = one[i - 1][j - 1];

        for j in range(1, P):
            one[i][1] = one[i][1] + zero[i - 1][j];

    # Stores count of binary
    # Strings that satisfy
    # the given condition
    res = 0;

    # Count binary Strings of
    # length N having less than
    # P consecutive 0s
    for i in range(1, P):
        res = res + zero[N][i];

    # Count binary Strings of
    # length N having less than
    # Q consecutive 1s
    for i in range(1, Q):
        res = res + one[N][i];

    return res;

# Driver Code
if __name__ == '__main__':

    N = 5;
    P = 2;
    Q = 3;
    print(cntBinStr(N, P, Q));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count binary Strings
// that satisfy the given condition
static int cntBinStr(int N, int P, int Q)
{

    // zero[i,j] stores count
    // of binary Strings of length i
    // having j consecutive 0s
    int [,]zero = new int[N + 1, P];

    // one[i,j] stores count
    // of binary Strings of length i
    // having j consecutive 1s
    int [,]one = new int[N + 1, Q];

    // Base case
    zero[1, 1] = one[1, 1] = 1;

    // Fill all the values of zero[i,j]
    // and one[i,j] in bottom up manner
    for(int i = 2; i <= N; i++)
    {
        for(int j = 2; j < P; j++)
        {
            zero[i, j] = zero[i - 1, j - 1];
        }

        for(int j = 1; j < Q; j++)
        {
            zero[i, 1] = zero[i, 1] +
                          one[i - 1, j];
        }

        for(int j = 2; j < Q; j++)
        {
            one[i, j] = one[i - 1, j - 1];
        }

        for(int j = 1; j < P; j++)
        {
            one[i, 1] = one[i, 1] +
                       zero[i - 1, j];
        }
    }

    // Stores count of binary Strings
    // that satisfy the given condition
    int res = 0;

    // Count binary Strings of
    // length N having less than
    // P consecutive 0s
    for(int i = 1; i < P; i++)
    {
        res = res + zero[N, i];
    }

    // Count binary Strings of
    // length N having less than
    // Q consecutive 1s
    for(int i = 1; i < Q; i++)
    {
        res = res + one[N, i];
    }
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5, P = 2, Q = 3;

    Console.Write(cntBinStr(N, P, Q));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to count binary strings
// that satisfy the given condition
function cntBinStr(N, P, Q)
{
    // zero[i][j] stores count
    // of binary strings of length i
    // having j consecutive 0s
    //and
    // Set all values of
    // zero[][] array to 0
    var zero = new Array(N+1).fill(0).
    map(item=>(new Array(P).fill(0)));

    // one[i][j] stores count
    // of binary strings of length i
    // having j consecutive 1s
    //and
    // Set all values of
    // one[i][j] array to 0
    var one  = new Array(N+1).fill(0).
    map(item=>(new Array(Q).fill(0)));;

    // Base case
    zero[1][1] = one[1][1] = 1;

    // Fill all the values of zero[i][j]
    // and one[i][j] in bottom up manner
    for (var i = 2; i <= N; i++) {

        for (var j = 2; j < P;
             j++) {
            zero[i][j] = zero[i - 1][j - 1];
        }

        for (var j = 1; j < Q;
             j++) {
            zero[i][1] = zero[i][1] + one[i - 1][j];
        }

        for (var j = 2; j < Q;
             j++) {
            one[i][j] = one[i - 1][j - 1];
        }

        for (var j = 1; j < P;
             j++) {
            one[i][1] = one[i][1] + zero[i - 1][j];
        }
    }

    // Stores count of binary strings
    // that satisfy the given condition
    var res = 0;

    // Count binary strings of
    // length N having less than
    // P consecutive 0s
    for (var i = 1; i < P; i++) {
        res = res + zero[N][i];
    }

    // Count binary strings of
    // length N having less than
    // Q consecutive 1s
    for (var i = 1; i < Q; i++) {
        res = res + one[N][i];
    }

    return res;
}

var N = 5, P = 2, Q = 3;
 document.write( cntBinStr(N, P, Q));

// This code in contributed by SoumikMondal

</script>
```

**Output**

```
7
```

***时间复杂度:** O(N * (P + Q))*
***辅助空间:** O(N * (P + Q))*
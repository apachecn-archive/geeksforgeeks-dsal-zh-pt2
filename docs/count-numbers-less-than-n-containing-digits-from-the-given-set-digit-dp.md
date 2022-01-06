# 计数给定集合中包含数字的小于 N 的数字:数字 DP

> 原文:[https://www . geeksforgeeks . org/count-numbers-小于 n-包含给定集合数字中的数字-dp/](https://www.geeksforgeeks.org/count-numbers-less-than-n-containing-digits-from-the-given-set-digit-dp/)

给定一个整数 **N** 和一组数字 **D[]** ，由[1，9]中的数字组成。任务是计算可能少于 **N** 的数字，这些数字来自给定的一组数字。

**示例:**

> **输入:**D =[“1”、“4”、“9”]，N = 10
> **输出:** 3
> **解释:**
> 给定的一组数字只有 3 个可能小于 3 的数字–
> 1、4、9
> 
> **输入:**D[]= {“1”、“3”、“5”、“7”}，N = 100
> **输出:** 20
> **解释:**
> 给定的一组数字只有 20 个可能小于 100 的数字–
> 1、3、5、7、11、13、15、17、31、33、35、37、51、53、55、57、71、73、77

**天真方法:**检查范围[1，N]中所有数字的位数，如果一个数字的所有位数都属于给定的位数集，则计数增加 1。

**高效方法:**其思想是使用[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/) 的概念，遍历给定的数字集合，生成严格小于给定数字 n 的所有数字。[递归地](https://www.geeksforgeeks.org/recursion/)为该数字的所有可能位置选择该数字，并传递一个布尔变量**以检查通过包含该数字，该数字是否落入给定范围。**

**让我们考虑一下 DP 的可能状态–**

1.  *****pos*** :告知要选择的数字的位置，使数字落入给定范围。**
2.  *****紧俏*** :这有助于我们了解当前位数是否受限。如果数字受到限制，则可以从给定的数字集中选择任何数字。否则，可以在[1，N[位置]]范围内选择数字。**
3.  *****大小*** :它会告诉你要选择的位数。**

**下面是递归函数的图示:**

*   ****基本情况:**这个问题的基本情况是当要选择的数字的位置等于要选择的数字的长度时，那么只有一个可能的数字包含到目前为止选择的数字。**

```
if (position == countDigits(N))
    return 1
```

*   ****递归情况:**为了生成给定范围内的数字，使用紧变量选择范围内可能的数字，如下所示:

    *   如果**的值为 0，表示包含该数字将使数字小于给定范围。**
    *   **否则，如果**紧**的值为 1，表示通过包含该数字，将给出大于给定范围的数字。因此，我们可以在获得紧值 1 后移除所有置换，以避免更多的递归调用。**** 
*   ****为每个位置选择每个数字后，存储可能的数字计数。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ implementation to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits
#include <bits/stdc++.h>

using namespace std;

int dp[15][2];

// Function to convert integer
// into the string
string convertToString(int num)
{
    stringstream ss;
    ss << num;
    string s = ss.str();
    return s;
}

// Recursive function to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits
int calculate(int pos, int tight,
    int D[], int sz, string& num)
{
    // Base case
    if (pos == num.length())
        return 1;

    // Condition when the subproblem
    // is computed previously
    if (dp[pos][tight] != -1)
        return dp[pos][tight];

    int val = 0;

    // Condition when the number
    // chosen till now is definietly
    // smaller than the given number N
    if (tight == 0) {

        // Loop to traverse all the
        // digits of the given set
        for (int i = 0; i < sz; i++) {

            if (D[i] < (num[pos] - '0')) {
                val += calculate(pos + 1,
                           1, D, sz, num);
            }
            else if (D[i] == num[pos] - '0')
                val += calculate(pos + 1,
                       tight, D, sz, num);
        }
    }
    else {
        // Loop to traverse all the
        // digits from the given set
        for (int i = 0; i < sz; i++) {
            val += calculate(pos + 1,
                    tight, D, sz, num);
        }
    }

    // Store the solution for
    // current subproblem
    return dp[pos][tight] = val;
}

// Function to count the numbers
// less then N from given set of digits
int countNumbers(int D[], int N, int sz)
{
    // Converting the number to string
    string num = convertToString(N);
    int len = num.length();

    // Initially no subproblem
    // is solved till now
    memset(dp, -1, sizeof(dp));

    // Find the solution of all the
    // number equal to the length of
    // the given number N
    int ans = calculate(0, 0, D, sz, num);

    // Loop to find the number less in
    // in the length of the given number
    for (int i = 1; i < len; i++)
        ans += calculate(i, 1, D, sz, num);

    return ans;
}

// Driver Code
int main()
{
    int sz = 3;

    int D[sz] = { 1, 4, 9 };
    int N = 10;

    // Function Call
    cout << countNumbers(D, N, sz);
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java implementation to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits
import java.util.*;

class GFG{

static int [][]dp = new int[15][2];

// Function to convert integer
// into the String
static String convertToString(int num)
{
    return String.valueOf(num);
}

// Recursive function to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits
static int calculate(int pos, int tight,
    int D[], int sz, String num)
{
    // Base case
    if (pos == num.length())
        return 1;

    // Condition when the subproblem
    // is computed previously
    if (dp[pos][tight] != -1)
        return dp[pos][tight];

    int val = 0;

    // Condition when the number
    // chosen till now is definietly
    // smaller than the given number N
    if (tight == 0) {

        // Loop to traverse all the
        // digits of the given set
        for (int i = 0; i < sz; i++) {

            if (D[i] < (num.charAt(pos) - '0')) {
                val += calculate(pos + 1,
                           1, D, sz, num);
            }
            else if (D[i] == num.charAt(pos) - '0')
                val += calculate(pos + 1,
                       tight, D, sz, num);
        }
    }
    else {
        // Loop to traverse all the
        // digits from the given set
        for (int i = 0; i < sz; i++) {
            val += calculate(pos + 1,
                    tight, D, sz, num);
        }
    }

    // Store the solution for
    // current subproblem
    return dp[pos][tight] = val;
}

// Function to count the numbers
// less then N from given set of digits
static int countNumbers(int D[], int N, int sz)
{
    // Converting the number to String
    String num = convertToString(N);
    int len = num.length();

    // Initially no subproblem
    // is solved till now
    for (int i = 0; i < 15; i++)
        for (int j = 0; j < 2; j++)
            dp[i][j] = -1;

    // Find the solution of all the
    // number equal to the length of
    // the given number N
    int ans = calculate(0, 0, D, sz, num);

    // Loop to find the number less in
    // in the length of the given number
    for (int i = 1; i < len; i++)
        ans += calculate(i, 1, D, sz, num);

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int sz = 3;

    int D[] = { 1, 4, 9 };
    int N = 10;

    // Function Call
    System.out.print(countNumbers(D, N, sz));
}
}

// This code is contributed by Rajput-Ji**
```

## ****蟒蛇 3****

```
**# Python3 implementation to find the
# count of numbers possible less
# than N, such that every digit
# is from the given set of digits
import numpy as np;
dp = np.ones((15,2))*-1;

# Function to convert integer
# into the string
def convertToString(num) :
    return str(num);

# Recursive function to find the
# count of numbers possible less
# than N, such that every digit
# is from the given set of digits
def calculate(pos,tight,  D, sz, num) :

    # Base case
    if (pos == len(num)):
        return 1;

    # Condition when the subproblem
    # is computed previously
    if (dp[pos][tight] != -1) :
        return dp[pos][tight];

    val = 0;

    # Condition when the number
    # chosen till now is definietly
    # smaller than the given number N
    if (tight == 0) :

        # Loop to traverse all the
        # digits of the given set
        for i in range(sz) :

            if (D[i] < (ord(num[pos]) - ord('0'))) :
                val += calculate(pos + 1, 1, D, sz, num);

            elif (D[i] == ord(num[pos]) - ord('0')) :
                val += calculate(pos + 1, tight, D, sz, num);

    else :
        # Loop to traverse all the
        # digits from the given set
        for i in range(sz) :
            val += calculate(pos + 1, tight, D, sz, num);

    # Store the solution for
    # current subproblem
    dp[pos][tight] = val;

    return dp[pos][tight];

# Function to count the numbers
# less then N from given set of digits
def countNumbers(D, N, sz) :

    # Converting the number to string
    num = convertToString(N);
    length = len(num);

    # Initially no subproblem
    # is solved till now
    # dp = np.ones((15,2))*-1;

    # Find the solution of all the
    # number equal to the length of
    # the given number N
    ans = calculate(0, 0, D, sz, num);

    # Loop to find the number less in
    # in the length of the given number
    for i in range(1,length) :
        ans += calculate(i, 1, D, sz, num);

    return ans;

# Driver Code
if __name__ == "__main__" :

    sz = 3;

    D = [ 1, 4, 9 ];
    N = 10;

    # Function Call
    print(countNumbers(D, N, sz));

    # This code is contributed by AnkitRai01**
```

## ****C#****

```
**// C# implementation to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits
using System;

class GFG{

static int [,]dp = new int[15, 2];

// Function to convert integer
// into the String
static String convertToString(int num)
{
    return String.Join("",num);
}

// Recursive function to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits
static int calculate(int pos, int tight,
    int []D, int sz, String num)
{
    // Base case
    if (pos == num.Length)
        return 1;

    // Condition when the subproblem
    // is computed previously
    if (dp[pos,tight] != -1)
        return dp[pos,tight];

    int val = 0;

    // Condition when the number
    // chosen till now is definietly
    // smaller than the given number N
    if (tight == 0) {

        // Loop to traverse all the
        // digits of the given set
        for (int i = 0; i < sz; i++) {

            if (D[i] < (num[pos] - '0')) {
                val += calculate(pos + 1,
                           1, D, sz, num);
            }
            else if (D[i] == num[pos] - '0')
                val += calculate(pos + 1,
                       tight, D, sz, num);
        }
    }
    else {
        // Loop to traverse all the
        // digits from the given set
        for (int i = 0; i < sz; i++) {
            val += calculate(pos + 1,
                    tight, D, sz, num);
        }
    }

    // Store the solution for
    // current subproblem
    return dp[pos,tight] = val;
}

// Function to count the numbers
// less then N from given set of digits
static int countNumbers(int []D, int N, int sz)
{
    // Converting the number to String
    String num = convertToString(N);
    int len = num.Length;

    // Initially no subproblem
    // is solved till now
    for (int i = 0; i < 15; i++)
        for (int j = 0; j < 2; j++)
            dp[i,j] = -1;

    // Find the solution of all the
    // number equal to the length of
    // the given number N
    int ans = calculate(0, 0, D, sz, num);

    // Loop to find the number less in
    // in the length of the given number
    for (int i = 1; i < len; i++)
        ans += calculate(i, 1, D, sz, num);

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int sz = 3;

    int []D = { 1, 4, 9 };
    int N = 10;

    // Function Call
    Console.Write(countNumbers(D, N, sz));
}
}

// This code is contributed by Princi Singh**
```

## ****java 描述语言****

```
**<script>

// JavaScript implementation to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits

var dp = Array.from(Array(15), ()=>Array(2).fill(-1));

// Recursive function to find the
// count of numbers possible less
// than N, such that every digit
// is from the given set of digits
function calculate(pos, tight, D, sz, num)
{
    // Base case
    if (pos == num.length)
        return 1;

    // Condition when the subproblem
    // is computed previously
    if (dp[pos][tight] != -1)
        return dp[pos][tight];

    var val = 0;

    // Condition when the number
    // chosen till now is definietly
    // smaller than the given number N
    if (tight == 0) {

        // Loop to traverse all the
        // digits of the given set
        for (var i = 0; i < sz; i++) {

            if (D[i] < (num[pos] - '0')) {
                val += calculate(pos + 1,
                           1, D, sz, num);
            }
            else if (D[i] == num[pos] - '0')
                val += calculate(pos + 1,
                       tight, D, sz, num);
        }
    }
    else {
        // Loop to traverse all the
        // digits from the given set
        for (var i = 0; i < sz; i++) {
            val += calculate(pos + 1,
                    tight, D, sz, num);
        }
    }

    // Store the solution for
    // current subproblem
    return dp[pos][tight] = val;
}

// Function to count the numbers
// less then N from given set of digits
function countNumbers(D, N, sz)
{
    // Converting the number to string
    var num = (N.toString());
    var len = num.length;

    // Find the solution of all the
    // number equal to the length of
    // the given number N
    var ans = calculate(0, 0, D, sz, num);

    // Loop to find the number less in
    // in the length of the given number
    for (var i = 1; i < len; i++)
        ans += calculate(i, 1, D, sz, num);

    return ans;
}

// Driver Code
var sz = 3;
var D = [1, 4, 9];
var N = 10;

// Function Call
document.write( countNumbers(D, N, sz));

</script>**
```

******Output:** 

```
3
```**** 

******时间复杂度**:O(Len(D))
T3】空间复杂度 : O(12*2)****
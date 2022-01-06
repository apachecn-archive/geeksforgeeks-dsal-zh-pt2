# 没有一对相等的连续数字的 N 位数字的计数

> 原文:[https://www . geeksforgeeks . org/n 位数计数-没有一对相等的连续数字/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-having-no-pair-of-equal-consecutive-digits/)

给定一个整数 **N** ，任务是找出 **N 位数**的总计数，使得没有两个连续的数字相等。

**示例:**

> **输入:** N = 2
> **输出:** 81
> **解释:**
> 计算可能的 2 位数，即[10，99] = 90
> 范围内的数字所有连续数字相等的 2 位数都是{11，22，33，44，55，66，77，88，99}。
> 因此，所需计数= 90–9 = 81
> 
> **输入:**N = 1
> T3】输出: 10

**天真法:**解决这个问题最简单的方法是迭代所有可能的 N 位数，并检查每个数字是否有任意两个连续的数字相等。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
void count(int N)
{

    // Base Case
    if (N == 1)
    {
        cout << 10 << endl;
        return;
    }

    // Lowest N-digit number
    int l = pow(10, N - 1);

    // Highest N-digit number
    int r = pow(10, N) - 1;

    // Stores the count of all
    // required numbers
    int ans = 0;

    // Iterate over all N-digit numbers
    for(int i = l; i <= r; i++)
    {
        string s = to_string(i);
        int flag = 0;

        // Iterate over all digits
        for(int j = 1; j < N; j++)
        {

            // Check for equal pair of
            // adjacent digits
            if (s[j] == s[j - 1])
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            ans++;
    }
    cout << ans << endl;
}

// Driver Code
int main()
{
    int N = 2;

    count(N);
    return 0;
}

// This code is contributed by rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG {

    // Function to count the number
    // of N-digit numbers with no
    // equal pair of consecutive digits
    public static void count(int N)
    {

        // Base Case
        if (N == 1) {
            System.out.println(10);
            return;
        }

        // Lowest N-digit number
        int l = (int)Math.pow(10, N - 1);

        // Highest N-digit number
        int r = (int)Math.pow(10, N) - 1;

        // Stores the count of all
        // required numbers
        int ans = 0;

        // Iterate over all N-digit numbers
        for (int i = l; i <= r; i++) {
            String s = Integer.toString(i);
            int flag = 0;

            // Iterate over all digits
            for (int j = 1; j < N; j++) {

                // Check for equal pair of
                // adjacent digits
                if (s.charAt(j) == s.charAt(j - 1)) {
                    flag = 1;
                    break;
                }
            }
            if (flag == 0)
                ans++;
        }
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2;
        count(N);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to count the number
# of N-digit numbers with no
# equal pair of consecutive digits
def count(N):

    # Base Case
    if (N == 1):
        print(10);
        return;

    # Lowest N-digit number
    l = int(pow(10, N - 1));

    # Highest N-digit number
    r = int(pow(10, N) - 1);

    # Stores the count of all
    # required numbers
    ans = 0;

    # Iterate over all N-digit numbers
    for i in range(l, r + 1):
        s = str(i);
        flag = 0;

        # Iterate over all digits
        for j in range(1, N):

            # Check for equal pair of
            # adjacent digits
            if (s[j] == s[j - 1]):
                flag = 1;
                break;

        if (flag == 0):
            ans+=1;

    print(ans);

# Driver Code
if __name__ == '__main__':
    N = 2;
    count(N);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
public static void count(int N)
{

    // Base Case
    if (N == 1)
    {
        Console.WriteLine(10);
        return;
    }

    // Lowest N-digit number
    int l = (int)Math.Pow(10, N - 1);

    // Highest N-digit number
    int r = (int)Math.Pow(10, N) - 1;

    // Stores the count of all
    // required numbers
    int ans = 0;

    // Iterate over all N-digit numbers
    for(int i = l; i <= r; i++)
    {
        String s = i.ToString();
        int flag = 0;

        // Iterate over all digits
        for(int j = 1; j < N; j++)
        {

            // Check for equal pair of
            // adjacent digits
            if (s[j] == s[j - 1])
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            ans++;
    }
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2;
    count(N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
function count(N)
{

    // Base Case
    if (N == 1)
    {
        document.write(10 + "<br>");
        return;
    }

    // Lowest N-digit number
    var l = Math.pow(10, N - 1);

    // Highest N-digit number
    var r = Math.pow(10, N) - 1;

    // Stores the count of all
    // required numbers
    var ans = 0;

    // Iterate over all N-digit numbers
    for(var i = l; i <= r; i++)
    {
        var s = (i.toString());
        var flag = 0;

        // Iterate over all digits
        for(var j = 1; j < N; j++)
        {

            // Check for equal pair of
            // adjacent digits
            if (s[j] == s[j - 1])
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            ans++;
    }
    document.write( ans + "<br>");
}

// Driver Code
var N = 2;

count(N);

// This code is contributed by itsok

</script>
```

**Output:** 

```
81
```

***时间复杂度:** O(N * (10 <sup>N</sup> ，其中 N 为给定整数。*
***辅助空间:** O(1)*

**动态规划方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法进行优化。按照以下步骤解决问题:

*   初始化 **DP[][]** ，其中 **DP[i][j]** 存储有 **i** 位数字的计数，以 **j** 结束。
*   从 **2** 迭代到 **N** ，按照以下步骤操作:
    *   将**DP【I-1】【j】**中 **j** 范围从 **0** 到 **9** 的所有数值相加，计算有效 **i-1** 位数的总数，并存储在 **temp** 中。
    *   更新**DP[I][j]= temp–DP[I-1][j]**，其中 **j** 的范围从 **0 到 9** 。
*   结果是**DP【N】【j】**之和，其中 **j** 的范围从 **0 到 9**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
void count(int N)
{

   // Base Case
   if (N == 1)
   {
     cout << (10) << endl;
     return;
   }

  int dp[N][10];
  memset(dp, 0, sizeof(dp));
  for (int i = 1; i < 10; i++)
    dp[0][i] = 1;
  for (int i = 1; i < N; i++)
  {

    // Calculate the total count
    // of valid (i-1)-digit numbers
    int temp = 0;
    for (int j = 0; j < 10; j++)
      temp += dp[i - 1][j];

    // Update dp[][] table
    for (int j = 0; j < 10; j++)
      dp[i][j] = temp - dp[i - 1][j];
  }

  // Calculate the count of
  // required N-digit numbers
  int ans = 0;
  for (int i = 0; i < 10; i++)
    ans += dp[N - 1][i];
  cout << ans << endl;
}

// Driver Code
int main()
{
  int N = 2;
  count(N);
  return 0;
}

// This code is contributed by sapnasingh4991
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// of the above approach
import java.util.*;
class GFG {

    // Function to count the number
    // of N-digit numbers with no
    // equal pair of consecutive digits
    public static void count(int N)
    {

        // Base Case
        if (N == 1) {
            System.out.println(10);
            return;
        }

        int dp[][] = new int[N][10];

        for (int i = 1; i < 10; i++)
            dp[0][i] = 1;
        for (int i = 1; i < N; i++) {

            // Calculate the total count
            // of valid (i-1)-digit numbers
            int temp = 0;
            for (int j = 0; j < 10; j++)
                temp += dp[i - 1][j];

            // Update dp[][] table
            for (int j = 0; j < 10; j++)
                dp[i][j] = temp - dp[i - 1][j];
        }

        // Calculate the count of
        // required N-digit numbers
        int ans = 0;
        for (int i = 0; i < 10; i++)
            ans += dp[N - 1][i];
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2;
        count(N);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# of the above approach

# Function to count the number
# of N-digit numbers with no
# equal pair of consecutive digits
def count(N):

    # Base Case
    if (N == 1):
        print(10);
        return;

    dp = [[0 for i in range(10)]
             for j in range(N)]

    for i in range(1,10):
        dp[0][i] = 1;
    for i in range(1, N):

        # Calculate the total count
        # of valid (i-1)-digit numbers
        temp = 0;
        for j in range(10):
            temp += dp[i - 1][j];

        # Update dp table
        for j in range(10):
            dp[i][j] = temp - dp[i - 1][j];

    # Calculate the count of
    # required N-digit numbers
    ans = 0;
    for i in range(10):
        ans += dp[N - 1][i];
    print(ans);

# Driver Code
if __name__ == '__main__':
    N = 2;
    count(N);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# Program to implement
// of the above approach
using System;
class GFG{

  // Function to count the number
  // of N-digit numbers with no
  // equal pair of consecutive digits
  public static void count(int N)
  {

    // Base Case
    if (N == 1)
    {
      Console.WriteLine(10);
      return;
    }

    int [,]dp = new int[N, 10];

    for (int i = 1; i < 10; i++)
      dp[0, i] = 1;
    for (int i = 1; i < N; i++)
    {

      // Calculate the total count
      // of valid (i-1)-digit numbers
      int temp = 0;
      for (int j = 0; j < 10; j++)
        temp += dp[i - 1, j];

      // Update [,]dp table
      for (int j = 0; j < 10; j++)
        dp[i, j] = temp - dp[i - 1, j];
    }

    // Calculate the count of
    // required N-digit numbers
    int ans = 0;
    for (int i = 0; i < 10; i++)
      ans += dp[N - 1, i];
    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 2;
    count(N);
  }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
function count(N)
{

    // Base Case
    if (N == 1)
    {
        document.write((10) + "<br>");
        return;
    }

    var dp = Array.from(Array(N),
                   ()=> Array(10).fill(0));

    for(var i = 1; i < 10; i++)
        dp[0][i] = 1;

    for(var i = 1; i < N; i++)
    {

        // Calculate the total count
        // of valid (i-1)-digit numbers
        var temp = 0;
        for(var j = 0; j < 10; j++)
            temp += dp[i - 1][j];

        // Update dp[][] table
        for(var j = 0; j < 10; j++)
            dp[i][j] = temp - dp[i - 1][j];
    }

    // Calculate the count of
    // required N-digit numbers
    var ans = 0;
    for(var i = 0; i < 10; i++)
        ans += dp[N - 1][i];

    document.write(ans);
}

// Driver Code
var N = 2;

count(N);

// This code is contributed by noob2000

</script>
```

**Output:** 

```
81
```

***时间复杂度:** O(N)，其中 N 为给定整数*
***辅助空间:** O(N)*

**高效方法:**通过观察可以进一步优化上述方法，对于任意 N 位数，需要的答案是**9<sup>N</sup>T5】，可以使用[二进制幂运算](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)进行计算。**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Iterative Function to calculate
// (x^y) % mod in O(log y)
int power(int x, int y, int mod)
{
    // Initialize result
    int res = 1;

    // Update x if x >= mod
    x = x % mod;

    // If x is divisible by mod
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if ((y & 1) == 1)
            res = (res * x) % mod;

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x) % mod;
    }
    return res;
}

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
void count(int N)
{

    // Base Case
    if (N == 1)
    {
        cout << 10 << endl;
        return;
    }

    cout << (power(9, N, 1000000007)) << endl;
}

// Driver Code
int main()
{
    int N = 3;
    count(N);
    return 0;
}

// This code is contributed by sapnasingh4991
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// of the above approach
import java.util.*;

class GFG {

    // Iterative Function to calculate
    // (x^y) % mod in O(log y)
    static int power(int x, int y, int mod)
    {
        // Initialize result
        int res = 1;

        // Update x if x >= mod
        x = x % mod;

        // If x is divisible by mod
        if (x == 0)
            return 0;

        while (y > 0) {

            // If y is odd, multiply x
            // with result
            if ((y & 1) == 1)
                res = (res * x) % mod;

            // y must be even now
            // y = y / 2
            y = y >> 1;
            x = (x * x) % mod;
        }
        return res;
    }

    // Function to count the number
    // of N-digit numbers with no
    // equal pair of consecutive digits
    public static void count(int N)
    {

        // Base Case
        if (N == 1) {
            System.out.println(10);
            return;
        }

        System.out.println(power(9, N,
                                 1000000007));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 3;
        count(N);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# of the above approach

# Iterative Function to calculate
# (x^y) % mod in O(log y)
def power(x, y, mod):

    # Initialize result
    res = 1;

    # Update x if x >= mod
    x = x % mod;

    # If x is divisible by mod
    if (x == 0):
        return 0;

    while (y > 0):

        # If y is odd, multiply x
        # with result
        if ((y & 1) == 1):
            res = (res * x) % mod;

        # y must be even now
        # y = y / 2
        y = y >> 1;
        x = (x * x) % mod;

    return res;

# Function to count the number
# of N-digit numbers with no
# equal pair of consecutive digits
def count(N):

    # Base Case
    if (N == 1):
        print(10);
        return;

    print(power(9, N, 1000000007));

# Driver Code
if __name__ == '__main__':
    N = 3;
    count(N);

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# program to implement
// of the above approach
using System;

class GFG{

// Iterative Function to calculate
// (x^y) % mod in O(log y)
static int power(int x, int y, int mod)
{

    // Initialize result
    int res = 1;

    // Update x if x >= mod
    x = x % mod;

    // If x is divisible by mod
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if ((y & 1) == 1)
            res = (res * x) % mod;

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x) % mod;
    }
    return res;
}

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
public static void count(int N)
{

    // Base Case
    if (N == 1)
    {
        Console.WriteLine(10);
        return;
    }

    Console.WriteLine(power(9, N,
                            1000000007));
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    count(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// of the above approach

// Iterative Function to calculate
// (x^y) % mod in O(log y)
function power(x, y, mod)
{

    // Initialize result
    let res = 1;

    // Update x if x >= mod
    x = x % mod;

    // If x is divisible by mod
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if ((y & 1) == 1)
            res = (res * x) % mod;

        // y must be even now
        // y = y / 2
        y = y >> 1;
        x = (x * x) % mod;
    }
    return res;
}

// Function to count the number
// of N-digit numbers with no
// equal pair of consecutive digits
function count(N)
{

    // Base Case
    if (N == 1)
    {
        document.write(10);
        return;
    }
    document.write(power(9, N, 1000000007));
}

// Driver Code
let N = 3;

count(N);

// this code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
729
```

***时间复杂度:** O(logN)*
***空间复杂度:** O(1)*
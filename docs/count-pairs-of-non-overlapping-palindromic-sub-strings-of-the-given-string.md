# 统计给定串的不重叠回文子串对

> 原文:[https://www . geesforgeks . org/count-对-非重叠-回文-给定字符串的子字符串/](https://www.geeksforgeeks.org/count-pairs-of-non-overlapping-palindromic-sub-strings-of-the-given-string/)

给定一根绳子 **S** 。任务是统计不重叠的回文子串对 **S1** 和 **S2** ，使得串应该是**S1【L1…R1】**和**S2【L2…R2】**，其中**0≤L1≤R1<L2≤R2<N**。任务是统计非重叠回文子串的对的数量。
**示例:**

> **输入:** s = "aaa"
> **输出:** 5
> 所有可能的对为(s[0]，s[1])，(s[0]，s[2])、
> (s[0]，s[1，2])、(s[1]，s[2])和(s[0，1]，s[2])
> **输入:** s = "abacaba"
> **输出:**30

**方法:**我们可以用动态规划来解决上面的问题。我们可以首先创建 **DP** 表，该表存储**子串【I。j]** 是不是回文。我们维护一个布尔**DP【n】【n】**以自下而上的方式填充。如果子串是回文， **dp[i][j]** 的值为真，否则为假。为了计算 dp[i][j]，我们首先检查 **dp[i+1][j-1]** 的值，如果该值为真且 **s[i]** 与 **s[j]** 相同，则我们使 **dp[i][j]** 为真。否则， **dp[i][j]** 的值为假。此后，可以遵循以下步骤来获得对的数量。

*   创建一个**左[]** 数组，其中**左[i]** 存储包括 I 在内的索引 I 左边回文数的计数
*   创建一个**右[]** 数组，其中**右[i]** 存储包括 I 在内的索引 I 右边回文数的计数
*   从 **0** 迭代到**长度-1** ，加上**左[I]*右[i+1]** 。每个索引的总和将是所需的对数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100

// Pre-processing function
void pre_process(bool dp[N][N], string s)
{

    // Get the size of the string
    int n = s.size();

    // Initially mark every
    // position as false
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            dp[i][j] = false;
    }

    // For the length
    for (int j = 1; j <= n; j++) {

        // Iterate for every index with
        // length j
        for (int i = 0; i <= n - j; i++) {

            // If the length is less than 2
            if (j <= 2) {

                // If characters are equal
                if (s[i] == s[i + j - 1])
                    dp[i][i + j - 1] = true;
            }

            // Check for equal
            else if (s[i] == s[i + j - 1])
                dp[i][i + j - 1] = dp[i + 1][i + j - 2];
        }
    }
}

// Function to return the number of pairs
int countPairs(string s)
{

    // Create the dp table initially
    bool dp[N][N];
    pre_process(dp, s);
    int n = s.length();

    // Declare the left array
    int left[n];
    memset(left, 0, sizeof left);

    // Declare the right array
    int right[n];
    memset(right, 0, sizeof right);

    // Initially left[0] is 1
    left[0] = 1;

    // Count the number of palindrome
    // pairs to the left
    for (int i = 1; i < n; i++) {

        for (int j = 0; j <= i; j++) {

            if (dp[j][i] == 1)
                left[i]++;
        }
    }

    // Initially right most as 1
    right[n - 1] = 1;

    // Count the number of palindrome
    // pairs to the right
    for (int i = n - 2; i >= 0; i--) {

        right[i] = right[i + 1];

        for (int j = n - 1; j >= i; j--) {

            if (dp[i][j] == 1)
                right[i]++;
        }
    }

    int ans = 0;

    // Count the number of pairs
    for (int i = 0; i < n - 1; i++)
        ans += left[i] * right[i + 1];

    return ans;
}

// Driver code
int main()
{
    string s = "abacaba";
    cout << countPairs(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int N = 100;

    // Pre-processing function
    static void pre_process(boolean dp[][], char[] s)
    {

        // Get the size of the string
        int n = s.length;

        // Initially mark every
        // position as false
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dp[i][j] = false;
            }
        }

        // For the length
        for (int j = 1; j <= n; j++)
        {

            // Iterate for every index with
            // length j
            for (int i = 0; i <= n - j; i++)
            {

                // If the length is less than 2
                if (j <= 2)
                {

                    // If characters are equal
                    if (s[i] == s[i + j - 1])
                    {
                        dp[i][i + j - 1] = true;
                    }
                }
                // Check for equal
                else if (s[i] == s[i + j - 1])
                {
                    dp[i][i + j - 1] = dp[i + 1][i + j - 2];
                }
            }
        }
    }

    // Function to return the number of pairs
    static int countPairs(String s)
    {

        // Create the dp table initially
        boolean dp[][] = new boolean[N][N];
        pre_process(dp, s.toCharArray());
        int n = s.length();

        // Declare the left array
        int left[] = new int[n];

        // Declare the right array
        int right[] = new int[n];

        // Initially left[0] is 1
        left[0] = 1;

        // Count the number of palindrome
        // pairs to the left
        for (int i = 1; i < n; i++)
        {

            for (int j = 0; j <= i; j++)
            {

                if (dp[j][i] == true)
                {
                    left[i]++;
                }
            }
        }

        // Initially right most as 1
        right[n - 1] = 1;

        // Count the number of palindrome
        // pairs to the right
        for (int i = n - 2; i >= 0; i--)
        {

            right[i] = right[i + 1];

            for (int j = n - 1; j >= i; j--)
            {

                if (dp[i][j] == true)
                {
                    right[i]++;
                }
            }
        }

        int ans = 0;

        // Count the number of pairs
        for (int i = 0; i < n - 1; i++)
        {
            ans += left[i] * right[i + 1];
        }

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abacaba";
        System.out.println(countPairs(s));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 100

# Pre-processing function
def pre_process(dp, s):

    # Get the size of the string
    n = len(s)

    # Initially mark every
    # position as false
    for i in range(n):
        for j in range(n):
            dp[i][j] = False

    # For the length
    for j in range(1, n + 1):

        # Iterate for every index with
        # length j
        for i in range(n - j + 1):

            # If the length is less than 2
            if (j <= 2):

                # If characters are equal
                if (s[i] == s[i + j - 1]):
                    dp[i][i + j - 1] = True

            # Check for equal
            elif (s[i] == s[i + j - 1]):
                dp[i][i + j - 1] = dp[i + 1][i + j - 2]

# Function to return the number of pairs
def countPairs(s):

    # Create the dp table initially
    dp = [[False for i in range(N)]
                 for j in range(N)]
    pre_process(dp, s)
    n = len(s)

    # Declare the left array
    left = [0 for i in range(n)]

    # Declare the right array
    right = [0 for i in range(n)]

    # Initially left[0] is 1
    left[0] = 1

    # Count the number of palindrome
    # pairs to the left
    for i in range(1, n):

        for j in range(i + 1):

            if (dp[j][i] == 1):
                left[i] += 1

    # Initially right most as 1
    right[n - 1] = 1

    # Count the number of palindrome
    # pairs to the right
    for i in range(n - 2, -1, -1):

        right[i] = right[i + 1]

        for j in range(n - 1, i - 1, -1):

            if (dp[i][j] == 1):
                right[i] += 1

    ans = 0

    # Count the number of pairs
    for i in range(n - 1):
        ans += left[i] * right[i + 1]

    return ans

# Driver code
s = "abacaba"
print(countPairs(s))

# This code is contributed by mohit kumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$N = 100;

// Pre-processing function
function pre_process($dp, $s)
{

    // Get the size of the string
    $n = strlen($s);

    // Initially mark every
    // position as false
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
            $dp[$i][$j] = false;
    }

    // For the length
    for ($j = 1; $j <= $n; $j++)
    {

        // Iterate for every index with
        // length j
        for ($i = 0; $i <= $n - $j; $i++)
        {

            // If the length is less than 2
            if ($j <= 2)
            {

                // If characters are equal
                if ($s[$i] == $s[$i + $j - 1])
                    $dp[$i][$i + $j - 1] = true;
            }

            // Check for equal
            else if ($s[$i] == $s[$i + $j - 1])
                $dp[$i][$i + $j - 1] = $dp[$i + 1][$i + $j - 2];
        }
    }
    return $dp;
}

// Function to return the number of pairs
function countPairs($s)
{

    // Create the dp table initially
    $dp = array(array());
    $dp = pre_process($dp, $s);

    $n = strlen($s);

    // Declare the left array
    $left = array_fill(0, $n, 0);

    // Declare the right array
    $right = array_fill(0, $n, 0);

    // Initially left[0] is 1
    $left[0] = 1;

    // Count the number of palindrome
    // pairs to the left
    for ($i = 1; $i < $n; $i++)
    {
        for ($j = 0; $j <= $i; $j++)
        {
            if ($dp[$j][$i] == 1)
                $left[$i]++;
        }
    }

    // Initially right most as 1
    $right[$n - 1] = 1;

    // Count the number of palindrome
    // pairs to the right
    for ($i = $n - 2; $i >= 0; $i--)
    {
        $right[$i] = $right[$i + 1];

        for ($j = $n - 1; $j >= $i; $j--)
        {
            if ($dp[$i][$j] == 1)
                $right[$i]++;
        }
    }

    $ans = 0;

    // Count the number of pairs
    for ($i = 0; $i < $n - 1; $i++)
        $ans += $left[$i] * $right[$i + 1];

    return $ans;
}

// Driver code
$s = "abacaba";
echo countPairs($s);

// This code is contributed by Ryuga
?>
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int N = 100;

    // Pre-processing function
    static void pre_process(bool [,]dp, char[] s)
    {

        // Get the size of the string
        int n = s.Length;

        // Initially mark every
        // position as false
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dp[i,j] = false;
            }
        }

        // For the length
        for (int j = 1; j <= n; j++)
        {

            // Iterate for every index with
            // length j
            for (int i = 0; i <= n - j; i++)
            {

                // If the length is less than 2
                if (j <= 2)
                {

                    // If characters are equal
                    if (s[i] == s[i + j - 1])
                    {
                        dp[i,i + j - 1] = true;
                    }
                }
                // Check for equal
                else if (s[i] == s[i + j - 1])
                {
                    dp[i,i + j - 1] = dp[i + 1,i + j - 2];
                }
            }
        }
    }

    // Function to return the number of pairs
    static int countPairs(String s)
    {

        // Create the dp table initially
        bool [,]dp = new bool[N,N];
        pre_process(dp, s.ToCharArray());
        int n = s.Length;

        // Declare the left array
        int []left = new int[n];

        // Declare the right array
        int []right = new int[n];

        // Initially left[0] is 1
        left[0] = 1;

        // Count the number of palindrome
        // pairs to the left
        for (int i = 1; i < n; i++)
        {

            for (int j = 0; j <= i; j++)
            {

                if (dp[j,i] == true)
                {
                    left[i]++;
                }
            }
        }

        // Initially right most as 1
        right[n - 1] = 1;

        // Count the number of palindrome
        // pairs to the right
        for (int i = n - 2; i >= 0; i--)
        {

            right[i] = right[i + 1];

            for (int j = n - 1; j >= i; j--)
            {

                if (dp[i,j] == true)
                {
                    right[i]++;
                }
            }
        }

        int ans = 0;

        // Count the number of pairs
        for (int i = 0; i < n - 1; i++)
        {
            ans += left[i] * right[i + 1];
        }

        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "abacaba";
        Console.Write(countPairs(s));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
var N = 100;

    // Pre-processing function
    function pre_process( dp,  s) {

        // Get the size of the string
        var n = s.length;

        // Initially mark every
        // position as false
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                dp[i][j] = false;
            }
        }

        // For the length
        for (j = 1; j <= n; j++) {

            // Iterate for every index with
            // length j
            for (i = 0; i <= n - j; i++) {

                // If the length is less than 2
                if (j <= 2) {

                    // If characters are equal
                    if (s[i] == s[i + j - 1]) {
                        dp[i][i + j - 1] = true;
                    }
                }
                // Check for equal
                else if (s[i] == s[i + j - 1]) {
                    dp[i][i + j - 1] = dp[i + 1][i + j - 2];
                }
            }
        }
    }

    // Function to return the number of pairs
    function countPairs(s) {

        // Create the dp table initially
        var dp = Array(N).fill().map(()=>Array(N).fill(false));
        pre_process(dp, s);
        var n = s.length;

        // Declare the left array
        var left = Array(n).fill(0);

        // Declare the right array
        var right = Array(n).fill(0);

        // Initially left[0] is 1
        left[0] = 1;

        // Count the number of palindrome
        // pairs to the left
        for (i = 1; i < n; i++) {

            for (j = 0; j <= i; j++) {

                if (dp[j][i] == true) {
                    left[i]++;
                }
            }
        }

        // Initially right most as 1
        right[n - 1] = 1;

        // Count the number of palindrome
        // pairs to the right
        for (i = n - 2; i >= 0; i--) {

            right[i] = right[i + 1];

            for (j = n - 1; j >= i; j--) {

                if (dp[i][j] == true) {
                    right[i]++;
                }
            }
        }

        var ans = 0;

        // Count the number of pairs
        for (i = 0; i < n - 1; i++) {
            ans += left[i] * right[i + 1];
        }

        return ans;
    }

    // Driver code

        var s = "abacaba";
        document.write(countPairs(s));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
36
```
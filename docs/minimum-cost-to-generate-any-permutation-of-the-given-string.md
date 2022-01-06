# 生成给定字符串的任何排列的最小成本

> 原文:[https://www . geeksforgeeks . org/生成给定字符串的任意排列的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-generate-any-permutation-of-the-given-string/)

给定大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，该字符串由第一个 **N** 字母和大小为 **N*N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)mat【】组成，其中**mat【I】【j】**代表将字母表的 **i <sup>th</sup>** 字符放在**j<sup>th</sup>T22 之前的成本任务是找到生成给定字符串的任何[排列的最小成本。](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)**

**示例:**

> **输入:** str = "abcde "，mat[][]= {{0，5，1，5，3}，{4，0，9，4，2}，{7，9，0，10，7}，{1，2，8，0，2}，{3，9，7，7，0}}
> **输出:** 8
> **解释:**
> 置换' dbeac '可以最小代价 8 生成。
> 放置 d = 0 的成本(因为没有 prev 字符)
> 在 d 之后放置 b 的成本= mat[4][2] = 2
> 在 b 之后放置 e 的成本= mat[2][5] = 2
> 在 e 之后放置 a 的成本= mat[5][1] = 3
> 在 a 之后放置 c 的成本= mat[1][3] = 1
> 总成本= 2 + 2 + 3 + 1 = 8
> 
> **输入:** str = "abcde "，mat[][] = {{0，9，4，8，10}，{7，0，9，5，5}，{2，8，0，4，1}，{4，10，5，0，5}，{4，3，4，7，0 }}
> **输出:** 13

**天真方法:**天真的想法是[生成给定字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能排列，并找到每个排列的成本。然后打印所有可能成本中的最小成本。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N！)*

**有效方法:**优化上述方法的思路是使用[带位屏蔽的动态编程](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)。请注意，所有字符都是不同的，可能只有 26 个字母。所以用一个遮罩来存储每个角色的存在。以下是步骤:

1.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的所有字符，并将每个字符放在每个可用的位置，即掩码中设置了该位。
2.  然后，将角色放置在当前位置，并计算放置角色的成本。
3.  通过翻转当前字符的位，移动到下一个位置。
4.  在每次迭代中，掩码代表当前位置的可用字符数。
5.  完成上述步骤后，打印所有计算成本中的最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if the current bit is set
bool check(int mask, int i)
{
    int c = (mask & (1 << i));
    return c != 0;
}

// Function to find the minimum cost
// to form any permutation of string s
int solve(vector<vector<int>> a, string s,
          int n, int prev, int mask,
          vector<vector<int>> dp)
{

    // Base Case
    if (mask == 0)
        return 0;

    // Return the precomputed state
    if (dp[mask][prev + 1] != -1)
        return dp[mask][prev + 1];

    int ans = 10000;

    // Iterate over the string and
    // check all possible characters
    // available for current position
    for(int i = 0; i < s.length(); i++)
    {
        int id = s[i] - 'a';

        // Check if character can be
        // placed at current position
        if (check(mask, id))
        {

            // As there is no previous
            // character so the cost
            // for 1st character is 0
            if (prev == -1)
            {
                ans = min(ans, solve(a, s, n, id,
                                     mask ^ (1 << id), dp));
            }

            // Find the cost of current
            // character and move to next
            // position
            else
            {
                ans = min(ans, a[prev][id] +
                          solve(a, s, n, id,
                                mask ^ (1 << id), dp));
            }
        }
    }

    // Store the answer for each
    // current state
    dp[mask][prev + 1] = ans;
    return ans;
}

// Function that generates any
// permutation of the given
// string with minimum cost
void generatePermutation(int mask, int n,
                         vector<vector<int>> a,
                         string s)
{

    // Initialize dp table
    vector<vector<int>> dp((1 << n) + 5 ,
           vector<int> (n + 5, -1));

    // Set all the bits of the
    // current character id
    for(int i = 0; i < s.length(); i++)
    {
        int id = s[i] - 'a';
        mask |= (1 << id);
    }

    // Minimum cost of generating
    // the permutation
    cout << solve(a, s, n, -1, mask, dp)
         << endl;
}

// Driver Code  
int main()
{
    int N = 5;
    string str = "abcde";

    vector<vector<int>> mat = { { 0, 5, 1, 5, 3 },
                                { 4, 0, 9, 4, 2 },
                                { 7, 9, 0, 10, 7 },
                                { 1, 2, 8, 0, 2 },
                                { 3, 9, 7, 7, 0 } };

    // Function Call
    generatePermutation(0, N, mat, str);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

public class Main {

    // Function to find the minimum cost
    // to form any permutation of string s
    public static int solve(
        int a[][], String s, int n,
        int prev, int mask, int[][] dp)
    {
        // Base Case
        if (mask == 0)
            return 0;

        // Return the precomputed state
        if (dp[mask][prev + 1] != -1)
            return dp[mask][prev + 1];

        int ans = 10000;

        // Iterate over the string and
        // check all possible characters
        // available for current position
        for (int i = 0; i < s.length(); i++) {

            int id = s.charAt(i) - 'a';

            // Check if character can be
            // placed at current position
            if (check(mask, id)) {

                // As there is no previous
                // character so the cost
                // for 1st character is 0
                if (prev == -1) {

                    ans
                        = Math.min(ans,
                                   solve(
                                       a, s,
                                       n, id,
                                       mask ^ (1 << id),
                                       dp));
                }

                // Find the cost of current
                // character and move to next
                // position
                else {
                    ans = Math.min(
                        ans,
                        a[prev][id]
                            + solve(
                                  a, s,
                                  n, id,
                                  mask ^ (1 << id),
                                  dp));
                }
            }
        }

        // Store the answer for each
        // current state
        dp[mask][prev + 1] = ans;
        return ans;
    }

    // Function that returns true
    // if the current bit is set
    public static boolean
    check(int mask, int i)
    {
        int c = (mask & (1 << i));
        return c != 0;
    }

    // Function that generates any
    // permutation of the given
    // string with minimum cost
    static void generatePermutation(
        int mask, int n, int a[][],
        String s)
    {

        // Initialize dp table
        int dp[][] = new int[(1 << n) + 5][n + 5];

        for (int i[] : dp)
            Arrays.fill(i, -1);

        // Set all the bits of the
        // current character id
        for (int i = 0;
             i < s.length(); i++) {

            int id = s.charAt(i) - 'a';
            mask |= (1 << id);
        }

        // Minimum cost of generating
        // the permutation
        System.out.println(solve(
            a, s, n, -1, mask, dp));
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 5;

        String str = "abcde";

        int mat[][] = { { 0, 5, 1, 5, 3 },
                        { 4, 0, 9, 4, 2 },
                        { 7, 9, 0, 10, 7 },
                        { 1, 2, 8, 0, 2 },
                        { 3, 9, 7, 7, 0 } };

        // Function Call
        generatePermutation(0, N, mat, str);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the
# minimum cost to form
# any permutation of
# string s
def solve(a, s, n, prev,
          mask, dp):
    # Base Case
    if (mask == 0):
        return 0;

    # Return the precomputed state
    if (dp[mask][prev + 1] != -1):
        return dp[mask][prev + 1];

    ans = 10000;

    # Iterate over the string and
    # check all possible characters
    # available for current position
    for i in range(len(s)):
        id = ord(s[i]) - ord('a');

        # Check if character can be
        # placed at current position
        if (check(mask, id)):

            # As there is no previous
            # character so the cost
            # for 1st character is 0
            if (prev == -1):
                ans = min(ans,
                      solve(a, s,
                            n, id,
                            mask ^ (1 <<
                            id), dp));

            # Find the cost of current
            # character and move to next
            # position
            else:
                ans = min(ans, a[prev][id] +
                      solve(a, s, n,
                            id, mask ^
                            (1 << id), dp));

    # Store the answer for each
    # current state
    dp[mask][prev + 1] = ans;
    return ans;

# Function that returns
# True if the current
# bit is set
def check(mask, i):

    c = (mask & (1 << i));
    return c != 0;

# Function that generates any
# permutation of the given
# string with minimum cost
def generatePermutation(mask, n,
                        a, s):

    # Initialize dp table
    dp = [[-1 for i in range(n + 5)]
              for j in range((1 << n) + 5)]

    # Set all the bits of the
    # current character id
    for i in range(len(s)):
        id = ord(s[i]) - ord('a');
        mask |= (1 << id);

    # Minimum cost of generating
    # the permutation
    print(solve(a, s, n,
                -1, mask, dp));

# Driver Code
if __name__ == '__main__':

    N = 5;
    str = "abcde";
    mat = [[0, 5, 1, 5, 3],
           [4, 0, 9, 4, 2],
           [7, 9, 0, 10, 7],
           [1, 2, 8, 0, 2],
           [3, 9, 7, 7, 0]];

    # Function Call
    generatePermutation(0, N,
                        mat, str);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the minimum cost
// to form any permutation of string s
public static int solve(int[,]a, String s, int n,
                        int prev, int mask, int[,] dp)
{
  // Base Case
  if (mask == 0)
    return 0;

  // Return the precomputed state
  if (dp[mask,prev + 1] != -1)
    return dp[mask, prev + 1];

  int ans = 10000;

  // Iterate over the string and
  // check all possible characters
  // available for current position
  for (int i = 0;
           i < s.Length; i++)
  {
    int id = s[i] - 'a';

    // Check if character can be
    // placed at current position
    if (check(mask, id))
    {
      // As there is no previous
      // character so the cost
      // for 1st character is 0
      if (prev == -1)
      {
        ans = Math.Min(ans,
                       solve(a, s, n, id,
                             mask ^ (1 << id), dp));
      }

      // Find the cost of current
      // character and move to next
      // position
      else
      {
        ans = Math.Min(ans, a[prev,id] +
                       solve(a, s, n, id,
                             mask ^ (1 << id), dp));
      }
    }
  }

  // Store the answer for each
  // current state
  dp[mask, prev + 1] = ans;
  return ans;
}

// Function that returns true
// if the current bit is set
public static bool check(int mask, int i)
{
  int c = (mask & (1 << i));
  return c != 0;
}

// Function that generates any
// permutation of the given
// string with minimum cost
static void generatePermutation(int mask, int n,
                                int[,]a, String s)
{
  // Initialize dp table
  int [,]dp = new int[(1 << n) + 5,
                      n + 5];

  for(int i = 0;
          i < (1 << n) + 5; i++)
    for(int j = 0;
            j < n + 5; j++)
      dp[i, j] = -1;

  // Set all the bits of the
  // current character id
  for (int i = 0;
       i < s.Length; i++)
  {
    int id = s[i] - 'a';
    mask |= (1 << id);
  }

  // Minimum cost of generating
  // the permutation
  Console.WriteLine(solve(a, s, n,
                          -1, mask, dp));
}

// Driver Code
public static void Main(String []args)
{
  int N = 5;
  String str = "abcde";
  int [,]mat = {{0, 5, 1, 5, 3},
                {4, 0, 9, 4, 2},
                {7, 9, 0, 10, 7},
                {1, 2, 8, 0, 2},
                {3, 9, 7, 7, 0}};

  // Function Call
  generatePermutation(0, N, mat, str);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that returns true
// if the current bit is set
function check(mask, i)
{
    var c = (mask & (1 << i));
    return c != 0;
}

// Function to find the minimum cost
// to form any permutation of string s
function solve(a, s,  n, prev, mask, dp)
{

    // Base Case
    if (mask == 0)
        return 0;

    // Return the precomputed state
    if (dp[mask][prev + 1] != -1)
        return dp[mask][prev + 1];

    var ans = 10000;

    // Iterate over the string and
    // check all possible characters
    // available for current position
    for(var i = 0; i < s.length; i++)
    {
        var id = s[i].charCodeAt(0) - 'a'.charCodeAt(0);

        // Check if character can be
        // placed at current position
        if (check(mask, id))
        {

            // As there is no previous
            // character so the cost
            // for 1st character is 0
            if (prev == -1)
            {
                ans = Math.min(ans, solve(a, s, n, id,
                                     mask ^ (1 << id), dp));
            }

            // Find the cost of current
            // character and move to next
            // position
            else
            {
                ans = Math.min(ans, a[prev][id] +
                          solve(a, s, n, id,
                                mask ^ (1 << id), dp));
            }
        }
    }

    // Store the answer for each
    // current state
    dp[mask][prev + 1] = ans;
    return ans;
}

// Function that generates any
// permutation of the given
// string with minimum cost
function generatePermutation(mask, n, a,  s)
{

    // Initialize dp table
    var dp = Array.from(Array((1 << n) + 5), ()=> Array(n + 5).fill(-1));

    // Set all the bits of the
    // current character id
    for(var i = 0; i < s.length; i++)
    {
        var id = s[i].charCodeAt(0) - 'a'.charCodeAt(0);
        mask |= (1 << id);
    }

    // Minimum cost of generating
    // the permutation
    document.write( solve(a, s, n, -1, mask, dp) + "<br>");
}

// Driver Code  
var N = 5;
var str = "abcde";
var mat = [ [ 0, 5, 1, 5, 3 ],
                            [ 4, 0, 9, 4, 2 ],
                            [ 7, 9, 0, 10, 7 ],
                            [ 1, 2, 8, 0, 2 ],
                            [ 3, 9, 7, 7, 0 ] ];
// Function Call
generatePermutation(0, N, mat, str);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N*2 <sup>N</sup> )*
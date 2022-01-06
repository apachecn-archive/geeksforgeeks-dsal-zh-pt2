# 使 N 被 25 整除所需的最小给定移动次数

> 原文:[https://www . geeksforgeeks . org/最小给定移动次数-需要使 n 被 25 整除/](https://www.geeksforgeeks.org/minimum-number-of-given-moves-required-to-make-n-divisible-by-25/)

给定一个没有前导零的数字 **N** (1 ≤ N ≤ 10 <sup>18</sup> )。任务是找到**让 N 被 25** 整除所需的最小移动次数。每次移动时，可以交换任意两个相邻的数字，并确保任何时候数字都不能包含任何前导零。如果无法使 N 被 25 整除，则打印 **-1** 。
**举例:**

> **输入:** N = 7560
> **输出:** 1
> 交换(5，6)，N 变成 7650，可被 25 整除
> **输入:** N = 100
> **输出:** 0

**方法:**迭代数字中的所有数字对。让这一对中的第一个数字在位置 I，第二个数字在位置 j，让我们把这些数字放在数字的最后两个位置。但是，现在这个数字可以包含一个前导零。找到最左边的非零数字，并将其移动到第一个位置。然后，如果当前数字可被 25 整除，尝试用交换的数量更新答案。所有这些操作的最小互换次数是必需的答案。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of moves required to make n divisible
// by 25
int minMoves(long long n)
{

    // Convert number into string
    string s = to_string(n);

    // To store required answer
    int ans = INT_MAX;

    // Length of the string
    int len = s.size();

    // To check all possible pairs
    for (int i = 0; i < len; ++i) {
        for (int j = 0; j < len; ++j) {
            if (i == j)
                continue;

            // Make a duplicate string
            string t = s;
            int cur = 0;

            // Number of swaps required to place
            // ith digit in last position
            for (int k = i; k < len - 1; ++k) {
                swap(t[k], t[k + 1]);
                ++cur;
            }

            // Number of swaps required to place
            // jth digit in 2nd last position
            for (int k = j - (j > i); k < len - 2; ++k) {
                swap(t[k], t[k + 1]);
                ++cur;
            }

            // Find first non zero digit
            int pos = -1;
            for (int k = 0; k < len; ++k) {
                if (t[k] != '0') {
                    pos = k;
                    break;
                }
            }

            // Place first non zero digit
            // in the first position
            for (int k = pos; k > 0; --k) {
                swap(t[k], t[k - 1]);
                ++cur;
            }

            // Convert string to number
            long long nn = atoll(t.c_str());

            // If this number is divisible by 25
            // then cur is one of the possible answer
            if (nn % 25 == 0)
                ans = min(ans, cur);
        }
    }

    // If not possible
    if (ans == INT_MAX)
        return -1;

    return ans;
}

// Driver code
int main()
{
    long long n = 509201;
    cout << minMoves(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the minimum number
    // of moves required to make n divisible
    // by 25
    static int minMoves(int n)
    {

        // Convert number into string
        String s = Integer.toString(n);

        // To store required answer
        int ans = Integer.MAX_VALUE;

        // Length of the string
        int len = s.length();

        // To check all possible pairs
        for (int i = 0; i < len; ++i)
        {
            for (int j = 0; j < len; ++j)
            {
                if (i == j)
                    continue;

                // Make a duplicate string
                char t [] = s.toCharArray();
                int cur = 0;

                // Number of swaps required to place
                // ith digit in last position
                for (int k = i; k < len - 1; ++k)
                {
                    swap(t, k, k + 1);
                    ++cur;
                }

                // Number of swaps required to place
                // jth digit in 2nd last position
                for (int k = j - ((j > i)? 1 : 0 ); k < len - 2; ++k)
                {
                    swap(t, k, k + 1);
                    ++cur;
                }

                // Find first non zero digit
                int pos = -1;
                for (int k = 0; k < len; ++k)
                {
                    if (t[k] != '0')
                    {
                        pos = k;
                        break;
                    }
                }

                // Place first non zero digit
                // in the first position
                for (int k = pos; k > 0; --k)
                {
                    swap(t, k, k - 1);
                    ++cur;
                }

                // Convert string to number
                long nn = Integer.parseInt(String.valueOf(t));

                // If this number is divisible by 25
                // then cur is one of the possible answer
                if (nn % 25 == 0)
                    ans = Math.min(ans, cur);
            }
        }

        // If not possible
        if (ans == Integer.MAX_VALUE)
            return -1;

        return ans;
    }

    static void swap(char t [], int i, int j)
    {
        char temp = t[i];
        t[i] = t[j];
        t[j] = temp;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 509201;
        System.out.println(minMoves(n));
    }
}

// This code is contributed by Archana_Kumari
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the minimum number
# of moves required to make n divisible
# by 25
def minMoves(n):

    # Convert number into string
    s = str(n);

    # To store required answer
    ans = sys.maxsize;

    # Length of the string
    len1 = len(s);

    # To check all possible pairs
    for i in range(len1):
        for j in range(len1):
            if (i == j):
                continue;

            # Make a duplicate string
            t = s;
            cur = 0;

            # Number of swaps required to place
            # ith digit in last position
            list1 = list(t);
            for k in range(i,len1 - 1):
                e = list1[k];
                list1[k] = list1[k + 1];
                list1[k + 1] = e;
                cur += 1;
            t = ''.join(list1);

            # Number of swaps required to place
            # jth digit in 2nd last position
            list1 = list(t);
            for k in range(j - (j > i),len1 - 2):
                e = list1[k];
                list1[k] = list1[k + 1];
                list1[k + 1] = e;
                cur += 1;
            t = ''.join(list1);

            # Find first non zero digit
            pos = -1;
            for k in range(len1):
                if (t[k] != '0'):
                    pos = k;
                    break;

            # Place first non zero digit
            # in the first position
            for k in range(pos,0,-1):
                e = list1[k];
                list1[k] = list1[k + 1];
                list1[k + 1] = e;
                cur += 1;
            t = ''.join(list1);

            # Convert string to number
            nn = int(t);

            # If this number is divisible by 25
            # then cur is one of the possible answer
            if (nn % 25 == 0):
                ans = min(ans, cur);

    # If not possible
    if (ans == sys.maxsize):
        return -1;

    return ans;

# Driver code
n = 509201;
print(minMoves(n));

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum number
    // of moves required to make n divisible
    // by 25
    static int minMoves(int n)
    {

        // Convert number into string
        string s = n.ToString();

        // To store required answer
        int ans = Int32.MaxValue;

        // Length of the string
        int len = s.Length;

        // To check all possible pairs
        for (int i = 0; i < len; ++i)
        {
            for (int j = 0; j < len; ++j)
            {
                if (i == j)
                    continue;

                // Make a duplicate string
                char[] t = s.ToCharArray();
                int cur = 0;

                // Number of swaps required to place
                // ith digit in last position
                for (int k = i; k < len - 1; ++k)
                {
                    swap(t, k, k + 1);
                    ++cur;
                }

                // Number of swaps required to place
                // jth digit in 2nd last position
                for (int k = j - ((j > i)? 1 : 0 ); k < len - 2; ++k)
                {
                    swap(t, k, k + 1);
                    ++cur;
                }

                // Find first non zero digit
                int pos = -1;
                for (int k = 0; k < len; ++k)
                {
                    if (t[k] != '0')
                    {
                        pos = k;
                        break;
                    }
                }

                // Place first non zero digit
                // in the first position
                for (int k = pos; k > 0; --k)
                {
                    swap(t, k, k - 1);
                    ++cur;
                }

                // Convert string to number
                int nn = Convert.ToInt32(new String(t));

                // If this number is divisible by 25
                // then cur is one of the possible answer
                if (nn % 25 == 0)
                    ans = Math.Min(ans, cur);
            }
        }

        // If not possible
        if (ans == Int32.MaxValue)
            return -1;

        return ans;
    }

    static void swap(char []t, int i, int j)
    {
        char temp = t[i];
        t[i] = t[j];
        t[j] = temp;
    }

    // Driver code
    static void Main()
    {
        int n = 509201;
        Console.WriteLine(minMoves(n));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum number
// of moves required to make n divisible
// by 25
function minMoves($n)
{

    // Convert number into string
    $s = strval($n);

    // To store required answer
    $ans = PHP_INT_MAX;

    // Length of the string
    $len = strlen($s);

    // To check all possible pairs
    for ($i = 0; $i < $len; ++$i)
    {
        for ($j = 0; $j < $len; ++$j)
        {
            if ($i == $j)
                continue;

            // Make a duplicate string
            $t = $s;
            $cur = 0;

            // Number of swaps required to place
            // ith digit in last position
            for ($k = $i;$k < $len - 1; ++$k)
            {
                $e=$t[$k];
                $t[$k]=$t[$k + 1];
                $t[$k+1]=$e;
                ++$cur;
            }

            // Number of swaps required to place
            // jth digit in 2nd last position
            for ($k = $j - ($j > $i);
                 $k < $len - 2; ++$k)
            {
                $e = $t[$k];
                $t[$k] = $t[$k + 1];
                $t[$k + 1] = $e;
                ++$cur;
            }

            // Find first non zero digit
            $pos = -1;
            for ($k = 0; $k < $len; ++$k)
            {
                if ($t[$k] != '0')
                {
                    $pos = $k;
                    break;
                }
            }

            // Place first non zero digit
            // in the first position
            for ($k = $pos; $k > 0; --$k)
            {
                $e = $t[$k];
                $t[$k] = $t[$k + 1];
                $t[$k + 1] = $e;
                ++$cur;
            }

            // Convert string to number
            $nn = intval($t);

            // If this number is divisible by 25
            // then cur is one of the possible answer
            if ($nn % 25 == 0)
                $ans = min($ans, $cur);
        }
    }

    // If not possible
    if ($ans == PHP_INT_MAX)
        return -1;

    return $ans;
}

// Driver code
$n = 509201;
echo minMoves($n);

// This code is contributed
// by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum number
    // of moves required to make n divisible
    // by 25
    function minMoves(n)
    {

        // Convert number into string
        let s = n.toString();

        // To store required answer
        let ans = Number.MAX_VALUE;

        // Length of the string
        let len = s.length;

        // To check all possible pairs
        for (let i = 0; i < len; ++i)
        {
            for (let j = 0; j < len; ++j)
            {
                if (i == j)
                    continue;

                // Make a duplicate string
                let t = s.split('');
                let cur = 0;

                // Number of swaps required to place
                // ith digit in last position
                for (let k = i; k < len - 1; ++k)
                {
                    swap(t, k, k + 1);
                    ++cur;
                }

                // Number of swaps required to place
                // jth digit in 2nd last position
                for (let k = j - ((j > i)? 1 : 0 ); k < len - 2; ++k)
                {
                    swap(t, k, k + 1);
                    ++cur;
                }

                // Find first non zero digit
                let pos = -1;
                for (let k = 0; k < len; ++k)
                {
                    if (t[k] != '0')
                    {
                        pos = k;
                        break;
                    }
                }

                // Place first non zero digit
                // in the first position
                for (let k = pos; k > 0; --k)
                {
                    swap(t, k, k - 1);
                    ++cur;
                }

                // Convert string to number
                let nn = parseInt(t.join(""));

                // If this number is divisible by 25
                // then cur is one of the possible answer
                if (nn % 25 == 0)
                    ans = Math.min(ans, cur);
            }
        }

        // If not possible
        if (ans == Number.MAX_VALUE)
            return -1;

        return ans;
    }

    function swap(t, i, j)
    {
        let temp = t[i];
        t[i] = t[j];
        t[j] = temp;
    }

    let n = 509201;
      document.write(minMoves(n));

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
4
```
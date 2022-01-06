# 二进制字符串中最多一次交换的最长连续 1 的长度

> 原文:[https://www . geesforgeks . org/二进制字符串中最多一个替换的最长连续长度/](https://www.geeksforgeeks.org/length-of-longest-consecutive-ones-by-at-most-one-swap-in-a-binary-string/)

给定长度为![N   ](img/f989322861c562053413d20a4adaecdf.png "Rendered by QuickLaTeX.com")的二进制字符串。允许在 0 和 1 之间最多进行一次交换。任务是找到可以实现的最长连续 1 的长度。
**例:**

```
Input : str = "111011101"
Output : 7 
We can swap 0 at 4th with 1 at 10th position

Input : str = "111000"
Output : 3 
We cannot obtain more than 3 1's after 
```

**接近** :

1.  在一个变量中计算数组中所有的 1，比如 *cnt_one* 。
2.  保持两个向量或数组从左到右存储累积的向量或数组。
3.  每当出现 0:
    *   如果(**左[i-1] +右[i+1] < cnt_one** )存储 **max_count =左[I-1]+右[i+1] + 1** ，通过交换，我们将获得一个额外的 1 来代替 0。
    *   else **max_count =左[i-1] +右[i+1]** 。
4.  输出是可以达到的 max_count 的最大值。

以下是上述方法的实现:

## C++

```
// C++ program to find length of longest consecutive
// ones by at most one swap in a Binary String

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the length of the
// longest consecutive 1's
int maximum_one(string s, int n)
{
    // To count all 1's in the string
    int cnt_one = 0;

    int max_cnt = 0, temp = 0;

    for (int i = 0; i < n; i++) {
        if (s[i] == '1') {
            cnt_one++;
            temp++;
        }
        else {
            max_cnt = max(temp, max_cnt);
            temp = 0;
        }
    }

    max_cnt = max(max_cnt, temp);

    // To store cumulative 1's
    int left[n], right[n];

    if (s[0] == '1')
        left[0] = 1;
    else
        left[0] = 0;

    if (s[n - 1] == '1')
        right[n - 1] = 1;
    else
        right[n - 1] = 0;

    // Counting cumulative 1's from left
    for (int i = 1; i < n; i++) {
        if (s[i] == '1')
            left[i] = left[i - 1] + 1;

        // If 0 then start new cumulative
        // one from that i
        else
            left[i] = 0;
    }

    for (int i = n - 2; i >= 0; i--) {
        if (s[i] == '1')
            right[i] = right[i + 1] + 1;

        else
            right[i] = 0;
    }

    for (int i = 1; i < n - 1; i++) {
        // perform step 3 of the approach
        if (s[i] == '0') {

            // step 3
            int sum = left[i - 1] + right[i + 1];

            if (sum < cnt_one)
                max_cnt = max(max_cnt, sum + 1);

            else
                max_cnt = max(max_cnt, sum);
        }
    }

    return max_cnt;
}

// Driver Code
int main()
{
    // string
    string s = "111011101";

    cout << maximum_one(s, s.length());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find length of longest consecutive
// ones by at most one swap in a Binary String

import java.io.*;

class GFG {

    // Function to calculate the length of the
    // longest consecutive 1's
    static int maximum_one(String s, int n)
    {
        // To count all 1's in the string
        int cnt_one = 0;

        int max_cnt = 0, temp = 0;

        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == '1') {
                cnt_one++;
                temp++;
            }
            else {
                max_cnt = Math.max(max_cnt, temp);
                temp = 0;
            }
        }
        max_cnt = Math.max(max_cnt, temp);

        // To store cumulative 1's
        int[] left = new int[n];
        int right[] = new int[n];

        if (s.charAt(0) == '1')
            left[0] = 1;
        else
            left[0] = 0;

        if (s.charAt(n - 1) == '1')
            right[n - 1] = 1;
        else
            right[n - 1] = 0;

        // Counting cumulative 1's from left
        for (int i = 1; i < n; i++) {
            if (s.charAt(i) == '1')
                left[i] = left[i - 1] + 1;

            // If 0 then start new cumulative
            // one from that i
            else
                left[i] = 0;
        }

        for (int i = n - 2; i >= 0; i--) {
            if (s.charAt(i) == '1')
                right[i] = right[i + 1] + 1;

            else
                right[i] = 0;
        }

        for (int i = 1; i < n - 1; i++) {
            // perform step 3 of the approach
            if (s.charAt(i) == '0') {

                // step 3
                int sum = left[i - 1] + right[i + 1];

                if (sum < cnt_one)
                    max_cnt = Math.max(max_cnt, sum + 1);

                else
                    max_cnt = Math.max(max_cnt, sum);
            }
        }

        return max_cnt;
    }

    // Driver Code

    public static void main(String[] args)
    {
        // string
        String s = "111011101";

        System.out.println(maximum_one(s, s.length()));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to find length of
# longest consecutive ones by at most
# one swap in a Binary String

# Function to calculate the length
# of the longest consecutive 1's

def maximum_one(s, n):

    # To count all 1's in the string
    cnt_one = 0

    cnt, max_cnt = 0, 0

    for i in range(n):
        if (s[i] == '1'):
            cnt_one += 1
            cnt += 1
        else:
            max_cnt = max(max_cnt, cnt)
            cnt = 0

    max_cnt = max(max_cnt, cnt)

    # To store cumulative 1's
    left = [0] * n
    right = [0] * n

    if (s[0] == '1'):
        left[0] = 1

    else:
        left[0] = 0

    if (s[n - 1] == '1'):
        right[n - 1] = 1

    else:
        right[n - 1] = 0

    # Counting cumulative 1's from left
    for i in range(1, n):
        if (s[i] == '1'):
            left[i] = left[i - 1] + 1

        # If 0 then start new cumulative
        # one from that i
        else:
            left[i] = 0

    for i in range(n - 2, -1, -1):

        if (s[i] == '1'):
            right[i] = right[i + 1] + 1

        else:
            right[i] = 0

    for i in range(1, n-1):

        # perform step 3 of the approach
        if (s[i] == '0'):

            # step 3
            sum = left[i - 1] + right[i + 1]

            if (sum < cnt_one):
                max_cnt = max(max_cnt, sum+1)

            else:
                max_cnt = max(max_cnt, sum)

    return max_cnt

# Driver Code
if __name__ == "__main__":

    # string
    s = "111011101"

    print(maximum_one(s, len(s)))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find length of longest consecutive
// ones by at most one swap in a Binary String
using System;

class GFG {

    // Function to calculate the length of the
    // longest consecutive 1's
    static int maximum_one(string s, int n)
    {
        // To count all 1's in the string
        int cnt_one = 0;

        for (int i = 0; i < n; i++) {
            if (s[i] == '1')
                cnt_one++;
        }

        // To store cumulative 1's
        int[] left = new int[n];
        int[] right = new int[n];

        if (s[0] == '1')
            left[0] = 1;
        else
            left[0] = 0;

        if (s[n - 1] == '1')
            right[n - 1] = 1;
        else
            right[n - 1] = 0;

        // Counting cumulative 1's from left
        for (int i = 1; i < n; i++) {
            if (s[i] == '1')
                left[i] = left[i - 1] + 1;

            // If 0 then start new cumulative
            // one from that i
            else
                left[i] = 0;
        }

        for (int i = n - 2; i >= 0; i--) {
            if (s[i] == '1')
                right[i] = right[i + 1] + 1;

            else
                right[i] = 0;
        }

        int cnt = 0, max_cnt = 0;

        for (int i = 1; i < n - 1; i++) {
            // perform step 3 of the approach
            if (s[i] == '0') {

                // step 3
                int sum = left[i - 1] + right[i + 1];

                if (sum < cnt_one)
                    cnt = sum + 1;

                else
                    cnt = sum;

                max_cnt = Math.Max(max_cnt, cnt);
                cnt = 0;
            }
        }

        return max_cnt;
    }

    // Driver Code

    public static void Main()
    {
        // string
        string s = "111011101";

        Console.WriteLine(maximum_one(s, s.Length));
    }
}
// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of longest
// consecutive ones by at most one swap
// in a Binary String

// Function to calculate the length
// of the longest consecutive 1's
function maximum_one($s, $n)
{
    // To count all 1's in the string
    $cnt_one = 0;

    for ($i = 0; $i < $n; $i++)
    {
        if ($s[$i] == '1')
            $cnt_one++;
    }

    // To store cumulative 1's
    // $left[$n]; $right[$n];
    if ($s[0] == '1')
        $left[0] = 1;
    else
        $left[0] = 0;

    if ($s[$n - 1] == '1')
        $right[$n - 1] = 1;
    else
        $right[$n - 1] = 0;

    // Counting cumulative 1's from left
    for ($i = 1; $i < $n; $i++)
    {
        if ($s[$i] == '1')
            $left[$i] = $left[$i - 1] + 1;

        // If 0 then start new cumulative
        // one from that i
        else
            $left[$i] = 0;
    }

    for ($i = $n - 2; $i >= 0; $i--)
    {
        if ($s[$i] == '1')
            $right[$i] = $right[$i + 1] + 1;

        else
            $right[$i] = 0;
    }

    $cnt = 0; $max_cnt = 0;

    for ($i = 1; $i < $n - 1; $i++)
    {
        // perform step 3 of the approach
        if ($s[$i] == '0')
        {

            // step 3
            $sum = $left[$i - 1] + $right[$i + 1];

            if ($sum < $cnt_one)
                $cnt = $sum + 1;

            else
                $cnt = $sum;

            $max_cnt = max($max_cnt, $cnt);
            $cnt = 0;
        }
    }
    return $max_cnt;
}

// Driver Code

// string
$s = "111011101";

echo maximum_one($s, strlen($s));

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find length of longest consecutive
// ones by at most one swap in a Binary String

// Function to calculate the length of the
// longest consecutive 1's
function maximum_one(s, n)
{
    // To count all 1's in the string
    var cnt_one = 0;

    var max_cnt = 0, temp=0;

    for (var i = 0; i < n; i++)
    {
        if (s[i] == '1')
        {
            cnt_one++;
            temp++;
        }
        else
        {
            max_cnt = Math.max(temp,max_cnt);
            temp=0;
        }
    }

    max_cnt = Math.max(max_cnt, temp);

    // To store cumulative 1's
    var left = Array(n);
    var right = Array(n);

    if (s[0] == '1')
        left[0] = 1;
    else
        left[0] = 0;

    if (s[n - 1] == '1')
        right[n - 1] = 1;
    else
        right[n - 1] = 0;

    // Counting cumulative 1's from left
    for (var i = 1; i < n; i++) {
        if (s[i] == '1')
            left[i] = left[i - 1] + 1;

        // If 0 then start new cumulative
        // one from that i
        else
            left[i] = 0;
    }

    for (var i = n - 2; i >= 0; i--) {
        if (s[i] == '1')
            right[i] = right[i + 1] + 1;

        else
            right[i] = 0;
    }

    for (var i = 1; i < n - 1; i++) {
        // perform step 3 of the approach
        if (s[i] == '0') {

            // step 3
            var sum = left[i - 1] + right[i + 1];

            if (sum < cnt_one)
                max_cnt = Math.max(max_cnt, sum+1);

            else
                max_cnt = Math.max(max_cnt, sum);

        }
    }

    return max_cnt;
}

// Driver Code
// string
var s = "111011101";
document.write( maximum_one(s, s.length));

</script>
```

**Output:** 

```
7
```

**时间复杂度** : O(N)
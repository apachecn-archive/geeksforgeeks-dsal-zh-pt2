# 最长子阵列，最大值和最小值之差最多为 1

> 原文:[https://www . geeksforgeeks . org/最长子阵列最大和最小差值最多为 1/](https://www.geeksforgeeks.org/longest-subarray-such-that-the-difference-of-max-and-min-is-at-most-one/)

给定一个 n 个数字的数组，其中每个数字与前一个数字之间的差值不超过 1。找到最长的连续子阵列，使范围内的最大值和最小值之差不超过 1。

**例:**

```
Input : {3, 3, 4, 4, 5, 6}
Output : 4
The longest subarray here is {3, 3, 4, 4}

Input : {7, 7, 7}
Output : 3
The longest subarray here is {7, 7, 7}

Input : {9, 8, 8, 9, 9, 10}
Output : 5
The longest subarray here is {9, 8, 8, 9, 9}
```

如果序列中最大值和最小值之间的差值不超过 1，则序列仅由一个或两个连续的数字组成。其思想是遍历数组并跟踪当前子数组中的当前元素和前一个元素。如果我们发现一个元素与当前元素或先前元素不同，我们就更新当前元素和先前元素。如果需要，我们还会更新结果。

## C++

```
// C++ code to find longest
// subarray with difference
// between max and min as at-most 1.
#include<bits/stdc++.h>
using namespace std;

int longestSubarray(int input[], 
                    int length)
{
    int prev = -1;
    int current, next;
    int prevCount = 0, currentCount = 1;

    // longest constant range length
    int longest = 1;

    // first number
    current = input[0];

    for (int i = 1; i < length; i++)
    {
        next = input[i];

        // If we see same number
        if (next == current) 
        {
            currentCount++;
        }

        // If we see different number, 
        // but same as previous.
        else if (next == prev)
        {
            prevCount += currentCount;
            prev = current;
            current = next;
            currentCount = 1;
        }

        // If number is neither same 
        // as previous nor as current. 
        else 
        {
            longest = max(longest, 
                          currentCount + prevCount);
            prev = current;
            prevCount = currentCount;
            current = next;
            currentCount = 1;
        }
    }

    return max(longest, 
               currentCount + prevCount);
}

// Driver Code
int main()
{
    int input[] = { 5, 5, 6, 7, 6 }; 
    int n = sizeof(input) / sizeof(int);
    cout << longestSubarray(input, n);
    return 0;
}

// This code is contributed
// by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find longest subarray with difference
// between max and min as at-most 1.
public class Demo {

    public static int longestSubarray(int[] input)
    {
        int prev = -1;
        int current, next;
        int prevCount = 0, currentCount = 1;

        // longest constant range length
        int longest = 1;

        // first number
        current = input[0];

        for (int i = 1; i < input.length; i++) {
            next = input[i];

            // If we see same number
            if (next == current) {
                currentCount++;
            }

            // If we see different number, but
            // same as previous.
            else if (next == prev) {
                prevCount += currentCount;
                prev = current;
                current = next;
                currentCount = 1;
            }

            // If number is neither same as previous
            // nor as current. 
            else {
                longest = Math.max(longest, currentCount + prevCount);
                prev = current;
                prevCount = currentCount;
                current = next;
                currentCount = 1;
            }
        }

        return Math.max(longest, currentCount + prevCount);
    }

    public static void main(String[] args)
    {
        int[] input = { 5, 5, 6, 7, 6 };
        System.out.println(longestSubarray(input));
    }
}
```

## 蟒蛇 3

```
# Python 3 code to find longest
# subarray with difference
# between max and min as at-most 1.
def longestSubarray(input, length):

    prev = -1
    prevCount = 0
    currentCount = 1

    # longest constant range length
    longest = 1

    # first number
    current = input[0]

    for i in range(1, length):

        next = input[i]

        # If we see same number
        if next == current :
            currentCount += 1

        # If we see different number, 
        # but same as previous.
        elif next == prev :
            prevCount += currentCount
            prev = current
            current = next
            currentCount = 1

        # If number is neither same 
        # as previous nor as current. 
        else:
            longest = max(longest, 
                          currentCount + 
                          prevCount)
            prev = current
            prevCount = currentCount
            current = next
            currentCount = 1

    return max(longest, 
            currentCount + prevCount)

# Driver Code
if __name__ == "__main__":
    input = [ 5, 5, 6, 7, 6 ]
    n = len(input)
    print(longestSubarray(input, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to find longest 
// subarray with difference 
// between max and min as 
// at-most 1.
using System;

class GFG
{
public static int longestSubarray(int[] input)
{
    int prev = -1;
    int current, next;
    int prevCount = 0, 
        currentCount = 1;

    // longest constant 
    // range length
    int longest = 1;

    // first number
    current = input[0];

    for (int i = 1; 
             i < input.Length; i++)
    {
        next = input[i];

        // If we see same number
        if (next == current) 
        {
            currentCount++;
        }

        // If we see different number, 
        // but same as previous.
        else if (next == prev) 
        {
            prevCount += currentCount;
            prev = current;
            current = next;
            currentCount = 1;
        }

        // If number is neither 
        // same as previous
        // nor as current. 
        else 
        {
            longest = Math.Max(longest, 
                               currentCount + 
                               prevCount);
            prev = current;
            prevCount = currentCount;
            current = next;
            currentCount = 1;
        }
    }

    return Math.Max(longest, 
                    currentCount + prevCount);
}

// Driver Code
public static void Main(String[] args)
{
    int[] input = {5, 5, 6, 7, 6};
    Console.WriteLine(longestSubarray(input));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find longest subarray 
// with difference between max and 
// min as at-most 1.
function longestSubarray($input, $length)
{
    $prev = -1;
    $prevCount = 0; 
    $currentCount = 1;

    // longest constant range length
    $longest = 1;

    // first number
    $current = $input[0];

    for ($i = 1; $i < $length; $i++) 
    {
        $next = $input[$i];

        // If we see same number
        if ($next == $current) 
        {
            $currentCount++;
        }

        // If we see different number, 
        // but same as previous.
        else if ($next == $prev)
        {
            $prevCount += $currentCount;
            $prev = $current;
            $current = $next;
            $currentCount = 1;
        }

        // If number is neither same 
        // as previous nor as current. 
        else 
        {
            $longest = max($longest, 
                           $currentCount + 
                           $prevCount);
            $prev = $current;
            $prevCount = $currentCount;
            $current = $next;
            $currentCount = 1;
        }
    }

    return max($longest,
               $currentCount + $prevCount);
}

// Driver Code
$input = array( 5, 5, 6, 7, 6 );
echo(longestSubarray($input, count($input)));

// This code is contributed 
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>

// Javascript code to find longest
// subarray with difference
// between max and min as at-most 1.

    function longestSubarray(input)
    {
        let prev = -1;
        let current, next;
        let prevCount = 0, currentCount = 1;

        // longest constant range length
        let longest = 1;

        // first number
        current = input[0];

        for (let i = 1; i < input.length; i++) {
            next = input[i];

            // If we see same number
            if (next == current) {
                currentCount++;
            }

            // If we see different number, but
            // same as previous.
            else if (next == prev) {
                prevCount += currentCount;
                prev = current;
                current = next;
                currentCount = 1;
            }

            // If number is neither same as previous
            // nor as current. 
            else {
                longest = Math.max(longest, 
                currentCount + prevCount);
                prev = current;
                prevCount = currentCount;
                current = next;
                currentCount = 1;
            }
        }

        return Math.max(longest, 
        currentCount + prevCount);
    }

    let input=[5, 5, 6, 7, 6];
    document.write(longestSubarray(input));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)，其中 n 为输入数组的长度。
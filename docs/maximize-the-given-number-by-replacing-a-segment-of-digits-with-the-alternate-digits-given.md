# 通过用给定的备用数字替换一段数字来最大化给定的数字

> 原文:[https://www . geesforgeks . org/通过用给定的备用数字替换一段数字来最大化给定的数字/](https://www.geeksforgeeks.org/maximize-the-given-number-by-replacing-a-segment-of-digits-with-the-alternate-digits-given/)

给定许多 **N** 位数。我们还获得了 **10** 号码，代表从 **0** 到 **9** 的所有一位数号码的备用号码。我们可以用给定的替换数字替换 **N** 中的任何数字，但是我们只允许替换任何连续的数字段一次，任务是替换任何连续的数字段，使得获得的数字是所有可能替换中最大的。

**示例:**

> **输入:** n = 1337，a[] = {0，1，2，5，4，6，6，3，1，9}
> **输出:** 1557
> 1 可以替换为 1 作为 a[1] = 1(无效果)
> 3 可以替换为 5
> 7 可以替换为 3(如果需要最大化数量则不需要)
> **输入:**数量= 1111，a

**方法:**由于我们需要得到最大可能的数，因此从左边迭代，找到替代数大于当前数的数，并不断替换即将到来的数，直到替代数不小。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized number
string get_maximum(string s, int a[])
{
    int n = s.size();

    // Iterate till the end of the string
    for (int i = 0; i < n; i++) {

        // Check if it is greater or not
        if (s[i] - '0' < a[s[i] - '0']) {
            int j = i;

            // Replace with the alternate till smaller
            while (j < n && (s[j] - '0' <= a[s[j] - '0'])) {
                s[j] = '0' + a[s[j] - '0'];
                j++;
            }

            return s;
        }
    }

    // Return original s in case
    // no change took place
    return s;
}

// Driver Code
int main()
{
    string s = "1337";
    int a[] = { 0, 1, 2, 5, 4, 6, 6, 3, 1, 9 };
    cout << get_maximum(s, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximized number
static String get_maximum(char[] s, int a[])
{
    int n = s.length;

    // Iterate till the end of the string
    for (int i = 0; i < n; i++)
    {

        // Check if it is greater or not
        if (s[i] - '0' < a[s[i] - '0'])
        {
            int j = i;

            // Replace with the alternate till smaller
            while (j < n && (s[j] - '0' <= a[s[j] - '0']))
            {
                s[j] = (char) ('0' + a[s[j] - '0']);
                j++;
            }

            return String.valueOf(s);
        }
    }

    // Return original s in case
    // no change took place
    return String.valueOf(s);
}

// Driver Code
public static void main(String[] args)
{
    String s = "1337";
    int a[] = { 0, 1, 2, 5, 4, 6, 6, 3, 1, 9 };
    System.out.println(get_maximum(s.toCharArray(), a));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximized number
def get_maximum(s, a) :
    s = list(s)
    n = len(s)

    # Iterate till the end of the string
    for i in range(n) :

        # Check if it is greater or not
        if (ord(s[i]) - ord('0') < a[ord(s[i]) - ord('0')]) :
            j = i

            # Replace with the alternate till smaller
            while (j < n and (ord(s[j]) - ord('0') <=
                            a[ord(s[j]) - ord('0')])) :
                s[j] = chr(ord('0') + a[ord(s[j]) - ord('0')])
                j += 1

            return "".join(s);

    # Return original s in case
    # no change took place
    return s

# Driver Code
if __name__ == "__main__" :

    s = "1337"
    a = [ 0, 1, 2, 5, 4, 6, 6, 3, 1, 9 ]
    print(get_maximum(s, a))

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximized number
static String get_maximum(char[] s, int[] a)
{
    int n = s.Length;

    // Iterate till the end of the string
    for (int i = 0; i < n; i++)
    {

        // Check if it is greater or not
        if (s[i] - '0' < a[s[i] - '0'])
        {
            int j = i;

            // Replace with the alternate till smaller
            while (j < n && (s[j] - '0' <= a[s[j] - '0']))
            {
                s[j] = (char) ('0' + a[s[j] - '0']);
                j++;
            }

            return String.Join("",s);
        }
    }

    // Return original s in case
    // no change took place
    return String.Join("",s);
}

// Driver Code
public static void Main(String[] args)
{
    String s = "1337";
    int[] a = { 0, 1, 2, 5, 4, 6, 6, 3, 1, 9 };
    Console.WriteLine(get_maximum(s.ToCharArray(), a));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function to return the maximized number

function get_maximum($s, $a)
{
    $n = strlen($s);

    // Iterate till the end of the string
    for ($i = 0; $i < $n; $i++)
    {

        // Check if it is greater or not
        if ($s[$i] - '0' < $a[$s[$i] - '0'])
        {
            $j = $i;

            // Replace with the alternate till smaller
            while ($j < $n && ($s[$j] - '0' <= $a[$s[$j] - '0']))
            {
                $s[$j] = '0' + $a[$s[$j] - '0'];
                $j++;
            }

            return $s;
        }
    }

    // Return original s in case
    // no change took place
    return $s;
}

    // Driver Code
    $s = "1337";
    $a = array( 0, 1, 2, 5, 4, 6, 6, 3, 1, 9 );
    echo get_maximum($s, $a);

    // This Code is contributed is Tushill.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximized number
    function get_maximum(s, a)
    {
        let n = s.length;

        // Iterate till the end of the string
        for (let i = 0; i < n; i++)
        {

            // Check if it is greater or not
            if (s[i].charCodeAt() - '0'.charCodeAt()
            < a[s[i].charCodeAt() - '0'.charCodeAt()])
            {
                let j = i;

                // Replace with the alternate till smaller
                while (j < n && (s[j].charCodeAt() - '0'.charCodeAt()
                <= a[s[j].charCodeAt() - '0'.charCodeAt()]))
                {
                    s[j] = String.fromCharCode('0'.charCodeAt()
                    + a[s[j].charCodeAt() - '0'.charCodeAt()]);
                    j++;
                }

                return s.join("");
            }
        }

        // Return original s in case
        // no change took place
        return s.join("");
    }

    let s = "1337";
    let a = [ 0, 1, 2, 5, 4, 6, 6, 3, 1, 9 ];
    document.write(get_maximum(s.split(''), a));

</script>
```

**Output:** 

```
1557
```
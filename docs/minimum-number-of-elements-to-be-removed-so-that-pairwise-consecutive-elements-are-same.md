# 要移除的元素的最小数量，以便两两连续的元素相同

> 原文:[https://www . geeksforgeeks . org/待移除元素的最小数量，以便成对连续的元素相同/](https://www.geeksforgeeks.org/minimum-number-of-elements-to-be-removed-so-that-pairwise-consecutive-elements-are-same/)

给定一根弦**弦**。任务是计算要移除的元素的最小数量，以便两两连续的元素相同
**示例** :

> **输入** : str = "11344"
> **输出** : 1
> 从第三位去掉数字 3，使字符串变为 1144。因此两两连续的元素是相同的。于是回答是 1。
> **输入** : str = "55553"
> **输出** : 1
> 从第 5 位去掉数字 3，使字符串变为 5555。因此两两连续的元素是相同的。于是回答是 1。

**接近:**检查当前两个连续元素是否相同。如果是，则将索引增加 2，并继续检查，直到遍历完所有元素。否则将索引增加 1，计数增加 1。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number of elements
// to remove from a number so that pairwise two
// consecutive digits are same.
int countConsecutive(string s)
{

    // initialize counting variable
    int count = 0;

    for (int i = 0; i < s.size(); i++) {

        // check if two consecutive digits are same
        if (s[i] == s[i + 1])
            i++;
        else
            count++;
    }

    return count;
}

// Driver code
int main()
{
    string str = "44522255";
    cout << countConsecutive(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG {

// Function to count the minimum number of elements
// to remove from a number so that pairwise two
// consecutive digits are same.
    static int countConsecutive(String s) {

        // initialize counting variable
        int count = 0;

        for (int i = 0; i < s.length(); i++) {

            // check if two consecutive digits are same
            if (s.charAt(i) == s.charAt(i + 1)) {
                i++;
            } else {
                count++;
            }
        }

        return count;
    }

// Driver code
    public static void main(String args[]) {
        String str = "44522255";
        System.out.println(countConsecutive(str));

    }
}

// This code is contributed by PrinciRaj19992
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to count the minimum number of
# elements to remove from a number so that
# pairwise two consecutive digits are same.
def countConsecutive(s):

    # initialize counting variable
    count = -1

    for i in range(len(s)-1):

        # check if two consecutive
        # digits are same
        if(i <= len(s)):
            if (s[i] is s[i + 1]):
                i += 1
            else:
                count += 1
    return count

# Driver code
if __name__ == '__main__':
    str = "44522255"
    print(countConsecutive(str))

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of above approach
using System;
public class GFG {

    // Function to count the minimum number of elements
    // to remove from a number so that pairwise two
    // consecutive digits are same.
    static int countConsecutive(String s) {

        // initialize counting variable
        int count = 0;

        for (int i = 0; i < s.Length; i++) {

            // check if two consecutive digits are same
            if (s[i] == s[i+1]) {
                i++;
            } else {
                count++;
            }
        }

        return count;
    }

// Driver code
    public static void Main() {
        String str = "44522255";
        Console.WriteLine(countConsecutive(str));

    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count the minimum number
// of elements to remove from a number so
// that pairwise two consecutive digits are same.
function countConsecutive($s)
{

    // initialize counting variable
    $count = 0;

    for ($i = 0; $i < strlen($s); $i++)
    {

        // check if two consecutive
        // digits are same
        if ($s[$i] == $s[$i + 1])
            $i++;
        else
            $count++;
    }

    return $count;
}

// Driver code
$str = "44522255";
echo countConsecutive($str);

// This code is contributed by Sachin.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to count the minimum number of elements
// to remove from a number so that pairwise two
// consecutive digits are same.
function countConsecutive(s)
{

    // initialize counting variable
    let count = 0;

    for (let i = 0; i < s.length; i++) {

        // check if two consecutive digits are same
        if (s[i] == s[i + 1])
            i++;
        else
            count++;
    }

    return count;
}

// Driver code
    let str = "44522255";
    document.write(countConsecutive(str));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
2
```
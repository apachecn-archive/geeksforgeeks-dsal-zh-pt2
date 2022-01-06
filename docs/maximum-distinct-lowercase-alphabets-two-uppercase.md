# 两个大写字母之间的最大不同小写字母数

> 原文:[https://www . geesforgeks . org/maximum-distinct-小写-字母-两个-大写/](https://www.geeksforgeeks.org/maximum-distinct-lowercase-alphabets-two-uppercase/)

给定一个包含小写字母和大写字母的字符串，找出两个大写字母之间出现的不同小写字母的最大数量。
**例**:

```
Input : zACaAbbaazzC
Output : The maximum count = 3

Input : edxedxxxCQiIVmYEUtLi
Output : The maximum count = 1
```

**方法 1(使用字符计数数组):**

*   声明一个大小为 26 的数组，其中数组的每个索引代表英语字母表中的一个字符
*   遍历字符串的整个长度
*   对于每个小写字符，将相应数组的索引增加 1。
*   对于每个大写字符，迭代数组并计算值大于零的位置数。
*   如果该计数大于最大计数，更新最大计数器，**将数组初始化为 0** 。

下面是上述方法的实现。

## C++

```
// CPP Program to find maximum
// lowercase alphabets present
// between two uppercase alphabets
#include <bits/stdc++.h>
using namespace std;

#define MAX_CHAR 26

// Function which computes the
// maximum number of distinct
// lowercase alphabets between
// two uppercase alphabets
int maxLower(string str)
{
    int n = str.length();

    // Ignoring lowercase characters in the
    // beginning.
    int i = 0;
    for (; i < n; i++) {
        if (str[i] >= 'A' && str[i] <= 'Z') {
            i++;
            break;
        }
    }

    // We start from next of first capital letter
    // and traverse through remaining character.
    int maxCount = 0;
    int count[MAX_CHAR] = { 0 };
    for (; i < n; i++) {

        // If character is in uppercase,
        if (str[i] >= 'A' && str[i] <= 'Z') {

            // Count all distinct lower case
            // characters
            int currCount = 0;
            for (int j = 0; j < MAX_CHAR; j++)
                if (count[j] > 0)
                    currCount++;

            // Update maximum count
            maxCount = max(maxCount, currCount);

            // Reset count array
            memset(count, 0, sizeof(count));
        }

        // If character is in lowercase
        if (str[i] >= 'a' && str[i] <= 'z')
            count[str[i] - 'a']++;
    }

    return maxCount;
}

// Driver function
int main()
{
    string str = "zACaAbbaazzC";
    cout << maxLower(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find maximum
// lowercase alphabets present
// between two uppercase alphabets
import java.util.Arrays;

class GFG
{

    static final int MAX_CHAR = 26;

    // Function which computes the
    // maximum number of distinct
    // lowercase alphabets between
    // two uppercase alphabets
    static int maxLower(String str)
    {
        int n = str.length();

        // Ignoring lowercase characters in the
        // beginning.
        int i = 0;
        for (; i < n; i++)
        {
            if (str.charAt(i) >= 'A' && str.charAt(i) <= 'Z')
            {
                i++;
                break;
            }
        }

        // We start from next of first capital letter
        // and traverse through remaining character.
        int maxCount = 0;
        int count[] = new int[MAX_CHAR];
        for (; i < n; i++)
        {

            // If character is in uppercase,
            if (str.charAt(i) >= 'A' && str.charAt(i) <= 'Z')
            {

                // Count all distinct lower case
                // characters
                int currCount = 0;
                for (int j = 0; j < MAX_CHAR; j++)
                {
                    if (count[j] > 0)
                    {
                        currCount++;
                    }
                }

                // Update maximum count
                maxCount = Math.max(maxCount, currCount);

                // Reset count array
                Arrays.fill(count, 0);
            }

            // If character is in lowercase
            if (str.charAt(i) >= 'a' && str.charAt(i) <= 'z')
            {
                count[str.charAt(i) - 'a']++;
            }
        }
        return maxCount;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "zACaAbbaazzC";
        System.out.println(maxLower(str));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program to find maximum
# lowercase alphabets present
# between two uppercase alphabets

MAX_CHAR = 26

# Function which computes the
# maximum number of distinct
# lowercase alphabets between
# two uppercase alphabets
def maxLower(str):
    n = len(str)

    # Ignoring lowercase characters
    # in the beginning.
    i = 0
    for i in range(n):
        if str[i] >= 'A' and str[i] <= 'Z':
            i += 1
            break

    # We start from next of first capital
    # letter and traverse through
    # remaining character.
    maxCount = 0
    count = []
    for j in range(MAX_CHAR):
        count.append(0)

    for j in range(i, n):

        # If character is in uppercase,
        if str[j] >= 'A' and str[j] <= 'Z':

            # Count all distinct lower
            # case characters
            currCount = 0
            for k in range(MAX_CHAR):
                if count[k] > 0:
                    currCount += 1

            # Update maximum count
            maxCount = max(maxCount, currCount)

            # Reset count array
            for y in count:
                y = 0

        # If character is in lowercase
        if str[j] >= 'a' and str[j] <= 'z':
            count[ord(str[j]) - ord('a')] += 1

    return maxCount

# Driver function
str = "zACaAbbaazzC";
print(maxLower(str))

# This code is contributed by Upendra Bartwal
```

## C#

```
// C# Program to find maximum
// lowercase alphabets present
// between two uppercase alphabets
using System;
using System.Collections.Generic;            

class GFG
{
    static int MAX_CHAR = 26;

    // Function which computes the
    // maximum number of distinct
    // lowercase alphabets between
    // two uppercase alphabets
    static int maxLower(String str)
    {
        int n = str.Length;

        // Ignoring lowercase characters in the
        // beginning.
        int i = 0;
        for (; i < n; i++)
        {
            if (str[i] >= 'A' && str[i] <= 'Z')
            {
                i++;
                break;
            }
        }

        // We start from next of first capital letter
        // and traverse through remaining character.
        int maxCount = 0;
        int []count = new int[MAX_CHAR];
        for (; i < n; i++)
        {

            // If character is in uppercase,
            if (str[i] >= 'A' && str[i] <= 'Z')
            {

                // Count all distinct lower case
                // characters
                int currCount = 0;
                for (int j = 0; j < MAX_CHAR; j++)
                {
                    if (count[j] > 0)
                    {
                        currCount++;
                    }
                }

                // Update maximum count
                maxCount = Math.Max(maxCount, currCount);

                // Reset count array
                Array.Fill(count, 0);
            }

            // If character is in lowercase
            if (str[i] >= 'a' && str[i] <= 'z')
            {
                count[str[i] - 'a']++;
            }
        }
        return maxCount;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "zACaAbbaazzC";
        Console.WriteLine(maxLower(str));
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find maximum
// lowercase alphabets present
// between two uppercase alphabets
$MAX_CHAR = 26;

// Function which computes the
// maximum number of distinct
// lowercase alphabets between
// two uppercase alphabets
function maxLower($str)
{
    global $MAX_CHAR;
    $n = strlen($str);

    // Ignoring lowercase characters in
    // the beginning.
    $i = 0;
    for (; $i < $n; $i++)
    {
        if ($str[$i] >= 'A' &&
            $str[$i] <= 'Z')
        {
            $i++;
            break;
        }
    }

    // We start from next of first capital letter
    // and traverse through remaining character.
    $maxCount = 0;
    $count = array_fill(0, $MAX_CHAR, NULL);
    for (; $i < $n; $i++)
    {

        // If character is in uppercase,
        if ($str[$i] >= 'A' && $str[$i] <= 'Z')
        {

            // Count all distinct lower case
            // characters
            $currCount = 0;
            for ($j = 0; $j < $MAX_CHAR; $j++)
                if ($count[$j] > 0)
                    $currCount++;

            // Update maximum count
            $maxCount = max($maxCount, $currCount);

            // Reset count array
            $count = array_fill(0, $MAX_CHAR, NULL);
        }

        // If character is in lowercase
        if ($str[$i] >= 'a' && $str[$i] <= 'z')
            $count[ord($str[$i]) - ord('a')]++;
    }

    return $maxCount;
}

// Driver Code
$str = "zACaAbbaazzC";
echo maxLower($str);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript Program to find maximum
// lowercase alphabets present
// between two uppercase alphabets

    let MAX_CHAR = 26;

    // Function which computes the
    // maximum number of distinct
    // lowercase alphabets between
    // two uppercase alphabets
    function maxLower(str)
    {
        let n = str.length;

        // Ignoring lowercase characters in the
        // beginning.
        let i = 0;
        for (; i < n; i++)
        {
            if (str[i] >= 'A' && str[i] <= 'Z')
            {
                i++;
                break;
            }
        }

        // We start from next of first capital letter
        // and traverse through remaining character.
        let maxCount = 0;
        let count = new Array(MAX_CHAR);
        for (; i < n; i++)
        {

            // If character is in uppercase,
            if (str[i] >= 'A' && str[i] <= 'Z')
            {

                // Count all distinct lower case
                // characters
                let currCount = 0;
                for (let j = 0; j < MAX_CHAR; j++)
                {
                    if (count[j] > 0)
                    {
                        currCount++;
                    }
                }

                // Update maximum count
                maxCount = Math.max(maxCount, currCount);

                // Reset count array
                for(let i=0;i<count.length;i++)
                {
                    count[i]=0;
                }
            }

            // If character is in lowercase
            if (str[i] >= 'a' && str[i] <= 'z')
            {
                count[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
            }
        }
        return maxCount;
    }

    // Driver code
    let str = "zACaAbbaazzC";
    document.write(maxLower(str));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
3
```
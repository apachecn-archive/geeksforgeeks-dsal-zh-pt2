# 【ASCII 值小于和大于 k 的字母计数

> 原文:[https://www . geesforgeks . org/字母计数-具有-ascii 值-小于和大于-k/](https://www.geeksforgeeks.org/count-of-alphabets-having-ascii-value-less-than-and-greater-than-k/)

给定一个字符串，任务是计算 ASCII 值小于和大于或等于给定整数 k 的字母数量。

**示例:**

```
Input: str = "GeeksForGeeks", k = 90
Output: 3, 10
G, F, G have ascii values less than 90.
e, e, k, s, o, r, e, e, k, s have ascii values 
greater than or equal to 90

Input: str = "geeksforgeeks", k = 90
Output: 0, 13 
```

**方法:**开始遍历字符串，检查当前字符的 ASCII 值是否小于 k。如果是，则增加计数。
因此，剩余字符的 ASCII 值将大于或等于 k。因此，对于 ASCII 值大于或等于 k 的字符，打印**len _ of _ String–count**
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// characters whose ascii value is less than k
int CountCharacters(string str, int k)
{
    // Initialising the count to 0
    int cnt = 0;

    int len = str.length();
    for (int i = 0; i < len; i++) {
        // Incrementing the count
        // if the value is less
        if (str[i] < k)
            cnt++;
    }

    // return the count
    return cnt;
}

// Driver code
int main()
{
    string str = "GeeksForGeeks";
    int k = 90;

    int count = CountCharacters(str, k);
    cout << "Characters with ASCII values"
            " less than K are "
         << count;

    cout << "\nCharacters with ASCII values"
            " greater than or equal to K are "
         << str.length() - count;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG {

// Function to count the number of
// characters whose ascii value is less than k
static int CountCharacters(String str, int k)
{
    // Initialising the count to 0
    int cnt = 0;

    int len = str.length();
    for (int i = 0; i < len; i++) {
        // Incrementing the count
        // if the value is less
        if (((int)str.charAt(i)) < k)
            cnt++;
    }

    // return the count
    return cnt;
}

// Driver code
public static void main(String args[])
{
    String str = "GeeksForGeeks";
    int k = 90;

    int count = CountCharacters(str, k);
    System.out.println("Characters with ASCII values less than K are "+count);

    System.out.println("Characters with ASCII values greater than or equal to K are "+(str.length() - count));

}
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to count the number of
# characters whose ascii value is
# less than k
def CountCharacters(str, k):

    # Initialising the count to 0
    cnt = 0

    l = len(str)
    for i in range(l):

        # Incrementing the count
        # if the value is less
        if (ord(str[i]) < k):
            cnt += 1

    # return the count
    return cnt

# Driver code
if __name__ == "__main__":

    str = "GeeksForGeeks"
    k = 90

    count = CountCharacters(str, k)
    print ("Characters with ASCII values",
                "less than K are", count)

    print ("Characters with ASCII values",
           "greater than or equal to K are",
                           len(str) - count)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the above approach
using System;
class GFG {

// Function to count the number of
// characters whose ascii value is less than k
static int CountCharacters(String str, int k)
{
    // Initialising the count to 0
    int cnt = 0;

    int len = str.Length;
    for (int i = 0; i < len; i++)
    {
        // Incrementing the count
        // if the value is less
        if (((int)str[i]) < k)
            cnt++;
    }

    // return the count
    return cnt;
}

// Driver code
public static void Main()
{
    String str = "GeeksForGeeks";
    int k = 90;
    int count = CountCharacters(str, k);
    Console.WriteLine("Characters with ASCII values" +
                        "less than K are " + count);

    Console.WriteLine("Characters with ASCII values greater" +
                    "than or equal to K are "+(str.Length - count));
}
}

// This code is contributed by princiraj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count the number of
// characters whose ascii value is less than k
function CountCharacters($str, $k)
{
    // Initialising the count to 0
    $cnt = 0;

    $len = strlen($str);
    for ($i = 0; $i < $len; $i++)
    {
        // Incrementing the count
        // if the value is less
        if ($str[$i] < chr($k))
            $cnt += 1;
    }

    // return the count
    return $cnt;
}

// Driver code
$str = "GeeksForGeeks";
$k = 90;

$count = CountCharacters($str, $k);
echo("Characters with ASCII values" .
       " less than K are " . $count);

echo("\nCharacters with ASCII values" .
     " greater than or equal to K are " .
                (strlen($str) - $count));

// This code contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // Function to count the number of
    // characters whose ascii value is less than k
    function CountCharacters(str,k)
    {
        // Initialising the count to 0
    let cnt = 0;

    let len = str.length;
    for (let i = 0; i < len; i++) {
        // Incrementing the count
        // if the value is less
        if (str[i].charCodeAt(0) < k)
            cnt++;
    }

    // return the count
    return cnt;
    }

    // Driver code
    let str = "GeeksForGeeks";
    let k = 90;
    let count = CountCharacters(str, k);
    document.write("Characters with ASCII values less than K are "+count+"<br>");

    document.write("Characters with ASCII values greater than or equal to K are "+(str.length - count));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Characters with ASCII values less than K are 3
Characters with ASCII values greater than or equal to K are 10
```

**时间复杂度:** O(N)
# 对一个字符串进行最小化的更改，以使所有子字符串都不同

> 原文:[https://www . geesforgeks . org/minimum-changes-to-a-string-make-all-substrings-distinct/](https://www.geeksforgeeks.org/minimum-changes-to-a-string-to-make-all-substrings-distinct/)

给定一个字符串，找到对它的最小更改数，以便该字符串的所有子字符串都变得不同。
**例:**

```
Input :  str = "aab"
Output : 1
If we change one instance of 'a'
to any character from 'c' to 'z',
we get all distinct substrings.

Input : str = "aa"
Output : 1
```

要使所有子字符串都不同，每个字符都必须不同。所以我们只需要计算重复字符的数量。如果字符串长度超过 26，那么我们不能将其转换为包含所有不同子字符串的字符串(这里我们假设字符串应该只包含小写字符，“a”到“z”)

## C++

```
// CPP program to count number of changes
// to make all substrings distinct.
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// Returns minimum changes to str so
// that no substring is repeated.
int minChanges(string &str)
{
    int n = str.length();

    // If length is more than maximum
    // allowed characters, we cannot
    // get the required string.
    if (n > MAX_CHAR)
       return -1;

    // Variable to store count of
    // distinct characters
    int dist_count = 0;

    // To store counts of different
    // characters
    int count[MAX_CHAR] = {0};

    for (int i = 0; i < n; i++) {
        if (count[str[i] - 'a'] == 0)
            dist_count++;
        count[(str[i] - 'a')]++;
    }

    // Answer is, n - number of distinct char
    return (n - dist_count);
}

// Driver function
int main()
{
    string str = "aebaecedabbee";
    cout << minChanges(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to count number of changes
// to make all substrings distinct.
import java.lang.*;
import java.util.*;

class GFG
{
    static final int MAX_CHAR = 26;

    // Returns minimum changes to str so
    // that no substring is repeated.
    public static int minChanges(String str)
    {

        int n = str.length();

        // If length is more than maximum
        // allowed characters, we cannot
        // get the required string.
        if (n > MAX_CHAR)
            return -1;

        // Variable to store count of
        // distinct characters
        int dist_count = 0;
        int count[] = new int[MAX_CHAR];

        // To store counts of different
        // characters
        for(int i = 0; i < MAX_CHAR; i++)
            count[i] = 0;

        for (int i = 0; i < n; i++)
        {
            if(count[str.charAt(i)-'a'] == 0)
                dist_count++;
            count[str.charAt(i)-'a']++;
        }

        // Answer is, n - number of distinct char
        return (n-dist_count);
    }

    //Driver function
    public static void main (String[] args) {

        String str = "aebaecedabbee";

        System.out.println(minChanges(str));
    }
}

/* This code is contributed by Akash Singh*/
```

## 蟒蛇 3

```
# Python3 program to count number of changes
# to make all substrings distinct.

MAX_CHAR = [26]

# Returns minimum changes to str so
# that no substring is repeated.
def minChanges(str):

    n = len(str )

    # If length is more than maximum
    # allowed characters, we cannot
    # get the required string.
    if (n > MAX_CHAR[0]):
        return -1

    # Variable to store count of
    # distinct characters
    dist_count = 0

    # To store counts of different
    # characters
    count = [0] * MAX_CHAR[0]

    for i in range(n):
        if (count[ord(str[i]) - ord('a')] == 0) :
            dist_count += 1
        count[(ord(str[i]) - ord('a'))] += 1

    # Answer is, n - number of distinct char
    return (n - dist_count)

# Driver Code
if __name__ == '__main__':
    str = "aebaecedabbee"
    print(minChanges(str))

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to count number of changes
// to make all substrings distinct.
using System;

class GFG
{
    static int MAX_CHAR = 26;

    // Returns minimum changes to str so
    // that no substring is repeated.
    public static int minChanges(string str)
    {

        int n = str.Length;

        // If length is more than maximum
        // allowed characters, we cannot
        // get the required string.
        if (n > MAX_CHAR)
            return -1;

        // Variable to store count of
        // distinct characters
        int dist_count = 0;
        int []count = new int[MAX_CHAR];

        // To store counts of different
        // characters
        for(int i = 0; i < MAX_CHAR; i++)
            count[i] = 0;

        for (int i = 0; i < n; i++)
        {
            if(count[str[i] - 'a'] == 0)
                dist_count++;
            count[str[i] - 'a']++;
        }

        // Answer is, n - number of distinct char
        return (n - dist_count);
    }

    //Driver function
    public static void Main () {

        string str = "aebaecedabbee";

        Console.WriteLine(minChanges(str));
    }
}

/* This code is contributed by Akash Singh*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of changes
// to make all substrings distinct.

// Returns minimum changes to str so
// that no substring is repeated.
function minChanges($str)
{
    $n = strlen($str);

    // If length is more than maximum
    // allowed characters, we cannot
    // get the required string.
    if ($n > 26)
    return -1;

    // Variable to store count of
    // distinct characters
    $dist_count = 0;

    // To store counts of different
    // characters
    $count = array_fill(0, 26, 0);
    for ($i = 0; $i < $n; $i++)
    {
        if ($count[ord($str[$i]) - 97] == 0)
            $dist_count++;
        $count[ord($str[$i]) -97]++;
    }

    // Answer is, n - number of
    // distinct char
    return ($n - $dist_count);
}

// Driver Code
$str = "aebaecedabbee";
echo minChanges($str);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to count number of changes
// to make all substrings distinct.

   var MAX_CHAR = 26;

    // Returns minimum changes to str so
    // that no substring is repeated.
    function minChanges(str)
    {

        var n = str.length;

        // If length is more than maximum
        // allowed characters, we cannot
        // get the required string.
        if (n > MAX_CHAR)
            return -1;

        // Variable to store count of
        // distinct characters
        var dist_count = 0;
        var count = Array.from({length: MAX_CHAR}, (_, i) => 0);

        // To store counts of different
        // characters
        for(var i = 0; i < MAX_CHAR; i++)
            count[i] = 0;

        for (var i = 0; i < n; i++)
        {
            if(count[str.charAt(i).charCodeAt(0)-'a'.charCodeAt(0)] == 0)
                dist_count++;
            count[str.charAt(i).charCodeAt(0)-'a'.charCodeAt(0)]++;
        }

        // Answer is, n - number of distinct char
        return (n-dist_count);
    }

// Driver function
var str = "aebaecedabbee";

document.write(minChanges(str));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
8
```
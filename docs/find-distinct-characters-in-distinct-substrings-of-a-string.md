# 在字符串的不同子串中找到不同的字符

> 原文:[https://www . geesforgeks . org/find-distinct-characters-in-distinct-substrings-of-a-string/](https://www.geeksforgeeks.org/find-distinct-characters-in-distinct-substrings-of-a-string/)

给定一个字符串 **str** ，任务是找到给定字符串的所有不同子字符串中不同字符的计数。
**例:**

> **输入:**str = " ABCA "
> T3】输出:18
> T6】
> 
> | 不同的子字符串 | 独特的特征 |
> | --- | --- |
> | A | one |
> | AB 型血 | Two |
> | 字母表 | three |
> | ABCA | three |
> | B | one |
> | 公元前 | Two |
> | BCA | three |
> | C | one |
> | 加拿大 | Two |
> 
> 因此，1 + 2 + 3 + 3 + 1 + 2 + 3 + 1 + 2 = 18
> **输入:** str = "AAAB"
> **输出:** 10

**方法:**获取给定字符串的所有可能的子字符串，并使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)检查当前子字符串之前是否已被处理。现在，对于每个不同的子字符串，计算其中的不同字符(同样可以使用 set 来这样做)。所有不同子串的计数之和就是最终答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of distinct
// characters in all the distinct
// sub-strings of the given string
int countTotalDistinct(string str)
{
    int cnt = 0;

    // To store all the sub-strings
    set<string> items;

    for (int i = 0; i < str.length(); ++i) {

        // To store the current sub-string
        string temp = "";

        // To store the characters of the
        // current sub-string
        set<char> ans;
        for (int j = i; j < str.length(); ++j) {
            temp = temp + str[j];
            ans.insert(str[j]);

            // If current sub-string hasn't
            // been stored before
            if (items.find(temp) == items.end()) {

                // Insert it into the set
                items.insert(temp);

                // Update the count of
                // distinct characters
                cnt += ans.size();
            }
        }
    }

    return cnt;
}

// Driver code
int main()
{
    string str = "ABCA";

    cout << countTotalDistinct(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashSet;

class geeks
{

    // Function to return the count of distinct
    // characters in all the distinct
    // sub-strings of the given string
    public static int countTotalDistinct(String str)
    {
        int cnt = 0;

        // To store all the sub-strings
        HashSet<String> items = new HashSet<>();

        for (int i = 0; i < str.length(); ++i)
        {

            // To store the current sub-string
            String temp = "";

            // To store the characters of the
            // current sub-string
            HashSet<Character> ans = new HashSet<>();
            for (int j = i; j < str.length(); ++j)
            {
                temp = temp + str.charAt(j);
                ans.add(str.charAt(j));

                // If current sub-string hasn't
                // been stored before
                if (!items.contains(temp))
                {

                    // Insert it into the set
                    items.add(temp);

                    // Update the count of
                    // distinct characters
                    cnt += ans.size();
                }
            }
        }

        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "ABCA";
        System.out.println(countTotalDistinct(str));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of distinct
# characters in all the distinct
# sub-strings of the given string
def countTotalDistinct(string) :

    cnt = 0;

    # To store all the sub-strings
    items = set();

    for i in range(len(string)) :

        # To store the current sub-string
        temp = "";

        # To store the characters of the
        # current sub-string
        ans = set();
        for j in range(i, len(string)) :
            temp = temp + string[j];
            ans.add(string[j]);

            # If current sub-string hasn't
            # been stored before
            if temp not in items :

                # Insert it into the set
                items.add(temp);

                # Update the count of
                # distinct characters
                cnt += len(ans);

    return cnt;

# Driver code
if __name__ == "__main__" :

    string = "ABCA";

    print(countTotalDistinct(string));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class geeks
{

    // Function to return the count of distinct
    // characters in all the distinct
    // sub-strings of the given string
    public static int countTotalDistinct(String str)
    {
        int cnt = 0;

        // To store all the sub-strings
        HashSet<String> items = new HashSet<String>();

        for (int i = 0; i < str.Length; ++i)
        {

            // To store the current sub-string
            String temp = "";

            // To store the characters of the
            // current sub-string
            HashSet<char> ans = new HashSet<char>();
            for (int j = i; j < str.Length; ++j)
            {
                temp = temp + str[j];
                ans.Add(str[j]);

                // If current sub-string hasn't
                // been stored before
                if (!items.Contains(temp))
                {

                    // Insert it into the set
                    items.Add(temp);

                    // Update the count of
                    // distinct characters
                    cnt += ans.Count;
                }
            }
        }

        return cnt;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "ABCA";
        Console.WriteLine(countTotalDistinct(str));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// js implementation of the approach

// Function to return the count of distinct
// characters in all the distinct
// sub-strings of the given string
function countTotalDistinct(str)
{
    let cnt = 0;

    // To store all the sub-strings
    let items = new Set();

    for (let i = 0; i < str.length; ++i) {

        // To store the current sub-string
        let temp = "";

        // To store the characters of the
        // current sub-string
        let ans = new Set();
        for (let j = i; j < str.length; ++j) {
            temp = temp + str[j];
            ans.add(str[j]);
            // If current sub-string hasn't
            // been stored before
            if (!items.has(temp)) {

                // Insert it into the set
                items.add(temp);

                // Update the count of
                // distinct characters
                cnt += ans.size;
            }
        }
    }

    return cnt;
}

// Driver code
let str = "ABCA";
document.write(countTotalDistinct(str));

</script>
```

**Output:** 

```
18
```

**时间复杂度:** O(n^2)

由于使用了嵌套循环，如果 n^2

**空间复杂度:** O(n)

使用两组大小为 n 的值，因此复杂度将是 O(2n)，而不是 O(n)。
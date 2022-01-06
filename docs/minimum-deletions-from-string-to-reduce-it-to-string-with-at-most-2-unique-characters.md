# 从字符串中删除的最少数量，以将其减少为最多包含 2 个唯一字符的字符串

> 原文:[https://www . geeksforgeeks . org/从字符串到最多 2 个唯一字符的字符串的最小删除数/](https://www.geeksforgeeks.org/minimum-deletions-from-string-to-reduce-it-to-string-with-at-most-2-unique-characters/)

给定一个包含小写英文字母的字符串![S  ](img/286065faa2e31cda66548efbe78a36d1.png "Rendered by QuickLaTeX.com")。任务是找到需要删除的最小字符数，以便剩余的字符串最多包含 2 个唯一字符。
**注意**:最后一个字符串可以有重复的字符。任务只是用最少的删除来减少字符串，这样在结果字符串中最多可以有 2 个唯一的字符。

**示例:**

> **输入:**S = " geeks forgeeks "
> T3】输出: 7
> 去掉 7 个字符后，最后的字符串会是“geegee”
> 
> **输入:**S = " hello world "
> T3】输出: 5

**方法:**首先[统计每个字符](https://www.geeksforgeeks.org/program-count-occurrence-given-character-string/)在给定字符串内的出现次数，然后只选择出现次数最多的两个字符，即字符串中出现次数最多的两个字符。结果会是:

> 字符串长度–(出现第一个最频繁的字符+出现第二个最频繁的字符)

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum deletions
int check(string s)
{

    int i, j;
    // Array to store the occurrences
    // of each characters
    int fr[26] = {0} ;

    // Length of the string
    int n = s.size() ;
    for(i = 0; i < n; i++)
    {

        // ASCII of the character
        char x = s[i] ;

        // Increasing the frequency for this character
        fr[x-'a'] += 1 ;

    }

    int minimum = INT_MAX;

    for(i = 0 ; i < 26; i++)
    {
        for( j = i + 1;j < 26; j++)
        {

            // Choosing two character
            int z = fr[i] + fr[j] ;

            // Finding the minimum deletion
            minimum = min(minimum, n - z) ;
        }
    }

    return minimum ;
}

/* Driver code */
int main()
{
    string s ="geeksforgeeks" ;
    cout << check(s) ;
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class GFG{

// Function to find the minimum deletions
static int check(String s)
{

    int i,j;
    // Array to store the occurrences
    // of each characters
    int fr[] = new int[26] ;

    // Length of the string
    int n = s.length() ;
    for(i = 0; i < n; i++)
    {

        // ASCII of the character
        char x = s.charAt(i) ;

        // Increasing the frequency for this character
        fr[x-'a'] += 1 ;

    }

    int minimum = Integer.MAX_VALUE;

    for(i = 0 ; i < 26; i++)
    {
        for( j = i + 1;j < 26; j++)
        {

            // Choosing two character
            int z = fr[i] + fr[j] ;

            // Finding the minimum deletion
            minimum = Math.min(minimum, n-z) ;
        }
    }

    return minimum ;
}

    /* Driver program to test above functions */
     public static void main(String []args){

        String s ="geeksforgeeks" ;
        System.out.println(check(s)) ;

        }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the minimum deletions
def check(s):

    # Array to store the occurrences
    # of each characters
    fr =[0]*26

    # Length of the string
    n = len(s)
    for i in range(n):

        # ASCII of the character
        x = ord(s[i])

        # Increasing the frequency for this character
        fr[x-97] += 1

    minimum = 99999999999

    for i in range(26):
        for j in range(i + 1, 26):

            # Choosing two character
            z = fr[i] + fr[j]

            # Finding the minimum deletion
            minimum = min(minimum, n-z)

    return minimum

# Driver code
s ="geeksforgeeks"
print(check(s))
```

## C#

```
// C# implementation of the above approach

using System;
public class GFG{

// Function to find the minimum deletions
static int check(string s)
{

    int i,j;
    // Array to store the occurrences
    // of each characters
    int[] fr = new int[26] ;

    // Length of the string
    int n = s.Length ;
    for(i = 0; i < n; i++)
    {

        // ASCII of the character
        char x = s[i] ;

        // Increasing the frequency for this character
        fr[x-'a'] += 1 ;

    }

    int minimum = int.MaxValue;

    for(i = 0 ; i < 26; i++)
    {
        for( j = i + 1;j < 26; j++)
        {

            // Choosing two character
            int z = fr[i] + fr[j] ;

            // Finding the minimum deletion
            minimum = Math.Min(minimum, n-z) ;
        }
    }

    return minimum ;
}

    /* Driver program to test above functions */
     public static void Main(){

        string s ="geeksforgeeks" ;
        Console.Write(check(s)) ;

        }
}
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the minimum deletions
function check(s)
{

    var i, j;
    // Array to store the occurrences
    // of each characters
    var fr = Array(26).fill(0);

    // Length of the string
    var n = s.length ;
    for(i = 0; i < n; i++)
    {

        // ASCII of the character
        var x = s[i] ;

        // Increasing the frequency for this character
        fr[x.charCodeAt(0) -'a'.charCodeAt(0)] += 1 ;

    }

    var minimum = 10000000000;

    for(i = 0 ; i < 26; i++)
    {
        for( j = i + 1;j < 26; j++)
        {

            // Choosing two character
            var z = fr[i] + fr[j] ;

            // Finding the minimum deletion
            minimum = Math.min(minimum, n - z) ;
        }
    }

    return minimum ;
}

/* Driver code */
var s ="geeksforgeeks" ;
document.write( check(s));

</script>
```

**Output:** 

```
7
```

**时间复杂度** : O(N)，其中 N 为给定字符串的长度。
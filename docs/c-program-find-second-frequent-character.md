# 寻找第二个最常见字符的程序

> 原文:[https://www . geesforgeks . org/c-program-find-second-frequency-character/](https://www.geeksforgeeks.org/c-program-find-second-frequent-character/)

给定一个字符串，找出其中第二频繁的字符。预期的时间复杂度是 O(n)，其中 n 是输入字符串的长度。
**例:**

```
Input: str = "aabababa";
Output: Second most frequent character is 'b'

Input: str = "geeksforgeeks";
Output: Second most frequent character is 'g'

Input: str = "geeksquiz";
Output: Second most frequent character is 'g'
The output can also be any other character with 
count 1 like 'z', 'i'.

Input: str = "abcd";
Output: No Second most frequent character
```

一个简单的解决方案是从第一个字符开始，计算它的出现次数，然后是第二个字符，依此类推。在计算这些事件时，请记录最大值和第二个最大值。该解的时间复杂度为 O(n <sup>2</sup> )。
我们可以使用大小等于 256 的计数数组在 O(n)时间内解决这个问题(假设字符以 ASCII 格式存储)。以下是该方法的实施情况。

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define NO_OF_CHARS 256

// CPP function to find the
// second most frequent character
// in a given string 'str'
char getSecondMostFreq(string str)
{
    // count number of occurrences of every character.
    int count[NO_OF_CHARS] = {0}, i;
    for (i = 0; str[i]; i++)
        (count[str[i]])++;

    // Traverse through the count[] and
    // find second highest element.
    int first = 0, second = 0;
    for (i = 0; i < NO_OF_CHARS; i++)
    {
        /* If current element is smaller
        than first then update both
        first and second */
        if (count[i] > count[first])
        {
            second = first;
            first = i;
        }

        /* If count[i] is in between first
        and second then update second */
        else if (count[i] > count[second] &&
                count[i] != count[first])
            second = i;
    }

    return second;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    char res = getSecondMostFreq(str);
    if (res != '\0')
        cout << "Second most frequent char is " << res;
    else
        cout << "No second most frequent character";
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
#define NO_OF_CHARS 256

// C function to find the second most frequent character
// in a given string 'str'
char getSecondMostFreq(char *str)
{
    // count number of occurrences of every character.
    int count[NO_OF_CHARS] = {0}, i;
    for (i=0; str[i]; i++)
        (count[str[i]])++;

    // Traverse through the count[] and find second highest element.
    int first = 0, second = 0;
    for (i = 0; i < NO_OF_CHARS; i++)
    {
        /* If current element is smaller than first then update both
          first and second */
        if (count[i] > count[first])
        {
            second = first;
            first = i;
        }

        /* If count[i] is in between first and second then update second  */
        else if (count[i] > count[second] &&
                 count[i] != count[first])
            second = i;
    }

    return second;
}

// Driver program to test above function
int main()
{
  char str[] = "geeksforgeeks";
  char res = getSecondMostFreq(str);
  if (res != '\0')
     printf("Second most frequent char is %c", res);
  else
     printf("No second most frequent character");
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the second
// most frequent character in a given string
public class GFG
{
    static final int NO_OF_CHARS = 256;

    // finds the second most frequently occurring
    // char
    static char getSecondMostFreq(String str)
    {
        // count number of occurrences of every
        // character.
        int[] count = new int[NO_OF_CHARS];
        int i;
        for (i=0; i< str.length(); i++)
            (count[str.charAt(i)])++;

        // Traverse through the count[] and find
        // second highest element.
        int first = 0, second = 0;
        for (i = 0; i < NO_OF_CHARS; i++)
        {
            /* If current element is smaller than
            first then update both first and second */
            if (count[i] > count[first])
            {
                second = first;
                first = i;
            }

            /* If count[i] is in between first and
            second then update second  */
            else if (count[i] > count[second] &&
                     count[i] != count[first])
                second = i;
        }

        return (char)second;
    }

    // Driver program to test above function
    public static void main(String args[])
    {
      String str = "geeksforgeeks";
      char res = getSecondMostFreq(str);
      if (res != '\0')
         System.out.println("Second most frequent char"+
                                       " is " + res);
      else
         System.out.println("No second most frequent"+
                                       "character");
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 Program to find the
# second most frequent character
# in a given string

# Function to find the second
# most frequent character
# in a given string 'str'
def getSecondMostFreq(str) :

    NO_OF_CHARS = 256

    # Initialize count list of
    # 256 size with value 0
    count = [0] * NO_OF_CHARS

    # count number of occurrences
    # of every character.
    for i in range(len(str)) :
        count[ord(str[i])] += 1

    first, second = 0, 0

    # Traverse through the count[]
    # and find second highest element.
    for i in range(NO_OF_CHARS) :

        # If current element is smaller
        # than first then update both
        # first and second
        if count[i] > count[first] :

            second = first
            first = i

        # If count[i] is in between
        # first and second
        # then update second */
        elif (count[i] > count[second] and
            count[i] != count[first] ) :

            second = i

    # return character
    return chr(second)

# Driver code
if __name__ == "__main__" :

    str = "geeksforgeeks"

    # function calling
    res = getSecondMostFreq(str)
    if res != '\0' :
        print("Second most frequent char is", res)
    else :
        print("No second most frequent character")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program to find the second most frequent
// character in a given string
using System;

public class GFG {

    static int NO_OF_CHARS = 256;

    // finds the second most frequently
    // occurring char
    static char getSecondMostFreq(string str)
    {

        // count number of occurrences of every
        // character.
        int []count = new int[NO_OF_CHARS];

        for (int i = 0; i < str.Length; i++)
            (count[str[i]])++;

        // Traverse through the count[] and find
        // second highest element.
        int first = 0, second = 0;

        for (int i = 0; i < NO_OF_CHARS; i++)
        {

            /* If current element is smaller
            than first then update both first
            and second */
            if (count[i] > count[first])
            {
                second = first;
                first = i;
            }

            /* If count[i] is in between first
            and second then update second */
            else if (count[i] > count[second] &&
                       count[i] != count[first])
                second = i;
        }

        return (char)second;
    }

    // Driver program to test above function
    public static void Main()
    {
        string str = "geeksforgeeks";
        char res = getSecondMostFreq(str);

        if (res != '\0')
            Console.Write("Second most frequent char"+
                                        " is " + res);
        else
            Console.Write("No second most frequent"+
                                        "character");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
$NO_OF_CHARS=256;

// PHP function to find the
// second most frequent character
// in a given string 'str'
function getSecondMostFreq($str)
{
    global $NO_OF_CHARS;

    // count number of occurrences of every character.
    $count=array_fill(0,$NO_OF_CHARS,0);
    for ($i = 0; $i < strlen($str); $i++)
        $count[ord($str[$i])]++;

    // Traverse through the count[] and
    // find second highest element.
    $first = $second = 0;
    for ($i = 0; $i < $NO_OF_CHARS; $i++)
    {
        /* If current element is smaller
        than first then update both
        first and second */
        if ($count[$i] > $count[$first])
        {
            $second = $first;
            $first = $i;
        }

        /* If count[i] is in between first
        and second then update second */
        else if ($count[$i] > $count[$second] &&
                $count[$i] != $count[$first])
            $second = $i;
    }

    return chr($second);
}

    // Driver code
    $str = "geeksforgeeks";
    $res = getSecondMostFreq($str);
    if (strlen($res))
        echo "Second most frequent char is ".$res;
    else
        echo "No second most frequent character";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // JavaScript Program to find
    // the second most frequent
    // character in a given string

    let NO_OF_CHARS = 256;

    // finds the second most frequently
    // occurring char
    function getSecondMostFreq(str)
    {

        // count number of occurrences of every
        // character.
        let count = new Array(NO_OF_CHARS);
        count.fill(0);

        for (let i = 0; i < str.length; i++)
            (count[str[i].charCodeAt()])++;

        // Traverse through the count[] and find
        // second highest element.
        let first = 0, second = 0;

        for (let i = 0; i < NO_OF_CHARS; i++)
        {

            /* If current element is smaller
            than first then update both first
            and second */
            if (count[i] > count[first])
            {
                second = first;
                first = i;
            }

            /* If count[i] is in between first
            and second then update second */
            else if (count[i] > count[second] &&
                       count[i] != count[first])
                second = i;
        }

        return String.fromCharCode(second);
    }

    let str = "geeksforgeeks";
    let res = getSecondMostFreq(str);

    if (res != '\0')
      document.write("Second most frequent char"+
                    " is " + res);
    else
      document.write("No second most frequent"+
                    "character");

</script>
```

**输出:**

```
Second most frequent char is g
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息
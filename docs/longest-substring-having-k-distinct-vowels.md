# 具有 K 个不同元音的最长子串

> 原文:[https://www . geesforgeks . org/最长-substring-having-k-distinct-元音/](https://www.geeksforgeeks.org/longest-substring-having-k-distinct-vowels/)

给定一个字符串 s，我们必须找到包含 K 个不同元音的最长子串 s 的长度。
注意:将大写和小写字符视为两个不同的字符。
**例:**

> **输入:**s = " therasbeetwittwo "，k = 1
> **输出:** 14
> **说明:**只有 1 个元音的最长子串是【cebeetwittw】
> ，长度为 14。
> **输入:**s =“artyebui”，k = 2
> **输出:** 6
> **解释:**只有 2 个元音的最长子串是“rtyebu”

**蛮力方法:**对于每个子串，我们检查 K 个不同元音的标准并检查长度。最后，最大的长度将是结果。
**高效方法:**这里我们维护子串中出现的元音计数。直到 K 不为零，我们计算子串中出现的不同元音。当 K 变成负的时候，我们开始删除在那之前找到的子串的第一个元音，这样之后就有可能出现新的子串(更大的长度)。当我们删除元音时，我们减少它的计数，这样新的子串可能包含出现在字符串后面部分的元音。当 K 为 0 时，我们得到子串的长度。
以下是上述方法的实施

## C++

```
// CPP program to find the longest substring
// with k distinct vowels.
#include <bits/stdc++.h>
using namespace std;

#define MAX 128

// Function to check whether a character is
// vowel or not
bool isVowel(char x)
{
    return (x == 'a' || x == 'e' || x == 'i' ||
            x == 'o' || x == 'u' || x == 'A' ||
            x == 'E' || x == 'I' || x == 'O' ||
            x == 'U');
}

int KDistinctVowel(char s[], int k)
{
    // length of string
    int n = strlen(s);

    // array for count of characters
    int c[MAX];
    memset(c, 0, sizeof(c));

    // Initialize result to be
    // negative
    int result = -1;

    for (int i = 0, j = -1; i < n; ++i) {

        int x = s[i];

        // If letter is vowel then we
        // increment its count value
        // and decrease the k value so
        // that if we again encounter the
        // same vowel character then we
        // don't consider it for our result
        if (isVowel(x)) {
            if (++c[x] == 1) {

                // Decrementing the K value
                --k;
            }
        }

        // Till k is 0 above if condition run
        // after that this while loop condition
        // also become active. Here what we have
        // done actually is that, if K is less
        // than 0 then we eliminate the first
        // vowel we have encountered till that
        // time . Now K is incremented and k
        // becomes 0\. So, now we calculate the
        // length of substring from the present
        // index to the deleted index of vowel
        // which result in our results.
        while (k < 0) {

            x = s[++j];
            if (isVowel(x)) {

                // decreasing the count
                // so that it may appear
                // in another substring
                // appearing after this
                // present substring
                if (--c[x] == 0) {

                    // incrementing the K value
                    ++k;
                }
            }
        }

        // Checking the maximum value
        // of the result by comparing
        // the length of substring
        // whenever K value is 0 means
        // K distinct vowel is present
        // in substring
        if (k == 0)
            result = max(result, i - j);       
    }
    return result;
}

// Driver code
int main(void)
{
    char s[] = "tHeracEBetwEEntheTwo";
    int k = 1;
    cout << KDistinctVowel(s, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest substring
// with k distinct vowels.

class GFG {

    static int MAX = 128;

    // Function to check whether a character is
    // vowel or not
    static boolean isVowel(char x) {
        return (x == 'a' || x == 'e' || x == 'i' ||
                x == 'o' || x == 'u' || x == 'A' ||
                x == 'E' || x == 'I' || x == 'O' ||
                x == 'U');
    }

    static int KDistinctVowel(String s, int k) {
        // length of string
        int n = s.length();

        // array for count of characters
        int[] c = new int[MAX];
        //Array.Clear(c, 0, c.Length);

        // Initialize result to be
        // negative
        int result = -1;

        for (int i = 0, j = -1; i < n; ++i) {

            char x = s.charAt(i);

            // If letter is vowel then we
            // increment its count value
            // and decrease the k value so
            // that if we again encounter the
            // same vowel character then we
            // don't consider it for our result
            if (isVowel(x)) {
                if (++c[x] == 1) {

                    // Decrementing the K value
                    --k;
                }
            }

            // Till k is 0 above if condition run
            // after that this while loop condition
            // also become active. Here what we have
            // done actually is that, if K is less
            // than 0 then we eliminate the first
            // vowel we have encountered till that
            // time . Now K is incremented and k
            // becomes 0\. So, now we calculate the
            // length of substring from the present
            // index to the deleted index of vowel
            // which result in our results.
            while (k < 0) {

                x = s.charAt(++j);
                if (isVowel(x)) {

                    // decreasing the count
                    // so that it may appear
                    // in another substring
                    // appearing after this
                    // present substring
                    if (--c[x] == 0) {

                        // incrementing the K value
                        ++k;
                    }
                }
            }

            // Checking the maximum value
            // of the result by comparing
            // the length of substring
            // whenever K value is 0 means
            // K distinct vowel is present
            // in substring
            if (k == 0) {
                result = Math.max(result, i - j);
            }
        }
        return result;
    }

    // Driver code
    public static void main(String[] args) {
        String s = "tHeracEBetwEEntheTwo";
        int k = 1;
        System.out.println(KDistinctVowel(s, k));
    }
}

/* This Java code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python3 program to find the longest substring
# with k distinct vowels.

MAX = 128

# Function to check whether a character is
# vowel or not
def isVowel(x):

    return (x == 'a' or x == 'e' or x == 'i' or
            x == 'o' or x == 'u' or x == 'A' or
            x == 'E' or x == 'I' or x == 'O' or
            x == 'U')

def KDistinctVowel(c,k):
    n = len(s)

    c = [0 for i in range(MAX)]
    result = -1

    j = -1

    for i in range(n):
        x=s[i]

        # If letter is vowel then we
        # increment its count value
        # and decrease the k value so
        # that if we again encounter the
        # same vowel character then we
        # don't consider it for our result

        if isVowel(x):
            c[ord(x)] += 1
            if c[ord(x)] == 1:
                k -= 1

        # Till k is 0 above if condition run
        # after that this while loop condition
        # also become active. Here what we have
        # done actually is that, if K is less
        # than 0 then we eliminate the first
        # vowel we have encountered till that
        # time . Now K is incremented and k
        # becomes 0\. So, now we calculate the
        # length of substring from the present
        # index to the deleted index of vowel
        # which result in our results.
        while k < 0:
            j += 1
            x = s[j]
            if isVowel(x):

                # decreasing the count
                # so that it may appear
                # in another substring
                # appearing after this
                # present substring
                c[ord(x)] -= 1
                k += 1

        # Checking the maximum value
        # of the result by comparing
        # the length of substring
        # whenever K value is 0 means
        # K distinct vowel is present
        # in substring    

        if k == 0:
            result = max(result, i - j)

    return result

s = "tHeracEBetwEEntheTwo"
k = 1
print(KDistinctVowel(s, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the longest substring
// with k distinct vowels.
using System;

class GFG {

    static int MAX = 128;

    // Function to check whether a character is
    // vowel or not
    static bool isVowel(char x)
    {
        return (x == 'a' || x == 'e' || x == 'i' ||
                x == 'o' || x == 'u' || x == 'A' ||
                x == 'E' || x == 'I' || x == 'O' ||
                x == 'U');
    }

    static int KDistinctVowel(string s, int k)
    {
        // length of string
        int n = s.Length;

        // array for count of characters
        int []c = new int[MAX];
        Array.Clear(c, 0, c.Length);

        // Initialize result to be
        // negative
        int result = -1;

        for (int i = 0, j = -1; i < n; ++i) {

            char x = s[i];

            // If letter is vowel then we
            // increment its count value
            // and decrease the k value so
            // that if we again encounter the
            // same vowel character then we
            // don't consider it for our result
            if (isVowel(x)) {
                if (++c[x] == 1) {

                    // Decrementing the K value
                    --k;
                }
            }

            // Till k is 0 above if condition run
            // after that this while loop condition
            // also become active. Here what we have
            // done actually is that, if K is less
            // than 0 then we eliminate the first
            // vowel we have encountered till that
            // time . Now K is incremented and k
            // becomes 0\. So, now we calculate the
            // length of substring from the present
            // index to the deleted index of vowel
            // which result in our results.
            while (k < 0) {

                x = s[++j];
                if (isVowel(x)) {

                    // decreasing the count
                    // so that it may appear
                    // in another substring
                    // appearing after this
                    // present substring
                    if (--c[x] == 0) {

                        // incrementing the K value
                        ++k;
                    }
                }
            }

            // Checking the maximum value
            // of the result by comparing
            // the length of substring
            // whenever K value is 0 means
            // K distinct vowel is present
            // in substring
            if (k == 0) {
                result = Math.Max(result, i - j);
            }
        }
        return result;
    }

    // Driver code
    static void Main()
    {
        string s = "tHeracEBetwEEntheTwo";
        int k = 1;
        Console.Write(KDistinctVowel(s, k));
    }
}

// This code is contributed Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the longest
// substring with k distinct vowels.
$MAX = 128;

// Function to check whether a
// character is vowel or not
function isVowel($x)
{
    return ($x == 'a' || $x == 'e' || $x == 'i' ||
            $x == 'o' || $x == 'u' || $x == 'A' ||
            $x == 'E' || $x == 'I' || $x == 'O' ||
            $x == 'U');
}

function KDistinctVowel($s, $k)
{
    global $MAX;

    // length of string
    $n = strlen($s);

    // array for count of characters
    $c = array_fill(0, $MAX, NULL);

    // Initialize result to be negative
    $result = -1;

    for ($i = 0, $j = -1; $i < $n; ++$i)
    {
        $x = $s[$i];

        // If letter is vowel then we increment
        // its count value and decrease the k
        // value so that if we again encounter
        // the same vowel character then we
        // don't consider it for our result
        if (isVowel($x))
        {
            if (++$c[ord($x)] == 1)
            {

                // Decrementing the K value
                --$k;
            }
        }

        // Till k is 0 above if condition run
        // after that this while loop condition
        // also become active. Here what we have
        // done actually is that, if K is less
        // than 0 then we eliminate the first
        // vowel we have encountered till that
        // time . Now K is incremented and k
        // becomes 0\. So, now we calculate the
        // length of substring from the present
        // index to the deleted index of vowel
        // which result in our results.
        while ($k < 0)
        {
            $x = $s[++$j];
            if (isVowel($x))
            {

                // decreasing the count so that it
                // may appear in another substring
                // appearing after this present
                // substring
                if (--$c[ord($x)] == 0)
                {

                    // incrementing the K value
                    ++$k;
                }
            }
        }

        // Checking the maximum value of the
        // result by comparing the length of
        // substring whenever K value is 0
        // means K distinct vowel is present
        // in substring
        if ($k == 0)
            $result = max($result, $i - $j);    
    }
    return $result;
}

// Driver code
$s = "tHeracEBetwEEntheTwo";
$k = 1;
echo KDistinctVowel($s, $k);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to find the longest substring
// with k distinct vowels.

    let MAX = 128;

    // Function to check whether a character is
    // vowel or not
    function isVowel(x)
    {
        return (x == 'a' || x == 'e' || x == 'i' ||
                x == 'o' || x == 'u' || x == 'A' ||
                x == 'E' || x == 'I' || x == 'O' ||
                x == 'U');
    }

    function KDistinctVowel(s,k)
    {
        // length of string
        let n = s.length;

        // array for count of characters
        let c = new Array(MAX);
        for(let i=0;i<c.length;i++)
        {
            c[i]=0;
        }
        //Array.Clear(c, 0, c.Length);

        // Initialize result to be
        // negative
        let result = -1;

        for (let i = 0, j = -1; i < n; ++i) {

            let x = s[i];

            // If letter is vowel then we
            // increment its count value
            // and decrease the k value so
            // that if we again encounter the
            // same vowel character then we
            // don't consider it for our result
            if (isVowel(x)) {
                if (++c[x.charCodeAt(0)] == 1) {

                    // Decrementing the K value
                    --k;
                }
            }

            // Till k is 0 above if condition run
            // after that this while loop condition
            // also become active. Here what we have
            // done actually is that, if K is less
            // than 0 then we eliminate the first
            // vowel we have encountered till that
            // time . Now K is incremented and k
            // becomes 0\. So, now we calculate the
            // length of substring from the present
            // index to the deleted index of vowel
            // which result in our results.
            while (k < 0) {

                x = s[++j];
                if (isVowel(x)) {

                    // decreasing the count
                    // so that it may appear
                    // in another substring
                    // appearing after this
                    // present substring
                    if (--c[x.charCodeAt(0)] == 0) {

                        // incrementing the K value
                        ++k;
                    }
                }
            }

            // Checking the maximum value
            // of the result by comparing
            // the length of substring
            // whenever K value is 0 means
            // K distinct vowel is present
            // in substring
            if (k == 0) {
                result = Math.max(result, i - j);
            }
        }
        return result;
    }

    // Driver code
    let s = "tHeracEBetwEEntheTwo";
    let k = 1;
    document.write(KDistinctVowel(s, k));

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
7
```
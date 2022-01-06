# 用以下操作加密给定的字符串

> 原文:[https://www . geesforgeks . org/用以下操作加密给定字符串/](https://www.geeksforgeeks.org/encrypt-the-given-string-with-the-following-operations/)

给定一个字符串 **s** ，任务是用以下方式加密该字符串:

1.  如果当前字符的频率是偶数，那么将当前字符增加 x。
2.  如果当前字符的频率是奇数，那么将当前字符减少 x。

**注意:**所有的操作都是循环的，即在“z”上加 1 会得到“a”，在“a”上减 1 会得到“z”

**示例:**

> **输入:**s =“abcda”，x=3
> **输出:**dyzad
> “a”在字符串中出现 2 次，因此将“a”增加 3 次会变成“d”
> “b”在字符串中出现 1 次，因此将“b”减少 3 次会变成“y”
> “c”在字符串中出现 1 次，因此将“c”减少 3 次会变成“z”
> “d”在字符串中出现 1 次，因此将“d”减少 3 次
> 
> **输入:** s="aabbc "，x=5
> **输出:** ffggx

**进场:**

*   创建一个频率数组来存储每个字符的频率。
*   遍历给定的字符串，如果每个字符的频率为偶数，则递增 x，否则如果频率为奇数，则递减 x。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach:
#include <bits/stdc++.h>
#define MAX 26
using namespace std;

// Function to return the encrypted string
string encryptStr(string str, int n, int x)
{

    // Reduce x because rotation of
    // length 26 is unnecessary
    x = x % MAX;

    // Calculate the frequency of characters
    int freq[MAX] = {0};

    for(int i = 0; i < n; i++)
    {
        freq[str[i] - 'a']++;
    }

    for(int i = 0; i < n; i++)
    {

        // If the frequency of current character
        // is even then increment it by x
        if (freq[str[i] - 'a'] % 2 == 0)
        {
            int pos = (str[i] - 'a' + x) % MAX;
            str[i] = (char)(pos + 'a');
        }

        // Else decrement it by x
        else
        {
            int pos = (str[i] - 'a' - x);

            if (pos < 0)
            {
                pos += MAX;
            }

            str[i] = (char)(pos + 'a');
        }
    }

    // Return the count
    return str;
}

// Driver code
int main()
{
    string s = "abcda";
    int n = s.size();
    int x = 3;

    cout << encryptStr(s, n, x) << endl;

    return 0;
}

// This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach:
public class GFG {

    static final int MAX = 26;

    // Function to return the encrypted string
    static String encryptStr(String str, int n, int x)
    {

        // Reduce x because rotation of
        // length 26 is unnecessary
        x = x % MAX;
        char arr[] = str.toCharArray();

        // calculate the frequency of characters
        int freq[] = new int[MAX];
        for (int i = 0; i < n; i++)
            freq[arr[i] - 'a']++;

        for (int i = 0; i < n; i++) {

            // If the frequency of current character
            // is even then increment it by x
            if (freq[arr[i] - 'a'] % 2 == 0) {
                int pos = (arr[i] - 'a' + x) % MAX;
                arr[i] = (char)(pos + 'a');
            }

            // Else decrement it by x
            else {
                int pos = (arr[i] - 'a' - x);
                if (pos < 0)
                    pos += MAX;
                arr[i] = (char)(pos + 'a');
            }
        }

        // Return the count
        return String.valueOf(arr);
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abcda";
        int n = s.length();
        int x = 3;
        System.out.println(encryptStr(s, n, x));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach:
MAX = 26

# Function to return the encrypted string
def encryptstrr(strr, n, x):

    # Reduce x because rotation of
    # length 26 is unnecessary
    x = x % MAX
    arr = list(strr)

    # calculate the frequency of characters
    freq = [0]*MAX
    for i in range(n):
        freq[ord(arr[i]) - ord('a')] += 1

    for i in range(n):

        # If the frequency of current character
        # is even then increment it by x
        if (freq[ord(arr[i]) - ord('a')] % 2 == 0):
            pos = (ord(arr[i]) - ord('a') + x) % MAX
            arr[i] = chr(pos + ord('a'))

        # Else decrement it by x
        else:
            pos = (ord(arr[i]) - ord('a') - x)
            if (pos < 0):
                pos += MAX
            arr[i] = chr(pos + ord('a'))

    # Return the count
    return "".join(arr)

# Driver code
s = "abcda"
n = len(s)
x = 3
print(encryptstrr(s, n, x))

# This code is contributed by
# shubhamsingh10
```

## C#

```
// C# implementation of the above approach:
using System;

class GFG
{

    static int MAX = 26;

    // Function to return the encrypted string
    public static char[] encryptStr(String str,
                                    int n, int x)
    {

        // Reduce x because rotation of
        // length 26 is unnecessary
        x = x % MAX;
        char[] arr = str.ToCharArray();

        // calculate the frequency of characters
        int[] freq = new int[MAX];
        for (int i = 0; i < n; i++)
            freq[arr[i] - 'a']++;

        for (int i = 0; i < n; i++)
        {

            // If the frequency of current character
            // is even then increment it by x
            if (freq[arr[i] - 'a'] % 2 == 0)
            {
                int pos = (arr[i] - 'a' + x) % MAX;
                arr[i] = (char)(pos + 'a');
            }

            // Else decrement it by x
            else
            {
                int pos = (arr[i] - 'a' - x);
                if (pos < 0)
                    pos += MAX;
                arr[i] = (char)(pos + 'a');
            }
        }

        // Return the count
        return arr;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "abcda";
        int n = s.Length;
        int x = 3;
        Console.WriteLine(encryptStr(s, n, x));
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach:
var MAX = 26;

// Function to return the encrypted string
function encryptStr(str, n, x)
{

    // Reduce x because rotation of
    // length 26 is unnecessary
    x = x % MAX;

    // Calculate the frequency of characters
    var freq = Array(MAX).fill(0);

    for(var i = 0; i < n; i++)
    {
        freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    for(var i = 0; i < n; i++)
    {

        // If the frequency of current character
        // is even then increment it by x
        if (freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)] % 2 == 0)
        {
            var pos = (str[i].charCodeAt(0) - 'a'.charCodeAt(0) + x) % MAX;
            str[i] = String.fromCharCode(pos + 'a'.charCodeAt(0));
        }

        // Else decrement it by x
        else
        {
            var pos = (str[i].charCodeAt(0) - 'a'.charCodeAt(0) - x);

            if (pos < 0)
            {
                pos += MAX;
            }

            str[i] = String.fromCharCode(pos + 'a'.charCodeAt(0));
        }
    }

    // Return the count
    return str.join('');
}

// Driver code
var s = "abcda";
var n = s.length;
var x = 3;

document.write( encryptStr(s.split(''), n, x));

</script>
```

**Output:** 

```
dyzad
```

**时间复杂度:** O(N)
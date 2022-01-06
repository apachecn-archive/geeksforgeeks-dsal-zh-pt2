# 频率最高的字符串中最长的前缀

> 原文:[https://www . geesforgeks . org/最高频率最长字符串前缀/](https://www.geeksforgeeks.org/longest-prefix-in-a-string-with-highest-frequency/)

给定一个字符串，找到频率最高的前缀。如果两个前缀具有相同的频率，那么考虑长度最大的那个。
**例:**

```
Input : str = "abc" 
Output : abc
Each prefix has same frequency(one) and the 
prefix with maximum length is "abc".

Input : str = "abcab"
Output : ab
Both prefix "a" and "ab" occur two times and the 
prefix with maximum length is "ab".
```

其思想是观察给定字符串的每个前缀都将包含字符串的第一个字符，并且第一个字符本身也是给定字符串的前缀。所以出现次数最多的前缀是第一个字符。现在的任务仍然是最大化最高频率前缀的长度。
**进场:**

1.  取一个向量来存储字符串第一个元素的索引。
2.  如果第一个元素只出现一次，那么最长的前缀将是整个字符串。
3.  否则，循环直到第一个元素第二次出现，并在每个存储的索引后检查一个字母。
4.  如果没有错配，我们就前进，否则我们就停下来。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find Longest prefix string with the
// highest frequency
void prefix(string str)
{
    int k = 1, j;
    int n = str.length();

    vector<int> g;
    int flag = 0;

    // storing all indices where first element is found
    for (int i = 1; i < n; i++) {
        if (str[i] == str[0]) {
            g.push_back(i);
            flag = 1;
        }
    }

    // if the first letter in the string does not occur
    // again  then answer will be the whole string
    if (flag == 0) {
        cout << str << endl;
    }
    else {
        int len = g.size();

        // loop till second appearance of the first element
        while (k < g[0]) {

            int cnt = 0;
            for (j = 0; j < len; j++) {

                // check one letter after every stored index
                if (str[g[j] + k] == str[k]) {
                    cnt++;
                }
            }

            // If there is no mismatch we move forward
            if (cnt == len) {
                k++;
            }
            // otherwise we stop
            else {
                break;
            }
        }

        for (int i = 0; i < k; i++) {
            cout << str[i];
        }

        cout << endl;
    }
}

// Driver Code
int main()
{
    string str = "abcab";
    prefix(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to find Longest prefix string with the
    // highest frequency
    static void prefix(char[] str)
    {
        int k = 1, j;
        int n = str.length;

        Vector<Integer> g = new Vector<>();
        int flag = 0;

        // storing all indices where first element is found
        for (int i = 1; i < n; i++)
        {
            if (str[i] == str[0])
            {
                g.add(i);
                flag = 1;
            }
        }

        // if the first letter in the string does not occur
        // again then answer will be the whole string
        if (flag == 0)
        {
            System.out.println(String.valueOf(str));
        }
        else
        {
            int len = g.size();

            // loop till second appearance of the first element
            while (k < g.get(0))
            {

                int cnt = 0;
                for (j = 0; j < len; j++)
                {

                    // check one letter after every stored index
                    if ((g.get(j) + k) < n &&
                        str[g.get(j) + k] == str[k])
                    {
                        cnt++;
                    }
                }

                // If there is no mismatch we move forward
                if (cnt == len)
                {
                    k++;
                }
                // otherwise we stop
                else
                {
                    break;
                }
            }

            for (int i = 0; i < k; i++)
            {
                System.out.print(str[i]);
            }

            System.out.println();
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        String str = "abcab";
        prefix(str.toCharArray());
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find Longest prefix string with the
# highest frequency
def prefix(string) :

    k = 1;
    n = len(string);

    g = [];
    flag = 0;

    # storing all indices where first element is found
    for i in range(1, n) :
        if (string[i] == string[0]) :
            g.append(i);
            flag = 1;

    # if the first letter in the string does not occur
    # again then answer will be the whole string
    if (flag == 0) :
        print(string);

    else :
        length = len(g);

        # loop till second appearance of the first element
        while (k < g[0]) :
            cnt = 0;

            for j in range(length) :

                # check one letter after every stored index
                if (string[g[j] + k] == string[k]) :
                    cnt += 1;

            # If there is no mismatch we move forward
            if (cnt == len) :
                k += 1;

            # otherwise we stop
            else :
                break;

        for i in range(k+1) :
            print(string[i],end="");

        print()

# Driver Code
if __name__ == "__main__" :

    string = "abcab";
    prefix(string);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find Longest prefix string with the
    // highest frequency
    static void prefix(char[] str)
    {
        int k = 1, j;
        int n = str.Length;

        List<int> g = new List<int>();
        int flag = 0;

        // storing all indices where first element is found
        for (int i = 1; i < n; i++)
        {
            if (str[i] == str[0])
            {
                g.Add(i);
                flag = 1;
            }
        }

        // if the first letter in the string does not occur
        // again then answer will be the whole string
        if (flag == 0)
        {
            Console.WriteLine(String.Join("",str));
        }
        else
        {
            int len = g.Count;

            // loop till second appearance of the first element
            while (k < g[0])
            {

                int cnt = 0;
                for (j = 0; j < len; j++)
                {

                    // check one letter after every stored index
                    if ((g[j] + k) < n &&
                        str[g[j] + k] == str[k])
                    {
                        cnt++;
                    }
                }

                // If there is no mismatch we move forward
                if (cnt == len)
                {
                    k++;
                }
                // otherwise we stop
                else
                {
                    break;
                }
            }

            for (int i = 0; i < k; i++)
            {
                Console.Write(str[i]);
            }

            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main()
    {
        String str = "abcab";
        prefix(str.ToCharArray());
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to find Longest prefix string with the
    // highest frequency
    function prefix(str)
    {
        let k = 1, j;
        let n = str.length;

        let g = [];
        let flag = 0;

        // storing all indices where first element is found
        for (let i = 1; i < n; i++)
        {
            if (str[i] == str[0])
            {

                g.push(i);
                flag = 1;
            }
        }

        // if the first letter in the string does not occur
        // again then answer will be the whole string
        if (flag == 0)
        {
            document.write((str.join("")));
        }
        else
        {
            let len = g.length;

            // loop till second appearance of the first element
            while (k < g[0])
            {

                let cnt = 0;
                for (j = 0; j < len; j++)
                {

                    // check one letter after every stored index
                    if ((g[j] + k) < n &&
                        str[g[j] + k] == str[k])
                    {
                        cnt++;
                    }
                }

                // If there is no mismatch we move forward
                if (cnt == len)
                {
                    k++;
                }
                // otherwise we stop
                else
                {
                    break;
                }
            }

            for (let i = 0; i < k; i++)
            {
                document.write(str[i]);
            }

            document.write("<br/>");
        }
    }

// Driver Code

     let str = "abcab";
     prefix(str);

 // This code is co tributed by sanjoy_62.
</script>
```

**Output:** 

```
ab
```

**时间复杂度:** O(N)
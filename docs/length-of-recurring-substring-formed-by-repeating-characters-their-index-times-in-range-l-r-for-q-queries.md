# 在 Q 查询的[L，R]范围内重复字符索引次数形成的循环子串长度

> 原文:[https://www . geesforgeks . org/由重复字符构成的重复子串长度-它们的索引-范围内时间-l-r-for-q-query/](https://www.geeksforgeeks.org/length-of-recurring-substring-formed-by-repeating-characters-their-index-times-in-range-l-r-for-q-queries/)

给定一个字符串 **S** ，两个整数 **L** 和 **R** 。任务是在给定的范围内找到子串的**长度**，使得每个字符**恰好在 **k** 次之后重复**，其中 k 是字母表中对应字符的**索引**。打印 **q** 查询所需的结果

**示例**:

> **输入**:s =“cbbde”，q = 3，查询[] = { { 2，4 }，{ 3，5 }，{ 1，3 } }；
> **输出** : {8，7，11}
> **解释**:给定范围内重复出现后的子串:“bbddddeeeee”。因此，子串的长度= 11
> 
> **输入**:s =“xyyz”，q = 1，查询[] = {1，2}
> **输出** : 49

**方法**:该方法涉及到预计算的思想，用于求解 O(1)中的每个查询。

*   首先，通过重复字符的索引次数来创建字符串
*   为形成的字符串中的每个字符预先计算范围[0，i]的循环子字符串的长度。
*   在前缀数组的帮助下，将当前字符指向的相应值的总和存储在字母表中。
*   对于每个查询，确定循环子字符串的长度，并将结果打印在 O(1)中

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// recurring substring in range [l, r]
int recurringSubstring(string s, int l, int r)
{

    // Length of the string
    int N = s.size();

    // Variable to store the index of
    // the character in the alphabet
    int a[N];
    for (int i = 0; i < N; i++) {

        a[i] = (s[i] - 'a') + 1;
    }

    // Prefix array to store the sum
    int prefix[N];
    prefix[0] = a[0];

    for (int i = 1; i < N; i++) {

        prefix[i] = prefix[i - 1] + a[i];
    }

    l = l - 1;
    r = r - 1;

    // If l is greater than 0
    if (l != 0) {

        return prefix[r] - prefix[l - 1];
    }

    // If l is less or equal to 0
    else {

        return prefix[r];
    }
}

void recurSubQueries(string s,
                     pair<int, int> queries[],
                     int q)
{
    for (int i = 0; i < q; i++) {
        int l = queries[i].first;
        int r = queries[i].second;
        cout << recurringSubstring(s, l, r)
             << endl;
    }
}

// Driver Code
int main()
{

    string s = "cbbde";
    int q = 3;
    pair<int, int> queries[]
        = { { 2, 4 }, { 3, 5 }, { 1, 3 } };

    recurSubQueries(s, queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG
{

    // Function to find the length of
    // recurring substring in range [l, r]
    static int recurringSubstring(String s, int l, int r)
    {

        // Length of the string
        int N = s.length();

        // Variable to store the index of
        // the character in the alphabet
        int a[] = new int[N];
        for (int i = 0; i < N; i++) {

            a[i] = (s.charAt(i) - 'a') + 1;
        }

        // Prefix array to store the sum
        int prefix[] = new int[N];
        prefix[0] = a[0];

        for (int i = 1; i < N; i++) {

            prefix[i] = prefix[i - 1] + a[i];
        }

        l = l - 1;
        r = r - 1;

        // If l is greater than 0
        if (l != 0) {

            return prefix[r] - prefix[l - 1];
        }

        // If l is less or equal to 0
        else {

            return prefix[r];
        }
    }

    static void recurSubQueries(String s, int queries[][],
                                int q)
    {
        for (int i = 0; i < q; i++) {
            int l = queries[i][0];
            int r = queries[i][1];
            System.out.println(recurringSubstring(s, l, r));
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "cbbde";
        int q = 3;
        int[][] queries = { { 2, 4 }, { 3, 5 }, { 1, 3 } };

        recurSubQueries(s, queries, q);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the length of
# recurring substring in range [l, r]
def recurringSubstring(s, l, r):

    # Length of the string
    N = len(s);

    # Variable to store the index of
    # the character in the alphabet
    a = [0 for i in range(N)];

    for i in range(N):
        a[i] = ord(s[i]) - ord('a') + 1;

    # Prefix array to store the sum
    prefix = [0 for i in range(N)];
    prefix[0] = a[0];

    for i in range(N):
        prefix[i] = prefix[i - 1] + a[i];

    l = l - 1;
    r = r - 1;

    # If l is greater than 0
    if (l != 0):

        return prefix[r] - prefix[l - 1];

    # If l is less or equal to 0
    else:

        return prefix[r];

def recurSubQueries(s, queries, q):
    for i in range(q):
        l = queries[i][0];
        r = queries[i][1];
        print(recurringSubstring(s, l, r));

# Driver Code
if __name__ == '__main__':
    s = "cbbde";
    q = 3;
    queries = [[2, 4], [3, 5], [1, 3]];

    recurSubQueries(s, queries, q);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# code for the above approach
using System;

public class GFG
{

    // Function to find the length of
    // recurring substring in range [l, r]
    static int recurringSubstring(String s, int l, int r)
    {

        // Length of the string
        int N = s.Length;

        // Variable to store the index of
        // the character in the alphabet
        int []a = new int[N];
        for (int i = 0; i < N; i++) {

            a[i] = (s[i] - 'a') + 1;
        }

        // Prefix array to store the sum
        int []prefix = new int[N];
        prefix[0] = a[0];

        for (int i = 1; i < N; i++) {

            prefix[i] = prefix[i - 1] + a[i];
        }

        l = l - 1;
        r = r - 1;

        // If l is greater than 0
        if (l != 0) {

            return prefix[r] - prefix[l - 1];
        }

        // If l is less or equal to 0
        else {

            return prefix[r];
        }
    }

    static void recurSubQueries(String s, int [,]queries,
                                int q)
    {
        for (int i = 0; i < q; i++) {
            int l = queries[i,0];
            int r = queries[i,1];
            Console.WriteLine(recurringSubstring(s, l, r));
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "cbbde";
        int q = 3;
        int[,] queries = { { 2, 4 }, { 3, 5 }, { 1, 3 } };

        recurSubQueries(s, queries, q);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find the length of
    // recurring substring in range [l, r]
    const recurringSubstring = (s, l, r) => {

        // Length of the string
        let N = s.length;

        // Variable to store the index of
        // the character in the alphabet
        let a = new Array(N).fill(0);
        for (let i = 0; i < N; i++) {

            a[i] = (s.charCodeAt(i) - 'a'.charCodeAt(0)) + 1;
        }

        // Prefix array to store the sum
        let prefix = new Array(N).fill(0);
        prefix[0] = a[0];

        for (let i = 1; i < N; i++) {

            prefix[i] = prefix[i - 1] + a[i];
        }

        l = l - 1;
        r = r - 1;

        // If l is greater than 0
        if (l != 0) {

            return prefix[r] - prefix[l - 1];
        }

        // If l is less or equal to 0
        else {

            return prefix[r];
        }
    }

    const recurSubQueries = (s, queries, q) => {
        for (let i = 0; i < q; i++) {
            let l = queries[i][0];
            let r = queries[i][1];
            document.write(`${recurringSubstring(s, l, r)}<br/>`);
        }
    }

    // Driver Code
    let s = "cbbde";
    let q = 3;
    let queries = [[2, 4], [3, 5], [1, 3]];

    recurSubQueries(s, queries, q);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
8
11
7
```

***时间复杂度*** : O(N+Q)，其中 N 为弦的长度
***辅助空间*** : O(N)
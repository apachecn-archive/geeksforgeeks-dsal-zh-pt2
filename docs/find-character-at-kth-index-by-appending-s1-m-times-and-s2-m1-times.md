# 追加 S1 (M)次和 S2 (M+1)次

找到第 k 个索引处的字符

> 原文:[https://www . geesforgeks . org/find-character-at-kth-index-by-appending-S1-m-times-and-S2-m1-times/](https://www.geeksforgeeks.org/find-character-at-kth-index-by-appending-s1-m-times-and-s2-m1-times/)

给定两个[字符串](https://www.geeksforgeeks.org/strings-in-java/)、 **S1** 和 **S2** 以及一个整数 **K** 。一根[弦](https://www.geeksforgeeks.org/strings-in-java/) **弦**可以通过执行以下操作制成:

*   最初取一个空字符串
*   追加 S1 一次
*   追加 S2 两次
*   追加 S1 三次
*   追加 S2 四次
*   追加 S1 五次
*   追加 S2 六次
*   你可以继续构建这个字符串，直到它到达 K

任务是在新的[字符串](https://www.geeksforgeeks.org/strings-in-java/) **字符串中找到 **k <sup>th</sup>** 位置的字符。**

> **输入:**S1 =“a”，S2 =“BC”，k = 4
> **输出:** b
> **说明:**S3 =“a”+“bcbc”+“AAA”+“bcbcbcbc”= =>abbcaabcbcbcbcbc。所以第四个索引上的字符是“b”
> 
> **输入:**S1 =“Geeks”，S2 =“for”，k = 3
> **输出:** e
> **解释:**S3 =“Geeks”+“for”+“Geeks Geeks”= =>Geeks forgeeks Geeks。所以第三个位置的字符是“e”。

**方法:**简单的解决方法是继续在[字符串](https://www.geeksforgeeks.org/strings-in-java/) **字符串中添加[字符串](https://www.geeksforgeeks.org/strings-in-java/)，**直到索引达到 **k.** 然后，将字符返回到索引 **k** 。

下面是上述方法的实现。

## C++

```
// C++ program to solve the above approach
#include<bits/stdc++.h>
using namespace std;

char KthCharacter(string s, string t, long k)
{

  // initializing first and second variable
  // as to store how many string 's'
  // and string 't' will be appended
  long f = 1;
  long ss = 2;
  string tmp = "";

  // storing tmp length
  int len = tmp.length();

  // if length of string tmp is greater than k, then
  // we have reached our destination string now we can
  // return character at index k
  while (len < k) {

    long tf = f;
    long ts = ss;

    // appending s to tmp, f times
    while (tf-- != 0) {
      tmp += s;
    }

    // appending t to tmp, s times
    while (ts-- != 0) {
      tmp += t;
    }
    f += 2;
    ss += 2;
    len = tmp.length();
  }

  // extracting output character
  char output = tmp[k - 1];
  return output;
}

// Driver code
int main()
{
  string S1 = "a", S2 = "bc";
  int k = 4;
  char ans = KthCharacter(S1, S2, k);
  cout<<ans;
}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve the above approach

import java.io.*;

class GFG {
    static char KthCharacter(String s, String t, long k)
    {
        // initializing first and second variable
        // as to store how many string 's'
        // and string 't' will be appended
        long f = 1;
        long ss = 2;
        String tmp = "";

        // storing tmp length
        int len = tmp.length();

        // if length of string tmp is greater than k, then
        // we have reached our destination string now we can
        // return character at index k
        while (len < k) {

            long tf = f;
            long ts = ss;

            // appending s to tmp, f times
            while (tf-- != 0) {
                tmp += s;
            }

            // appending t to tmp, s times
            while (ts-- != 0) {
                tmp += t;
            }
            f += 2;
            ss += 2;
            len = tmp.length();
        }

        // extracting output character
        char output = tmp.charAt((int)k - 1);
        return output;
    }

    // Driver code
    public static void main(String[] args)
    {

        String S1 = "a", S2 = "bc";
        int k = 4;
        char ans = KthCharacter(S1, S2, k);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python program to solve the above approach
def KthCharacter(s, t, k):

    # initializing first and second variable
    # as to store how many string 's'
    # and string 't' will be appended
    f = 1
    ss = 2
    tmp = ""

    # storing tmp length
    lenn = len(tmp)

    # if length of string tmp is greater than k, then
    # we have reached our destination string now we can
    # return character at index k
    while (lenn < k):
        tf = f
        ts = ss

        # appending s to tmp, f times
        while (tf != 0):
            tf -=1
            tmp += s
        # appending t to tmp, s times
        while (ts != 0) :
            ts -=1
            tmp += t

        f += 2
        ss += 2
        lenn = len(tmp)

    # extracting output character
    output = tmp[k - 1]
    return output

# Driver code
S1 = "a"
S2 = "bc"
k = 4
ans = KthCharacter(S1, S2, k)
print(ans)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to solve the above approach
using System;

class GFG {
    static char KthCharacter(string s, string t, long k)
    {
        // initializing first and second variable
        // as to store how many string 's'
        // and string 't' will be appended
        long f = 1;
        long ss = 2;
        string tmp = "";

        // storing tmp length
        int len = tmp.Length;

        // if length of string tmp is greater than k, then
        // we have reached our destination string now we can
        // return character at index k
        while (len < k) {

            long tf = f;
            long ts = ss;

            // appending s to tmp, f times
            while (tf-- != 0) {
                tmp += s;
            }

            // appending t to tmp, s times
            while (ts-- != 0) {
                tmp += t;
            }
            f += 2;
            ss += 2;
            len = tmp.Length;
        }

        // extracting output character
        char output = tmp[(int)k - 1];
        return output;
    }

    // Driver code
    public static void Main(string[] args)
    {

        string S1 = "a", S2 = "bc";
        int k = 4;
        char ans = KthCharacter(S1, S2, k);
        Console.Write(ans);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program to solve the above approach

function KthCharacter(s, t, k) {
  // initializing first and second variable
  // as to store how many string 's'
  // and string 't' will be appended
  let f = 1;
  let ss = 2;
  let tmp = "";

  // storing tmp length
  let len = tmp.length;

  // if length of string tmp is greater than k, then
  // we have reached our destination string now we can
  // return character at index k
  while (len < k) {
    let tf = f;
    let ts = ss;

    // appending s to tmp, f times
    while (tf-- != 0) {
      tmp += s;
    }

    // appending t to tmp, s times
    while (ts-- != 0) {
      tmp += t;
    }
    f += 2;
    ss += 2;
    len = tmp.length;
  }

  // extracting output character
  let output = tmp[k - 1];
  return output;
}

// Driver code

let S1 = "a",
  S2 = "bc";
let k = 4;
let ans = KthCharacter(S1, S2, k);
document.write(ans);

</script>
```

**Output**

```
b
```

***时间复杂度:**O(K)*
T5**辅助空间:** O(K)

**高效方法:**由于 **K** 是**长**类型，而[字符串](https://www.geeksforgeeks.org/strings-in-java/)的大小只能达到 int 的最大可能值，因此无法使用该代码，并且不会在所有情况下都通过。与其将[字符串](https://www.geeksforgeeks.org/strings-in-java/) **s** 和 **t** 附加到 **temp** 上，不如从 **K、**中减去 **s** 的长度和 **t** 的长度，使范围始终在 **int** 类型内。按照以下步骤解决问题:

*   将两个变量 **n** 和 **m** 初始化为各自[弦](https://www.geeksforgeeks.org/strings-in-java/)T6s**t**的长度
*   初始化两个变量，**第一个**和**第二个**为 **1** 和 **2** 保持时间计数[字符串](https://www.geeksforgeeks.org/strings-in-java/)T10】s 和 **t** 必须追加**。**
*   初始化变量**输出**以将字符存储在新的[字符串](https://www.geeksforgeeks.org/strings-in-java/)中的**k<sup>th</sup>T5】位置。**
*   [循环迭代](https://www.geeksforgeeks.org/java-while-loop-with-examples/#:~:text=Java%20while%20loop%20is%20a, as%20a%20repeating%20if%20statement.&text=If%20the%20condition%20evaluates%20to, and%20go%20to%20update%20expression.)直到 **k** 大于 **0:**
    *   如果 **k** 大于 **first*n** ，则从 **k** 中减去该值，并将 **first** 的值增加 **2。**
    *   如果 **k** 大于**秒*m** ，则从 **k** 中减去该值，并将**秒**的值增加 **2。**
    *   否则( **k** 小于**秒* m)**则第二个[字符串](https://www.geeksforgeeks.org/strings-in-java/) **t** 中的字符将作为答案，因为[字符串](https://www.geeksforgeeks.org/strings-in-java/) **t** 将被追加**秒**次， **k** 将在此位置范围内。
    *   将变量 **ind** 初始化为 **k%m** 的模数，在[字符串](https://www.geeksforgeeks.org/strings-in-java/)中 **ind** 位置的字符将是答案。将字符存储在变量**输出中。**
    *   否则( **k** 小于**第一* n)**，那么第二个[字符串](https://www.geeksforgeeks.org/strings-in-java/) **s** 中的字符将作为答案，因为[字符串](https://www.geeksforgeeks.org/strings-in-java/) **s** 将被追加**第一个**次， **k** 将在该位置范围内。
    *   将变量 **ind** 初始化为 **k%n** 的模数，位于[字符串](https://www.geeksforgeeks.org/strings-in-java/)中 **ind** 位置的字符将是答案。将字符存储在变量**输出中。**
*   执行上述步骤后，返回**的值，输出**作为答案。

下面是上述方法的实现。

## C++

```
// C++ program to solve the above approach
#include<bits/stdc++.h>
using namespace std;

char KthCharacter(string s, string t, long k)
{

  // storing length
  long n = s.length();
  long m = t.length();

  // variables for temporary strings of s and t
  long first = 1;
  long second = 2;

  // final output variable
  char output = '?';
  while (k > 0) {

    // if k is greater than even after adding string
    // 's' 'first' times  (let's call it x) we'll
    // subtract x from k
    if (k > first * n) {

      long x = first * n;
      k = k - x;

      // incrementing first by 2, as said in
      // problem statement
      first = first + 2;

      // if k is greater than even after adding
      // string 't' 'second' times  (let's call it
      // y) we'll subtract y from k
      if (k > second * m) {

        long y = second * m;
        k = k - y;

        // incrementing second by two as said in
        // problem statement
        second = second + 2;
      }

      // if k is smaller than y, then the
      // character
      // will be at position k%m.
      else {

        // returning character at k index
        long ind = k % m;
        ind--;
        if (ind < 0)
          ind = m - 1;
        output = t[(int)ind];
        break;
      }
    }

    // if k is smaller than x, then the character
    // is at position k%n
    else {

      // returning character at k index
      long ind = k % n;
      ind--;
      if (ind < 0)
        ind = n - 1;
      output = s[(int)ind];
      break;
    }
  }
  return output;
}

// Driver code
int main()
{

  string S1 = "a", S2 = "bc";
  int k = 4;
  char ans = KthCharacter(S1, S2, k);
  cout<<(ans);
  return 0;
}

// This code is contributed by umadevi9616
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve the above approach

import java.io.*;

class GFG {
    static char KthCharacter(String s, String t, long k)
    {
        // storing length
        long n = s.length();
        long m = t.length();

        // variables for temporary strings of s and t
        long first = 1;
        long second = 2;

        // final output variable
        char output = '?';
        while (k > 0) {

            // if k is greater than even after adding string
            // 's' 'first' times  (let's call it x) we'll
            // subtract x from k
            if (k > first * n) {

                long x = first * n;
                k = k - x;

                // incrementing first by 2, as said in
                // problem statement
                first = first + 2;

                // if k is greater than even after adding
                // string 't' 'second' times  (let's call it
                // y) we'll subtract y from k
                if (k > second * m) {

                    long y = second * m;
                    k = k - y;

                    // incrementing second by two as said in
                    // problem statement
                    second = second + 2;
                }

                // if k is smaller than y, then the
                // character
                // will be at position k%m.
                else {

                    // returning character at k index
                    long ind = k % m;
                    ind--;
                    if (ind < 0)
                        ind = m - 1;
                    output = t.charAt((int)ind);
                    break;
                }
            }

            // if k is smaller than x, then the character
            // is at position k%n
            else {

                // returning character at k index
                long ind = k % n;
                ind--;
                if (ind < 0)
                    ind = n - 1;
                output = s.charAt((int)ind);
                break;
            }
        }
        return output;
    }

    // Driver code
    public static void main(String[] args)
    {

        String S1 = "a", S2 = "bc";
        int k = 4;
        char ans = KthCharacter(S1, S2, k);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python program to solve the above approach
def KthCharacter(s, t, k):

        # storing length
        n = len(s)
        m = len(t)

        # variables for temporary strings of s and t
        first = 1
        second = 2

        # final output variable
        output = '?'
        while (k > 0):

            # if k is greater than even after adding string
            # 's' 'first' times  (let's call it x) we'll
            # subtract x from k
            if (k > first * n):
                x = first * n
                k = k - x

                # incrementing first by 2, as said in
                # problem statement
                first = first + 2

                # if k is greater than even after adding
                # string 't' 'second' times  (let's call it
                # y) we'll subtract y from k
                if (k > second * m):

                    y = second * m
                    k = k - y

                    # incrementing second by two as said in
                    # problem statement
                    second = second + 2

                # if k is smaller than y, then the
                # character
                # will be at position k%m.
                else:

                    # returning character at k index
                    ind = k % m
                    ind-=1
                    if (ind < 0):
                        ind = m - 1
                    output = t[ind]
                    break

            # if k is smaller than x, then the character
            # is at position k%n
            else:

                # returning character at k index
                ind = k % n
                ind-=1
                if (ind < 0):
                    ind = n - 1
                output = s[ind]
                break

        return output

# Driver code
S1 = "a"
S2 = "bc"
k = 4
ans = KthCharacter(S1, S2, k)
print(ans)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to solve the above approach
using System;

public class GFG {
    static char Kthchar(String s, String t, long k)
    {

        // storing length
        long n = s.Length;
        long m = t.Length;

        // variables for temporary strings of s and t
        long first = 1;
        long second = 2;

        // readonly output variable
        char output = '?';
        while (k > 0) {

            // if k is greater than even after adding string
            // 's' 'first' times  (let's call it x) we'll
            // subtract x from k
            if (k > first * n) {

                long x = first * n;
                k = k - x;

                // incrementing first by 2, as said in
                // problem statement
                first = first + 2;

                // if k is greater than even after adding
                // string 't' 'second' times  (let's call it
                // y) we'll subtract y from k
                if (k > second * m) {

                    long y = second * m;
                    k = k - y;

                    // incrementing second by two as said in
                    // problem statement
                    second = second + 2;
                }

                // if k is smaller than y, then the
                // character
                // will be at position k%m.
                else {

                    // returning character at k index
                    long ind = k % m;
                    ind--;
                    if (ind < 0)
                        ind = m - 1;
                    output = t[(int)(ind)];
                    break;
                }
            }

            // if k is smaller than x, then the character
            // is at position k%n
            else {

                // returning character at k index
                long ind = k % n;
                ind--;
                if (ind < 0)
                    ind = n - 1;
                output = s[(int)(ind)];
                break;
            }
        }
        return output;
    }

    // Driver code
    public static void Main(String[] args)
    {

        String S1 = "a", S2 = "bc";
        int k = 4;
        char ans = Kthchar(S1, S2, k);
        Console.WriteLine(ans);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// javascript program to solve the above approach

   function KthCharacter(s, t , k)
    {
        // storing length
        var n = s.length;
        var m = t.length;

        // variables for temporary strings of s and t
        var first = 1;
        var second = 2;

        // final output variable
        var output = '?';
        while (k > 0) {

            // if k is greater than even after adding string
            // 's' 'first' times  (let's call it x) we'll
            // subtract x from k
            if (k > first * n) {

                var x = first * n;
                k = k - x;

                // incrementing first by 2, as said in
                // problem statement
                first = first + 2;

                // if k is greater than even after adding
                // string 't' 'second' times  (let's call it
                // y) we'll subtract y from k
                if (k > second * m) {

                    var y = second * m;
                    k = k - y;

                    // incrementing second by two as said in
                    // problem statement
                    second = second + 2;
                }

                // if k is smaller than y, then the
                // character
                // will be at position k%m.
                else {

                    // returning character at k index
                    var ind = k % m;
                    ind--;
                    if (ind < 0)
                        ind = m - 1;
                    output = t.charAt(parseInt(ind));
                    break;
                }
            }

            // if k is smaller than x, then the character
            // is at position k%n
            else {

                // returning character at k index
                var ind = k % n;
                ind--;
                if (ind < 0)
                    ind = n - 1;
                output = s.charAt(parseInt(ind));
                break;
            }
        }
        return output;
    }

    // Driver code

    var S1 = "a", S2 = "bc";
    var k = 4;
    var ans = KthCharacter(S1, S2, k);
    document.write(ans);

// This code contributed by Princi Singh
</script>
```

**Output**

```
b
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*
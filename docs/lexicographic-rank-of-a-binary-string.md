# 二进制字符串的字典排序

> 原文:[https://www . geeksforgeeks . org/词典-二进制字符串排名/](https://www.geeksforgeeks.org/lexicographic-rank-of-a-binary-string/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到给定字符串的[字典顺序。](https://www.geeksforgeeks.org/lexicographic-rank-of-a-string/)

**示例:**

> **输入:** S = "001"
> **输出:** 8
> **解释:**
> 字符串按其排列顺序依次为:
> “0”= 1、
> “1”= 2、
> “00”= 3、
> “01”= 4、
> “10”= 5、
> “11”= 6、
> “000”= 7、
> 
> **输入:**S = " 01 "
> T3】输出: 4

**天真方法:**最简单的方法是生成长度为 **N** 的所有可能的二进制字符串(*由 **0s** 和 **1s*** 组成)，并将它们存储在数组中。完成后，[按照字典顺序对字符串数组进行排序](https://www.geeksforgeeks.org/compare-two-strings-lexicographically-in-java/)并打印数组中给定字符串的索引。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**想法是通过用 **0** 替换每次出现的 **'a'** ，用 **1** 替换 **'b'** ，生成由 **0s** 和 **1s** 组成的二进制字符串。因此，列表中的字符串变成:

> “a”= 0、
> “b”= 1、
> “aa”= 00、
> “ab”= 01、
> “ba”= 10、
> “bb”= 11、
> “AAA”= 000、
> “aab”= 001 等等。

可以观察到，对于大小为 **N** 的弦，在给定弦之前存在长度小于 **N** 的**(2<sup>N</sup>–2)**弦。让它等于 **X** 。现在，它在长度为 **N** 的字符串中的字典位置可以通过[将字符串转换成它的十进制等价数](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)并加 1 来计算。让它等于 **Y** 。

> 一个字符串的秩= X+Y+1
> =(2<sup>N</sup>–2)+Y+1
> = 2<sup>N</sup>+Y–1

下面是上述方法的实现:

## C++

```
//C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the rank of a string
void findRank(string s)
{

  // Store the length of the string
  int N = s.size();

  // Stores its equivalent decimal value
  string bin;

  // Traverse the string
  for (int i = 0; i < N; i++)
  {
    if (s[i] == '0')
      bin += "0";
    else
      bin += "1";
  }

  // Store the number of strings of
  // length less than N occurring
  // before the given string
  long long X = 1ll<<N;

  // Store the decimal equivalent
  // number of string bin
  long long res = 0, val = 1;
  for(int i = N - 1; i >= 0; i--)
  {
    if (bin[i] == '1') 
      res += (val);

    val *= 2ll;
  }

  long long Y = res;

  // Store the rank in answer
  long ans = X + Y - 1;

  // Print the answer
  cout << ans;
}

// Driver program
int main()
{
  string S = "001";
  findRank(S);
  return 0;
}

// This code is contributed by jyoti369.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
public class Main {

    // Function to find the rank of a string
    static void findRank(String s)
    {
        // Store the length of the string
        int N = s.length();

        // Stores its equivalent decimal value
        StringBuilder sb = new StringBuilder("");

        // Traverse the string
        for (int i = 0; i < N; i++) {

            if (s.charAt(i) == '0')
                sb.append('0');
            else
                sb.append('1');
        }

        String bin = sb.toString();

        // Store the number of strings of
        // length less than N occurring
        // before the given string
        long X = (long)Math.pow(2, N);

        // Store the decimal equivalent
        // number of string bin
        long Y = Long.parseLong(bin, 2);

        // Store the rank in answer
        long ans = X + Y - 1;

        // Print the answer
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "001";
        findRank(S);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the rank of a string
def findRank(s):

    # Store the length of the string
    N = len(s);

    # Stores its equivalent decimal value
    sb = "";

    # Traverse the string
    for i in range(0,N):

        if (s[i] == '0'):
            sb += str('0');
        else:
            sb += str('1');

    bin = str(sb);

    # Store the number of strings of
    # length less than N occurring
    # before the given string
    X = pow(2, N);

    # Store the decimal equivalent
    # number of string bin
    Y = int(bin);

    # Store the rank in answer
    ans = X + Y - 1;

    # Prthe answer
    print(ans);

# Driver Code
if __name__ == '__main__':
    S = "001";
    findRank(S);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to find the rank of a String
static void findRank(string s)
{

  // Store the length of the String
  int N = s.Length;

  // Stores its equivalent decimal value
  string bin = "";

  // Traverse the String
  for (int i = 0; i < N; i++)
  {
    if (s[i] == '0')
      bin += "0";
    else
      bin += "1";
  }

  // Store the number of string s of
  // length less than N occurring
  // before the given String
  int X = 1<<N;

  // Store the decimal equivalent
  // number of String bin
  int res = 0, val = 1;
  for(int i = N - 1; i >= 0; i--)
  {
    if (bin[i] == '1') 
      res += (val);

    val *= 2;
  }
  int Y = res;

  // Store the rank in answer
  int ans = X + Y - 1;

  // Print the answer
  Console.Write(ans);
}

// Driver Code
public static void Main()
{
   string S = "001";
    findRank(S);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the rank of a string
function findRank( s)
{

// Store the length of the string
var N = s.length;

// Stores its equivalent decimal value
var bin = "";

// Traverse the string
for (var i = 0; i < N; i++)
{
    if (s[i] == '0')
        bin += "0";
    else
        bin += "1";
}

// Store the number of strings of
// length less than N occurring
// before the given string
var X = 1<<N;

// Store the decimal equivalent
// number of string bin
var res = 0, val = 1;
for(var i = N - 1; i >= 0; i--)
{
    if (bin[i] == '1')
        res += (val);

    val *= 2;
}

var Y = res;

// Store the rank in answer
var ans = X + Y - 1;

// Print the answer
document.write( ans);
}

// Driver program
var S = "001";
findRank(S);

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
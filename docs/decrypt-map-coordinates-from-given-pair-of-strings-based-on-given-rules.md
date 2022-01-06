# 根据给定的规则从给定的字符串对中解密地图坐标

> 原文:[https://www . geesforgeks . org/decrypt-map-coordinates-from-给定字符串对-基于给定规则/](https://www.geeksforgeeks.org/decrypt-map-coordinates-from-given-pair-of-strings-based-on-given-rules/)

给定一对大小为 **M** 和 **N 的小写[字符串](https://www.geeksforgeeks.org/stringstream-c-applications/) **string1[]** 和 **string2[]** ，任务是根据以下规则解密这些字符串。加密的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)的最后一个字符表示方向纬度字符串(只有两个[ **n-North，s-South** )经度字符串(另外两个[ **e-East，w-West** )。除了最后一个字符，该字符串表示整数值，而不管它是纬度字符串还是经度字符串。坐标的整数部分可以解码为([出现次数最多的字母数](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)–[出现次数最少的字符串数](https://www.geeksforgeeks.org/python-least-frequent-character-in-string/))。**

**示例:**

> **输入:**string1[]=“babbeddcs”，string 2[]=“aeeaecacw”
> T3】输出: 2 南 1 西
> T6】说明:在 string 1 中，最后一个字符是 s，所以南方，最频繁的字符是频率为 3 的 b，最少的是频率为 1 的 a、e 和 c。同样，对于另一个字符串，即 string2。
> 
> **输入:**string 1[]=“ddcs”，string 2[]=“aeew”
> T3】输出: 1 南 1 西

**做法:**解决这个问题的思路是统计每个字符串的字符最大和最小出现频率，检查最后一个字符。按照以下步骤解决此问题:

*   将变量 **c1** 和 **c2** 初始化为字符串 **string1【】和 **string2【】的最后一个字符。****
*   [用 **0** 初始化向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)**f1【26】**和**F2【26】**以存储频率。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **string1[]** 和 **string2[]** 和[将字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)的所有字符的频率存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **f1[]** 和 **f2[]。**
*   初始化变量 **ma1、mi1、ma2** 和 **mi2** ，以存储字符串 **string1[]** 和字符串 **string2[]** 的最大和最小出现频率字符。
*   [遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **f1[]** 和 **f2[]** ，存储 **ma1、mi1、ma2** 和 **mi2 的值。**
*   执行上述步骤后，打印上述计算的结果。

下面是上述方法的实现。

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to decrypt the strings
void find(string string1, string string2)
{

    // Size of the strings
    int M = string1.length(),
        N = string2.length();

    // Last characters of the strings
    char c1 = string1[M - 1],
         c2 = string2[N - 1];

    // Arrays to store the frequencies
    vector<int> f1(26, 0), f2(26, 0);

    // Calculate the frequency of characters
    // of both the strings
    for (int i = 0; i < M - 1; i++)
        f1[string1[i] - 'a']++;

    for (int i = 0; i < N - 1; i++)
        f2[string2[i] - 'a']++;

    // Variables to store the maximum and
    // minimum occurring character.
    int ma1 = 0, mi1 = M, ma2 = 0, mi2 = N;

    for (int i = 0; i < 26; i++) {
        ma1 = max(ma1, f1[i]);
        if (f1[i] > 0)
            mi1 = min(mi1, f1[i]);

        ma2 = max(ma2, f2[i]);
        if (f2[i] > 0)
            mi2 = min(mi2, f2[i]);
    }

    // Print the result
    cout << ma1 - mi1 << " ";
    if (c1 == 's')
        cout << "South ";
    else
        cout << "North ";
    cout << ma2 - mi2;
    if (c2 == 'e')
        cout << " East ";
    else
        cout << " West ";
}

// Driver Code
int main()
{

    string string1 = "babbeddcs",
           string2 = "aeeaecacw";

    find(string1, string2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
class GFG
{

// Function to decrypt the strings
static void find(String string1, String string2)
{

    // Size of the strings
    int M = string1.length();
    int N = string2.length();

    // Last characters of the strings
    char c1 = string1.charAt(M - 1);
    char c2 = string2.charAt(N - 1);

    // Arrays to store the frequencies
    int []f1 = new int[26];
    int []f2 = new int[26];

    // Calculate the frequency of characters
    // of both the strings
    for (int i = 0; i < M - 1; i++)
        f1[string1.charAt(i) - 'a']++;

    for (int i = 0; i < N - 1; i++)
        f2[string2.charAt(i) - 'a']++;

    // Variables to store the maximum and
    // minimum occurring character.
    int ma1 = 0, mi1 = M, ma2 = 0, mi2 = N;

    for (int i = 0; i < 26; i++) {
        ma1 = Math.max(ma1, f1[i]);
        if (f1[i] > 0)
            mi1 = Math.min(mi1, f1[i]);

        ma2 = Math.max(ma2, f2[i]);
        if (f2[i] > 0)
            mi2 = Math.min(mi2, f2[i]);
    }

    // Print the result
   System.out.print(ma1 - mi1 + " ");
    if (c1 == 's')
       System.out.print("South ");
    else
        System.out.print( "North ");
  System.out.print(ma2 - mi2);
    if (c2 == 'e')
        System.out.print( " East ");
    else
        System.out.print( " West ");
}

// Driver Code
    public static void main (String[] args) {
         String string1 = "babbeddcs";
         String string2 = "aeeaecacw";

       find(string1, string2);

    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to decrypt the strings
def find(string1, string2):

    # Size of the strings
    M = len(string1)
    N = len(string2)

    # Last characters of the strings
    c1 = string1[M - 1]
    c2 = string2[N - 1]

    # Arrays to store the frequencies
    f1 = [0 for _ in range(26)]
    f2 = [0 for _ in range(26)]

    # Calculate the frequency of characters
    # of both the strings
    for i in range(0, M - 1):
        f1[ord(string1[i]) - ord('a')] += 1

    for i in range(0, N - 1):
        f2[ord(string2[i]) - ord('a')] += 1

    # Variables to store the maximum and
    # minimum occurring character.
    ma1 = 0
    mi1 = M
    ma2 = 0
    mi2 = N

    for i in range(0, 26):
        ma1 = max(ma1, f1[i])
        if (f1[i] > 0):
            mi1 = min(mi1, f1[i])

        ma2 = max(ma2, f2[i])
        if (f2[i] > 0):
            mi2 = min(mi2, f2[i])

    # Print the result
    print(ma1 - mi1, end = " ")
    if (c1 == 's'):
        print("South", end = " ")
    else:
        print("North", end = " ")

    print(ma2 - mi2, end = "")
    if (c2 == 'e'):
        print(" East ", end = "")
    else:
        print(" West ")

# Driver Code
if __name__ == "__main__":

    string1 = "babbeddcs"
    string2 = "aeeaecacw"

    find(string1, string2)

# This code is contributed by rakeshsahni
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{
// Function to decrypt the strings
static void find(string string1, string string2)
{

    // Size of the strings
    int M = string1.Length;
    int N = string2.Length;

    // Last characters of the strings
    char c1 = string1[M - 1];
    char c2 = string2[N - 1];

    // Arrays to store the frequencies
    int []f1 = new int[26];
    int []f2 = new int[26];
    for(int i = 0; i < 26; i++) {
        f1[i] = 0;
        f2[i] = 0;
    }

    // Calculate the frequency of characters
    // of both the strings
    for (int i = 0; i < M - 1; i++)
        f1[string1[i] - 'a']++;

    for (int i = 0; i < N - 1; i++)
        f2[string2[i] - 'a']++;

    // Variables to store the maximum and
    // minimum occurring character.
    int ma1 = 0, mi1 = M, ma2 = 0, mi2 = N;

    for (int i = 0; i < 26; i++) {
        ma1 = Math.Max(ma1, f1[i]);
        if (f1[i] > 0)
            mi1 = Math.Min(mi1, f1[i]);

        ma2 = Math.Max(ma2, f2[i]);
        if (f2[i] > 0)
            mi2 = Math.Min(mi2, f2[i]);
    }

    // Print the result
    Console.Write(ma1 - mi1 + " ");
    if (c1 == 's')
        Console.Write("South ");
    else
        Console.Write("North ");
    Console.Write(ma2 - mi2);
    if (c2 == 'e')
        Console.Write(" East ");
    else
        Console.Write(" West ");
}

// Driver code
public static void Main() {

    string string1 = "babbeddcs";
    string string2 = "aeeaecacw";

    find(string1, string2);
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to decrypt the strings
function find(string1, string2)
{

    // Size of the strings
    let M = string1.length;
    let N = string2.length;

    // Last characters of the strings
    let c1 = string1[M - 1];
    let c2 = string2[N - 1];

    // Arrays to store the frequencies
    let f1 = [], f2 = [];
    for(let i = 0; i < 26; i++) {
        f1[i] = 0;
        f2[i] = 0;
    }

    // Calculate the frequency of characters
    // of both the strings
    for (let i = 0; i < M - 1; i++)
        f1[string1.charCodeAt(i) - 97]++;

    for (let i = 0; i < N - 1; i++)
        f2[string2.charCodeAt(i) - 97]++;

    // Variables to store the maximum and
    // minimum occurring character.
    let ma1 = 0, mi1 = M, ma2 = 0, mi2 = N;

    for (let i = 0; i < 26; i++) {
        ma1 = Math.max(ma1, f1[i]);
        if (f1[i] > 0)
            mi1 = Math.min(mi1, f1[i]);

        ma2 = Math.max(ma2, f2[i]);
        if (f2[i] > 0)
            mi2 = Math.min(mi2, f2[i]);
    }

    // Print the result
    document.write(ma1 - mi1 + " ");
    if (c1 == 's')
        document.write("South ");
    else
        document.write("North ");
    document.write(ma2 - mi2);
    if (c2 == 'e')
        document.write(" East ");
    else
        document.write(" West ");
}

// Driver Code
let string1 = "babbeddcs";
let string2 = "aeeaecacw";

find(string1, string2);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output:** 

```
2 South 1 West
```

***时间复杂度:** O(max(M，N))*
***辅助空间:** O(1)*
# 给定字符串中非等距字符的三元组计数

> 原文:[https://www . geeksforgeeks . org/非等距字符给定字符串的三元组计数/](https://www.geeksforgeeks.org/count-of-triplets-from-the-given-string-with-non-equidistant-characters/)

给定一个包含字母“a”、“b”和“c”的字符串 **s** ，任务是计算由这三个字符组成的所有可能的三元组，它们之间的距离不应该相同。

> 两个字母之间的距离基本上就是它们的指数之差。

**示例:**

> **输入:** s = "aabc"
> **输出:** 1
> **解释:**
> 由‘a’、‘b’和‘c’组成的两个可能的三元组是{1，3，4}和{ 2，3，4}。
> 但是第二个三元组中的字符是等距的。因此，只有一个可能的三元组满足上述条件。
> 
> **输入:**s = " abbcabc "
> T3】输出: 13

**方法:**
要解决上面提到的问题，我们需要遵循下面给出的步骤:

*   统计给定字符串 s 中出现的所有字母“a”、“b”、“c”。
*   通过将它们各自的计数相乘，找出包含 a、b、c 的所有三元组。
*   在此之后，减去索引之间具有相同距离的所有三元组，并打印结果输出。

下面是上述方法的实现:

## C++

```
// C++ Program to count of triplets
// from the given string with
// non-equidistant characters

#include <bits/stdc++.h>
using namespace std;

// Function to count valid triplets
void CountValidTriplet(string s, int n)
{
    // Store frequencies of a, b and c
    int count_a = 0,
        count_b = 0,
        count_c = 0;

    for (int i = 0; i < n; i++) {

        // If the current letter is 'a'
        if (s[i] == 'a')
            count_a++;

        // If the current letter is 'b'
        if (s[i] == 'b')
            count_b++;

        // If the current letter is 'c'
        if (s[i] == 'c')
            count_c++;
    }

    // Calculate total no of triplets
    int Total_triplet = count_a
                        * count_b
                        * count_c;

    // Subtract invalid triplets
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            if ((2 * j - i) < n
                && s[j] != s[i]
                && s[j * 2 - i] != s[j]
                && s[2 * j - i] != s[i])

                Total_triplet--;
        }
    }
    cout << Total_triplet;
}

// Driver Code
int main()
{
    string s = "abcbcabc";

    int n = s.length();

    CountValidTriplet(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of triplets
// from the given string with
// non-equidistant characters
import java.util.*;

class GFG{

// Function to count valid triplets
static void CountValidTriplet(String s, int n)
{

    // Store frequencies of a, b and c
    int count_a = 0,
        count_b = 0,
        count_c = 0;

    for(int i = 0; i < n; i++)
    {

       // If the current letter is 'a'
       if (s.charAt(i) == 'a')
           count_a++;

       // If the current letter is 'b'
       if (s.charAt(i) == 'b')
           count_b++;

       // If the current letter is 'c'
       if (s.charAt(i) == 'c')
           count_c++;
    }

    // Calculate total no of triplets
    int Total_triplet = count_a * count_b * count_c;

    // Subtract invalid triplets
    for(int i = 0; i < n; i++)
    {
       for(int j = i + 1; j < n; j++)
       {
          if ((2 * j - i) < n &&
              s.charAt(j) != s.charAt(i) &&
              s.charAt(j * 2 - i) != s.charAt(j) &&
              s.charAt(2 * j - i) != s.charAt(i))
              Total_triplet--;
       }
    }
    System.out.println(Total_triplet);
}

// Driver code
public static void main(String[] args)
{
    String s = "abcbcabc";
    int n = s.length();

    CountValidTriplet(s, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to count of triplets
# from the given string with
# non-equidistant characters

# Function to count valid triplets
def CountValidTriplet(s, n):

    # Store frequencies of a, b and c
    count_a = 0
    count_b = 0
    count_c = 0

    for i in range(n):

        # If the current letter is 'a'
        if (s[i] == 'a'):
            count_a += 1

        # If the current letter is 'b'
        if (s[i] == 'b'):
            count_b += 1

        # If the current letter is 'c'
        if (s[i] == 'c'):
            count_c += 1

    # Calculate total no of triplets
    Total_triplet = count_a * count_b * count_c

    # Subtract invalid triplets
    for i in range(n):
        for j in range(i + 1, n):

            if ((2 * j - i) < n and
                   s[j] != s[i] and
                   s[j * 2 - i] != s[j] and
                   s[2 * j - i] != s[i]):

                Total_triplet -= 1

    print(Total_triplet)

# Driver Code
s = "abcbcabc"
n = len(s)
CountValidTriplet(s, n)

# This code is contributed by yatinagg
```

## C#

```
// C# program to count of triplets
// from the given string with
// non-equidistant characters
using System;

class GFG{

// Function to count valid triplets
static void CountValidTriplet(string s, int n)
{

    // Store frequencies of a, b and c
    int count_a = 0,
        count_b = 0,
        count_c = 0;

    for(int i = 0; i < n; i++)
    {
       // If the current letter is 'a'
       if (s[i] == 'a')
           count_a++;

       // If the current letter is 'b'
       if (s[i] == 'b')
           count_b++;

       // If the current letter is 'c'
       if (s[i] == 'c')
           count_c++;
    }

    // Calculate total no of triplets
    int Total_triplet = count_a * count_b * count_c;

    // Subtract invalid triplets
    for(int i = 0; i < n; i++)
    {
       for(int j = i + 1; j < n; j++)
       {
          if ((2 * j - i) < n &&
              s[j] != s[i] &&
              s[j * 2 - i] != s[j] &&
              s[2 * j - i] != s[i])
              Total_triplet--;
       }
    }
    Console.Write(Total_triplet);
}

// Driver code
public static void Main()
{
    string s = "abcbcabc";
    int n = s.Length;

    CountValidTriplet(s, n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to count of triplets
// from the given string with
// non-equidistant characters

// Function to count valid triplets
function CountValidTriplet(s, n)
{

    // Store frequencies of a, b and c
    let count_a = 0,
        count_b = 0,
        count_c = 0;

    for(let i = 0; i < n; i++)
    {

        // If the current letter is 'a'
        if (s[i] == 'a')
            count_a++;

        // If the current letter is 'b'
        if (s[i] == 'b')
            count_b++;

        // If the current letter is 'c'
        if (s[i] == 'c')
            count_c++;
    }

    // Calculate total no of triplets
    let Total_triplet = count_a * count_b * count_c;

    // Subtract invalid triplets
    for(let i = 0; i < n; i++)
    {
        for(let j = i + 1; j < n; j++)
        {
            if ((2 * j - i) < n &&
                s[j] != s[i] &&
                s[j * 2 - i] != s[j] &&
                s[2 * j - i] != s[i])
                Total_triplet--;
        }
    }
    document.write(Total_triplet);
}

// Driver code
let s = "abcbcabc";
let n = s.length;

CountValidTriplet(s, n);

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
13
```

**时间复杂度:**T2【O】(N<sup>2</sup>)。其中 N 为给定字符串的长度。
**辅助空间:** O(1)。
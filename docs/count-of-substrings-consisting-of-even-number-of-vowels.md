# 由偶数个元音组成的子串计数

> 原文:[https://www . geesforgeks . org/count-of-substrings-由偶数个元音组成/](https://www.geeksforgeeks.org/count-of-substrings-consisting-of-even-number-of-vowels/)

给定一个长度为 **N** 的字符串 **S** ，任务是找到非空子串的数量，这些子串具有*甚至*数量的[元音](https://www.geeksforgeeks.org/find-substrings-contain-vowels/)。

**示例:**

> **输入:** N = 5，S =“abcde”
> **输出:** 7
> **解释:**
> 所有可能的元音数为偶数的子串为:
> 子串元音
> { abcde } 2
> { b } 0
> { BC } 0
> { BCD } 0
> { c } 0
> { CD } 0
> { d } 0
> **输入:**

**天真方法:**
解决问题最简单的方法是[生成给定字符串的所有可能的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，对于每个子串，统计元音的个数，检查是否为*甚至*。如果发现均匀，增加**计数**。最后，检查所有子串后，打印**计数**的值作为答案。

以下是上述方法的实现:

## C++

```
// C++ program to implement
//the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to check
// if a character is a vowel
bool isVowel(char c)
{
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return true;

    return false;
}

// Function to calculate and return the
// count of substrings with even number
// of vowels
void countSubstrings(string s, int n)
{

    // Stores the count of substrings
    int result = 0;

    for(int i = 0; i < n; i++)
    {
        int count = 0;
        for(int j = i; j < n; j++)
        {

            // If the current character
            // is a vowel
            if (isVowel(s[j]))
            {

                // Increase count
                count++;
            }

            // If substring contains
            // even number of vowels
            if (count % 2 == 0)

                // Increase the answer
                result++;
        }
    }

    // Print the final answer
    cout << result;
}

// Driver Code
int main()
{
    int n = 5;
    string s = "abcde";

    countSubstrings(s, n);
    return 0;
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG {

    // Utility function to check
    // if a character is a vowel
    static boolean isVowel(char c)
    {
        if (c == 'a' || c == 'e' || c == 'i'
            || c == 'o' || c == 'u')
            return true;

        return false;
    }

    // Function to calculate and return the
    // count of substrings with even number
    // of vowels
    static void countSubstrings(String s, int n)
    {

        // Stores the count of substrings
        int result = 0;

        for (int i = 0; i < n; i++) {
            int count = 0;
            for (int j = i; j < n; j++) {

                // If the current character
                // is a vowel
                if (isVowel(s.charAt(j))) {

                    // Increase count
                    count++;
                }

                // If substring contains
                // even number of vowels
                if (count % 2 == 0)

                    // Increase the answer
                    result++;
            }
        }

        // Print the final answer
        System.out.println(result);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        String s = "abcde";
        countSubstrings(s, n);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Utility function to check
# if a character is a vowel
def isVowel(c):

    if (c == 'a' or c == 'e' or
        c == 'i' or c == 'o' or
        c == 'u'):
        return True

    return False

# Function to calculate and return the
# count of substrings with even number
# of vowels
def countSubstrings(s, n):

    # Stores the count of substrings
    result = 0

    for i in range(n):
        count = 0
        for j in range(i, n):

            # If the current character
            # is a vowel
            if (isVowel(s[j])):

                #Increase count
                count += 1

            # If substring contains
            # even number of vowels
            if (count % 2 == 0):

                #Increase the answer
                result += 1

    # Print the final answer
    print(result)

# Driver Code
if __name__ == '__main__':

    n = 5
    s = "abcde"
    countSubstrings(s, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Utility function to check
// if a character is a vowel
static bool isVowel(char c)
{
    if (c == 'a' || c == 'e' || c == 'i' ||
        c == 'o' || c == 'u')
        return true;

    return false;
}

// Function to calculate and return the
// count of substrings with even number
// of vowels
static void countSubstrings(String s, int n)
{

    // Stores the count of substrings
    int result = 0;

    for(int i = 0; i < n; i++)
    {
        int count = 0;
        for(int j = i; j < n; j++)
        {

            // If the current character
            // is a vowel
            if (isVowel(s[j]))
            {

                // Increase count
                count++;
            }

            // If substring contains
            // even number of vowels
            if (count % 2 == 0)

                // Increase the answer
                result++;
        }
    }

    // Print the final answer
    Console.WriteLine(result);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    String s = "abcde";

    countSubstrings(s, n);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Utility function to check
    // if a character is a vowel
    function isVowel(c)
    {
        if (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u')
            return true;

        return false;
    }

    // Function to calculate and return the
    // count of substrings with even number
    // of vowels
    function countSubstrings(s, n)
    {

        // Stores the count of substrings
        let result = 0;

        for(let i = 0; i < n; i++)
        {
            let count = 0;
            for(let j = i; j < n; j++)
            {

                // If the current character
                // is a vowel
                if (isVowel(s[j]))
                {

                    // Increase count
                    count++;
                }

                // If substring contains
                // even number of vowels
                if (count % 2 == 0)

                    // Increase the answer
                    result++;
            }
        }

        // Print the final answer
        document.write(result);
    }

    let n = 5;
    let s = "abcde";

    countSubstrings(s, n);

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**
按照以下步骤优化上述方法:

*   初始化累积计数模数组**温度[]** ，这样:

> **temp[0]** :存储元音数为偶数的子串计数。
> **temp[1]** :存储具有奇数个元音的子串的计数。

*   任何子串**【S】<sub>I</sub>、S<sub>j</sub>**都将包含 ***甚至*** 数量的元音如果**【S<sub>0</sub>、S<sub>I-1</sub>】**中的元音数量与**【S<sub>0</sub>、S<sub>j</sub>**中的元音数量具有相同的奇偶性，
*   由于带有偶数个元音和奇数个元音的子串的计数存储在**temp【】**中，因此，通过使用**握手引理**:

> **子串总数=(temp[0]*(temp[0]–1))/2+(temp[1]*(temp[1]–1))/2**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to check
// if a character is a vowel
bool isVowel(char c)
{
    if (c == 'a' || c == 'e' ||
        c == 'i' || c == 'o' ||
        c == 'u')
        return true;

    return false;
}

// Function to calculate and return the
// count of substrings with even number
// of vowels
void countSubstrings(string s, int n)
{

    // Stores the count of substrings
    // with even and odd number of
    // vowels respectively
    int temp[] = { 1, 0 };

    int result = 0, sum = 0;
    for(int i = 0; i <= n - 1; i++)
    {

        // Update count of vowels modulo 2
        // in sum to obtain even or odd
        sum += (isVowel(s[i]) ? 1 : 0);
        sum %= 2;

        // Increment even/odd count
        temp[sum]++;
    }

    // Count substrings with even number
    // of vowels using Handshaking Lemma
    result += ((temp[0] * (temp[0] - 1)) / 2);
    result += ((temp[1] * (temp[1] - 1)) / 2);

    cout << result;
}

// Driver Code
int main()
{
    int n = 5;
    string s = "abcde";

    countSubstrings(s, n);
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG {

    // Utility function to check
    // if a character is a vowel
    static boolean isVowel(char c)
    {
        if (c == 'a' || c == 'e' || c == 'i'
            || c == 'o' || c == 'u')
            return true;

        return false;
    }

    // Function to calculate and return the
    // count of substrings with even number
    // of vowels
    static void countSubstrings(String s, int n)
    {
        // Stores the count of substrings
        // with even and odd number of
        // vowels respectively
        int temp[] = { 1, 0 };

        int result = 0, sum = 0;
        for (int i = 0; i <= n - 1; i++) {

            // Update count of vowels modulo 2
            // in sum to obtain even or odd
            sum += (isVowel(s.charAt(i)) ? 1 : 0);
            sum %= 2;

            // Increment even/odd count
            temp[sum]++;
        }

        // Count substrings with even number
        // of vowels using Handshaking Lemma
        result += ((temp[0] * (temp[0] - 1)) / 2);
        result += ((temp[1] * (temp[1] - 1)) / 2);

        System.out.println(result);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        String s = "abcde";
        countSubstrings(s, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Utility function to check
# if a character is a vowel
def isVowel(c):

    if (c == 'a' or c == 'e' or
        c == 'i' or c == 'o' or
        c == 'u'):
        return True;

    return False;

# Function to calculate and return the
# count of substrings with even number
# of vowels
def countSubstrings(s, n):

    # Stores the count of substrings
    # with even and odd number of
    # vowels respectively
    temp = [1, 0];

    result = 0;
    sum = 0;
    for i in range(0, n):

        # Update count of vowels modulo 2
        # in sum to obtain even or odd
        sum += (1 if isVowel(s[i]) else 0);
        sum %= 2;

        # Increment even/odd count
        temp[sum] += 1;

    # Count substrings with even number
    # of vowels using Handshaking Lemma
    result += ((temp[0] * (temp[0] - 1)) // 2);
    result += ((temp[1] * (temp[1] - 1)) // 2);

    print(result);

# Driver Code
if __name__ == '__main__':

    n = 5;
    s = "abcde";

    countSubstrings(s, n);

# This code is contributed by amal kumar choubey
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG {

  // Utility function to check
  // if a character is a vowel
  static bool isVowel(char c)
  {
    if (c == 'a' || c == 'e' || c == 'i' ||
        c == 'o' || c == 'u')
      return true;

    return false;
  }

  // Function to calculate and return the
  // count of substrings with even number
  // of vowels
  static void countSubstrings(String s, int n)
  {
    // Stores the count of substrings
    // with even and odd number of
    // vowels respectively
    int []temp = { 1, 0 };

    int result = 0, sum = 0;
    for (int i = 0; i <= n - 1; i++)
    {
      // Update count of vowels modulo 2
      // in sum to obtain even or odd
      sum += (isVowel(s[i]) ? 1 : 0);
      sum %= 2;

      // Increment even/odd count
      temp[sum]++;
    }

    // Count substrings with even number
    // of vowels using Handshaking Lemma
    result += ((temp[0] * (temp[0] - 1)) / 2);
    result += ((temp[1] * (temp[1] - 1)) / 2);

    Console.Write(result);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int n = 5;
    String s = "abcde";
    countSubstrings(s, n);
  }
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>
    // Javascript program to implement
    // the above approach

    // Utility function to check
    // if a character is a vowel
    function isVowel(c)
    {
        if (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u')
            return true;

        return false;
    }

    // Function to calculate and return the
    // count of substrings with even number
    // of vowels
    function countSubstrings(s, n)
    {

        // Stores the count of substrings
        // with even and odd number of
        // vowels respectively
        let temp = [ 1, 0 ];

        let result = 0, sum = 0;
        for(let i = 0; i <= n - 1; i++)
        {

            // Update count of vowels modulo 2
            // in sum to obtain even or odd
            sum += (isVowel(s[i]) ? 1 : 0);
            sum %= 2;

            // Increment even/odd count
            temp[sum]++;
        }

        // Count substrings with even number
        // of vowels using Handshaking Lemma
        result += ((temp[0] * (temp[0] - 1)) / 2);
        result += ((temp[1] * (temp[1] - 1)) / 2);

        document.write(result);
    }

    let n = 5;
    let s = "abcde";

    countSubstrings(s, n);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*
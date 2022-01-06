# 为使每个字符的频率为质数

所要进行的最小字符添加/删除

> 原文:[https://www . geeksforgeeks . org/每个字符的最小添加-移除-要完成的字符-生成频率-质数/](https://www.geeksforgeeks.org/minimum-addition-removal-of-characters-to-be-done-to-make-frequency-of-each-character-prime/)

给定一个长度为 **N** 的字符串 **S** ，任务是找到使每个不同字符的频率为质数所需的最小运算。一个字符的频率可以在一次操作中增加或减少 1。

**示例:**

> **输入:**S =“ABBA”
> T3】输出: 0
> **说明:**字符串 S 中有两个字符，‘a’的频率是 2，是素数。“b”的频率是 2，也是一个质数。因此，这种情况下不需要任何操作。
> 
> **输入:**S = " aaaaaaaaaa "
> T3】输出:2
> T6】说明:字符串中‘a’的出现频率为 9。要么从字符串中删除 2 a，要么在字符串中添加 2 a，使“a”的频率为质数。因此，所需的最小操作数是 2。

**天真方法:**
找到字符串中每个字符的[频率。让频率为 **X** 。找出大于 X 小于 X 的质数，比较 **X** 与找到的两个质数之差，选择最接近的质数。将最接近的质数与 **X** 之差加到运算次数上。因此，将获得最小数量的操作。这是一种低效的方法，因为寻找素数的下限和上限是未知的。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)

**有效方法:**

1.  使用[筛选算法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)到[找到 N 个以内的所有素数](https://www.geeksforgeeks.org/print-all-prime-numbers-less-than-or-equal-to-n/)并将其存储在数组中。
2.  找出从 **i = 1 到 N** 的所有数字的最近的下素数，并将 **i** 与其最近的下素数之差存储在一个数组中，比如 **arr1[]** 。
3.  找出从 **i = 1 到 N** 的所有数字中最近的高素数，并将 **i** 与其最近的高素数之差存储在一个数组中，比如 **arr2[]** 。
4.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)和 f [找到字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)中所有不同字符的频率，并使用[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)保存这些不同字符的频率。
5.  让任意不同字符的频率为 X，然后从数组 **arr1[]** 和 **arr2[]** 中找出 X 与最近素数之间的距离。
6.  选择两者之间较小的距离，并将该距离与操作数相加。
7.  对所有不同的字符执行此操作，最后打印操作数。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

// using the sieve to find
// the prime factors.
void spf_array(int spf[], int d)
{
    spf[1] = 1;
    int i = 0;

    // setting every number
    // as prime number initially
    for (i = 2; i <= d; i++) {
        spf[i] = i;
    }

    // removing the even numbers as
    // they cannot be prime except 2
    for (i = 2; i <= d; i = i + 2) {
        spf[i] = 2;
    }

    for (i = 3; i * i <= d; i++) {
        // if they are prime
        if (spf[i] == i) {
            int j;

            // iterating the loop for
            // prime and eliminate all
            // the multiples of three
            for (j = i * i; j <= d; j = j + i) {
                if (spf[j] == j) {
                    spf[j] = i;
                }
            }
        }
    }
}

// function to find the closest
// prime number of every
// number upto N (size of the string)
void closest_prime_spf(int spf[],
                       int cspf[], int d)
{
    // for the base case
    cspf[1] = 1;

    int i = 0, j = 0, k = 0;

    // iterating to find the
    // distance from the
    // lesser nearest prime
    for (i = 2; i < d; i++) {
        if (spf[i] != i) {
            cspf[i] = abs(i - k);
        }
        else {
            cspf[i] = -1;
            k = i;
        }
    }

    // iterating to find the
    // distance from the
    // lesser nearest prime
    for (i = d - 1; i >= 2; i--) {
        if (spf[i] != i) {
            if (cspf[i] > abs(k - i)) {
                cspf[i] = abs(k - i);
            }
        }
        else {
            k = i;
        }
    }
}

// function to find the
// minimum operation
int minimum_operation(int cspf[],
                      string s)
{

    // created map to find the
    // frequency of distinct characters
    unordered_map<char, int> m;

    // variable to iterate and
    // holding the minimum operation
    int i = 0, k = 0;

    // loop for calculation frequency
    for (i = 0; i < s.length(); i++) {
        m[s[i]] = m[s[i]] + 1;
    }

    // iterate over frequency
    // if we not get a character
    // frequency prime
    // then we find the closest
    // prime and add
    for (auto x : m) {
        int h = x.second;
        if (cspf[h] != -1) {
            k = k + cspf[h];
        }
    }
    return k;
}

// Function to find the
// minimum number of operations
void minOper(string s)
{

    int spf[s.length() + 1];
    int cspf[s.length() + 1];

    // function called to create
    // the spf
    spf_array(spf, s.length() + 1);

    // function called to
    // create the cspf
    closest_prime_spf(spf, cspf,
                      s.length() + 1);

    cout << minimum_operation(cspf, s)
         << endl;
}

// Driver Code
int main()
{
    // input string
    string s = "aaaaaaaaabbcccccc";

    minOper(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Using the sieve to find
// the prime factors.
static void spf_array(int spf[], int d)
{
    spf[1] = 1;
    int i = 0;

    // Setting every number
    // as prime number initially
    for(i = 2; i < d; i++)
    {
        spf[i] = i;
    }

    // Removing the even numbers as
    // they cannot be prime except 2
    for(i = 2; i < d; i = i + 2)
    {
        spf[i] = 2;
    }

    for(i = 3; i * i <= d; i++)
    {

        // If they are prime
        if (spf[i] == i)
        {
            int j;

            // Iterating the loop for
            // prime and eliminate all
            // the multiples of three
            for(j = i * i; j < d; j = j + i)
            {
                if (spf[j] == j)
                {
                    spf[j] = i;
                }
            }
        }
    }
}

// Function to find the closest
// prime number of every
// number upto N (size of the String)
static void closest_prime_spf(int spf[],
                              int cspf[],
                              int d)
{

    // For the base case
    cspf[1] = 1;

    int i = 0, k = 0;

    // Iterating to find the
    // distance from the
    // lesser nearest prime
    for(i = 2; i < d; i++)
    {
        if (spf[i] != i)
        {
            cspf[i] = Math.abs(i - k);
        }
        else
        {
            cspf[i] = -1;
            k = i;
        }
    }

    // Iterating to find the
    // distance from the
    // lesser nearest prime
    for(i = d - 1; i >= 2; i--)
    {
        if (spf[i] != i)
        {
            if (cspf[i] > Math.abs(k - i))
            {
                cspf[i] = Math.abs(k - i);
            }
        }
        else
        {
            k = i;
        }
    }
}

// Function to find the
// minimum operation
static int minimum_operation(int cspf[],
                             String s)
{

    // Created map to find the
    // frequency of distinct characters
    HashMap<Character, Integer> m = new HashMap<>();

    // Variable to iterate and
    // holding the minimum operation
    int i = 0, k = 0;

    // Loop for calculation frequency
    for(i = 0; i < s.length(); i++)
    {
        if (m.containsKey(s.charAt(i)))
            m.put(s.charAt(i),
            m.get(s.charAt(i)) + 1);
        else
            m.put(s.charAt(i), 1);
    }

    // Iterate over frequency
    // if we not get a character
    // frequency prime then we
    // find the closest
    // prime and add
    for(Map.Entry<Character,
                  Integer> x : m.entrySet())
    {
        int h = x.getValue();
        if (cspf[h] != -1)
        {
            k = k + cspf[h];
        }
    }
    return k;
}

// Function to find the
// minimum number of operations
static void minOper(String s)
{
    int []spf = new int[s.length() + 1];
    int []cspf = new int[s.length() + 1];

    // Function called to create
    // the spf
    spf_array(spf, s.length() + 1);

    // Function called to
    // create the cspf
    closest_prime_spf(spf, cspf,
                      s.length() + 1);

    System.out.print(minimum_operation(cspf, s) + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Input String
    String s = "aaaaaaaaabbcccccc";

    minOper(s);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 code for the above approach
from collections import defaultdict

# Using the sieve to find
# the prime factors.
def spf_array(spf, d):

    spf[1] = 1
    i = 0

    # Setting every number as prime
    # number initially and remove
    # even numbers as 2 as they
    # cannot be prime except 2
    for i in range(2, d + 1):
        if (i % 2 == 0):
          spf[i] = 2
        else:
          spf[i] = i

    i = 3
    while i * i <= d:

        # If they are prime
        if (spf[i] == i):

            # Iterating the loop for
            # prime and eliminate all
            # the multiples of three
            j = i * i
            while j < d + 1:
                if (spf[j] == j):
                    spf[j] = i

                j = j + i

        i += 1

# Function to find the closest
# prime number of every number
# upto N (size of the string)
def closest_prime_spf(spf, cspf, d):

    # For the base case
    cspf[1] = 1

    i = 0
    j = 0
    k = 0

    # Iterating to find the
    # distance from the
    # lesser nearest prime
    for i in range(2, d):
        if (spf[i] != i):
            cspf[i] = abs(i - k)
        else:
            cspf[i] = -1
            k = i

    # Iterating to find the
    # distance from the
    # lesser nearest prime
    for i in range(d - 1, 1, -1):
        if (spf[i] != i):
            if (cspf[i] > abs(k - i)):
                cspf[i] = abs(k - i)
        else:
            k = i

# Function to find the
# minimum operation
def minimum_operation(cspf, s):

    # Created map to find the
    # frequency of distinct characters
    m = defaultdict(int)

    # Variable to iterate and
    # holding the minimum operation
    i = 0
    k = 0

    # Loop for calculation frequency
    for i in range(len(s)):
        m[s[i]] = m[s[i]] + 1

    # Iterate over frequency if we
    # not get a character frequency
    # prime then we find the closest
    # prime and add
    #print (cspf)
    for x in m.values():
        h = x

        if (cspf[h] != -1):
            k = k + cspf[h]

    return k

# Function to find the
# minimum number of operations
def minOper(s):

    spf = [0] * (len(s) + 2)
    cspf = [0] * (len(s) + 2)

    # Function called to create
    # the spf
    spf_array(spf, len(s) + 1)

    # Function called to
    # create the cspf
    closest_prime_spf(spf, cspf,
                      len(s) + 1)

    print(minimum_operation(cspf, s))

# Driver Code
if __name__ == "__main__":

    # Input string
    s = "aaaaaaaaabbcccccc"

    minOper(s)

# This code is contributed by chitranayal
```

## C#

```
// C# code for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Using the sieve to find
// the prime factors.
static void spf_array(int []spf,
                      int d)
{
  spf[1] = 1;
  int i = 0;

  // Setting every number
  // as prime number initially
  for(i = 2; i < d; i++)
  {
    spf[i] = i;
  }

  // Removing the even numbers as
  // they cannot be prime except 2
  for(i = 2; i < d; i = i + 2)
  {
    spf[i] = 2;
  }

  for(i = 3; i * i <= d; i++)
  {
    // If they are prime
    if (spf[i] == i)
    {
      int j;

      // Iterating the loop for
      // prime and eliminate all
      // the multiples of three
      for(j = i * i; j < d; j = j + i)
      {
        if (spf[j] == j)
        {
          spf[j] = i;
        }
      }
    }
  }
}

// Function to find the closest
// prime number of every
// number upto N (size of the String)
static void closest_prime_spf(int []spf,
                              int []cspf,
                              int d)
{   
  // For the base case
  cspf[1] = 1;

  int i = 0, k = 0;

  // Iterating to find the
  // distance from the
  // lesser nearest prime
  for(i = 2; i < d; i++)
  {
    if (spf[i] != i)
    {
      cspf[i] = Math.Abs(i - k);
    }
    else
    {
      cspf[i] = -1;
      k = i;
    }
  }

  // Iterating to find the
  // distance from the
  // lesser nearest prime
  for(i = d - 1; i >= 2; i--)
  {
    if (spf[i] != i)
    {
      if (cspf[i] > Math.Abs(k - i))
      {
        cspf[i] = Math.Abs(k - i);
      }
    }
    else
    {
      k = i;
    }
  }
}

// Function to find the
// minimum operation
static int minimum_operation(int []cspf,
                             String s)
{

  // Created map to find the
  // frequency of distinct characters
  Dictionary<char,
             int> m = new Dictionary<char,
                                     int>();

  // Variable to iterate and
  // holding the minimum operation
  int i = 0, k = 0;

  // Loop for calculation
  // frequency
  for(i = 0; i < s.Length; i++)
  {
    if (m.ContainsKey(s[i]))
      m[s[i]] = m[s[i]] + 1;
    else
      m.Add(s[i], 1);
  }

  // Iterate over frequency
  // if we not get a character
  // frequency prime then we
  // find the closest
  // prime and add
  foreach(KeyValuePair<char,
                       int> x in m)
  {
    int h = x.Value;
    if (cspf[h] != -1)
    {
      k = k + cspf[h];
    }
  }
  return k;
}

// Function to find the
// minimum number of operations
static void minOper(String s)
{
  int []spf = new int[s.Length + 1];
  int []cspf = new int[s.Length + 1];

  // Function called to create
  // the spf
  spf_array(spf, s.Length + 1);

  // Function called to
  // create the cspf
  closest_prime_spf(spf, cspf,
                    s.Length + 1);

  Console.Write(minimum_operation(
                cspf, s) + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Input String
  String s = "aaaaaaaaabbcccccc";

  minOper(s);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript code for the
      // above approach
      // Using the sieve to find
      // the prime factors.
      function spf_array(spf, d) {
        spf[1] = 1;
        var i = 0;

        // Setting every number
        // as prime number initially
        for (i = 2; i < d; i++) {
          spf[i] = i;
        }

        // Removing the even numbers as
        // they cannot be prime except 2
        for (i = 2; i < d; i = i + 2) {
          spf[i] = 2;
        }

        for (i = 3; i * i <= d; i++) {
          // If they are prime
          if (spf[i] === i) {
            var j;

            // Iterating the loop for
            // prime and eliminate all
            // the multiples of three
            for (j = i * i; j < d; j = j + i) {
              if (spf[j] === j) {
                spf[j] = i;
              }
            }
          }
        }
      }

      // Function to find the closest
      // prime number of every
      // number upto N (size of the String)
      function closest_prime_spf(spf, cspf, d) {
        // For the base case
        cspf[1] = 1;

        var i = 0,
          k = 0;

        // Iterating to find the
        // distance from the
        // lesser nearest prime
        for (i = 2; i < d; i++) {
          if (spf[i] !== i) {
            cspf[i] = Math.abs(i - k);
          } else {
            cspf[i] = -1;
            k = i;
          }
        }

        // Iterating to find the
        // distance from the
        // lesser nearest prime
        for (i = d - 1; i >= 2; i--) {
          if (spf[i] !== i) {
            if (cspf[i] > Math.abs(k - i)) {
              cspf[i] = Math.abs(k - i);
            }
          } else {
            k = i;
          }
        }
      }

      // Function to find the
      // minimum operation
      function minimum_operation(cspf, s) {
        // Created map to find the
        // frequency of distinct characters
        var m = {};

        // Variable to iterate and
        // holding the minimum operation
        var i = 0,
          k = 0;

        // Loop for calculation
        // frequency
        for (i = 0; i < s.length; i++) {
          if (m.hasOwnProperty(s[i])) m[s[i]] = m[s[i]] + 1;
          else m[s[i]] = 1;
        }

        // Iterate over frequency
        // if we not get a character
        // frequency prime then we
        // find the closest
        // prime and add
        for (const [key, value] of Object.entries(m)) {
          var h = value;
          if (cspf[h] !== -1) {
            k = k + cspf[h];
          }
        }
        return k;
      }

      // Function to find the
      // minimum number of operations
      function minOper(s) {
        var spf = new Array(s.length + 1).fill(0);
        var cspf = new Array(s.length + 1).fill(0);

        // Function called to create
        // the spf
        spf_array(spf, s.length + 1);

        // Function called to
        // create the cspf
        closest_prime_spf(spf, cspf, s.length + 1);

        document.write(minimum_operation(cspf, s) + "<br>");
      }

      // Driver Code
      // Input String
      var s = "aaaaaaaaabbcccccc";

      minOper(s);
    </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间复杂度:** O(N)*
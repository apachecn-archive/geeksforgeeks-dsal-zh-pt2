# 在不删除字符的情况下制作两个字符串字谜所需的最小操作次数|第 2 集

> 原文:[https://www . geeksforgeeks . org/最小操作次数-需要生成两个字符串-不删除字符集的字谜-2/](https://www.geeksforgeeks.org/minimum-number-of-manipulations-required-to-make-two-strings-anagram-without-deletion-of-character-set-2/)

给定两根同等大小的[弦](https://www.geeksforgeeks.org/category/data-structures/c-strings/)T2 和**t**大小 **N** 。一步选择**t【】**的任意字符，替换为另一个字符。返回最小步数，使 **t[]** 成为 **s[]** 的[字谜](http://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。

> **注意:**字符串的字谜是包含具有不同(或相同)顺序的相同字符的字符串。

**示例:**

> **输入:** s = "baa "，t = "aba"
> **输出:** 0
> **说明:**两个字符串包含相同的字符
> 
> **输入:** s = "ddcf "，t = "cedk"
> **输出:** 2
> **说明:**在这里，我们需要更改任意一个字符串中的两个字符，使它们完全相同。我们可以在 s1 中更改“d”和“f ”,或者在 s2 中更改“e”和“k”。

**哈希方法:**哈希方法已经在本文的[集 1 中讨论过。在本文中，我们将研究如何使用地图解决这个问题。](https://www.geeksforgeeks.org/minimum-number-of-manipulations-required-to-make-two-strings-anagram-without-deletion-of-character/)

**方法:**想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)来[存储字符串](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)**s【】**的每个字符的频率，然后在遍历字符串**t【】**[时，检查该字符是否存在于地图](https://www.geeksforgeeks.org/check-key-present-cpp-map-unordered_map/)中。如果是，则将其值减少 **1。**否则，将计数增加 **1。**按照以下步骤解决问题:

*   初始化变量**计数**为 **0** 存储答案。
*   [初始化一个**无序 _ 地图< char，int >**](https://www.geeksforgeeks.org/default-values-in-a-map-in-c-stl/) **一个【】**来存储频率。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下步骤:
    *   [将 **a【我】**的](https://www.geeksforgeeks.org/unordered_map-insert-in-c-stl/)值增加 **1。**
*   [使用变量 **j** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并执行以下任务:
    *   如果 **a[j]** 大于 **0** ，则将 **a[j]** 的值减少 **1。**
    *   否则，将**计数**的值增加 **1。**
*   执行上述步骤后，打印**计数**的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum changes
// to make the 2 strings anagram
int minSteps(string s, string t)
{
    unordered_map<char, int> a;

    // For counting the steps to be changed
    int count = 0;
    for (auto i : s) {

        // Increasing the count if the no.
        // is present
        a[i]++;
    }
    for (auto j : t) {

        // Checking if the element of s is
        // present in t or not
        if (a[j] > 0) {

            // If present than decrease the
            // no. in map by 1
            a[j]--;
        }
        else {

            // If not present
            // increase count by 1
            count++;
        }
    }
    cout << count;

    // Return count
    return count;
}

// Driver Code
int main()
{
    string s = "ddcf", t = "cedk";

    minSteps(s, t);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

  // Function to count the minimum changes
  // to make the 2 Strings anagram
  static int minSteps(String s, String t) {
    HashMap<Character, Integer> a =
      new HashMap<Character, Integer>();

    // For counting the steps to be changed
    int count = 0;
    for (char i : s.toCharArray()) {

      // Increasing the count if the no.
      // is present
      if (a.containsKey(i)) {
        a.put(i, a.get(i) + 1);
      } else {
        a.put(i, 1);
      }

    }
    for (char j : t.toCharArray()) {

      // Checking if the element of s is
      // present in t or not
      if (a.containsKey(j)) {

        // If present than decrease the
        // no. in map by 1
        a.put(j, a.get(j) - 1);
      } else {

        // If not present
        // increase count by 1
        count++;
      }
    }
    System.out.print(count);

    // Return count
    return count;
  }

  // Driver Code
  public static void main(String[] args) {
    String s = "ddcf", t = "cedk";

    minSteps(s, t);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach

# Function to count the minimum changes
# to make the 2 strings anagram
def minSteps(s, t):

    a = {}

    # For counting the steps to be changed
    count = 0

    for i in s:

        # Increasing the count if the no.
        # is present
        if i in a:
            a[i] += 1
        else:
            a[i] = 1

    for j in t:

                # Checking if the element of s is
                # present in t or not
        if j in a:

                        # If present than decrease the
                        # no. in map by 1
            a[j] -= 1

        else:

            # If not present
            # increase count by 1
            count += 1

    print(count)

    # Return count
    return count

# Driver Code
if __name__ == "__main__":

    s = "ddcf"
    t = "cedk"

    minSteps(s, t)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

  // Function to count the minimum changes
  // to make the 2 Strings anagram
  static int minSteps(String s, String t) {
    Dictionary<char, int> a =
      new Dictionary<char, int>();

    // For counting the steps to be changed
    int count = 0;
    foreach (char i in s.ToCharArray()) {

      // Increasing the count if the no.
      // is present
      if (a.ContainsKey(i)) {
        a[i] = a[i] + 1;
      } else {
        a.Add(i, 1);
      }

    }
    foreach (char j in t.ToCharArray()) {

      // Checking if the element of s is
      // present in t or not
      if (a.ContainsKey(j)) {

        // If present than decrease the
        // no. in map by 1
        a[j] = a[j] - 1;
      } else {

        // If not present
        // increase count by 1
        count++;
      }
    }
    Console.Write(count);

    // Return count
    return count;
  }

  // Driver Code
  public static void Main(String[] args) {
    String s = "ddcf", t = "cedk";

    minSteps(s, t);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to count the minimum changes
       // to make the 2 strings anagram
       function minSteps(s, t)
       {
           let a = new Map();

           // For counting the steps to be changed
           let count = 0;
           for (let i of s) {

               // Increasing the count if the no.
               // is present
               if (a.has(i)) {
                   a.set(i, 1)
               }
               else {
                   a.set(i, a.get(i) + 1)
               }
           }
           for (let j of t) {

               // Checking if the element of s is
               // present in t or not
               if (a.has(j)) {

                   // If present than decrease the
                   // no. in map by 1
                   a.set(j, a.get(j) - 1);
               }
               else {

                   // If not present
                   // increase count by 1
                   count++;
               }
           }
           document.write(count);

           // Return count
           return count;
       }

       // Driver Code
       let s = "ddcf", t = "cedk";
       minSteps(s, t);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(max(N，26))*
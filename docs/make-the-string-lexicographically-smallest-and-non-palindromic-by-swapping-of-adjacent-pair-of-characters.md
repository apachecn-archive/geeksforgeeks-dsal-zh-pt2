# 通过相邻字符对的交换使字符串在字典上最小且不重复

> 原文:[https://www . geeksforgeeks . org/通过相邻字符对的交换使字符串按字典顺序最小化和非回文化/](https://www.geeksforgeeks.org/make-the-string-lexicographically-smallest-and-non-palindromic-by-swapping-of-adjacent-pair-of-characters/)

给定由小写字母组成的字符串**字符串**，任务是通过多次交换字符串中的任意一对相邻字符来构建字典上最小的非回文字符串。
如果给定的字符串不能被转换为字典最小的非回文字符串，则打印“**-1”**。

**示例:**

> **输入:** str = "djfbw"
> **输出:** bdfjw
> **解释:**
> 执行以下交换操作，得到字典上最小的非回文字符串:
> 交换‘b’和‘f’，str 变成“djbfw”
> 交换‘j’和‘b’，str 变成“dbjfw”
> 交换‘b’和‘d’，str 变成“bdjfw”
> 交换‘j’
> 现在“bdfjw”是字典序上最小的字符串，不是回文。
> 
> **输入:**str[]=【PPP】
> T3】输出: -1

**天真方法:**想法是生成字符串的所有可能的[排列，并检查它们是否形成回文。打印其中最小的排列。](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*

**高效的方法:**这个想法是检查从给定字符串中可能的最小字符串是否是回文。以下是步骤:

1.  为了获得字典上最小的字符串，[对给定的字符串](https://www.geeksforgeeks.org/sort-string-characters/)进行排序，以递增的顺序排列字符串的字符。
2.  现在，如果排序后的字符串是回文，那么这意味着该字符串只有一种类型的字符，不能排列成不是回文的字符串。
3.  如果它不是回文，那么排序后的字符串在字典上是不是回文的最小字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the lexographically
// smallest string which is non-palindrome
void smallestNonPalindromic(string& s)
{

    // Sort the given string
    sort(s.begin(), s.end());

    // Store reverse of sorted string
    string reversestring
        = string(s.rbegin(), s.rend());

    // Check if the sorted string is
    // palindromic or not
    if (s != reversestring) {
        cout << s;
    }
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    // Given string str
    string str = "asmfjdeovnhekfnj";

    // Function Call
    smallestNonPalindromic(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// reverse string
static String reverse(String input)
{
  char[] a = input.toCharArray();
  int l, r = a.length - 1;
  for (l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.valueOf(a);
}

// Method to sort a string alphabetically
static String sortString(String inputString)
{
  // convert input string to char array
  char tempArray[] = inputString.toCharArray();

  // sort tempArray
  Arrays.sort(tempArray);

  // return new sorted string
  return new String(tempArray);
}

// Function to find the lexographically
// smallest String which is non-palindrome
static void smallestNonPalindromic(String s)
{
  // Sort the given String
  s = sortString(s);

  // Store reverse of sorted String
  String reverseString = reverse(s);

  // Check if the sorted String is
  // palindromic or not
  if (s != reverseString)
  {
    System.out.print(s);
  }

  else
  {
    System.out.print("-1");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given String str
  String str = "asmfjdeovnhekfnj";

  // Function Call
  smallestNonPalindromic(str);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the lexographically
# smallest string which is non-palindrome
def smallestNonPalindromic(s):

    # Sort the given string
    s = sorted(s)

    # Store reverse of sorted string
    reversestring = s[::-1]

    # Check if the sorted string is
    # palindromic or not
    if (s != reversestring):
        print("".join(s))
    else:
        print("-1")

# Driver Code
if __name__ == '__main__':

    # Given string str
    str = "asmfjdeovnhekfnj"

    # Function call
    smallestNonPalindromic(str)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Reverse string
static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;

    for(l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("", a);
}

// Method to sort a string alphabetically
static String sortString(String inputString)
{

    // Convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // Sort tempArray
    Array.Sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Function to find the lexographically
// smallest String which is non-palindrome
static void smallestNonPalindromic(String s)
{

    // Sort the given String
    s = sortString(s);

    // Store reverse of sorted String
    String reverseString = reverse(s);

    // Check if the sorted String is
    // palindromic or not
    if (s != reverseString)
    {
        Console.Write(s);
    }
    else
    {
        Console.Write("-1");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "asmfjdeovnhekfnj";

    // Function call
    smallestNonPalindromic(str);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find the lexographically
      // smallest string which is non-palindrome
      function smallestNonPalindromic(s) {
        var newStr = s.split("");

        // Sort the given string
        newStr.sort().reverse();

        // Store reverse of sorted string
        var reversestring = newStr.reverse().join("");

        // Check if the sorted string is
        // palindromic or not
        if (s !== reversestring) {
          document.write(newStr.join(""));
        } else {
          document.write("-1");
        }
      }

      // Driver Code
      // Given string str
      var str = "asmfjdeovnhekfnj";

      // Function Call
      smallestNonPalindromic(str);
    </script>
```

**Output:** 

```
adeeffhjjkmnnosv
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
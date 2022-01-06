# 可能由最多 K 个连续相似字符组成的字典上最大的字符串

> 原文:[https://www . geesforgeks . org/按字典顺序排列的最大可能字符串由最多 k 个连续相似字符组成/](https://www.geeksforgeeks.org/lexicographically-largest-string-possible-consisting-of-at-most-k-consecutive-similar-characters/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个整数 **K** ，任务是通过移除最多由 **K** 个连续相似字符组成的字符，从给定字符串中按字典顺序生成最大可能的字符串。

**示例:**

> **输入:** S = "baccc "，K = 2
> **输出:** ccbca
> 
> **输入:** S = "ccbbb "，K = 2
> T3】输出: ccbb

**方法:**按照以下步骤解决问题:

1.  初始化一个数组**字符集[]** 来存储字符串中每个字符的[频率。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)
2.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并存储数组中每个字符的频率。
3.  初始化一个变量**计数**来存储相似连续字符的计数
4.  初始化字符串**新字符串**以存储结果字符串。
5.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **字符集[]** 并将 **(i +'a')** 追加到**新字符串**。
6.  减少**字符集【I】**并增加**计数**。
7.  检查**计数是否= K** 和**字符集[i] > 0** ，然后从**字符集[]** 中找到最近的较小字符，并追加到**新字符串**中。如果最近的较小字符不可用，则打印**新闻字符串**
8.  否则，将**计数**重置为 **0** 。
9.  重复步骤 2 至 5，直到**字符集【I】>0**
10.  最后，返回**新闻字符串**。

**以下是上述方法的实施:**

## C++14

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return nearest
// lower character
char nextAvailableChar(vector<int> charset,
                       int start)
{
  // Traverse charset from start-1
  for (int i = start - 1; i >= 0; i--)
  {
    if (charset[i] > 0)
    {
      charset[i]--;
      return char(i + 'a');
    }
  }
  // If no character can be
  // appended
  return '\0';
}

// Function to find largest string
string newString(string originalLabel,
                 int limit)
{
  int n = originalLabel.length();

  // Stores the frequency of
  // characters
  vector<int> charset(26, 0);

  string newStrings = "";

  for(char i : originalLabel)
    charset[i - 'a']++;

  // Traverse the string
  for (int i = 25; i >= 0; i--)
  {
    int count = 0;

    // Append larger character
    while (charset[i] > 0)
    {
      newStrings += char(i + 'a');

      // Decrease count in charset
      charset[i]--;

      // Increase count
      count++;

      // Check if count reached
      // to charLimit
      if (charset[i] > 0 &&
          count == limit)
      {
        // Find nearest lower char
        char next = nextAvailableChar(charset, i);

        // If no character can be
        // appended
        if (next == '\0')
          return newStrings;

        // Append nearest lower
        // character
        newStrings += next;

        // Reset count for next
        // calculation
        count = 0;
      }
    }
  }

  // Return new largest string
  return newStrings;
}

//Driver code
int main()
{
  //Given string s
  string S = "ccbbb";

  int K = 2;
  cout << (newString(S, K));
}

// This code is contributed by Mohit Kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java solution for above approach
import java.util.*;

class GFG {

    // Function to find largest string
    static String newString(String originalLabel,
                            int limit)
    {
        int n = originalLabel.length();
        // Stores the frequency of characters
        int[] charset = new int[26];

        // Traverse the string
        for (int i = 0; i < n; i++) {
            charset[originalLabel.charAt(i) - 'a']++;
        }

        // Stores the resultant string
        StringBuilder newString
            = new StringBuilder(n);

        for (int i = 25; i >= 0; i--) {

            int count = 0;

            // Append larger character
            while (charset[i] > 0) {

                newString.append((char)(i + 'a'));

                // Decrease count in charset
                charset[i]--;

                // Increase count
                count++;

                // Check if count reached to charLimit
                if (charset[i] > 0 && count == limit) {

                    // Find nearest lower char
                    Character next
                        = nextAvailableChar(charset, i);

                    // If no character can be appended
                    if (next == null)
                        return newString.toString();

                    // Append nearest lower character
                    newString.append(next);

                    // Reset count for next calculation
                    count = 0;
                }
            }
        }

        // Return new largest string
        return newString.toString();
    }

    // Function to return nearest lower character
    static Character nextAvailableChar(int[] charset,
                                       int start)
    {
        // Traverse charset from start-1
        for (int i = start - 1; i >= 0; i--) {

            if (charset[i] > 0) {

                charset[i]--;
                return (char)(i + 'a');
            }
        }
        // If no character can be appended
        return null;
    }
    // Driver Code
    public static void main(String[] args)
    {
        String S = "ccbbb";
        int K = 2;
        System.out.println(newString(S, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to return nearest
# lower character
def nextAvailableChar(charset,
                      start):

    # Traverse charset from start-1
    for i in range(start - 1,
                   -1, -1):
        if (charset[i] > 0):
            charset[i] -= 1
            return chr(i + ord('a'))

    # If no character can be
    # appended
    return '\0'

# Function to find largest
# string
def newString(originalLabel,
              limit):

    n = len(originalLabel)

    # Stores the frequency of
    # characters
    charset = [0] * (26)

    newStrings = ""

    for i in originalLabel:
        charset[ord(i) -
                ord('a')] += 1

    # Traverse the string
    for i in range(25, -1, -1):
        count = 0

        # Append larger character
        while (charset[i] > 0):
            newStrings += chr(i + ord('a'))

            # Decrease count in
            # charset
            charset[i] -= 1

            # Increase count
            count += 1

            # Check if count reached
            # to charLimit
            if (charset[i] > 0 and
                count == limit):

                # Find nearest lower char
                next = nextAvailableChar(charset, i)

                # If no character can be
                # appended
                if (next == '\0'):
                    return newStrings

                # Append nearest lower
                # character
                newStrings += next

                # Reset count for next
                # calculation
                count = 0

    # Return new largest string
    return newStrings

# Driver code
if __name__ == "__main__":

    # Given string s
    S = "ccbbb"

    K = 2
    print(newString(S, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# solution for above
// approach
using System;
using System.Text;
class GFG{

// Function to find largest string
static String newString(String originalLabel,
                        int limit)
{
  int n = originalLabel.Length;

  // Stores the frequency of
  // characters
  int[] charset = new int[26];

  // Traverse the string
  for (int i = 0; i < n; i++)
  {
    charset[originalLabel[i] - 'a']++;
  }

  // Stores the resultant string
  StringBuilder newString =
                new StringBuilder(n);

  for (int i = 25; i >= 0; i--)
  {
    int count = 0;

    // Append larger character
    while (charset[i] > 0)
    {
      newString.Append((char)(i + 'a'));

      // Decrease count in charset
      charset[i]--;

      // Increase count
      count++;

      // Check if count reached
      // to charLimit
      if (charset[i] > 0 &&
          count == limit)
      {
        // Find nearest lower char
        char next =
             nextAvailableChar(charset, i);

        // If no character can be
        // appended
        if (next == 0)
          return newString.ToString();

        // Append nearest lower
        // character
        newString.Append(next);

        // Reset count for next
        // calculation
        count = 0;
      }
    }
  }

  // Return new largest string
  return newString.ToString();
}

// Function to return nearest
// lower character
static char nextAvailableChar(int[] charset,
                              int start)
{
  // Traverse charset from start-1
  for (int i = start - 1; i >= 0; i--)
  {
    if (charset[i] > 0)
    {
      charset[i]--;
      return (char)(i + 'a');
    }
  }

  // If no character can
  // be appended
  return '\0';
}

// Driver Code
public static void Main(String[] args)
{
  String S = "ccbbb";
  int K = 2;
  Console.WriteLine(
          newString(S, K));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript solution for above approach

    // Function to find largest string
    function newString(originalLabel,limit)
    {
        let n = originalLabel.length;

        // Stores the frequency of characters
        let charset = new Array(26);
         for(let i = 0; i < 26; i++)
        {
            charset[i] = 0;
        }

        // Traverse the string
        for (let i = 0; i < n; i++) {
            charset[originalLabel[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        // Stores the resultant string
        let newString = [];

        for (let i = 25; i >= 0; i--) {

            let count = 0;

            // Append larger character
            while (charset[i] > 0) {

                newString.push(String.fromCharCode(i + 'a'.charCodeAt(0)));

                // Decrease count in charset
                charset[i]--;

                // Increase count
                count++;

                // Check if count reached to charLimit
                if (charset[i] > 0 && count == limit) {

                    // Find nearest lower char
                    let next
                        = nextAvailableChar(charset, i);

                    // If no character can be appended
                    if (next == null)
                        return newString.join("");

                    // Append nearest lower character
                    newString.push(next);

                    // Reset count for next calculation
                    count = 0;
                }
            }
        }

        // Return new largest string
        return newString.join("");
    }

    // Function to return nearest lower character
    function nextAvailableChar(charset,start)
    {
        // Traverse charset from start-1
        for (let i = start - 1; i >= 0; i--) {

            if (charset[i] > 0) {

                charset[i]--;
                return String.fromCharCode(i + 'a'.charCodeAt(0));
            }
        }
        // If no character can be appended
        return null;
    }

    // Driver Code
    let S = "ccbbb";
    let K = 2;
    document.write(newString(S, K));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
ccbb
```

***时间复杂度:** O(N)，其中 N 是给定字符串的长度*
***辅助空间:** O(1)*
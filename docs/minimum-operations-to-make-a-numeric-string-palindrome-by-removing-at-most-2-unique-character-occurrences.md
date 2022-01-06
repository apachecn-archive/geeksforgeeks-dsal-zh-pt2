# 通过最多删除 2 个唯一字符来进行数字字符串回文的最小操作

> 原文:[https://www . geeksforgeeks . org/minimum-operations-to-make-a-numeric-string-回文-通过最多移除 2 个唯一字符-出现次数/](https://www.geeksforgeeks.org/minimum-operations-to-make-a-numeric-string-palindrome-by-removing-at-most-2-unique-character-occurrences/)

给定数字串**串**，任务是找到使串[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)所需的**最小**运算。操作定义为:

*   选择一个**字符**并删除其任何**事件**。
*   对于所有操作来说，选择的**唯一**字符的数量必须比 **2** 少

****示例**:**

> ****输入** : str = "11221"
> **输出** : 1
> **解释**:选择‘1’，从给定字符串的前两个字符中删除任何字符。运算后字符串变成“1221”，是回文。**
> 
> ****输入** : str = "1123211"
> **输出** : 0
> **解释**:给定的字符串已经是回文了。**
> 
>  ****输入** : str = "1332"
> **输出** : -1
> **说明**:选择单个字符后，仅删除所选字符的出现次数，该字符串不能成为回文。**

****进场:**这个问题可以借助[两点](https://www.geeksforgeeks.org/two-pointers-technique/)进场解决。
按照以下步骤解决问题:**

1.  **将变量**的答案**初始化为 n，存储我们的最终答案(n 是字符串的长度)。**
2.  **迭代“0”到“9”，我们称之为 currentCharacter。**
3.  **将**初始化为 **0** 移除**。它存储要从字符串中删除的最小字符数**当前字符**类型，使其成为回文。**
4.  **将 **i** 和 **j** 分别初始化为 **0** 和**n–1**。**
5.  **将一个**可能的**初始化为**真**。它帮助我们确定是否有可能通过仅删除字符 c 的出现来使字符串成为回文。**
6.  **现在运行嵌套的**同时**循环，直到 **i** 小于 **j** 。

    *   情况 1: str[i]等于 str[j]，这意味着我们在当前步骤中不需要删除任何字符，因此我们可以增加 I 和减少 j。
    *   情况 2: str[i]不等于 str[j]，但 str[i]等于 currentCharacter。增加 **i = i + 1** 和**tobe removed = tobe removed+1**来移除这个角色。
    *   情况 3: str[i]不等于 str[j]，但 str[j]等于 currentCharacter。增加**j = j–1**和**移除=移除+ 1** 来移除这个角色
    *   情况 4: str[i]不等于 str[j]。这意味着我们不能通过删除**currentcharter 来使我们的字符串成为回文。**** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
void solve(string str)
{
    // Length of the string
    int n = str.length();

    // answer variable for final answer
    // initializing it with INF
    int answer = n;

    // Iterating over characters
    // from '0' to '9' (string
    // consist of those characters only)
    for (char currentCharacter = '0';
         currentCharacter <= '9';
         currentCharacter++) {

        // i and j variables to check corresponding
        // characters from the start and the end
        int i = 0, j = n - 1;

        // toBeRemoved store the character of type
        // currentCharacter to be removed
        // to make the string palindrome

        int toBeRemoved = 0;
        bool possible = true;
        while (i < j) {
            // If corresponding currentCharacters are
            // already same
            if (str[i] == str[j]) {
                i++, j--;
            }

            // If corresponding currentCharacters are
            // not same and str[i] is equal to
            // currentCharacter
            // remove it and check for str[i + 1] and
            // str[j] in the next iteration
            else if (str[i] != str[j]
                     && str[i] == currentCharacter) {
                toBeRemoved++;
                i++;
            }

            // If corresponding currentCharacters are
            // not same and str[j] is equal to
            // currentCharacter
            // remove it and check for str[j - 1] and
            // str[i] in the next iteration
            else if (str[i] != str[j]
                     && str[j] == currentCharacter) {
                toBeRemoved++;
                j--;
            }

            // Character of currentCharacter type
            // can't be removed
            // to make the str palindrome.
            // Hence, we mark possible to false
            // break out of the loop
            else {
                possible = false;
                break;
            }
        }

        // If it is possible to remove
        // some occurences of currentCharacters
        // we will update our answer
        if (possible)

            // Take the minimum value out
            // of answer and toBeRemoved
            answer = min(answer, toBeRemoved);
    }

    // Print the final answer
    if (answer == n)
        cout << "-1";
    else
        cout << answer;
}

// Driver Code
int main()
{
    // Given string
    string str = "11221";
    solve(str);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code for the above approach
import java.io.*;

class GFG
{

  // Function to find the minimum operations
  static void solve(String str)
  {
    // Length of the string
    int n = str.length();

    // answer variable for final answer
    // initializing it with INF
    int answer = n;

    // Iterating over characters
    // from '0' to '9' (string
    // consist of those characters only)
    for (char currentCharacter = '0';
         currentCharacter <= '9';
         currentCharacter++) {

      // i and j variables to check corresponding
      // characters from the start and the end
      int i = 0, j = n - 1;

      // toBeRemoved store the character of type
      // currentCharacter to be removed
      // to make the string palindrome

      int toBeRemoved = 0;
      boolean possible = true;
      while (i < j) {
        // If corresponding currentCharacters are
        // already same
        if (str.charAt(i) == str.charAt(j)) {
          i++; j--;
        }

        // If corresponding currentCharacters are
        // not same and str[i] is equal to
        // currentCharacter
        // remove it and check for str[i + 1] and
        // str[j] in the next iteration
        else if (str.charAt(i) != str.charAt(j)
                 && str.charAt(i) == currentCharacter) {
          toBeRemoved++;
          i++;
        }

        // If corresponding currentCharacters are
        // not same and str[j] is equal to
        // currentCharacter
        // remove it and check for str[j - 1] and
        // str[i] in the next iteration
        else if (str.charAt(i) != str.charAt(j)
                 && str.charAt(j)  == currentCharacter) {
          toBeRemoved++;
          j--;
        }

        // Character of currentCharacter type
        // can't be removed
        // to make the str palindrome.
        // Hence, we mark possible to false
        // break out of the loop
        else {
          possible = false;
          break;
        }
      }

      // If it is possible to remove
      // some occurences of currentCharacters
      // we will update our answer
      if (possible)

        // Take the minimum value out
        // of answer and toBeRemoved
        answer = Math.min(answer, toBeRemoved);
    }

    // Print the final answer
    if (answer == n)
      System.out.println("-1");
    else
      System.out.println(answer);
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given string
    String str = "11221";
    solve(str);
  }
}

// This code is contributed by lokeshpotta20.
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to find the minimum operations
def solve(str):

    # Length of the string
    n = len(str)

    # answer variable for final answer
    # initializing it with INF
    answer = n;
    currentCharacter = '0'

    # Iterating over characters
    # from '0' to '9' (string
    # consist of those characters only)
    while(currentCharacter <= '9'):

        # i and j variables to check corresponding
        # characters from the start and the end
        i = 0
        j = n - 1

        # toBeRemoved store the character of type
        # currentCharacter to be removed
        # to make the string palindrome
        toBeRemoved = 0
        possible = True
        while (i < j):

            # If corresponding currentCharacters are
            # already same
            if (str[i] == str[j]):
                i += 1
                j -= 1

            # If corresponding currentCharacters are
            # not same and str[i] is equal to
            # currentCharacter
            # remove it and check for str[i + 1] and
            # str[j] in the next iteration
            elif (str[i] != str[j] and str[i] == currentCharacter):
                toBeRemoved += 1   
                i += 1

            # If corresponding currentCharacters are
            # not same and str[j] is equal to
            # currentCharacter
            # remove it and check for str[j - 1] and
            # str[i] in the next iteration
            elif (str[i] != str[j] and str[j] == currentCharacter):
                toBeRemoved += 1
                j -= 1

            # Character of currentCharacter type
            # can't be removed
            # to make the str palindrome.
            # Hence, we mark possible to false
            # break out of the loop
            else:
                possible = False;
                break;

            currentCharacter = f"{int(currentCharacter) + 1}"

        # If it is possible to remove
        # some occurences of currentCharacters
        # we will update our answer
        if (possible):

            # Take the minimum value out
            # of answer and toBeRemoved
            answer = min(answer, toBeRemoved);

    # Print the final answer
    if (answer == n):
        print("-1");
    else:
        print(answer);

# Driver Code

# Given string
str = "11221";
solve(str);

# This code is contributed by Saurabh Jaiswal
```

## **C#**

```
// C# program for above approach
using System;
class GFG
{

// Function to find the minimum operations
static void solve(string str)
{
    // Length of the string
    int n = str.Length;

    // answer variable for final answer
    // initializing it with INF
    int answer = n;

    // Iterating over characters
    // from '0' to '9' (string
    // consist of those characters only)
    for (char currentCharacter = '0';
         currentCharacter <= '9';
         currentCharacter++) {

        // i and j variables to check corresponding
        // characters from the start and the end
        int i = 0, j = n - 1;

        // toBeRemoved store the character of type
        // currentCharacter to be removed
        // to make the string palindrome

        int toBeRemoved = 0;
        bool possible = true;
        while (i < j) {
            // If corresponding currentCharacters are
            // already same
            if (str[i] == str[j]) {
                i++;
                j--;
            }

            // If corresponding currentCharacters are
            // not same and str[i] is equal to
            // currentCharacter
            // remove it and check for str[i + 1] and
            // str[j] in the next iteration
            else if (str[i] != str[j]
                     && str[i] == currentCharacter) {
                toBeRemoved++;
                i++;
            }

            // If corresponding currentCharacters are
            // not same and str[j] is equal to
            // currentCharacter
            // remove it and check for str[j - 1] and
            // str[i] in the next iteration
            else if (str[i] != str[j]
                     && str[j] == currentCharacter) {
                toBeRemoved++;
                j--;
            }

            // Character of currentCharacter type
            // can't be removed
            // to make the str palindrome.
            // Hence, we mark possible to false
            // break out of the loop
            else {
                possible = false;
                break;
            }
        }

        // If it is possible to remove
        // some occurences of currentCharacters
        // we will update our answer
        if (possible)

            // Take the minimum value out
            // of answer and toBeRemoved
            answer = Math.Min(answer, toBeRemoved);
    }

    // Print the final answer
    if (answer == n)
        Console.Write("-1");
    else
        Console.Write(answer);
}

// Driver Code
public static void Main()
{
    // Given string
    string str = "11221";
    solve(str);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to find the minimum operations
function solve(str)
{
    // Length of the string
    let n = str.length;

    // answer variable for final answer
    // initializing it with INF
    let answer = n;

    // Iterating over characters
    // from '0' to '9' (string
    // consist of those characters only)
    for (let currentCharacter = '0';
         currentCharacter <= '9';
         currentCharacter++) {

        // i and j variables to check corresponding
        // characters from the start and the end
        let i = 0, j = n - 1;

        // toBeRemoved store the character of type
        // currentCharacter to be removed
        // to make the string palindrome

        let toBeRemoved = 0;
        let possible = true;
        while (i < j) {
            // If corresponding currentCharacters are
            // already same
            if (str[i] == str[j]) {
                i++;
                j--;
            }

            // If corresponding currentCharacters are
            // not same and str[i] is equal to
            // currentCharacter
            // remove it and check for str[i + 1] and
            // str[j] in the next iteration
            else if (str[i] != str[j]
                     && str[i] == currentCharacter) {
                toBeRemoved++;
                i++;
            }

            // If corresponding currentCharacters are
            // not same and str[j] is equal to
            // currentCharacter
            // remove it and check for str[j - 1] and
            // str[i] in the next iteration
            else if (str[i] != str[j]
                     && str[j] == currentCharacter) {
                toBeRemoved++;
                j--;
            }

            // Character of currentCharacter type
            // can't be removed
            // to make the str palindrome.
            // Hence, we mark possible to false
            // break out of the loop
            else {
                possible = false;
                break;
            }
        }

        // If it is possible to remove
        // some occurences of currentCharacters
        // we will update our answer
        if (possible)

            // Take the minimum value out
            // of answer and toBeRemoved
            answer = Math.min(answer, toBeRemoved);
    }

    // Print the final answer
    if (answer == n)
        document.write("-1");
    else
        document.write(answer);
}

// Driver Code

// Given string
let str = "11221";
solve(str);

// This code is contributed by Samim Hossain Mondal.
</script>
```

****Output**

```
1
```** 

*****时间复杂度*** **:** O(10 * n) = O(n)，其中 n 为字符串的长度。
***辅助空间*** **:** O(1)**
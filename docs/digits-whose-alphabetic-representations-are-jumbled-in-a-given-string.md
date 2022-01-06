# 字母表示混杂在给定字符串中的数字

> 原文:[https://www . geesforgeks . org/digits-其字母表示在给定的字符串中是混杂的/](https://www.geeksforgeeks.org/digits-whose-alphabetic-representations-are-jumbled-in-a-given-string/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，该字符串是范围**【0–9】**中任意数字的英文表示，格式混乱。任务是从这个表示中找到数字。
***注:**按任意顺序打印数字*

**示例**

> **输入:**S = " owoftnoer "
> T3】输出: 124
> **说明:**这里的数字是一、二、四的乱码形式。因此，所需的输出可以是 124 或 421 或 214 等。
> 
> **输入**:S =
> 输出 : 0016

**方法:**通过观察一个有趣的事实可以很容易地解决这个问题，即所有偶数都至少有一个字符不存在于任何其他字符串中，而所有奇数都没有:

> 以下数字有唯一的字母:
> 
> *   **零:**只有带 **z** 的数字
> *   **二:**只有数字带 **w**
> *   **四:**只有数字带 **u**
> *   **六:**只有数字加上 **x**
> *   **八:**仅数字带 **g**

对于奇数，每个字母也会出现在其他数字中。单词中的奇数是{一、三、五、七、九}。按照下面给出的步骤解决问题

*   创建一个字符串向量 **num** 来保存从 **0** 到 **9** 的英文字母数字，以及一个整数向量[T7，**count【】**的大小为 **10** ，还创建一个答案字符串 **ans** 来显示数字。](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)
*   现在，[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)从 **i = 0 到 N-1** 。
*   如果 **s[i] = 'z'** ，将**计数【0】**增加 **1** 。
*   如果 **s[i] = 'w'** ，将**计数【2】**增加 **1** 。
*   如果 **s[i] = 'g'** ，将**计数【8】**增加 **1** 。
*   如果 **s[i] = 'x'** ，将**计数【6】**增加 **1** 。
*   如果 **s[i] = 'v'** ，将**计数【5】**增加 **1** 。
*   如果 **s[i] = 'o'** ，将**计数【1】**增加 **1** 。
*   如果 **s[i] = 's'** ，将**计数【7】**增加 **1** 。
*   如果 **s[i] = 'f'** ，将**计数【4】**增加 **1** 。
*   如果 **s[i] = 'h'** ，将**计数【3】**增加 **1** 。
*   如果 **s[i] = 'i'** ，将**计数【9】**增加 **1** 。
*   现在，更新[向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)的元素，如下所示:

> *   **Count [7] = Count [7]–Count [6]** .
> *   **Count [5] = Count [5]–Count [7]** .
> *   **Count [4] = Count [4]–Count [5]** .
> *   **Count [1] = Count [1]–(Count [2]+Count [4]+Count [0])**
> *   **Count [3] = Count [3]–Count [8]** .
> *   **Count [9] = Count [9]–(Count [5]+Count [6]+Count [8])**

*   现在，[遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)从 **0 到 9** 并追加字符 **(i + '0')** 到 **ans** ，**计数【I】**次。
*   最后打印 **ans** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert the jumbled
// string into digits
string finddigits(string s)
{

    // Strings of digits 0-9
    string num[]
        = { "zero", "one", "two",
            "three", "four", "five",
            "six", "seven", "eight", "nine" };

    // Initialize vector
    vector<int> arr(10);

    // Initialize answer
    string ans = "";

    // Size of the string
    int n = s.size();

    // Traverse the string
    for (int i = 0; i < n; i++) {
        if (s[i] == 'z')
            arr[0]++;
        if (s[i] == 'w')
            arr[2]++;
        if (s[i] == 'g')
            arr[8]++;
        if (s[i] == 'x')
            arr[6]++;
        if (s[i] == 'v')
            arr[5]++;
        if (s[i] == 'o')
            arr[1]++;
        if (s[i] == 's')
            arr[7]++;
        if (s[i] == 'f')
            arr[4]++;
        if (s[i] == 'h')
            arr[3]++;
        if (s[i] == 'i')
            arr[9]++;
    }

    // Update the elements of the vector
    arr[7] -= arr[6];
    arr[5] -= arr[7];
    arr[4] -= arr[5];
    arr[1] -= (arr[2] + arr[4] + arr[0]);
    arr[3] -= arr[8];
    arr[9] -= (arr[5] + arr[6] + arr[8]);

    // Print the digits into their
    // original format
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < arr[i]; j++) {
            ans += (char)(i + '0');
        }
    }

    // Return answer
    return ans;
}

// Driver Code
int main()
{
    string s = "owoftnuoer";
    cout << finddigits(s) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

  // Function to convert the jumbled
  // string into digits
  static String finddigits(String s)
  {

    // Strings of digits 0-9
    String[] num
      = { "zero", "one", "two",   "three", "four",
         "five", "six", "seven", "eight", "nine" };

    // Initialize vector
    int[] arr = new int[10];

    // Initialize answer
    String ans = "";

    // Size of the string
    int n = s.length();

    // Traverse the string
    for (int i = 0; i < n; i++) {
      if (s.charAt(i) == 'z')
        arr[0]++;
      if (s.charAt(i) == 'w')
        arr[2]++;
      if (s.charAt(i) == 'g')
        arr[8]++;
      if (s.charAt(i) == 'x')
        arr[6]++;
      if (s.charAt(i) == 'v')
        arr[5]++;
      if (s.charAt(i) == 'o')
        arr[1]++;
      if (s.charAt(i) == 's')
        arr[7]++;
      if (s.charAt(i) == 'f')
        arr[4]++;
      if (s.charAt(i) == 'h')
        arr[3]++;
      if (s.charAt(i) == 'i')
        arr[9]++;
    }

    // Update the elements of the vector
    arr[7] -= arr[6];
    arr[5] -= arr[7];
    arr[4] -= arr[5];
    arr[1] -= (arr[2] + arr[4] + arr[0]);
    arr[3] -= arr[8];
    arr[9] -= (arr[5] + arr[6] + arr[8]);

    // Print the digits into their
    // original format
    for (int i = 0; i < 10; i++) {
      for (int j = 0; j < arr[i]; j++) {
        ans += (char)(i + '0');
      }
    }

    // Return answer
    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {
    String s = "owoftnuoer";
    System.out.println(finddigits(s));
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to convert the jumbled
# into digits
def finddigits(s):

    # Strings of digits 0-9
    num = [ "zero", "one", "two", "three",
            "four", "five", "six", "seven",
            "eight", "nine"]

    # Initialize vector
    arr = [0] * (10)

    # Initialize answer
    ans = ""

    # Size of the string
    n = len(s)

    # Traverse the string
    for i in range(n):
        if (s[i] == 'z'):
            arr[0] += 1
        if (s[i] == 'w'):
            arr[2] += 1
        if (s[i] == 'g'):
            arr[8] += 1
        if (s[i] == 'x'):
            arr[6] += 1
        if (s[i] == 'v'):
            arr[5] += 1
        if (s[i] == 'o'):
            arr[1] += 1
        if (s[i] == 's'):
            arr[7] += 1
        if (s[i] == 'f'):
            arr[4] += 1
        if (s[i] == 'h'):
            arr[3] += 1
        if (s[i] == 'i'):
            arr[9] += 1

    # Update the elements of the vector
    arr[7] -= arr[6]
    arr[5] -= arr[7]
    arr[4] -= arr[5]
    arr[1] -= (arr[2] + arr[4] + arr[0])
    arr[3] -= arr[8]
    arr[9] -= (arr[5] + arr[6] + arr[8])

    # Print the digits into their
    # original format
    for i in range(10):
        for j in range(arr[i]):
            ans += chr((i) + ord('0'))

    # Return answer
    return ans

# Driver Code
if __name__ == '__main__':

    s = "owoftnuoer"

    print(finddigits(s))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to convert the jumbled
  // string into digits
  static string finddigits(string s)
  {

    // Initialize vector
    int[] arr = new int[10];

    // Initialize answer
    string ans = "";

    // Size of the string
    int n = s.Length;

    // Traverse the string
    for (int i = 0; i < n; i++) {
      if (s[i] == 'z')
        arr[0]++;
      if (s[i] == 'w')
        arr[2]++;
      if (s[i] == 'g')
        arr[8]++;
      if (s[i] == 'x')
        arr[6]++;
      if (s[i] == 'v')
        arr[5]++;
      if (s[i] == 'o')
        arr[1]++;
      if (s[i] == 's')
        arr[7]++;
      if (s[i] == 'f')
        arr[4]++;
      if (s[i] == 'h')
        arr[3]++;
      if (s[i] == 'i')
        arr[9]++;
    }

    // Update the elements of the vector
    arr[7] -= arr[6];
    arr[5] -= arr[7];
    arr[4] -= arr[5];
    arr[1] -= (arr[2] + arr[4] + arr[0]);
    arr[3] -= arr[8];
    arr[9] -= (arr[5] + arr[6] + arr[8]);

    // Print the digits into their
    // original format
    for (int i = 0; i < 10; i++) {
      for (int j = 0; j < arr[i]; j++) {
        ans += (char)(i + '0');
      }
    }

    // Return answer
    return ans;
  }

  // Driver Code
  static public void Main()
  {
    string s = "owoftnuoer";
    Console.WriteLine(finddigits(s));
  }
}

// This code is contributed by Dharanendra L V
```

**Output:** 

```
124
```

***时间复杂度:** O(N)其中 **N** 是* [*字符串的长度*](https://www.geeksforgeeks.org/find-length-of-a-string-in-python-4-ways/)
***辅助空间:** O(N)*
# 要选择的字符串的最大数量，以便有一个多数字符

> 原文:[https://www . geeksforgeeks . org/待选字符串的最大数量-存在多数字符/](https://www.geeksforgeeks.org/maximum-count-of-strings-to-be-selected-such-that-there-is-a-majority-character/)

给定一个由[小写字符](https://www.geeksforgeeks.org/count-uppercase-lowercase-special-character-numeric-values/)组成的字符串的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A[]****N**[，任务是找到最大数量的字符串，使得一个字符占多数，即一个字符在所有字符串中的出现次数大于所有其他字符的总和。](https://www.geeksforgeeks.org/category/data-structures/c-strings/)

**示例:**

> **输入:**A[]= {“ABA”、“abcde”、“ABA”}
> **输出:** 2
> **说明:**在选择{“ABA”、“ABA”}时，字符‘A’的出现次数为 4，其余字符的出现次数为 2，小于 4。因此，最多可以选择 2 个字符串。
> 
> **输入:**A[]= {“bzc”、“zzzdz”、“e”}
> **输出:** 3
> **说明:**所有的字符串都可以选择，其中‘z’占多数。

**方法:**这个问题有[贪婪](https://www.geeksforgeeks.org/greedy-algorithms/)的解决方案。想法是，考虑从**‘a’**到**‘z’**的所有小写字符，对于每个字符，找到可以选择的最大字符串数，这样该字符的出现次数大于所有其他字符的总和。答案是最多。现在的主要问题是如何找到字符串的最大数量，使得一个特定的字符占多数，解决这个问题使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)。其思想是，为了找到特定字符**‘ch’的最大字符串数，**尝试选择**‘ch’**的出现次数相对于所有其他字符的出现次数最多的字符串，即**(ch’的出现次数–所有其他字符的出现次数)**为**最大值的字符串**，这样将来就有可能添加更多的字符串。

按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **CalDif(字符串 s，char ch)** ，并执行以下任务:
    *   将变量 **chcount** 初始化为 **0** 以存储该字符的计数，将 **othercount** 初始化为 **0** 以存储其他字符的计数。
    *   使用变量 **x** 遍历字符串 **s** ，并执行以下任务:
        *   如果当前位置的字符为 **ch、**，则通过 **1** 增加 **chcount** 的值，否则通过 **1 增加 **othercount** 的值。**
    *   返回 **chcount** 和 **othercount 之间的差值。**
*   初始化变量**和**，分配 **0** ，将存储最终答案。
*   [使用变量 **i** 遍历小写字符范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【a，z】**，并执行以下步骤:
    *   [初始化一个长度为 **N** 的向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **arr[]** ，其中**arr【I】**将为 **i-th** 字符串存储**(ch 的出现–所有其他字符的出现)**。
    *   [运行从 **i=0** 到 **N-1** 的循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)
        *   对于第 **i <sup>个</sup>** 字符串，使用[功能](https://www.geeksforgeeks.org/functions-in-c/) **计算**(出现 ch–出现所有其他字符)**并将其分配给**arr【I】**。**
    *   [按降序排列](https://www.geeksforgeeks.org/quick-sort/) **arr[]** 。
    *   初始化两个变量**温度**和**计数**并将 **0** 分配给它们。
    *   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，做**temp+= arr[I]****计数++** ，其中 **i** 从 **0** 开始，直到 **temp < = 0** 。
    *   设置 **ans** 和 **count** 的 **ans** 最大值。
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate (occurrence of ch -
// occurrence of all other characters combined)
int CalDiff(string s, char ch)
{
    // Initialize ch count as 0
    int chcount = 0;

    // Initialize all other char count as 0
    int othercount = 0;

    // Traversing the string
    for (auto x : s) {
        // Current character is ch
        if (x == ch)
            chcount++;
        // Current character is not ch
        else
            othercount++;
    }

    // Return the final result
    return (chcount - othercount);
}

// Function to calculate maximum number of string
// with one character as majority
int MaximumNumberOfString(string A[], int N)
{
    // Initializing ans with 0, to store final answer
    int ans = 0;

    // For every character from 'a' to 'z' run loop
    for (char ch = 'a'; ch <= 'z'; ch++) {

        // Initialize arr to store character count
        // difference
        vector<int> arr(N);

        // Traverse every string
        for (int i = 0; i < N; i++) {

            // Calculate the required value by
            // function call and assign it to arr[i]
            arr[i] = CalDiff(A[i], ch);
        }

        // Sort arr[] in decreasing order
        sort(arr.begin(), arr.end(), greater<int>());

        // Initialize temp and count as 0
        int temp = 0, count = 0;

        // Adding the first arr[] element to temp
        temp += arr[0];

        // Maintaining j as index
        int j = 1;

        // Run loop until temp <= 0
        while (temp > 0) {
            // Increasing count
            count++;

            // Adding temp with next arr[] element
            if (j != N)
                temp += arr[j++];
            else
                break;
        }

        // Set ans as max of ans and count
        ans = max(ans, count);
    }

    // Returning the final result
    return ans;
}

// Driver Code
int main()
{
    // Input
    string A[] = { "aba", "abcde", "aba" };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << MaximumNumberOfString(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to calculate (occurrence of ch -
// occurrence of all other characters combined)
static int CalDiff(String s, char ch)
{

    // Initialize ch count as 0
    int chcount = 0;

    // Initialize all other char count as 0
    int othercount = 0;

    // Traversing the String
    for (int x : s.toCharArray())
    {

        // Current character is ch
        if (x == ch)
            chcount++;

        // Current character is not ch
        else
            othercount++;
    }

    // Return the final result
    return (chcount - othercount);
}

// Function to calculate maximum number of String
// with one character as majority
static int MaximumNumberOfString(String A[], int N)
{

    // Initializing ans with 0, to store final answer
    int ans = 0;

    // For every character from 'a' to 'z' run loop
    for (char ch = 'a'; ch <= 'z'; ch++) {

        // Initialize arr to store character count
        // difference
       int []arr = new int[N];

        // Traverse every String
        for (int i = 0; i < N; i++) {

            // Calculate the required value by
            // function call and assign it to arr[i]
            arr[i] = CalDiff(A[i], ch);
        }

        // Sort arr[] in decreasing order
        Arrays.sort(arr);
        arr = reverse(arr);

        // Initialize temp and count as 0
        int temp = 0, count = 0;

        // Adding the first arr[] element to temp
        temp += arr[0];

        // Maintaining j as index
        int j = 1;

        // Run loop until temp <= 0
        while (temp > 0)
        {

            // Increasing count
            count++;

            // Adding temp with next arr[] element
            if (j != N)
                temp += arr[j++];
            else
                break;
        }

        // Set ans as max of ans and count
        ans = Math.max(ans, count);
    }

    // Returning the final result
    return ans;
}
static int[] reverse(int a[]) {
    int i, n = a.length, t;
    for (i = 0; i < n / 2; i++) {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    String A[] = { "aba", "abcde", "aba" };
    int N = A.length;

    // Function call
    System.out.print(MaximumNumberOfString(A, N));

}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to calculate (occurrence of ch -
# occurrence of all other characters combined)
def CalDiff(s, ch):
    # Initialize ch count as 0
    chcount = 0

    # Initialize all other char count as 0
    othercount = 0

    # Traversing the string
    for x in s:
        # Current character is ch
        if (x == ch):
            chcount += 1
        # Current character is not ch
        else:
            othercount += 1

    # Return the final result
    return (chcount - othercount)

# Function to calculate maximum number of string
# with one character as majority
def MaximumNumberOfString(A, N):
    # Initializing ans with 0, to store final answer
    ans = 0

    # For every character from 'a' to 'z' run loop
    for ch in range(97,123,1):
        # Initialize arr to store character count
        # difference
        arr = [0 for i in range(N)]

        # Traverse every string
        for i in range(N):
            # Calculate the required value by
            # function call and assign it to arr[i]
            arr[i] = CalDiff(A[i], chr(ch))

        # Sort arr[] in decreasing order
        arr.sort(reverse = True)

        # Initialize temp and count as 0
        temp = 0
        count = 0

        # Adding the first arr[] element to temp
        temp += arr[0]

        # Maintaining j as index
        j = 1

        # Run loop until temp <= 0
        while (temp > 0):
            # Increasing count
            count += 1

            # Adding temp with next arr[] element
            if (j != N):
                temp += arr[j]
                j += 1
            else:
                break

        # Set ans as max of ans and count
        ans = max(ans, count)

    # Returning the final result
    return ans

# Driver Code
if __name__ == '__main__':
    # Input
    A = ["aba", "abcde", "aba"]
    N = len(A)

    # Function call
    print(MaximumNumberOfString(A, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate (occurrence of ch -
// occurrence of all other characters combined)
static int CalDiff(string s, char ch)
{

    // Initialize ch count as 0
    int chcount = 0;

    // Initialize all other char count as 0
    int othercount = 0;

    // Traversing the String
    foreach(int x in s.ToCharArray())
    {

        // Current character is ch
        if (x == ch)
            chcount++;

        // Current character is not ch
        else
            othercount++;
    }

    // Return the final result
    return(chcount - othercount);
}

// Function to calculate maximum number of String
// with one character as majority
static int MaximumNumberOfString(string[] A, int N)
{

    // Initializing ans with 0, to store final answer
    int ans = 0;

    // For every character from 'a' to 'z' run loop
    for(char ch = 'a'; ch <= 'z'; ch++)
    {

        // Initialize arr to store character count
        // difference
        int []arr = new int[N];

        // Traverse every String
        for(int i = 0; i < N; i++)
        {

            // Calculate the required value by
            // function call and assign it to arr[i]
            arr[i] = CalDiff(A[i], ch);
        }

        // Sort arr[] in decreasing order
        Array.Sort(arr);
        arr = reverse(arr);

        // Initialize temp and count as 0
        int temp = 0, count = 0;

        // Adding the first arr[] element to temp
        temp += arr[0];

        // Maintaining j as index
        int j = 1;

        // Run loop until temp <= 0
        while (temp > 0)
        {

            // Increasing count
            count++;

            // Adding temp with next arr[] element
            if (j != N)
                temp += arr[j++];
            else
                break;
        }

        // Set ans as max of ans and count
        ans = Math.Max(ans, count);
    }

    // Returning the final result
    return ans;
}

static int[] reverse(int[] a)
{
    int i, n = a.Length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void Main(String []args)
{

    // Input
    string[] A = { "aba", "abcde", "aba" };
    int N = A.Length;

    // Function call
    Console.WriteLine(MaximumNumberOfString(A, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate (occurrence of ch -
// occurrence of all other characters combined)
function CalDiff(s, ch) {
  // Initialize ch count as 0
  let chcount = 0;

  // Initialize all other char count as 0
  let othercount = 0;

  // Traversing the string
  for (let x of s) {
    // Current character is ch
    if (x == ch) chcount++;
    // Current character is not ch
    else othercount++;
  }

  // Return the final result
  return chcount - othercount;
}

// Function to calculate maximum number of string
// with one character as majority
function MaximumNumberOfString(A, N) {
  // Initializing ans with 0, to store final answer
  let ans = 0;

  // For every character from 'a' to 'z' run loop
  for (let ch = "a".charCodeAt(0); ch <= "z".charCodeAt(0); ch++) {
    // Initialize arr to store character count
    // difference
    let arr = new Array(N);

    // Traverse every string
    for (let i = 0; i < N; i++) {
      // Calculate the required value by
      // function call and assign it to arr[i]
      arr[i] = CalDiff(A[i], String.fromCharCode(ch));
    }

    // Sort arr[] in decreasing order
    arr.sort((a, b) => b - a);

    // Initialize temp and count as 0
    let temp = 0,
      count = 0;

    // Adding the first arr[] element to temp
    temp += arr[0];

    // Maintaining j as index
    let j = 1;

    // Run loop until temp <= 0
    while (temp > 0) {
      // Increasing count
      count++;

      // Adding temp with next arr[] element
      if (j != N) temp += arr[j++];
      else break;
    }

    // Set ans as max of ans and count
    ans = Math.max(ans, count);
  }

  // Returning the final result
  return ans;
}

// Driver Code

// Input
let A = ["aba", "abcde", "aba"];
let N = A.length;

// Function call
document.write(MaximumNumberOfString(A, N));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(N * |s|)，其中|s|为最大字符串长度。*
***辅助空间:** O(N)*
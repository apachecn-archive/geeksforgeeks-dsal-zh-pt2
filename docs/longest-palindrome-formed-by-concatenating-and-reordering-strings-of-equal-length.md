# 由长度相等的字符串串联和重新排序形成的最长回文

> 原文:[https://www . geesforgeks . org/最长回文-通过连接和重新排序等长字符串形成/](https://www.geeksforgeeks.org/longest-palindrome-formed-by-concatenating-and-reordering-strings-of-equal-length/)

给定一个由等长的 **N** 串 **M** 组成的数组 **arr[]** ，任务是通过串联这些串来创建最长的回文。也可以从给定的字符串集合中重新排序和丢弃一些字符串。

**示例:**

> **输入:** N = 3，arr[]= {“tab”，“one”，“bat”}，M = 3
> **输出:** tabbat
> 说明:
> 在给定的一组输入字符串中组合“tab”和“bat”时，形成最长的回文字符串。
> 
> **输入:** N = 4，arr[]= {“oo”、“ox”、“xo”、“xx”}，M = 2
> **输出:** oxxxxo

**观察:**假设我们从给定的数组中选择了一些 **K** 字符串，在选择这些 K 字符串后得到的字符串是回文。那么需要对可能的 K 值进行的观察是:

*   **K is even:** Then for every integer x (1 <= x <= K/2):

    ```
    Sx = rev(SK - x + 1)

    ```

    比如构成回文最长的字符串是 S<sub>1</sub>=“tab”，S<sub>2</sub>=“ab”，S<sub>3</sub>=“ba”，S<sub>4</sub>=“bat”。这里，K = 4。因此，S <sub>1</sub> = rev(S <sub>4</sub> )和 S <sub>2</sub> = rev(S <sub>3</sub> )。

*   **K 为奇数:**除上述观察外，中弦 **S <sub>(K+1)/2</sub>** 为回文。

**逼近:**很明显，从上面的观察，要得到最大的回文，给定的数组还必须包含字符串的逆序。因此，对于每一个字符串，我们发现是否有另一个字符串是它的反串。如果存在，那么我们把这一对字符串分别加到左端和右端。如果有一个或多个字符串本身是回文，选择其中任何一个，并将其放在中间。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// Longest palindrome that can be formed
// by concatenating and reordering
// given N strings of equal length
#include <bits/stdc++.h>
using namespace std;

// Function to print the longest palindrome
void printPalindrome(vector<string> left,
                     string mid, vector<string> right)
{
    // Printing every string in left vector
    for (string x : left)
        cout << x;

    // Printing the palindromic string
    // in the middle
    cout << mid;

    // Printing the reverse of the right vector
    // to make the final output palindromic
    reverse(right.begin(), right.end());
    for (string x : right)
        cout << x;

    cout << endl;
}

// Function to find and print the
// longest palindrome that can be formed
void findPalindrome(vector<string>& S, int N, int M)
{
    set<string> dict;
    for (int i = 0; i < M; i++) {
        cin >> S[i];
        // Inserting each string in the set
        dict.insert(S[i]);
    }

    // Vectors to add the strings
    // in the left and right side
    vector<string> left, right;

    // To add the already present palindrome
    // string in the middle of the solution
    string mid;

    // Iterating through all the given strings
    for (int i = 0; i < N; i++) {
        string t = S[i];
        reverse(t.begin(), t.end());

        // If the string is a palindrome
        // it is added in the middle
        if (t == S[i])
            mid = t;

        // Checking if the reverse
        // of the string is already
        // present in the set
        else if (dict.find(t) != dict.end()) {
            left.push_back(S[i]);
            right.push_back(t);
            dict.erase(S[i]);
            dict.erase(t);
        }
    }

    printPalindrome(left, mid, right);
}

// Driver code
int main()
{
    vector<string> S{ "tab", "one", "bat" };
    int M = 3;
    int N = S.size();
    findPalindrome(S, N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// Longest palindrome that can be formed
// by concatenating and reordering
// given N Strings of equal length
import java.util.*;

class GFG{

// Function to print the longest palindrome
static void printPalindrome(Vector<String> left,
                     String mid, Vector<String> right)
{
    // Printing every String in left vector
    for (String x : left)
        System.out.print(x);

    // Printing the palindromic String
    // in the middle
    System.out.print(mid);

    // Printing the reverse of the right vector
    // to make the final output palindromic
    Collections.reverse(right);
    for (String x : right)
        System.out.print(x);

    System.out.println();
}

// Function to find and print the
// longest palindrome that can be formed
static void findPalindrome(Vector<String> S, int N, int M)
{
    HashSet<String> dict = new HashSet<String>();
    for (int i = 0; i < M; i++) {
        // Inserting each String in the set
        dict.add(S.get(i));
    }

    // Vectors to add the Strings
    // in the left and right side
    Vector<String> left = new Vector<String>(), right = new Vector<String>();

    // To add the already present palindrome
    // String in the middle of the solution
    String mid="";

    // Iterating through all the given Strings
    for (int i = 0; i < N; i++) {
        String t = S.get(i);
        t = reverse(t);

        // If the String is a palindrome
        // it is added in the middle
        if (t == S.get(i))
            mid = t;

        // Checking if the reverse
        // of the String is already
        // present in the set
        else if (dict.contains(t)) {
            left.add(S.get(i));
            right.add(t);
            dict.remove(S.get(i));
            dict.remove(t);
        }
    }

    printPalindrome(left, mid, right);
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
} 
// Driver code
public static void main(String[] args)
{
    String arr[] = { "tab", "one", "bat" };
    Vector<String> S = new Vector<String>(Arrays.asList(arr));
    int M = 3;
    int N = S.size();
    findPalindrome(S, N, M);
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Function to print the longest palindrome
def printPalindrome(left,mid,right):

    # Printing every string in left vector
    for x in left:
        print(x, end="")

    # Printing the palindromic string
    # in the middle
    print(mid, end="")

    # Printing the reverse of the right vector
    # to make the final output palindromic
    right = right[::-1]
    for x in right:
        print(x, end = "")

    print('\n', end = "")

# Function to find and print the
# longest palindrome that can be formed
def findPalindrome(S, N, M):
    d = set()
    for i in range(M):
        # Inserting each string in the set
        d.add(S[i])

    # Vectors to add the strings
    # in the left and right side
    left = []
    right = []

    # To add the already present palindrome
    # string in the middle of the solution
    mid = ""

    # Iterating through all the given strings
    for i in range(N):
        t = S[i]
        t = t[::-1]

        # If the string is a palindrome
        # it is added in the middle
        if (t == S[i]):
            mid = t

        # Checking if the reverse
        # of the string is already
        # present in the set
        elif (t in d):
            left.append(S[i])
            right.append(t)
            d.remove(S[i])
            d.remove(t)

    printPalindrome(left, mid, right)

# Driver code
if __name__ == '__main__':
    S = ["tab", "one", "bat"]
    M = 3
    N = len(S)
    findPalindrome(S, N, M)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find the
// longest palindrome that can be formed
// by concatenating and reordering
// given N Strings of equal length
using System;
using System.Collections.Generic;

class GFG{

// Function to print the longest palindrome
static void printPalindrome(List<String> left,
                    String mid, List<String> right)
{
    // Printing every String in left vector
    foreach (String x in left)
        Console.Write(x);

    // Printing the palindromic String
    // in the middle
    Console.Write(mid);

    // Printing the reverse of the right vector
    // to make the readonly output palindromic
    right.Reverse();
    foreach (String x in right)
        Console.Write(x);

    Console.WriteLine();
}

// Function to find and print the
// longest palindrome that can be formed
static void findPalindrome(List<String> S, int N, int M)
{
    HashSet<String> dict = new HashSet<String>();
    for (int i = 0; i < M; i++) {

        // Inserting each String in the set
        dict.Add(S[i]);
    }

    // Lists to add the Strings
    // in the left and right side
    List<String> left = new List<String>(), 
    right = new List<String>();

    // To add the already present palindrome
    // String in the middle of the solution
    String mid="";

    // Iterating through all the given Strings
    for (int i = 0; i < N; i++) {
        String t = S[i];
        t = reverse(t);

        // If the String is a palindrome
        // it is added in the middle
        if (t == S[i])
            mid = t;

        // Checking if the reverse
        // of the String is already
        // present in the set
        else if (dict.Contains(t)) {
            left.Add(S[i]);
            right.Add(t);
            dict.Remove(S[i]);
            dict.Remove(t);
        }
    }

    printPalindrome(left, mid, right);
}
static String reverse(String input) {
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
} 

// Driver code
public static void Main(String[] args)
{
    String []arr = { "tab", "one", "bat" };
    List<String> S = new List<String>(arr);
    int M = 3;
    int N = S.Count;
    findPalindrome(S, N, M);
}
}

// This code is contributed by Princi Singh
```

**Output:**

```
tabbat

```
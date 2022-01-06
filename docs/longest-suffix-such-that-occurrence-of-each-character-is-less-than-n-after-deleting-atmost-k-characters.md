# 最长后缀，删除 atmost K 个字符后每个字符出现次数小于 N

> 原文:[https://www . geesforgeks . org/最长后缀-每个字符的出现次数小于删除后的 n-Atmos-k-characters/](https://www.geeksforgeeks.org/longest-suffix-such-that-occurrence-of-each-character-is-less-than-n-after-deleting-atmost-k-characters/)

给定一个字符串 **S** 和两个整数 **N** 和 **K** ，任务是找到最大长度后缀，使得后缀字符串中每个字符的出现次数小于 **N** 和 atmat**K**元素可以从输入字符串中删除，以获得最大长度后缀。
**举例:**

> **输入:**S =“iahagafedcba”，N = 1，K = 0
> **输出:** fedcba
> **解释:**
> 给定字符串
> 中的最大长度后缀，这样每个字符出现一次就是“fedcba”，
> 因为如果我们取字符串“afedcba”，
> 那么字符“a”出现一次就是 2。
> **输入:**S =“iahagafedcba”，N = 1，K = 2
> **输出:** hgfedcba
> **解释:**
> 给定字符串中的最大长度后缀
> 这样每个字符出现一次就是“hgfedcba”，
> 在删除字符“a”两次之后。

**方法:**想法是使用[哈希映射](https://www.geeksforgeeks.org/hashing-data-structure/)来存储字符串的字符频率。

*   初始化一个空字符串以存储该字符串的最长后缀。
*   使用循环从最后迭代字符串–
    *   将字符在哈希映射中的出现次数增加 1
    *   如果当前字符的出现次数小于 N，则将该字符添加到后缀字符串中
    *   否则，如果 K 值大于 0，则将 K 值减 1
*   打印后缀字符串。

以下是上述方法的实现:

## C++

```
// C++ implementation to find
// longest suffix of the string
// such that occurrence of each
// character is less than K
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// length suffix in the string
void maximumSuffix(string s,
               int n, int k){

    // Length of the string
    int i = s.length() - 1;

    // Map to store the number
    // of occurrence of character
    int arr[26] = { 0 };
    string suffix = "";

    // Loop to iterate string
    // from the last character
    while (i > -1) {

        int index = s[i] - 'a';

        // Condition to check if the
        // occurrence of each character
        // is less than given number
        if (arr[index] < n) {
            arr[index]++;
            suffix += s[i];
            i--;
            continue;
        }

        // Condition when character
        // cannot be deleted
        if (k == 0)
            break;
        k--;
        i--;
    }
    reverse(suffix.begin(), suffix.end());

    // Longest suffix
    cout << suffix;
}

// Driver Code
int main()
{
    string str = "iahagafedcba";

    int n = 1, k = 2;

    // Function call
    maximumSuffix(str, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// longest suffix of the String
// such that occurrence of each
// character is less than K
class GFG{

// Function to find the maximum
// length suffix in the String
static void maximumSuffix(String s,
            int n, int k){

    // Length of the String
    int i = s.length() - 1;

    // Map to store the number
    // of occurrence of character
    int arr[] = new int[26];
    String suffix = "";

    // Loop to iterate String
    // from the last character
    while (i > -1) {

        int index = s.charAt(i) - 'a';

        // Condition to check if the
        // occurrence of each character
        // is less than given number
        if (arr[index] < n) {
            arr[index]++;
            suffix += s.charAt(i);
            i--;
            continue;
        }

        // Condition when character
        // cannot be deleted
        if (k == 0)
            break;
        k--;
        i--;
    }
    suffix = reverse(suffix);

    // Longest suffix
    System.out.print(suffix);
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

// Driver Code
public static void main(String[] args)
{
    String str = "iahagafedcba";

    int n = 1, k = 2;

    // Function call
    maximumSuffix(str, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation to find
# longest suffix of the string
# such that occurrence of each
# character is less than K

# Function to find the maximum
# length suffix in the string
def maximumSuffix(s, n, k):

    # Length of the string
    i = len(s)- 1

    # Map to store the number
    # of occurrence of character
    arr = [0 for i in range(26)]
    suffix = ""

    # Loop to iterate string
    # from the last character
    while (i > -1):
        index = ord(s[i]) - ord('a');

        # Condition to check if the
        # occurrence of each character
        # is less than given number
        if (arr[index] < n):
            arr[index] += 1
            suffix += s[i]
            i -= 1
            continue

        # Condition when character
        # cannot be deleted
        if (k == 0):
            break
        k -= 1
        i -= 1

    suffix = suffix[::-1]

    # Longest suffix
    print(suffix)

# Driver Code
if __name__ == '__main__':
    str = "iahagafedcba"

    n = 1
    k = 2

    # Function call
    maximumSuffix(str, n, k)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to find
// longest suffix of the String
// such that occurrence of each
// character is less than K
using System;

class GFG{

// Function to find the maximum
// length suffix in the String
static void maximumSuffix(String s,
            int n, int k){

    // Length of the String
    int i = s.Length - 1;

    // Map to store the number
    // of occurrence of character
    int []arr = new int[26];
    String suffix = "";

    // Loop to iterate String
    // from the last character
    while (i > -1) {

        int index = s[i] - 'a';

        // Condition to check if the
        // occurrence of each character
        // is less than given number
        if (arr[index] < n) {
            arr[index]++;
            suffix += s[i];
            i--;
            continue;
        }

        // Condition when character
        // cannot be deleted
        if (k == 0)
            break;
        k--;
        i--;
    }
    suffix = reverse(suffix);

    // longest suffix
    Console.Write(suffix);
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

// Driver Code
public static void Main(String[] args)
{
    String str = "iahagafedcba";

    int n = 1, k = 2;

    // Function call
    maximumSuffix(str, n, k);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
hgfedcba
```

**业绩分析:**

*   **时间复杂度:**在上面给出的方法中，有一个循环用于迭代字符串，在最坏的情况下需要 O(L)时间。因此，该方法的时间复杂度为 **O(L)** 。
*   **辅助空间复杂度:**在上面给定的方法中，有额外的空间用于存储角色的频率。因此，上述方法的辅助空间复杂度为 **O(L)**
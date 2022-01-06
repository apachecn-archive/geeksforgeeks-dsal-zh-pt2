# 如何找到字典序前排列？

> 原文:[https://www . geeksforgeeks . org/词典-previous-排列-in-c/](https://www.geeksforgeeks.org/lexicographically-previous-permutation-in-c/)

给定一个单词，找到它的字典上较小的排列。例如，字典上较小的“4321”排列是“4312”，下一个较小的“4312”排列是“4231”。如果字符串按升序排序，则下一个字典上较小的排列不存在。

我们已经讨论了[next _ replacement()](https://www.geeksforgeeks.org/find-the-next-lexicographically-greater-word-than-a-given-word/)，它修改一个字符串，以便它存储字典上较小的置换。STL 还提供了 STD::prev _ 置换。如果函数可以将对象重新排列为字典上较小的排列，则返回“真”。否则，它返回“假”。

## C++

```
// C++ program to demonstrate working of
// prev_permutation()
#include <bits/stdc++.h>
using namespace std;

// Driver code
int main()
{
    string str = "4321";
    if (prev_permutation(str.begin(), str.end()))
        cout << "Previous permutation is " << str;
    else
        cout << "Previous permutation doesn't exist";
    return 0;
}
```

**Output**

```
Previous permutation is 4312
```

**如何编写自己的 prev _()？**
下面是寻找前一个排列的步骤:

1.  找到最大的索引 I，使得字符串[I–1]>字符串[i]。
2.  找到最大的索引 j，使得 j >= i 并且字符串[j]
3.  交换 str[j]和 str[I–1]。
4.  从 str[i]开始反转子数组。

以下是上述步骤的实施–

## C++

```
// C++ program to print all permutations with
// duplicates allowed using prev_permutation()
#include <bits/stdc++.h>
using namespace std;

// Function to compute the previous permutation
bool prevPermutation(string& str)
{
    // Find index of the last element of the string
    int n = str.length() - 1;

    // Find largest index i such that str[i - 1] >
    // str[i]
    int i = n;
    while (i > 0 && str[i - 1] <= str[i])
        i--;

    // if string is sorted in ascending order
    // we're at the last permutation
    if (i <= 0)
        return false;

    // Note - str[i..n] is sorted in ascending order

    // Find rightmost element's index that is less
    // than str[i - 1]
    int j = i - 1;
    while (j + 1 <= n && str[j + 1] < str[i - 1])
        j++;

    // Swap character at i-1 with j
    swap(str[i - 1], str[j]);

    // Reverse the substring [i..n]
    reverse(str.begin() + i, str.end());

    return true;
}

// Driver code
int main()
{
    string str = "4321";
    if (prevPermutation(str))
        cout << "Previous permutation is " << str;
    else
        cout << "Previous permutation doesn't exist";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all
// permutations with duplicates
// allowed using prev_permutation()

class GFG {

    // Function to compute
    // the previous permutation
    static boolean prevPermutation(char[] str)
    {

        // Find index of the last
        // element of the string
        int n = str.length - 1;

        // Find largest index i such
        // that str[i - 1] > str[i]
        int i = n;
        while (i > 0 && str[i - 1] <= str[i]) {
            i--;
        }

        // if string is sorted in
        // ascending order we're
        // at the last permutation
        if (i <= 0) {
            return false;
        }

        // Note - str[i..n] is sorted
        // in ascending order Find
        // rightmost element's index
        // that is less than str[i - 1]
        int j = i - 1;
        while (j + 1 <= n && str[j + 1] <= str[i - 1]) {
            j++;
        }

        // Swap character at i-1 with j
        swap(str, i - 1, j);

        // Reverse the substring [i..n]
        StringBuilder sb
            = new StringBuilder(String.valueOf(str));
        sb.reverse();
        str = sb.toString().toCharArray();

        return true;
    }

    static String swap(char[] ch, int i, int j)
    {
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return String.valueOf(ch);
    }

    // Driver code
    public static void main(String[] args)
    {
        char[] str = "4321".toCharArray();
        if (prevPermutation(str)) {
            System.out.println("Previous permutation is "
                               + String.valueOf(str));
        }
        else {
            System.out.println("Previous permutation"
                               + "doesn't exist");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python 3 program to
# print all permutations with
# duplicates allowed
# using prev_permutation()

# Function to compute the
# previous permutation

def prevPermutation(str):

    # Find index of the last element
    # of the string
    n = len(str) - 1

    # Find largest index i such that
    # str[i - 1] > str[i]
    i = n
    while (i > 0 and str[i - 1] <= str[i]):
        i -= 1

    # if string is sorted in ascending order
    # we're at the last permutation
    if (i <= 0):
        return False

    # Note - str[i..n] is sorted in
    # ascending order

    # Find rightmost element's index
    # that is less than str[i - 1]
    j = i - 1
    while (j + 1 <= n and
           str[j + 1] <= str[i - 1]):
        j += 1

    # Swap character at i-1 with j
    str = list(str)
    temp = str[i - 1]
    str[i - 1] = str[j]
    str[j] = temp
    str = ''.join(str)

    # Reverse the substring [i..n]
    str[::-1]

    return True, str

# Driver code
if __name__ == '__main__':
    str = "4321"

    b, str = prevPermutation(str)

    if (b == True):
        print("Previous permutation is", str)
    else:
        print("Previous permutation doesn't exist")

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to print all
// permutations with duplicates
// allowed using prev_permutation()
using System;

class GFG {

    // Function to compute
    // the previous permutation
    static Boolean prevPermutation(char[] str)
    {

        // Find index of the last
        // element of the string
        int n = str.Length - 1;

        // Find largest index i such
        // that str[i - 1] > str[i]
        int i = n;
        while (i > 0 && str[i - 1] <= str[i]) {
            i--;
        }

        // if string is sorted in
        // ascending order we're
        // at the last permutation
        if (i <= 0) {
            return false;
        }

        // Note - str[i..n] is sorted
        // in ascending order Find
        // rightmost element's index
        // that is less than str[i - 1]
        int j = i - 1;
        while (j + 1 <= n && str[j + 1] <= str[i - 1]) {
            j++;
        }

        // Swap character at i-1 with j
        swap(str, i - 1, j);

        // Reverse the substring [i..n]
        String sb = String.Join("", str);
        sb = reverse(sb);
        str = sb.ToString().ToCharArray();

        return true;
    }

    static String swap(char[] ch, int i, int j)
    {
        char temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return String.Join("", ch);
    }
    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--) {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("", temparray);
    }

    // Driver code
    public static void Main(String[] args)
    {
        char[] str = "4321".ToCharArray();
        if (prevPermutation(str)) {
            Console.WriteLine("Previous permutation is "
                              + String.Join("", str));
        }
        else {
            Console.WriteLine("Previous permutation"
                              + "doesn't exist");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to print all
// permutations with duplicates
// allowed using prev_permutation()

// Function to compute
// the previous permutation
function prevPermutation(str)
{

    // Find index of the last
    // element of the string
    let n = str.length - 1;

    // Find largest index i such
    // that str[i - 1] > str[i]
    let i = n;
    while (i > 0 && str[i - 1].charCodeAt(0) <=
                    str[i].charCodeAt(0))
    {
        i--;
    }   

    // If string is sorted in
    // ascending order we're
    // at the last permutation
    if (i <= 0)
    {
        return false;
    }

    // Note - str[i..n] is sorted
    // in ascending order Find
    // rightmost element's index
    // that is less than str[i - 1]
    let j = i - 1;
    while (j + 1 <= n &&
       str[j + 1].charCodeAt(0) <=
       str[i - 1].charCodeAt(0))
    {
        j++;
    }

    // Swap character at i-1 with j
    let temp = str[i - 1];
    str[i - 1] = str[j];
    str[j] = temp;

    // Reverse the substring [i..n]
    //str.reverse();
    return true;
}

// Driver code
let  str = "4321".split("");
if (prevPermutation(str))
{
    document.write("Previous permutation is " +
                  (str).join(""));
}
else
{
    document.write("Previous permutation" +
                   "doesn't exist");
}

// This code is contributed by rag2127

</script>
```

**Output**

```
Previous permutation is 4312
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上述话题的信息，请写评论
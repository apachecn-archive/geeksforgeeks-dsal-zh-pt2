# 计数满足给定条件的字符串对

> 原文:[https://www . geeksforgeeks . org/count-满足给定条件的字符串对/](https://www.geeksforgeeks.org/count-pairs-of-strings-that-satisfy-the-given-conditions/)

给定一个由小写字符组成的 **N** 字符串的数组 **arr[]** ，任务是对数组中满足给定条件的对进行计数:

1.  两个字符串具有相等的对数。
2.  这两个字符串的第一个元音是相同的。
3.  两根弦的最后一个元音是相同的。

**注意**一根弦只能单对使用。

**示例:**

> **输入:** arr[] = {“极客”、“for”、“极客”、“极客”}
> **输出:** 1
> 唯一有效的一对是(“极客”、“极客”)。
> “极客”也可以和“极客”配对，但是
> 两个“极客”都已经配对了。
> 
> **输入:** arr[] = {“代码”、“拍摄”、“模式”}
> T3】输出: 1

**方法:**我们将为每个单词存储出现在一个单词中的所有元音，我们制作第一个元音、最后一个元音和元音总数的元组，并使用 map 存储关于该元组的相应索引。最后，我们将遍历映射，并计算使用存储在映射中的元组值可以形成的对的数量。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if c is vowel
bool is_vowel(char c)
{
    return (c == 'a' || c == 'e' || c == 'i'
            || c == 'o' || c == 'u');
}

// Function to return the count of required pairs
int count(string s[], int n)
{

    map<tuple<char, char, int>, vector<int> > map;

    // For every string of the array
    for (int i = 0; i < n; i++) {

        // Vector to store the vowels
        // of the current string
        vector<char> vowel;
        for (int j = 0; j < s[i].size(); j++) {

            // If current character is a vowel
            if (is_vowel(s[i][j]))
                vowel.push_back(s[i][j]);
        }

        // If current string contains vowels
        if (vowel.size() > 0) {
            int len = vowel.size();

            // Create tuple (first vowel,
            // last vowel, total vowels)
            map[make_tuple(vowel[0],
                           vowel[len - 1], len)]
                .push_back(i);
        }
    }

    int count = 0;
    for (auto i : map) {

        // v stores the indices for which
        // the given condition satisfies
        // Total valid pairs will be half the size
        vector<int> v = i.second;
        count += v.size() / 2;
    }

    return count;
}

// Driver code
int main()
{
    string s[] = { "geeks", "for", "geeks" };
    int n = sizeof(s) / sizeof(string);

    cout << count(s, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if c is vowel
def is_vowel(c):
    return (c == 'a' or c == 'e' or c == 'i'
            or c == 'o' or c == 'u')

# Function to return the count of required pairs
def count(s, n):

    map=dict()

    # For every of the array
    for i in range(n):

        # Vector to store the vowels
        # of the current string
        vowel=[]
        for j in range(len(s[i])):

            # If current character is a vowel
            if (is_vowel(s[i][j])):
                vowel.append(s[i][j])

        # If current contains vowels
        if (len(vowel) > 0):
            Len = len(vowel)

            # Create tuple (first vowel,
            # last vowel, total vowels)
            if (vowel[0],vowel[Len - 1], Len) in map.keys():
                map[(vowel[0],vowel[Len - 1], Len)].append(i)
            else:
                map[(vowel[0],vowel[Len - 1], Len)]=[i,]

    count = 0
    for i in map:

        # v stores the indices for which
        # the given condition satisfies
        # Total valid pairs will be half the size
        v = map[i]
        count += len(v)// 2

    return count

# Driver code
s = ["geeks", "for", "geeks"]
n = len(s)

print(count(s, n))

# This code is contributed by mohit kumar 29
```

**Output:**

```
1

```
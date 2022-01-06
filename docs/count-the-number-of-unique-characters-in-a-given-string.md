# 计算给定字符串中唯一字符的数量

> 原文:[https://www . geesforgeks . org/count-给定字符串中唯一字符的数量/](https://www.geeksforgeeks.org/count-the-number-of-unique-characters-in-a-given-string/)

给定一个由小写英文字母组成的字符串、**字符串**，任务是找出字符串中存在的唯一字符的数量。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:** 7
> **解释:**给定字符串“geeksforgeeks”包含 7 个唯一字符{'g '，' e '，' k '，' s '，' f '，' o '，' r'}。
> 
> **输入:** str = "夫人"
> T3】输出: 3

**方法:**给定的问题可以使用[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)来解决。这个想法是初始化一个[无序集](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)，存储给定字符串的所有不同字符。遍历字符串后集合的大小是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Program to count the number of
// unique characters in a string
int cntDistinct(string str)
{
    // Set to store unique characters
    // in the given string
    unordered_set<char> s;

    // Loop to traverse the string
    for (int i = 0; i < str.size(); i++) {

        // Insert current character
        // into the set
        s.insert(str[i]);
    }

    // Return Answer
    return s.size();
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";
    cout << cntDistinct(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Program to count the number of
// unique characters in a string
static int cntDistinct(String str)
{

    // Set to store unique characters
    // in the given string
    HashSet<Character> s = new HashSet<Character>();

    // Loop to traverse the string
    for(int i = 0; i < str.length(); i++)
    {

        // Insert current character
        // into the set
        s.add(str.charAt(i));
    }

    // Return Answer
    return s.size();
}

// Driver Code
public static void main(String args[])
{
    String str = "geeksforgeeks";
    System.out.print(cntDistinct(str));
}
}

// This code is contributed by sanjoy_62
```

**Output**

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
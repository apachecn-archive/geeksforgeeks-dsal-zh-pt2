# 计算单词数组中恰好出现两次的单词数

> 原文:[https://www . geesforgeks . org/count-字数-出现-正好-两次-数组-字数/](https://www.geeksforgeeks.org/count-words-appear-exactly-two-times-array-words/)

给定 n 个字的数组。有些单词重复两次，我们需要统计这样的单词。

**示例:**

```
Input : s[] = {"hate", "love", "peace", "love", 
               "peace", "hate", "love", "peace", 
               "love", "peace"};
Output : 1
There is only one word "hate" that appears twice

Input : s[] = {"Om", "Om", "Shankar", "Tripathi", 
                "Tom", "Jerry", "Jerry"};
Output : 2
There are two words "Om" and "Jerry" that appear
twice.
```

来源:亚马逊采访

1.  遍历给定的数组，在哈希表中存储字数
2.  遍历哈希表，用计数 2 计数所有单词。

下面是实现:

## C++

```
// C++ program to count all words with count
// exactly 2.
#include <bits/stdc++.h>
using namespace std;

// Returns count of words with frequency
// exactly 2.
int countWords(string str[], int n)
{
    unordered_map<string, int> m;
    for (int i = 0; i < n; i++)
        m[str[i]] += 1;

    int res = 0;
    for (auto it = m.begin(); it != m.end(); it++)
        if ((it->second == 2))
            res++;

    return res;
}

// Driver code
int main()
{
    string s[] = { "hate", "love", "peace", "love",
                   "peace", "hate", "love", "peace",
                   "love", "peace" };
    int n = sizeof(s) / sizeof(s[0]);
    cout << countWords(s, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all words with count
// exactly 2.
import java.util.HashMap;
import java.util.Map;
public class GFG {

    // Returns count of words with frequency
    // exactly 2.
    static int countWords(String str[], int n)
    {
        // map to store count of each word
        HashMap<String, Integer> m = new HashMap<>();

        for (int i = 0; i < n; i++){
            if(m.containsKey(str[i])){
                int get = m.get(str[i]);
                m.put(str[i], get + 1);
            }
            else{
                m.put(str[i], 1);
            }
        }

        int res = 0;
        for (Map.Entry<String, Integer> it: m.entrySet()){
            if(it.getValue() == 2)
                res++;
        }

        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        String s[] = { "hate", "love", "peace", "love",
                       "peace", "hate", "love", "peace",
                       "love", "peace" };
        int n = s.length;
        System.out.println( countWords(s, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python program to count all
# words with count
# exactly 2.

# Returns count of words with frequency
# exactly 2.
def countWords(stri, n):
    m = dict()
    for i in range(n):
        m[stri[i]] = m.get(stri[i],0) + 1

    res = 0
    for i in m.values():
        if i == 2:
            res += 1

    return res

# Driver code
s = [ "hate", "love", "peace", "love",
      "peace", "hate", "love", "peace",
                "love", "peace" ]
n = len(s)
print(countWords(s, n))

# This code is contributed
# by Shubham Rana
```

## C#

```
// C# program to count all words with count
// exactly 2.
using System;
using System.Collections.Generic;

class GFG
{

    // Returns count of words with frequency
    // exactly 2.
    static int countWords(String []str, int n)
    {
        // map to store count of each word
        Dictionary<String,int> m = new Dictionary<String,int>();

        for (int i = 0; i < n; i++)
        {
            if(m.ContainsKey(str[i]))
            {
                int get = m[str[i]];
                m.Remove(str[i]);
                m.Add(str[i], get + 1);
            }
            else
            {
                m.Add(str[i], 1);
            }
        }

        int res = 0;
        foreach(KeyValuePair<String, int> it in m)
        {
            if(it.Value == 2)
                res++;
        }

        return res;
    }

    // Driver code
    public static void Main(String []args)
    {
        String []a = { "hate", "love", "peace", "love",
                    "peace", "hate", "love", "peace",
                    "love", "peace" };
        int n = a.Length;
        Console.WriteLine( countWords(a, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to count all words with count
// exactly 2.

// Returns count of words with frequency
// exactly 2.
function countWords(str, n)
{
    var m = new Map();
    for (var i = 0; i < n; i++)
    {
        if(m.has(str[i]))
            m.set(str[i], m.get(str[i])+1)
        else
            m.set(str[i], 1)
    }

    var res = 0;

    m.forEach((value, key) => {

        if ((value == 2))
            res++;
    });
    return res;
}

// Driver code
var s = ["hate", "love", "peace", "love",
               "peace", "hate", "love", "peace",
               "love", "peace" ];
var n = s.length;
document.write( countWords(s, n));

</script>
```

**Output**

```
1
```

#### **方法二:使用**内置的 **Python 函数:**

*   使用 [**计数器**](https://www.geeksforgeeks.org/python-counter-objects-elements/) 功能计算每个单词的频率
*   频率字典中的遍历
*   检查哪个单词的频率为 2。如果是，增加计数
*   打印计数

下面是实现:

## 计算机编程语言

```
# importing Counter from collections
from collections import Counter

# Python program to count all words with count exactly 2.
# Returns count of words with frequency exactly 2.
def countWords(stri, n):

    # Calculating frequency using Counter
    m = Counter(stri)

    count = 0
    # Traversing in freq dictionary
    for i in m:
        if m[i] == 2:
            count += 1

    return count

# Driver code
s = ["hate", "love", "peace", "love",
     "peace", "hate", "love", "peace",
     "love", "peace"]
n = len(s)
print(countWords(s, n))

# This code is contributed by vikkycirus
```

**Output**

```
1
```

本文由**索米亚提瓦里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
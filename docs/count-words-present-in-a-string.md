# 计算字符串中出现的单词数

> 原文:[https://www . geesforgeks . org/count-words-present-in-a-string/](https://www.geeksforgeeks.org/count-words-present-in-a-string/)

给定一个单词数组和一个字符串，我们需要计算给定字符串中存在的所有单词。

**示例:**

```
Input : words[] = { "welcome", "to", "geeks", "portal"}
            str = "geeksforgeeks is a computer science portal for geeks."
Output :  2
Two words "portal" and "geeks" is present in str.

Input : words[] = {"Save", "Water", "Save", "Yourself"}
        str     = "Save"
Output :1

```

 **步骤:**

1.  [从字符串中提取每个单词。](https://www.geeksforgeeks.org/extracting-word-string-java/)
2.  对于每个单词，检查它是否在单词数组中(通过创建集合/映射)。如果存在，增加结果。

下面是上述步骤的 Java 实现

```
// Java program to count number 
// of words present in a string

import java.util.HashSet;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Test 
{
    static int countOccurrence(String[] word, String str) 
    {
        // counter
        int counter = 0;

        // for extracting words
        Pattern p = Pattern.compile("[a-zA-Z]+");
        Matcher m = p.matcher(str);

        // HashSet for quick check whether
        //  a word in str present in word[] or not
        HashSet<String> hs = new HashSet<String>();

        for (String string : word) {
            hs.add(string);
        }

        while(m.find())
        {
            if(hs.contains(m.group()))
                counter++;
        }

        return counter;

    }

    public static void main(String[] args) 
    {
        String word[] = { "welcome", "to", "geeks", "portal"};

        String str = "geeksforgeeks is a computer science portal for geeks.";

        System.out.println(countOccurrence(word,str));

    }

}
```

输出:

```
2

```

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
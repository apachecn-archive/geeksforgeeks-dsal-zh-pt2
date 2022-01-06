# 提取给定字符串中存在的网址

> 原文:[https://www . geesforgeks . org/extract-URLs-present-in-a-给定字符串/](https://www.geeksforgeeks.org/extract-urls-present-in-a-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是从字符串中找到并提取所有的网址。如果字符串中没有[网址](https://en.wikipedia.org/wiki/URL)，则打印 **"-1"** 。

**示例:**

> **输入:** S = "欢迎来到 https://www.geeksforgeeks.org 计算机科学门户"
> **输出:**https://www.geeksforgeeks.org
> **解释:**
> 给定字符串包含 URL ' https://www . geeksforgeeks . org '。
> 
> **输入:** S =“欢迎来到 https://www.geeksforgeeks.org 计算机科学门户网站 https://write.geeksforgeeks.org 门户”
> **输出:**
> https://write.geeksforgeeks.org
> https://www.geeksforgeeks.org
> **说明:**
> 给定的字符串包含两个 URL‘https://write . geeksforgeeks . org’和‘https://www . geeksforgeeks . org’。

**做法:**思路是用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决这个问题。按照以下步骤解决给定的问题:

*   创建一个[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)从字符串中提取所有网址，如下所述:

> **regex = "\\b(？:https？| ftp |文件://[-a-za-z0-9+&@ #/%？=~_|！:，。；]*[-a-za-z0-9+&@ #/% = ~ _ |]]"**

*   [用 Java 创建一个 ArrayList](https://www.geeksforgeeks.org/initialize-an-arraylist-in-java/)并使用 [Pattern.compile()](https://www.geeksforgeeks.org/pattern-compilestring-method-in-java-with-examples/) 编译正则表达式。
*   将给定的字符串与正则表达式匹配。在 Java 中，这可以通过使用 [Pattern.matcher()](https://www.geeksforgeeks.org/matcher-pattern-method-in-java-with-examples/) 来完成。
*   找到从匹配结果的**第一个索引到匹配结果**的**最后一个索引的子串，并将这个[子串](https://www.geeksforgeeks.org/substring-in-cpp/)添加到列表中。**
*   完成上述步骤后，如果发现列表为空，则打印**-1”**，因为字符串 **S** 中没有**网址**。否则，打印列表中存储的所有字符串。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.util.regex.*;
class GFG {

    // Function to extract all the URL
    // from the string
    public static void extractURL(
        String str)
    {

        // Creating an empty ArrayList
        List<String> list
            = new ArrayList<>();

        // Regular Expression to extract
        // URL from the string
        String regex
            = "\\b((?:https?|ftp|file):"
              + "//[-a-zA-Z0-9+&@#/%?="
              + "~_|!:, .;]*[-a-zA-Z0-9+"
              + "&@#/%=~_|])";

        // Compile the Regular Expression
        Pattern p = Pattern.compile(
            regex,
            Pattern.CASE_INSENSITIVE);

        // Find the match between string
        // and the regular expression
        Matcher m = p.matcher(str);

        // Find the next subsequence of
        // the input subsequence that
        // find the pattern
        while (m.find()) {

            // Find the substring from the
            // first index of match result
            // to the last index of match
            // result and add in the list
            list.add(str.substring(
                m.start(0), m.end(0)));
        }

        // IF there no URL present
        if (list.size() == 0) {
            System.out.println("-1");
            return;
        }

        // Print all the URLs stored
        for (String url : list) {
            System.out.println(url);
        }
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given String str
        String str
            = "Welcome to https:// www.geeksforgeeks"
              + ".org Computer Science Portal";

        // Function Call
        extractURL(str);
    }
}
```

**Output:**

```
https://www.geeksforgeeks.org

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)
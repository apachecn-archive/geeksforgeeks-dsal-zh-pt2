# 从给定字符串中提取最大数值|集合 2 (Regex 方法)

> 原文:[https://www . geesforgeks . org/extract-maximum-numeric-value-given-string-set-2-regex-approach/](https://www.geeksforgeeks.org/extract-maximum-numeric-value-given-string-set-2-regex-approach/)

给定一个字母数字字符串，从该字符串中提取最大数值。

示例:

```
Input : 100klh564abc365bg
Output : 564
Maximum numeric value among 100, 564 
and 365 is 564.
Input : abchsd0365sdhs
Output : 365

```

在[集合 1](https://www.geeksforgeeks.org/extract-maximum-numeric-value-given-string/) 中，我们讨论了从给定字符串中提取数值的一般方法。在这篇文章中，我们将讨论相同的[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)方法。

下面是至少一个数字的正则表达式之一。

```
\d+

```

所以 Regex 的解决方法很简单:

1.  Initialize MAX = 0
2.  Run a loop on matcher, and once a match is found, the numeric string is converted into an integer and compared with MAX.
    *   If the value is greater than MAX, update MAX to a value.
3.  Finally, return to MAX.

```
// Java regex program to extract the maximum value

import java.util.regex.Matcher;
import java.util.regex.Pattern;

class GFG 
{
    // Method to extract the maximum value
    static int extractMaximum(String str)
    {
        // regular expression for atleast one numeric digit
        String regex = "\\d+";

        // compiling regex
        Pattern p = Pattern.compile(regex);

        // Matcher object
        Matcher m = p.matcher(str);

        // initialize MAX = 0
        int MAX = 0;

        // loop over matcher
        while(m.find())
        {
            // convert numeric string to integer
            int num = Integer.parseInt(m.group());

            // compare num with MAX, update MAX if num > MAX
            if(num > MAX)
                MAX = num;
        }

        return MAX;    
    }

    public static void main (String[] args)
    {
        String str = "100klh564abc365bg";

        System.out.println(extractMaximum(str));
    }
}
```

输出:

```
564

```

但是，如果数字大于该整数范围，上述程序将不起作用。你可以尝试 *[parseLong()](https://www.geeksforgeeks.org/java-lang-long-class-in-java/)* 方法获取高达 *long* 范围的数字。但是要处理大数(大于*长*范围)的情况，我们可以借助 java 中的 [BigInteger](https://www.geeksforgeeks.org/biginteger-class-in-java/) 类。下面是 java 程序来演示同样的情况。

```
// Java regex program to extract the maximum value
// in case of large numbers

import java.math.BigInteger;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

class GFG 
{
    // Method to extract the maximum value
    static BigInteger extractMaximum(String str)
    {
        // regular expression for atleast one numeric digit
        String regex = "\\d+";

        // compiling regex
        Pattern p = Pattern.compile(regex);

        // Matcher object
        Matcher m = p.matcher(str);

        // initialize MAX = 0
        BigInteger MAX = BigInteger.ZERO;

        // loop over matcher
        while(m.find())
        {
            // convert numeric string to BigIntegr
            BigInteger num = new BigInteger(m.group());

            // compare num with MAX, update MAX if num > MAX
            if(num.compareTo(MAX) > 0)
                MAX = num;
        }

        return MAX;    
    }

    public static void main (String[] args)
    {
        String str = "100klh564231315151313151315abc365bg";

        System.out.println(extractMaximum(str));
    }
}
```

输出:

```
564231315151313151315

```

本文由**高拉夫·米格拉尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
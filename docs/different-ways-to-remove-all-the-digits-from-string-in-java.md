# Java 中去除字符串中所有数字的不同方法

> 原文:[https://www . geeksforgeeks . org/从 java 字符串中删除所有数字的不同方法/](https://www.geeksforgeeks.org/different-ways-to-remove-all-the-digits-from-string-in-java/)

给定[字母数字字符串](https://www.geeksforgeeks.org/how-to-check-string-is-alphanumeric-or-not-using-regular-expression/)字符串，任务是编写一个 Java 程序，从该字符串中删除所有数字，并打印修改后的字符串。

**示例:**

> **输入:** str = "GeeksForGeeks123 "
> 
> **输出:** GeeksForGeeks
> 
> **说明:**给定的字符串包含数字 1、2 和 3。我们删除所有数字并打印修改后的字符串。
> 
> **输入:** str = "12Java "
> 
> **输出:** Java
> 
> **说明:**给定的字符串包含数字 1 和 2。我们删除所有数字并打印修改后的字符串。

**法一:使用** [**弦**](https://www.geeksforgeeks.org/java-string-tochararray-example/) 法

1.  获取字符串以删除所有数字。
2.  将给定的字符串转换为字符数组。
3.  初始化一个存储结果的空字符串。
4.  从头到尾遍历字符数组。
5.  检查指定的字符是否不是数字，然后将该字符添加到结果变量中。
6.  现在，打印结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove all the
// digit from string
class GFG {

    // Function to remove all the digit
    // from string
    public static String removeAllDigit(String str)
    {
        // Converting the given string
        // into a character array
        char[] charArray = str.toCharArray();
        String result = "";

        // Traverse the character array
        for (int i = 0; i < charArray.length; i++) {

            // Check if the specified character is not digit
            // then add this character into result variable
            if (!Character.isDigit(charArray[i])) {
                result = result + charArray[i];
            }
        }

        // Return result
        return result;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given alphanumeric string str
        String str = "GeeksForGeeks123";

        // Print the modified string
        System.out.println(removeAllDigit(str));
    }
}
```

**Output**

```
GeeksForGeeks

```

*   ***时间复杂度:*** O(N)
*   ***空间复杂度:*** O(N)

**方法二:使用**[**string . charat()**](https://www.geeksforgeeks.org/java-string-charat-method-example/)T6】方法

1.  获取字符串以删除所有数字。
2.  初始化一个存储结果的空字符串。
3.  从头到尾遍历字符串。
4.  检查指定的字符是否不是数字，然后将该字符添加到结果变量中。
5.  现在，打印结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove all the
// digit from string
class GFG {

    // Function to remove all the digit
    // from string
    public static String removeAllDigit(String str)
    {
        String result = "";

        // Traverse the String from start to end
        for (int i = 0; i < str.length(); i++) {

            // Check if the specified character is not digit
            // then add this character into result variable
            if (!Character.isDigit(str.charAt(i))) {
                result = result + str.charAt(i);
            }
        }

        // Return result
        return result;
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given alphanumeric string str
        String str = "GeeksForGeeks123";

        // Print the modified string
        System.out.println(removeAllDigit(str));
    }
}
```

**Output**

```
GeeksForGeeks

```

*   ***时间复杂度:*** O(N)
*   ***空间复杂度:*** O(1)

**方法三:使用**[**string . replace all()**](https://www.geeksforgeeks.org/java-lang-string-replace-method-java/)T6】方法

其思想是使用 String.replaceAll()方法，用给定的替换字符串替换与给定的[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)匹配的所有字符序列。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove all the
// digit from string
class GFG {

    // Function to remove all the digit
    // from string
    public static String removeAllDigit(String str)
    {
        // Replaces all the sequence of characters
        // that matches the given regex with
        // the given replacement string
        return str.replaceAll("\\d", "");
    }

    // Driver Code
    public static void main(String args[])
    {

        // Given alphanumeric string str
        String str = "GeeksForGeeks123";

        // Print the modified string
        System.out.println(removeAllDigit(str));
    }
}
```

**Output**

```
GeeksForGeeks

```

*   ***时间复杂度:*** O(N)
*   ***空间复杂度:*** O(1)
# 确定字符串是否具有所有唯一字符

> 原文:[https://www . geesforgeks . org/decision-string-unique-characters/](https://www.geeksforgeeks.org/determine-string-unique-characters/)

给定一个字符串，确定该字符串是否包含所有唯一字符。

**示例:**

```
Input : abcd10jk
Output : true

Input : hutg9mnd!nk9
Output : false
```

**方法 1–蛮力技术**:用变量 I 和 j 运行 2 个循环。比较字符串[i]和字符串[j]。如果它们在任何时候变得相等，则返回 false。
T3】时间复杂度 : O(n <sup>2</sup>

## C++

```
// C++ program to illustrate string
// with unique characters using
// brute force technique
#include <bits/stdc++.h>
using namespace std;

bool uniqueCharacters(string str)
{

    // If at any time we encounter 2
    // same characters, return false
    for (int i = 0; i < str.length() - 1; i++) {
        for (int j = i + 1; j < str.length(); j++) {
            if (str[i] == str[j]) {
                return false;
            }
        }
    }

    // If no duplicate characters encountered,
    // return true
    return true;
}

// driver code
int main()
{
    string str = "GeeksforGeeks";

    if (uniqueCharacters(str)) {
        cout << "The String " << str
             << " has all unique characters\n";
    }
    else {
        cout << "The String " << str
             << " has duplicate characters\n";
    }
    return 0;
}
// This code is contributed by Divyam Madaan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate string with
// unique characters using brute force technique
import java.util.*;

class GfG {
    boolean uniqueCharacters(String str)
    {
        // If at any time we encounter 2 same
        // characters, return false
        for (int i = 0; i < str.length(); i++)
            for (int j = i + 1; j < str.length(); j++)
                if (str.charAt(i) == str.charAt(j))
                    return false;

        // If no duplicate characters encountered,
        // return true
        return true;
    }

    public static void main(String args[])
    {
        GfG obj = new GfG();
        String input = "GeeksforGeeks";

        if (obj.uniqueCharacters(input))
            System.out.println("The String " + input + " has all unique characters");
        else
            System.out.println("The String " + input + " has duplicate characters");
    }
}
```

## 蟒蛇 3

```
# Python program to illustrate string
# with unique characters using
# brute force technique

def uniqueCharacters(str):

    # If at any time we encounter 2
    # same characters, return false
    for i in range(len(str)):
        for j in range(i + 1,len(str)):
            if(str[i] == str[j]):
                return False;

    # If no duplicate characters
    # encountered, return true
    return True;

# Driver Code
str = "GeeksforGeeks";

if(uniqueCharacters(str)):
    print("The String ", str," has all unique characters");
else:
    print("The String ", str, " has duplicate characters");

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to illustrate string with
// unique characters using brute force
// technique
using System;

public class GFG {

    static bool uniqueCharacters(String str)
    {

        // If at any time we encounter 2
        // same characters, return false
        for (int i = 0; i < str.Length; i++)
            for (int j = i + 1; j < str.Length; j++)
                if (str[i] == str[j])
                    return false;

        // If no duplicate characters
        // encountered, return true
        return true;
    }

    public static void Main()
    {
        string input = "GeeksforGeeks";

        if (uniqueCharacters(input) == true)
            Console.WriteLine("The String " + input
                              + " has all unique characters");
        else
            Console.WriteLine("The String " + input
                              + " has duplicate characters");
    }
}

// This code is contributed by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to illustrate string
// with unique characters using
// brute force technique

function uniqueCharacters($str)
{

    // If at any time we encounter 2
    // same characters, return false
    for($i = 0; $i < strlen($str); $i++)
    {
        for($j = $i + 1; $j < strlen($str); $j++)
        {
            if($str[$i] == $str[$j])
            {
                return false;
            }
        }
    }

    // If no duplicate characters
    // encountered, return true
    return true;
}

// Driver Code
$str = "GeeksforGeeks";

if(uniqueCharacters($str))
{
    echo "The String ", $str,
          " has all unique characters\n";
}
else
{
    echo "The String ", $str,
         " has duplicate characters\n";
}

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to illustrate string with
// unique characters using brute force
// technique
function uniqueCharacters(str)
{

    // If at any time we encounter 2
    // same characters, return false
    for(let i = 0; i < str.length; i++)
        for(let j = i + 1; j < str.length; j++)
            if (str[i] == str[j])
                return false;

    // If no duplicate characters
    // encountered, return true
    return true;
}

// Driver code
let input = "GeeksforGeeks";

if (uniqueCharacters(input) == true)
    document.write("The String " + input +
                   " has all unique characters" + "</br>");
else
    document.write("The String " + input +
                   " has duplicate characters");

// This code is contributed by decode2207

</script>
```

**输出:**

```
The String GeeksforGeeks has duplicate characters
```

注意:请注意，该程序区分大小写。

**方法 2–排序**:使用基于字符 ASCII 值的排序
**时间复杂度** : O(n log n)

## C++

```
// C++ program to illustrate string
// with unique characters using
// brute force technique
#include <bits/stdc++.h>
using namespace std;

bool uniqueCharacters(string str)
{

    // Using sorting
    sort(str.begin(), str.end());

    for (int i = 0; i < str.length()-1; i++) {

        // if at any time, 2 adjacent
        // elements become equal,
        // return false
        if (str[i] == str[i + 1]) {
            return false;
        }
    }
    return true;
}

// driver code
int main()
{

    string str = "GeeksforGeeks";

    if (uniqueCharacters(str)) {
        cout << "The String " << str
             << " has all unique characters\n";
    }
    else {

        cout << "The String " << str
             << " has duplicate characters\n";
    }
    return 0;
}
// This code is contributed by Divyam Madaan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check string with unique
// characters using sorting technique
import java.util.*;

class GfG {
    /* Convert the string to character array
       for sorting */
    boolean uniqueCharacters(String str)
    {
        char[] chArray = str.toCharArray();

        // Using sorting
        // Arrays.sort() uses binarySort in the background
        // for non-primitives which is of O(nlogn) time complexity
        Arrays.sort(chArray);

        for (int i = 0; i < chArray.length - 1; i++) {
            // if the adjacent elements are not
            // equal, move to next element
            if (chArray[i] != chArray[i + 1])
                continue;

            // if at any time, 2 adjacent elements
            // become equal, return false
            else
                return false;
        }
        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        GfG obj = new GfG();
        String input = "GeeksforGeeks";

        if (obj.uniqueCharacters(input))
            System.out.println("The String " + input
                               + " has all unique characters");
        else
            System.out.println("The String " + input
                               + " has duplicate characters");
    }
}
```

## 蟒蛇 3

```
# Python3 program to illustrate string
# with unique characters using
# brute force technique
def uniqueCharacters(st):

    # Using sorting
    st = sorted(st)

    for i in range(len(st)-1):

        # if at any time, 2 adjacent
        # elements become equal,
        # return false
        if (st[i] == st[i + 1]) :
            return False

    return True

# Driver code
if __name__=='__main__':

    st = "GeeksforGeeks"

    if (uniqueCharacters(st)) :
        print("The String",st,"has all unique characters\n")

    else :
        print("The String",st,"has duplicate characters\n")

# This code is contributed by AbhiThakur
```

## C#

```
// C# program to check string with unique
// characters using sorting technique
using System;

public class GFG {

    /* Convert the string to character array
    for sorting */
    static bool uniqueCharacters(String str)
    {
        char[] chArray = str.ToCharArray();

        // Using sorting
        Array.Sort(chArray);

        for (int i = 0; i < chArray.Length - 1; i++) {

            // if the adjacent elements are not
            // equal, move to next element
            if (chArray[i] != chArray[i + 1])
                continue;

            // if at any time, 2 adjacent elements
            // become equal, return false
            else
                return false;
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        string input = "GeeksforGeeks";

        if (uniqueCharacters(input) == true)
            Console.WriteLine("The String " + input
                              + " has all unique characters");
        else
            Console.WriteLine("The String " + input
                              + " has duplicate characters");
    }
}

// This code is contributed by shiv_bhakt.
```

## java 描述语言

```
<script>

    // Javascript program to
    // check string with unique
    // characters using sorting technique

    /* Convert the string to character array
    for sorting */
    function uniqueCharacters(str)
    {
        let chArray = str.split('');

        // Using sorting
        chArray.sort();

        for (let i = 0; i < chArray.length - 1; i++)
        {

            // if the adjacent elements are not
            // equal, move to next element
            if (chArray[i] != chArray[i + 1])
                continue;

            // if at any time, 2 adjacent elements
            // become equal, return false
            else
                return false;
        }

        return true;
    }

    let input = "GeeksforGeeks";

    if (uniqueCharacters(input) == true)
      document.write("The String " + input +
      " has all unique characters" + "</br>");
    else
      document.write("The String " + input +
      " has duplicate characters" + "</br>");

</script>
```

**输出:**

```
The String GeeksforGeeks has duplicate characters
```

**方法 3–使用额外的数据结构**:该方法假设 ASCII 字符集(8 位)。这个想法是为字符维护一个布尔数组。256 个索引代表 256 个字符。所有数组元素最初都设置为 false。当我们迭代字符串时，在等于字符 int 值的索引处设置 true。如果在任何时候，我们遇到数组值已经为真，这意味着具有该 int 值的字符被重复。

**时间复杂度:** O(n)

## C++

```
#include <cstring>
#include <iostream>
using namespace std;

const int MAX_CHAR = 256;

bool uniqueCharacters(string str)
{

    // If length is greater than 265,
    // some characters must have been repeated
    if (str.length() > MAX_CHAR)
        return false;

    bool chars[MAX_CHAR] = { 0 };
    for (int i = 0; i < str.length(); i++) {
        if (chars[int(str[i])] == true)
            return false;

        chars[int(str[i])] = true;
    }
    return true;
}

// driver code
int main()
{
    string str = "GeeksforGeeks";

    if (uniqueCharacters(str)) {
        cout << "The String " << str
             << " has all unique characters\n";
    }
    else {

        cout << "The String " << str
             << " has duplicate characters\n";
    }
    return 0;
}
// This code is contributed by Divyam Madaan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate String With
// Unique Characters using data structure
import java.util.*;

class GfG {
    int MAX_CHAR = 256;

    boolean uniqueCharacters(String str)
    {
        // If length is greater than 256,
        // some characters must have been repeated
        if (str.length() > MAX_CHAR)
            return false;

        boolean[] chars = new boolean[MAX_CHAR];
        Arrays.fill(chars, false);

        for (int i = 0; i < str.length(); i++) {
            int index = (int)str.charAt(i);

            /* If the value is already true, string
               has duplicate characters, return false */
            if (chars[index] == true)
                return false;

            chars[index] = true;
        }

        /* No duplicates encountered, return true */
        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        GfG obj = new GfG();
        String input = "GeeksforGeeks";

        if (obj.uniqueCharacters(input))
            System.out.println("The String " + input
                               + " has all unique characters");
        else
            System.out.println("The String " + input
                               + " has duplicate characters");
    }
}
```

## 蟒蛇 3

```
# Python program to illustrate
# string with unique characters
# using data structure
MAX_CHAR = 256;

def uniqueCharacters(string):
    n = len(string)

    # If length is greater than 256,
    # some characters must have
    # been repeated
    if n > MAX_CHAR:
        return False

    chars = [False] * MAX_CHAR

    for i in range(n):
        index = ord(string[i])

        '''
         * If the value is already True,
         string has duplicate characters,
         return False'''
        if (chars[index] == True):
            return False

        chars[index] = True

    ''' No duplicates encountered,
        return True '''
    return True

# Driver code
if __name__ == '__main__':

    input = "GeeksforGeeks"
    if (uniqueCharacters(input)):
        print("The String", input,
              "has all unique characters")
    else:
        print("The String", input,
              "has duplicate characters")

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program to illustrate String With
// Unique Characters using data structure
using System;

class GfG {
    static int MAX_CHAR = 256;

    bool uniqueCharacters(String str)
    {
        // If length is greater than 256,
        // some characters must have been repeated
        if (str.Length > MAX_CHAR)
            return false;

        bool[] chars = new bool[MAX_CHAR];
        for (int i = 0; i < MAX_CHAR; i++) {
            chars[i] = false;
        }
        for (int i = 0; i < str.Length; i++) {
            int index = (int)str[i];

            /* If the value is already true, string
            has duplicate characters, return false */
            if (chars[index] == true)
                return false;

            chars[index] = true;
        }

        /* No duplicates encountered, return true */
        return true;
    }

    // Driver code
    public static void Main(String[] args)
    {
        GfG obj = new GfG();
        String input = "GeeksforGeeks";

        if (obj.uniqueCharacters(input))
            Console.WriteLine("The String " + input
                              + " has all unique characters");
        else
            Console.WriteLine("The String " + input
                              + " has duplicate characters");
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to illustrate String With
    // Unique Characters using data structure

    let MAX_CHAR = 256;

    function uniqueCharacters(str)
    {
        // If length is greater than 256,
        // some characters must have been repeated
        if (str.length > MAX_CHAR)
            return false;

        let chars = new Array(MAX_CHAR);
        for (let i = 0; i < MAX_CHAR; i++) {
            chars[i] = false;
        }
        for (let i = 0; i < str.length; i++) {
            let index = str[i].charCodeAt();

            /* If the value is already true, string
            has duplicate characters, return false */
            if (chars[index] == true)
                return false;

            chars[index] = true;
        }

        /* No duplicates encountered, return true */
        return true;
    }

    let input = "GeeksforGeeks";

    if (uniqueCharacters(input))
      document.write("The String " + input
                        + " has all unique characters");
    else
      document.write("The String " + input
                        + " has duplicate characters");

</script>
```

**输出:**

```
The String GeeksforGeeks has duplicate characters
```

**方法 4–没有额外的数据结构:**该方法对于字母为 a-z 的字符串有效。这种方法有点棘手。我们不维护布尔数组，而是维护一个名为 checker(32 位)的整数值。当我们迭代字符串时，我们通过语句***int Bitatindex = str . charat(I)-“a”找到了与“a”相关的字符的 int 值；***
然后用语句***1<<bitAtIndex***将该 int 值的位设置为 1。
现在，如果该位已经在检查器中设置，位“与”操作将使检查器>为 0。在这种情况下返回 false。
否则更新 checker，用语句 ***使该索引的位 1 = checker |(1<<bitAtIndex)；***

**时间复杂度** : O(n)

## C++

```
// C++ program to illustrate string
// with unique characters using
// brute force technique
#include <bits/stdc++.h>
using namespace std;

bool uniqueCharacters(string str)
{

    // Assuming string can have characters
    // a-z, this has 32 bits set to 0
    int checker = 0;

    for (int i = 0; i < str.length(); i++) {

        int bitAtIndex = str[i] - 'a';

        // if that bit is already set in
        // checker, return false
        if ((checker & (1 << bitAtIndex)) > 0) {
            return false;
        }

        // otherwise update and continue by
        // setting that bit in the checker
        checker = checker | (1 << bitAtIndex);
    }

    // no duplicates encountered, return true
    return true;
}

// driver code
int main()
{

    string str = "geeksforgeeks";

    if (uniqueCharacters(str)) {
        cout << "The String " << str
             << " has all unique characters\n";
    }
    else {
        cout << "The String " << str
             << " has duplicate characters\n";
    }
    return 0;
}
// This code is contributed by Divyam Madaan
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate String with unique
// characters without using any data structure
import java.util.*;

class GfG {
    boolean uniqueCharacters(String str)
    {
        // Assuming string can have characters a-z
        // this has 32 bits set to 0
        int checker = 0;

        for (int i = 0; i < str.length(); i++) {
            int bitAtIndex = str.charAt(i) - 'a';

            // if that bit is already set in checker,
            // return false
            if ((checker & (1 << bitAtIndex)) > 0)
                return false;

            // otherwise update and continue by
            // setting that bit in the checker
            checker = checker | (1 << bitAtIndex);
        }

        // no duplicates encountered, return true
        return true;
    }

    // Driver Code
    public static void main(String args[])
    {
        GfG obj = new GfG();
        String input = "geekforgeeks";

        if (obj.uniqueCharacters(input))
            System.out.println("The String " + input
                               + " has all unique characters");
        else
            System.out.println("The String " + input
                               + " has duplicate characters");
    }
}
```

## 蟒蛇 3

```
# Python3 program to illustrate String with unique
# characters without using any data structure
import math

def uniqueCharacters(string):

    # Assuming string can have characters
    # a-z this has 32 bits set to 0
    checker = 0

    for i in range(len(string)):
        bitAtIndex = ord(string[i]) - ord('a')

        # If that bit is already set in
        # checker, return False
        if ((bitAtIndex) > 0):
            if ((checker & ((1 << bitAtIndex))) > 0):
                return False

            # Otherwise update and continue by
            # setting that bit in the checker
            checker = checker | (1 << bitAtIndex)

    # No duplicates encountered, return True
    return True

# Driver Code
if __name__ == '__main__':

    input = "geekforgeeks"

    if (uniqueCharacters(input)):
        print("The String " + input +
              " has all unique characters")
    else:
        print("The String " + input +
              " has duplicate characters")

# This code is contributed by Princi Singh
```

## C#

```
// C# program to illustrate String
// with unique characters without
// using any data structure
using System;

class GFG {
    public virtual bool uniqueCharacters(string str)
    {
        // Assuming string can have
        // characters a-z this has
        // 32 bits set to 0
        int checker = 0;

        for (int i = 0; i < str.Length; i++) {
            int bitAtIndex = str[i] - 'a';

            // if that bit is already set
            // in checker, return false
            if ((checker & (1 << bitAtIndex)) > 0) {
                return false;
            }

            // otherwise update and continue by
            // setting that bit in the checker
            checker = checker | (1 << bitAtIndex);
        }

        // no duplicates encountered,
        // return true
        return true;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        GFG obj = new GFG();
        string input = "geekforgeeks";

        if (obj.uniqueCharacters(input)) {
            Console.WriteLine("The String " + input + " has all unique characters");
        }
        else {
            Console.WriteLine("The String " + input + " has duplicate characters");
        }
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to illustrate
// string with unique characters
// using brute force technique
function uniqueCharacters($str)
{

    // Assuming string can have
    // characters a-z, this has
    // 32 bits set to 0
    $checker = 0;

    for ($i = 0; $i < strlen($str); $i++)
    {
        $bitAtIndex = $str[$i] - 'a';

        // if that bit is already set
        // in checker, return false
        if (($checker &
            (1 << $bitAtIndex)) > 0)
        {
            return false;
        }

    // otherwise update and continue by
    // setting that bit in the checker
    $checker = $checker |
               (1 << $bitAtIndex);
    }

    // no duplicates encountered,
    // return true
    return true;
}

// Driver Code
$str = "geeksforgeeks";

if(uniqueCharacters($str))
{
    echo "The String ", $str,
         " has all unique characters\n";
}
else
{
    echo "The String ", $str,
         " has duplicate characters\n";
}

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to illustrate String
    // with unique characters without
    // using any data structure

    function uniqueCharacters(str)
    {
        // Assuming string can have
        // characters a-z this has
        // 32 bits set to 0
        let checker = 0;

        for (let i = 0; i < str.length; i++) {
            let bitAtIndex = str[i] - 'a';

            // if that bit is already set
            // in checker, return false
            if ((checker & (1 << bitAtIndex)) > 0) {
                return false;
            }

            // otherwise update and continue by
            // setting that bit in the checker
            checker = checker | (1 << bitAtIndex);
        }

        // no duplicates encountered,
        // return true
        return true;
    }

    let input = "geekforgeeks";

    if (uniqueCharacters(input)) {
      document.write("The String " + input + " has all unique characters");
    }
    else {
      document.write("The String " + input + " has duplicate characters");
    }

</script>
```

**输出:**

```
The String GeekforGeeks has duplicate characters
```

**练习:**上面的程序是不区分大小写的，你可以尝试制作同样区分大小写的程序，即 GEeks 和 Geeks 都给出不同的输出。

使用 [Java 流](https://www.geeksforgeeks.org/stream-in-java/):

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Collections;
import java.util.stream.Collectors;
class GfG {
    boolean uniqueCharacters(String s)
    {
        // If at any character more than once create another stream
        // stream count more than 0, return false
        return s.chars().filter(e-> Collections.frequency(s.chars().boxed().collect(Collectors.toList()), e) > 1).count() > 1 ? false: true;
    }

    public static void main(String args[])
    {
        GfG obj = new GfG();
        String input = "GeeksforGeeks";

        if (obj.uniqueCharacters(input))
            System.out.println("The String " + input + " has all unique characters");
        else
            System.out.println("The String " + input + " has duplicate characters");
    }
}

//Write Java code here
```

**参考:**
破解盖尔的编码访谈

**方法 5:使用 set()函数:**

*   将字符串转换为集合。
*   如果集合的长度等于字符串的长度，则返回真否则返回假。

下面是上述方法的实现

## C++

```
// C++ program to illustrate String with unique
// characters using set data structure
#include <bits/stdc++.h>
using namespace std;

bool uniqueCharacters(string str)
{
    set<char> char_set;

    // Inserting character of string into set
    for(char c : str)
    {
        char_set.insert(c);
    }

    // If length of set is equal to len of string
    // then it will have unique characters
    if (char_set.size() == str.size())
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver code
int main()
{
    string str = "GeeksforGeeks";

    if (uniqueCharacters(str))
    {
        cout << "The String " << str
             << " has all unique characters\n";
    }
    else
    {
        cout << "The String " << str
             << " has duplicate characters\n";
    }
    return 0;
}

// This code is contributed by abhishekjha558498
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate String with unique
// characters using set data structure
import java.util.*;

class GFG{

static boolean uniqueCharacters(String str)
{
    HashSet<Character> char_set = new HashSet<>();

    // Inserting character of String into set
    for(int c  = 0; c< str.length();c++)
    {
        char_set.add(str.charAt(c));
    }

    // If length of set is equal to len of String
    // then it will have unique characters
    if (char_set.size() == str.length())
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver code
public static void main(String[] args)
{
    String str = "GeeksforGeeks";

    if (uniqueCharacters(str))
    {
        System.out.print("The String " +  str
            + " has all unique characters\n");
    }
    else
    {
        System.out.print("The String " +  str
            + " has duplicate characters\n");
    }
}
}

// This code contributed by umadevi9616
```

## 蟒蛇 3

```
# Python3 program to illustrate String with unique
# characters
def uniqueCharacters(str):

    # Converting string to set
    setstring = set(str)

    # If length of set is equal to len of string
    # then it will have unique characters
    if(len(setstring) == len(str)):
        return True

    return False

# Driver Code
if __name__ == '__main__':

    input = "GeeksforGeeks"

    if (uniqueCharacters(input)):
        print("The String " + input +
              " has all unique characters")
    else:
        print("The String " + input +
              " has duplicate characters")

# This code is contributed by vikkycirus
```

## C#

```
// C# program to illustrate String with unique
// characters using set data structure
using System;
using System.Collections.Generic;

public class GFG {

    static bool uniquechars(String str)
    {
        HashSet<char> char_set = new HashSet<char>();

        // Inserting character of String into set
        for (int c = 0; c < str.Length; c++) {
            char_set.Add(str);
        }

        // If length of set is equal to len of String
        // then it will have unique characters
        if (char_set.Count == str.Length) {
            return true;
        }
        else {
            return false;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "GeeksforGeeks";

        if (uniquechars(str)) {
            Console.Write("The String " + str
                          + " has all unique characters\n");
        }
        else {
            Console.Write("The String " + str
                          + " has duplicate characters\n");
        }
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>

// Function program to illustrate String
// with unique characters
function uniqueCharacters(str)
{

    // Converting string to set
    var setstring = new Set(str)

    // If length of set is equal to len of string
    // then it will have unique characters
    if (setstring.size == str.length)
    {
        return true
    }
    else
    {
        return false
    }
}

// Driver Code
var input = "GeeksforGeeks"

if (uniqueCharacters(input))
{
    document.write("The String " + input +
                   " has all unique characters") ;
}
else
{
    document.write("The String " + input +
                   " has duplicate characters")
}

// This code is contributed by bunnyram19

</script>
```

**输出:**

```
The String GeeksforGeeks has duplicate characters
```

**时间复杂度:** O(nlogn)

本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
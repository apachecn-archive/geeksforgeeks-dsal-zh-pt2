# 从给定的列号中找到 Excel 列名

> 原文:[https://www . geesforgeks . org/find-excel-column-name-given-number/](https://www.geeksforgeeks.org/find-excel-column-name-given-number/)

MS Excel 的列有 A，B，C，…，Z，AA，AB，AC，…这样的模式。，AZ，BA，BB，… ZZ，AAA，AAB …..等等。换句话说，第 1 列命名为“A”，第 2 列命名为“B”，第 27 列命名为“AA”。
给定一个列号，找到其对应的 Excel 列名。以下是更多的例子。

```
Input          Output
 26             Z
 51             AY
 52             AZ
 80             CB
 676            YZ
 702            ZZ
 705            AAC
```

感谢 [Mrigank Dembla](https://www.geeksforgeeks.org/amazon-interview-set-95-sde/#) 在评论中提出以下解决方案。
假设我们有一个数字 n，比如说 28。因此，对应于它，我们需要打印列名。我们需要用 26 取余数。

如果带有 26 的余数为 0(意味着 26，52，等等)，那么我们在输出字符串中输入“Z”，新的 n 变成 n/26 -1，因为这里我们认为 26 是“Z”，而实际上它是相对于“A”的第 25 位。

同样，如果余数为非零。(比如 1、2、3 等等)然后我们需要在字符串中相应地插入 char，并做 n = n/26。

最后，我们反转字符串并打印。

**例:**
n = 700
余数(n%26)为 24。所以我们把“X”放在输出字符串中，n 变成 n/26，也就是 26。
余数(26%26)为 0。所以我们把“Z”放在输出字符串中，n 变成 n/26 -1，也就是 0。

下面是上述方法的实现。

## C++

```
// C++ program to find Excel
// column name from a given
// column number
#include <bits/stdc++.h>
#define MAX 50
using namespace std;

// Function to print Excel column name for a given column number
void printString(int n)
{
    char str[MAX]; // To store result (Excel column name)
    int i = 0; // To store current index in str which is result

    while (n > 0) {
        // Find remainder
        int rem = n % 26;

        // If remainder is 0, then a 'Z' must be there in output
        if (rem == 0) {
            str[i++] = 'Z';
            n = (n / 26) - 1;
        }
        else // If remainder is non-zero
        {
            str[i++] = (rem - 1) + 'A';
            n = n / 26;
        }
    }
    str[i] = '\0';

    // Reverse the string and print result
    reverse(str, str + strlen(str));
    cout << str << endl;

    return;
}

// Driver program to test above function
int main()
{
    printString(26);
    printString(51);
    printString(52);
    printString(80);
    printString(676);
    printString(702);
    printString(705);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Excel
// column name from a given
// column number

public class ExcelColumnTitle {
    // Function to print Excel column
    // name for a given column number
    private static void printString(int columnNumber)
    {
        // To store result (Excel column name)
        StringBuilder columnName = new StringBuilder();

        while (columnNumber > 0) {
            // Find remainder
            int rem = columnNumber % 26;

            // If remainder is 0, then a
            // 'Z' must be there in output
            if (rem == 0) {
                columnName.append("Z");
                columnNumber = (columnNumber / 26) - 1;
            }
            else // If remainder is non-zero
            {
                columnName.append((char)((rem - 1) + 'A'));
                columnNumber = columnNumber / 26;
            }
        }

        // Reverse the string and print result
        System.out.println(columnName.reverse());
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        printString(26);
        printString(51);
        printString(52);
        printString(80);
        printString(676);
        printString(702);
        printString(705);
    }
}

// This code is contributed by Harikrishnan Rajan
```

## 计算机编程语言

```
# Python program to find Excel column name from a
# given column number

MAX = 50

# Function to print Excel column name
# for a given column number
def printString(n):

    # To store result (Excel column name)
    string = ["\0"] * MAX

    # To store current index in str which is result
    i = 0

    while n > 0:
        # Find remainder
        rem = n % 26

        # if remainder is 0, then a
        # 'Z' must be there in output
        if rem == 0:
            string[i] = 'Z'
            i += 1
            n = (n / 26) - 1
        else:
            string[i] = chr((rem - 1) + ord('A'))
            i += 1
            n = n / 26
    string[i] = '\0'

    # Reverse the string and print result
    string = string[::-1]
    print "".join(string)

# Driver program to test the above Function
printString(26)
printString(51)
printString(52)
printString(80)
printString(676)
printString(702)
printString(705)

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to find Excel
// column name from a given
// column number
using System;

class GFG{

static String reverse(String input)
{
    char[] reversedString = input.ToCharArray();
    Array.Reverse(reversedString);
    return new String(reversedString);
}

// Function to print Excel column
// name for a given column number
private static void printString(int columnNumber)
{

    // To store result (Excel column name)
    String columnName = "";

    while (columnNumber > 0)
    {

        // Find remainder
        int rem = columnNumber % 26;

        // If remainder is 0, then a
        // 'Z' must be there in output
        if (rem == 0)
        {
            columnName += "Z";
            columnNumber = (columnNumber / 26) - 1;
        }

        // If remainder is non-zero
        else
        {
            columnName += (char)((rem - 1) + 'A');
            columnNumber = columnNumber / 26;
        }
    }

    // Reverse the string
    columnName = reverse(columnName);

    // Print result
    Console.WriteLine(columnName.ToString());
}

// Driver code
public static void Main(String[] args)
{
    printString(26);
    printString(51);
    printString(52);
    printString(80);
    printString(676);
    printString(702);
    printString(705);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript program to find Excel
// column name from a given
// column number

// Function to print Excel column
    // name for a given column number
function printString(columnNumber)
{
    // To store result (Excel column name)
        let columnName = [];

        while (columnNumber > 0) {
            // Find remainder
            let rem = columnNumber % 26;

            // If remainder is 0, then a
            // 'Z' must be there in output
            if (rem == 0) {
                columnName.push("Z");
                columnNumber = Math.floor(columnNumber / 26) - 1;
            }
            else // If remainder is non-zero
            {
                columnName.push(String.fromCharCode((rem - 1) + 'A'.charCodeAt(0)));
                columnNumber = Math.floor(columnNumber / 26);
            }
        }

        // Reverse the string and print result
        document.write(columnName.reverse().join("")+"<br>");
}

// Driver program to test above function
printString(26);
printString(51);
printString(52);
printString(80);
printString(676);
printString(702);
printString(705);

// This code is contributed by rag2127
</script>
```

**Output**

```
Z
AY
AZ
CB
YZ
ZZ
AAC
```

**方法 2**
问题类似于将十进制数转换为其二进制表示，但不是二进制基数系统，其中我们只有两位数字 0 和 1，这里我们有来自 A-Z 的 26 个字符。
所以，我们处理的是基数 26，而不是基数二进制。
这不是乐趣的终点，在这个数字系统中我们没有零，因为 A 代表 1，B 代表 2，以此类推 Z 代表 26。
为了使问题易于理解，我们分两步处理问题:

1.  考虑到系统中也有 0，将数字转换为以 26 为基数的表示。
2.  将表示更改为系统中没有 0 的表示。

怎么做？这里有一个例子

**第一步:**
考虑我们有数字 676，如何得到它在基数 26 系统中的表示？就像我们对一个二进制系统做的一样，我们用 26 做除法和余数，而不是用 2 做除法和余数。

```
Base 26 representation of 676 is : 100 
```

**第二步**
但是嘿，我们的表示不能为零。对吗？因为它不是我们数字系统的一部分。我们如何摆脱零？很简单，但在此之前，让我们提醒一个简单的数学技巧:

```
Subtraction: 
5000 - 9, How do you subtract 9 from 0 ? You borrow
from next significant bit, right.  
```

*   在十进制数字系统中，为了处理零，我们借用 10 并从下一个有效数字中减去 1。
*   在基数为 26 的数字系统中，为了处理零，我们借用 26 并从下一个有效位减去 1。

所以把 100 <sub>26</sub> 转换成没有‘0’的数字系统，我们得到(25 26) <sub>26</sub>
相同的符号表示是:YZ

下面是同样的实现:

## C++

```
#include <iostream>
using namespace std;

void printString(int n)
{
    int arr[10000];
    int i = 0;

    // Step 1: Converting to number assuming
    // 0 in number system
    while (n) {
        arr[i] = n % 26;
        n = n / 26;
        i++;
    }

    // Step 2: Getting rid of 0, as 0 is
    // not part of number system
    for (int j = 0; j < i - 1; j++) {
        if (arr[j] <= 0) {
            arr[j] += 26;
            arr[j + 1] = arr[j + 1] - 1;
        }
    }

    for (int j = i; j >= 0; j--) {
        if (arr[j] > 0)
            cout << char('A' + arr[j] - 1);
    }

    cout << endl;
}

// Driver program to test above function
int main()
{
    printString(26);
    printString(51);
    printString(52);
    printString(80);
    printString(676);
    printString(702);
    printString(705);
    return 0;
}

// This code is contributed by Ankur Goel
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

static void printString(int n)
{
    int []arr = new int[10000];
    int i = 0;

    // Step 1: Converting to number
    // assuming 0 in number system
    while (n > 0)
    {
        arr[i] = n % 26;
        n = n / 26;
        i++;
    }

    // Step 2: Getting rid of 0, as 0 is
    // not part of number system
    for(int j = 0; j < i - 1; j++)
    {
        if (arr[j] <= 0)
        {
            arr[j] += 26;
            arr[j + 1] = arr[j + 1] - 1;
        }
    }

    for(int j = i; j >= 0; j--)
    {
        if (arr[j] > 0)
            System.out.print(
                (char)('A' + arr[j] - 1));
    }
    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    printString(26);
    printString(51);
    printString(52);
    printString(80);
    printString(676);
    printString(702);
    printString(705);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
def printString(n):

    arr = [0] * 10000
    i = 0

    # Step 1: Converting to number
    # assuming 0 in number system
    while (n > 0):
        arr[i] = n % 26
        n = int(n // 26)
        i += 1

    #Step 2: Getting rid of 0, as 0 is
    # not part of number system
    for j in range(0, i - 1):
        if (arr[j] <= 0):
            arr[j] += 26
            arr[j + 1] = arr[j + 1] - 1

    for j in range(i, -1, -1):
        if (arr[j] > 0):
            print(chr(ord('A') +
                  (arr[j] - 1)), end = "");

    print();

# Driver code
if __name__ == '__main__':

    printString(26);
    printString(51);
    printString(52);
    printString(80);
    printString(676);
    printString(702);
    printString(705);

# This code is contributed by Princi Singh
```

## C#

```
using System;
class GFG{

static void printString(int n)
{
  int []arr = new int[10000];
  int i = 0;

  // Step 1: Converting to
  // number assuming 0 in
  // number system
  while (n > 0)
  {
    arr[i] = n % 26;
    n = n / 26;
    i++;
  }

  // Step 2: Getting rid of 0,
  // as 0 is not part of number
  // system
  for(int j = 0; j < i - 1; j++)
  {
    if (arr[j] <= 0)
    {
      arr[j] += 26;
      arr[j + 1] = arr[j + 1] - 1;
    }
  }

  for(int j = i; j >= 0; j--)
  {
    if (arr[j] > 0)
      Console.Write((char)('A' +
                     arr[j] - 1));
  }
  Console.WriteLine();
}

// Driver code
public static void Main(String[] args)
{
  printString(26);
  printString(51);
  printString(52);
  printString(80);
  printString(676);
  printString(702);
  printString(705);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

function printString(n){
    let arr = [];
    let i = 0;

    // Step 1: Converting to number assuming
    // 0 in number system
    while (n) {
        arr[i] = n % 26;
        n = Math.floor(n / 26);
        i++;
    }

    // Step 2: Getting rid of 0, as 0 is
    // not part of number system
    for (let j = 0; j < i - 1; j++) {
        if (arr[j] <= 0) {
            arr[j] += 26;
            arr[j + 1] = arr[j + 1] - 1;
        }
    }
    let ans = '';
    for (let j = i; j >= 0; j--) {
        if (arr[j] > 0)
            ans += String.fromCharCode(65 + arr[j] - 1);
    }

    document.write(ans + "<br>");
}

// Driver program to test above function

printString(26);
printString(51);
printString(52);
printString(80);
printString(676);
printString(702);
printString(705);

</script>
```

**Output**

```
Z
AY
AZ
CB
YZ
ZZ
AAC
```

**方法 3:**

**我们可以使用递归函数，这肯定会减少时间，提高效率:**

字母表是按顺序排列的，比如:“ABCDEFGHIJKLMNOPQRSTUVWXYZ”。您在使用 excel 时已经体验到，列和行的编号是按字母顺序进行的。

以下是我如何有目的地思考逻辑是如何安排的。

(在数学术语中，[a，b ]表示从‘a’到‘b’)。

[1，26] = [A，Z](理解为‘1’代表‘A’，而‘26’代表‘Z”)。对于[27，52]，它将像[AA，AZ]，对于[57，78]，它将是[BA，BZ]

逻辑是每当字母表以 26 结尾时，就按顺序追加字母表。

例如，如果数字是‘27’，大于‘26’，那么我们只需要除以 26，我们得到的余数是 1，我们看到“1”是“A”，可以递归完成。

我们将为此使用 python..

算法是:

1.取一个数组，将字母从 A 到 Z 排序。(也可以使用导入字符串和字符串函数获取大写的“A 到 Z”。)

2.**如果**数小于等于‘26’，只需从数组中获取字母并打印即可。

3.**如果**大于 26，使用商数余数规则，如果余数为零，有 2 种可能的方法，**如果**商数为“1”，只需从索引[r-1](‘r’是余数)中散列出字母，**否则**从 num =(q-1)中调用函数，并在前面追加到字母索引[r-1]中。

4.**如果**余数不等于“0”，调用 num = (q)的函数，并在前面追加字母索引[r-1]。

与此相关的代码是:

## 蟒蛇 3

```
# Or you can simply take a string and perform this logic ,no issue i found in here.
alpha = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
# defined a recursive function here.
# if number is less than "26", simply hash out (index-1)
# There are sub possibilities in possibilities,
# 1.if remainder is zero(if quotient is 1 or not 1) and
# 2\. if remainder is not zero

def num_hash(num):
    if num < 26:
        return alpha[num-1]
    else:
        q, r = num//26, num % 26
        if r == 0:
            if q == 1:
                return alpha[r-1]
            else:
                return num_hash(q-1) + alpha[r-1]
        else:
            return num_hash(q) + alpha[r-1]

# Calling the function out here and printing the ALphabets
# This code is robust ,work for any positive integer only.
# You can try as much as you want
print(num_hash(26))
print(num_hash(51))
print(num_hash(52))
print(num_hash(80))
print(num_hash(676))
print(num_hash(702))
print(num_hash(705))
```

**Output**

```
Z
AY
AZ
CB
YZ
ZZ
AAC
```

**相关文章:**
[从栏目标题](https://www.geeksforgeeks.org/find-excel-column-number-column-title/)
找到 Excel 栏目编号本文由 **Kartik** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
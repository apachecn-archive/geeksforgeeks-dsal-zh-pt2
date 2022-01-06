# 字符串的不同排列|第 2 集

> 原文:[https://www . geesforgeks . org/distinct-置换-string-set-2/](https://www.geeksforgeeks.org/distinct-permutations-string-set-2/)

打印重复字符串的所有不同排列。

**示例:**

```
Input : ABCA
Output : AABC AACB ABAC ABCA ACBA 
         ACAB BAAC BACA BCAA CABA 
         CAAB CBAA
```

打印所有不同排列的算法已经在这里讨论过了。在这里，我们将讨论另一种方法来做同样的事情。首先回想一下我们如何在输入字符串中打印没有任何重复的排列。这里给出。现在让我们以字符串“ABAC”为例。生成排列时，假设我们在 index = 0，用它后面的所有元素交换它。当我们达到 i=2 时，我们看到在字符串 s[index…i-1]中，有一个等于 s[i]的索引。因此，交换它将产生重复的排列。因此，我们不交换它。下面更好解释。

**图解**:用下面的例子让我们理解一下。

```
i = 0 1 2 3
    A B A C
index = 0, s[0] = A
Start swapping s[index] with s[i] following it:
i = index + 1 = 1 

Since s[index] != s[i], swap and recur.

i = 2, s[index] == s[i], don't swap

i = 3,  s[index] != s[i], swap and recur. 
```

下面的代码也是如此。

## C++

```
// C++ program to distinct permutations of the string
#include <bits/stdc++.h>
using namespace std;

// Returns true if str[curr] does not matches with any of the
// characters after str[start]
bool shouldSwap(char str[], int start, int curr)
{
    for (int i = start; i < curr; i++)
        if (str[i] == str[curr])
            return 0;
    return 1;
}

// Prints all distinct permutations in str[0..n-1]
void findPermutations(char str[], int index, int n)
{
    if (index >= n) {
        cout << str << endl;
        return;
    }

    for (int i = index; i < n; i++) {

        // Proceed further for str[i] only if it
        // doesn't match with any of the characters
        // after str[index]
        bool check = shouldSwap(str, index, i);
        if (check) {
            swap(str[index], str[i]);
            findPermutations(str, index + 1, n);
            swap(str[index], str[i]);
        }
    }
}

// Driver code
int main()
{
    char str[] = "ABCA";
    int n = strlen(str);
    findPermutations(str, 0, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to distinct permutations of the string
public class GFG {

// Returns true if str[curr] does not matches with any of the
// characters after str[start]
    static boolean shouldSwap(char str[], int start, int curr) {
        for (int i = start; i < curr; i++) {
            if (str[i] == str[curr]) {
                return false;
            }
        }
        return true;
    }

// Prints all distinct permutations in str[0..n-1]
    static void findPermutations(char str[], int index, int n) {
        if (index >= n) {
            System.out.println(str);
            return;
        }

        for (int i = index; i < n; i++) {

            // Proceed further for str[i] only if it
            // doesn't match with any of the characters
            // after str[index]
            boolean check = shouldSwap(str, index, i);
            if (check) {
                swap(str, index, i);
                findPermutations(str, index + 1, n);
                swap(str, index, i);
            }
        }
    }

    static void swap(char[] str, int i, int j) {
        char c = str[i];
        str[i] = str[j];
        str[j] = c;
    }

    // Driver code
    public static void main(String[] args) {

        char str[] = {'A', 'B', 'C', 'A'};
        int n = str.length;
        findPermutations(str, 0, n);
    }

}
```

## 蟒蛇 3

```
# Python3 program to distinct
# permutations of the string

# Returns true if str[curr] does not
# matches with any of the characters
# after str[start]
def shouldSwap(string, start, curr):

    for i in range(start, curr):
        if string[i] == string[curr]:
            return 0
    return 1

# Prints all distinct permutations
# in str[0..n-1]
def findPermutations(string, index, n):

    if index >= n:
        print(''.join(string))
        return

    for i in range(index, n):

        # Proceed further for str[i] only
        # if it doesn't match with any of
        # the characters after str[index]
        check = shouldSwap(string, index, i)
        if check:
            string[index], string[i] = string[i], string[index]
            findPermutations(string, index + 1, n)
            string[index], string[i] = string[i], string[index]

# Driver code
if __name__ == "__main__":

    string = list("ABCA")
    n = len(string)
    findPermutations(string, 0, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to distinct permutations
// of the string
using System;

class GFG
{

// Returns true if str[curr] does
// not matches with any of the
// characters after str[start]
static bool shouldSwap(char []str,
                       int start, int curr)
{
    for (int i = start; i < curr; i++)
    {
        if (str[i] == str[curr])
        {
            return false;
        }
    }
    return true;
}

// Prints all distinct permutations
// in str[0..n-1]
static void findPermutations(char []str,
                             int index, int n)
{
    if (index >= n)
    {
        Console.WriteLine(str);
        return;
    }

    for (int i = index; i < n; i++)
    {

        // Proceed further for str[i] only
        // if it doesn't match with any of
        // the characters after str[index]
        bool check = shouldSwap(str, index, i);
        if (check)
        {
            swap(str, index, i);
            findPermutations(str, index + 1, n);
            swap(str, index, i);
        }
    }
}

static void swap(char[] str, int i, int j)
{
    char c = str[i];
    str[i] = str[j];
    str[j] = c;
}

// Driver code
public static void Main()
{
    char []str = {'A', 'B', 'C', 'A'};
    int n = str.Length;
    findPermutations(str, 0, n);
}
}

// This code is contributed
// by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to distinct permutations of the string

// Returns true if str[curr] does not matches with any of the
// characters after str[start]
    function shouldSwap(str, start, curr) {
        for (let i = start; i < curr; i++) {
            if (str[i] == str[curr]) {
                return false;
            }
        }
        return true;
    }

// Prints all distinct permutations in str[0..n-1]
    function findPermutations(str, index, n) {
        if (index >= n) {
            document.write(str);
            document.write("<br/>")
            return;
        }

        for (let i = index; i < n; i++) {

            // Proceed further for str[i] only if it
            // doesn't match with any of the characters
            // after str[index]
            let check = shouldSwap(str, index, i);
            if (check) {
                swap(str, index, i);
                findPermutations(str, index + 1, n);
                swap(str, index, i);
            }
        }
    }

    function swap(str, i, j) {
        let c = str[i];
        str[i] = str[j];
        str[j] = c;
    }

// Driver code

        let str = ['A', 'B', 'C', 'A'];
        let n = str.length;
        findPermutations(str, 0, n);

</script>
```

**Output**

```
ABCA
ABAC
ACBA
ACAB
AACB
AABC
BACA
BAAC
BCAA
CBAA
CABA
CAAB
```

**更好的方法:**

生成所有不同的字符串就是简单地使用一些 if 条件。上面的技术在递归中使用了一个额外的循环，这导致了很大的时间复杂度。相反，我们可以通过一些预处理来改进它。我们首先给定的字符串排序，然后应用下面的代码。

下面是上述想法的实现:

## C++

```
// C++ program to print all the permutation
// of the given string.
#include <algorithm>
#include <iostream>
#include <string>
using namespace std;

// count of total permutations
int total = 0;

void permute(int i, string s)
{
    // base case
    if (i == (s.length() - 1)) {
        cout << s << endl;
        total++;
        return;
    }

    char prev = '*';

    // loop from j = 1 to length of string
    for (int j = i; j < s.length(); j++) {
        string temp = s;
        if (j > i && temp[i] == temp[j])
            continue;
        if (prev != '*' && prev == s[j]) {
            continue;
        }

        // swap the elements
        swap(temp[i], temp[j]);
        prev = s[j];

        // recursion call
        permute(i + 1, temp);
    }
}

// Driver code
int main()
{
    string s = "abca";

    // sort
    sort(s.begin(), s.end());

    // Function call
    permute(0, s);
    cout << "Total distinct permutations = " << total
         << endl;
    return 0;
}

// This code is contributed by risingStark.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all the permutation
// of the given String.
//include <algorithm>

//include <String>
import java.util.*;

class GFG{

// Count of total permutations
static int total = 0;

static void permute(int i, String s)
{

    // Base case
    if (i == (s.length() - 1))
    {
        System.out.print(s + "\n");
        total++;
        return;
    }

    char prev = '*';

    // Loop from j = 1 to length of String
    for(int j = i; j < s.length(); j++)
    {
        char []temp = s.toCharArray();
        if (j > i && temp[i] == temp[j])
            continue;
        if (prev != '*' && prev == s.charAt(j))
        {
            continue;
        }

        // Swap the elements
        temp = swap(temp,i,j);
        prev = s.charAt(j);

        // Recursion call
        permute(i + 1, String.valueOf(temp));
    }
}

static char[] swap(char []arr, int i, int j)
{
    char temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

static String sortString(String inputString)
{

    // Convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // Sort tempArray
    Arrays.sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Driver code
public static void main(String[] args)
{
    String s = "abca";

    // Sort
    s = sortString(s);

    // Function call
    permute(0, s);
    System.out.print("Total distinct permutations = " +
                     total +"\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to print all the permutation
// of the given String.

// Count of total permutations
let total = 0;
function permute(i,s)
{
    // Base case
    if (i == (s.length - 1))
    {
        document.write(s + "<br>");
        total++;
        return;
    }

    let prev = '*';

    // Loop from j = 1 to length of String
    for(let j = i; j < s.length; j++)
    {
        let temp = s.split("");
        if (j > i && temp[i] == temp[j])
            continue;
        if (prev != '*' && prev == s[j])
        {
            continue;
        }

        // Swap the elements
        temp = swap(temp,i,j);
        prev = s[j];

        // Recursion call
        permute(i + 1, (temp).join(""));
    }
}

function swap(arr,i,j)
{
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

function sortString(inputString)
{
    // Convert input string to char array
    let tempArray = inputString.split("");

    // Sort tempArray
    (tempArray).sort();

    // Return new sorted string
    return (tempArray).join("");
}

// Driver code
let s = "abca";

// Sort
s = sortString(s);

// Function call
permute(0, s);
document.write("Total distinct permutations = " +
                 total +"<br>");

// This code is contributed by rag2127

</script>
```

**Output**

```
aabc
aacb
abac
abca
acba
acab
baac
baca
bcaa
caba
caab
cbaa
Total distinct permutations = 12
```

**时间复杂度:**如果我们取字符串的长度为 N，那么我的代码复杂度将为 O(N log N)进行排序，O(N*N！)进行排列。总时间复杂度为 0(N 对数 N + N*N！)这实际上只是 O(N*N！).
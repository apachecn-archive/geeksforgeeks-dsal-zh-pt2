# 将一个回文串转换成另一个回文串所需的最小切割数

> 原文:[https://www . geesforgeks . org/minimum-cuts-需要将一个回文串转换为不同的回文串/](https://www.geeksforgeeks.org/minimum-cuts-required-to-convert-a-palindromic-string-to-a-different-palindromic-string/)

给定回文串 **s** ，任务是找到最小值 **k** ，这样你就可以把这个串切割成 **k+1** 个部分，然后把它们统一起来，这样最后的串就是一个回文，它就不等于最初的串 **s** 。如果不可能，则打印 **-1** 。
**举例:**

```
Input : string = "civic" 
Output : 2
Explanation : ci | v | ic --> ic | v | ci --> icvci

Input : string = "gggg"
Output : -1

Input : string = "redder" 
Output : 1
Explanation : red | der --> der | red --> derred

Input : string = "aaaasaaaa" 
Output : -1
```

**方法 1:** 给出形成的回文串应该与给定的串不同。
所以当我们的字符串由 n 或 n-1(当 n 为奇数时)个相等的字符组成时，那么就没有办法得到答案。例如–

```
String : "aaaasaaaa"
String : "aaaa"
```

以上字符串不能形成除给定字符串以外的回文。
否则，剪切长度为 **l** 的最长前缀 s，该前缀由长度等于 **l-1** 的相等字符组成。现在类似地剪切长度为 **l-1** 的后缀，并将剩余部分称为中间部分。
现在我们有**前缀= s[1..l]** 和 suf =**s[(n-l+1)..n]** 。交换前缀和后缀，然后把三个部分结合在一起，保持中间不变。

```
prefix + mid + suffix [Tex]suffix + mid + prefix[/Tex]
```

所以很明显我们可以分两次得到答案。最后，你只需要检查一下是否有可能一次得到答案。为此，只需从头到尾剪切一个元素，并将其附加在前面，然后继续这个循环移位。在此期间，如果我们得到一个回文字符串，而不是给定的字符串，那么这意味着我们可以在一次剪切中得到答案。
以下是上述方法的实施:

## C++

```
// CPP program to solve the above problem

#include <bits/stdc++.h>
using namespace std;

// Function to check if string is palindrome or not
bool isPalindrome(string s)
{
    for (int i = 0; i < s.length(); ++i) {
        if (s[i] != s[s.length() - i - 1]) {
            return false;
        }
    }
    return true;
}

// Function to check if it is possible to
// get result by making just one cut
bool ans(string s)
{
    string s2 = s;

    for (int i = 0; i < s.length(); ++i) {
        // Appending last element in front
        s2 = s2.back() + s2;
        // Removing last element
        s2.pop_back();

        // Checking whether string s2 is palindrome
        // and different from s.
        if (s != s2 && isPalindrome(s2)) {
            return true;
        }
    }
    return false;
}

int solve(string s)
{
    // If length is <=3 then it is impossible
    if (s.length() <= 3) {
        return -1;
    }

    // Array to store frequency of characters
    int cnt[25] = {};

    // Store count of characters in a array
    for (int i = 0; i < s.length(); i++) {
        cnt[s[i] - 'a']++;
    }

    // Condition for edge cases
    if (*max_element(cnt, cnt + 25) >= (s.length() - 1)) {
        return -1;
    }
    else {
        // Return 1 if it is possible to get palindromic
        // string in just one cut.
        // Else we can always reached in two cuttings.
        return (ans(s) ? 1 : 2);
    }
}

// Driver Code
int main()
{

    string s = "nolon";

    cout << solve(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve the above problem
import java.util.Arrays;

class GFG
{

// Function to check if string is palindrome or not
static boolean isPalindrome(String s)
{
    for (int i = 0; i < s.length(); ++i)
    {
        if (s.charAt(i) != s.charAt(s.length() - i - 1))
        {
            return false;
        }
    }
    return true;
}

// Function to check if it is possible to
// get result by making just one cut
static boolean ans(String s)
{
    String s2 = s;

    for (int i = 0; i < s.length(); ++i)
    {
        // Appending last element in front
        s2 = s2.charAt(s2.length()-1) + s2;

        // Removing last element
        s2 = s2.substring(0,s2.length()-1);

        // Checking whether string s2 is palindrome
        // and different from s.
        if ((s == null ? s2 != null : !s.equals(s2)) &&
                                        isPalindrome(s2))
        {
            return true;
        }
    }
    return false;
}

static int solve(String s)
{
    // If length is <=3 then it is impossible
    if (s.length() <= 3)
    {
        return -1;
    }

    // Array to store frequency of characters
    int cnt[] = new int[25];

    // Store count of characters in a array
    for (int i = 0; i < s.length(); i++)
    {
        cnt[s.charAt(i) - 'a']++;
    }

    // Condition for edge cases
    if (Arrays.stream(cnt).max().getAsInt() >=
                                (s.length() - 1))
    {
        return -1;
    }
    else
    {
        // Return 1 if it is possible to get palindromic
        // string in just one cut.
        // Else we can always reached in two cuttings.
        return (ans(s) ? 1 : 2);
    }
}

// Driver Code
public static void main(String[] args)
{
        String s = "nolon";
        System.out.println(solve(s));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to solve the above problem

# Function to check if string is palindrome or not
def isPalindrome(s):
    for i in range(len(s)):
        if (s[i] != s[len(s) - i - 1]):
            return False

    return true

# Function to check if it is possible to
# get result by making just one cut
def ans(s):
    s2 = s

    for i in range(len(s)):

        # Appending last element in front
        s2 = s2[len(s2) - 1] + s2

        # Removing last element
        s2 = s2[0:len(s2) - 1]

        # Checking whether string s2 is palindrome
        # and different from s.
        if (s != s2 and isPalindrome(s2)):
            return True

    return False

def solve(s):

    # If length is <=3 then it is impossible
    if (len(s) <= 3):
        return -1

    # Array to store frequency of characters
    cnt = [0 for i in range(26)]

    # Store count of characters in a array
    for i in range(len(s)):
        cnt[ord(s[i]) - ord('a')] += 1

    # Condition for edge cases
    max = cnt[0]
    for i in range(len(cnt)):
        if cnt[i]>max:
            max = cnt[i]
    if (max >= len(s) - 1):
        return -1

    else:

        # Return 1 if it is possible to get
        # palindromic string in just one cut.
        # Else we can always reached in two cuttings.
        if ans(s) == True:
            return 1
        else:
            return 2

# Driver Code
if __name__ == '__main__':
    s = "nolon"

    print(solve(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to solve the above problem
using System;
using System.Linq;

class GFG
{

// Function to check if string is palindrome or not
static bool isPalindrome(string s)
{
    for (int i = 0; i < s.Length; ++i)
    {
        if (s[i] != s[s.Length - i - 1])
        {
            return false;
        }
    }
    return true;
}

// Function to check if it is possible to
// get result by making just one cut
static bool ans(string s)
{
    string s2 = s;

    for (int i = 0; i < s.Length; ++i)
    {
        // Appending last element in front
        s2 = s2[s2.Length-1] + s2;

        // Removing last element
        s2 = s2.Substring(0,s2.Length-1);

        // Checking whether string s2 is palindrome
        // and different from s.
        if ((s == null ? s2 != null : !s.Equals(s2)) &&
                                        isPalindrome(s2))
        {
            return true;
        }
    }
    return false;
}

static int solve(string s)
{
    // If length is <=3 then it is impossible
    if (s.Length <= 3)
    {
        return -1;
    }

    // Array to store frequency of characters
    int[] cnt = new int[25];

    // Store count of characters in a array
    for (int i = 0; i < s.Length; i++)
    {
        cnt[s[i] - 'a']++;
    }

    // Condition for edge cases
    if (cnt.Max() >=(s.Length - 1))
    {
        return -1;
    }
    else
    {
        // Return 1 if it is possible to get palindromic
        // string in just one cut.
        // Else we can always reached in two cuttings.
        return (ans(s) ? 1 : 2);
    }
}

// Driver Code
static void Main()
{
    string s = "nolon";
    Console.WriteLine(solve(s));
}
}

// This code contributed by mits
```

## java 描述语言

```
<script>

// JavaScript program to solve the above problem

// Function to check if string is palindrome or not
function isPalindrome(s)
{
    for (let i = 0; i < s.length; ++i)
    {
        if (s[i] != s[s.length - i - 1])
        {
            return false;
        }
    }
    return true;
}

// Function to check if it is possible to
// get result by making just one cut
function ans(s)
{
    let s2 = s;

    for (let i = 0; i < s.length; ++i)
    {
        // Appending last element in front
        s2 = s2[s2.length-1] + s2;

        // Removing last element
        s2 = s2.substring(0,s2.length-1);

        // Checking whether string s2 is palindrome
        // and different from s.
        if ((s == null ? s2 != null : !s == (s2)) &&
                                        isPalindrome(s2))
        {
            return true;
        }
    }
    return false;
}

function solve(s)
{
    // If length is <=3 then it is impossible
    if (s.length <= 3)
    {
        return -1;
    }

    // Array to store frequency of characters
    let cnt = new Array(25);
    for(let i=0;i<25;i++)
        cnt[i]=0;

    // Store count of characters in a array
    for (let i = 0; i < s.length; i++)
    {
        cnt[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    // Condition for edge cases
    if (Math.max(...cnt) >= (s.length - 1))
    {
        return -1;
    }
    else
    {
        // Return 1 if it is possible to get palindromic
        // string in just one cut.
        // Else we can always reached in two cuttings.
        return (ans(s) ? 1 : 2);
    }
}

// Driver Code
let s = "nolon";
document.write(solve(s));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(N)
**高效途径:**同样，如果我们的字符串由 N 或 n-1(当 N 为奇数时)个相等的字符组成，那么就没有办法得到答案。
现在，把这个问题分成两部分:弦长是**偶数**还是**奇数**。
如果字符串长度为**奇数**，那么我们总是有一个中间元素在其中，所以只需在中间元素周围进行 2 次切割，将字符串分成三段，并交换第一段和第三段。
比如说，我们有一个字符串:

```
nolon --> no | l | on --> on | l | no --> onlno
```

如果字符串长度为**甚至**，那么检查半字符串本身是否是回文字符串。
如果是这样的话:

1.  将一个字符串递归地分成两部分，检查得到的半个字符串是否是回文。
2.  如果字符串长度为奇数，则简单地返回 2。

```
asaasa --> as | aa | sa --> sa | aa | as --> saaaas
```

1.  如果结果字符串不是回文，则返回 1。

```
toottoot --> to | ottoot --> ottoot | to --> ottootto
```

否则我们可以从中间剪断这根绳子，形成两段，然后互相交换。
**例如** :

```
voov --> vo | ov --> ov | vo --> ovvo
```

以下是上述方法的实现:

## C++

```
// CPP program to solve the above problem

#include <bits/stdc++.h>
using namespace std;

// Recursive function to find minimum number
// of cuts if length of string is even
int solveEven(string s)
{
    // If length is odd then return 2
    if (s.length() % 2 == 1)
        return 2;

    // To check if half of palindromic string
    // is itself a palindrome
    string ls = s.substr(0, s.length() / 2);

    string rs = s.substr(s.length() / 2, s.length());

    // If not then return 1
    if (ls != rs)
        return 1;

    // Else call function with half palindromic string
    return solveEven(ls);
}

// Function to find minimum number of cuts
// If length of string is odd
int solveOdd(string s)
{
    return 2;
}

int solve(string s)
{
    // If length is <=3 then it is impossible
    if (s.length() <= 3) {
        return -1;
    }

    // Array to store frequency of characters
    int cnt[25] = {};

    // Store count of characters in a array
    for (int i = 0; i < s.length(); i++) {
        cnt[s[i] - 'a']++;
    }

    // Condition for edge cases
    if (*max_element(cnt, cnt + 25) >= s.length() - 1) {
        return -1;
    }

    // If length is even
    if (s.length() % 2 == 0)
        return solveEven(s);

    // If length is odd
    if (s.length() % 2 == 1)
        return solveOdd(s);
}

// Driver Code
int main()
{
    string s = "nolon";

    cout << solve(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve the above problem
import java.util.Arrays;

class GFG
{

    // Recursive function to find minimum number
    // of cuts if length of String is even
    static int solveEven(String s)
    {
        // If length is odd then return 2
        if (s.length() % 2 == 1)
        {
            return 2;
        }

        // To check if half of palindromic String
        // is itself a palindrome
        String ls = s.substring(0, s.length() / 2);

        String rs = s.substring(s.length() / 2, s.length());

        // If not then return 1
        if (ls != rs)
        {
            return 1;
        }

        // Else call function with half palindromic String
        return solveEven(ls);
    }

    // Function to find minimum number of cuts
    // If length of String is odd
    static int solveOdd(String s)
    {
        return 2;
    }

    static int solve(String s)
    {
        // If length is <=3 then it is impossible
        if (s.length() <= 3)
        {
            return -1;
        }

        // Array to store frequency of characters
        int cnt[] = new int[25];

        // Store count of characters in a array
        for (int i = 0; i < s.length(); i++)
        {
            cnt[s.charAt(i) - 'a']++;
        }

        // Condition for edge cases
        if (Arrays.stream(cnt).max().getAsInt() >= s.length() - 1)
        {
            return -1;
        }

        // If length is even
        if (s.length() % 2 == 0)
        {
            return solveEven(s);
        }

        // If length is odd
        if (s.length() % 2 == 1)
        {
            return solveOdd(s);
        }
        return Integer.MIN_VALUE;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "nolon";
        System.out.println(solve(s));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to solve the above problem

# Recursive function to find minimum number
# of cuts if length of string is even
def solveEven(s):

    # If length is odd then return 2
    if len(s) % 2 == 1:
        return 2

    # To check if half of palindromic
    # string is itself a palindrome
    ls = s[0 : len(s) // 2]
    rs = s[len(s) // 2 : len(s)]

    # If not then return 1
    if ls != rs:
        return 1

    # Else call function with
    # half palindromic string
    return solveEven(ls)

# Function to find minimum number of cuts
# If length of string is odd
def solveOdd(s):
    return 2

def solve(s):

    # If length is <=3 then it is impossible
    if len(s) <= 3:
        return -1

    # Array to store frequency of characters
    cnt = [0] * 25

    # Store count of characters in a array
    for i in range(0, len(s)):
        cnt[ord(s[i]) - ord('a')] += 1

    # Condition for edge cases
    if max(cnt) >= len(s) - 1:
        return -1

    # If length is even
    if len(s) % 2 == 0:
        return solveEven(s)

    # If length is odd
    if len(s) % 2 == 1:
        return solveOdd(s)

# Driver Code
if __name__ == "__main__":

    s = "nolon"
    print(solve(s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to solve the above problem
using System;
using System.Linq;

class GFG
{

    // Recursive function to find minimum number
    // of cuts if length of String is even
    static int solveEven(String s)
    {
        // If length is odd then return 2
        if (s.Length % 2 == 1)
        {
            return 2;
        }

        // To check if half of palindromic String
        // is itself a palindrome
        String ls = s.Substring(0, s.Length / 2);

        String rs = s.Substring(s.Length / 2, s.Length);

        // If not then return 1
        if (ls != rs)
        {
            return 1;
        }

        // Else call function with half palindromic String
        return solveEven(ls);
    }

    // Function to find minimum number of cuts
    // If length of String is odd
    static int solveOdd(String s)
    {
        return 2;
    }

    static int solve(String s)
    {
        // If length is <=3 then it is impossible
        if (s.Length <= 3)
        {
            return -1;
        }

        // Array to store frequency of characters
        int []cnt = new int[25];

        // Store count of characters in a array
        for (int i = 0; i < s.Length; i++)
        {
            cnt[s[i] - 'a']++;
        }

        // Condition for edge cases
        if (cnt.Max() >= s.Length - 1)
        {
            return -1;
        }

        // If length is even
        if (s.Length % 2 == 0)
        {
            return solveEven(s);
        }

        // If length is odd
        if (s.Length % 2 == 1)
        {
            return solveOdd(s);
        }
        return int.MinValue;
    }

    // Driver Code
    public static void Main()
    {
        String s = "nolon";
        Console.WriteLine(solve(s));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to solve the above problem

// Recursive function to find minimum number
    // of cuts if length of String is even
function solveEven(s)
{
    // If length is odd then return 2
        if (s.length % 2 == 1)
        {
            return 2;
        }

        // To check if half of palindromic String
        // is itself a palindrome
        let ls = s.substring(0, s.length / 2);

        let rs = s.substring(s.length / 2, s.length);

        // If not then return 1
        if (ls != rs)
        {
            return 1;
        }

        // Else call function with half palindromic String
        return solveEven(ls);
}

// Function to find minimum number of cuts
    // If length of String is odd
function solveOdd(s)
{
    return 2;
}

function solve(s)
{
    // If length is <=3 then it is impossible
        if (s.length <= 3)
        {
            return -1;
        }

        // Array to store frequency of characters
        let cnt = new Array(25);
        for(let i=0;i<25;i++)
            cnt[i]=0;

        // Store count of characters in a array
        for (let i = 0; i < s.length; i++)
        {
            cnt[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        // Condition for edge cases
        if (Math.max(...cnt) >= s.length - 1)
        {
            return -1;
        }

        // If length is even
        if (s.length % 2 == 0)
        {
            return solveEven(s);
        }

        // If length is odd
        if (s.length % 2 == 1)
        {
            return solveOdd(s);
        }
        return Number.MIN_VALUE;
}

// Driver Code
let s = "nolon";
document.write(solve(s));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)

**辅助** **空间** : O(max(26，N))
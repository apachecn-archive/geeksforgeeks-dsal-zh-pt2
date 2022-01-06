# 为使给定的两个字符串相等，从末尾删除的最少字符数

> 原文:[https://www . geeksforgeeks . org/要删除的最少字符数-从末端到使给定的两个字符串相等/](https://www.geeksforgeeks.org/minimum-characters-to-be-deleted-from-the-end-to-make-given-two-strings-equal/)

给定两个字符串 **S1** 和 **S2** ，任务是找到要从两个字符串末尾删除的最小字符数，使它们相等。

> 两个空字符串将被视为相同。

**示例:**

> **输入:**S1 =“ABCD”，S2 =“absefr”
> **输出:** 6
> **说明:**
> S1 末尾删除字符{'d '，' c'}，S2 末尾删除字符{'r '，' f '，' e '，' s'}使字符串相等。
> 
> **输入:** S1 =【极客】，S2 =【极客 for】
> **输出:** 3
> **说明:**
> S2 末尾删除字符{'f '，' o '，' r'}。

**方法:**
同时从两个字符串的开头开始迭代，检查字符是否相等。两个字符串中字符不同的第一个索引是两个字符串末尾的所有字符都需要删除的索引。

以下是上述方法的实现:

## C++

```
// C++ Program to count minimum
// number of characters to be deleted
// to make the strings equal
#include <bits/stdc++.h>
using namespace std;

// Function that finds minimum
// character required to be deleted
int minDel(string s1, string s2)
{
    int i = 0;

    // Iterate in the strings
    while (i < min(s1.length(),
                   s2.length())) {

        // Check if the characters are
        // not equal
        if (s1[i] != s2[i]) {

            break;
        }

        i++;
    }

    // Return the result
    int ans = (s1.length() - i)
              + (s2.length() - i);
    return ans;
}

// Driver Program
int main()
{
    string s1 = "geeks",
           s2 = "geeksfor";

    cout << minDel(s1, s2)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum number  
// of characters to be deleted to make  
// the strings equal 

class GFG{

// Function that finds minimum 
// character required to be deleted 
static int minDel(String s1, String s2)
{
    int i = 0;

    // Iterate in the strings 
    while (i < Math.min(s1.length(), 
                        s2.length())) 
    {

        // Check if the characters are 
        // not equal 
        if (s1.charAt(i) != s2.charAt(i))
        {
            break;
        }
        i++;
    }

    // Return the result 
    int ans = ((s1.length() - i) + 
               (s2.length() - i));
    return ans;
}

// Driver code 
public static void main(String[] args)
{
    String s1 = "geeks";
    String s2 = "geeksfor";

    System.out.println(minDel(s1, s2));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to count minimum number
# of characters to be deleted to make
# the strings equal

# Function that finds minimum
# character required to be deleted
def minDel(s1, s2):

    i = 0;

    # Iterate in the strings
    while (i < min(len(s1), len(s2))):

        # Check if the characters are
        # not equal
        if (s1[i] != s2[i]):
            break;

        i += 1;

    # Return the result
    ans = ((len(s1) - i) + (len(s2) - i));
    return ans;

# Driver code
if __name__ == '__main__':

    s1 = "geeks";
    s2 = "geeksfor";

    print(minDel(s1, s2));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to count minimum number 
// of characters to be deleted to make 
// the strings equal 
using System;

class GFG{

// Function that finds minimum 
// character required to be deleted 
static int minDel(String s1, String s2)
{
    int i = 0;

    // Iterate in the strings 
    while (i < Math.Min(s1.Length, 
                        s2.Length)) 
    {

        // Check if the characters 
        // are not equal 
        if (s1[i] != s2[i])
        {
            break;
        }
        i++;
    }

    // Return the result 
    int ans = ((s1.Length - i) + 
               (s2.Length - i));
    return ans;
}

// Driver code 
public static void Main(String[] args)
{
    String s1 = "geeks";
    String s2 = "geeksfor";

    Console.WriteLine(minDel(s1, s2));
}
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
3

```

***时间复杂度:** O(min(len(s1)，len(S2))
**辅助空间:** O(1)*
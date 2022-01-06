# 字符串中重复项之间的最小距离

> 原文:[https://www . geesforgeks . org/字符串中重复项之间的最小距离/](https://www.geeksforgeeks.org/minimum-distance-between-duplicates-in-a-string/)

给定一根[弦](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 及其长度 **N** (前提是 **N > 0** )。任务是找到相同重复字符之间的最小距离，如果[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 中没有重复字符，则返回 **-1** 。

***例:***

> **输入:** S = "geeksforgeeks "，N = 13
> **输出:** 0
> **解释** :
> 最小距离字符串 S = "geeksforgeeks "中的重复字符为' e '。
> 它们的索引之间的最小差异为 0(即字符“e”出现在索引 1 和 2 中)。
> 
> **输入:**S =“abdfhbih”，N = 8
> **输出:** 2
> **解释** :
> 最小距离字符串 S =“abdfhbih”中的重复字符为‘h’。
> 它们的指数之间的最小差异是 2(即字符‘h’出现在指数 4 和 7 处)。

**天真方法:**这个问题可以通过使用两个嵌套循环来解决，一个循环在每个索引处考虑一个元素**[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 中的‘I’**，下一个循环将在 **S.** 中找到与**I<sup>th</sup>T11】相同的匹配字符**

首先，将重复字符之间的每个差异存储在变量中，并检查当前距离是否小于存储在同一变量中的前一个值。最后返回存储**最小值**的变量。有一个**角格**，即当有**无重复字符时**返回 **-1** 。按照以下步骤解决此问题:

*   初始化一个变量 **minDis** 为 **N** 来存储重复字符的最小距离。
*   [使用变量 **i:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N-1】**中迭代:
        *   如果 **S[i]** 等于 **S[j]** 并且它们之间的距离小于 **minDis，**更新 **minDis** ，然后**断开**循环
*   如果 **minDis** 值未更新，即表示没有重复字符，则返回 **-1，**否则返回**minDis–1。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// This function is used to find
// minimum distance between same
// repeating characters
int shortestDistance(string S, int N)
{

    // Store minimum distance between same
    // repeating characters
    int minDis = S.length();

    // For loop to consider each element
    // of string
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // Comparison of string characters and
            // updating the minDis value
            if (S[i] == S[j] and (j - i) < minDis)
            {
                minDis = j - i;

                // As this value would be least
                // therefore break
                break;
            }
        }
    }

    // If minDis value is not updated that means
    // no repeating characters
    if (minDis == S.length())
        return -1;
    else

        // Minimum distance is minDis - 1
        return minDis - 1;
}

// Driver Code
int main()
{

    // Given Input
    string S = "geeksforgeeks";
    int N = 13;

    // Function Call
    cout << (shortestDistance(S, N));
}

// This code is contributed by lokeshpotta20
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// This function is used to find
// minimum distance between same
// repeating characters
static int shortestDistance(String S, int N)
{

    // Store minimum distance between same
    // repeating characters
    int minDis = S.length();

    // For loop to consider each element
    // of string
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // Comparison of string characters and
            // updating the minDis value
            if (S.charAt(i) == S.charAt(j) &&
               (j - i) < minDis)
            {
                minDis = j - i;

                // As this value would be least
                // therefore break
                break;
            }
        }
    }

    // If minDis value is not updated that means
    // no repeating characters
    if (minDis == S.length())
        return -1;

    // Minimum distance is minDis - 1
    else
        return minDis - 1;
}

// Driver code
public static void main(String[] args)
{

    // Given input
    String S = "geeksforgeeks";
    int N = 13;

    // Function call
    System.out.println(shortestDistance(S, N));
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# This function is used to find
# minimum distance between same
# repeating characters

def shortestDistance(S, N):

    # Store minimum distance between same
    # repeating characters
    minDis = len(S)

    # For loop to consider each element of string
    for i in range(N):
        for j in range(i+1, N):
            # Comparison of string characters and
            # updating the minDis value
            if(S[i] == S[j] and (j-i) < minDis):
                minDis = j-i
                # As this value would be least therefore break
                break
    # If minDis value is not updated that means
    # no repeating characters
    if(minDis == len(S)):
        return -1
    else:
        # Minimum distance is minDis - 1
        return minDis - 1

# Driver Code

# Given Input
S = "geeksforgeeks"
N = 13

# Function Call
print(shortestDistance(S, N))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// This function is used to find
// minimum distance between same
// repeating characters
static int shortestDistance(string S, int N)
{

    // Store minimum distance between same
    // repeating characters
    int minDis = S.Length;

    // For loop to consider each element
    // of string
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {

            // Comparison of string characters and
            // updating the minDis value
             if (S[i] == S[j] && (j - i) < minDis)
            {
                minDis = j - i;

                // As this value would be least
                // therefore break
                break;
            }
        }
    }

    // If minDis value is not updated that means
    // no repeating characters
    if (minDis == S.Length)
        return -1;

    // Minimum distance is minDis - 1
    else
        return minDis - 1;
}

// Driver code
public static void Main(String[] args)
{

    // Given input
    string S = "geeksforgeeks";
    int N = 13;

    // Function call
    Console.Write(shortestDistance(S, N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// This function is used to find
// minimum distance between same
// repeating characters
function shortestDistance( S, N)
{

    // Store minimum distance between same
    // repeating characters
    var minDis = S.length;

    // For loop to consider each element
    // of string
    for(var i = 0; i < N; i++)
    {
        for(var j = i + 1; j < N; j++)
        {

            // Comparison of string characters and
            // updating the minDis value
            if (S.charAt(i) == S.charAt(j) &&
               (j - i) < minDis)
            {
                minDis = j - i;

                // As this value would be least
                // therefore break
                break;
            }
        }
    }

    // If minDis value is not updated that means
    // no repeating characters
    if (minDis == S.length)
        return -1;

    // Minimum distance is minDis - 1
    else
        return minDis - 1;
}

// Driver code
// Given input
    var S = "geeksforgeeks";
    var N = 13;

    // Function call
    document.write(shortestDistance(S, N));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
0
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**这个问题可以通过使用[**字典**](https://www.geeksforgeeks.org/python-dictionary/) **或** [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) **来解决。**首先，将**最后一个索引**存储到字典的字符中，这样就可以用字典中相同字符的最后一个值减去它，并进一步将距离存储到列表中。最后返回列表的**最小值**。按照以下步骤解决此问题:

*   初始化一个[字典](https://www.geeksforgeeks.org/python-dictionary/) **dic** 来保存字符的最后一次出现，初始化一个列表 **dis** 来存储距离。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代:
    *   如果字典中有字符:
        *   然后，提取其最后值 **dic[S[i]]** 并用当前位置 **i.** 更新
        *   将差异存储在变量**var = I–DIC[S[I]]**中，并将其附加到列表 **dis 中。**
    *   如果字符不存在，用当前位置初始化。
*   如果 **dis** 的长度为 **0** 表示没有重复字符，则返回 **-1，**否则返回**min(dis)–1。**

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;
import java.util.*;

class GFG{

// This function is used to find
// minimum distance between same
// repeating characters
static int shortestDistance(String S, int N)
{

    // Define a hashmap and an arraylist
    HashMap<Character,
            Integer> dic = new HashMap<Character,
                                       Integer>();
    ArrayList<Integer> dis = new ArrayList<>();

    // Temporary variable
    int var;

    // Traverse through string
    for(int i = 0; i < N; i++)
    {

        // If character present in dictionary
        if (dic.get(S.charAt(i)) != null)
        {

            // Difference between current position
            // and last stored value
            var = i - dic.get(S.charAt(i));

            // Updating current position
            dic.put(S.charAt(i), i);

            // Storing difference in list
            dis.add(var);
        }

        // If character not in dictionary assign
        // it with initial of its position
        else
        {
            dic.put(S.charAt(i), i);
        }
    }

    // If no element inserted in list
    // i.e. no repeating characterss
    if (dis.size() == 0)
        return -1;

    // Return minimum distance
    else
        return Collections.min(dis) - 1;
}

// Driver code
public static void main(String[] args)
{

    // Given input
    String S = "geeksforgeeks";
    int N = 13;

    // Function call
    System.out.println(shortestDistance(S, N));
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# This function is used to find the
# required the minimum distances of
# repeating characters
def shortestDistance(S, N):

    # Define dictionary and list
    dic = {}
    dis = []

    # Traverse through string
    for i in range(N):
        # If character present in dictionary
        if S[i] in dic:
            # Difference between current position
            # and last stored value
            var = i- dic[S[i]]
            # Updating current position
            dic[S[i]] = i
            # Storing difference in list
            dis.append(var)
        # If character not in dictionary assign
        # it with initial of its position   
        else:
            dic[S[i]] = i
    # If no element inserted in list
    # i.e. no repeating characters       
    if(len(dis) == 0):
        return -1
    # Return minimum distance 
    else:
        return min(dis)-1

# Driver code

# Given Input
S = "geeksforgeeks"
N = 13

# Function Call
print(shortestDistance(S, N))
```

## C#

```
// C# implementation of above approach

using System;
using System.Collections.Generic;

public class GFG {

    // This function is used to find
    // minimum distance between same
    // repeating characters
    static int shortestDistance(String S, int N) {

        // Define a hashmap and an arraylist
        Dictionary<char, int> dic = new Dictionary<char, int>();
        List<int> dis = new List<int>();

        // Temporary variable
        int var;

        // Traverse through string
        for (int i = 0; i < N; i++) {

            // If character present in dictionary
            if (dic.ContainsKey(S[i])) {

                // Difference between current position
                // and last stored value
                var = i - dic[S[i]];

                // Updating current position
                dic[S[i]]= i;

                // Storing difference in list
                dis.Add(var);
            }

            // If character not in dictionary assign
            // it with initial of its position
            else {
                dic.Add(S[i], i);
            }
        }
dis.Sort();
        // If no element inserted in list
        // i.e. no repeating characterss
        if (dis.Count == 0)
            return -1;

        // Return minimum distance
        else
            return  dis[0]- 1;
    }

    // Driver code
    public static void Main(String[] args) {

        // Given input
        String S = "geeksforgeeks";
        int N = 13;

        // Function call
        Console.WriteLine(shortestDistance(S, N));
    }
}

// This code contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript implementation of above approach
// This function is used to find
    // minimum distance between same
    // repeating characters
    function shortestDistance( S , N) {

        // Define a hashmap and an arraylist
        var dic = new Map();
        var dis = new Array();

        // Temporary variable
        var var1;

        // Traverse through string
        for (i = 0; i < N; i++) {

            // If character present in dictionary
            if (dic[S[i]] != null) {

                // Difference between current position
                // and last stored value
                var1 = i - dic[S[i]];

                // Updating current position
                dic[S[i]] = i;

                // Storing difference in list
                dis.push(var1);
            }

            // If character not in dictionary assign
            // it with initial of its position
            else {
                dic[S[i]]= i;
            }
        }

        // If no element inserted in list
        // i.e. no repeating characterss
        if (dis.length == 0)
            return -1;

        // Return minimum distance
        else
            return dis.reduce(function(previous,current){
                      return previous < current ? previous:current
                   }) - 1;
    }

    // Driver code

        // Given input
        var S = "geeksforgeeks";
        var N = 13;

        // Function call
        document.write(shortestDistance(S, N));

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**交替** **解决方案:**以下问题也可以使用改进的两点法来解决。这个想法基本上是为每个字符保持一个左指针，一旦那个特定的字符被重复，左指针指向该字符最近的索引。在这样做的同时，我们可以维护一个变量 ans，它将存储任意两个重复字符之间的最小距离。这可以通过访问向量数组来实现，该数组将存储当前字符在数组中的最近索引。

按照以下步骤解决此问题:

*   初始化一个访问向量来存储任何字符的最后一个索引(左指针)
*   迭代范围[0，N-1]:
    *   如果角色以前被访问过:
    *   找出字符之间的距离，并检查两者之间的距离是否最小。
    *   如果小于之前的最小值，请更新其值。
*   更新当前字符在访问数组中的最后一个索引。

如果没有获得最小距离(即当 ans 的值为 INT_MAX 时)，则意味着没有重复字符。在这种情况下返回-1；

下面是上述方法的实现:

## C++

```
// C++ Program to find the minimum distance between two
// repeating characters in a string using two pointers technique

#include <bits/stdc++.h>
using namespace std;

// This function is used to find
// minimum distance between any two
// repeating characters
// using two - pointers and hashing technique
int shortestDistance(string s, int n) {

    // hash array to store character's last index
    vector<int> visited(128, -1);
    int ans = INT_MAX;

    // Traverse through the string
    for(int right = 0; right < n; right++) {
        char c = s[right];
        int left = visited;

        // If the character is present in visited array
        // find if its forming minimum distance
        if(left != -1)
            ans = min(ans, right - left -1);

          // update current character's last index
        visited = right;
    }
    // Return minimum distance found, else -1
    return ans == INT_MAX ? -1 : ans;
}

int main(){
    // Given Input
    string s = "geeksforgeeks";
    int n = 13;

    // Function Call
    cout << (shortestDistance(s, n));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum distance between two
// repeating characters in a String using two pointers
// technique
import java.util.*;

class GFG {

    // This function is used to find
    // minimum distance between any two
    // repeating characters
    // using two - pointers and hashing technique
    static int shortestDistance(String s, int n)
    {

        // hash array to store character's last index
        int[] visited = new int[128];
        Arrays.fill(visited, -1);
        int ans = Integer.MAX_VALUE;

        // Traverse through the String
        for (int right = 0; right < n; right++) {
            char c = s.charAt(right);
            int left = visited;

            // If the character is present in visited array
            // find if its forming minimum distance
            if (left != -1)
                ans = Math.min(ans, right - left - 1);

            // update current character's last index
            visited = right;
        }

        // Return minimum distance found, else -1
        return ans == Integer.MAX_VALUE ? -1 : ans;
    }

  // Driver code
    public static void main(String[] args)
    {

        // Given Input
        String s = "geeksforgeeks";
        int n = 13;

        // Function Call
        System.out.print(shortestDistance(s, n));
    }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python Program to find the minimum distance between two
# repeating characters in a String using two pointers
# technique
import sys

# This function is used to find
# minimum distance between any two
# repeating characters
# using two - pointers and hashing technique
def shortestDistance(s, n):

    # hash array to store character's last index
    visited = [-1 for i in range(128)];

    ans = sys.maxsize;

    # Traverse through the String
    for right in range(n):
        c = (s[right]);
        left = visited[ord(c)];

        # If the character is present in visited array
        # find if its forming minimum distance
        if (left != -1):
            ans = min(ans, right - left - 1);

        # update current character's last index
        visited[ord(c)] = right;

    # Return minimum distance found, else -1
    if(ans == sys.maxsize):
        return -1;
    else:
        return ans;

# Driver code
if __name__ == '__main__':

    # Given Input
    s = "geeksforgeeks";
    n = 13;

    # Function Call
    print(shortestDistance(s, n));

# This code is contributed by umadevi9616
```

## C#

```
// C# Program to find the minimum distance between two
// repeating characters in a String using two pointers
// technique
using System;

public class GFG {

    // This function is used to find
    // minimum distance between any two
    // repeating characters
    // using two - pointers and hashing technique
    static int shortestDistance(string s, int n)
    {

        // hash array to store character's last index
        int[] visited = new int[128];
        for(int i = 0; i < 128; i++)
            visited[i] = -1;
        int ans = int.MaxValue;

        // Traverse through the String
        for (int right = 0; right < n; right++) {
            char c = s[right];
            int left = visited;

            // If the character is present in visited array
            // find if its forming minimum distance
            if (left != -1)
                ans = Math.Min(ans, right - left - 1);

            // update current character's last index
            visited = right;
        }

        // Return minimum distance found, else -1
        return ans == int.MaxValue ? -1 : ans;
    }

  // Driver code
    public static void Main(String[] args)
    {

        // Given Input
        string s = "geeksforgeeks";
        int n = 13;

        // Function Call
        Console.Write(shortestDistance(s, n));
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript Program to find the minimum distance between two
// repeating characters in a String using two pointers
// technique

    // This function is used to find
    // minimum distance between any two
    // repeating characters
    // using two - pointers and hashing technique
    function shortestDistance(s , n) {

        // hash array to store character's last index
        var visited = Array(128).fill(-1);

        var ans = Number.MAX_VALUE;

        // Traverse through the String
        for (var right = 0; right < n; right++) {
            var left = visited[s.charCodeAt(right)];

            // If the character is present in visited array
            // find if its forming minimum distance
            if (left != -1)
                ans = Math.min(ans, right - left - 1);

            // update current character's last index
            visited[s.charCodeAt(right)] = right;
        }

        // Return minimum distance found, else -1
        return ans == Number.MAX_VALUE ? -1 : ans;
    }

    // Driver code

        // Given Input
        var s = "geeksforgeeks";
        var n = 13;

        // Function Call
        document.write(shortestDistance(s, n));

// This code is contributed by umadevi9616
</script>
```

**Output**

```
0
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
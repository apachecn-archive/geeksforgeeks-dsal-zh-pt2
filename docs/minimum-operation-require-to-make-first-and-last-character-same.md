# 使第一个和最后一个字符相同所需的最小操作

> 原文:[https://www . geesforgeks . org/最小操作-要求制作首末字符-相同/](https://www.geeksforgeeks.org/minimum-operation-require-to-make-first-and-last-character-same/)

给定一根绳子 **S** 。您可以进行两种类型的操作:

*   从字符串前面删除一个字符。
*   从字符串末尾删除一个字符。

任务是找到使 S 的第一个和最后一个字符相同所需的最少操作。如果不可能，打印“-1”。

**示例:**

```
Input : S = "bacdefghipalop"
Output : 4
Remove 'b' from the front and remove 'p', 'o',
'l' from the end of the string S.

Input : S = "pqr"
Output : -1
```

**方法:**
**递归:**调用一个递归函数传递四个参数字符串，开始索引、结束索引和现在仍然存在的淘汰数量的计数。

下面是上述方法的实现:

## C++

```
// CPP program to minimum operation require
// to make first and last character same
#include <bits/stdc++.h>
using namespace std;

const int MAX = INT_MAX;

// Recursive function call
int minOperation(string &s,int i,int j,int count)
{
    if((i>=s.size() && j<0) || (i == j))
        return MAX;
    if(s[i] == s[j])
        return count;

    // Decrement ending index only
    if(i >=s.size())
        return minOperation(s,i,j-1,count+1);

    // Increment starting index only
    else if(j<0)
        return minOperation(s,i+1,j,count+1);

    // Increment starting index and decrement index
    else
        return min(minOperation(s,i,j-1,count+1),minOperation(s,i+1,j,count+1));

}

// Driver code
int main() {

    string s = "bacdefghipalop";

    // Function call
    int ans = minOperation(s,0,s.size()-1,0);

    if(ans == MAX)
        cout<<-1;
    else
        cout<<ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimum operation require
// to make first and last character same
import java.util.*;

class GFG
{

    static final int MAX = Integer.MAX_VALUE;

    // Recursive function call
    static int minOperation(String s, int i, int j, int count)
    {
        if ((i >= s.length() && j < 0) || (i == j))
            return MAX;

        if (s.charAt(i) == s.charAt(j))
            return count;

        // Decrement ending index only
        if (i >= s.length())
            return minOperation(s, i, j - 1, count + 1);

        // Increment starting index only
        else if (j < 0)
            return minOperation(s, i + 1, j, count + 1);

        // Increment starting index and decrement index
        else
            return Math.min(minOperation(s, i, j - 1, count + 1),
                            minOperation(s, i + 1, j, count + 1));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "bacdefghipalop";

        // Function call
        int ans = minOperation(s, 0, s.length() - 1, 0);

        if (ans == MAX)
            System.out.println(-1);
        else
            System.out.println(ans);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to minimum operation require
# to make first and last character same
import sys

MAX = sys.maxsize

# Recursive function call
def minOperation(s, i, j, count):

    if ((i >= len(s) and j < 0) or (i == j)):
        return MAX
    if (s[i] == s[j]):
        return count

    # Decrement ending index only
    if (i >=len(s)):
        return minOperation(s, i, j - 1,
                              count + 1)

    # Increment starting index only
    elif (j < 0):
        return minOperation(s, i + 1, j,
                           count + 1)

    # Increment starting index
    # and decrement index
    else:
        return min(minOperation(s, i, j - 1,
                                  count + 1),
                   minOperation(s, i + 1, j,
                               count + 1))

# Driver code
if __name__ == '__main__':

    s = "bacdefghipalop"

    # Function call
    ans = minOperation(s, 0, len(s) - 1, 0)

    if (ans == MAX):
        print(-1)
    else:
        print(ans)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to minimum operation require
// to make first and last character same
using System;
class GFG
{
  static int MAX = Int32.MaxValue;

  // Recursive function call
  static int minOperation(string s, int i, int j, int count)
  {
    if ((i >= s.Length && j < 0) || (i == j))
      return MAX;

    if (s[i] == s[j])
      return count;

    // Decrement ending index only
    if (i >= s.Length)
      return minOperation(s, i, j - 1, count + 1);

    // Increment starting index only
    else if (j < 0)
      return minOperation(s, i + 1, j, count + 1);

    // Increment starting index and decrement index
    else
      return Math.Min(minOperation(s, i, j - 1, count + 1),
                      minOperation(s, i + 1, j, count + 1));
  }

  // Driver Code
  public static void Main()
  {
    string s = "bacdefghipalop";

    // Function call
    int ans = minOperation(s, 0, s.Length - 1, 0);

    if (ans == MAX)
      Console.Write(-1);
    else
      Console.Write(ans);
  }
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program to minimum operation require
// to make first and last character same

var MAX = 1000000000;

// Recursive function call
function minOperation( s,i,j,count)
{
    if((i>=s.length && j<0) || (i == j))
        return MAX;
    if(s[i] == s[j])
        return count;

    // Decrement ending index only
    if(i >=s.length)
        return minOperation(s,i,j-1,count+1);

    // Increment starting index only
    else if(j<0)
        return minOperation(s,i+1,j,count+1);

    // Increment starting index and decrement index
    else
        return Math.min(minOperation(s,i,j-1,count+1),
        minOperation(s,i+1,j,count+1));

}

// Driver code
var s = "bacdefghipalop";

// Function call
var ans = minOperation(s,0,s.length-1,0);

if(ans == MAX)
    document.write( -1);
else
    document.write( ans);

</script>
```

**输出:**

```
4
```

**动态编程:**
想法是一旦我们在每次递归调用期间找到 Min，就防止对 count 进行进一步的递归调用> = Min。它节省了大量的时间，并且在时间复杂度方面几乎与制表法相当。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find minimum operation require
// to make first and last character same
#include <bits/stdc++.h>
using namespace std;
const int MAX = INT_MAX;

// To store the visited strings
map <string,int> m;

int Min = INT_MAX;

// Function to find minimum operation require
// to make first and last character same
int minOperation(string &s,int i,int j,int count)
{
    // Base conditions
    if((i>=s.size() && j<0) || (i == j))
        return MAX;

    // If answer found
    if(s[i] == s[j] || (count >= Min))
        return count;

    string str = to_string(i) + "|"+to_string(j);

    // If string is already visited
    if(m.find(str) == m.end())
    {
        // Decrement ending index only
        if(i >=s.size())
        m[str]= minOperation(s,i,j-1,count+1);

        // Increment starting index only
        else if(j<0)
        m[str]= minOperation(s,i+1,j,count+1);

        // Increment starting index and decrement index
        else
        m[str]= min(minOperation(s,i,j-1,count+1),minOperation(s,i+1,j,count+1));
    }

    // Store the minimum value
    if(m[str] < Min)
            Min = m[str];
    return m[str];

}

// Driver code
int main()
{
    string s = "bacdefghipalop";

    // Function call
    int ans = minOperation(s,0,s.size()-1,0);

    if(ans == MAX)
        cout<<-1;
    else
        cout<<ans;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum operation require
// to make first and last character same
import java.io.*;
import java.util.*;
class GFG
{
    static int MAX = Integer.MAX_VALUE;
    static HashMap<String, Integer> m = new HashMap<>();
    static int Min = Integer.MAX_VALUE;

    // Function to find minimum operation require
    // to make first and last character same
    static int minOperation(String s,int i,int j,int count)
    {

        // Base conditions
        if((i >= s.length() && j < 0)|| (i == j))
        {
            return MAX;
        }

        // If answer found
        if(s.charAt(i) == s.charAt(j) || (count >= Min))
        {
            return count;
        }
        String str = String.valueOf(i) + "|" + String.valueOf(j);

      // If string is already visited
        if(!m.containsKey(str))
        {

          // Decrement ending index only
            if(i >= s.length())
            {
                m.put(str,minOperation(s, i, j - 1, count + 1));
            }

            // Increment starting index only
            else if(j < 0)
            {
                m.put(str,minOperation(s, i + 1, j, count + 1));
            }

            // Increment starting index and decrement index
            else
            {
                m.put(str,Math.min(minOperation(s, i, j - 1, count + 1), minOperation(s, i + 1, j, count + 1)));
            }
        }

        // Store the minimum value
        if(m.get(str) < Min)
        {
            Min = m.get(str);

        }
        return m.get(str);
    }

    // Driver code
    public static void main (String[] args)
    {
        String s = "bacdefghipalop";

        // Function call
        int ans=minOperation(s, 0, s.length() - 1, 0);
        if(ans == MAX)
        {
            System.out.println(-1);
        }
        else
        {
            System.out.println(ans);
        }

    }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python program to find minimum operation require
# to make first and last character same
import sys
MAX = sys.maxsize

# To store the visited strings
m = {}
Min = sys.maxsize

# Function to find minimum operation require
# to make first and last character same
def minOperation(s, i, j, count):
    global Min, MAX

    # Base conditions
    if((i >= len(s) and j < 0) or (i == j)):
        return MAX

    # If answer found
    if(s[i] == s[j] or count >= Min):
        return count
    Str = str(i) + "|" + str(j)

    # If string is already visited
    if Str not in m:

        # Decrement ending index only
        if(i >= len(s)):
            m[Str] = minOperation(s, i, j - 1, count + 1)

        # Increment starting index only
        elif(j < 0):
            m[Str] = minOperation(s, i + 1, j, count + 1)

        # Increment starting index and decrement index
        else:
            m[Str] = min(minOperation(s, i, j - 1, count + 1), minOperation(s, i + 1, j, count + 1))

    # Store the minimum value
    if(m[Str] < Min):
        Min = m[Str]
    return m[Str]

# Driver code
s = "bacdefghipalop"

# Function call
ans = minOperation(s, 0, len(s) - 1, 0)
if(ans == MAX):
    print(-1)
else:
    print(ans)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find minimum operation require
// to make first and last character same
using System;
using System.Collections.Generic;  
class GFG
{

    static int MAX = Int32.MaxValue;
    static Dictionary<string, int> m = new Dictionary<string, int>();
    static int Min = Int32.MaxValue;

    // Function to find minimum operation require
    // to make first and last character same
    static int minOperation(string s,int i,int j,int count)
    {

        // Base conditions
        if((i >= s.Length && j < 0)|| (i == j))
        {
            return MAX;
        }

        // If answer found
        if(s[i] == s[j] || (count >= Min))
        {
            return count;
        }
        string str = i.ToString() + "|" + j.ToString();

        // If string is already visited
        if(!m.ContainsKey(str))
        {

          // Decrement ending index only
            if(i >= s.Length)
            {
                m[str] = minOperation(s, i, j - 1, count + 1);
            }

            // Increment starting index only
            else if(j < 0)
            {
                m[str] = minOperation(s, i + 1, j, count + 1);
            }

            // Increment starting index and decrement index
            else
            {
                m[str] = Math.Min(minOperation(s, i, j - 1, count + 1), minOperation(s, i + 1, j, count + 1));
            }
        }

        // Store the minimum value
        if(m[str] < Min)
        {
            Min = m[str];

        }
        return m[str];
    }

  // Driver code
  static void Main()
  {
    string s = "bacdefghipalop";

    // Function call
    int ans=minOperation(s, 0, s.Length - 1, 0);
    if(ans == MAX)
    {
        Console.WriteLine(-1);
    }
    else
    {
        Console.WriteLine(ans);
    }
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// Javascript program to find minimum operation require
// to make first and last character same
    let MAX = Number.MAX_VALUE;
    let m = new Map();
    let Min = Number.MAX_VALUE;

    // Function to find minimum operation require
    // to make first and last character same
    function minOperation(s, i, j, count)
    {

        // Base conditions
        if((i >= s.length && j < 0)|| (i == j))
        {
            return MAX;
        }

        // If answer found
        if(s[i] == s[j] || (count >= Min))
        {
            return count;
        }
        let str = (i).toString() + "|" + (j).toString();

      // If string is already visited
        if(!m.has(str))
        {

          // Decrement ending index only
            if(i >= s.length)
            {
                m.set(str,minOperation(s, i, j - 1, count + 1));
            }

            // Increment starting index only
            else if(j < 0)
            {
                m.set(str,minOperation(s, i + 1, j, count + 1));
            }

            // Increment starting index and decrement index
            else
            {
                m.set(str,Math.min(minOperation(s, i, j - 1, count + 1), minOperation(s, i + 1, j, count + 1)));
            }
        }

        // Store the minimum value
        if(m.get(str) < Min)
        {
            Min = m.get(str);

        }
        return m.get(str);
    }

    // Driver code   
    let s = "bacdefghipalop";

    // Function call
        let ans=minOperation(s, 0, s.length - 1, 0);
        if(ans == MAX)
        {
            document.write(-1);
        }
        else
        {
            document.write(ans);
        }

// This code is contributed by unknown2108
</script>
```

**输出:**

```
4
```

**带制表功能的动态编程:**
其思想是找出字符串中每个字符的第一次和最后一次出现。所需的操作总数将只是“删除第一个事件所需的操作数”加上“删除最后一个事件所需的操作数”。因此，对字符串中的每个字符执行此操作，答案将是对每个字符执行的此类操作最少。
例如，S = " zabcdefghaabbbb "，计算在前面和结尾都有字符' a '所需的操作，意思是说字符串" a…"。一个”。对于最少的操作数，我们将形成字符串“abcdefghaa”，即我们将从前面删除一个字符“z”，从后面删除 4 个字符“bbbb”。因此总共需要 5 次操作。
因此，对每个字符应用上述算法，因此我们可以找到这些操作的最小值。

下面是这种方法的实现:

## C++

```
// C++ program to find minimum operation
// require to make first and last character same
#include <bits/stdc++.h>
using namespace std;
#define MAX 256

// Return the minimum operation require
// to make string first and last character same.
int minimumOperation(string s)
{
    int n = s.length();

    // Store indexes of first occurrences of characters.
    vector<int> first_occ(MAX, -1);

    // Initialize result
    int res = INT_MAX;

    // Traverse through all characters
    for (int i=0; i<n; i++)
    {
        // Find first occurrence
        char x = s[i];
        if (first_occ[x] == -1)
        first_occ[x] = i;

        // Update result for subsequent occurrences
        else
        {
        int last_occ = (n-i-1);
        res = min(res, first_occ[x] + last_occ);
        }
    }
    return res;
}

// Driven Program
int main()
{
    string s = "bacdefghipalop";
    cout << minimumOperation(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// operation require to make
// first and last character same

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static final int MAX=256;

// Return the minimum operation requires to
// make string first and last character same.
static int minimumOperation(String s)
{
    int n = s.length();

    // Store indexes of first occurrences of characters.
    Vector<Integer> first_occ=new Vector<Integer>();

    //Initialize all the elements to -1
    for(int i=0;i<MAX;i++)
    first_occ.add(i,-1);

    // Initialize result
    int res = Integer.MAX_VALUE;

    // Traverse through all characters
    for (int i=0; i<n; i++)
    {
        // Find first occurrence
        int x = (int)s.charAt(i);
        if (first_occ.elementAt(x) == -1)
        first_occ.set(x,i);

        // Update result for subsequent occurrences
        else
        {
        int last_occ = (n-i-1);
        res = Math.min(res, first_occ.get(x) + last_occ);
        }
    }
    return res;
}

// Driven Program
public static void main(String args[])
{
    String s = "bacdefghipalop";
    System.out.println(minimumOperation(s));
}
}
```

## 蟒蛇 3

```
# Python3 program to find minimum operation
# require to make first and last character same
MAX = 256

# Return the minimum operation require to
# make string first and last character same.
def minimumOperation(s):

    n = len(s)

    # Store indexes of first
    # occurrences of characters.
    first_occ = [-1] * MAX

    # Initialize result
    res = float('inf')

    # Traverse through all characters
    for i in range(0, n):

        # Find first occurrence
        x = s[i]
        if first_occ[ord(x)] == -1:
            first_occ[ord(x)] = i

        # Update result for subsequent occurrences
        else:
            last_occ = n - i - 1
            res = min(res, first_occ[ord(x)] + last_occ)

    return res

# Driver Code
if __name__ == "__main__":

    s = "bacdefghipalop"
    print(minimumOperation(s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find minimum
// operation require to make
// first and last character same
using System;
using System.Collections.Generic;

class GFG
{

static int MAX = 256;

// Return the minimum operation requires to
// make string first and last character same.
static int minimumOperation(String s)
{
    int n = s.Length;

    // Store indexes of first occurrences of characters.
    List<int> first_occ = new List<int>();

    //Initialize all the elements to -1
    for(int i = 0; i < MAX; i++)
    first_occ.Insert(i,-1);

    // Initialize result
    int res = int.MaxValue;

    // Traverse through all characters
    for (int i = 0; i < n; i++)
    {
        // Find first occurrence
        int x = (int)s[i];
        if (first_occ[x] == -1)
        first_occ.Insert(x,i);

        // Update result for subsequent occurrences
        else
        {
            int last_occ = (n - i - 1);
            res = Math.Min(res, first_occ[x] + last_occ);
        }
    }
    return res;
}

// Driver code
public static void Main(String []args)
{
    String s = "bacdefghipalop";
    Console.WriteLine(minimumOperation(s));
}
}

// This code contributed by Rajput-Ji
```

**Output:** 

```
4
```

时间复杂度:O(n)
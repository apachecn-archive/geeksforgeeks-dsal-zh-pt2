# 最小化使字符串的所有剩余字符唯一所需的删除成本

> 原文:[https://www . geeksforgeeks . org/最小化移除成本-使字符串中所有剩余字符唯一化所需的成本/](https://www.geeksforgeeks.org/minimize-cost-of-removals-required-to-make-all-remaining-characters-of-the-string-unique/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**和一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **成本[]** ，其中**成本【I】**表示从字符串**字符串**中移除 **i <sup>th</sup>** 字符的成本，任务是找到最小的移除成本，以使字符串的每个字符[唯一](https://www.geeksforgeeks.org/determine-string-unique-characters/)。

**示例:**

> **输入:** str = "AAABBB "，成本= {1，2，3，4，5，6}
> **输出:** 12
> **解释:**删除索引 0，1，3，4 处的字符将 str 修改为“AB”。因此，清除的总成本= 1 + 2 + 4 + 5 = 12
> 
> **输入:** str = "geeksforgeeks "，成本= {1，2，3，4，5，5，4，3，2，1，1，2，3}
> **输出:** 10
> **解释:**移除索引 0，1，9，10，11，12 处的字符将 str 修改为“eksforg”。因此，清除的总成本= 1 + 2 + 1 + 1 + 2 + 3 = 10

**天真方法:**解决问题最简单的方法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，对于每个字符，遍历剩余的字符并找到它的出现。存储移除事件的最大成本。将删除该字符所有其他匹配项的成本加到总和中。最后，对字符串的所有字符完成此操作后，打印得到的最终总和。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost of
// removing characters to make the String unique
int delCost(string s, int cost[], int l1, int l2)
{

    // stores the visited character
    bool visited[l1];
    memset(visited, 0, sizeof(visited));

    // stores the answer
    int ans = 0;

    // traverse the String
    for (int i = 0; i < l1; i++)
    {

        // if already visited
        if (visited[i])
        {
            continue;
        }

        // Stores the maximum cost of
        // removing a particular character
        int maxDel = 0;

        // Store the total deletion cost of
        // a particular character
        int totalCost = 0;

        // Mark the current character visited
        visited[i] = 1;

        // Traverse the indices of the String [i, N-1]
        for (int j = i; j < l1; j++)
        {

            // If any duplicate is found
            if (s[i] == s[j])
            {

                // Update the maximum cost
                // and total cost
                maxDel = max(maxDel, cost[j]);
                totalCost += cost[j];

                // Mark the current character visited
                visited[j] = 1;
            }
        }

        // Keep the character with
        // maximum cost and delete the rest
        ans += totalCost - maxDel;
    }

    // return the minimum cost
    return ans;
}

// Driver code
int main()
{

    // input String
    string s = "AAABBB";
    int l1 = s.size();

    // input array
    int cost[] = { 1, 2, 3, 4, 5, 6 };
    int l2 = sizeof(cost) / sizeof(cost[0]);

    // function call
    cout << delCost(s, cost, l1, l2);
    return 0;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG
{

  // Function to find the minimum cost of
  // removing characters to make the string unique
  public static int delCost(String s, int[] cost)
  {

    // stores the visited character
    boolean visited[] = new boolean[s.length()];

    // stores the answer
    int ans = 0;

    // traverse the string
    for (int i = 0; i < s.length(); i++)
    {

      // if already visited
      if (visited[i])
      {
        continue;
      }

      // Stores the maximum cost of
      // removing a particular character
      int maxDel = 0;

      // Store the total deletion cost of
      // a particular character
      int totalCost = 0;

      // Mark the current character visited
      visited[i] = true;

      // Traverse the indices of the string [i, N-1]
      for (int j = i; j < s.length(); j++)
      {

        // If any duplicate is found
        if (s.charAt(i) == s.charAt(j))
        {

          // Update the maximum cost
          // and total cost
          maxDel = Math.max(maxDel, cost[j]);
          totalCost += cost[j];

          // Mark the current character visited
          visited[j] = true;
        }
      }

      // Keep the character with
      // maximum cost and delete the rest
      ans += totalCost - maxDel;
    }

    // return the minimum cost
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {

    // input string
    String s = "AAABBB";

    // input array
    int[] cost = { 1, 2, 3, 4, 5, 6 };

    // function call
    System.out.println(delCost(s, cost));
  }
}

// This code is contributed by aditya7409
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum cost of
# removing characters to make the string unique
def delCost(s, cost):

    # Stores the visited characters
    visited = [False]*len(s)

    # Stores the answer
    ans = 0

    # Traverse the string
    for i in range(len(s)):

          # If already visited
        if visited[i]: 
            continue

        # Stores the maximum cost of
        # removing a particular character
        maxDel = 0

        # Store the total deletion cost of
        # a particular character
        totCost = 0

        # Mark the current character visited
        visited[i] = True

        # Traverse the indices of the string [i, N-1]
        for j in range(i, len(s)):

            # If any duplicate is found
            if s[i] == s[j]: 

                # Update the maximum cost
                # and total cost
                maxDel = max(maxDel, cost[j])
                totCost += cost[j]

                # Mark the current character visited
                visited[j] = True

        # Keep the character with
        # maximum cost and delete the rest
        ans += totCost - maxDel

       # Return the minimum cost
    return ans

# Driver code
# Given string
string = "AAABBB"

# Given cost array
cost = [1, 2, 3, 4, 5, 6]

# Function Call
print(delCost(string, cost))
```

## C#

```
// C# program to implement
// the above approach 
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum cost of
// removing characters to make the string unique
public static int delCost(string s, int[] cost)
{

    // Stores the visited character
    bool[] visited = new bool[s.Length];

    // Stores the answer
    int ans = 0;

    // Traverse the string
    for(int i = 0; i < s.Length; i++)
    {

        // If already visited
        if (visited[i] != false)
        {
            continue;
        }

        // Stores the maximum cost of
        // removing a particular character
        int maxDel = 0;

        // Store the total deletion cost of
        // a particular character
        int totalCost = 0;

        // Mark the current character visited
        visited[i] = true;

        // Traverse the indices of the
        // string [i, N-1]
        for(int j = i; j < s.Length; j++)
        {

            // If any duplicate is found
            if (s[i] == s[j])
            {

                // Update the maximum cost
                // and total cost
                maxDel = Math.Max(maxDel, cost[j]);
                totalCost += cost[j];

                // Mark the current character visited
                visited[j] = true;
            }
        }

        // Keep the character with
        // maximum cost and delete
        // the rest
        ans += totalCost - maxDel;
    }

    // Return the minimum cost
    return ans;
}

// Driver Code   
public static void Main ()   
{   

    // Input string
    string s = "AAABBB";

    // Input array
    int[] cost = { 1, 2, 3, 4, 5, 6 };

    // Function call
    Console.Write(delCost(s, cost));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Function to find the minimum cost of
    // removing characters to make the string unique
    function delCost( s,  cost) {

        // stores the visited character
        var visited =Array(s.length).fill(false);

        // stores the answer
        var ans = 0;

        // traverse the string
        for (i = 0; i < s.length; i++) {

            // if already visited
            if (visited[i]) {
                continue;
            }

            // Stores the maximum cost of
            // removing a particular character
            var maxDel = 0;

            // Store the total deletion cost of
            // a particular character
            var totalCost = 0;

            // Mark the current character visited
            visited[i] = true;

            // Traverse the indices of the string [i, N-1]
            for (j = i; j < s.length; j++) {

                // If any duplicate is found
                if (s.charAt(i) == s.charAt(j)) {

                    // Update the maximum cost
                    // and total cost
                    maxDel = Math.max(maxDel, cost[j]);
                    totalCost += cost[j];

                    // Mark the current character visited
                    visited[j] = true;
                }
            }

            // Keep the character with
            // maximum cost and delete the rest
            ans += totalCost - maxDel;
        }

        // return the minimum cost
        return ans;
    }

    // Driver code

        // input string
        var s = "AAABBB";

        // input array
        var cost = [ 1, 2, 3, 4, 5, 6 ];

        // function call
        document.write(delCost(s, cost));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
12
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)

**高效途径:**优化上述途径，思路是使用 [Hashmap](https://www.geeksforgeeks.org/hashing-data-structure/) 。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，来存储所需的最小成本。
*   初始化两个[hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)，比如 **forMax** 和 **forTot** ，分别存储每个角色的最大和总移除成本。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 。
    *   更新**FORmax[s[I]]= max(FORmax(s[I])，cost[i])** 。
    *   更新 **forTot[s[i]] +=成本[i]** 。
*   [遍历散列表](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) **表单**
    *   对于每个字符，保留最大成本字符，并通过更新 **ans += forTot[i]-forMax[i]** 删除其其他重复字符。
*   打印〔t0〕年〔t1〕年。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost of
// removing characters to make the string unique
int delCost(string s, int cost[])
{

    // Store the minimum cost required
    int ans = 0;

    // Create a dictionary to store the
    // maximum cost of removal a character
    map<char, int> forMax;

    // Create a dictionary to store the total
    // deletion cost of a character
    map<char, int> forTot;

    // Traverse the string, S
    for (int i = 0; i < s.length(); i++) {

        // Keep track of maximum cost of each character
        if (!forMax[s[i]]) {
            forMax[s[i]] = cost[i];
        }
        else {

            // Update the maximum deletion cost
            forMax[s[i]] = max(cost[i], forMax[s[i]]);
        }

        // Keep track of the total cost of each character
        if (!forTot[s[i]]) {
            forTot[s[i]] = cost[i];
        }
        else {

            // Update the total deletion cost
            forTot[s[i]] = forTot[s[i]] + cost[i];
        }
    }

    // Traverse through all the unique characters
    for (auto i : forMax) {

        // Keep the maximum cost character and
        // delete the rest
        ans += forTot[i.first] - i.second;
    }

    // Return the answer
    return ans;
}

// Driver code
int main()
{

    // Given string
    string s = "AAABBB";

    // Given cost array
    int cost[] = { 1, 2, 3, 4, 5, 6 };

    // Function Call
    cout << (delCost(s, cost));
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to find the minimum cost of
  // removing characters to make the string unique
  static int delCost(String s, int[] cost)
  {

    // Store the minimum cost required
    int ans = 0;

    // Create a dictionary to store the
    // maximum cost of removal a character
    HashMap<Character, Integer> forMax = new HashMap<>();

    // Create a dictionary to store the total
    // deletion cost of a character
    HashMap<Character, Integer> forTot = new HashMap<>();

    // Traverse the string, S
    for(int i = 0; i < s.length(); i++)
    {

      // Keep track of maximum cost of each character
      if(!forMax.containsKey(s.charAt(i)))
      {
        forMax.put(s.charAt(i), cost[i]);
      }
      else
      {

        // Update the maximum deletion cost
        forMax.put(s.charAt(i), Math.max(cost[i], forMax.get(s.charAt(i))));
      }

      // Keep track of the total cost of each character
      if(!forTot.containsKey(s.charAt(i)))
      {
        forTot.put(s.charAt(i), cost[i]);
      }
      else
      {

        // Update the total deletion cost
        forTot.put(s.charAt(i), forTot.get(s.charAt(i)) + cost[i]);
      }
    }

    // Traverse through all the unique characters
    for (Map.Entry<Character, Integer> i : forMax.entrySet())
    {

      // Keep the maximum cost character and
      // delete the rest
      ans += forTot.get(i.getKey()) - i.getValue();
    }

    // Return the answer
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given string
    String s = "AAABBB";

    // Given cost array
    int[] cost = {1, 2, 3, 4, 5, 6};

    // Function Call
    System.out.println(delCost(s, cost));
  }
}

// This code is contributed by divyeshrabaddiya07.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum cost of
# removing characters to make the string unique
def delCost(s, cost):

    # Store the minimum cost required
    ans = 0

    # Create a dictionary to store the
    # maximum cost of removal a character
    forMax = {}

    # Create a dictionary to store the total
    # deletion cost of a character
    forTot = {}

    # Traverse the string, S
    for i in range(len(s)):

          # Keep track of maximum cost of each character
        if s[i] not in forMax: 
            forMax[s[i]] = cost[i]
        else:

              # Update the maximum deletion cost
            forMax[s[i]] = max(cost[i], forMax[s[i]])

        # Keep track of the total cost of each character
        if s[i] not in forTot: 
            forTot[s[i]] = cost[i]
        else:

              # Update the total deletion cost
            forTot[s[i]] += cost[i]

    # Traverse through all the unique characters
    for i in forMax:

          # Keep the maximum cost character and
        # delete the rest
        ans += forTot[i] - forMax[i]

    # Return the answer
    return ans

# Driver code
# Given string
string = "AAABBB"

# Given cost array
cost = [1, 2, 3, 4, 5, 6]

# Function Call
print(delCost(string, cost))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find the minimum cost of
  // removing characters to make the string unique
  static int delCost(string s, int[] cost)
  {

    // Store the minimum cost required
    int ans = 0;

    // Create a dictionary to store the
    // maximum cost of removal a character
    Dictionary<int, int> forMax = new Dictionary<int, int>();

    // Create a dictionary to store the total
    // deletion cost of a character
    Dictionary<int, int> forTot = new Dictionary<int, int>();

    // Traverse the string, S
    for(int i = 0; i < s.Length; i++)
    {

      // Keep track of maximum cost of each character
      if(!forMax.ContainsKey(s[i]))
      {
        forMax[s[i]] = cost[i];
      }
      else
      {

        // Update the maximum deletion cost
        forMax[s[i]] = Math.Max(cost[i], forMax[s[i]]);
      }

      // Keep track of the total cost of each character
      if(!forTot.ContainsKey(s[i]))
      {
        forTot[s[i]] = cost[i];
      }
      else
      {

        // Update the total deletion cost
        forTot[s[i]] += cost[i];
      }
    }

    // Traverse through all the unique characters
    foreach(KeyValuePair<int, int> i in forMax)
    {

      // Keep the maximum cost character and
      // delete the rest
      ans += forTot[i.Key] - i.Value;
    }

    // Return the answer
    return ans;
  }

  // Driver code
  static void Main()
  {

    // Given string
    string s = "AAABBB";

    // Given cost array
    int[] cost = {1, 2, 3, 4, 5, 6};

    // Function Call
    Console.WriteLine(delCost(s, cost));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum cost of
// removing characters to make the string unique
function delCost(s, cost)
{

    // Store the minimum cost required
    var ans = 0;

    // Create a dictionary to store the
    // maximum cost of removal a character
    var forMax = new Map();

    // Create a dictionary to store the total
    // deletion cost of a character
    var forTot = new Map();

    // Traverse the string, S
    for (var i = 0; i < s.length; i++) {

        // Keep track of maximum cost of each character
        if (!forMax.has(s[i])) {
            forMax.set(s[i], cost[i]);
        }
        else {

            // Update the maximum deletion cost
            forMax.set(s[i], Math.max(forMax.get(s[i]),cost[i]))
        }

        // Keep track of the total cost of each character
        if (!forTot.has(s[i])) {
            forTot.set(s[i], cost[i]);
        }
        else {

            // Update the total deletion cost
            forTot.set(s[i], forTot.get(s[i]) + cost[i])
        }
    }

    // Traverse through all the unique characters
    forMax.forEach((value, key) => {

        // Keep the maximum cost character and
        // delete the rest
        ans += forTot.get(key) - value;
    });

    // Return the answer
    return ans;
}

// Driver code

// Given string
var s = "AAABBB";

// Given cost array
var cost = [1, 2, 3, 4, 5, 6];

// Function Call
document.write(delCost(s, cost));

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)
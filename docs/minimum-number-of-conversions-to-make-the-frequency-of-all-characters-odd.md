# 使所有字符的频率为奇数的最小转换次数

> 原文:[https://www . geesforgeks . org/最小转换次数-使所有字符的频率为奇数/](https://www.geeksforgeeks.org/minimum-number-of-conversions-to-make-the-frequency-of-all-characters-odd/)

给定小写字母的字符串**字符串**，任务是输出要进行的最小转换次数，使得所有字符重复奇数次，如果任务不可能，则打印-1。任何字母表都可以转换成任何其他小写字母。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:** 2
> **解释:**将一个‘g’转换为‘e’，将一个‘k’转换为‘s’
> 
> **输入:** str = "geeks"
> **输出:** 1
> **解释:**将“e”转换为字符串中不存在的任何字符

**方法:**给定的问题可以使用[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)来解决。这个想法是计算字母重复偶数次的次数，并将它们的频率存储在 hashmap 中。可以遵循以下方法来解决问题:

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-the-characters-of-a-string-in-java/)并将所有字符放入散列表中:
*   如果该字符已经出现在[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)中，则将其频率增加 1
*   [迭代 hashmap](https://www.geeksforgeeks.org/how-to-iterate-hashmap-in-java/) 并计算偶数频率的字符数，并将其存储在变量 **count** 中
*   如果**计数**的值为:
    *   偶数，然后返回**计数/ 2**
*   奇数，hashmap 的大小为:
    *   小于 26 则返回**计数/ 2 + 1**
    *   等于 26，然后返回-1

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return minimum
// number of conversions required
int maxconv(string s)
{
    // Declare a hashmap
    unordered_map<char, int> map;

    // Insert character into the map
    for (auto x : s) {

        // Increment the frequency of the
        // character present in the string
        map[x]++;
    }

    // Count to store number of even
    // frequency elements
    int count = 0;

    // Loop to calculate characters
    // with even frequency
    for (auto z : map) {

        // If frequency is even
        if (z.second % 2 == 0)

            // Increment the count
            count++;
    }

    // If characters with even
    // frequency are even
    if (count % 2 == 0)

        // return count / 2 as the answer
        return count / 2;

    // If characters with even
    // frequency are even are odd
    else if (count % 2 != 0) {

        // If map contains less than
        // 26 distinct characters
        if (map.size() < 26) {

            // Return count / 2 + 1
            // as the answer
            return (count / 2) + 1;
        }
        else {

            // If map contains 26
            // distinct characters
            return -1;
        }
    }
}
int main()
{
    // Initialize the string
    string s = "geeksforgeeks";

    // Call the function and
    // print the output
    cout << maxconv(s) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;
class GFG
{

    // Function to return minimum
    // number of conversions required
    static int maxconv(String s)
    {

        // Declare a hashmap
        HashMap<Character, Integer> map
            = new HashMap<Character, Integer>();

        // Converting given string to char array

        char[] strArray =s.toCharArray();

        // Insert character into the map
        for (char c : strArray) {
            if (map.containsKey(c)) {

                // If char is present in charCountMap,
                // incrementing it's count by 1
                map.put(c, map.get(c) + 1);
            }
            else {

                // If char is not present in charCountMap,
                // putting this char to charCountMap with 1
                // as it's value
                map.put(c, 1);
            }
        }

        // Count to store number of even
        // frequency elements
        int count = 0;

        // Loop to calculate characters
        // with even frequency
        for (Map.Entry entry : map.entrySet())
        {
            if ((int)entry.getValue() % 2 == 0)
            {

                // Increment the count
                count++;
            }
        }

        // If characters with even
        // frequency are even
        if ((count % 2) == 0)

            // return count / 2 as the answer
            return count / 2;

        // If characters with even
        // frequency are even are odd
        else if (count % 2 != 0) {

            // If map contains less than
            // 26 distinct characters
            if (map.size() < 26) {

                // Return count / 2 + 1
                // as the answer
                return (count / 2) + 1;
            }
            else {

                // If map contains 26
                // distinct characters
                return -1;
            }
        }
      return -1;
    }
    public static void main(String[] args)
    {

        // Initialize the string
        String s = "geeksforgeeks";

        // Call the function and
        // print the output

        System.out.println(maxconv(s));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python implementation for the above approach

# Function to return minimum
# number of conversions required
def maxconv(s):

    # Declare a hashmap
    map = {}

    # Insert character into the map
    for x in s:

        # Increment the frequency of the
        # character present in the string
        if x in map:
            map[x] += 1
        else:
            map[x] = 1

        # Count to store number of even
        # frequency elements
    count = 0

    # Loop to calculate characters
    # with even frequency
    for z in map:

                # If frequency is even
        if (map[z] % 2 == 0):

                        # Increment the count
            count += 1

        # If characters with even
        # frequency are even
    if (count % 2 == 0):

                # return count / 2 as the answer
        return count // 2

        # If characters with even
        # frequency are even are odd
    elif (count % 2 != 0):

        # If map contains less than
        # 26 distinct characters
        if (len(map) < 26):

            # Return count / 2 + 1
            # as the answer
            return (count // 2) + 1

        else:

            # If map contains 26
            # distinct characters
            return -1

if __name__ == "__main__":

        # Initialize the string
    s = "geeksforgeeks"

    # Call the function and
    # print the output
    print(maxconv(s))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to return minimum
    // number of conversions required
    static int maxconv(String s)
    {

        // Declare a hashmap
        Dictionary<char, int> map = new Dictionary<char, int>();

        // Converting given string to char array
        char[] strArray = s.ToCharArray();

        // Insert character into the map
        foreach (char c in strArray)
        {
            if (map.ContainsKey(c))
            {

                // If char is present in charCountMap,
                // incrementing it's count by 1
                map = map + 1;
            }
            else
            {

                // If char is not present in charCountMap,
                // putting this char to charCountMap with 1
                // as it's value
                map = 1;
            }
        }

        // Count to store number of even
        // frequency elements
        int count = 0;

        // Loop to calculate characters
        // with even frequency
        foreach (int entry in map.Values)
        {
            if (entry % 2 == 0)
            {

                // Increment the count
                count++;
            }
        }

        // If characters with even
        // frequency are even
        if ((count % 2) == 0)

            // return count / 2 as the answer
            return count / 2;

        // If characters with even
        // frequency are even are odd
        else if (count % 2 != 0)
        {

            // If map contains less than
            // 26 distinct characters
            if (map.Count < 26)
            {

                // Return count / 2 + 1
                // as the answer
                return (count / 2) + 1;
            }
            else
            {

                // If map contains 26
                // distinct characters
                return -1;
            }
        }
        return -1;
    }

    public static void Main()
    {

        // Initialize the string
        String s = "geeksforgeeks";

        // Call the function and
        // print the output
        Console.Write(maxconv(s));
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to return minimum
// number of conversions required
function maxconv(s)
{

  // Declare a hashmap
  let map = new Map();

  // Insert character into the map
  for (x of s) {

    // Increment the frequency of the
    // character present in the string
    if (map.has(x)) {
      map.set(x, map.get(x) + 1)
    } else {
      map.set(x, 1)
    }
  }

  // Count to store number of even
  // frequency elements
  let count = 0;

  // Loop to calculate characters
  // with even frequency
  for (z of map) {

    // If frequency is even
    if (z[1] % 2 == 0)

      // Increment the count
      count++;
  }

  // If characters with even
  // frequency are even
  if (count % 2 == 0)

    // return count / 2 as the answer
    return Math.floor(count / 2);

  // If characters with even
  // frequency are even are odd
  else if (count % 2 != 0) {

    // If map contains less than
    // 26 distinct characters
    if (map.length < 26) {

      // Return count / 2 + 1
      // as the answer
      return Math.floor(count / 2) + 1;
    }
    else {

      // If map contains 26
      // distinct characters
      return -1;
    }
  }
}

// Initialize the string
let s = "geeksforgeeks";

// Call the function and
// print the output
document.write(maxconv(s))

// This code is contributed by gfgking.
</script>
```

**Output**

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)
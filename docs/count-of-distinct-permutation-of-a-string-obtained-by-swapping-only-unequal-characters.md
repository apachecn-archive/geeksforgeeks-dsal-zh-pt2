# 仅通过交换不相等的字符获得的字符串的不同排列的计数

> 原文:[https://www . geesforgeks . org/通过仅交换不相等字符获得的字符串的不同排列计数/](https://www.geeksforgeeks.org/count-of-distinct-permutation-of-a-string-obtained-by-swapping-only-unequal-characters/)

给定一个字符串，找出可以通过交换两个索引获得的唯一置换的数量，以便这些索引处的元素是不同的。

**注意:**交换总是在原始字符串中执行。

**示例:**

> **输入:** str = "sstt"
> **输出:** 5
> **解释:**
> 用 str[2]交换 str[0]，字符串得到有效的“tsst”(str[0]！=str[2])
> 用 str[3]交换 str[0]。字符串获得“tsts”
> 用字符串[2]交换字符串[1]，字符串获得“stst”
> 用字符串[3]交换字符串[1]，字符串获得“stts”
> 因此可以获得总共 5 个字符串，包括给定的字符串(“sstt”)
> 
> **输入:**str = " ABCD "
> T3】输出: 7

**方法:**使用 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 可以通过以下步骤解决问题:

1.  创建一个 hashmap 并存储给定字符串中每个字符的频率。
2.  创建一个变量 **count，**来存储给定字符串中的字符总数，即 **count=str.length()** 和一个变量 **ans** 来存储可能的唯一排列数并初始化 ans=0。
3.  遍历字符串，对于每个字符:
    *   查找当前索引右侧出现的不同字符的数量。这可以通过用总计数减去该字符的频率来实现。
    *   现在将这个计算值添加到**和**中，因为这是当前字符可以交换的字符数，以创建唯一的排列。
    *   现在，降低当前字符的频率并计数 1，这样它就不会干扰出现在它右边的相同元素的计算。
4.  返回 ans+1，因为给定的字符串也是唯一的排列。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate total
// number of valid permutations
int validPermutations(string str)
{
    unordered_map<char, int> m;

    // Creating count which is equal to the
    // Total number of characters present and
    // ans that will store the number of unique
    // permutations
    int count = str.length(), ans = 0;

    // Storing frequency of each character
    // present in the string
    for (int i = 0; i < str.length(); i++) {
        m[str[i]]++;
    }
    for (int i = 0; i < str.length(); i++) {
        // Adding count of characters by excluding
        // characters equal to current char
        ans += count - m[str[i]];

        // Reduce the frequency of the current character
        // and count by 1, so that it cannot interfere
        // with the calculations of the same elements
        // present to the right of it.
        m[str[i]]--;
        count--;
    }

    // Return ans+1 (Because the given string
    // is also a unique permutation)
    return ans + 1;
}

// Driver Code
int main()
{
    string str = "sstt";
    cout << validPermutations(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

// Importing HashMap class
import java.util.HashMap;

class GFG {

    // Function to calculate total
    // number of valid permutations
    static int validPermutations(String str)
    {

        HashMap<Character, Integer> m
            = new HashMap<Character, Integer>();

        // Creating count which is equal to the
        // Total number of characters present and
        // ans that will store the number of unique
        // permutations
        int count = str.length(), ans = 0;

        // Storing frequency of each character
        // present in the string
        for (int i = 0; i < str.length(); i++) {
            m.put(str.charAt(i),
                  m.getOrDefault(str.charAt(i), 0) + 1);
        }

        for (int i = 0; i < str.length(); i++) {
            // Adding count of characters by excluding
            // characters equal to current char
            ans += count - m.get(str.charAt(i));

            // Reduce the frequency of the current character
            // and count by 1, so that it cannot interfere
            // with the calculations of the same elements
            // present to the right of it.
            m.put(str.charAt(i), m.get(str.charAt(i)) - 1);
            count--;
        }

        // Return ans+1 (Because the given string
        // is also a unique permutation)
        return ans + 1;
    }

    public static void main(String[] args)
    {
        String str = "sstt";

        System.out.println(validPermutations(str));
    }
}

// This code is contributed by rajsanghavi9.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to calculate total
# number of valid permutations
def validPermutations(str):
    m = {}

    # Creating count which is equal to the
    # Total number of characters present and
    # ans that will store the number of unique
    # permutations
    count = len(str)
    ans = 0

    # Storing frequency of each character
    # present in the string
    for i in range(len(str)):
        if(str[i] in m):
            m[str[i]] += 1
        else:
            m[str[i]] = 1
    for i in range(len(str)):

        # Adding count of characters by excluding
        # characters equal to current char
        ans += count - m[str[i]]

        # Reduce the frequency of the current character
        # and count by 1, so that it cannot interfere
        # with the calculations of the same elements
        # present to the right of it.
        m[str[i]] -= 1
        count -= 1

    # Return ans+1 (Because the given string
    # is also a unique permutation)
    return ans + 1

# Driver Code
if __name__ == '__main__':
    str = "sstt"
    print(validPermutations(str))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach

// Importing Dictionary class
using System;
using System.Collections.Generic;

public class GFG {

    // Function to calculate total
    // number of valid permutations
    static int validPermutations(String str)
    {

        Dictionary<char, int> m
            = new Dictionary<char, int>();

        // Creating count which is equal to the
        // Total number of characters present and
        // ans that will store the number of unique
        // permutations
        int count = str.Length, ans = 0;

        // Storing frequency of each character
        // present in the string
        for (int i = 0; i < str.Length; i++) {
            if(m.ContainsKey(str[i]))
                m[str[i]]=m[str[i]]+1;
            else
                m.Add(str[i], 1);
        }

        for (int i = 0; i < str.Length; i++) {
            // Adding count of characters by excluding
            // characters equal to current char
            ans += count - m[str[i]];

            // Reduce the frequency of the current character
            // and count by 1, so that it cannot interfere
            // with the calculations of the same elements
            // present to the right of it.
            if(m.ContainsKey(str[i]))
                m[str[i]]=m[str[i]]-1;
            count--;
        }

        // Return ans+1 (Because the given string
        // is also a unique permutation)
        return ans + 1;
    }

    public static void Main(String[] args)
    {
        String str = "sstt";

        Console.WriteLine(validPermutations(str));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate total
// number of valid permutations
function validPermutations(str) {
  let m = new Map();

  // Creating count which is equal to the
  // Total number of characters present and
  // ans that will store the number of unique
  // permutations
  let count = str.length,
    ans = 0;

  // Storing frequency of each character
  // present in the string
  for (let i = 0; i < str.length; i++) {
    if (m.has(str[i])) {
      m.set(str[i], m.get(str[i]) + 1);
    } else {
      m.set(str[i], 1);
    }
  }
  for (let i = 0; i < str.length; i++)
  {

    // Adding count of characters by excluding
    // characters equal to current char
    ans += count - m.get(str[i]);

    // Reduce the frequency of the current character
    // and count by 1, so that it cannot interfere
    // with the calculations of the same elements
    // present to the right of it.
    m.set(str[i], m.get(str[i]) - 1);
    count--;
  }

  // Return ans+1 (Because the given string
  // is also a unique permutation)
  return ans + 1;
}

// Driver Code
let str = "sstt";
document.write(validPermutations(str));

</script>
```

**Output:** 

```
5
```

***时间复杂度:*** *O(n)*

***辅助空间:** O(n)*
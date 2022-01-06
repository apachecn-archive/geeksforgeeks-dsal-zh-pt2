# 在最多一次交换中找到字典上最小的字符串

> 原文:[https://www . geesforgeks . org/find-按字典顺序排列-最小-最多一个字符串-交换/](https://www.geeksforgeeks.org/find-lexicographically-smallest-string-in-at-most-one-swaps/)

给定一根长度为 **N** 的绳子**绳子**。任务是当最多只允许一次交换时，找出字典上最小的字符串。即两个指标 **1 < = i，j < = n** 可以选择互换。此操作最多可执行一次。

**示例:**

> **输入:** str = "string"
> **输出:** gtrins
> **解释:**
> 选择 i=1，j=6，字符串变成–gtrins。这是字典上可以形成的最小字符串。
> 
> **输入:**【str = " zyxw】
> **输出:** wyxz

**方法:**想法是使用[排序](http://www.geeksforgeeks.org/sorting-algorithms/)并为给定的字符串计算可能的最小字典序字符串。计算排序后的字符串后，从给定的字符串中找到第一个不匹配的字符，并用排序后的字符串中最后出现的不匹配字符替换它。

例如，让 str =“极客”和 sorted =“EEG ks”。首先是无与伦比的性格。必须交换该字符，使其与排序后的字符串相匹配。结果字典最小字符串。当用最后出现的“e”替换“g”时，字符串就变成了 eegks，它在字典上是最小的。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the lexicographically
// smallest string that can be formed by
// swapping at most one character.
// The characters might not necessarily
// be adjacent.
string findSmallest(string s)
{
    int len = s.size();

    // Store last occurrence of every character
      // and  set -1 as default for every character.
    vector<int> loccur(26,-1);

    for (int i = len - 1; i >= 0; --i) {

        // Character index to fill
        // in the last occurrence array
        int chI = s[i] - 'a';
        if (loccur[chI] == -1) {

            // If this is true then this
            // character is being visited
            // for the first time from the last
            // Thus last occurrence of this
            // character is stored in this index
            loccur[chI] = i;
        }
    }

    string sorted_s = s;
    sort(sorted_s.begin(), sorted_s.end());

    for (int i = 0; i < len; ++i) {
        if (s[i] != sorted_s[i]) {

            // Character to replace
            int chI = sorted_s[i] - 'a';

            // Find the last occurrence
            // of this character.
            int last_occ = loccur[chI];

            // Swap this with the last occurrence
            swap(s[i], s[last_occ]);
            break;
        }
    }

    return s;
}

// Driver code
int main()
{
    string s = "geeks";
    cout << findSmallest(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to return the lexicographically
// smallest String that can be formed by
// swapping at most one character.
// The characters might not necessarily
// be adjacent.
static String findSmallest(char []s)
{
    int len = s.length;

    // Store last occurrence of every character
    int []loccur = new int[26];

    // Set -1 as default for every character.
    Arrays.fill(loccur, -1);

    for (int i = len - 1; i >= 0; --i) {

        // Character index to fill
        // in the last occurrence array
        int chI = s[i] - 'a';
        if (loccur[chI] == -1) {

            // If this is true then this
            // character is being visited
            // for the first time from the last
            // Thus last occurrence of this
            // character is stored in this index
            loccur[chI] = i;
        }
    }

    char []sorted_s = s;
    Arrays.sort(sorted_s);

    for (int i = 0; i < len; ++i) {
        if (s[i] != sorted_s[i]) {

            // Character to replace
            int chI = sorted_s[i] - 'a';

            // Find the last occurrence
            // of this character.
            int last_occ = loccur[chI];

            // Swap this with the last occurrence
            char temp = s[last_occ];
            s[last_occ] = s[i];
            s[i] = temp;
            break;
        }
    }

    return String.valueOf(s);
}

// Driver code
public static void main(String[] args)
{
    String s = "geeks";
    System.out.print(findSmallest(s.toCharArray()));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the lexicographically
# smallest string that can be formed by
# swapping at most one character.
# The characters might not necessarily
# be adjacent.
def findSmallest(s) :

    length = len(s);

    # Store last occurrence of every character
    # Set -1 as default for every character.
    loccur = [-1]*26;

    for i in range(length - 1, -1, -1) :

        # Character index to fill
        # in the last occurrence array
        chI = ord(s[i]) - ord('a');
        if (loccur[chI] == -1) :

            # If this is true then this
            # character is being visited
            # for the first time from the last
            # Thus last occurrence of this
            # character is stored in this index
            loccur[chI] = i;

    sorted_s = s;
    sorted_s.sort();

    for i in range(length) :
        if (s[i] != sorted_s[i]) :

            # Character to replace
            chI = ord(sorted_s[i]) - ord('a');

            # Find the last occurrence
            # of this character.
            last_occ = loccur[chI];

            # Swap this with the last occurrence
            # swap(s[i], s[last_occ]);
            s[i],s[last_occ] = s[last_occ],s[i]
            break;

    return "".join(s);

# Driver code
if __name__ == "__main__" :

    s = "geeks";

    print(findSmallest(list(s)));

# This code is contributed by Yash_R
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to return the lexicographically
// smallest String that can be formed by
// swapping at most one character.
// The characters might not necessarily
// be adjacent.
static String findSmallest(char []s)
{
    int len = s.Length;

    // Store last occurrence of every character
    int []loccur = new int[26];

    // Set -1 as default for every character.
    for (int i = 0; i < 26; i++)
        loccur[i] = -1;

    for (int i = len - 1; i >= 0; --i) {

        // char index to fill
        // in the last occurrence array
        int chI = s[i] - 'a';
        if (loccur[chI] == -1) {

            // If this is true then this
            // character is being visited
            // for the first time from the last
            // Thus last occurrence of this
            // character is stored in this index
            loccur[chI] = i;
        }
    }

    char []sorted_s = s;
    Array.Sort(sorted_s);

    for (int i = 0; i < len; ++i) {
        if (s[i] != sorted_s[i]) {

            // char to replace
            int chI = sorted_s[i] - 'a';

            // Find the last occurrence
            // of this character.
            int last_occ = loccur[chI];

            // Swap this with the last occurrence
            char temp = s[last_occ];
            s[last_occ] = s[i];
            s[i] = temp;
            break;
        }
    }

    return String.Join("", s);
}

// Driver code
public static void Main(String[] args)
{
    String s = "geeks";
    Console.Write(findSmallest(s.ToCharArray()));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the lexicographically
// smallest string that can be formed by
// swapping at most one character.
// The characters might not necessarily
// be adjacent.
function findSmallest(s)
{
    let len = s.length;

    // Store last occurrence of every character
    let loccur = new Array(26);

    // Set -1 as default for every character.
    loccur.fill(-1);

    for(let i = len - 1; i >= 0; --i)
    {

        // Character index to fill
        // in the last occurrence array
        let chI = s[i].charCodeAt() -
                   'a'.charCodeAt();
        if (loccur[chI] == -1)
        {

            // If this is true then this
            // character is being visited
            // for the first time from the last
            // Thus last occurrence of this
            // character is stored in this index
            loccur[chI] = i;
        }
    }

    let sorted_s = s;
    sorted_s.sort();

    for(let i = 0; i < len; ++i)
    {
        if (s[i] != sorted_s[i])
        {

            // Character to replace
            let chI = sorted_s[i].charCodeAt() -
                              'a'.charCodeAt();

            // Find the last occurrence
            // of this character.
            let last_occ = loccur[chI];

            // Swap this with the last occurrence
            let temp = s[i];
            s[i] = s[last_occ];
            s[last_occ] = temp;
            break;
        }
    }
    return s.join("");
}

// Driver code
let s = "geeks";

document.write(findSmallest(s.split('')));

// This code is contributed by vaibhavrabadiya3

</script>
```

**Output:** 

```
eegks
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)
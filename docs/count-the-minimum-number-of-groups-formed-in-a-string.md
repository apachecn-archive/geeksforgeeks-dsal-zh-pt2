# 计算一个字符串中形成的最小组数

> 原文:[https://www . geeksforgeeks . org/count-最小字符串分组数/](https://www.geeksforgeeks.org/count-the-minimum-number-of-groups-formed-in-a-string/)

给定一个由两个或多个大写英文字母组成的字符串。任务是通过用相同的单个字符替换连续字符来计算完全覆盖字符串所需的最小组数。

**示例:**

```
Input : S = "TTWWW"
Output : 2
Explanation : 
There are 2 groups formed. One by covering the 2 consecutive T and the other by 3 consecutive W. 

Input : S = "FFMMMF"
Output : 3
Explanation : 
Minimum number of groups formed is 3 that is two F's, three M's and one F .
Note: Three F's were not included in one group because they are not consecutive in the string s.
```

**方法:**
解决上述问题的主要思路是将字符串‘S’中相邻的字符逐一进行比较。例如，如果字符不同，即字符串的连续字母不相同，则形成的总组的计数器递增 1，以此类推，直到我们达到字符串的长度。

以下是上述方法的实施情况:

## C++

```
// C++ implementation to Count the
// minimum number of groups formed in a string
// by replacing consecutive characters
// with same single character
#include<bits/stdc++.h>

using namespace std;

// Function to count the minimum number
// of groups formed in the given string s
void group_formed(string S){

    // Initializing count as one since
    // the string is not NULL
    int count = 1;

    for (int i = 0; i < S.size() - 1; i++){

        // Comparing adjacent characters
        if ( S[i] != S[i+1])
            count += 1;
          }

    cout << (count);
  }

// Driver Code
int main(){
    string S = "TTWWW";

    group_formed(S);
  }

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Count the
// minimum number of groups formed in a string
// by replacing consecutive characters
// with same single character
class GFG {

    // Function to count the minimum number
    // of groups formed in the given string s
    static void group_formed(String S){

        // Initializing count as one since
        // the string is not NULL
        int count = 1;

        for (int i = 0; i < S.length() - 1; i++){

            // Comparing adjacent characters
            if ( S.charAt(i) != S.charAt(i+1))
                count += 1;
            }

        System.out.println(count);
    }

    // Driver Code
    public static void main (String[] args) {
        String S = "TTWWW";

        group_formed(S);
    }
}

 // This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to Count the
# minimum number of groups formed in a string
# by replacing consecutive characters
# with same single character

# Function to count the minimum number
# of groups formed in the given string s
def group_formed(S):

    # Initializing count as one since
    # the string is not NULL
    count = 1

    for i in range (len(S)-1):
        a = S[i]
        b = S[i + 1]

        # Comparing adjacent characters
        if ( a != b):

            count += 1

    print (count)

# Driver Code
if __name__ == "__main__":
    S = "TTWWW"

    group_formed(S)
```

## C#

```
// C# implementation to Count the
// minimum number of groups formed
// in a string by replacing consecutive
// characters with same single character
using System;

class GFG{

// Function to count the minimum number
// of groups formed in the given string s
static void group_formed(String S)
{

    // Initializing count as one since
    // the string is not NULL
    int count = 1;

    for(int i = 0; i < S.Length - 1; i++)
    {

       // Comparing adjacent characters
       if (S[i] != S[i + 1])
           count += 1;
    }
    Console.Write(count);
}

// Driver Code
public static void Main (String[] args)
{
    String S = "TTWWW";

    group_formed(S);
}
}

// This code is contributed by Rajnis09
```

## java 描述语言

```
<script>

// Javascript implementation to Count the
// minimum number of groups formed
// in a string by replacing consecutive
// characters with same single character

// Function to count the minimum number
// of groups formed in the given string s
function group_formed(S)
{

    // Initializing count as one since
    // the string is not NULL
    let count = 1;

    for(let i = 0; i < S.length - 1; i++)
    {

        // Comparing adjacent characters
        if (S[i] != S[i + 1])
            count += 1;
    }
    document.write(count);
}

// Driver code
let S = "TTWWW";

group_formed(S);

// This code is contributed by divyesh072019 

</script>
```

**Output:** 

```
2
```
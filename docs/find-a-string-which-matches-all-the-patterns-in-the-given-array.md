# 找到与给定数组中所有模式匹配的字符串

> 原文:[https://www . geesforgeks . org/find-a-string-match-all-in-the-patterns-in-给定数组/](https://www.geeksforgeeks.org/find-a-string-which-matches-all-the-patterns-in-the-given-array/)

给定一个字符串数组 **arr[]** ，其中包含字符模式和“*”表示任何一组字符，包括空字符串。任务是找到一个匹配数组中所有模式的字符串。
**注:**如无此可能图案，打印-1。
**示例:**

> **输入:**arr[]= {“pq * du * q”、“pq*abc*q”、“p * d * q”}
> **输出:** pqduabcdq
> **解释:**
> 模式“pqduabcdq”匹配所有字符串:
> **字符串 1:**
> 第一个“*”可以用空字符串替换。
> 第二个“*”可以用“abcdq”代替。
> **字符串 2:**
> 第一个“*”可以替换为“du”
> 第二个“*”可以替换为“d”
> **字符串 3:**
> 第一个“*”可以替换为“q”
> 第二个“*”可以替换为“uabcd”
> **输入:**arr[]= {“a * c”、“* }
> **输出:** ac

**做法:**思路是在所有模式中找到共同的前缀和后缀串，然后每个模式的中间可以用每个模式中的第一个或最后一个“*”代替。以下是该方法的示例:

*   创建三个与每个模式的前缀、后缀和中间部分匹配的空字符串。
*   迭代数组中的每个模式，对于每个模式:
    *   查找模式中的第一个和最后一个“*”。
    *   迭代现有前缀，检查它是否与模式的当前前缀匹配，如果有任何字符与模式不匹配，返回-1。
    *   如果在当前模式的前缀中有剩余的部分，则将其附加到公共字符串的前缀中。
    *   同样，匹配模式的后缀。
    *   最后，将除中间初始化字符串中的“*”之外的所有中间字符追加到公共字符串中。
*   最后，连接公共字符串的前缀、中间和后缀部分。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// string which matches
// all the patterns

#include<bits/stdc++.h>
using namespace std;

// Function to find a common string
// which matches all the pattern
string find(vector<string> S,int N)
{
    // For storing prefix till
    // first most * without conflicts
    string pref;

    // For storing suffix till
    // last most * without conflicts
    string suff;

    // For storing all middle
    // characters between
    // first and last *
    string mid;

    // Loop to iterate over every
    // pattern of the array
    for (int i = 0; i < N; i++) {

        // Index of the first "*"
        int first = int(
            S[i].find_first_of('*')
            );

        // Index of Last "*"
        int last = int(
            S[i].find_last_of('*')
            );

        // Iterate over the first "*"
        for (int z = 0; z < int(pref.size()) &&
                              z < first; z++) {
            if (pref[z] != S[i][z]) {
                return "*";
            }
        }

        // Prefix till first most *
        // without conflicts
        for (int z = int(pref.size());
                       z < first; z++) {
            pref += S[i][z];
        }

        // Iterate till last
        // most * from last
        for (int z = 0; z < int(suff.size()) &&
               int(S[i].size())-1-z > last; z++) {
            if (suff[z] != S[i][int(S[i].size())-1-z]) {
                return "*";
            }
        }

        // Make suffix till last
        // most * without conflicts
        for (int z = int(suff.size());
         int(S[i].size())-1-z > last; z++) {
            suff += S[i][int(S[i].size())-1-z];
        }

        // Take all middle characters
        // in between first and last most *
        for (int z = first; z <= last; z++) {
            if (S[i][z] != '*') mid += S[i][z];
        }
    }

    reverse(suff.begin(), suff.end());
    return pref + mid + suff;
}

// Driver Code
int main() {

    int N = 3;
    vector<string> s(N);

    // Take all
    // the strings
    s[0]="pq*du*q";
    s[1]="pq*abc*q";
    s[2]="p*d*q";

    // Method for finding
    // common string
    cout<<find(s,N);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation
# to find the string which
# matches all the patterns

# Function to find a common
# string which matches all
# the pattern
def find(S, N):

    # For storing prefix
    # till first most *
    # without conflicts
    pref = ""

    # For storing suffix
    # till last most *
    # without conflicts
    suff = ""

    # For storing all middle
    # characters between
    # first and last *
    mid = ""

    # Loop to iterate over every
    # pattern of the array
    for i in range(N):

        # Index of the first "*"
        first = int(S[i].index("*"))

        # Index of Last "*"
        last = int(S[i].rindex("*"))

        # Iterate over the first "*"
        for z in range(len(pref)):
            if(z < first):
                if(pref[z] != S[i][z]):
                    return "*"

        # Prefix till first most *
        # without conflicts
        for z in range(len(pref),first):
            pref += S[i][z];

        # Iterate till last
        # most * from last
        for z in range(len(suff)):
            if(len(S[i]) - 1 - z > last):
                if(suff[z] != S[i][len(S[i]) - 1 - z]):
                    return "*"

        # Make suffix till last
        # most * without conflicts
        for z in range(len(suff),
                       len(S[i]) - 1 - last):
            suff += S[i][len(S[i]) - 1 - z]

        # Take all middle characters
        # in between first and last most *
        for z in range(first, last + 1):
            if(S[i][z] != '*'):
                mid += S[i][z]

    suff=suff[:: -1]
    return pref + mid + suff

# Driver Code
N = 3
s = ["" for i in range(N)]

# Take all
# the strings
s[0] = "pq*du*q"
s[1] = "pq*abc*q"
s[2] = "p*d*q"

# Method for finding
# common string
print(find(s, N))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
pqduabcdq

```
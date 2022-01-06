# 计数由相等数量的 a、b、c 和 d 组成的子串

> 原文:[https://www . geeksforgeeks . org/count-substrings-由-a-b-c-和-d-等数组成/](https://www.geeksforgeeks.org/count-substrings-consisting-of-equal-number-of-a-b-c-and-d/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是计算数量相等的**【a】****【b】****【c】**和**【d】**的非空子字符串。

**示例:**

> **输入:** str = "abcdef"
> **输出:** 6
> **解释:**
> 由等个数的 **'a'** ， **'b'** ， **'c'** ， **'d'** 组成的子串为{“ABCD”、“abcde”、“abcdf”、“abcdef”、“e”、“f”}。
> 因此，要求输出为 6。
> 
> **输入:**输出: 0

**方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以解决问题。这个想法是基于以下观察:

> 如果子串{str[0]，…，str[i] }中的字符{ 'a '，' b '，' c '，' d' }的频率为{ p，q，r，s}，子串{str[0]，…，str[j] }的频率为{ p + x，q + x，r + x，s + x }，则子串{ str[i]，…，str[j] }必须包含相等数量的 **'a'** ， **'b'** ， **'c**

按照以下步骤解决问题:

*   初始化一个变量，比如 **cntSub** ，以存储相同数量的**【a】****【b】****【c】****【d】**的子串计数。
*   初始化一张[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp** ，来存储字符{**【a】****【b】****【c】****【d】**}的相对频率。

> 如果字符**‘a’**、**‘b’**、**‘c’**、**‘d’**的频率为{ p，q，r，s }，那么字符的相对频率为{ p–y，q–y，r–y，s–y }，其中 y = min({p，q，r，s})

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，存储字符**【a】****【b】****【c】**和**【d】**的相对频率。
*   [使用地图的关键值作为 **i** 遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，对于每个关键值，将 **cntSub** 的值增加![{mp[i] \choose 2}   ](img/bfa0f2fac8a0f9dd3067639a4493f08f.png "Rendered by QuickLaTeX.com")。
*   最后，打印 **cntSub** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the substring with
// equal number of a, b, c and d
int countSubstrings(string str)
{

    // Stores relative frequency of
    // the characters {'a', 'b', 'c', 'd'}
    map<pair<pair<int, int>,
             pair<int, int> >,
        int>
        mp;

    // Initially, frequencies of
    // 'a', 'b', 'c' and 'd' are 0.
    mp[{ { 0, 0 }, { 0, 0 } }]++;

    // Stores relative
    // frequency of 'a'
    int p = 0;

    // Stores relative
    // frequency of 'b'
    int q = 0;

    // Stores relative
    // frequency of 'c'
    int r = 0;

    // Stores relative
    // frequency of 'd'
    int s = 0;

    // Stores count of substring with equal
    // number of 'a', 'b', 'c' and 'd'
    int cntSub = 0;

    // Iterate over the characters
    // of the string
    for (int i = 0; i < str.length(); i++) {

        // If current character
        // is 'a'
        if (str[i] == 'a') {

            // Update p
            p++;

            // Stores minimum
            // of { p, q, r, s}
            int Y = min(min(s, r),
                        min(p, q));

            // Update p
            p -= Y;

            // Update q
            q -= Y;

            // Update r
            r -= Y;

            // Update s
            s -= Y;
        }

        // If current character is b
        else if (str[i] == 'b') {

            // Update q
            q++;

            // Stores minimum
            // of { p, q, r, s}
            int Y = min(min(p, q),
                        min(r, s));

            // Update p
            p -= Y;

            // Update q
            q -= Y;

            // Update r
            r -= Y;

            // Update s
            s -= Y;
        }
        else if (str[i] == 'c') {

            // Update r
            r++;

            // Stores minimum
            // of { p, q, r, s}
            int Y = min(min(p, q),
                        min(r, s));

            // Update p
            p -= Y;

            // Update q
            q -= Y;

            // Update r
            r -= Y;

            // Update s
            s -= Y;
        }
        else if (str[i] == 'd') {

            // Update s
            s++;

            // Stores minimum
            // of { p, q, r, s}
            int Y = min(min(p, q),
                        min(r, s));

            // Update p
            p -= Y;

            // Update q
            q -= Y;

            // Update r
            r -= Y;

            // Update s
            s -= Y;
        }

        // Update relative frequency
        // of {p, q, r, s}
        mp[{ { p, q }, { r, s } }]++;
    }

    // Traverse the map
    for (auto& e : mp) {

        // Stores count of
        // relative frequency
        int freq = e.second;

        // Update cntSub
        cntSub += (freq) * (freq - 1) / 2;
    }
    return cntSub;
}

// Driver Code
int main()
{

    string str = "abcdefg";

    // Function Call
    cout << countSubstrings(str);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the substring with
# equal number of a, b, c and d
def countSubstrings(Str) :

    # Stores relative frequency of
    # the characters {'a', 'b', 'c', 'd'}
    mp = {}

    # Initially, frequencies of
    # 'a', 'b', 'c' and 'd' are 0.
    if ((0, 0), (0, 0)) in mp :
        mp[(0, 0), (0, 0)] += 1
    else :
        mp[(0, 0), (0, 0)] = 1

    # Stores relative
    # frequency of 'a'
    p = 0

    # Stores relative
    # frequency of 'b'
    q = 0

    # Stores relative
    # frequency of 'c'
    r = 0

    # Stores relative
    # frequency of 'd'
    s = 0

    # Stores count of substring with equal
    # number of 'a', 'b', 'c' and 'd'
    cntSub = 0

    # Iterate over the characters
    # of the string
    for i in range(len(Str)) :

        # If current character
        # is 'a'
        if (Str[i] == 'a') :
            # Update p
            p += 1

            # Stores minimum
            # of { p, q, r, s}
            Y = min(min(s, r), min(p, q))

            # Update p
            p -= Y

            # Update q
            q -= Y

            # Update r
            r -= Y

            # Update s
            s -= Y

        # If current character is b
        elif (Str[i] == 'b') :

            # Update q
            q += 1

            # Stores minimum
            # of { p, q, r, s}
            Y = min(min(p, q), min(r, s))

            # Update p
            p -= Y

            # Update q
            q -= Y

            # Update r
            r -= Y

            # Update s
            s -= Y

        elif (Str[i] == 'c') :

            # Update r
            r += 1

            # Stores minimum
            # of { p, q, r, s}
            Y = min(min(p, q),min(r, s))

            # Update p
            p -= Y

            # Update q
            q -= Y

            # Update r
            r -= Y

            # Update s
            s -= Y

        elif (Str[i] == 'd') :

            # Update s
            s += 1

            # Stores minimum
            # of { p, q, r, s}
            Y = min(min(p, q),min(r, s))

            # Update p
            p -= Y

            # Update q
            q -= Y

            # Update r
            r -= Y

            # Update s
            s -= Y

        # Update relative frequency
        # of {p, q, r, s}
        if ((p, q), (r, s)) in mp :
            mp[(p, q), (r, s)] += 1
        else :
            mp[(p, q), (r, s)] = 1

    # Traverse the map
    for e in mp :

        # Stores count of
        # relative frequency

        freq = mp[e]

        # Update cntSub
        cntSub += (freq) * (freq - 1) // 2

    return cntSub

  # Driver code
Str = "abcdefg"

# Function Call
print(countSubstrings(Str))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic; 
class GFG {

    // Function to count the substring with
    // equal number of a, b, c and d
    static int countSubstrings(string str)
    {

        // Stores relative frequency of
        // the characters {'a', 'b', 'c', 'd'}
        Dictionary<Tuple<Tuple<int, int>,
      Tuple<int, int>>, int> mp =
        new Dictionary<Tuple<Tuple<int, int>,
      Tuple<int, int>>, int>(); 

        // Initially, frequencies of
        // 'a', 'b', 'c' and 'd' are 0.
        if(mp.ContainsKey(new Tuple<Tuple<int, int>,
                          Tuple<int, int>>(new Tuple<int, int>(0, 0),
                                           new Tuple<int, int>(0, 0))))
        {
            mp[new Tuple<Tuple<int, int>,
               Tuple<int, int>>(new Tuple<int, int>(0, 0),
                                new Tuple<int, int>(0, 0))]++;
        }
        else{
            mp[new Tuple<Tuple<int, int>,
               Tuple<int, int>>(new Tuple<int, int>(0, 0),
                                new Tuple<int, int>(0, 0))] = 1;
        }

        // Stores relative
        // frequency of 'a'
        int p = 0;

        // Stores relative
        // frequency of 'b'
        int q = 0;

        // Stores relative
        // frequency of 'c'
        int r = 0;

        // Stores relative
        // frequency of 'd'
        int s = 0;

        // Stores count of substring with equal
        // number of 'a', 'b', 'c' and 'd'
        int cntSub = 0;

        // Iterate over the characters
        // of the string
        for (int i = 0; i < str.Length; i++) {

            // If current character
            // is 'a'
            if (str[i] == 'a') {

                // Update p
                p++;

                // Stores minimum
                // of { p, q, r, s}
                int Y = Math.Min(Math.Min(s, r),
                            Math.Min(p, q));

                // Update p
                p -= Y;

                // Update q
                q -= Y;

                // Update r
                r -= Y;

                // Update s
                s -= Y;
            }

            // If current character is b
            else if (str[i] == 'b') {

                // Update q
                q++;

                // Stores minimum
                // of { p, q, r, s}
                int Y = Math.Min(Math.Min(p, q),
                            Math.Min(r, s));

                // Update p
                p -= Y;

                // Update q
                q -= Y;

                // Update r
                r -= Y;

                // Update s
                s -= Y;
            }
            else if (str[i] == 'c') {

                // Update r
                r++;

                // Stores minimum
                // of { p, q, r, s}
                int Y = Math.Min(Math.Min(p, q),
                            Math.Min(r, s));

                // Update p
                p -= Y;

                // Update q
                q -= Y;

                // Update r
                r -= Y;

                // Update s
                s -= Y;
            }
            else if (str[i] == 'd') {

                // Update s
                s++;

                // Stores minimum
                // of { p, q, r, s}
                int Y = Math.Min(Math.Min(p, q),
                            Math.Min(r, s));

                // Update p
                p -= Y;

                // Update q
                q -= Y;

                // Update r
                r -= Y;

                // Update s
                s -= Y;
            }

            // Update relative frequency
            // of {p, q, r, s}
            if(mp.ContainsKey(new Tuple<Tuple<int, int>,
                              Tuple<int, int>>(new Tuple<int, int>(p, q),
                                               new Tuple<int, int>(r, s))))
            {
                mp[new Tuple<Tuple<int, int>,
                   Tuple<int, int>>(new Tuple<int, int>(p, q),
                                    new Tuple<int, int>(r, s))]++;
            }
            else{
                mp[new Tuple<Tuple<int, int>,
                   Tuple<int, int>>(new Tuple<int, int>(p, q),
                                    new Tuple<int, int>(r, s))] = 1;
            }
        }

        // Traverse the map
        foreach(KeyValuePair<Tuple<Tuple<int, int>,
                Tuple<int, int>>, int> e in mp)
        {

            // Stores count of
            // relative frequency
            int freq = e.Value;

            // Update cntSub
            cntSub += (freq) * (freq - 1) / 2;
        }
        return cntSub;
    }

  // Driver code
  static void Main()
  {

    string str = "abcdefg";

    // Function Call
    Console.WriteLine(countSubstrings(str));
  }
}

// This code is contributed by divyesh072019
```

**Output:** 

```
10
```

***时间复杂度:** O(N * Log(N))*
***辅助空间:** O(N)*
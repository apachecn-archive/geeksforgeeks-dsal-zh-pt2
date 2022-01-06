# 元音的最长有序子序列

> 原文:[https://www . geesforgeks . org/元音最长有序子序列/](https://www.geeksforgeeks.org/longest-ordered-subsequence-of-vowels/)

给定一个仅由元音组成的字符串，找到给定字符串中最长的子序列，使其由所有五个元音组成，并且是一个或多个 a 的序列，后面是一个或多个 e，接着是一个或多个 I，接着是一个或多个 o，接着是一个或多个 u。

如果有多个最长的子序列，打印任意一个。

**示例:**

```
Input :  str = "aeiaaioooaauuaeiou" 
Output :  {a, a, a, a, a, a, e, i, o, u}
There are two possible outputs in this case: 
{a, a, a, a, a, a, e, i, o, u} and, 
{a, e, i, i, o, o, o, u, u, u}
each of length 10

Input : str = "aaauuiieeou"
Output : No subsequence possible
```

**方法:**
我们递归地遍历字符串中的所有字符，并遵循给定的条件:

1.  如果子序列是空的，只有当它是“a”时，我们才在当前索引处包含元音。否则，我们继续下一个索引。
2.  如果当前索引处的元音与子序列中包含的最后一个元音相同，我们就包含它。
3.  如果当前索引处的元音是包含在子序列中的最后一个元音之后的下一个可能的元音(即 a –> e –> I –> o –> u ),我们有两个选择:要么包含它，要么继续下一个索引。因此我们选择给出最长子序列的那个。
4.  如果以上条件都不满足，我们继续下一个索引(以避免子序列中元音的无效排序)。
5.  如果我们已经到达字符串的末尾，我们检查当前子序列是否有效。如果它是有效的(即如果它包含所有的元音)，我们返回它，否则我们返回一个空列表。

**方法 1**

下面是上述方法的实现:

## C++

```
// C++ program to find the longest subsequence
// of vowels in the specified order
#include <bits/stdc++.h>
using namespace std;

vector<char> vowels = { 'a', 'e', 'i', 'o', 'u' };

// Mapping values for vowels
map<char, int> mapping = { { 'a', 0 }, { 'e', 1 },
                           { 'i', 2 }, { 'o', 3 },
                           { 'u', 4 } };

// Function to check if given subsequence
// contains all the vowels or not
bool isValidSequence(string subList)
{
    for(char c : vowels)
    {

        // not contain vowel
        if (subList.find(c) == std::string::npos)
            return 0;
    } 
    return 1;
}

// Function to find the longest subsequence
// of vowels in the given string in specified
// order
string longestSubsequence(string str,
                          string subList,
                          int index)
{

    // If we have reached the end of the
    // string, return the subsequence
    // if it is valid, else return an
    // empty list
    int len = str.length();

    if (index >= len)
    {
        if (isValidSequence(subList))
            return subList;
        else
            return "";
    }

    // If there is no vowel in the
    // subsequence yet, add vowel
    // at current index if it is 'a',
    // else move on to the next character
    // in the string 
    else if (subList.size() == 0)
   {
       if (str[index] != 'a')
         return longestSubsequence(
             str, "", index + 1);
       else
         return longestSubsequence(
             str, subList + str[index],
                    index + 1);
   }

    //  If the last vowel in the subsequence
    // until now is same as the vowel at
    // current index, add it to the subsequence
    else if (mapping[subList[subList.size() - 1]] ==
             mapping[str[index]])
        return longestSubsequence(
            str, subList+str[index], index + 1);

    // If the vowel at the current index comes
    // right after the last vowel in the
    // subsequence, we have two options:
    // either to add the vowel in the
    // subsequence, or move on to next character.
    // We choose the one which gives the longest
    // subsequence.
    else if (mapping[subList[subList.size() - 1]] + 1 ==
             mapping[str[index]])
    {
        string sub1 = longestSubsequence(
            str, subList + str[index], index + 1);
        string sub2 = longestSubsequence(
            str, subList, index + 1);

        if (sub1.length() > sub2.length())
            return sub1;
        else
            return sub2;
    }   
    else
        return longestSubsequence(
            str, subList, index + 1);    
}

// Driver Code
int main()
{
    string  str= "aeiaaioooauuaeiou";

    string subsequence = longestSubsequence(
        str, "", 0);

    if (subsequence.length() == 0)
        cout << "No subsequence possible\n";
    else
        cout << subsequence << "\n";
}

// This code is contributed by ajaykr00kj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest subsequence
// of vowels in the specified order
import java.util.*;
public class Main
{
    static Vector<Character> vowels = new Vector<Character>();

    // Mapping values for vowels
    static HashMap<Character, Integer> mapping = new HashMap<Character, Integer>();

    // Function to check if given subsequence
    // contains all the vowels or not
    static boolean isValidSequence(String subList)
    {
        for(char c : vowels)
        {

            // not contain vowel
            if (subList.indexOf(c) < 0)
                return false;
        }
        return true;
    }

    // Function to find the longest subsequence
    // of vowels in the given string in specified
    // order
    static String longestSubsequence(String str, String subList, int index)
    {

        // If we have reached the end of the
        // string, return the subsequence
        // if it is valid, else return an
        // empty list
        int len = str.length();

        if (index >= len)
        {
            if (isValidSequence(subList))
                return subList;
            else
                return "";
        }

        // If there is no vowel in the
        // subsequence yet, add vowel
        // at current index if it is 'a',
        // else move on to the next character
        // in the string
        else if (subList.length() == 0)
       {
           if (str.charAt(index) != 'a')
             return longestSubsequence(str, "", index + 1);
           else
             return longestSubsequence(str, subList + str.charAt(index), index + 1);
       }

        //  If the last vowel in the subsequence
        // until now is same as the vowel at
        // current index, add it to the subsequence
        else if (mapping.get(subList.charAt(subList.length() - 1)) ==
                 mapping.get(str.charAt(index)))
            return longestSubsequence(str, subList+str.charAt(index), index + 1);

        // If the vowel at the current index comes
        // right after the last vowel in the
        // subsequence, we have two options:
        // either to add the vowel in the
        // subsequence, or move on to next character.
        // We choose the one which gives the longest
        // subsequence.
        else if (mapping.get(subList.charAt(subList.length() - 1)) + 1 ==
                 mapping.get(str.charAt(index)))
        {
            String sub1 = longestSubsequence(
                str, subList + str.charAt(index), index + 1);
            String sub2 = longestSubsequence(
                str, subList, index + 1);

            if (sub1.length() > sub2.length())
                return sub1;
            else
                return sub2;
        } 
        else
            return longestSubsequence(
                str, subList, index + 1);  
    }

    public static void main(String[] args) {
        mapping.put('a', 0);
        mapping.put('e', 1);
        mapping.put('i', 2);
        mapping.put('o', 3);
        mapping.put('u', 4);

        vowels.add('a');
        vowels.add('e');
        vowels.add('i');
        vowels.add('o');
        vowels.add('u');

        String str= "aeiaaioooauuaeiou";

        String subsequence = longestSubsequence(str, "", 0);

        if (subsequence.length() == 0)
            System.out.println("No subsequence possible");
        else
        {
            System.out.print("[");
            for(int i = 0; i < subsequence.length() - 1; i++)
            {
                System.out.print("'" + subsequence.charAt(i) + "'" + ", ");
            }
            System.out.print("'" + subsequence.charAt(subsequence.length()-1) + "'" + "]");
        }
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program to find the longest subsequence
# of vowels in the specified order

vowels = ['a', 'e', 'i', 'o', 'u']

# Mapping values for vowels
mapping = {'a': 0, 'e': 1, 'i': 2, 'o': 3, 'u': 4}

# Function to check if given subsequence
# contains all the vowels or not
def isValidSequence(subList):

    for vowel in vowels:
        if vowel not in subList:
            return False

    return True

# Function to find the longest subsequence of vowels
# in the given string in specified order
def longestSubsequence(string, subList, index):

    # If we have reached the end of the string,
    # return the subsequence
    # if it is valid, else return an empty list
    if index == len(string):
        if isValidSequence(subList) == True:
            return subList
        else:
            return []

    else:
        # If there is no vowel in the subsequence yet,
        # add vowel at current index if it is 'a',
        # else move on to the next character
        # in the string
        if len(subList) == 0:

            if string[index] != 'a':
                return longestSubsequence(string, subList, index + 1)
            else:
                return longestSubsequence(string, subList + \
                            [string[index]], index + 1)

        # If the last vowel in the subsequence until
        # now is same as the vowel at current index,
        # add it to the subsequence
        elif mapping[subList[-1]] == mapping[string[index]]:
            return longestSubsequence(string, subList + \
                            [string[index]], index + 1)

        # If the vowel at the current index comes
        # right after the last vowel
        # in the subsequence, we have two options:
        # either to add the vowel in
        # the subsequence, or move on to next character.
        # We choose the one which gives the longest subsequence.
        elif (mapping[subList[-1]] + 1) == mapping[string[index]]:

            sub1 = longestSubsequence(string, subList + \
                                [string[index]], index + 1)
            sub2 = longestSubsequence(string, subList, index + 1)

            if len(sub1) > len(sub2):
                return sub1
            else:
                return sub2

        else:
            return longestSubsequence(string, subList, index + 1)

# Driver Code
if __name__ == "__main__":

    string = "aeiaaioooauuaeiou"

    subsequence = longestSubsequence(string, [], 0)
    if len(subsequence) == 0:
        print("No subsequence possible")
    else:
        print(subsequence)

```

## C#

```
// C# program to find the longest subsequence
// of vowels in the specified order
using System;
using System.Collections.Generic;
class GFG {

    static List<char> vowels = new List<char>(new char[]{'a', 'e', 'i', 'o', 'u'});

    // Mapping values for vowels
    static Dictionary<char, int> mapping = new Dictionary<char, int>();

    // Function to check if given subsequence
    // contains all the vowels or not
    static bool isValidSequence(string subList)
    {
        foreach(char c in vowels)
        {

            // not contain vowel
            if (subList.IndexOf(c) < 0)
                return false;
        }
        return true;
    }

    // Function to find the longest subsequence
    // of vowels in the given string in specified
    // order
    static string longestSubsequence(string str,
                              string subList,
                              int index)
    {

        // If we have reached the end of the
        // string, return the subsequence
        // if it is valid, else return an
        // empty list
        int len = str.Length;

        if (index >= len)
        {
            if (isValidSequence(subList))
                return subList;
            else
                return "";
        }

        // If there is no vowel in the
        // subsequence yet, add vowel
        // at current index if it is 'a',
        // else move on to the next character
        // in the string
        else if (subList.Length == 0)
       {
           if (str[index] != 'a')
             return longestSubsequence(
                 str, "", index + 1);
           else
             return longestSubsequence(
                 str, subList + str[index],
                        index + 1);
       }

        //  If the last vowel in the subsequence
        // until now is same as the vowel at
        // current index, add it to the subsequence
        else if (mapping[subList[subList.Length - 1]] ==
                 mapping[str[index]])
            return longestSubsequence(
                str, subList+str[index], index + 1);

        // If the vowel at the current index comes
        // right after the last vowel in the
        // subsequence, we have two options:
        // either to add the vowel in the
        // subsequence, or move on to next character.
        // We choose the one which gives the longest
        // subsequence.
        else if (mapping[subList[subList.Length - 1]] + 1 ==
                 mapping[str[index]])
        {
            string sub1 = longestSubsequence(
                str, subList + str[index], index + 1);
            string sub2 = longestSubsequence(
                str, subList, index + 1);

            if (sub1.Length > sub2.Length)
                return sub1;
            else
                return sub2;
        }  
        else
            return longestSubsequence(
                str, subList, index + 1);   
    }

  static void Main() {
    mapping['a'] = 0;
    mapping['e'] = 1;
    mapping['i'] = 2;
    mapping['o'] = 3;
    mapping['u'] = 4;

    string str= "aeiaaioooauuaeiou";

    string subsequence = longestSubsequence(str, "", 0);

    if (subsequence.Length == 0)
        Console.Write("No subsequence possible");
    else
    {
        Console.Write("[");
        for(int i = 0; i < subsequence.Length - 1; i++)
        {
            Console.Write("'" + subsequence[i] + "'" + ", ");
        }
        Console.Write("'" + subsequence[subsequence.Length-1] + "'" + "]");
    }
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program to find the longest subsequence
    // of vowels in the specified order

    let vowels = [ 'a', 'e', 'i', 'o', 'u' ];

    // Mapping values for vowels
    let mapping = new Map();
    mapping['a'] = 0;
    mapping['e'] = 1;
    mapping['i'] = 2;
    mapping['o'] = 3;
    mapping['u'] = 4;

    // Function to check if given subsequence
    // contains all the vowels or not
    function isValidSequence(subList)
    {
        for(let c = 0; c < vowels.length; c++)
        {

            // not contain vowel
            if (!subList.includes(vowels))
                return false;
        }
        return true;
    }

    // Function to find the longest subsequence
    // of vowels in the given string in specified
    // order
    function longestSubsequence(str, subList, index)
    {

        // If we have reached the end of the
        // string, return the subsequence
        // if it is valid, else return an
        // empty list
        let len = str.length;

        if (index >= len)
        {
            if (isValidSequence(subList))
                return subList;
            else
                return "";
        }

        // If there is no vowel in the
        // subsequence yet, add vowel
        // at current index if it is 'a',
        // else move on to the next character
        // in the string
        else if (subList.length == 0)
       {
           if (str[index] != 'a')
             return longestSubsequence(str, "", index + 1);
           else
             return longestSubsequence(str, subList + str[index], index + 1);
       }

        //  If the last vowel in the subsequence
        // until now is same as the vowel at
        // current index, add it to the subsequence
        else if (mapping[subList[subList.length - 1]] == mapping[str[index]])
            return longestSubsequence(str, subList+str[index], index + 1);

        // If the vowel at the current index comes
        // right after the last vowel in the
        // subsequence, we have two options:
        // either to add the vowel in the
        // subsequence, or move on to next character.
        // We choose the one which gives the longest
        // subsequence.
        else if (mapping[subList[subList.length - 1]] + 1 == mapping[str[index]])
        {
            let sub1 = longestSubsequence(
                str, subList + str[index], index + 1);
            let sub2 = longestSubsequence(
                str, subList, index + 1);

            if (sub1.length > sub2.length)
                return sub1;
            else
                return sub2;
        }  
        else
            return longestSubsequence(str, subList, index + 1);   
    }

    let str= "aeiaaioooauuaeiou";

    let subsequence = longestSubsequence(str, "", 0);

    if (subsequence.length == 0)
        document.write("No subsequence possible");
    else
    {
        document.write("[")
        for(let i = 0; i < subsequence.length - 1; i++)
        {
            document.write("'" + subsequence[i] + "'" + ", ");
        }
        document.write("'" + subsequence[subsequence.length-1] + "'" + "]");
    }

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
['a', 'e', 'i', 'i', 'o', 'o', 'o', 'u', 'u', 'u']
```

**方法 2(动态规划)**

## 蟒蛇 3

```
from random import choice

def longest_subsequence(string):
    def helper(chosen="", i=0):
        if i == len(string):
            return chosen if set("aeiou").issubset(set(chosen)) else ""

        hashable = (chosen[-1] if chosen else None, len(chosen), i)

        if hashable in memo:
            return memo[hashable]

        if not chosen:
            res = helper("a" if string[i] == "a" else chosen, i + 1)
        elif chosen[-1] == string[i]:
            res = helper(chosen + string[i], i + 1)
        elif mapping[chosen[-1]] + 1 == mapping[string[i]]:
            sub1 = helper(chosen + string[i], i + 1)
            sub2 = helper(chosen, i + 1)

            res = sub1 if len(sub1) > len(sub2) else sub2
        else:
            res = helper(chosen, i + 1)

        memo[hashable] = res
        return res

    mapping = {x: i for i, x in enumerate("aeiou")}
    memo = {}
    return helper()

if __name__ == "__main__":
    tests = [
        "aeiaaioooaauuaeiou",
        "aaauuiieeou",
        "".join(choice("aeiou") for _ in range(40)),
        "".join(choice("aeiou") for _ in range(900))
    ]

    for string in tests:
        print("original:", string)
        subsequence = longest_subsequence(string)

        if subsequence:
            print("\nmax subsequence:", "".join(subsequence))
        else:
            print("No subsequence possible")

        print("-" * 40, "\n")
```

**Output:** 

```
original: aeiaaioooaauuaeiou

max subsequence: aaaaaaeiou
---------------------------------------- 

original: aaauuiieeou
No subsequence possible
---------------------------------------- 

original: auaaioeoiaooaauoeuaueouuoeiiooiiaiiuioio

max subsequence: aaaaaaeeeiioou
---------------------------------------- 

original: eaaioeaieoaiueiuiaeiuueeueouoiuueeuaooooiuaiaeuaaieiauaiauuieaoeeeieeoiuaiuuuaaoieooooeioeiouuaoeaouooiauiuiioaoeeeuaoeooiueoaiuioeaeaaouiiiauiuuauoiaiaauaeooeuaiuoeeaaeoaiaoiueieeuaioieouuaaiieeaaeiioaoieoauieoueoauaieueoaeiaoaeoeuiaiauuauouoouaeaueeeioauaieiaieoaeiiueuaaoeuoiueaaiaiaouoouueoauoeieaioeeuueiaaoaiaiiaiueuauaeaieuioooiaeooeaueeoueiueeaueuuiaeuoiuiaeioeeuoaiuueuiaaueueuaeoueuaiaiiuiaouoiueuuueeaueeoaiaaouuiioeioeiaaiieaieiiieeeiaaoaeoououaooiioieuoaeaueuoeaueaoaieeeeauouaaaeiiuoiiuieuuoouuaaoiuaiaoaeeeeiauuuuoiuuoeiieuoaeaouaaooiuuuaeaeaeioeuuauaeaioiuuueuuiuieoieooeoiuioeouuuuaooeueaiooaeiieeieuauoeoaieaeiaaeeoiieiaeuouuuuououiuaueoeooaaeeuuiiaiiueoueaaauaiaieiuiiieauaaioauiuoiiiaieeuaieieiuooeaeooooeouioaooieooeaaaeeeuouiiooiaiieeeuoieeuueouiuuoioeeoiuaauuaaeaueeeiuuuueeeaaeuuoeeeuuieeueeuiaeioeaoiiiiauuoeieeioooaoaeueouiaoeouioaueoaioiuoieuoueuiuouiuaiiaeiuueaiaeuaaeouoa

max subsequence: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeiiiiiiiiiiiiiiiiiiiooooooooooooooouuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuuu
----------------------------------------
```
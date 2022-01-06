# 按顺序删除连续的相同单词

> 原文:[https://www . geesforgeks . org/delete-continuous-word-sequence/](https://www.geeksforgeeks.org/delete-consecutive-words-sequence/)

给定一个由 n 个字符串组成的序列，任务是检查任何两个相似的单词是否在一起，然后它们相互销毁，然后打印两两销毁后序列中剩余的单词数。
**例:**

```
Input : ab aa aa bcd ab
Output : 3
As aa, aa destroys each other so, ab bcd ab is the
new sequence.

Input :  tom jerry jerry tom
Output : 0
As first both jerry will destroy each other.
Then sequence will be tom, tom they will also destroy
each other. So, the final sequence doesn't contain any
word.
```

**方法 1:**

```
1- Start traversing the sequence by storing it in vector.
  a) Check if the current string is equal to next string
     if yes, erase both from the vector.
  b) And check the same till last.
2- Return vector size.
```

## C++

```
// C++ program to remove consecutive same words
#include<bits/stdc++.h>
using namespace std;

// Function to find the size of manipulated sequence
int removeConsecutiveSame(vector <string > v)
{
    int n = v.size();

    // Start traversing the sequence
    for (int i=0; i<n-1; )
    {
        // Compare the current string with next one
        // Erase both if equal
        if (v[i].compare(v[i+1]) == 0)
        {
            // Erase function delete the element and
            // also shifts other element that's why
            // i is not updated
            v.erase(v.begin()+i);
            v.erase(v.begin()+i);

            // Update i, as to check from previous
            // element again
            if (i > 0)
                i--;

            // Reduce sequence size
            n = n-2;
        }

        // Increment i, if not equal
        else
            i++;
    }

    // Return modified size
    return v.size();
}

// Driver code
int main()
{
    vector<string> v = { "tom", "jerry", "jerry", "tom"};
    cout << removeConsecutiveSame(v);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove consecutive same words

import java.util.Vector;

class Test
{
    // Method to find the size of manipulated sequence
    static int removeConsecutiveSame(Vector <String > v)
    {
        int n = v.size();

        // Start traversing the sequence
        for (int i=0; i<n-1; )
        {
            // Compare the current string with next one
            // Erase both if equal
            if (v.get(i).equals(v.get(i+1)))
            {
                // Erase function delete the element and
                // also shifts other element that's why
                // i is not updated
                v.remove(i);
                v.remove(i);

                // Update i, as to check from previous
                // element again
                if (i > 0)
                    i--;

                // Reduce sequence size
                n = n-2;
            }

            // Increment i, if not equal
            else
                i++;
        }

        // Return modified size
        return v.size();
    }

    // Driver method
    public static void main(String[] args)
    {
        Vector<String> v = new Vector<>();

        v.addElement("tom"); v.addElement("jerry");
        v.addElement("jerry");v.addElement("tom");

        System.out.println(removeConsecutiveSame(v));
    }
}
```

## 蟒蛇 3

```
# Python3 program to remove consecutive
# same words

# Function to find the size of
# manipulated sequence
def removeConsecutiveSame(v):

    n = len(v)

    # Start traversing the sequence
    i = 0
    while(i < n - 1):

        # Compare the current string with
        # next one Erase both if equal
        if ((i + 1) < len(v)) and (v[i] == v[i + 1]):

            # Erase function delete the element and
            # also shifts other element that's why
            # i is not updated
            v = v[:i]
            v = v[:i]

            # Update i, as to check from previous
            # element again
            if (i > 0):
                i -= 1

            # Reduce sequence size
            n = n - 2

        # Increment i, if not equal
        else:
            i += 1

    # Return modified size
    return len(v[:i - 1])

# Driver Code
if __name__ == '__main__':
    v = ["tom", "jerry", "jerry", "tom"]
    print(removeConsecutiveSame(v))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to remove consecutive same words
using System;
using System.Collections.Generic;

class GFG
{
// Method to find the size of
// manipulated sequence
public static int removeConsecutiveSame(List<string> v)
{
    int n = v.Count;

    // Start traversing the sequence
    for (int i = 0; i < n - 1;)
    {
        // Compare the current string with
        // next one Erase both if equal
        if (v[i].Equals(v[i + 1]))
        {
            // Erase function delete the element and
            // also shifts other element that's why
            // i is not updated
            v.RemoveAt(i);
            v.RemoveAt(i);

            // Update i, as to check from
            // previous element again
            if (i > 0)
            {
                i--;
            }

            // Reduce sequence size
            n = n - 2;
        }

        // Increment i, if not equal
        else
        {
            i++;
        }
    }

    // Return modified size
    return v.Count;
}

// Driver Code
public static void Main(string[] args)
{
    List<string> v = new List<string>();

    v.Add("tom");
    v.Add("jerry");
    v.Add("jerry");
    v.Add("tom");

    Console.WriteLine(removeConsecutiveSame(v));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// Javascript program to remove consecutive same words

// Method to find the size of
// manipulated sequence
function removeConsecutiveSame(v)
{
    let n = v.length;

    // Start traversing the sequence
    for (let i = 0; i < n - 1;)
    {

        // Compare the current string with
        // next one Erase both if equal
        if (v[i] == (v[i + 1]))
        {

            // Erase function delete the element and
            // also shifts other element that's why
            // i is not updated
            v.splice(i, 1);
            v.splice(i, 1);

            // Update i, as to check from
            // previous element again
            if (i > 0) {
                i--;
            }

            // Reduce sequence size
            n = n - 2;
        }

        // Increment i, if not equal
        else {
            i++;
        }
    }

    // Return modified size
    return v.length;
}

// Driver Code

let v = [];

v.push("tom");
v.push("jerry");
v.push("jerry");
v.push("tom");

document.write(removeConsecutiveSame(v));

// This code is contributed by gfgking
</script>
```

**输出:**

```
0
```

**方法二:(使用叠加)**

```
1- Start traversing the strings and push into stack.
    a) Check if the current string is same as the string
       at the top of the stack
        i) If yes, pop the string from top.
        ii) Else push the current string.
2- Return stack size if the whole sequence is traversed.
```

## C++

```
//  C++ implementation of above method
#include<bits/stdc++.h>
using namespace std;

// Function to find the size of manipulated sequence
int removeConsecutiveSame(vector <string> v)
{
    stack<string> st;

    // Start traversing the sequence
    for (int i=0; i<v.size(); i++)
    {
        // Push the current string if the stack
        // is empty
        if (st.empty())
            st.push(v[i]);
        else
        {
            string str = st.top();

            // compare the current string with stack top
            // if equal, pop the top
            if (str.compare(v[i]) == 0)
                st.pop();

            // Otherwise push the current string
            else
                st.push(v[i]);
        }
    }

    // Return stack size
    return st.size();
}

// Driver code
int main()
{
    vector<string> V = { "ab", "aa", "aa", "bcd", "ab"};
    cout << removeConsecutiveSame(V);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java implementation of above method

import java.util.Stack;
import java.util.Vector;

class Test
{
    // Method to find the size of manipulated sequence
    static int removeConsecutiveSame(Vector <String> v)
    {
        Stack<String> st = new Stack<>();

        // Start traversing the sequence
        for (int i=0; i<v.size(); i++)
        {
            // Push the current string if the stack
            // is empty
            if (st.empty())
                st.push(v.get(i));
            else
            {
                String str = st.peek();

                // compare the current string with stack top
                // if equal, pop the top
                if (str.equals(v.get(i)))   
                    st.pop();

                // Otherwise push the current string
                else
                    st.push(v.get(i));
            }
        }

        // Return stack size
        return st.size();
    }

    // Driver method
    public static void main(String[] args)
    {
        Vector<String> v = new Vector<>();

        v.addElement("ab"); v.addElement("aa");
        v.addElement("aa");v.addElement("bcd");
        v.addElement("ab");

        System.out.println(removeConsecutiveSame(v));
    }
}
```

## 蟒蛇 3

```
# Python implementation of above method

# Function to find the size of manipulated sequence
def removeConsecutiveSame(v):
    st = []

    # Start traversing the sequence
    for i in range(len(v)):

        # Push the current string if the stack
        # is empty
        if (len(st) == 0):
            st.append(v[i])
        else:
            Str = st[-1]

            # compare the current string with stack top
            # if equal, pop the top
            if (Str == v[i]):
                st.pop()

            # Otherwise push the current string
            else:
                st.append(v[i])

    # Return stack size
    return len(st)

# Driver code
if __name__ == '__main__':
    V = [ "ab", "aa", "aa", "bcd", "ab"]
    print(removeConsecutiveSame(V))

# This code is contributed by PranchalK.
```

## C#

```
// C# implementation of above method
using System;
using System.Collections.Generic;

class GFG
{
// Method to find the size of
// manipulated sequence
public static int removeConsecutiveSame(List<string> v)
{
    Stack<string> st = new Stack<string>();

    // Start traversing the sequence
    for (int i = 0; i < v.Count; i++)
    {
        // Push the current string if
        // the stack is empty
        if (st.Count == 0)
        {
            st.Push(v[i]);
        }
        else
        {
            string str = st.Peek();

            // compare the current string with 
            // stack top if equal, pop the top
            if (str.Equals(v[i]))
            {
                st.Pop();
            }

            // Otherwise push the current
            // string
            else
            {
                st.Push(v[i]);
            }
        }
    }

    // Return stack size
    return st.Count;
}

// Driver Code
public static void Main(string[] args)
{
    List<string> v = new List<string>();

    v.Add("ab");
    v.Add("aa");
    v.Add("aa");
    v.Add("bcd");
    v.Add("ab");

    Console.WriteLine(removeConsecutiveSame(v));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript implementation of above method

    // Method to find the size of
    // manipulated sequence
    function removeConsecutiveSame(v)
    {
        let st = [];

        // Start traversing the sequence
        for (let i = 0; i < v.length; i++)
        {
            // Push the current string if
            // the stack is empty
            if (st.length == 0)
            {
                st.push(v[i]);
            }
            else
            {
                let str = st[st.length - 1];

                // compare the current string with
                // stack top if equal, pop the top
                if (str == v[i])
                {
                    st.pop();
                }

                // Otherwise push the current
                // string
                else
                {
                    st.push(v[i]);
                }
            }
        }

        // Return stack size
        return st.length;
    }

    let v = [];

    v.push("ab");
    v.push("aa");
    v.push("aa");
    v.push("bcd");
    v.push("ab");

    document.write(removeConsecutiveSame(v));

// This code is contributed by decode2207.
</script>
```

**输出:**

```
3
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
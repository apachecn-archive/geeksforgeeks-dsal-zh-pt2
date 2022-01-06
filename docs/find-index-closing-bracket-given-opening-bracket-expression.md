# 在表达式

中找到给定左括号的右括号索引

> 原文:[https://www . geesforgeks . org/find-index-closing-括号-given-open-括号-expression/](https://www.geeksforgeeks.org/find-index-closing-bracket-given-opening-bracket-expression/)

给定一个带括号的字符串。如果给定了开括号的起始索引，则找到闭括号的索引。

示例:

```
Input : string = [ABC[23]][89]
        index = 0
Output : 8
The opening bracket at index 0 corresponds
to closing bracket at index 8.

```

思路是使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)。我们遍历给定索引中的给定表达式，并继续推进起始括号。每当我们遇到一个结束括号，我们弹出一个开始括号。如果堆栈在任何时候变成空的，我们就返回那个索引。

## C++

```
// CPP program to find index of closing
// bracket for given opening bracket.
#include <bits/stdc++.h>
using namespace std;

// Function to find index of closing
// bracket for given opening bracket.
void test(string expression, int index){
    int i;

    // If index given is invalid and is 
    // not an opening bracket.
    if(expression[index]!='['){
        cout << expression << ", " <<
                    index << ": -1\n";
        return;
    }

    // Stack to store opening brackets.
    stack <int> st;

    // Traverse through string starting from
    // given index.
    for(i = index; i < expression.length(); i++){

        // If current character is an 
        // opening bracket push it in stack.
        if(expression[i] == '[')
          st.push(expression[i]);

        // If current character is a closing
        // bracket, pop from stack. If stack 
        // is empty, then this closing
        // bracket is required bracket.
        else if(expression[i] == ']'){
            st.pop();
            if(st.empty()){
                cout << expression << ", " << 
                       index << ": " << i << "\n";
                return;
            }
        }
    }

    // If no matching closing bracket
    // is found.
    cout << expression << ", " <<
                index << ": -1\n";
}

// Driver Code
int main() {
    test("[ABC[23]][89]", 0); // should be 8
    test("[ABC[23]][89]", 4); // should be 7
    test("[ABC[23]][89]", 9); // should be 12
    test("[ABC[23]][89]", 1); // No matching bracket
    return 0;
}

// This code is contributed by Nikhil Jindal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find index of closing 
// bracket for given opening bracket. 
import java.util.Stack;
class GFG {

// Function to find index of closing 
// bracket for given opening bracket. 
    static void test(String expression, int index) {
        int i;

        // If index given is invalid and is 
        // not an opening bracket. 
        if (expression.charAt(index) != '[') {
            System.out.print(expression + ", "
                    + index + ": -1\n");
            return;
        }

        // Stack to store opening brackets. 
        Stack<Integer> st = new Stack<>();

        // Traverse through string starting from 
        // given index. 
        for (i = index; i < expression.length(); i++) {

            // If current character is an 
            // opening bracket push it in stack. 
            if (expression.charAt(i) == '[') {
                st.push((int) expression.charAt(i));
            } // If current character is a closing 
            // bracket, pop from stack. If stack 
            // is empty, then this closing 
            // bracket is required bracket. 
            else if (expression.charAt(i) == ']') {
                st.pop();
                if (st.empty()) {
                    System.out.print(expression + ", "
                            + index + ": " + i + "\n");
                    return;
                }
            }
        }

        // If no matching closing bracket 
        // is found. 
        System.out.print(expression + ", "
                + index + ": -1\n");
    }

// Driver Code 
    public static void main(String[] args) {
        test("[ABC[23]][89]", 0); // should be 8 
        test("[ABC[23]][89]", 4); // should be 7 
        test("[ABC[23]][89]", 9); // should be 12 
        test("[ABC[23]][89]", 1); // No matching bracket 
    }
// this code is contributed by Rajput-Ji
}
```

## 计算机编程语言

```
# Python program to find index of closing
# bracket for a given opening bracket.
from collections import deque

def getIndex(s, i):

    # If input is invalid.
    if s[i] != '[':
        return -1

    # Create a deque to use it as a stack.
    d = deque()

    # Traverse through all elements
    # starting from i.
    for k in range(i, len(s)):

        # Pop a starting bracket
        # for every closing bracket
        if s[k] == ']':
            d.popleft()

        # Push all starting brackets
        elif s[k] == '[':
            d.append(s[i])

        # If deque becomes empty
        if not d:
            return k

    return -1

# Driver code to test above method.
def test(s, i):
    matching_index = getIndex(s, i)
    print(s + ", " + str(i) + ": " + str(matching_index))

def main():
    test("[ABC[23]][89]", 0) # should be 8
    test("[ABC[23]][89]", 4) # should be 7
    test("[ABC[23]][89]", 9) # should be 12
    test("[ABC[23]][89]", 1) # No matching bracket

if __name__ == "__main__":
    main()
```

## C#

```
// C# program to find index of closing 
// bracket for given opening bracket. 
using System;
using System.Collections;
public class GFG { 

// Function to find index of closing 
// bracket for given opening bracket. 
    static void test(String expression, int index) { 
        int i; 

        // If index given is invalid and is 
        // not an opening bracket. 
        if (expression[index] != '[') { 
            Console.Write(expression + ", "
                    + index + ": -1\n"); 
            return; 
        } 

        // Stack to store opening brackets. 
        Stack st = new Stack(); 

        // Traverse through string starting from 
        // given index. 
        for (i = index; i < expression.Length; i++) { 

            // If current character is an 
            // opening bracket push it in stack. 
            if (expression[i] == '[') { 
                st.Push((int) expression[i]); 
            } // If current character is a closing 
            // bracket, pop from stack. If stack 
            // is empty, then this closing 
            // bracket is required bracket. 
            else if (expression[i] == ']') { 
                st.Pop(); 
                if (st.Count==0) { 
                    Console.Write(expression + ", "
                            + index + ": " + i + "\n"); 
                    return; 
                } 
            } 
        } 

        // If no matching closing bracket 
        // is found. 
        Console.Write(expression + ", "
                + index + ": -1\n"); 
    } 

// Driver Code 
    public static void Main() { 
        test("[ABC[23]][89]", 0); // should be 8 
        test("[ABC[23]][89]", 4); // should be 7 
        test("[ABC[23]][89]", 9); // should be 12 
        test("[ABC[23]][89]", 1); // No matching bracket 
    } 
} 

// This code is contributed by 29AjayKumar

```

**输出:**

```
[ABC[23]][89], 0: 8
[ABC[23]][89], 4: 7
[ABC[23]][89], 9: 12
[ABC[23]][89], 1: -1

```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
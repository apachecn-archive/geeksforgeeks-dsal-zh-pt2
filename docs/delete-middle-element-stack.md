# 删除堆栈的中间元素

> 原文:[https://www.geeksforgeeks.org/delete-middle-element-stack/](https://www.geeksforgeeks.org/delete-middle-element-stack/)

给定一个带有 push()、pop()、empty()操作的堆栈，在不使用任何额外数据结构的情况下删除它的中间部分。

```
Input  : Stack[] = [1, 2, 3, 4, 5]
Output : Stack[] = [1, 2, 4, 5]

Input  : Stack[] = [1, 2, 3, 4, 5, 6]
Output : Stack[] = [1, 2, 4, 5, 6]
```

想法是使用递归调用。我们首先一个一个地移除所有项目，然后我们重复。在递归调用之后，我们将除中间项之外的所有项推回。

## C++

```
// C++ code to delete middle of a stack
// without using additional data structure.
#include<bits/stdc++.h>
using namespace std;

// Deletes middle of stack of size
// n. Curr is current item number
void deleteMid(stack<char> &st, int n,
                          int curr=0)
{
   // If stack is empty or all items
   // are traversed
   if (st.empty() || curr == n)
     return;

   // Remove current item
   char x = st.top();
   st.pop();

   // Remove other items
   deleteMid(st, n, curr+1);

   // Put all items back except middle
   if (curr != n/2)
     st.push(x);
}

//Driver function to test above functions
int main()
{
    stack<char> st;

    //push elements into the stack
    st.push('1');
    st.push('2');
    st.push('3');
    st.push('4');
    st.push('5');
    st.push('6');
    st.push('7');

    deleteMid(st, st.size());

    // Printing stack after deletion
    // of middle.
    while (!st.empty())
    {
        char p=st.top();
        st.pop();
        cout << p << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to delete middle of a stack
// without using additional data structure.
import java.io.*;
import java.util.*;

public class GFG {

    // Deletes middle of stack of size
    // n. Curr is current item number
    static void deleteMid(Stack<Character> st,
                              int n, int curr)
    {

        // If stack is empty or all items
        // are traversed
        if (st.empty() || curr == n)
            return;

        // Remove current item
        char x = st.pop();

        // Remove other items
        deleteMid(st, n, curr+1);

        // Put all items back except middle
        if (curr != n/2)
            st.push(x);
    }

    // Driver function to test above functions
    public static void main(String args[])
    {
        Stack<Character> st =
                  new Stack<Character>();

        // push elements into the stack
        st.push('1');
        st.push('2');
        st.push('3');
        st.push('4');
        st.push('5');
        st.push('6');
        st.push('7');

        deleteMid(st, st.size(), 0);

        // Printing stack after deletion
        // of middle.
        while (!st.empty())
        {
            char p=st.pop();
            System.out.print(p + " ");
        }
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python3 code to delete middle of a stack
# without using additional data structure.

# Deletes middle of stack of size
# n. Curr is current item number
class Stack:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()

    def peek(self):
        return self.items[len(self.items)-1]

    def size(self):
        return len(self.items)

def deleteMid(st, n, curr) :

    # If stack is empty or all items
    # are traversed
    if (st.isEmpty() or curr == n) :
        return

    # Remove current item
    x = st.peek()
    st.pop()

    # Remove other items
    deleteMid(st, n, curr+1)

    # Put all items back except middle
    if (curr != int(n/2)) :
        st.push(x)

# Driver function to test above functions
st = Stack()

# push elements into the stack
st.push('1')
st.push('2')
st.push('3')
st.push('4')
st.push('5')
st.push('6')
st.push('7')

deleteMid(st, st.size(), 0)

# Printing stack after deletion
# of middle.
while (st.isEmpty() == False) :
    p = st.peek()
    st.pop()
    print (str(p) + " ", end="")

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# code to delete middle of a stack
// without using additional data structure.
using System;
using System.Collections.Generic;

class GFG {

    // Deletes middle of stack of size
    // n. Curr is current item number
    static void deleteMid(Stack<char> st,
                          int n,
                          int curr = 0)
    {

        // If stack is empty or all
        // items are traversed
        if (st.Count == 0 || curr == n)
            return;

        // Remove current item
        char x = st.Peek();
        st.Pop();

        // Remove other items
        deleteMid(st, n, curr+1);

        // Put all items
        // back except middle
        if (curr != n / 2)
            st.Push(x);
    }

    // Driver Code
    public static void Main()
    {
        Stack<char> st = new Stack<char>();

        // push elements into the stack
        st.Push('1');
        st.Push('2');
        st.Push('3');
        st.Push('4');
        st.Push('5');
        st.Push('6');
        st.Push('7');

        deleteMid(st, st.Count);

        // Printing stack after
        // deletion of middle.
        while (st.Count != 0)
        {
            char p=st.Peek();
            st.Pop();
            Console.Write(p + " ");
        }
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## java 描述语言

```
<script>
    // Javascript code to delete middle of a stack
    // without using additional data structure.

    // Deletes middle of stack of size
    // n. Curr is current item number
    function deleteMid(st, n, curr)
    {

        // If stack is empty or all items
        // are traversed
        if (st.length == 0 || curr == n)
            return;

        // Remove current item
        let x = st[st.length - 1];
        st.pop();

        // Remove other items
        deleteMid(st, n, curr+1);

        // Put all items back except middle
        if (curr != parseInt(n/2, 10))
            st.push(x);
    }

    let st = [];

    // push elements into the stack
    st.push('1');
    st.push('2');
    st.push('3');
    st.push('4');
    st.push('5');
    st.push('6');
    st.push('7');

    deleteMid(st, st.length, 0);

    // Printing stack after deletion
    // of middle.
    while (st.length > 0)
    {
      let p = st[st.length - 1];
      st.pop();
      document.write(p + " ");
    }

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
7 6 5 3 2 1 
```
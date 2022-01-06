# 从堆栈中删除所有偶数元素

> 原文:[https://www . geesforgeks . org/delete-all-even-elements-from-a-stack/](https://www.geeksforgeeks.org/delete-all-even-elements-from-a-stack/)

给定一个具有 **n 个**元素的堆栈，任务是在不影响元素顺序的情况下移除堆栈中的所有元素。
**例:**

> **输入:**s = 16<-15<-29<-24<-19(TOP)
> **输出:** 19 29 15
> 19 29 15 是奇数元素的顺序，它们将从给定的堆栈中弹出
> 。
> **输入:**s = 1<-2<-3<-4<-5(TOP)
> **输出:** 5 3 1

**进场:**

1.  创建一个临时堆栈 **temp** 并开始弹出给定堆栈的元素**。**
2.  **对于每个弹出的元素，说出**值**，如果**值% 2 == 1** ，则将其推至**温度**。**
3.  **在第 2 步结束时， **temp** 将包含来自 **s** 的所有奇数元素，但顺序相反。**
4.  **现在，要获得原始订单，从 **temp** 弹出每个元素，并将其推送到 **s** 。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <stack>
#include <iostream>
#include <stdio.h>

using namespace std;

// Utility function to print
// the contents of a stack
static void printStack(stack<int> s)
{
    while (!s.empty())
    {
        cout << s.top() << " ";
        s.pop();
    }
}

// Function to delete all even
// elements from the stack
static void deleteEven(stack<int> s)
{
    stack<int> temp;
    // While stack is not empty
    while (!s.empty())
    {
        int val = s.top();
        s.pop();

        // If value is odd then push
        // it to the temporary stack
        if (val % 2 == 1)
            temp.push(val);
    }

    // Transfer the contents of the temporary stack
    // to the original stack in order to get
    // the original order of the elements
    while (!temp.empty())
    {
        s.push(temp.top());
        temp.pop();
    }

    // Print the modified stack content
    printStack(s);
}

// Driver Code
int main()
{
    stack<int> s;
    s.push(16);
    s.push(15);
    s.push(29);
    s.push(24);
    s.push(19);
    deleteEven(s);
    return 0;
}

// This code is contributed by Vivekkumar Singh
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.Stack;
class GFG {

    // Utility function to print
    // the contents of a stack
    static void printStack(Stack<Integer> stack)
    {
        while (!stack.isEmpty())
            System.out.print(stack.pop() + " ");
    }

    // Function to delete all even
    // elements from the stack
    static void deleteEven(Stack<Integer> stack)
    {
        Stack<Integer> temp = new Stack<>();

        // While stack is not empty
        while (!stack.isEmpty()) {
            int val = stack.pop();

            // If value is odd then push
            // it to the temporary stack
            if (val % 2 == 1)
                temp.push(val);
        }

        // Transfer the contents of the temporary stack
        // to the original stack in order to get
        // the original order of the elements
        while (!temp.isEmpty())
            stack.push(temp.pop());

        // Print the modified stack content
        printStack(stack);
    }

    // Driver code
    public static void main(String[] args)
    {
        Stack<Integer> stack = new Stack<>();
        stack.push(16);
        stack.push(15);
        stack.push(29);
        stack.push(24);
        stack.push(19);

        deleteEven(stack);
    }
}
```

## **蟒蛇 3**

```
# Python implementation of the approach

# Utility function to print
# the contents of a stack
def printStack(s):
    while (len(s)!=0):
        print(s.pop(),end=" ")

# Function to delete all even
# elements from the stack
def deleteEven(s):
    temp = []

    # While stack is not empty
    while (len(s)!=0):
        val=s.pop()

        # If value is odd then push
        # it to the temporary stack
        if (val % 2 == 1):
            temp.append(val)

    # Transfer the contents of the temporary stack
    # to the original stack in order to get
    # the original order of the elements
    while (len(temp)!=0):
        s.append(temp.pop())

    # Print the modified stack content
    printStack(s);

# Driver Code
s = []
s.append(16)
s.append(15)
s.append(29)
s.append(24)
s.append(19)
deleteEven(s)

# This code is contributed by rag2127.
```

## **C#**

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Utility function to print
    // the contents of a stack
    static void printStack(Stack<int> stack)
    {
        while (stack.Count != 0)
            Console.Write(stack.Pop() + " ");
    }

    // Function to delete all even
    // elements from the stack
    static void deleteEven(Stack<int> stack)
    {
        Stack<int> temp = new Stack<int>();

        // While stack is not empty
        while (stack.Count != 0)
        {
            int val = stack.Pop();

            // If value is odd then push
            // it to the temporary stack
            if (val % 2 == 1)
                temp.Push(val);
        }

        // Transfer the contents of the temporary stack
        // to the original stack in order to get
        // the original order of the elements
        while (temp.Count != 0)
            stack.Push(temp.Pop());

        // Print the modified stack content
        printStack(stack);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Stack<int> stack = new Stack<int>();
        stack.Push(16);
        stack.Push(15);
        stack.Push(29);
        stack.Push(24);
        stack.Push(19);

        deleteEven(stack);
    }
}

// This code has been contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// JavaScript implementation of the approach

// Utility function to print
// the contents of a stack
function printStack(s)
{
    while (s.length!=0)
    {
        document.write( s[s.length-1] + " ");
        s.pop();
    }
}

// Function to delete all even
// elements from the stack
function deleteEven(s)
{
    var temp = [];
    // While stack is not empty
    while (s.length!=0)
    {
        var val = s[s.length-1];
        s.pop();

        // If value is odd then push
        // it to the temporary stack
        if (val % 2 == 1)
            temp.push(val);
    }

    // Transfer the contents of the temporary stack
    // to the original stack in order to get
    // the original order of the elements
    while (temp.length!=0)
    {
        s.push(temp[temp.length-1]);
        temp.pop();
    }

    // Print the modified stack content
    printStack(s);
}

// Driver Code
var s = [];
s.push(16);
s.push(15);
s.push(29);
s.push(24);
s.push(19);
deleteEven(s);

</script>
```

****Output:** 

```
19 29 15
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(N)**
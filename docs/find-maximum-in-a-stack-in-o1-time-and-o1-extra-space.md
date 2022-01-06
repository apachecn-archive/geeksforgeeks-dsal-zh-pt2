# 在 O(1)时间和 O(1)额外空间中找到堆栈中的最大值

> 原文:[https://www . geeksforgeeks . org/find-最大堆内堆外空间时间和堆外空间时间/](https://www.geeksforgeeks.org/find-maximum-in-a-stack-in-o1-time-and-o1-extra-space/)

给定一堆整数。任务是设计一个特殊的堆栈，以便在 O(1)时间和 O(1)额外空间中找到最大元素。
**例** :

```
Given Stack :
2
5
1
64   --> Maximum

So Output must be 64 when getMax() is called.
```

下面是设计用于从堆栈中推送和弹出元素的不同功能。
**推(x)** :在栈顶插入 x。

*   如果堆栈为空，则将 x 插入堆栈，并使 maxEle 等于 x。
*   如果堆栈不为空，将 x 与 maxEle 进行比较。出现了两种情况:
    *   如果 x 小于或等于 maxEle，只需插入 x。
    *   如果 x 大于 maxEle，将(2 * x–maxEle)插入堆栈，使 maxEle 等于 x。例如，假设以前的 MaxEle 为 3。现在我们要插入 4。我们将 maxEle 更新为 4，并将 2 * 4–3 = 5 插入堆栈。

**Pop() :** 从堆栈顶部移除元素。

*   从顶部移除元素。假设被移除的元素是 y。出现两种情况:
    *   如果 y 小于或等于 maxEle，堆栈中的最大元素仍然是 maxEle。
    *   如果 y 大于 maxEle，最大元素现在变成(2 * MaxEle–y)，所以更新(MaxEle = 2 * MaxEle–y)。这是我们从当前最大值中检索前一个最大值及其在堆栈中的值的地方。例如，让要移除的元素为 5，maxEle 为 4。我们删除 5，并将 maxEle 更新为 2 * 4–5 = 3。

**要点:**

*   如果一个元素的实际值到目前为止是最大的，那么堆栈就不保存它。
*   实际最大元素总是存储在 maxEle 中

**插图**

**推(x)**

*   要插入的数字:3，堆栈为空，所以在堆栈中插入 3，maxEle = 3。
*   要插入的数字:5，堆栈不为空，5> maxEle，将(2*5-3)插入堆栈，maxEle = 5。
*   要插入的数字:2，堆栈不为空，2< maxEle，将 2 插入堆栈，maxEle = 5。
*   要插入的数字:1，堆栈不为空，1< maxEle，在堆栈中插入 1，maxEle = 5。

**【pop()**

*   最初，堆栈中最大的元素 maxEle 是 5。
*   删除的数字:1，因为 1 小于 maxEle，所以只弹出 1。maxEle=5。
*   移除的数字:2，2
*   删除的数字:7，7> maxEle，原始数字是 maxEle，即 5，新的 MaxEle = 2 * 5–7 = 3。

## C++

```
// C++ program to implement a stack that supports
// getMaximum() in O(1) time and O(1) extra space.
#include <bits/stdc++.h>
using namespace std;

// A user defined stack that supports getMax() in
// addition to push() and pop()
struct MyStack {
    stack<int> s;
    int maxEle;

    // Prints maximum element of MyStack
    void getMax()
    {
        if (s.empty())
            cout << "Stack is empty\n";

        // variable maxEle stores the maximum element
        // in the stack.
        else
            cout << "Maximum Element in the stack is: "
                 << maxEle << "\n";
    }

    // Prints top element of MyStack
    void peek()
    {
        if (s.empty()) {
            cout << "Stack is empty ";
            return;
        }

        int t = s.top(); // Top element.

        cout << "Top Most Element is: ";

        // If t < maxEle means maxEle stores
        // value of t.
        (t > maxEle) ? cout << maxEle : cout << t;
    }

    // Remove the top element from MyStack
    void pop()
    {
        if (s.empty()) {
            cout << "Stack is empty\n";
            return;
        }

        cout << "Top Most Element Removed: ";
        int t = s.top();
        s.pop();

        // Maximum will change as the maximum element
        // of the stack is being removed.
        if (t > maxEle) {
            cout << maxEle << "\n";
            maxEle = 2 * maxEle - t;
        }

        else
            cout << t << "\n";
    }

    // Removes top element from MyStack
    void push(int x)
    {
        // Insert new number into the stack
        if (s.empty()) {
            maxEle = x;
            s.push(x);
            cout << "Number Inserted: " << x << "\n";
            return;
        }

        // If new number is less than maxEle
        if (x > maxEle) {
            s.push(2 * x - maxEle);
            maxEle = x;
        }

        else
            s.push(x);

        cout << "Number Inserted: " << x << "\n";
    }
};

// Driver Code
int main()
{
    MyStack s;
    s.push(3);
    s.push(5);
    s.getMax();
    s.push(7);
    s.push(19);
    s.getMax();
    s.pop();
    s.getMax();
    s.pop();
    s.peek();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement a stack that supports
// getMaximum() in O(1) time and O(1) extra space.
import java.util.*;

class GFG
{

// A user defined stack that supports getMax() in
// addition to push() and pop()
static class MyStack
{
    Stack<Integer> s = new Stack<Integer>();
    int maxEle;

    // Prints maximum element of MyStack
    void getMax()
    {
        if (s.empty())
            System.out.print("Stack is empty\n");

        // variable maxEle stores the maximum element
        // in the stack.
        else
            System.out.print("Maximum Element in" +
                        "the stack is: "+maxEle + "\n");

    }

    // Prints top element of MyStack
    void peek()
    {
        if (s.empty())
        {

            System.out.print("Stack is empty ");
            return;
        }

        int t = s.peek(); // Top element.

        System.out.print("Top Most Element is: ");

        // If t < maxEle means maxEle stores
        // value of t.
        if(t > maxEle)
            System.out.print(maxEle);
        else
            System.out.print(t);
    }

    // Remove the top element from MyStack
    void pop()
    {
        if (s.empty())
        {
            System.out.print("Stack is empty\n");
            return;
        }

        System.out.print("Top Most Element Removed: ");
        int t = s.peek();
        s.pop();

        // Maximum will change as the maximum element
        // of the stack is being removed.
        if (t > maxEle)
        {
            System.out.print(maxEle + "\n");
            maxEle = 2 * maxEle - t;
        }

        else
            System.out.print(t + "\n");
    }

    // Removes top element from MyStack
    void push(int x)
    {
        // Insert new number into the stack
        if (s.empty())
        {
            maxEle = x;
            s.push(x);
            System.out.print("Number Inserted: " + x + "\n");
            return;
        }

        // If new number is less than maxEle
        if (x > maxEle)
        {
            s.push(2 * x - maxEle);
            maxEle = x;
        }

        else
            s.push(x);

        System.out.print("Number Inserted: " + x + "\n");
    }
};

// Driver Code
public static void main(String[] args)
{
    MyStack s = new MyStack();
    s.push(3);
    s.push(5);
    s.getMax();
    s.push(7);
    s.push(19);
    s.getMax();
    s.pop();
    s.getMax();
    s.pop();
    s.peek();
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Class to make a Node
class Node:
    #Constructor which assign argument to nade's value
    def __init__(self, value):
        self.value = value
        self.next = None

    # This method returns the string representation of the object.
    def __str__(self):
        return "Node({})".format(self.value)

    #  __repr__ is same as __str__
    __repr__ = __str__

class Stack:
    # Stack Constructor initialise top of stack and counter.
    def __init__(self):
        self.top = None
        self.count = 0
        self.maximum = None

    #This method returns the string representation of the object (stack).
    def __str__(self):
        temp=self.top
        out=[]
        while temp:
            out.append(str(temp.value))
            temp=temp.next
        out='\n'.join(out)
        return ('Top {} \n\nStack :\n{}'.format(self.top,out))

    #  __repr__ is same as __str__
    __repr__=__str__

    #This method is used to get minimum element of stack
    def getMax(self):
        if self.top is None:
            return "Stack is empty"
        else:
            print("Maximum Element in the stack is: {}" .format(self.maximum))

    # Method to check if Stack is Empty or not
    def isEmpty(self):
        # If top equals to None then stack is empty
        if self.top == None:
            return True
        else:
        # If top not equal to None then stack is empty
            return False

    # This method returns length of stack      
    def __len__(self):
        self.count = 0
        tempNode = self.top
        while tempNode:
            tempNode = tempNode.next
            self.count+=1
        return self.count

    # This method returns top of stack      
    def peek(self):
        if self.top is None:
            print ("Stack is empty")
        else:   
            if self.top.value > self.maximum:
                print("Top Most Element is: {}" .format(self.maximum))
            else:
                print("Top Most Element is: {}" .format(self.top.value))

    #This method is used to add node to stack
    def push(self,value):
        if self.top is None:
            self.top = Node(value)
            self.maximum = value

        elif value > self.maximum :
            temp = (2 * value) - self.maximum
            new_node = Node(temp)
            new_node.next = self.top
            self.top = new_node
            self.maximum = value
        else:
            new_node = Node(value)
            new_node.next = self.top
            self.top = new_node
        print("Number Inserted: {}" .format(value))

    #This method is used to pop top of stack
    def pop(self):
        if self.top is None:
            print( "Stack is empty")
        else:
            removedNode = self.top.value
            self.top = self.top.next
            if removedNode > self.maximum:
                print ("Top Most Element Removed :{} " .format(self.maximum))
                self.maximum = ( ( 2 * self.maximum ) - removedNode )
            else:
                print ("Top Most Element Removed : {}" .format(removedNode))

 # Driver program to test above class 
stack = Stack()

stack.push(3)
stack.push(5)
stack.getMax()
stack.push(7)
stack.push(19)
stack.getMax()    
stack.pop()
stack.getMax()
stack.pop()
stack.peek()

# This code is contributed by Blinkii
```

## C#

```
// C# program to implement a stack that supports
// getMaximum() in O(1) time and O(1) extra space.
using System;
using System.Collections.Generic;

class GFG
{

// A user defined stack that supports getMax() in
// addition to push() and pop()
public class MyStack
{
    public Stack<int> s = new Stack<int>();
    public int maxEle;

    // Prints maximum element of MyStack
    public void getMax()
    {
        if (s.Count == 0)
            Console.Write("Stack is empty\n");

        // variable maxEle stores the maximum element
        // in the stack.
        else
            Console.Write("Maximum Element in" +
                        "the stack is: "+maxEle + "\n");

    }

    // Prints top element of MyStack
    public void peek()
    {
        if (s.Count == 0)
        {

            Console.Write("Stack is empty ");
            return;
        }

        int t = s.Peek(); // Top element.

        Console.Write("Top Most Element is: ");

        // If t < maxEle means maxEle stores
        // value of t.
        if(t > maxEle)
            Console.Write(maxEle);
        else
            Console.Write(t);
    }

    // Remove the top element from MyStack
    public void pop()
    {
        if (s.Count == 0)
        {
            Console.Write("Stack is empty\n");
            return;
        }

        Console.Write("Top Most Element Removed: ");
        int t = s.Peek();
        s.Pop();

        // Maximum will change as the maximum element
        // of the stack is being removed.
        if (t > maxEle)
        {
            Console.Write(maxEle + "\n");
            maxEle = 2 * maxEle - t;
        }

        else
            Console.Write(t + "\n");
    }

    // Removes top element from MyStack
    public void push(int x)
    {
        // Insert new number into the stack
        if (s.Count == 0)
        {
            maxEle = x;
            s.Push(x);
            Console.Write("Number Inserted: " + x + "\n");
            return;
        }

        // If new number is less than maxEle
        if (x > maxEle)
        {
            s.Push(2 * x - maxEle);
            maxEle = x;
        }

        else
            s.Push(x);

        Console.Write("Number Inserted: " + x + "\n");
    }
};

// Driver Code
public static void Main(String[] args)
{
    MyStack s = new MyStack();
    s.push(3);
    s.push(5);
    s.getMax();
    s.push(7);
    s.push(19);
    s.getMax();
    s.pop();
    s.getMax();
    s.pop();
    s.peek();
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program to implement a stack that supports
    // getMaximum() in O(1) time and O(1) extra space.

    let s = [];
    let maxEle;

    // Prints maximum element of MyStack
    function getMax()
    {
        if (s.length == 0)
            document.write("Stack is empty" + "</br>");

        // variable maxEle stores the maximum element
        // in the stack.
        else
            document.write("Maximum Element in " +
                        "the stack is: "+maxEle + "</br>");

    }

    // Prints top element of MyStack
    function peek()
    {
        if (s.length == 0)
        {

            document.write("Stack is empty ");
            return;
        }

        let t = s[s.length - 1]; // Top element.

        document.write("Top Most Element is: ");

        // If t < maxEle means maxEle stores
        // value of t.
        if(t > maxEle)
            document.write(maxEle);
        else
            document.write(t);
    }

    // Remove the top element from MyStack
    function pop()
    {
        if (s.length == 0)
        {
            document.write("Stack is empty" + "</br>");
            return;
        }

        document.write("Top Most Element Removed: ");
        let t = s[s.length - 1];
        s.pop();

        // Maximum will change as the maximum element
        // of the stack is being removed.
        if (t > maxEle)
        {
            document.write(maxEle + "</br>");
            maxEle = 2 * maxEle - t;
        }

        else
            document.write(t + "</br>");
    }

    // Removes top element from MyStack
    function push(x)
    {
        // Insert new number into the stack
        if (s.length == 0)
        {
            maxEle = x;
            s.push(x);
            document.write("Number Inserted: " + x + "</br>");
            return;
        }

        // If new number is less than maxEle
        if (x > maxEle)
        {
            s.push(2 * x - maxEle);
            maxEle = x;
        }

        else
            s.push(x);

        document.write("Number Inserted: " + x + "</br>");
    }

    push(3);
    push(5);
    getMax();
    push(7);
    push(19);
    getMax();
    pop();
    getMax();
    pop();
    peek();

    //  This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
Number Inserted: 3
Number Inserted: 5
Maximum Element in the stack is: 5
Number Inserted: 7
Number Inserted: 19
Maximum Element in the stack is: 19
Top Most Element Removed: 19
Maximum Element in the stack is: 7
Top Most Element Removed: 7
Top Most Element is: 5
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
# 设计一个栈来检索原始元素，返回 O(1)时间和 O(1)空间的最小元素

> 原文:[https://www . geesforgeks . org/design-a-stack-to-retrieve-original-elements-and-return-最小元素 in-o1-time-and-o1-space/](https://www.geeksforgeeks.org/design-a-stack-to-retrieve-original-elements-and-return-the-minimum-element-in-o1-time-and-o1-space/)

我们的任务是设计一个支持所有堆栈操作的数据结构特殊堆栈，如 **push()** 、 **pop()** 、 **isEmpty()** 、 **isFull()** 和一个应该从特殊堆栈返回最小元素的附加操作 **getMin(** )。SpecialStack 的所有这些操作都必须以时间复杂度 O(1)来执行。要实现 SpecialStack，应该只使用标准的 Stack 数据结构，而不要使用数组、列表等其他数据结构。
示例:

```
Consider the following Special-Stack
16  --> TOP
15
29
19
18

When getMin() is called it should return 15, which is the minimum 
element in the current stack. 

If we do pop two times on stack, the stack becomes
29  --> TOP
19
18

When getMin() is called, it should return 18 which is the minimum 
in the current stack.
```

这里讨论了一种使用 0(1)时间和 0(1)额外空间的**方法**。然而，在前一篇文章中，原始元素没有恢复。在任何给定的时间点都只返回最小元素。
在本文中，对之前的方法进行了修改，以便在 **pop()** 操作期间也可以检索原始元素。
**方法:**
考虑一个变量 **minimum** ，我们在其中存储栈中的最小元素。现在，如果我们从堆栈中弹出最小元素呢？我们如何将最小变量更新为下一个最小值？一种解决方案是按照排序顺序维护另一个堆栈，以便最小的元素总是在顶部。然而，这是一种 O(n)空间方法。
为了在 **O(1)** 空间中实现这一点，我们需要一种方法将一个元素的当前值和下一个最小值存储在同一个节点中。这可以通过应用简单的数学来实现:

```
new_value = 2*current_value - minimum
```

我们将这个新值而不是当前值推入堆栈。从新值中检索当前值和下一个最小值:

```
current_value = (new_value + minimum)/2
minimum = new_value - 2*current
```

当 **Push(x)** 操作完成后，我们遵循下面给出的算法:

> 1.  If the stack is empty
>     1.  Insert X into the stack
>     2.  Make the minimum value equal to X. 。
> 2.  If the stack is not empty
>     1.  If x is less than the minimum value
>         1.  Set temp equal to 2 * x- minimum.
>         2.  Set the minimum value equal to X.
>         3.  Set x equal to temp

当操作 **Pop(x)** 完成时，我们遵循下面给出的算法:

> 1.  If the stack is not empty
>     1.  Set x equal to the topmost element
>     2.  If x is less than the minimum value
>         1.  Set the minimum value equal to 2 * minimum value–x
>         2.  Set x equal to (x+ min) /2
>     3.  Return x

当调用 getMin()时，我们返回变量中存储的元素，*最小值* :

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to retrieve original elements of the
// from a Stack which returns the minimum element
// in O(1) time and O(1) space

class Stack {
    Node top;

    // Stores minimum element of the stack
    int minimum;

    // Function to push an element
    void push(Node node)
    {
        int current = node.getData();
        if (top == null) {
            top = node;
            minimum = current;
        }
        else {
            if (current < minimum) {
                node.setData(2 * current - minimum);
                minimum = current;
            }
            node.setNext(top);
            top = node;
        }
    }

    // Retrieves topmost element
    Node pop()
    {
        Node node = top;
        if (node != null) {
            int current = node.getData();
            if (current < minimum) {
                minimum = 2 * minimum - current;
                node.setData((current + minimum) / 2);
            }
            top = top.getNext();
        }
        return node;
    }

    // Retrieves topmost element without
    // popping it from the stack
    Node peek()
    {
        Node node = null;
        if (top != null) {
            node = new Node();
            int current = top.getData();
            node.setData(current < minimum ? minimum : current);
        }
        return node;
    }

    // Function to print all elements in the stack
    void printAll()
    {
        Node ptr = top;
        int min = minimum;
        if (ptr != null) { // if stack is not empty
            while (true) {
                int val = ptr.getData();
                if (val < min) {
                    min = 2 * min - val;
                    val = (val + min) / 2;
                }
                System.out.print(val + "  ");
                ptr = ptr.getNext();
                if (ptr == null)
                    break;
            }
            System.out.println();
        }
        else
            System.out.println("Empty!");
    }

    // Returns minimum of Stack
    int getMin()
    {
        return minimum;
    }

    boolean isEmpty()
    {
        return top == null;
    }
}

// Node class which contains data
// and pointer to next node
class Node {
    int data;
    Node next;
    Node()
    {
        data = -1;
        next = null;
    }

    Node(int d)
    {
        data = d;
        next = null;
    }

    void setData(int data)
    {
        this.data = data;
    }

    void setNext(Node next)
    {
        this.next = next;
    }

    Node getNext()
    {
        return next;
    }

    int getData()
    {
        return data;
    }
}

// Driver Code
public class Main {
    public static void main(String[] args)
    {
        // Create a new stack
        Stack stack = new Stack();
        Node node;

        // Push the element into the stack
        stack.push(new Node(5));
        stack.push(new Node(3));
        stack.push(new Node(4));

        // Calls the method to print the stack
        System.out.println("Elements in the stack are:");
        stack.printAll();

        // Print current minimum element if stack is
        // not empty
        System.out.println(stack.isEmpty() ? "\nEmpty Stack!" :
                                "\nMinimum: " + stack.getMin());

        // Push new elements into the stack
        stack.push(new Node(1));
        stack.push(new Node(2));

        // Printing the stack
        System.out.println("\nStack after adding new elements:");
        stack.printAll();

        // Print current minimum element if stack is
        // not empty
        System.out.println(stack.isEmpty() ? "\nEmpty Stack!" :
                                    "\nMinimum: " + stack.getMin());

        // Pop elements from the stack
        node = stack.pop();
        System.out.println("\nElement Popped: "
                        + (node == null ? "Empty!" : node.getData()));

        node = stack.pop();
        System.out.println("Element Popped: "
                        + (node == null ? "Empty!" : node.getData()));

        // Printing stack after popping elements
        System.out.println("\nStack after removing top two elements:");
        stack.printAll();

        // Printing current Minimum element in the stack
        System.out.println(stack.isEmpty() ? "\nEmpty Stack!" :
                                        "\nMinimum: " + stack.getMin());

        // Printing top element of the stack
        node = stack.peek();

        System.out.println("\nTop: " + (node == null ?
                                       "\nEmpty!" : node.getData()));
    }
}
```

## 蟒蛇 3

```
"""
Python program to retrieve original elements of the
from a Stack which returns the minimum element
in O(1) time and O(1) space
"""

# Class to make a Node
class Node:

    # Constructor which assign argument to nade's value
    def __init__(self, value):
        self.value = value
        self.next = None

    # This method returns the string
    # representation of the object.
    def __str__(self):
        return "Node({})".format(self.value)

    # __repr__ is same as __str__
    __repr__ = __str__

class Stack:

    # Stack Constructor initialise
    # top of stack and counter.
    def __init__(self):
        self.top = None
        self.count = 0
        self.minimum = None

    # This method returns the string
    # representation of the object (stack).
    def __str__(self):
        temp=self.top
        m = self.minimum
        out=[]
        if temp is None:
            print("Empty Stack")
        else:
            while not temp is None :
                val = temp.value
                if val < m:
                    m = (2 * m) -val
                    val = ( val + m ) / 2
                out.append(str(int(val)))
                temp=temp.next
            out=' '.join(out)
            return (out)

    # __repr__ is same as __str__
    __repr__=__str__

    # This method is used to get minimum element of stack
    def getMin(self):
        if self.top is None:
            return "Stack is empty"
        else:
            return self.minimum

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
            if self.top.value < self.minimum:
                return self.minimum
            else:
                return self.top.value

    # This method is used to add node to stack
    def push(self,value):
        if self.top is None:
            self.top = Node(value)
            self.minimum = value

        else:
            new_node = Node(value)
            if value < self.minimum:
                temp = (2 * value) - self.minimum
                new_node.value = temp
                self.minimum = value
            new_node.next = self.top
            self.top = new_node

    # This method is used to pop top of stack
    def pop(self):
        new_node = self.top
        if self.top is None:
            print( "Stack is empty")
        else:
            removedNode = new_node.value
            if removedNode < self.minimum:
                self.minimum = ( ( 2 * self.minimum ) - removedNode )
                new_node.value = ( (removedNode + self.minimum) / 2 )
            self.top = self.top.next
            return int(new_node.value)

# Driver program to test above class
stack = Stack()

stack.push(5)
stack.push(3)
stack.push(4)
print("Elements in the stack are:")
print(stack)

print("Minimum: {}" .format( stack.getMin() ) )

stack.push(1)
stack.push(2)

print("Stack after adding new elements:")
print(stack)

print("Minimum:{}" .format( stack.getMin() ) )
print("Element Popped: {}".format(stack.pop()))
print("Element Popped: {}".format(stack.pop()))

print("Stack after removing top two elements: ")
print(stack)

print("Minimum: {}" .format( stack.getMin() ) )

print("Top: {}".format( stack.peek() ) )

# This code is contributed by Blinkii
```

## C#

```
// C# program to retrieve original elements of the
// from a Stack which returns the minimum element
// in O(1) time and O(1) space
using System;

public class Stack
{
    Node top;

    // Stores minimum element of the stack
    public int minimum;

    // Function to push an element
    public void push(Node node)
    {
        int current = node.getData();
        if (top == null)
        {
            top = node;
            minimum = current;
        }
        else
        {
            if (current < minimum)
            {
                node.setData(2 * current - minimum);
                minimum = current;
            }
            node.setNext(top);
            top = node;
        }
    }

    // Retrieves topmost element
    public Node pop()
    {
        Node node = top;
        if (node != null)
        {
            int current = node.getData();
            if (current < minimum)
            {
                minimum = 2 * minimum - current;
                node.setData((current + minimum) / 2);
            }
            top = top.getNext();
        }
        return node;
    }

    // Retrieves topmost element without
    // popping it from the stack
    public Node peek()
    {
        Node node = null;
        if (top != null)
        {
            node = new Node();
            int current = top.getData();
            node.setData(current < minimum ? minimum : current);
        }
        return node;
    }

    // Function to print all elements in the stack
    public void printAll()
    {
        Node ptr = top;
        int min = minimum;
        if (ptr != null)
        {
            // if stack is not empty
            while (true)
            {
                int val = ptr.getData();
                if (val < min)
                {
                    min = 2 * min - val;
                    val = (val + min) / 2;
                }
                Console.Write(val + " ");
                ptr = ptr.getNext();
                if (ptr == null)
                    break;
            }
            Console.WriteLine();
        }
        else
            Console.WriteLine("Empty!");
    }

    // Returns minimum of Stack
    public int getMin()
    {
        return minimum;
    }

    public bool isEmpty()
    {
        return top == null;
    }
}

// Node class which contains data
// and pointer to next node
public class Node
{
    public int data;
    public Node next;
    public Node()
    {
        data = -1;
        next = null;
    }

    public Node(int d)
    {
        data = d;
        next = null;
    }

    public void setData(int data)
    {
        this.data = data;
    }

    public void setNext(Node next)
    {
        this.next = next;
    }

    public Node getNext()
    {
        return next;
    }

    public int getData()
    {
        return data;
    }
}

// Driver Code
public class MainClass
{
    public static void Main(String[] args)
    {
        // Create a new stack
        Stack stack = new Stack();
        Node node;

        // Push the element into the stack
        stack.push(new Node(5));
        stack.push(new Node(3));
        stack.push(new Node(4));

        // Calls the method to print the stack
        Console.WriteLine("Elements in the stack are:");
        stack.printAll();

        // Print current minimum element if stack is
        // not empty
        Console.WriteLine(stack.isEmpty() ? "\nEmpty Stack!" :
                                "\nMinimum: " + stack.getMin());

        // Push new elements into the stack
        stack.push(new Node(1));
        stack.push(new Node(2));

        // Printing the stack
        Console.WriteLine("\nStack after adding new elements:");
        stack.printAll();

        // Print current minimum element if stack is
        // not empty
        Console.WriteLine(stack.isEmpty() ? "\nEmpty Stack!" :
                                    "\nMinimum: " + stack.getMin());

        // Pop elements from the stack
        node = stack.pop();
        if(node == null)
            Console.WriteLine("\nElement Popped: "+"Empty!");
        else
            Console.WriteLine("\nElement Popped: "+node.getData());

        node = stack.pop();
        if(node == null)
            Console.WriteLine("Element Popped: "+"Empty!");
        else
            Console.WriteLine("Element Popped: "+node.getData());

        // Printing stack after popping elements
        Console.WriteLine("\nStack after removing top two elements:");
        stack.printAll();

        // Printing current Minimum element in the stack
        Console.WriteLine(stack.isEmpty() ? "\nEmpty Stack!" :
                                        "\nMinimum: " + stack.getMin());

        // Printing top element of the stack
        node = stack.peek();
        if(node == null)
            Console.WriteLine("\nTop: "+"\nEmpty!");
        else
            Console.WriteLine("\nTop: "+node.getData());

    }
}

// This code is contributed by Rajput-Ji
```

## C++

```
// Cpp program to retrieve original elements of the
// from a Stack which returns the minimum element
// in O(1) time and O(1) space

#include<bits/stdc++.h>
using namespace std;

// Node class which contains data
// and pointer to next node
class Node {
  public:
    int data;
    Node* next;
    Node()
    {
        data = -1;
        next = NULL;
    }

    Node(int d)
    {
        data = d;
        next = NULL;
    }

    void setData(int data)
    {
        this->data = data;
    }

    void setNext(Node* next)
    {
        this->next = next;
    }

    Node* getNext()
    {
        return next;
    }

    int getData()
    {
        return data;
    }
};

class Stack{
  public:
    Node* top;
    // Stores minimum element of the stack
    int minimum;

    // Function to push an element
    void push(Node* node)
    {
      int current=node->getData();
      if(top == NULL)
      {
        top=node;
        minimum=current;
      }
      else{
        if(current < minimum)
        {
          node->setData(2*current - minimum);
          minimum = current;
        }
        node->setNext(top);
        top=node;
      }
    }

   // Retrieves topmost element
    Node* pop()
    {
      Node* node = top;
      if(node!=NULL)
      {
        int current=node->getData();
        if(current<minimum)
        {
          minimum = 2*minimum - current;
          node->setData((current + minimum) / 2);
          }
            top = top->getNext();
        }
        return node;
    }

    // Retrieves topmost element without
    // popping it from the stack
    Node* peek()
    {
        Node* node = NULL;
        if (top != NULL) {
            node = new Node();
            int current = top->getData();
            node->setData(current < minimum ? minimum : current);
        }
        return node;
    }

    // Function to print all elements in the stack
    void printAll()
    {
        Node* ptr = top;
        int min = minimum;
        if (ptr != NULL) { // if stack is not empty
            while (true) {
                int val = ptr->getData();
                if (val < min) {
                    min = 2 * min - val;
                    val = (val + min) / 2;
                }
                cout << val << "  ";
                ptr = ptr->getNext();
                if (ptr == NULL)
                    break;
            }
            cout << '\n';
        }
        else
           cout << "Empty!\n";
    }

    // Returns minimum of Stack
    int getMin()
    {
        return minimum;
    }

    bool isEmpty()
    {
        return top == NULL;
    }
};

int main()
{
  Stack* stack = new Stack();
  Node* node;
  stack->push(new Node(5));
  stack->push(new Node(3));
  stack->push(new Node(4));

  // Calls the method to print the stack
  cout << "Elements in the stack are:\n";
  stack->printAll();

  // Print current minimum element if stack is
  // not empty
  if(stack->isEmpty())
    cout << "Empty Stack!\n";
  else
    cout << "Minimum: " <<  stack->getMin() << '\n';

  // Push new elements into the stack
  stack->push(new Node(1));
  stack->push(new Node(2));

  // Printing the stack
  cout << "Stack after adding new elements:\n";
  stack->printAll();

  // Print current minimum element if stack is
  // not empty
   if(stack->isEmpty())
    cout << "Empty Stack!\n";
  else
    cout << "Minimum: " <<  stack->getMin() << '\n';

  // Pop elements from the stack
  node = stack->pop();
  cout << "Element Popped: ";
  if(node == NULL)
   cout << "Empty!\n";
  else
   cout << node->getData() << '\n';
  node = stack->pop();
  cout << "Element Popped: ";
  if(node == NULL)
   cout << "Empty!\n";
  else
   cout << node->getData() << '\n';

  // Printing stack after popping elements
  cout << "Stack after removing top two elements:\n";
  stack->printAll();

  // Printing current Minimum element in the stack
   if(stack->isEmpty())
    cout << "Empty Stack!\n";
  else
    cout << "Minimum: " <<  stack->getMin() << '\n';   
  // Printing top element of the stack
  node = stack->peek();

  cout << "Top: " ;
  if(node == NULL)
  cout << "Empty!\n";
  else
  cout << node->getData() << '\n';
  return 0;
}
```

**Output:** 

```
Elements in the stack are:
4  3  5  

Minimum: 3

Stack after adding new elements:
2  1  4  3  5  

Minimum: 1

Element Popped: 2
Element Popped: 1

Stack after removing top two elements:
4  3  5  

Minimum: 3

Top: 4
```
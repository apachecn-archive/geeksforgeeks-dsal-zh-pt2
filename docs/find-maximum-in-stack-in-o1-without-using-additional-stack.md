# 在不使用额外堆栈的情况下，在 O(1)中找到堆栈中的最大值

> 原文:[https://www . geeksforgeeks . org/find-不使用额外堆栈的最大堆栈长度/](https://www.geeksforgeeks.org/find-maximum-in-stack-in-o1-without-using-additional-stack/)

任务是设计一个堆栈，在不使用额外堆栈的情况下，可以在 O(1)时间内获得堆栈中的最大值。

**示例:**

> **输入:**
> 推(2)
> findMax()
> 推(6)
> find max()
> pop()
> find max()
> **输出:**
> 2 插入堆栈中
> 最大值:2
> 6 插入堆栈中
> 最大值:6
> 元素弹出
> 堆栈中最大值:2

**方法:**不要将单个元素推送到堆栈中，而是推一对。这对由**(值，本地最大值)**组成，其中**本地最大值**是该元素的最大值。

*   当我们插入新元素时，如果新元素大于它下面的局部最大值，我们将新元素的局部最大值设置为等于元素本身。
*   否则，我们将新元素的局部最大值设置为其下元素的局部最大值。
*   栈顶的局部最大值将是整体最大值。
*   现在，如果我们想知道任何给定点的最大值，我们会向堆栈顶部询问与之相关的局部最大值，这可以在 O(1)中完成。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

struct Block {

    // A block has two elements
    // as components
    int value, localMax;
};

class Stack {

private:
    // Pointer of type block,
    // Will be useful later as the
    // size can be dynamically allocated
    struct Block* S;
    int size, top;

public:
    Stack(int);
    void push(int);
    void pop();
    void max();
};

Stack::Stack(int n)
{

    // Setting size of stack and
    // initial value of top
    size = n;
    S = new Block[n];
    top = -1;
}

// Function to push an element to the stack
void Stack::push(int n)
{

    // Doesn't allow pushing elements
    // if stack is full
    if (top == size - 1) {
        cout << "Stack is full" << endl;
    }
    else {
        top++;

        // If the inserted element is the first element
        // then it is the maximum element, since no other
        // elements is in the stack, so the localMax
        // of the first element is the element itself
        if (top == 0) {
            S[top].value = n;
            S[top].localMax = n;
        }
        else {

            // If the newly pushed element is
            // less than the localMax of element below it,
            // Then the over all maximum doesn't change
            // and hence, the localMax of the newly inserted
            // element is same as element below it
            if (S[top - 1].localMax > n) {
                S[top].value = n;
                S[top].localMax = S[top - 1].localMax;
            }

            // Newly inserted element is greater than the localMax
            // below it, hence the localMax of new element
            // is the element itself
            else {
                S[top].value = n;
                S[top].localMax = n;
            }
        }

        cout << n << " inserted in stack" << endl;
    }
}

// Function to remove an element
// from the top of the stack
void Stack::pop()
{

    // If stack is empty
    if (top == -1) {
        cout << "Stack is empty" << endl;
    }

    // Remove the element if the stack
    // is not empty
    else {
        top--;
        cout << "Element popped" << endl;
    }
}

// Function to find the maximum
// element from the stack
void Stack::max()
{

    // If stack is empty
    if (top == -1) {
        cout << "Stack is empty" << endl;
    }
    else {

        // The overall maximum is the local maximum
        // of the top element
        cout << "Maximum value in the stack: "
             << S[top].localMax << endl;
    }
}

// Driver code
int main()
{

    // Create stack of size 5
    Stack S1(5);

    S1.push(2);
    S1.max();
    S1.push(6);
    S1.max();
    S1.pop();
    S1.max();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static class Block
{

    // A block has two elements
    // as components
    int value, localMax;
};

static class Stack
{

    // Pointer of type block,
    // Will be useful later as the
    // size can be dynamically allocated
    Block S[];
    int size, top;

Stack(int n)
{

    // Setting size of stack and
    // initial value of top
    size = n;
    S = new Block[n];
    for(int i=0;i<n;i++)S[i]=new Block();
    top = -1;
}

// Function to push an element to the stack
void push(int n)
{

    // Doesn't allow pushing elements
    // if stack is full
    if (top == size - 1)
    {
        System.out.print( "Stack is full" );
    }
    else
    {
        top++;

        // If the inserted element is the first element
        // then it is the maximum element, since no other
        // elements is in the stack, so the localMax
        // of the first element is the element itself
        if (top == 0)
        {
            S[top].value = n;
            S[top].localMax = n;
        }
        else
        {

            // If the newly pushed element is
            // less than the localMax of element below it,
            // Then the over all maximum doesn't change
            // and hence, the localMax of the newly inserted
            // element is same as element below it
            if (S[top - 1].localMax > n)
            {
                S[top].value = n;
                S[top].localMax = S[top - 1].localMax;
            }

            // Newly inserted element is greater than the localMax
            // below it, hence the localMax of new element
            // is the element itself
            else
            {
                S[top].value = n;
                S[top].localMax = n;
            }
        }

        System.out.println( n + " inserted in stack" );
    }
}

// Function to remove an element
// from the top of the stack
void pop()
{

    // If stack is empty
    if (top == -1)
    {
        System.out.println( "Stack is empty");
    }

    // Remove the element if the stack
    // is not empty
    else
    {
        top--;
        System.out.println( "Element popped" );
    }
}

// Function to find the maximum
// element from the stack
void max()
{

    // If stack is empty
    if (top == -1)
    {
        System.out.println( "Stack is empty");
    }
    else
    {

        // The overall maximum is the local maximum
        // of the top element
        System.out.println( "Maximum value in the stack: "+
                                            S[top].localMax);
    }
}
}

// Driver code
public static void main(String args[])
{

    // Create stack of size 5
    Stack S1=new Stack(5);

    S1.push(2);
    S1.max();
    S1.push(6);
    S1.max();
    S1.pop();
    S1.max();
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
class Block:

    # A block has two elements
    # as components  (i.e. value and localMax)
    def __init__(self, value, localMax):
        self.value = value
        self.localMax = localMax

class Stack:
    def __init__(self, size):

        # Setting size of stack and
        # initial value of top
        self.stack = [None] * size
        self.size = size
        self.top = -1

    # Function to push an element
    # to the stack
    def push(self, value):

        # Don't allow pushing elements
        # if stack is full
        if self.top == self.size - 1:
            print("Stack is full")
        else:
            self.top += 1

            # If the inserted element is the first element
            # then it is the maximum element, since no other
            # elements is in the stack, so the localMax
            # of the first element is the element itself
            if self.top == 0:
                self.stack[self.top] = Block(value, value)

            else:

                # If the newly pushed element is less
                # than the localMax of element below it,
                # Then the over all maximum doesn't change
                # and hence, the localMax of the newly inserted
                # element is same as element below it
                if self.stack[self.top - 1].localMax > value:
                    self.stack[self.top] = Block(
                        value, self.stack[self.top - 1].localMax)

                # Newly inserted element is greater than
                # the localMax below it, hence the localMax
                # of new element is the element itself
                else:
                    self.stack
                    self.stack[self.top] = Block(value, value)

            print(value, "inserted in the stack")

    # Function to remove an element 
    # from the top of the stack         
    def pop(self):

        # If stack is empty
        if self.top == -1:
            print("Stack is empty")

        # Remove the element if the stack
        # is not empty
        else:
            self.top -= 1
            print("Element popped")

    # Function to find the maximum 
    # element from the stack 
    def max(self):

        # If stack is empty
        if self.top == -1:
            print("Stack is empty")
        else:

            # The overall maximum is the local maximum
            # of the top element
            print("Maximum value in the stack:",
                  self.stack[self.top].localMax)

# Driver code

# Create stack of size 5
stack = Stack(5)
stack.push(2)
stack.max()
stack.push(6)
stack.max()
stack.pop()
stack.max()

# This code is contributed by girishthatte
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

public class Block
{

    // A block has two elements
    // as components
    public int value, localMax;
};

public class Stack
{

    // Pointer of type block,
    // Will be useful later as the
    // size can be dynamically allocated
    public Block []S;
    public int size, top;

public Stack(int n)
{

    // Setting size of stack and
    // initial value of top
    size = n;
    S = new Block[n];
    for(int i = 0; i < n; i++)S[i] = new Block();
    top = -1;
}

// Function to push an element to the stack
public void push(int n)
{

    // Doesn't allow pushing elements
    // if stack is full
    if (top == size - 1)
    {
        Console.Write( "Stack is full" );
    }
    else
    {
        top++;

        // If the inserted element is the first element
        // then it is the maximum element, since no other
        // elements is in the stack, so the localMax
        // of the first element is the element itself
        if (top == 0)
        {
            S[top].value = n;
            S[top].localMax = n;
        }
        else
        {

            // If the newly pushed element is
            // less than the localMax of element below it,
            // Then the over all maximum doesn't change
            // and hence, the localMax of the newly inserted
            // element is same as element below it
            if (S[top - 1].localMax > n)
            {
                S[top].value = n;
                S[top].localMax = S[top - 1].localMax;
            }

            // Newly inserted element is greater than the localMax
            // below it, hence the localMax of new element
            // is the element itself
            else
            {
                S[top].value = n;
                S[top].localMax = n;
            }
        }

        Console.WriteLine( n + " inserted in stack" );
    }
}

// Function to remove an element
// from the top of the stack
public void pop()
{

    // If stack is empty
    if (top == -1)
    {
        Console.WriteLine( "Stack is empty");
    }

    // Remove the element if the stack
    // is not empty
    else
    {
        top--;
        Console.WriteLine( "Element popped" );
    }
}

// Function to find the maximum
// element from the stack
public void max()
{

    // If stack is empty
    if (top == -1)
    {
        Console.WriteLine( "Stack is empty");
    }
    else
    {

        // The overall maximum is the local maximum
        // of the top element
        Console.WriteLine( "Maximum value in the stack: "+
                                            S[top].localMax);
    }
}
}

// Driver code
public static void Main(String []args)
{

    // Create stack of size 5
    Stack S1 = new Stack(5);

    S1.push(2);
    S1.max();
    S1.push(6);
    S1.max();
    S1.pop();
    S1.max();
}
}

// This code contributed by Rajput-Ji
```

**Output:** 

```
2 inserted in stack
Maximum value in the stack: 2
6 inserted in stack
Maximum value in the stack: 6
Element popped
Maximum value in the stack: 2
```

**时间复杂度:** O(1)

**辅助空间:** O(1)
# 设计并实现特殊堆栈数据结构|新增空间优化版

> 原文:[https://www . geesforgeks . org/design-and-implement-special-stack-data-structure/](https://www.geeksforgeeks.org/design-and-implement-special-stack-data-structure/)

**问题:**设计一个数据结构 SpecialStack，它支持所有的堆栈操作，比如 push()，pop()，isEmpty()，isFull()和一个额外的操作 getMin()，它应该从 SpecialStack 返回最小元素。SpecialStack 的所有这些操作都必须是 O(1)。要实现 SpecialStack，您应该只使用标准的 Stack 数据结构，而不要使用数组、列表等其他数据结构。等等。

**示例:**

```
Consider the following SpecialStack
16  --> TOP
15
29
19
18

When getMin() is called it should 
return 15, which is the minimum 
element in the current stack. 

If we do pop two times on stack, 
the stack becomes
29  --> TOP
19
18

When getMin() is called, it should 
return 18 which is the minimum in 
the current stack.
```

**解决方法:**使用两个栈:一个存储实际栈元素，另一个作为辅助栈存储最小值。其思想是以这样一种方式执行 push()和 pop()操作，即辅助堆栈的顶部总是最小的。让我们看看 push()和 pop()操作是如何工作的。

**Push(int x) //将元素 x 插入到特殊堆栈**
1)将 x 推送到第一个堆栈(包含实际元素的堆栈)
2)将 x 与第二个堆栈(辅助堆栈)的顶部元素进行比较。让顶元素为 y.
…..a)如果 x 小于 y，则将 x 推到辅助堆栈。
…..b)如果 x 大于 y，则将 y 推到辅助堆栈。
**int Pop() //从特殊堆栈中移除一个元素并返回移除的元素**
1)从辅助堆栈中弹出顶部元素。
2)从实际堆栈中弹出顶部元素并返回。
步骤 1 是必要的，以确保辅助堆栈也为未来的操作而更新。
**int getMin() //从特殊栈**
返回最小元素 1)返回辅助栈的顶部元素。

我们可以看到**以上所有操作都是 O(1)** 。
我们来看一个例子。让我们假设两个堆栈最初都是空的，并且 18、19、29、15 和 16 被插入到 SpecialStack 中。

```
When we insert 18, both stacks change to following.
Actual Stack
18 <--- top     
Auxiliary Stack
18 <---- top

When 19 is inserted, both stacks change to following.
Actual Stack
19 <--- top     
18
Auxiliary Stack
18 <---- top
18

When 29 is inserted, both stacks change to following.
Actual Stack
29 <--- top     
19
18
Auxiliary Stack
18 <---- top
18
18

When 15 is inserted, both stacks change to following.
Actual Stack
15 <--- top     
29
19 
18
Auxiliary Stack
15 <---- top
18
18
18

When 16 is inserted, both stacks change to following.
Actual Stack
16 <--- top     
15
29
19 
18
Auxiliary Stack
15 <---- top
15
18
18
18
```

下面是 SpecialStack 类的实现。在下面的实现中，SpecialStack 继承自 Stack，有一个 Stack 对象 *min* ，作为辅助堆栈。

## C++

```
#include <iostream>
#include <stdlib.h>

using namespace std;

/* A simple stack class with
basic stack funtionalities */
class Stack {
private:
    static const int max = 100;
    int arr[max];
    int top;

public:
    Stack() { top = -1; }
    bool isEmpty();
    bool isFull();
    int pop();
    void push(int x);
};

/* Stack's member method to check
if the stack is empty */
bool Stack::isEmpty()
{
    if (top == -1)
        return true;
    return false;
}

/* Stack's member method to check
if the stack is full */
bool Stack::isFull()
{
    if (top == max - 1)
        return true;
    return false;
}

/* Stack's member method to remove
an element from it */
int Stack::pop()
{
    if (isEmpty()) {
        cout << "Stack Underflow";
        abort();
    }
    int x = arr[top];
    top--;
    return x;
}

/* Stack's member method to insert
an element to it */
void Stack::push(int x)
{
    if (isFull()) {
        cout << "Stack Overflow";
        abort();
    }
    top++;
    arr[top] = x;
}

/* A class that supports all the stack
operations and one additional
  operation getMin() that returns the
minimum element from stack at
  any time.  This class inherits from
the stack class and uses an
  auxiliary stack that holds minimum
elements */
class SpecialStack : public Stack {
    Stack min;

public:
    int pop();
    void push(int x);
    int getMin();
};

/* SpecialStack's member method to insert
 an element to it. This method
   makes sure that the min stack is also
updated with appropriate minimum
   values */
void SpecialStack::push(int x)
{
    if (isEmpty() == true) {
        Stack::push(x);
        min.push(x);
    }
    else {
        Stack::push(x);
        int y = min.pop();
        min.push(y);
        if (x < y)
            min.push(x);
        else
            min.push(y);
    }
}

/* SpecialStack's member method to
remove an element from it. This method
   removes top element from min stack also. */
int SpecialStack::pop()
{
    int x = Stack::pop();
    min.pop();
    return x;
}

/* SpecialStack's member method to get
 minimum element from it. */
int SpecialStack::getMin()
{
    int x = min.pop();
    min.push(x);
    return x;
}

/* Driver program to test SpecialStack
 methods */
int main()
{
    SpecialStack s;
    s.push(10);
    s.push(20);
    s.push(30);
    cout << s.getMin() << endl;
    s.push(5);
    cout << s.getMin();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of SpecialStack
// Note : here we use Stack class for
// Stack implementation

import java.util.Stack;

/* A class that supports all the
stack operations and one additional
operation getMin() that returns
the minimum element from stack at
any time. This class inherits from
the stack class and uses an
auxiliary stack that holds minimum
 elements */

class SpecialStack extends Stack<Integer> {
    Stack<Integer> min = new Stack<>();

    /* SpecialStack's member method to
insert an element to it. This method
    makes sure that the min stack is
also updated with appropriate minimum
    values */
    void push(int x)
    {
        if (isEmpty() == true) {
            super.push(x);
            min.push(x);
        }
        else {
            super.push(x);
            int y = min.pop();
            min.push(y);
            if (x < y)
                min.push(x);
            else
                min.push(y);
        }
    }

    /* SpecialStack's member method to
insert an element to it. This method
    makes sure that the min stack is
also updated with appropriate minimum
    values */
    public Integer pop()
    {
        int x = super.pop();
        min.pop();
        return x;
    }

    /* SpecialStack's member method to get
minimum element from it. */
    int getMin()
    {
        int x = min.pop();
        min.push(x);
        return x;
    }

    /* Driver program to test SpecialStack
methods */
    public static void main(String[] args)
    {
        SpecialStack s = new SpecialStack();
        s.push(10);
        s.push(20);
        s.push(30);
        System.out.println(s.getMin());
        s.push(5);
        System.out.println(s.getMin());
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
# A simple stack class with 
# basic stack funtionalities
class stack:

  def __init__(self):

    self.array = []
    self.top = -1
    self.max = 100 

  # Stack's member method to check
  # if the stack is empty
  def isEmpty(self):

    if self.top == -1:
      return True
    else:
      return False 

  # Stack's member method to check
  # if the stack is full 
  def isFull(self): 

    if self.top == self.max - 1:
      return True
    else:
      return False  

  # Stack's member method to
  # insert an element to it  

  def push(self, data):

    if self.isFull():
      print('Stack OverFlow')
      return
    else:
      self.top += 1
      self.array.append(data)    

  # Stack's member method to
  # remove an element from it
  def pop(self):

    if self.isEmpty():
      print('Stack UnderFlow')
      return
    else:
      self.top -= 1
      return self.array.pop()

# A class that supports all the stack 
# operations and one additional
# operation getMin() that returns the
# minimum element from stack at
# any time.  This class inherits from
# the stack class and uses an
# auxiliary stack that holds
# minimum elements 
class SpecialStack(stack):

  def __init__(self):
    super().__init__()
    self.Min = stack() 

  # SpecialStack's member method to
  # insert an element to it. This method
  # makes sure that the min stack is also
  # updated with appropriate minimum
  # values
  def push(self, x):

    if self.isEmpty():
      super().push(x)
      self.Min.push(x)
    else:
      super().push(x)
      y = self.Min.pop()
      self.Min.push(y)
      if x <= y:
        self.Min.push(x)
      else:
        self.Min.push(y) 

  # SpecialStack's member method to 
  # remove an element from it. This
  # method removes top element from
  # min stack also.
  def pop(self):

    x = super().pop()
    self.Min.pop()
    return x 

  # SpecialStack's member method
  # to get minimum element from it.
  def getmin(self):

    x = self.Min.pop()
    self.Min.push(x)
    return x

# Driver code
if __name__ == '__main__':

  s = SpecialStack()
  s.push(10)
  s.push(20)
  s.push(30)
  print(s.getmin())
  s.push(5)
  print(s.getmin())

# This code is contributed by rachitkatiyar99
```

**Output**

```
10
5
```

**复杂度分析:**

*   **时间复杂度:**
    1.  **对于插入操作:O(1)** (因为在堆栈中插入“推”需要恒定的时间)
    2.  **对于删除操作:O(1)** (因为堆栈中的删除“弹出”需要恒定的时间)
    3.  **对于“获取最小值”操作:O(1)** (因为我们使用了一个顶部作为最小元素的辅助堆栈)
*   **辅助空间:** O(n)。
    使用辅助堆栈存储值。

**空间优化版**
以上做法均可优化。我们可以限制辅助堆栈中的元素数量。只有当主栈的传入元素小于或等于辅助栈的顶部时，我们才能推送。同样，在弹出过程中，如果弹出元素等于辅助堆栈的顶部，则移除辅助堆栈的顶部元素。下面是 push()和 pop()的修改实现。

## C++

```
/* SpecialStack's member method to
   insert an element to it. This method
   makes sure that the min stack is
   also updated with appropriate minimum
   values */
void SpecialStack::push(int x)
{
    if (isEmpty() == true) {
        Stack::push(x);
        min.push(x);
    }
    else {
        Stack::push(x);
        int y = min.pop();
        min.push(y);

        /* push only when the incoming element
           of main stack is smaller
        than or equal to top of auxiliary stack */
        if (x <= y)
            min.push(x);
    }
}

/* SpecialStack's member method to
   remove an element from it. This method
   removes top element from min stack also. */
int SpecialStack::pop()
{
    int x = Stack::pop();
    int y = min.pop();

    /* Push the popped element y back
       only if it is not equal to x */
    if (y != x)
        min.push(y);

    return x;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* SpecialStack's member method to
insert an element to it. This method
makes sure that the min stack is
also updated with appropriate minimum
values */

void push(int x)
{
    if (isEmpty() == true) {
        super.push(x);
        min.push(x);
    }
    else {
        super.push(x);
        int y = min.pop();
        min.push(y);

        /* push only when the incoming
           element of main stack is smaller
        than or equal to top of auxiliary stack */
        if (x <= y)
            min.push(x);
    }
}

/* SpecialStack's member method to
   remove an element from it. This method
   removes top element from min stack also. */
public Integer pop()
{
    int x = super.pop();
    int y = min.pop();

    /* Push the popped element y back
       only if it is not equal to x */
    if (y != x)
        min.push(y);
    return x;
}

// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
''' SpecialStack's member method to
insert an element to it. This method
makes sure that the min stack is
also updated with appropriate minimum
values '''

def push(x):
    if (isEmpty() == True):
        super.append(x);
        min.append(x);

    else:
        super.append(x);
        y = min.pop();
        min.append(y);

        ''' push only when the incoming
           element of main stack is smaller
        than or equal to top of auxiliary stack '''
        if (x <= y):
            min.append(x);

''' SpecialStack's member method to
   remove an element from it. This method
   removes top element from min stack also. '''
def pop():
    x = super.pop();
    y = min.pop();

    ''' Push the popped element y back
       only if it is not equal to x '''
    if (y != x):
        min.append(y);
    return x;

# This code contributed by umadevi9616
```

## C#

```
/* SpecialStack's member method to
insert an element to it. This method
makes sure that the min stack is
also updated with appropriate minimum
values */

void push(int x)
{
    if (min.Count==0) {
        super.Push(x);
        min.Push(x);
    }
    else {
        super.Push(x);
        int y = min.Pop();
        min.Push(y);

        /* push only when the incoming
           element of main stack is smaller
        than or equal to top of auxiliary stack */
        if (x <= y)
            min.Push(x);
    }
}

/* SpecialStack's member method to
   remove an element from it. This method
   removes top element from min stack also. */
public int pop()
{
    int x = super.Pop();
    int y = min.Pop();

    /* Push the popped element y back
       only if it is not equal to x */
    if (y != x)
        min.Push(y);
    return x;
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
/* SpecialStack's member method to
insert an element to it. This method
makes sure that the min stack is
also updated with appropriate minimum
values */

function push(x)
{
    if (isEmpty() == true) {
        super.push(x);
        min.push(x);
    }
    else {
        super.push(x);
        var y = min.pop();
        min.push(y);

        /* push only when the incoming
           element of main stack is smaller
        than or equal to top of auxiliary stack */
        if (x <= y)
            min.push(x);
    }
}

/* SpecialStack's member method to
   remove an element from it. This method
   removes top element from min stack also. */
 function pop()
{
    var x = super.pop();
    var y = min.pop();

    /* Push the popped element y back
       only if it is not equal to x */
    if (y != x)
        min.push(y);
    return x;
}

// This code is contributed by umadevi9616
</script>
```

**复杂度分析:**

*   **时间复杂度:**
    1.  **对于插入操作:O(1)** (因为在堆栈中插入“推”需要恒定的时间)
    2.  **对于删除操作:O(1)** (因为堆栈中的删除“弹出”需要恒定的时间)
    3.  **对于“获取最小值”操作:O(1)** (因为我们使用了一个顶部为最小元素的辅助)
*   **辅助空间:** O(n)。
    最差情况下的复杂性与上述相同，但在其他情况下，由于忽略了重复，因此比上述方法占用的空间略少。

**进一步优化 O(1)时间复杂度和 O(1)空间复杂度解:**
上述方法可以进一步优化，使解在 O(1)时间复杂度和 O(1)空间复杂度下工作。其思想是将找到的最小元素(直到当前插入)与所有元素一起存储，作为虚拟值的提醒，并将实际元素存储为虚拟值的倍数。
例如，在将元素“e”推入堆栈时，将其存储为**(e * DUMMY _ VALUE+minFoundSoFar)**，这样我们就知道在插入“e”时堆栈中存在的最小值是多少。

要弹出实际值，只需返回 e/DUMMY_VALUE，并将新的最小值设置为**(minFoundSoFar % DUMMY _ VALUE)**。

**注意:如果我们试图在堆栈中插入 DUMMY_VALUE，下面的方法会失败，所以我们必须仔细选择 DUMMY_VALUE。**
假设堆栈中插入了以下元素–326185

**d** 为虚拟值。

**s** 是包装栈

**顶部**是堆栈的顶部元素

min 是插入/移除元素时的最小值

以下步骤显示了上述变量在任何时刻的当前状态–

> 1.  Push (3);
>     min = 3 **/The updated min is used as the stack here** t5] s = {3 * d+3}
>     top = (3 * d+3)/d = 3
>     
> 
> **//更新 min 为 min >当前元素**
> 
> **->**
> 
> **->**
> 
> **->**
> 
> 14.  s。推(1)；
>     min = 1 **//更新部为最小>当前元素**T33】s = { 3 * d+3->2 * d+2->6 * d+2->1 * d+1 }
>     top =(1 * d+1)/d = 1
>     
> 
> **->T41】2 * d+2**->T43】6 * d+2**->T45】1 * d+1**->T47】8 * d+1 }
> top =(8 * d+1)/d = 8
> T51】s . push(5)；
> min = 1
> s = { 3 * d+3**->T55】2 * d+2**->T57】6 * d+2**->T59】1 * d+1**->T61】8 * d+1**->T63】5 * d+1 }
> top =(5 * d+1)
> s = { 3 * d+3->2 * d+2->6 * d+2->1 * d+1->8 * d+1->5 * d+1 }
> top =(5 * d+1)/d = 5
> min =(8 * d+1)% d = 1**//min 始终是堆栈中第二个顶部元素的余数。**
> *   -好吧。pop()；
>     s = { 3 * d+3->【2 * d+2】>【6 * d+2】>【1 * d+1】>【8 * d+1】
>     top =(8 * d+1)/d = 8
>     min =(1 * d+1)% d = 1
>     t80*   -好吧。pop()
>     s = { 3 * d+3->
>     top =(1 * d+1)/d = 1
>     min =(6 * d+2)% d = 2
>     *   -好吧。pop()
>     s = { 3 * d+3->【2 * d+2】>【6 * d+2】
>     top =(6 * d+2)/d = 6
>     min =(2 * d+2)% d = 2
>     T93
> top =(2 * d+2)/d = 2
> min =(3 * d+3)% d = 3
> *   S. pop ()
>     s = {3 * d+3}
>     top = (3 * d+3)/d = 3
>     min =-1//Because the stack is now empty,******************

## C++

```
#include <iostream>
#include <stack>
#include <vector>
using namespace std;

/* A special stack having peek() pop() and
 * push() along with additional getMin() that
 * returns minimum value in a stack without
 * using extra space and all operations in O(1)
 * time.. ???? */
class SpecialStack
{

    // Sentinel value for min
    int min = -1; 

    // DEMO_VALUE
    static const int demoVal = 9999;
    stack<int> st;

public:

    void getMin()
    {
        cout << "min is: " << min << endl;
    }

    void push(int val)
    {

        // If stack is empty OR current element
        // is less than min, update min.
        if (st.empty() || val < min)
        {
            min = val;
        }

        // Encode the current value with
        // demoVal, combine with min and
        // insert into stack
        st.push(val * demoVal + min);
        cout << "pushed: " << val << endl;
    }

    int pop()
    {   
        // if stack is empty return -1;
        if ( st.empty() ) {
          cout << "stack underflow" << endl ;
          return -1;
        }

        int val = st.top();
        st.pop();

        // If stack is empty, there would
        // be no min value present, so
        // make min as -1
        if (!st.empty())
            min = st.top() % demoVal;
        else
            min = -1;

        cout << "popped: " << val / demoVal << endl;

        // Decode actual value from
        // encoded value
        return val / demoVal;
    }

    int peek()
    {

        // Decode actual value
        // from encoded value
        return st.top() / demoVal;
    }
};

// Driver Code
int main()
{
    SpecialStack s;

    vector<int> arr = { 3, 2, 6, 1, 8, 5, 5, 5, 5 };

    for(int i = 0; i < arr.size(); i++)
    {
        s.push(arr[i]);
        s.getMin();
    }

    cout << endl;
    for(int i = 0; i < arr.size(); i++)
    {
        s.pop();
        s.getMin();
    }
    return 0;
}

// This code is contributed by scisaif
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Stack;

/* A special stack having peek() pop() and push() along with
 * additional getMin() that returns minimum value in a stack
 * without using extra space and all operations in O(1)
 * time.. 🙂
 * */
public class SpecialStack {

    int min = -1; // sentinel value for min
    static int demoVal = 9999; // DEMO_VALUE
    Stack<Integer> st = new Stack<Integer>();

    void getMin() { System.out.println("min is: " + min); }

    void push(int val)
    {
        // if stack is empty OR current element is less than
        // min, update min..
        if (st.isEmpty() || val < min) {
            min = val;
        }

        st.push(val * demoVal
                + min); // encode the current value with
                        // demoVal, combine with min and
                        // insert into stack
        System.out.println("pushed: " + val);
    }

    int pop()
    {   
        // if stack is empty return -1;
        if (st.isEmpty() ) {
             System.out.println("stack underflow");
               return -1;
          }

        int val = st.pop();

        if (!st.isEmpty()) // if stack is empty, there would
                           // be no min value present, so
                           // make min as -1
            min = st.peek() % demoVal;
        else
            min = -1;
        System.out.println("popped: " + val / demoVal);
        return val / demoVal; // decode actual value from
                              // encoded value
    }

    int peek()
    {
        return st.peek() / demoVal; // decode actual value
                                    // from encoded value
    }

    // Driver Code
    public static void main(String[] args)
    {
        SpecialStack s = new SpecialStack();

        int[] arr = { 3, 2, 6, 1, 8, 5, 5, 5, 5 };

        for (int i = 0; i < arr.length; i++) {
            s.push(arr[i]);
            s.getMin();
        }
        System.out.println();
        for (int i = 0; i < arr.length; i++) {
            s.pop();
            s.getMin();
        }
    }
}
```

## C#

```
using System;
using System.Collections.Generic;

/* A special stack having peek() pop() and push() along with
 * additional getMin() that returns minimum value in a stack
 * without using extra space and all operations in O(1)
 * time.. 🙂
 * */
public class SpecialStack {

    int min = -1; // sentinel value for min
    static int demoVal = 9999; // DEMO_VALUE
    Stack<int> st = new Stack<int>();

    void getMin() { Console.WriteLine("min is: " + min); }

    void push(int val)
    {
        // if stack is empty OR current element is less than
        // min, update min..
        if (st.Count==0 || val < min) {
            min = val;
        }

        st.Push(val * demoVal
                + min); // encode the current value with
                        // demoVal, combine with min and
                        // insert into stack
        Console.WriteLine("pushed: " + val);
    }

    int pop()
    {   
        // if stack is empty return -1;
        if (st.Count==0 ) {
             Console.WriteLine("stack underflow");
               return -1;
          }

        int val = st.Pop();

        if (st.Count!=0) // if stack is empty, there would
                           // be no min value present, so
                           // make min as -1
            min = st.Peek() % demoVal;
        else
            min = -1;
        Console.WriteLine("popped: " + val / demoVal);
        return val / demoVal; // decode actual value from
                              // encoded value
    }

    int peek()
    {
        return st.Peek() / demoVal; // decode actual value
                                    // from encoded value
    }

    // Driver Code
    public static void Main(String[] args)
    {
        SpecialStack s = new SpecialStack();

        int[] arr = { 3, 2, 6, 1, 8, 5, 5, 5, 5 };

        for (int i = 0; i < arr.Length; i++) {
            s.push(arr[i]);
            s.getMin();
        }
        Console.WriteLine();
        for (int i = 0; i < arr.Length; i++) {
            s.pop();
            s.getMin();
        }
    }
}

// This code is contributed by gauravrajput1
```

**Output**

```
pushed: 3
min is: 3
pushed: 2
min is: 2
pushed: 6
min is: 2
pushed: 1
min is: 1
pushed: 8
min is: 1
pushed: 5
min is: 1
pushed: 5
min is: 1
pushed: 5
min is: 1
pushed: 5
min is: 1

popped: 5
min is: 1
popped: 5
min is: 1
popped: 5
min is: 1
popped: 5
min is: 1
popped: 8
min is: 1
popped: 1
min is: 2
popped: 6
min is: 2
popped: 2
min is: 3
popped: 3
min is: -1
```

**复杂度分析:**

**对于 push()操作:** O(1)(因为在堆栈中插入“push”需要恒定时间)
**对于 pop()操作:** O(1)(因为在堆栈中进行 pop 操作需要恒定时间)

**对于“获取最小值”操作:** O(1)(因为我们在整个代码中保持了最小值变量)

**辅助空间:** O(1)。不使用额外空间。

https://youtu.be/1Ld7gbW1oHc
[**借助**](https://www.geeksforgeeks.org/design-a-stack-that-supports-getmin-in-o1-time-and-o1-extra-space/) **[@Venki](https://www.geeksforgeeks.org/archives/14149/comment-page-1#comment-5366) 、 [@swarup](https://www.geeksforgeeks.org/archives/14149/comment-page-1#comment-5359) 、[@黄静](https://www.geeksforgeeks.org/archives/14149/comment-page-1#comment-5369)的输入，设计一个支持 O(1)时间内 getMin()和 O(1)额外空间**
的堆栈。
如果发现以上代码不正确，请写评论，或者找其他方法解决同样的问题。
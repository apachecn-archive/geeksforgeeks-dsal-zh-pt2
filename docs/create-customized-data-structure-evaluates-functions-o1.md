# 创建一个定制的数据结构，用于评估 O(1)

中的函数

> 原文:[https://www . geesforgeks . org/create-customized-data-structure-evaluate-functions-O1/](https://www.geeksforgeeks.org/create-customized-data-structure-evaluates-functions-o1/)

创建一个定制的数据结构，使其具有如下功能:-
getlasteelement()；
removeLastElement()；
AddElement()
GetMin()

**所有功能应为 O(1)**
问题来源:亚马逊面试问题

**方法:**
1)用两个元素创建类型结构的自定义堆栈，(元素，min_till_now)
2)在这个自定义数据类型上实现函数

## C++

```
// program to demonstrate customized data structure
// which supports functions in O(1)
#include <iostream>
#include <vector>
using namespace std;
const int MAXX = 1000;

// class stack
class stack {
    int minn;
    int size;

public:
    stack()
    {
        minn = 99999;
        size = -1;
    }
    vector<pair<int, int> > arr;
    int GetLastElement();
    int RemoveLastElement();
    int AddElement(int element);
    int GetMin();
};

// utility function for adding a new element
int stack::AddElement(int element)
{
    if (size > MAXX) {
        cout << "stack overflow, max size reached!\n";
        return 0;
    }
    if (element < minn)
        minn = element;
    arr.push_back(make_pair(element, minn));
    size++;
    return 1;
}

// utility function for returning last element of stack
int stack::GetLastElement()
{
    if (size == -1) {
        cout << "No elements in stack\n";
        return 0;
    }
    return arr[size].first;
}

// utility function for removing last element successfully;
int stack::RemoveLastElement()
{
    if (size == -1) {
        cout << "stack empty!!!\n";
        return 0;
    }

    // updating minimum element
    if (size > 0 && arr[size - 1].second > arr[size].second) {
        minn = arr[size - 1].second;
    }
    arr.pop_back();
    size -= 1;
    return 1;
}

// utility function for returning min element till now;
int stack::GetMin()
{
    if (size == -1) {
        cout << "stack empty!!\n";
        return 0;
    }
    return arr[size].second;
}

// Driver code
int main()
{
    stack s;
    int success = s.AddElement(5);
    if (success == 1)
        cout << "5 inserted successfully\n";

    success = s.AddElement(7);
    if (success == 1)
        cout << "7 inserted successfully\n";

    success = s.AddElement(3);
    if (success == 1)
        cout << "3 inserted successfully\n";
    int min1 = s.GetMin();
    cout << "min element  :: " << min1 << endl;

    success = s.RemoveLastElement();
    if (success == 1)
        cout << "removed successfully\n";

    success = s.AddElement(2);
    if (success == 1)
        cout << "2 inserted successfully\n";

    success = s.AddElement(9);
    if (success == 1)
        cout << "9 inserted successfully\n";
    int last = s.GetLastElement();
    cout << "Last element :: " << last << endl;

    success = s.AddElement(0);
    if (success == 1)
        cout << "0 inserted successfully\n";
    min1 = s.GetMin();
    cout << "min element  :: " << min1 << endl;

    success = s.RemoveLastElement();
    if (success == 1)
        cout << "removed successfully\n";

    success = s.AddElement(11);
    if (success == 1)
        cout << "11 inserted successfully\n";
    min1 = s.GetMin();
    cout << "min element  :: " << min1 << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// program to demonstrate customized data structure
// which supports functions in O(1)
import java.util.ArrayList;
public class Gfg
{

  // class Pair
  static class Pair{
    int element;
    int minElement;

    public Pair(int element, int minElement) {
      this.element = element;
      this.minElement = minElement;
    }
  }
  int min;
  ArrayList<Pair> stack = new ArrayList<>();

  public Gfg() {
    this.min = Integer.MAX_VALUE;
  }

  // utility function for adding a new element
  void addElement(int x)
  {
    if(stack.size() == 0 || x < min)
    {
      min=x;
    }
    Pair pair = new Pair(x,min);
    stack.add(pair);
    System.out.println(x + " inserted successfully");
  }

  // utility function for returning last element of stack
  int getLastElement()
  {
    if (stack.size() == 0)
    {
      System.out.println("UnderFlow Error");
      return -1;
    }
    else
    {
      return stack.get(stack.size() - 1).element;
    }
  }

  // utility function for removing last element successfully;
  void removeLastElement()
  {

    if (stack.size() == 0)
    {
      System.out.println("UnderFlow Error");
    }
    else if (stack.size() > 1)
    {
      min=stack.get(stack.size() - 2).minElement;
    }
    else
    {
      min=Integer.MAX_VALUE;
    }
    stack.remove(stack.size() - 1);
    System.out.println("removed successfully");
  }

  // utility function for returning min element till now;
  int getMin()
  {
    if (stack.size() == 0)
    {
      System.out.println("UnderFlow Error");
      return -1;
    }
    return stack.get(stack.size() - 1).minElement;
  }

  // Driver Code
  public static void main(String[] args) {
    Gfg newStack = new Gfg();
    newStack.addElement(5);
    newStack.addElement(7);
    newStack.addElement(3);
    System.out.println("min element :: "+newStack.getMin());
    newStack.removeLastElement();
    newStack.addElement(2);
    newStack.addElement(9);
    System.out.println("last element :: "+newStack.getLastElement());
    newStack.addElement(0);
    System.out.println("min element :: "+newStack.getMin());
    newStack.removeLastElement();
    newStack.addElement(11);
    System.out.println("min element :: "+newStack.getMin());
  }
}

// This code is contributed by AkashYadav4.
```

## 蟒蛇 3

```
# Program to demonstrate customized data structure
# which supports functions in O(1)
import sys

stack = []
Min = sys.maxsize

# Utility function for adding a new element
def addElement(x):

    global Min, stack
    if (len(stack) == 0 or x < Min):
        Min = x
    pair = [x, Min]
    stack.append(pair)
    print(x, "inserted successfully")

# Utility function for returning last
# element of stack
def getLastElement():

    global Min, stack

    if (len(stack) == 0):
        print("UnderFlow Error")
        return -1
    else:
        return stack[-1][0]

# Utility function for removing last
# element successfully;
def removeLastElement():

    global Min, stack
    if (len(stack) == 0):
        print("UnderFlow Error")
    elif (len(stack) > 1):
        Min = stack[-2][1]
    else:
        Min = sys.maxsize
    stack.pop()

    print("removed successfully")

# Utility function for returning min
# element till now;
def getMin():

    global Min, stack
    if (len(stack) == 0):
        print("UnderFlow Error")
        return -1

    return stack[-1][1]

# Driver code
addElement(5)
addElement(7)
addElement(3)
print("min element ::", getMin())
removeLastElement()
addElement(2)
addElement(9)
print("Last element ::", getLastElement())
addElement(0)
print("min element ::", getMin())
removeLastElement()
addElement(11)
print("min element ::", getMin())

# This code is contributed by mukesh07
```

## C#

```
// program to demonstrate customized data structure
// which supports functions in O(1)
using System;
using System.Collections.Generic;
class GFG {

  static List<Tuple<int,int>> stack = new List<Tuple<int,int>>();
  static int min = Int32.MaxValue;

  // utility function for adding a new element
  static void addElement(int x)
  {
    if(stack.Count == 0 || x < min)
    {
      min=x;
    }
    Tuple<int,int> pair = new Tuple<int,int>(x,min);
    stack.Add(pair);
    Console.WriteLine(x + " inserted successfully");
  }

  // utility function for returning last element of stack
  static int getLastElement()
  {
    if (stack.Count == 0)
    {
      Console.WriteLine("UnderFlow Error");
      return -1;
    }
    else
    {
      return stack[stack.Count - 1].Item1;
    }
  }

  // utility function for removing last element successfully;
  static void removeLastElement()
  {

    if (stack.Count == 0)
    {
      Console.WriteLine("UnderFlow Error");
    }
    else if (stack.Count > 1)
    {
      min=stack[stack.Count - 2].Item2;
    }
    else
    {
      min=Int32.MaxValue;
    }
    stack.RemoveAt(stack.Count - 1);
    Console.WriteLine("removed successfully");
  }

  // utility function for returning min element till now;
  static int getMin()
  {
    if (stack.Count == 0)
    {
      Console.WriteLine("UnderFlow Error");
      return -1;
    }
    return stack[stack.Count - 1].Item2;
  }

  static void Main() {
    addElement(5);
    addElement(7);
    addElement(3);
    Console.WriteLine("min element :: "+getMin());
    removeLastElement();
    addElement(2);
    addElement(9);
    Console.WriteLine("Last element :: "+getLastElement());
    addElement(0);
    Console.WriteLine("min element :: "+getMin());
    removeLastElement();
    addElement(11);
    Console.WriteLine("min element :: "+getMin());
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // program to demonstrate customized data structure
    // which supports functions in O(1)

    let min;
    let stack = [];

    min = Number.MAX_VALUE

    // utility function for adding a new element
    function addElement(x)
    {
      if(stack.length == 0 || x < min)
      {
        min=x;
      }
      let pair = [x,min];
      stack.push(pair);
      document.write(x + " inserted successfully" + "</br>");
    }

    // utility function for returning last element of stack
    function getLastElement()
    {
      if (stack.length == 0)
      {
        document.write("UnderFlow Error" + "</br>");
        return -1;
      }
      else
      {
        return stack[stack.length - 1][0];
      }
    }

    // utility function for removing last element successfully;
    function removeLastElement()
    {

      if (stack.length == 0)
      {
        document.write("UnderFlow Error" + "</br>");
      }
      else if (stack.length > 1)
      {
        min=stack[stack.length - 2][1];
      }
      else
      {
        min=Number.MAX_VALUE;
      }
      stack.pop();
      document.write("removed successfully" + "</br>");
    }

    // utility function for returning min element till now;
    function getMin()
    {
      if (stack.length == 0)
      {
        document.write("UnderFlow Error" + "</br>");
        return -1;
      }
      return stack[stack.length - 1][1];
    }

    addElement(5);
    addElement(7);
    addElement(3);
    document.write("min element :: "+getMin() + "</br>");
    removeLastElement();
    addElement(2);
    addElement(9);
    document.write("Last element :: "+getLastElement() + "</br>");
    addElement(0);
    document.write("min element :: "+getMin() + "</br>");
    removeLastElement();
    addElement(11);
    document.write("min element :: "+getMin() + "</br>");

    // This code is contributed by rameshtravel07.
</script>
```

输出:

```
5 inserted successfully
7 inserted successfully
3 inserted successfully
min element  :: 3
removed successfully
2 inserted successfully
9 inserted successfully
Last element :: 9
0 inserted successfully
min element  :: 0
removed successfully
11 inserted successfully
min element  :: 2
```

**时间复杂度:**各功能在 O(1)
中运行本文由 [**曼德普·辛格**](https://github.com/msdeep14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。
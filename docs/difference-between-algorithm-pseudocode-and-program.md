# 算法、伪代码和程序的区别

> 原文:[https://www . geesforgeks . org/算法-伪代码和程序之间的差异/](https://www.geeksforgeeks.org/difference-between-algorithm-pseudocode-and-program/)

在这篇文章中，我们将讨论最常见的误解，即算法和伪代码是一回事。**不**，他们不是！
我们先来看看定义，
**算法:系统逻辑方法**这是一个定义明确的、循序渐进的程序，允许计算机解决问题。
**伪代码:**它是一个简单的编程代码的**版本，用简单的英语，在用特定的编程语言实现程序之前，用简短的短语为程序写代码。
**程序:**是遵循编程语言的所有规则为问题**编写的精确代码。**** 

**算法:**

一个[算法](https://www.geeksforgeeks.org/fundamentals-of-algorithms/)被用来以明确定义的步骤的形式提供特定问题的解决方案。每当你用计算机解决一个特定的问题时，导致解决方案的步骤应该正确地传达给计算机。在计算机上执行一个算法时，诸如加法和减法之类的几个运算被组合起来执行更复杂的数学运算。算法可以使用**自然语言、** [**流程图**](https://www.geeksforgeeks.org/an-introduction-to-flowcharts/) 等表达。
为了更好的理解，我们来看一个例子。作为一名程序员，我们都知道线性搜索程序。([线性搜索](https://www.geeksforgeeks.org/linear-search/) )
**线性搜索算法:**

```
1\. Start from the leftmost element of arr[] and 
one by one compare x with each element of arr[]. 
2\. If x matches with an element, return the index. 
3\. If x doesn’t match with any of elements, return -1\. 
```

在这里，我们可以看到如何用简单的英语解释线性搜索程序的步骤。

**伪代码:**
它是**可以用来表示程序的算法的方法之一**。它**不像任何编程语言那样有特定的语法**，因此不能在计算机上执行。用于编写伪代码的格式有几种，大多数都是从 **C、Lisp、FORTRAN 等语言中提取结构。**
许多时间算法都是用伪代码表示的，因为熟悉不同编程语言的程序员可以阅读和理解它们。伪代码允许您包括几个控制结构，如 **While，If-then-else，Repeat-third，for 和 case** ，它存在于许多高级语言中。
**注:**伪代码是**而不是**一种实际的编程语言。
**线性搜索伪代码:**

```
FUNCTION linearSearch(list, searchTerm):
     FOR index FROM 0 -> length(list):
       IF list[index] == searchTerm THEN
           RETURN index
       ENDIF
       ENDLOOP
           RETURN -1
END FUNCTION 
```

在这里，我们没有使用任何特定的编程语言，而是以更简单的形式编写了线性搜索的步骤，可以进一步修改为适当的程序。

**程序:**
程序是供计算机遵循的一组指令。机器不能直接读取程序，因为它只理解机器代码。但是你可以用计算机语言写东西，然后编译器或解释器可以让计算机理解它。
**线性搜索程序:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ code for linearly search x in arr[].  If x
// is present  then return its  location,  otherwise
// return -1
int search(int arr[], int n, int x)
{
    int i;
    for (i = 0; i < n; i++)
        if (arr[i] == x)
         return i;
    return -1;
}
```

## 蟒蛇 3

```
# Python3 code for linearly search x in arr.  If x
# is present  then return its  location,  otherwise
# return -1
def search( arr,  n,  x):
    for i in range(n):
        if (arr[i] == x):
            return i
    return -1
```

**算法 vs 伪代码 vs 程序:**

1.  算法被定义为为给定问题提供解决方案的定义明确的步骤序列，而伪代码是可以用来表示算法的方法之一。

2.  虽然算法通常是用自然语言或普通英语编写的，但伪代码是用类似于高级编程语言的格式编写的。另一方面，程序允许我们用特定的编程语言编写代码。

因此，如上所述，您可以清楚地看到算法是如何用来生成伪代码的，通过遵循编程语言的特定语法来创建程序代码，伪代码被进一步扩展。
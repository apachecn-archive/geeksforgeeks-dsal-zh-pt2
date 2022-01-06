# 如何在单个数组中高效实现 k 个栈？

> 原文:[https://www . geesforgeks . org/efficient-implement-k-stacks-single-array/](https://www.geeksforgeeks.org/efficiently-implement-k-stacks-single-array/)

我们已经讨论了单个阵列中 2 个堆栈的[空间高效实现](https://www.geeksforgeeks.org/implement-two-stacks-in-an-array/)。在这篇文章中，讨论了 k 堆栈的一般解决方案。以下是详细的问题陈述。

*创建一个代表 k 个栈的数据结构 kStacks。kStacks 的实现应该只使用一个数组，即 k 个栈应该使用相同的数组来存储元素。kStacks 必须支持以下功能。*

*push(int x，int sn)–>push x 到堆叠编号‘sn’其中 sn 从 0 到 k-1
pop(int sn)–>从堆叠编号‘sn’中弹出一个元素其中 sn 从 0 到 k-1*

**方法 1(将数组划分为 n/k 大小的槽)**
实现 k 个栈的一种简单方法是将数组划分为 k 个各为 n/k 大小的槽，并固定不同栈的槽，即使用 arr[0]对第一个栈使用 arr[n/k-1]，对 stack2 使用 arr[n/k]对 arr[2n/k-1]，其中 arr[]是要用于实现两个栈的数组，数组大小为 n

这种方法的问题是数组空间的使用效率低。即使 arr[]中有可用空间，堆栈推送操作也可能导致堆栈溢出。例如，假设 k 是 2，数组大小(n)是 6，我们将 3 个元素推到第一个堆栈，不将任何东西推到第二个堆栈。当我们将第四个元素推到第一个元素时，即使数组中还有 3 个元素的空间，也会有溢出。

**方法 2 (A 空间高效实现)**
想法是使用两个额外的数组来高效实现数组中的 k 个栈。这对于整数堆栈可能没有多大意义，但是堆栈项目可能很大，例如员工、学生等的堆栈，其中每个项目都有数百字节。对于如此大的堆栈，使用的额外空间相对较少，因为我们使用两个*整数*数组作为额外空间。

以下是使用的两个额外数组:
***1) top[]:*** 这是 k 大小的数组，在所有堆栈中存储 top 元素的索引。
***2) next[]:*** 它的大小为 n，存储数组 arr[]中项目的下一个项目的索引。这里 arr[]是存储 k 个堆栈的实际数组。
与 k 个栈一起，arr[]中的一个空闲槽栈也被维护。这个堆栈的顶部存储在变量“free”中。

top[]中的所有条目都初始化为-1，表示所有堆栈都是空的。下一个[i]的所有条目都被初始化为 i+1，因为所有插槽最初都是空闲的，并指向下一个插槽。空闲堆栈的顶部，“空闲”被初始化为 0。

以下是上述想法的实现。

## C++

```
// A C++ program to demonstrate implementation of k stacks in a single 
// array in time and space efficient way
#include<bits/stdc++.h>
using namespace std;

// A C++ class to represent k stacks in a single array of size n
class kStacks
{
    int *arr;   // Array of size n to store actual content to be stored in stacks
    int *top;   // Array of size k to store indexes of top elements of stacks
    int *next;  // Array of size n to store next entry in all stacks
                // and free list
    int n, k;
    int free; // To store beginning index of free list
public:
    //constructor to create k stacks in an array of size n
    kStacks(int k, int n);

    // A utility function to check if there is space available
    bool isFull()   {  return (free == -1);  }

    // To push an item in stack number 'sn' where sn is from 0 to k-1
    void push(int item, int sn);

    // To pop an from stack number 'sn' where sn is from 0 to k-1
    int pop(int sn);

    // To check whether stack number 'sn' is empty or not
    bool isEmpty(int sn)  {  return (top[sn] == -1); }
};

//constructor to create k stacks in an array of size n
kStacks::kStacks(int k1, int n1)
{
    // Initialize n and k, and allocate memory for all arrays
    k = k1, n = n1;
    arr = new int[n];
    top = new int[k];
    next = new int[n];

    // Initialize all stacks as empty
    for (int i = 0; i < k; i++)
        top[i] = -1;

    // Initialize all spaces as free
    free = 0;
    for (int i=0; i<n-1; i++)
        next[i] = i+1;
    next[n-1] = -1;  // -1 is used to indicate end of free list
}

// To push an item in stack number 'sn' where sn is from 0 to k-1
void kStacks::push(int item, int sn)
{
    // Overflow check
    if (isFull())
    {
        cout << "\nStack Overflow\n";
        return;
    }

    int i = free;      // Store index of first free slot

    // Update index of free slot to index of next slot in free list
    free = next[i];

    // Update next of top and then top for stack number 'sn'
    next[i] = top[sn];
    top[sn] = i;

    // Put the item in array
    arr[i] = item;
}

// To pop an from stack number 'sn' where sn is from 0 to k-1
int kStacks::pop(int sn)
{
    // Underflow check
    if (isEmpty(sn))
    {
         cout << "\nStack Underflow\n";
         return INT_MAX;
    }

    // Find index of top item in stack number 'sn'
    int i = top[sn];

    top[sn] = next[i];  // Change top to store next of previous top

    // Attach the previous top to the beginning of free list
    next[i] = free;
    free = i;

    // Return the previous top item
    return arr[i];
}

/* Driver program to test twStacks class */
int main()
{
    // Let us create 3 stacks in an array of size 10
    int k = 3, n = 10;
    kStacks ks(k, n);

    // Let us put some items in stack number 2
    ks.push(15, 2);
    ks.push(45, 2);

    // Let us put some items in stack number 1
    ks.push(17, 1);
    ks.push(49, 1);
    ks.push(39, 1);

    // Let us put some items in stack number 0
    ks.push(11, 0);
    ks.push(9, 0);
    ks.push(7, 0);

    cout << "Popped element from stack 2 is " << ks.pop(2) << endl;
    cout << "Popped element from stack 1 is " << ks.pop(1) << endl;
    cout << "Popped element from stack 0 is " << ks.pop(0) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate implementation of k stacks in a single 
// array in time and space efficient way

public class GFG 
{
    // A Java class to represent k stacks in a single array of size n
    static class KStack 
    {
        int arr[];   // Array of size n to store actual content to be stored in stacks
        int top[];   // Array of size k to store indexes of top elements of stacks
        int next[];  // Array of size n to store next entry in all stacks
                     // and free list
        int n, k;
        int free; // To store beginning index of free list

        //constructor to create k stacks in an array of size n
        KStack(int k1, int n1) 
        {
            // Initialize n and k, and allocate memory for all arrays
            k = k1;
            n = n1;
            arr = new int[n];
            top = new int[k];
            next = new int[n];

            // Initialize all stacks as empty
            for (int i = 0; i < k; i++)
                top[i] = -1;

            // Initialize all spaces as free
            free = 0;
            for (int i = 0; i < n - 1; i++)
                next[i] = i + 1;
            next[n - 1] = -1; // -1 is used to indicate end of free list
        }

        // A utility function to check if there is space available
        boolean isFull() 
        {
            return (free == -1);
        }

        // To push an item in stack number 'sn' where sn is from 0 to k-1
        void push(int item, int sn) 
        {
            // Overflow check
            if (isFull()) 
            {
                System.out.println("Stack Overflow");
                return;
            }

            int i = free; // Store index of first free slot

            // Update index of free slot to index of next slot in free list
            free = next[i];

            // Update next of top and then top for stack number 'sn'
            next[i] = top[sn];
            top[sn] = i;

            // Put the item in array
            arr[i] = item;
        }

        // To pop an from stack number 'sn' where sn is from 0 to k-1
        int pop(int sn) 
        {
            // Underflow check
            if (isEmpty(sn)) 
            {
                System.out.println("Stack Underflow");
                return Integer.MAX_VALUE;
            }

            // Find index of top item in stack number 'sn'
            int i = top[sn];

            top[sn] = next[i]; // Change top to store next of previous top

            // Attach the previous top to the beginning of free list
            next[i] = free;
            free = i;

            // Return the previous top item
            return arr[i];
        }

        // To check whether stack number 'sn' is empty or not
        boolean isEmpty(int sn) 
        {
            return (top[sn] == -1);
        }

    }

    // Driver program
    public static void main(String[] args) 
    {
        // Let us create 3 stacks in an array of size 10
        int k = 3, n = 10;

        KStack ks = new KStack(k, n);

        ks.push(15, 2);
        ks.push(45, 2);

        // Let us put some items in stack number 1
        ks.push(17, 1);
        ks.push(49, 1);
        ks.push(39, 1);

        // Let us put some items in stack number 0
        ks.push(11, 0);
        ks.push(9, 0);
        ks.push(7, 0);

        System.out.println("Popped element from stack 2 is " + ks.pop(2));
        System.out.println("Popped element from stack 1 is " + ks.pop(1));
        System.out.println("Popped element from stack 0 is " + ks.pop(0));
    }
}
// This code is Contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to demonstrate implementation 
# of k stacks in a single array in time and space 
# efficient way 
class KStacks:

    def __init__(self, k, n):
        self.k = k # Number of stacks.
        self.n = n # Total size of array holding 
                   # all the 'k' stacks.

        # Array which holds 'k' stacks.
        self.arr = [0] * self.n

        # All stacks are empty to begin with 
        # (-1 denotes stack is empty).
        self.top = [-1] * self.k

        # Top of the free stack.
        self.free = 0

        # Points to the next element in either
        # 1\. One of the 'k' stacks or,
        # 2\. The 'free' stack.
        self.next = [i + 1 for i in range(self.n)]
        self.next[self.n - 1] = -1

    # Check whether given stack is empty.
    def isEmpty(self, sn):
        return self.top[sn] == -1

    # Check whether there is space left for 
    # pushing new elements or not.
    def isFull(self):
        return self.free == -1

    # Push 'item' onto given stack number 'sn'.
    def push(self, item, sn):
        if self.isFull():
            print("Stack Overflow")
            return

        # Get the first free position 
        # to insert at.
        insert_at = self.free

        # Adjust the free position.
        self.free = self.next[self.free]

        # Insert the item at the free 
        # position we obtained above.
        self.arr[insert_at] = item

        # Adjust next to point to the old
        # top of stack element.
        self.next[insert_at] = self.top[sn]

        # Set the new top of the stack.
        self.top[sn] = insert_at

    # Pop item from given stack number 'sn'.
    def pop(self, sn):
        if self.isEmpty(sn):
            return None

        # Get the item at the top of the stack.
        top_of_stack = self.top[sn]

        # Set new top of stack.
        self.top[sn] = self.next[self.top[sn]]

        # Push the old top_of_stack to 
        # the 'free' stack.
        self.next[top_of_stack] = self.free
        self.free = top_of_stack

        return self.arr[top_of_stack]

    def printstack(self, sn):
        top_index = self.top[sn]
        while (top_index != -1):
            print(self.arr[top_index])
            top_index = self.next[top_index]

# Driver Code
if __name__ == "__main__":

    # Create 3 stacks using an 
    # array of size 10.
    kstacks = KStacks(3, 10)

    # Push some items onto stack number 2.
    kstacks.push(15, 2)
    kstacks.push(45, 2)

    # Push some items onto stack number 1.
    kstacks.push(17, 1)
    kstacks.push(49, 1)
    kstacks.push(39, 1)

    # Push some items onto stack number 0.
    kstacks.push(11, 0)
    kstacks.push(9, 0)
    kstacks.push(7, 0)

    print("Popped element from stack 2 is " + 
                         str(kstacks.pop(2)))
    print("Popped element from stack 1 is " + 
                         str(kstacks.pop(1)))
    print("Popped element from stack 0 is " + 
                         str(kstacks.pop(0)))

    kstacks.printstack(0)

# This code is contributed by Varun Patil
```

## C#

```
using System;

// C# program to demonstrate implementation of k stacks in a single  
// array in time and space efficient way 

public class GFG
{
    // A c# class to represent k stacks in a single array of size n 
    public class KStack
    {
        public int[] arr; // Array of size n to store actual content to be stored in stacks
        public int[] top; // Array of size k to store indexes of top elements of stacks
        public int[] next; // Array of size n to store next entry in all stacks
                     // and free list 
        public int n, k;
        public int free; // To store beginning index of free list

        //constructor to create k stacks in an array of size n 
        public KStack(int k1, int n1)
        {
            // Initialize n and k, and allocate memory for all arrays 
            k = k1;
            n = n1;
            arr = new int[n];
            top = new int[k];
            next = new int[n];

            // Initialize all stacks as empty 
            for (int i = 0; i < k; i++)
            {
                top[i] = -1;
            }

            // Initialize all spaces as free 
            free = 0;
            for (int i = 0; i < n - 1; i++)
            {
                next[i] = i + 1;
            }
            next[n - 1] = -1; // -1 is used to indicate end of free list
        }

        // A utility function to check if there is space available 
        public virtual bool Full
        {
            get
            {
                return (free == -1);
            }
        }

        // To push an item in stack number 'sn' where sn is from 0 to k-1 
        public virtual void push(int item, int sn)
        {
            // Overflow check 
            if (Full)
            {
                Console.WriteLine("Stack Overflow");
                return;
            }

            int i = free; // Store index of first free slot

            // Update index of free slot to index of next slot in free list 
            free = next[i];

            // Update next of top and then top for stack number 'sn' 
            next[i] = top[sn];
            top[sn] = i;

            // Put the item in array 
            arr[i] = item;
        }

        // To pop an from stack number 'sn' where sn is from 0 to k-1 
        public virtual int pop(int sn)
        {
            // Underflow check 
            if (isEmpty(sn))
            {
                Console.WriteLine("Stack Underflow");
                return int.MaxValue;
            }

            // Find index of top item in stack number 'sn' 
            int i = top[sn];

            top[sn] = next[i]; // Change top to store next of previous top

            // Attach the previous top to the beginning of free list 
            next[i] = free;
            free = i;

            // Return the previous top item 
            return arr[i];
        }

        // To check whether stack number 'sn' is empty or not 
        public virtual bool isEmpty(int sn)
        {
            return (top[sn] == -1);
        }

    }

    // Driver program 
    public static void Main(string[] args)
    {
        // Let us create 3 stacks in an array of size 10 
        int k = 3, n = 10;

        KStack ks = new KStack(k, n);

        ks.push(15, 2);
        ks.push(45, 2);

        // Let us put some items in stack number 1 
        ks.push(17, 1);
        ks.push(49, 1);
        ks.push(39, 1);

        // Let us put some items in stack number 0 
        ks.push(11, 0);
        ks.push(9, 0);
        ks.push(7, 0);

        Console.WriteLine("Popped element from stack 2 is " + ks.pop(2));
        Console.WriteLine("Popped element from stack 1 is " + ks.pop(1));
        Console.WriteLine("Popped element from stack 0 is " + ks.pop(0));
    }
}

// This code is contributed by Shrikant13
```

**Output:**

```
Popped element from stack 2 is 45
Popped element from stack 1 is 39
Popped element from stack 0 is 7
```

push()和 pop()操作的时间复杂度为 O(1)。

上述实现的最佳部分是，如果堆栈中有可用的插槽，则可以将项目推入任何堆栈中，即不会浪费空间。

本文由**沙欣**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论
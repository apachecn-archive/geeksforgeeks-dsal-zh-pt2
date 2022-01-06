# 使用 STL 设计前中后队列

> 原文:[https://www . geesforgeks . org/design-front-middle-back-queue-use-STL/](https://www.geeksforgeeks.org/design-front-middle-back-queue-using-stl/)

设计有效支持队列中以下操作的数据结构:

*   **推 __front(x):** 在队列的前面插入一个元素。
*   **push__middle(x):** 在队列中间插入元素。
*   **将 _ _ 推回(x):** 在队列的后面插入元素。
*   **pop__front()** 移除队列的前端元素并返回。如果队列为空，返回 **-1。**
*   **pop__middle():** 移除队列的中间元素并返回。如果队列为空，返回 **-1。**
*   **pop__back():** 移除队列的后元素并返回。如果队列为空，返回 **-1。**

**例:**

<figure class="table">

| 操作 | 长队 | 返回 |
| --- | --- | --- |
| 向前推 _ _ 个(4) | four | _ |
| 将 _ _ 推回(2) | 4, 2 | _ |
| 按压 _ _ 中间(1) | 4, 1, 2 | _ |
| pop_front() | 1, 2 | four |
| pop__middle() | Two | one |
| pop__front() | _ | Two |
| pop__front() | _ | -1 |

[**德格**](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/) **为主的方法:**这个问题可以用两个[德格](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)来解决。这个想法是使用两个 deq。队列后面的操作要在第二次去重结束时进行，中间的操作要在第一次去重结束时进行。按照以下步骤解决问题:

*   如果第一个德格的大小大于第二个德格的大小，则移除第一个德格的结束元素，并将其添加到第二个德格的前面。
*   如果第二个德格的大小超过第一个德格的大小 1，则移除第二个德格的前元素，并将其推到第一个德格的末尾。
*   如果第一个 de quee 的大小大于第二个 de quee，则从第一个 de quee 中移除后元素，并将其插入第二个 de quee 中。
*   **推 __front(x):** 使用[推 _ _ front()](https://www.geeksforgeeks.org/dequepush_front-c-stl/)在第一个德格的前面插入一个元素 x。
*   **推回(x):** 使用[推回()](https://www.geeksforgeeks.org/dequepush_back-c-stl/)在第二个元素末尾插入一个元素 x
*   **推 _ _ 中(x):** 使用推 _ 回()将元素 x 插入到第一个 deque 的末尾。
*   **pop_front():**使用 pop _ front()移除第一个德格的前元素，如果德格的大小大于 **0** 。
*   **pop_back():**使用 pop _ back()移除第二个德格的结束元素，如果德格的大小大于 **0** 。
*   **pop _ middle():**如果第一个 decue 的大小大于使用 pop_back()时的大小，则删除第一个 decue 的结束元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Create class Queue.
class Queue {

    // Initialize two deques
    deque<int> first, second;

    // Function to balance the size of
    // first ans second deque
    void equalizeSizedeque1deque2()
    {

        // If size of less than second
        if (first.size() <= second.size())
            return;

        // Insert the last element of
        // first deque into second deque
        second.push_front(first.back());

        // Pop the front element
        // of the deque
        first.pop_back();
    }

    // Function to balance the size of
    // second and first deque
    void equalizeSizedeque2deque1()
    {

        // if size of second deque deceed
        // the first deque by 1
        if (second.size() <= first.size() + 1)
            return;

        // Insert front element of second
        // deque into the first
        first.push_back(second.front());

        // Remove front element of
        // second deque
        second.pop_front();
    }

public:
    // Function to insert element
    // at front of queue
    void push__front(int val)
    {

        // Insert val into first deque
        first.push_front(val);

        // Balancing the size of second
        equalizeSizedeque1deque2();
    }

    // Function to insert val
    // into the middle of queue
    void push__middle(int val)
    {

        // Insert val into first deque
        first.push_back(val);

        // Balancing the size of
        // second deque
        equalizeSizedeque1deque2();
    }

    // Function to insert val
    // into back of queue
    void push__back(int val)
    {

        // Insert val into second deque
        second.push_back(val);

        // Balancing the size of
        // second deque
        equalizeSizedeque2deque1();
    }

    // Function to pop front
    // element from queue
    int pop__front()
    {

        // If first deque and second
        // deque is empty
        if (first.empty() && second.empty())
            return -1;

        int ans;

        // If the first deque
        // is empty
        if (first.empty()) {

            // Stores front element
            // of second deque
            ans = second.front();

            // Pop front element of
            // second deque
            second.pop_front();
        }
        else {

            // Stores front element
            // of first deque
            ans = first.front();

            // Pop front element of
            // first deque
            first.pop_front();

            // Balancing the size of first
            equalizeSizedeque2deque1();
        }
        return ans;
    }

    // Function to pop middle
    // element of queue
    int pop__middle()
    {

        // If both deques are empty
        if (first.empty() && second.empty())
            return -1;

        // Stores mid element
        // of queue
        int ans;

        // If size of both deque is equal
        if (first.size() == second.size()) {

            // Stores back element
            // of first deque
            ans = first.back();

            // Pop back element of
            // first deque
            first.pop_back();
        }
        else {

            // Stores front element
            // of second deque
            ans = second.front();

            // Pop front element
            // from second deque
            second.pop_front();
        }
        return ans;
    }

    // Function to remove mid
    // element from queue
    int pop__back()
    {

        // If both the deque are empty
        if (first.empty() && second.empty())
            return -1;

        // Stores back element from
        // second deque
        int ans = second.back();

        // Pop back element from
        // second deque
        second.pop_back();

        // Balancing the size of second
        equalizeSizedeque1deque2();
        return ans;
    }
};

// Driver code
int main()
{
    Queue q;
    q.push__front(1);
    q.push__back(2);
    q.push__middle(3);
    cout << q.pop__middle() << " ";
    cout << q.pop__back() << " ";
    cout << q.pop__front() << " ";
    return 0;
}
```

**Output:** 

```
3 2 1
```

**时间复杂度分析:**

<figure class="table">

| 向前推 _ _ | pop__front() | 向后推 _ _ | pop__back() | 按压 _ _ 中间(x) | pop__middle() |
| --- | --- | --- | --- | --- | --- |
| O(1) | O(1) | O(1) | O(1) | O(1) | O(1) |

[**列出**](https://www.geeksforgeeks.org/list-cpp-stl/) **为主的方法:**按照以下步骤解决问题:

*   **推 __front(x):** 使用[推 _ _ front()](https://www.geeksforgeeks.org/listpush_front-listpush_back-c-stl/)在列表前面插入一个元素 **x** 。
*   **推回(x):** 使用[推回()](https://www.geeksforgeeks.org/list-push_back-function-in-c-stl/)在第二个列表的末尾插入一个元素 **x**
*   **按 __middle(x):** 使用 [advance()](https://www.geeksforgeeks.org/stdadvance-in-cpp/) 遍历列表，然后使用 [insert()](https://www.geeksforgeeks.org/list-insert-in-c-stl/) 在列表的中间位置插入元素
*   **pop _ front():**使用 [pop_front()](https://www.geeksforgeeks.org/list-pop_front-function-in-c-stl/) 移除列表中大于 **0** 的前元素，否则返回 **-1** 。
*   **pop_back():**如果列表的大小大于 0，使用 pop _ back()移除列表的最后一个元素，否则返回 **-1** 。
*   **pop__middle():** 如果列表的大小大于 **0** ，则使用 [advance()](https://www.geeksforgeeks.org/stdadvance-in-cpp/) 迭代到列表的中间元素，然后使用 erase()在该位置擦除元素。否则，返回 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Create structure of queue
class Queue {

    list<int> l;

public:
    // Function to push element
    // at front of the queue
    void push__front(int val)
    {
        l.push_front(val);
    }

    // Function to push element
    // at middle of the queue
    void push__middle(int val)
    {

        auto itr = l.begin();

        // Traverse the list
        advance(itr, l.size() / 2);

        // Insert element into
        // middle of the list
        l.insert(itr, val);
    }

    // Function to insert element
    // at the back of the queue
    void push__back(int val)
    {
        l.push_back(val);
    }

    // Function to pop element from
    // front of the queue
    int pop__front()
    {

        // Stores front element
        // of queue
        int val = -1;
        if (l.size()) {
            val = l.front();
            l.pop_front();
        }
        return val;
    }

    // Function to pop middle element
    // of the queue
    int pop__middle()
    {
        int val = -1;
        if (l.size()) {
            auto itr = l.begin();

            // Traverse the list
            advance(itr, (l.size() - 1) / 2);
            val = *itr;

            // Remove mid element
            // from queue
            l.erase(itr);
        }
        return val;
    }

    // Function to pop end
    // element of the queue
    int pop__back()
    {

        // Stores back element
        // of the queue
        int val = -1;

        if (l.size()) {
            val = l.back();
            l.pop_back();
        }
        return val;
    }
};

// Drivers code
int main()
{
    Queue q;
    q.push__front(1);
    q.push__back(2);
    q.push__middle(3);
    cout << q.pop__middle() << " ";
    cout << q.pop__back() << " ";
    cout << q.pop__front() << " ";
    return 0;
}
```

**Output:** 

```
3 2 1 
```

**时间复杂度分析:**

<figure class="table">

| 向前推 _ _ | pop__front() | 向后推 _ _ | pop__back() | 按压 _ _ 中间(x) | pop__middle() |
| --- | --- | --- | --- | --- | --- |
| O(1) | O(1) | O(1) | O(1) | O(N) | O(N) |

[**双链表**](https://www.geeksforgeeks.org/doubly-linked-list/) **基于方法:**通过存储**头**和**最后一个**节点的地址，在不使用 STL 的情况下，使用[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)也可以解决这个问题。按照以下步骤解决问题:

*   **向前推 _ _ x:**
    *   分配存储数据值 **x** 的空间，并将地址存储在**当前节点**指针中
    *   通过链接**头节点**和**头- >下一个节点**之间的**当前节点**插入元素 **x**
    *   将容量增加一
*   **推 _ _ 回(x):**
    *   分配存储数据值 **x** 的空间，并将地址存储在**当前节点**指针中
    *   将**当前节点**链接到**最后一个节点**和**最后一个- >前一个**节点之间，插入元素 **x**
    *   将容量增加一
*   **推 _ _ 中间(x):**
    *   分配存储数据值 **x** 的空间，并将地址存储在**当前节点**指针中
    *   初始化类型节点的**温度**指针
    *   通过执行 **temp=temp- >下一个**当前容量的一半，到达双向链表的**中间元素**
    *   现在通过重新链接节点将元素 **x** 插入到**温度**和**温度- >之间**
    *   将**容量**增加 1
*   **pop__front()**
    *   如果尺寸的**容量**小于 1，则返回-1
    *   否则，通过重新链接节点，删除**头**和**头- >下一个**节点之间的第一个节点
    *   将**容量**减少 1
    *   已删除元素的返回值
*   **pop__back():**
    *   如果**容量**小于 **1** ，则返回 **-1**
    *   否则，通过重新链接节点，删除最后一个**节点和最后一个**->节点之间的结束节点****
    *   将**容量**减少**一**
    *   已删除元素的返回值
*   **pop__middle():**
    *   初始化类型节点的**温度指针**
    *   通过执行 **temp=temp- > nex** t 当前容量的一半，到达双向链表的中间元素
    *   现在通过重新链接节点来删除上一个的**温度- >和下一个**的**温度- >之间的温度节点**
    *   将**容量**减少 1
    *   已删除元素的返回值

</figure>

</figure>

</figure>
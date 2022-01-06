# 设计一个队列数据结构，得到 O(1)时间内的最小值或最大值

> 原文:[https://www . geesforgeks . org/design-a-queue-data-structure-to-get-最小值或最大值-in-o1-time/](https://www.geeksforgeeks.org/design-a-queue-data-structure-to-get-minimum-or-maximum-in-o1-time/)

**问题:**设计一个特殊队列的数据结构，支持以下操作:查询、去查询、getMin()或 getMax()，其中 getMin()操作耗时 0(1)。
**例:**

```
Let the data to be inserted in queue be -
4, 2, 1, 6

Operation     Queue       Output
push(4)         4           -
push(2)        4, 2         -
push(1)       4, 2, 1       -
getMin()      4, 2, 1       1
push(6)      4, 2, 1, 6     -
pop()         2, 1, 6       4
pop()          1, 6         2
pop()            6          1
getMin()         6          6

// Notice the getMin() function call
// It returns the minimum element 
// of all the values present in the queue
```

**方法:**思路是使用[双端队列](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)如果结构返回最小元素，按递增顺序存储，如果结构返回最大元素，按递减顺序存储。数据结构的操作定义如下:

调查

*   将元素插入队列结构。
*   如果德奎结构的大小为空，即德奎的大小为 0。然后，从后面插入元素。
*   否则，如果在 de quee 结构中有一些元素，那么从 de quee 弹出元素，直到 de quee 的后面大于当前元素，然后最后从后面插入元素。

从开始

*   如果队列的第一个元素等于队列的前一个元素，则同时从队列和队列中弹出元素。
*   否则，从队列的前面弹出元素，以保持元素的顺序。

**获得最小值**

返回 Deque 的前元素，得到队列当前元素的最小元素。
以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
import java.io.*;

class SpecialQueue {

    Queue<Integer> q;
    Deque<Integer> dq;

    public SpecialQueue(){
        q = new LinkedList<>();
        dq = new ArrayDeque<>();
    }

    void enque(int data){
          // remove all elements from
          // from deque which are greater
        // than the current element 'data'
        while(!dq.isEmpty() && dq.getLast() > data){
            dq.removeLast();
        }
          // If queue is empty then
          // while loop is skipped.
        dq.addLast(data);
        q.add(data);
    }

    void deque(){
          // If min element is present
          // at front of queue
        if(dq.getFirst() == q.peek()){
            dq.removeFirst();
        }
        q.remove();
    }

      // Method to get min element in Queue
    int getMin() throws Exception{
          // If queue is Empty, return Exception
        if(q.isEmpty())
            throw new Exception("Queue is Empty");
        else
            return dq.getFirst();
    }
      public static void main(String[] args) throws Exception {
        SpecialQueue arr = new SpecialQueue();
        arr.enque(1);
        arr.enque(2);
          arr.enque(4);
        System.out.println(arr.getMin());
        arr.deque();
        System.out.println(arr.getMin());
    }
}
```

## C++

```
// C++ implementation to design
// a queue data structure to get
// minimum element in O(1) time

#include <bits/stdc++.h>

using namespace std;

template <typename T>

// Structure of the queue
class MinMaxQueue {
public:

    // Queue to store the
    // element to maintain the
    // order of insertion
    queue<T> Q;

    // Doubly ended queue to
    // get the minimum element
    // in the O(1) time
    deque<T> D;

    // Function to push a element
    // into the queue
    void enque_element(T element)
    {
        // If there is no element
        // in the queue
        if (Q.size() == 0) {
            Q.push(element);
            D.push_back(element);
        }
        else {
            Q.push(element);

            // Pop the elements out
            // until the element at
            // back is greater than
            // current element
            while (!D.empty() &&
               D.back() > element) {
                D.pop_back();
            }
            D.push_back(element);
        }
    }

    // Function to pop the element
    // out from the queue
    void deque_element()
    {
        // Condition when the Minimum
        // element is the element at
        // the front of the Deque
        if (Q.front() == D.front()) {
            Q.pop();
            D.pop_front();
        }
        else {
            Q.pop();
        }
    }

    // Function to get the
    // minimum element from
    // the queue
    T getMin()
    {
        return D.front();
    }
};

// Driver Code
int main()
{
    MinMaxQueue<int> k;
    int example[3] = { 1, 2, 4 };

    // Loop to enque element
    for (int i = 0; i < 3; i++) {
        k.enque_element(example[i]);
    }
    cout << k.getMin() << "\n";
    k.deque_element();
    cout << k.getMin() << "\n";
}
```

## 蟒蛇 3

```
# Python 3 implementation to design
# a queue data structure to get
# minimum element in O(1) time
from collections import deque as dq

# class for the queue

class MinMaxQueue:

    def __init__(self):
        # Queue to store the
        # element to maintain the
        # order of insertion
        self.Q = dq([])

        # Doubly ended queue to
        # get the minimum element
        # in the O(1) time
        self.D = dq([])

    # Function to push a element
    # into the queue
    def enque_element(self, element):
        # If there is no element
        # in the queue
        if (len(self.Q) == 0):
            self.Q.append(element)
            self.D.append(element)

        else:
            self.Q.append(element)

            # Pop the elements out
            # until the element at
            # back is greater than
            # current element
            while (self.D and
                   self.D[-1] > element):
                self.D.pop()

            self.D.append(element)

    # Function to pop the element
    # out from the queue

    def deque_element(self,):
        # Condition when the Minimum
        # element is the element at
        # the front of the Deque
        if (self.Q[0] == self.D[0]):
            self.Q.popleft()
            self.D.popleft()

        else:
            self.Q.popleft()

    # Function to get the
    # minimum element from
    # the queue

    def getMin(self,):
        return self.D[0]

# Driver Code
if __name__ == '__main__':
    k = MinMaxQueue()
    example = [1, 2, 4]

    # Loop to enque element
    for i in range(3):
        k.enque_element(example[i])

    print(k.getMin())
    k.deque_element()
    print(k.getMin())
```

**Output:** 

```
1
2
```
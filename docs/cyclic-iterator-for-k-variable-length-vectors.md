# K 个可变长度向量的循环迭代器

> 原文:[https://www . geeksforgeeks . org/cyclic-iterator-for-k-变长向量/](https://www.geeksforgeeks.org/cyclic-iterator-for-k-variable-length-vectors/)

给定 **K** 个向量，任务是设计一个循环迭代器，以循环方式打印这些向量的元素。**例如:** v1 = {1，2，3}，v2 = {4，5，6}和 v3 = {7，8，9}那么输出应该是 **1，4，7，2，5，8，3，6 和 9** 。

**示例:**

> **输入:** v1 = {1，2}，v2 = {3，4，5}，v3 = { 6 }
> T3】输出: 1 3 6 2 4 5
> 
> **输入:** v1 = {1，2}，v2 = {3，4 }
> T3】输出: 1 3 2 4

**方法:**创建两个数组，一个存储每个向量的开始迭代器，另一个存储每个向量的结束迭代器。然后循环打印矢量的内容。因为向量可以是可变长度的，所以跳过所有元素已经打印的向量。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Class for the cyclic iterator
class Iterator {
public:
    Iterator(vector<int>& a1, vector<int>& a2,
             vector<int>& a3, vector<int>& a4, int k);
    int numOfVectors;
    int currIndex;

    // Vectors to store the starting and the
    // ending iterators for each of the vector
    vector<vector<int>::iterator> iStart;
    vector<vector<int>::iterator> iEnd;

    // Function that returns true if
    // there are elements left to print
    bool hasNext();

    // Function that returns the next
    // element in a cyclic manner
    int next();
};

// Function that returns true if
// there are elements left to print
bool Iterator::hasNext()
{

    // If iterator of any vector has not
    // reached the end then return true
    for (int i = 0; i < numOfVectors; i++) {
        if (iStart[i] != iEnd[i])
            return true;
    }
    return false;
}

// Function that returns the next
// element in a cyclic manner
int Iterator::next()
{
    int elem = 0;
    if (iStart[currIndex] != iEnd[currIndex]) {
        elem = *iStart[currIndex]++;
        currIndex = (currIndex + 1) % numOfVectors;
        return elem;
    }
    else {
        currIndex = (currIndex + 1) % numOfVectors;
        return next();
    }
    return elem;
}

// Initialise object of the Iterator class
Iterator::Iterator(vector<int>& a1, vector<int>& a2,
                   vector<int>& a3, vector<int>& a4, int k)
{
    numOfVectors = k;
    iStart.resize(numOfVectors);
    iEnd.resize(numOfVectors);

    // Store begin iterators
    iStart[0] = a1.begin();
    iStart[1] = a2.begin();
    iStart[2] = a3.begin();
    iStart[3] = a4.begin();

    // Store ending iterators
    iEnd[0] = a1.end();
    iEnd[1] = a2.end();
    iEnd[2] = a3.end();
    iEnd[3] = a4.end();

    // CurrIndex denotes the vector's index
    // whose element is to be printed next
    currIndex = 0;
}

// Function to print the elements in a cyclic manner
void iterateCyclic(vector<int>& a1, vector<int>& a2,
                   vector<int>& a3, vector<int>& a4, int k)
{

    // Initialise the iterator
    Iterator it(a1, a2, a3, a4, k);

    // Print all the element
    // in a cyclic fashion
    while (it.hasNext()) {
        cout << it.next() << " ";
    }
}

// Driver code
int main()
{
    // Initialize the vectors
    vector<int> a1;
    a1.push_back(1);
    a1.push_back(2);
    a1.push_back(3);

    vector<int> a2;
    a2.push_back(4);
    a2.push_back(5);
    a2.push_back(6);
    a2.push_back(7);

    vector<int> a3;
    a3.push_back(8);
    a3.push_back(9);

    vector<int> a4;
    a4.push_back(10);
    a4.push_back(11);

    // Print the elements in a cyclic fashion
    iterateCyclic(a1, a2, a3, a4, 4);

    return 0;
}
```

**Output:**

```
1 4 8 10 2 5 9 11 3 6 7

```
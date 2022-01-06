# 使用堆排序的词典排序

> 原文:[https://www . geeksforgeeks . org/词典-排序-使用-堆-排序/](https://www.geeksforgeeks.org/lexicographical-ordering-using-heap-sort/)

给定字符串数组**arr[]**。任务是使用[堆排序](https://www.geeksforgeeks.org/heap-sort/)按照[字典顺序](https://en.wikipedia.org/wiki/Lexicographical_order)对数组进行排序。
**举例:**

> **输入:** arr[] = {“香蕉”、“苹果”、“芒果”、“菠萝”、“橙子”}
> **输出:**苹果香蕉芒果橙子菠萝
> **输入:**arr[]= {“CAB”、“ACB”、“ABC”、“CBA”、“BAC”}
> **输出:** ABC、ACB、BAC、BCA、CAB、CBA

**方法:**基本思想是使用[堆排序](https://www.geeksforgeeks.org/heap-sort/)，这里[最小堆](https://www.geeksforgeeks.org/heap-data-structure/)被用来按照字典顺序打印。
以下是该方法的实施:

## C++

```
// C++ implementation to print
// the string in Lexicographical order
#include <iostream>
#include <string>
using namespace std;

// Used for index in heap
int x = -1;

// Predefining the heap array
string heap[1000];

// Defining formation of the heap
void heapForm(string k)
{
    x++;

    heap[x] = k;

    int child = x;

    string tmp;

    int index = x / 2;

    // Iterative heapiFy
    while (index >= 0) {

        // Just swapping if the element
        // is smaller than already
        // stored element
        if (heap[index] > heap[child]) {

            // Swapping the current index
            // with its child
            tmp = heap[index];
            heap[index] = heap[child];
            heap[child] = tmp;
            child = index;

            // Moving upward in the
            // heap
            index = index / 2;
        }
        else {
            break;
        }
    }
}

// Defining heap sort
void heapSort()
{
    int left1, right1;

    while (x >= 0) {
        string k;
        k = heap[0];

        // Taking output of
        // the minimum element
        cout << k << " ";

        // Set first element
        // as a last one
        heap[0] = heap[x];

        // Decrement of the
        // size of the string
        x = x - 1;

        string tmp;

        int index = 0;

        int length = x;

        // Initializing the left
        // and right index
        left1 = 1;

        right1 = left1 + 1;

        while (left1 <= length) {

            // Process of heap sort
            // If root element is
            // minimum than its both
            // of the child then break
            if (heap[index] <= heap[left1]
                && heap[index] <= heap[right1]) {
                break;
            }

            // Otherwise checking that
            // the child which one is
            // smaller, swap them with
            // parent element
            else {

                // Swapping
                if (heap[left1] < heap[right1]) {
                    tmp = heap[index];
                    heap[index] = heap[left1];
                    heap[left1] = tmp;
                    index = left1;
                }

                else {
                    tmp = heap[index];
                    heap[index] = heap[right1];
                    heap[right1] = tmp;
                    index = right1;
                }
            }

            // Changing the left index
            // and right index
            left1 = 2 * left1;
            right1 = left1 + 1;
        }
    }
}

// Utility function
void sort(string k[], int n)
{

    // To heapiFy
    for (int i = 0; i < n; i++) {
        heapForm(k[i]);
    }

    // Calling heap sort function
    heapSort();
}

// Driver Code
int main()
{
    string arr[] = { "banana", "orange", "apple",
                   "pineapple", "berries", "lichi" };

    int n = sizeof(arr) / sizeof(arr[0]);

    sort(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print
// the string in Lexicographical order
class GFG
{

// Used for index in heap
static int x = -1;

// Predefining the heap array
static String []heap = new String[1000];

// Defining formation of the heap
static void heapForm(String k)
{
    x++;

    heap[x] = k;

    int child = x;

    String tmp;

    int index = x / 2;

    // Iterative heapiFy
    while (index >= 0)
    {

        // Just swapping if the element
        // is smaller than already
        // stored element
        if (heap[index].compareTo(heap[child]) > 0)
        {

            // Swapping the current index
            // with its child
            tmp = heap[index];
            heap[index] = heap[child];
            heap[child] = tmp;
            child = index;

            // Moving upward in the
            // heap
            index = index / 2;
        }
        else
        {
            break;
        }
    }
}

// Defining heap sort
static void heapSort()
{
    int left1, right1;

    while (x >= 0)
    {
        String k;
        k = heap[0];

        // Taking output of
        // the minimum element
        System.out.print(k + " ");

        // Set first element
        // as a last one
        heap[0] = heap[x];

        // Decrement of the
        // size of the string
        x = x - 1;

        String tmp;

        int index = 0;

        int length = x;

        // Initializing the left
        // and right index
        left1 = 1;

        right1 = left1 + 1;

        while (left1 <= length)
        {

            // Process of heap sort
            // If root element is
            // minimum than its both
            // of the child then break
            if (heap[index].compareTo(heap[left1]) <= 0 &&
                heap[index].compareTo(heap[right1]) <= 0)
            {
                break;
            }

            // Otherwise checking that
            // the child which one is
            // smaller, swap them with
            // parent element
            else
            {

                // Swapping
                if (heap[left1].compareTo(heap[right1])< 0)
                {
                    tmp = heap[index];
                    heap[index] = heap[left1];
                    heap[left1] = tmp;
                    index = left1;
                }

                else
                {
                    tmp = heap[index];
                    heap[index] = heap[right1];
                    heap[right1] = tmp;
                    index = right1;
                }
            }

            // Changing the left index
            // and right index
            left1 = 2 * left1;
            right1 = left1 + 1;
        }
    }
}

// Utility function
static void sort(String k[], int n)
{

    // To heapiFy
    for (int i = 0; i < n; i++)
    {
        heapForm(k[i]);
    }

    // Calling heap sort function
    heapSort();
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = {"banana", "orange", "apple",
                    "pineapple", "berries", "lichi" };

    int n = arr.length;

    sort(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to print
# the string in Lexicographical order

# Used for index in heap
x = -1;

# Predefining the heap array
heap = [0] * 1000;

# Defining formation of the heap
def heapForm(k):
    global x;
    x += 1;

    heap[x] = k;

    child = x;

    index = x // 2;

    # Iterative heapiFy
    while (index >= 0):

        # Just swapping if the element
        # is smaller than already
        # stored element
        if (heap[index] > heap[child]):

            # Swapping the current index
            # with its child
            tmp = heap[index];
            heap[index] = heap[child];
            heap[child] = tmp;
            child = index;

            # Moving upward in the
            # heap
            index = index // 2;

        else:
            break;

# Defining heap sort
def heapSort():
    global x;
    while (x >= 0):
        k = heap[0];

        # Taking output of
        # the minimum element
        print(k, end = " ");

        # Set first element
        # as a last one
        heap[0] = heap[x];

        # Decrement of the
        # size of the string
        x = x - 1;

        tmp = -1;

        index = 0;

        length = x;

        # Initializing the left
        # and right index
        left1 = 1;

        right1 = left1 + 1;

        while (left1 <= length):

            # Process of heap sort
            # If root element is
            # minimum than its both
            # of the child then break
            if (heap[index] <= heap[left1] and
                heap[index] <= heap[right1]):
                break;

            # Otherwise checking that
            # the child which one is
            # smaller, swap them with
            # parent element
            else:

                # Swapping
                if (heap[left1] < heap[right1]):
                    tmp = heap[index];
                    heap[index] = heap[left1];
                    heap[left1] = tmp;
                    index = left1;

                else:
                    tmp = heap[index];
                    heap[index] = heap[right1];
                    heap[right1] = tmp;
                    index = right1;

            # Changing the left index
            # and right index
            left1 = 2 * left1;
            right1 = left1 + 1;

# Utility function
def sort(k, n):

    # To heapiFy
    for i in range(n):
        heapForm(k[i]);

    # Calling heap sort function
    heapSort();

# Driver Code
if __name__ == '__main__':
    arr = ["banana", "orange", "apple",
           "pineapple", "berries", "lichi"];

    n = len(arr);

    sort(arr, n);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation to print
// the string in Lexicographical order
using System;

class GFG
{

// Used for index in heap
static int x = -1;

// Predefining the heap array
static String []heap = new String[1000];

// Defining formation of the heap
static void heapForm(String k)
{
    x++;

    heap[x] = k;

    int child = x;

    String tmp;

    int index = x / 2;

    // Iterative heapiFy
    while (index >= 0)
    {

        // Just swapping if the element
        // is smaller than already
        // stored element
        if (heap[index].CompareTo(heap[child]) > 0)
        {

            // Swapping the current index
            // with its child
            tmp = heap[index];
            heap[index] = heap[child];
            heap[child] = tmp;
            child = index;

            // Moving upward in the
            // heap
            index = index / 2;
        }
        else
        {
            break;
        }
    }
}

// Defining heap sort
static void heapSort()
{
    int left1, right1;

    while (x >= 0)
    {
        String k;
        k = heap[0];

        // Taking output of
        // the minimum element
        Console.Write(k + " ");

        // Set first element
        // as a last one
        heap[0] = heap[x];

        // Decrement of the
        // size of the string
        x = x - 1;

        String tmp;

        int index = 0;

        int length = x;

        // Initializing the left
        // and right index
        left1 = 1;

        right1 = left1 + 1;

        while (left1 <= length)
        {

            // Process of heap sort
            // If root element is
            // minimum than its both
            // of the child then break
            if (heap[index].CompareTo(heap[left1]) <= 0 &&
                heap[index].CompareTo(heap[right1]) <= 0)
            {
                break;
            }

            // Otherwise checking that the child
            // which one is smaller, swap them with
            // parent element
            else
            {

                // Swapping
                if (heap[left1].CompareTo(heap[right1]) < 0)
                {
                    tmp = heap[index];
                    heap[index] = heap[left1];
                    heap[left1] = tmp;
                    index = left1;
                }

                else
                {
                    tmp = heap[index];
                    heap[index] = heap[right1];
                    heap[right1] = tmp;
                    index = right1;
                }
            }

            // Changing the left index
            // and right index
            left1 = 2 * left1;
            right1 = left1 + 1;
        }
    }
}

// Utility function
static void sort(String []k, int n)
{

    // To heapiFy
    for (int i = 0; i < n; i++)
    {
        heapForm(k[i]);
    }

    // Calling heap sort function
    heapSort();
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = {"banana", "orange", "apple",
                    "pineapple", "berries", "lichi" };

    int n = arr.Length;

    sort(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
apple banana berries lichi orange pineapple
```